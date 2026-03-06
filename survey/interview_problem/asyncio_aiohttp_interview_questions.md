# asyncio / aiohttp 面試題整理（偏 NVIDIA / Meta / Google 風格）

> 這份題目偏向「大型系統、效能、可靠性」導向，符合一線公司常見問法。

## A. asyncio 核心觀念

1. `asyncio` 的 event loop 如何運作？`await` 背後做了什麼？
2. `coroutine`、`Task`、`Future` 三者差異是什麼？
3. `asyncio.create_task()` 和直接 `await` 的語意差異？
4. 什麼情況會造成 event loop starvation？如何避免？
5. 如何在 async 程式裡安全地呼叫 blocking I/O？（`run_in_executor` / `to_thread`）
6. `asyncio.gather()`、`wait()`、`as_completed()` 的差異與適用場景？
7. `return_exceptions=True` 的利弊？
8. cancellation 是怎麼傳遞的？`CancelledError` 要怎麼正確處理？
9. `shield()` 什麼時候該用、什麼時候不該用？
10. timeout 應該放在哪一層？（call-level / request-level / global）

## B. Python 3.11+ 結構化併發（高頻）

11. `TaskGroup` 相比 `gather` 的優點是什麼？
12. `ExceptionGroup` 是什麼？如何拆解多個子例外？
13. fail-fast 與 best-effort 併發策略怎麼設計？
14. 子任務失敗時，你會如何做 rollback 或補償？

## C. aiohttp 實作重點（Client）

15. 為什麼要重用 `ClientSession`？每 request 新建 session 的代價？
16. `TCPConnector(limit, limit_per_host, ttl_dns_cache)` 如何調參？
17. `ClientTimeout(total, connect, sock_connect, sock_read)` 應怎麼設定？
18. 如何實作 retry（只 retry 可重試錯誤）並避免重複 side effects？
19. 如何實作 exponential backoff + jitter？
20. 429/503 遇到時如何 respect `Retry-After`？
21. 如何避免 ephemeral port exhaustion / connection leak？
22. streaming response (`content.iter_chunked`) 使用時要注意什麼？
23. gzip/br 壓縮、JSON decode 大 payload 會有哪些瓶頸？
24. 如何在 client 端做 metrics/tracing（latency, inflight, error rate）？

## D. aiohttp Server（若職缺偏平台）

25. middleware 的執行順序與責任邊界怎麼設計？
26. 如何做 graceful shutdown（停止收新請求 + 等待 in-flight 結束）？
27. 如何限制單請求 body 大小與防止 slowloris？
28. 背景任務（background tasks）與 request lifecycle 如何解耦？
29. 如何設計 health check / readiness / liveness endpoints？
30. 你會怎麼做 per-client rate limiting 與全域併發保護？

## E. 系統設計導向（Meta/Google 常見）

31. 設計一個高併發 webhook dispatcher（10k req/s）會怎麼做？
32. 如何做 downstream fan-out（同時打 20 個服務）又不把自己打爆？
33. 如何設計 bulkhead（隔艙）避免某個依賴拖垮整體？
34. 什麼時候該用 queue（Kafka/RabbitMQ）取代同步 HTTP call？
35. 如果 P99 latency 飆高，你會如何定位瓶頸？
36. 你會怎麼定義 SLO / error budget 並映射到重試策略？
37. 如何避免 thundering herd（快取失效同時打 DB/API）？
38. 多區域部署時 timeout/retry 要怎麼改？
39. 若依賴服務間歇性 timeout，如何做 circuit breaker？
40. 如何在 async service 做 idempotency 保證？

## F. Debug / 效能排查（NVIDIA 風格偏重）

41. 如何抓出 event loop 被 blocking 的程式碼？
42. 如何觀察 task leak（任務沒結束）？
43. `uvloop` 的好處與限制是什麼？
44. `asyncio` debug mode 該怎麼用？
45. 高併發下記憶體暴增常見原因有哪些？
46. 如何量測 coroutine scheduling overhead？
47. 何時該改成 multiprocessing / Rust extension / C++ service？
48. TLS handshake 成本高時，client 端可做哪些優化？
49. 為什麼 connector limit 設太高反而變慢？
50. 如何設計可重現的壓測場景（warmup / steady / spike）？

## G. 實作題（白板 / take-home）

51. 實作 async bounded map：限制同時最多 N 個任務。
52. 實作帶 timeout + retry + jitter 的 `fetch_json()`。
53. 實作 async rate limiter（token bucket）。
54. 實作批次 fan-out，任一關鍵任務失敗則整批取消。
55. 實作可取消且可觀測（metrics/logging/tracing）的 crawler。
56. 實作 streaming proxy（上游 chunk 轉發到下游）。
57. 實作 graceful shutdown：SIGTERM 後 30 秒內收斂。
58. 實作 idempotent webhook receiver（去重 + 過期清理）。
59. 實作 per-host 連線池與全域併發上限。
60. 實作 API client SDK：統一 timeout/retry/error mapping。

## H. 面試官追問點（準備答案）

- 為什麼這樣設 timeout？依據是什麼數據？
- retry 造成流量放大怎麼控？
- 如何驗證沒有 connection leak？
- cancellation 會不會吞錯誤？
- 哪些情況你會「不要用 async」？

## I. 30 分鐘速練建議

1. 先口頭講清楚 event loop / Task / cancellation。
2. 手寫 `fetch_json`（timeout+retry+jitter+429）。
3. 手寫 bounded concurrency（Semaphore 或 TaskGroup）。
4. 補一段觀測：latency/error/inflight metrics。

---

如果你要，我可以再出一版「附參考答案要點」版本（每題 3~5 句標準答法），方便你直接背面試框架。
