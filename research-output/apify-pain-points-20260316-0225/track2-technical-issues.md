# Track 2: Apify Technical Issues, Platform Bugs, and Developer Friction

## Summary

- **RequestQueue race conditions**: Both JS and Python Crawlee have critical bugs where requests are marked handled without firing requestHandler under high concurrency, or the queue softlocks when consuming retried requests ([crawlee #3427](https://github.com/apify/crawlee/issues/3427), [crawlee-python #1598](https://github.com/apify/crawlee-python/issues/1598))
- **Dataset data loss**: `push_data()` succeeds silently but `get_data()` returns only a subset of items due to storage buffering bugs in concurrent processing -- fixed in crawlee-python 1.2.x but was a high-severity data integrity issue ([crawlee-python #1621](https://github.com/apify/crawlee-python/issues/1621))
- **MemoryStorage ENOENT errors**: Random `isTaskReadyFunction failed` crashes when request queue JSON files go missing, affecting both PuppeteerCrawler and PlaywrightCrawler; open since Sep 2025 with no fix ([crawlee #3156](https://github.com/apify/crawlee/issues/3156))
- **Memory leaks and OOM**: Python crawlee consumes ~1.7 GB just for 1000 httpx sessions with large proxy pools; Kubernetes deployments get OOM-killed because autoscaler can't detect actual memory usage in containerized environments ([crawlee-python #895](https://github.com/apify/crawlee-python/issues/895), [#1535](https://github.com/apify/crawlee-python/issues/1535))
- **v4 breaking changes**: AdaptivePlaywrightCrawler completely broken (processes zero requests), skipNavigation with CheerioCrawler crashes, incompatible ErrorHandler types ([crawlee #3447](https://github.com/apify/crawlee/issues/3447), [#3304](https://github.com/apify/crawlee/issues/3304), [#3424](https://github.com/apify/crawlee/issues/3424))
- **CLI friction**: `apify create` throws ECONNRESET errors, CLI fails with Node 22/24 + pnpm, `apify run` silently modifies INPUT.json, local runs succeed but platform deploys fail with cryptic errors ([apify-cli #924](https://github.com/apify/apify-cli/issues/924), [#941](https://github.com/apify/apify-cli/issues/941), [#1035](https://github.com/apify/apify-cli/issues/1035), [#866](https://github.com/apify/apify-cli/issues/866))
- **Make.com integration problems**: 10-second webhook timeout causes Actor runs to fail silently, "Get dataset items" returns empty when run asynchronously, JSON validation errors on dynamic inputs, Watch Actor module fails via HTTP ([Make community posts](https://community.make.com/t/run-an-actor-module-stops-suddenly/63953))
- **`forefront` option broken**: Adding requests with `forefront: true` to MemoryStorage RequestQueue doesn't actually prioritize them; confirmed by maintainers as a design flaw in batching ([crawlee #2669](https://github.com/apify/crawlee/issues/2669))
- **Shared RequestQueue bugs**: `maxRequestsPerCrawl` doesn't work when sharing a RequestManager, and `purgeRequestQueue` doesn't actually purge the default queue ([crawlee #3330](https://github.com/apify/crawlee/issues/3330), [#3367](https://github.com/apify/crawlee/issues/3367))
- **n8n + Apify**: Complex integration friction with duplicate scraping results, rate limit errors, and data nesting mismatches when building multi-step workflows ([n8n #16402](https://github.com/n8n-io/n8n/issues/16402))
- **Startup performance**: Importing crawlee + apify SDK adds 900ms+ to Node.js startup; Cheerio dependency pulled in even when unused ([crawlee #3212](https://github.com/apify/crawlee/issues/3212))
- **Python SDK API mismatch**: `browser_new_context_options` passed to wrong Playwright method (`launch_persistent_context` instead of `new_context`), causing TypeError on valid options like `storage_state` ([crawlee-python #1784](https://github.com/apify/crawlee-python/issues/1784))
- **Timeout handling**: Multiple discussions about confusing timeout behavior -- timeouts in failed request handlers can kill the entire crawler; separate retry limits for proxy vs request errors are poorly documented ([crawlee discussions #2428](https://github.com/apify/crawlee/discussions/2428), [#2254](https://github.com/apify/crawlee/discussions/2254))
- **Flaky test infrastructure**: Multiple crawlee-python tests marked as flaky (`test_autoscales`, `test_keep_alive`, `test_adaptive_context_query_selector_parsel`, `test_new_page_with_each_plugin`), suggesting underlying instability ([crawlee-python #1649-1660](https://github.com/apify/crawlee-python/issues/1649))

## Full Findings

### 1. RequestQueue Race Conditions & Softlocks

**crawlee #3427 (Open, Feb 2026)**: Under high concurrency (12+ concurrent), `PlaywrightCrawler` marks requests as "Handled" (State 3) without ever executing the `requestHandler`. The user built a detailed bridge system proving requests transition to handled state in the queue statistics while the handler Promise never resolves. Maintainers could not reproduce. When the user switched to `RequestQueueV1` as suggested workaround, they hit even more ENOENT errors with missing JSON files.

Source: https://github.com/apify/crawlee/issues/3427

**crawlee-python #1598 (Open, Dec 2025)**: `AutoscaledPool` can spin up unlimited tasks when RequestQueue has one in-progress request. `not RequestManager.is_empty` does not imply `__is_task_ready`, but the code assumes it does. The root cause: `is_empty` and `is_finished` got merged into a single method, and in-progress requests aren't accounted for. Particularly bad on macOS where it can consume 100% CPU. Collaborators confirmed: "the fact that we don't distinguish `is_empty` from `is_finished` in the request queue client sounds like something that could bite us later."

Source: https://github.com/apify/crawlee-python/issues/1598

### 2. Dataset Data Loss (Storage Buffering Bug)

**crawlee-python #1621 (Closed/Fixed, Dec 2025)**: `push_data()` in PlaywrightCrawler succeeds for all items but `get_data()` returns only ~50% of pushed items. No errors logged. Non-deterministic which items survive. Bug only manifests during concurrent/batch processing; single-URL processing works perfectly. Root cause: storage buffering mechanism (introduced to prevent partial results from failed requests) drops data from success handlers. All query methods affected (`get_data()`, `list_items()`, `iterate_items()`). Polling up to 10+ seconds doesn't help. Fixed in crawlee 1.2.x pre-release.

Impact: Silent data loss in production crawls with no warnings.

Source: https://github.com/apify/crawlee-python/issues/1621

### 3. MemoryStorage ENOENT / isTaskReadyFunction Failures

**crawlee #3156 (Open, Sep 2025)**: Random `ENOENT: no such file or directory` errors when accessing request queue JSON files. Manifests as `PuppeteerCrawler:AutoscaledPool: isTaskReadyFunction failed`. After retry, request queue reports "does not exist." Multiple users confirm this happens randomly with both PuppeteerCrawler and PlaywrightCrawler + Camoufox. Related to earlier issues #1951 and #1792. No fix available; users asked about alternative storage from PR #1901. Follow-up comment in Oct 2025 asking for timeline -- no response from maintainers.

Source: https://github.com/apify/crawlee/issues/3156

This same ENOENT pattern also appears in issue #3427 when users try `RequestQueueV1` as a workaround, showing widespread ENOENT errors across the storage layer.

### 4. Memory Issues & OOM in Python Crawlee

**crawlee-python #895 (Closed, Jan 2025)**: 1000 `httpx.AsyncClient` instances consume ~1.7 GB RAM. With large proxy pools (e.g., Apify RESIDENTIAL), each session gets its own HTTP client. Default `max_pool_size` of 1000 means the crawler's baseline memory is 2+ GB before any actual scraping. Collaborator confirmed: "for an HTTP crawler with default configuration, this memory consumption is very high. For users, this will really look like there's a terrible memory leak."

Source: https://github.com/apify/crawlee-python/issues/895

**crawlee-python #1535 (Open, Nov 2025)**: Kubernetes pods OOM-killed because crawlee increases desired concurrency continuously. Memory/CPU metrics show 0.0 because the autoscaler's metrics represent "overutilization ratio" not actual usage, confusing users. The autoscaler cannot detect actual memory usage in containerized environments correctly, defeating the purpose of automatic scaling.

Source: https://github.com/apify/crawlee-python/issues/1535

**crawlee #2074 (Closed, Sep 2023, long-standing)**: `SDK_SESSION_POOL_STATE.json` grows infinitely on crawler reruns, appending sessions and never purging. Can cause memory leak in long-running scenarios.

Source: https://github.com/apify/crawlee/issues/2074

### 5. Crawlee v4 Breaking Changes

**crawlee #3447 (Open, Feb 2026)**: `AdaptivePlaywrightCrawler` doesn't process any requests at all in v4. Complete regression -- the crawler starts and finishes immediately without handling any URLs.

Source: https://github.com/apify/crawlee/issues/3447

**crawlee #3304 (Open, Dec 2025)**: `skipNavigation` with `CheerioCrawler` crashes in v4. The `ContextPipeline` validation Proxy on `CrawlingContext` and `Request` throws errors when accessing `contentType` and `loadedUrl` properties that don't exist with `skipNavigation`. Double crash: first from `parseContent`, then from Shapeshift validation during error handling, terminating the crawler.

Source: https://github.com/apify/crawlee/issues/3304

**crawlee #3424 (Open, Feb 2026)**: `ErrorHandler` context type is incompatible in v4. Code that compiles in v3 throws type errors in v4. The expected argument type is unclear, and it's not clear if the type is explicitly exported.

Source: https://github.com/apify/crawlee/issues/3424

**crawlee #3420 (Open, Feb 2026)**: `extendContext` doesn't affect `pre/postNavigationHooks` contexts due to calling order in the context pipeline. At minimum, needs documentation.

Source: https://github.com/apify/crawlee/issues/3420

### 6. CLI Developer Experience Issues

**apify-cli #941 (Open, Oct 2025)**: CLI fails with Node.js v22.20.0+ and pnpm: `Cannot read properties of undefined (reading 'runtimeShorthand')`. Error occurs on both `apify run` and `apify push`. Maintainers acknowledged it's "an error in an error" -- the CLI incorrectly reports "No Node.js detected" and then the error handler itself crashes. Also reported with Node 24 on Windows.

Source: https://github.com/apify/apify-cli/issues/941

**apify-cli #924 (Open, Sep 2025)**: `apify create` throws ECONNRESET errors when trying to fetch the template list from server. No workaround provided. No comments from maintainers.

Source: https://github.com/apify/apify-cli/issues/924

**apify-cli #1035 (Open, Mar 2026)**: `apify run` modifies INPUT.json every time it runs -- injecting default values from the input schema, then attempting to restore (imperfectly). Users report pasted content gets reverted. Maintainer acknowledged: "the restore mechanism isn't bulletproof."

Source: https://github.com/apify/apify-cli/issues/1035

**apify-cli #866 (Open, Jul 2025)**: CLI locally runs a project that won't work on the platform. Missing `npm start` script in `package.json` doesn't cause any error locally (`apify run` infers how to start), but the platform deploy fails with cryptic Docker error and no useful logs.

Source: https://github.com/apify/apify-cli/issues/866

**apify-cli #886 (Open, Aug 2025)**: `apify push` errors with "Actor with identifier is already on the platform and was modified there since modified locally" after any change in the Apify Console, requiring `--force` flag. No ability to merge/diff changes.

Source: https://github.com/apify/apify-cli/issues/886

### 7. Make.com / Integromat Integration Issues

**Webhook Timeout (10s limit)**: Make.com has a 10-second timeout for webhook responses. Running Apify Actors synchronously in Make routinely exceeds this, causing 500 errors, incomplete runs, or scenario termination. Official workaround: run asynchronously, add "Wait for Actor to finish" module, then retrieve results -- but this adds complexity.

Source: https://help.apify.com/en/articles/11169468-troubleshooting-webhook-timeouts-when-running-actors-in-make

**"Run an Actor" stops processing**: Module stops after ~10 scrapes despite configured limits, with no error logs. Root cause traced to actor-level issues, but the lack of error feedback makes debugging extremely difficult.

Source: https://community.make.com/t/run-an-actor-module-stops-suddenly/63953

**"Get dataset items" returns empty**: When Run Actor module is configured asynchronously, the subsequent Get Dataset Items call executes before the actor finishes, returning empty data. Users must also use the correct `defaultDatasetId` from storage output.

Source: https://community.make.com/t/apify-module-get-dataset-items-returns-empty/37980

**JSON validation errors on dynamic inputs**: Mapping dynamic values (e.g., from Monday.com) into Apify Actor JSON input fields causes `validateInputJSON` errors even when the JSON is structurally correct. Users must pre-validate JSON with external tools.

Source: https://community.make.com/t/error-creating-an-apify-actor-run-module/57220

**Watch Actor module via HTTP**: Requires specific structured payload matching Apify's expected format -- not just a simple POST to the webhook URL. Poorly documented.

Source: https://community.make.com/t/issue-triggering-apify-watch-actor-module-via-http/57705

**Reddit: Make.com dynamic URL mapping**: User reported losing hours trying to pass dynamic URLs from Monday.com into Apify's `startUrls` JSON input. Error: "Items in input.startUrls at positions [0] do not contain valid URLs." The mapping UI produces values that fail Apify's JSON validation.

Source: https://www.reddit.com/r/Integromat/comments/1kj9say/makecom_apify_actor_json_input_not_working_with/

### 8. n8n Integration Issues

**n8n #16402 (Closed, Jun 2025)**: Comprehensive report of Apify + n8n friction: (1) Apify scraper returns duplicate results for unique inputs despite correct loop configuration, (2) "Payment required" / rate limit errors under webhook-triggered loads, (3) data structure mismatches where fields are nested under `item.json.data` vs top-level. n8n team said "I can't see anything that looks like a bug with n8n" and directed user to Apify support.

Source: https://github.com/n8n-io/n8n/issues/16402

### 9. forefront Option Broken in MemoryStorage

**crawlee #2669 (Closed, Sep 2024)**: `forefront: true` on `addRequests` doesn't actually prioritize requests in MemoryStorage. Two confirmed root causes: (1) `listHead` doesn't consider negative `orderNo` values used to encode forefront, (2) batching reads 25 requests at a time and doesn't incorporate newly-added forefront requests into the current batch. Workaround: use `Actor.init()`/`Actor.exit()` to force API-based storage where forefront works. Still broken for local/MemoryStorage use.

Source: https://github.com/apify/crawlee/issues/2669

### 10. Shared RequestManager / Queue Issues

**crawlee #3330 (Open, Jan 2026)**: `maxRequestsPerCrawl` doesn't work when sharing a `RequestManager` instance between crawlers. Second crawler counts handled requests from the first crawler's run, effectively skipping its own limit. Python version handles this differently via the `Statistics` class.

Source: https://github.com/apify/crawlee/issues/3330

**crawlee #3367 (Open, Jan 2026)**: `purgeRequestQueue` option doesn't actually purge the default `RequestQueue`. Second crawler won't process URLs already handled by the first. Workaround: manually `RequestQueue.open()` then `queue.drop()` before second run.

Source: https://github.com/apify/crawlee/issues/3367

### 11. TypeScript / Build Issues

**crawlee #2279 (Closed, Jan 2024)**: The `crawlee` metapackage used `^` for internal `@crawlee/` dependencies, causing npm to install newer incompatible versions. Combined with requiring TypeScript 5.3+ (without documenting this), users got 140+ TypeScript errors from `.d.ts` files. Fixed by pinning internal dependencies in v3.5.3. Workaround: `skipLibCheck` in tsconfig, or install `@crawlee/` packages directly.

Source: https://github.com/apify/crawlee/issues/2279

### 12. Session & Proxy Handling

**crawlee #2028 (Closed, Aug 2023)**: `retryOnBlocked` with proxy session rotation terminates the entire crawler when max session rotations are exceeded, instead of sending the request to `failedRequestHandler`. The `SessionError` handling conflated proxy errors with blocking detection.

Source: https://github.com/apify/crawlee/issues/2028

### 13. Startup Performance

**crawlee #3212 (Open, Oct 2025)**: Importing `crawlee` + `apify` SDK adds 900ms+ to Node.js startup on a 512MB Actor. Even importing just `@crawlee/cheerio` costs 550ms. Cheerio is pulled in even for `HttpCrawler` that only needs JSON parsing. The team is exploring dynamic imports and bundle optimization but noted: "I don't see many opportunities to reduce dependencies."

Source: https://github.com/apify/crawlee/issues/3212

### 14. Python SDK API Surface Issues

**crawlee-python #1784 (Open, Mar 2026)**: `browser_new_context_options` parameter is documented as accepting Playwright `browser.new_context()` kwargs, but the code passes them to `launch_persistent_context()` instead, which has a different parameter set. Using `storage_state` (a valid `new_context` option) causes a TypeError. Workaround: set `use_incognito_pages=True`.

Source: https://github.com/apify/crawlee-python/issues/1784

**Flaky tests**: Multiple crawlee-python tests are explicitly tracked as flaky: `test_autoscales` (#1655), `test_keep_alive` (#1649), `test_adaptive_context_query_selector_parsel` (#1650), `test_new_page_with_each_plugin` (#1660). These suggest underlying instability in the autoscaling and browser pool subsystems.

Sources: https://github.com/apify/crawlee-python/issues/1649 through #1660

### 15. Platform Limits (Documented)

Key constraints that affect developers:
- Concurrent runs: 25 (Free), 32 (Starter), 128 (Scale)
- Max memory per run: 8 GB (Free), 32 GB (Starter)
- Build timeout: 1,800 seconds
- Max log size: ~10 MB
- Dataset columns (tabular): 2,000 max
- Actors per user: 100
- Webhooks per user: 100
- API rate limiting returns 429 with no specific documented rate numbers

Source: https://docs.apify.com/platform/limits

### 16. Third-Party Integration Breakage

**agno #3513 (Closed, Jun 2025)**: Agno AI framework's Apify integration broke between versions -- `ApifyTools` stopped registering actors properly, passing string actor IDs where Callables were expected. Fixed in agno 1.6.0, but illustrates fragility of third-party integrations.

Source: https://github.com/agno-agi/agno/issues/3513

## Execution Log

| # | Action | Tool | URL/Target | Result | Reasoning |
|---|--------|------|------------|--------|-----------|
| 1 | Fetch crawlee-python #1621 | gh CLI | apify/crawlee-python/issues/1621 | Dataset race condition - detailed reproduction, fixed in 1.2.x | Specific issue from brief |
| 2 | Fetch crawlee-python #1598 | gh CLI | apify/crawlee-python/issues/1598 | RequestQueue softlock - open, design flaw confirmed | Specific issue from brief |
| 3 | Fetch crawlee #2669 | gh CLI | apify/crawlee/issues/2669 | forefront broken in MemoryStorage, closed with workaround | Specific issue from brief |
| 4 | Fetch crawlee #3156 | gh CLI | apify/crawlee/issues/3156 | ENOENT errors, open, no fix | Specific issue from brief |
| 5 | Fetch crawlee #2279 | gh CLI | apify/crawlee/issues/2279 | TS version mismatch, fixed in 3.5.3 | Specific issue from brief |
| 6 | Fetch n8n #16402 | gh CLI | n8n-io/n8n/issues/16402 | Apify integration friction, closed as n8n-side | Specific issue from brief |
| 7 | List open crawlee issues | gh CLI | apify/crawlee | 30 issues - found #3427, #3447, #3330, #3304, #3367, #3212 | Broad discovery |
| 8 | List open crawlee-python issues | gh CLI | apify/crawlee-python | 30 issues - found #1784, #1535, flaky tests | Broad discovery |
| 9 | List open apify-cli issues | gh CLI | apify/apify-cli | 20 issues - found #941, #924, #886, #866, #1035 | Broad discovery |
| 10 | Search StackOverflow/Apify | WebSearch | stackoverflow apify crawlee | Found timeout discussions, no direct SO questions | Looking for SO signal |
| 11 | Fetch crawlee #3427 | gh CLI | apify/crawlee/issues/3427 | Race condition - requests handled without handler, open | Follow-up from listing |
| 12 | Fetch crawlee #3447 | gh CLI | apify/crawlee/issues/3447 | AdaptivePlaywrightCrawler broken in v4 | Follow-up from listing |
| 13 | Fetch crawlee #3330 | gh CLI | apify/crawlee/issues/3330 | maxRequestsPerCrawl broken with shared queue | Follow-up from listing |
| 14 | Fetch crawlee #3304 | gh CLI | apify/crawlee/issues/3304 | skipNavigation crashes in v4 | Follow-up from listing |
| 15 | Fetch crawlee #3367 | gh CLI | apify/crawlee/issues/3367 | purgeRequestQueue doesn't work | Follow-up from listing |
| 16 | Fetch apify-cli #941 | gh CLI | apify/apify-cli/issues/941 | CLI crash with Node 22+ pnpm | Follow-up from listing |
| 17 | Search Make.com Apify issues | WebSearch | Make.com Apify integration | Found 6 Make community threads | Integration pain points |
| 18 | Fetch Make community posts | WebFetch | community.make.com (3 threads) | Timeout, empty datasets, JSON validation errors | Detail on Make issues |
| 19 | Search Apify community bugs | WebSearch | apify community bugs | Found crawlee #2028, #2074 | Cross-reference |
| 20 | Fetch crawlee #2074 | gh CLI | apify/crawlee/issues/2074 | Session pool growing infinitely | Memory/storage issues |
| 21 | Fetch crawlee #2028 | gh CLI | apify/crawlee/issues/2028 | retryOnBlocked terminates crawler | Session handling |
| 22 | Fetch apify-cli #924, #886 | gh CLI | apify/apify-cli | ECONNRESET, push conflicts | CLI issues |
| 23 | Fetch Reddit post | curl | reddit.com/r/Integromat | Make + Apify JSON input mapping friction | Reddit signal |
| 24 | Search memory leaks | WebSearch | apify crawlee memory leak | Found #895, #1535 | Memory issues |
| 25 | Fetch crawlee-python #895 | gh CLI | apify/crawlee-python/issues/895 | 1.7GB RAM for proxy pools | Memory analysis |
| 26 | Fetch crawlee-python #1535 | gh CLI | apify/crawlee-python/issues/1535 | OOM in Kubernetes | Containerization |
| 27 | Fetch platform limits | WebFetch | docs.apify.com/platform/limits | Concrete limits documented | Platform constraints |
| 28 | Fetch crawlee #3212 | gh CLI | apify/crawlee/issues/3212 | 900ms+ startup time | Performance |
| 29 | Fetch agno #3513 | gh CLI | agno-agi/agno/issues/3513 | Third-party integration breakage | Integration signal |
| 30 | Fetch apify-cli #866, #1035 | gh CLI | apify/apify-cli | Local/platform mismatch, INPUT.json mutation | CLI friction |
| 31 | Fetch crawlee-python #1784 | gh CLI | apify/crawlee-python/issues/1784 | browser_new_context_options API mismatch | Python SDK |
| 32 | Fetch webhook timeout help | WebFetch | help.apify.com | Make 10s timeout documented workaround | Integration |
| 33 | Search proxy/session issues | WebSearch | apify crawlee proxy session | Confirmed session rotation patterns | Session handling |
| 34 | Search timeout issues | WebSearch | apify crawlee timeout | Found discussion threads | Timeout UX |
| 35 | Search webhook/actor limits | WebSearch | apify actor webhook timeout | Webhook 30s limit, sync 5min limit | Platform constraints |
| 36 | Fetch crawlee #3420, #3424 | gh CLI | apify/crawlee | v4 type/context issues | v4 migration |

## Budget Used

- Searches: ~12 (soft limit: 25)
- Fetches (gh CLI + WebFetch): ~36 (soft limit: 60)
- Total web operations: ~48 within budget
