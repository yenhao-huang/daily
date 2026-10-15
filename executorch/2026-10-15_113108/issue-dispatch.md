# ExecuTorch Issue Dispatch

批次：2026-10-15_113108
更新時間：2026-10-15 13:30:41 Asia/Taipei
候選數：10

以下為尚未選定的候選介紹；問題依 issue、留言及關聯 PR 整理，未在本機重現。可能解法是待驗證方向，不代表已完成修正。
Note: scope 依題目使用 perf、inference、operator、export、runtime、memory、backend、ci 等。
本清單包含需先協調或拆分的架構題，已在個別介紹註明；有明確現成修正 PR 的其他候選已排除。

## 1. (operator): Cortex-M depthwise convolution 缺少輸入 layout 檢查

Issue：[ExecuTorch #23812](https://redirect.github.com/pytorch/executorch/issues/23812)
來源更新時間：2026-10-14T14:58:09Z

### 問題釐清

channels-first 輸入會被替換成只接受 channels-last 的 Cortex-M kernel，導致執行時報錯。原文提供 contiguous 輸入與 mean pooling 後接 depthwise convolution 的兩個案例；fake implementation 的形狀推導沒有阻止不支援的 layout。議題目前沒有留言或指派者。

### 可能解法

先用原文兩個案例確認 lowering 與 runtime 的 layout；依作者建議，在不支援時保留原 operator，或插入明確 layout conversion。同步檢查 fake implementation 的限制，加入轉換前後數值與 layout 回歸測試；完整執行需要 Cortex-M 測試環境。

## 2. (runtime): Python Module 對 device output 配置了 host memory

Issue：[ExecuTorch #23553](https://redirect.github.com/pytorch/executorch/issues/23553)
來源更新時間：2026-10-07T21:52:36Z

### 問題釐清

PyModule::allocate_output_tensors 對未規劃的輸出一律配置 host bytes，即使輸出標記為 CUDA。這可能被 delegate 拒絕，或在後續 GPU 複製時出錯。[既有 Method 修正](https://redirect.github.com/pytorch/executorch/pull/23547)已合併，但其描述明確將 Module 路徑留給本題；目前無指派者。

### 可能解法

參照 Method 的 device allocator 路徑，讓 Module 依輸出 device 配置 buffer，並讓回傳 tensor 正確持有生命週期。測試連續執行時舊輸出仍有效、device/CPU/零長度輸出與配置失敗情境；CUDA 行為需在實際 GPU 驗證。

## 3. (backend): Vulkan 對不支援 dtype 缺少 partition fallback

Issue：[ExecuTorch #11766](https://redirect.github.com/pytorch/executorch/issues/11766)
來源更新時間：2026-09-18T20:36:43Z

### 問題釐清

原始案例因 float64 在 Vulkan serialization 被拒絕而無法匯出；最新留言指出 float64、int16 已可使用，剩下 uint16、uint32 執行失敗及 uint64 序列化失敗。應重新確認目前支援矩陣，避免照舊清單把已支援 dtype 排除。

### 可能解法

在 partitioner 判斷輸入與輸出的 dtype 能力，對不支援的節點保留 CPU fallback，並確認 portable kernel 本身是否支援。以 unsigned dtype 測試匯出、delegate 邊界及數值一致性，也涵蓋已支援 dtype 的不退步測試。

## 4. (export): 新版 ultralytics 的 YOLO26 strict export 仍失敗

Issue：[ExecuTorch #23453](https://redirect.github.com/pytorch/executorch/issues/23453)
來源更新時間：2026-10-06T18:05:01Z

### 問題釐清

此題原本含兩個問題。[layout 修正](https://redirect.github.com/pytorch/executorch/pull/23505)已合併，處理 8.4.133–8.4.139 的 channels-last 權重；剩餘範圍是 8.4.140 以後 strict export 的 PendingUnbackedSymbolNotFound。既有 pin 讓 CI 避開問題，不等於新版已支援。

### 可能解法

以目前仍能重現的 ultralytics 版本縮小 unbacked symbol 的來源，檢查模型 wrapper 與匯出分支，先完成 strict export 與 portable 數值比對再提高 pin。不要重做已合併的 layout 修正；需下載模型權重並建立版本對照。

## 5. (inference): 補齊 Arm streaming wakeword 匯出與連續幀測試

Issue：[ExecuTorch #23440](https://redirect.github.com/pytorch/executorch/issues/23440)
來源更新時間：2026-10-05T22:04:06Z

### 問題釐清

需求是將 portable streaming wakeword 延伸到 TOSA FP/INT 與 Ethos-U55/U85。[已合併的模型 PR](https://redirect.github.com/pytorch/executorch/pull/23133)只加入模型、註冊與 eager 測試，明確未涵蓋 export/backend/runner；模型保留跨幀狀態，30 幀後輸出才有效。目前無指派者或留言。

### 可能解法

先確認 portable export 前置工作是否就緒，再以 successive frames 與 reset/replay 建立 TOSA reference 比對，之後驗證 U55/U85 FVP。測試需檢查跨幀 buffer 狀態與量化誤差；FVP、TOSA 工具鏈及前置 export 是環境／依賴條件。

## 6. (perf): 評估 XNNPACK workspace 與 ET activation memory 共用

Issue：[ExecuTorch #8764](https://redirect.github.com/pytorch/executorch/issues/8764)
來源更新時間：2026-10-14T21:31:09Z

### 問題釐清

[DelegateScratchSpec](https://redirect.github.com/pytorch/executorch/pull/21985)已合併，因此不能再把此題描述成完全沒有 scratch API。最新維護者留言表示 XNNPACK 仍使用 malloc，原本的整體記憶體需求尚未完全解決；也已有社群成員詢問量測切入點，正式開發前需釐清剩餘範圍。

### 可能解法

先選含 graph break 的模型量測 ET arena 與 XNNPACK workspace 的峰值及生命週期，再評估靜態 shape 能否預先取得 workspace 大小並使用既有 scratch API。先以量測與小型概念驗證決定是否值得整合，不承諾直接完成跨 delegate 的通用記憶體規劃。

## 7. (memory): 支援沒有固定上界的動態 tensor memory

Issue：[ExecuTorch #8766](https://redirect.github.com/pytorch/executorch/issues/8766)
來源更新時間：2026-10-06T16:27:55Z

### 問題釐清

原文希望避免所有 tensor 都依最大 shape 預留空間，並支援輸入尺寸範圍大或難以給定上界的模型。需求包含 activation buffer 重用、避免增加受限裝置 runtime 體積，以及資料相依 shape。最新留言仍在詢問進度，這是範圍較大的架構題。

### 可能解法

先驗證目前 main 的既有動態能力，將剩餘需求拆成最小案例，評估序列化 lifetime metadata、buffer 重新配置及 relocation。以 build option 隔離額外 runtime 成本，比較峰值記憶體與延遲；本題適合分階段研究，不宜承諾一週完成。

## 8. (operator): 補齊 while_loop 的 lowering 與 emitter 支援

Issue：[ExecuTorch #8769](https://redirect.github.com/pytorch/executorch/issues/8769)
來源更新時間：2026-09-18T20:13:22Z

### 問題釐清

題名同時提到 while_loop 與 scan，但 [scan 支援](https://redirect.github.com/pytorch/executorch/pull/16028)已合併，不能重做。討論中的 while 前段 pass 修正也已存在；最新留言指出仍在 emitter 被拒絕，測試還預期 Unsupported control flow operator。記憶體規劃與迴圈 shape 邊界需另外釐清。

### 可能解法

先以最小 while_loop 驗證失敗階段，再參照 cond/map/scan 的 emission，評估以現有 primitive 與 jump 表達迴圈。補零次／多次迭代、carry tensor、shape 上界與輸出數值測試，並獨立檢查迴圈生命週期的 memory planning；不要先假定需要擴充 runtime。

## 9. (export): 讓隱含 dim-order 轉換在 portable graph 中一致表達

Issue：[ExecuTorch #11086](https://redirect.github.com/pytorch/executorch/issues/11086)
來源更新時間：2026-10-05T20:59:31Z

### 問題釐清

PyTorch 的 Linear、reduction 或 convolution 可能隱含轉 layout，但匯出的節點 metadata 改變後，graph 不一定有對應 copy，portable kernel 因混合 dim order 失敗。近期討論指出局部插入 copy 可能造成錯值或把問題移到下游；已有其他人提出研究與承接意願，本題列為需協調的候選。

### 可能解法

先用 reduction 加 elementwise 與 channels-last Linear 的小案例重現，檢查輸入、輸出 metadata/spec 與實際 storage 的一致性。評估在 lowering 中同時插入 conversion 與傳播 output dim order，而非只對單一 kernel 打補丁。加入混合 layout 多算子鏈的數值回歸測試；開始前需由用戶確認是否與既有工作重疊。

## 10. (ci): 評估依賴更新流程與受控的排程設定

Issue：[ExecuTorch #21640](https://redirect.github.com/pytorch/executorch/issues/21640)
來源更新時間：2026-08-10T19:18:23Z

### 問題釐清

這是一項提案而非已證實的 runtime bug：作者建議每月更新非 breaking dependencies，並考慮套件發布等待期及 CI 觸發方式。目前沒有留言或關聯 PR；是否採用第三方 Action、哪些 pin 可自動更新，以及維護者是否接受，尚未定案。

### 可能解法

先盤點相依與版本 pin 的用途，提出最小設定草稿，評估現有工具、權限、可重現性與更新分組；只在個人 fork 驗證設定。不得設定社群 secrets、啟用社群 workflow 或自動發送社群 PR；是否採用及正式送出由用戶與維護者決定。
