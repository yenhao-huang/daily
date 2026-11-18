更新時間：2026-11-18 11:07:42 Asia/Taipei

| 選擇的 issue | 選擇 issue stage | issue 開發 stage | 用戶在社群寄送 PR stage | 社群評論 stage | 該 PR 被 merge stage |
| --- | --- | --- | --- | --- | --- |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 進行中 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 新一輪要求修改 | 未開始 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 | 未開始 | 回報待驗證 | 未開始 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 | 未開始 | 尚無社群 PR | 未開始 |
| [col2im.out](https://redirect.github.com/pytorch/executorch/issues/11327) · 僅追蹤 PR（未選題） | 未開始 | 完成 · [fork PR 48](https://github.com/yenhao-huang/executorch/pull/48) | 未開始 | 尚無社群 PR | 未開始 |
| [scatter_reduce.two_out](https://redirect.github.com/pytorch/executorch/issues/11330) · 僅追蹤 PR（未選題） | 未開始 | 完成 · [fork PR 3](https://github.com/yenhao-huang/executorch/pull/3) | 未開始 | 尚無社群 PR | 未開始 |
| [adaptive_avg_pool1d.out](https://redirect.github.com/pytorch/executorch/issues/11324) · 僅追蹤 PR（未選題） | 未開始 | 完成 · [fork PR 50](https://github.com/yenhao-huang/executorch/pull/50) | 未開始 | 尚無社群 PR | 未開始 |
| [avg_pool2d_backward.grad_input](https://redirect.github.com/pytorch/executorch/issues/11334) · 僅追蹤 PR（未選題） | 未開始 | 完成 · [fork PR 49](https://github.com/yenhao-huang/executorch/pull/49) | 未開始 | 尚無社群 PR | 未開始 |
| [native_layer_norm_backward.out](https://redirect.github.com/pytorch/executorch/issues/11337) · 僅追蹤 PR（未選題） | 未開始 | 完成 · [fork PR 51](https://github.com/yenhao-huang/executorch/pull/51) | 未開始 | 尚無社群 PR | 未開始 |

## Details

### issue 開發 stage

#### avg_pool3d.out（issue 11326）

- 開發：[PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) 已更新至 head `0a11519e19`，並將 main 的更新合併至此分支。逐軸 padding 檢查、reduction callback、空視窗防護與累加型別已更新；審查者確認上一輪四項要求均已處理。
- 驗證：目前提交的社群 CI 無失敗，但新一輪 review 指出 dim-order 匯出流程與測試覆蓋仍有缺口，開發維持待修正。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

#### QNN 16a8w gather（issue 24125）

- 開發：[個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) 仍 open，head `214feb698e` 不變。已修正 LPAI 被誤套 GatherNd 的回歸，並補上重複／靜態索引測試。依既有紀錄已通過 Claude CLI 完整審查，無待修發現。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/214feb698e774626456546b1e942cc6d185cf714/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664。實體 SM8850／HTPv81 驗收仍受阻；fork 未回報 CI checks，Claude ACCEPT 不代表實機或社群驗收。
- 下一步：完成實體裝置驗收，確認 `index + mul` 回報是否在修復範圍內。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

#### Vulkan per-token INT8（issue 22431）

- 開發：[個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) 仍 open，head `11d7b00408` 不變。修正涵蓋 FP16、大 token dispatch、共用 Q/DQ 與既有 allowlist 融合回歸。依既有紀錄已於 2026-10-29 13:53 Asia/Taipei 通過 Claude CLI 完整審查，無待修的已確認問題。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/11d7b004085896ba69c31030862c5ab1c199da20/docs/howard/22431.md)記錄 72 項 Vulkan／WebGPU Python 測試通過，另保留 32 組 INT8 C++ 案例證據。僅驗證 llvmpipe；實體 GPU、WebGPU native、encoder 品質與延遲未測，fork 無 CI checks。Claude ACCEPT 不等於社群核准或合併。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

#### col2im.out（issue 11327）

- 開發：[個人 fork PR 48](https://github.com/yenhao-huang/executorch/pull/48) 為 open、未合併，head `f3711c7500`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/f3711c750016908e9755037251e3899a49e96e2f/docs/howard/11327.md)。
- 驗證：新測試 22/22；整個 `portable_kernels_test` 過／跳過／失敗為 1883 / 104 / 0。數字由用戶提供，已與 PR 說明核對；本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

#### scatter_reduce.two_out（issue 11330）

- 開發：[個人 fork PR 3](https://github.com/yenhao-huang/executorch/pull/3) 為 open、未合併，head `80bc835157`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/80bc835157243f67034dd2807b7f7c4d5ab42982/docs/howard/11330.md)。 PR 3 為原地更新。
- 驗證：新測試 24/24；整個 `portable_kernels_test` 過／跳過／失敗為 1885 / 104 / 0。數字由用戶提供，已與 PR 說明核對；本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

#### adaptive_avg_pool1d.out（issue 11324）

- 開發：[個人 fork PR 50](https://github.com/yenhao-huang/executorch/pull/50) 為 open、未合併，head `9a33fe364e`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/9a33fe364ed3702bdbc3e9b7f82e863bb0ae8e9c/docs/howard/11324.md)。
- 驗證：新測試 23/23；整個 `portable_kernels_test` 過／跳過／失敗為 1884 / 104 / 0。數字由用戶提供，已與 PR 說明核對；本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

#### avg_pool2d_backward.grad_input（issue 11334）

- 開發：[個人 fork PR 49](https://github.com/yenhao-huang/executorch/pull/49) 為 open、未合併，head `083900b6bf`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/083900b6bf31f0bb9252b51d3097368d46e52ee9/docs/howard/11334.md)。
- 驗證：新測試 32/32；整個 `portable_kernels_test` 過／跳過／失敗為 1893 / 104 / 0。數字由用戶提供，已與 PR 說明核對；本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

#### native_layer_norm_backward.out（issue 11337）

- 開發：[個人 fork PR 51](https://github.com/yenhao-huang/executorch/pull/51) 為 open、未合併，head `9c1cd7f4c9`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/9c1cd7f4c973be5882a0a0c0e5bed784669b66f7/docs/howard/11337.md)。
- 驗證：新測試 19 過、1 跳過；整個 `portable_kernels_test` 過／跳過／失敗為 1880 / 105 / 0。數字由用戶提供，已與 PR 說明核對；本次未重跑測試。 新測試跳過項為 DynamicShapeUnbound，依 PR 說明需要 output_resize。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

### 社群評論 stage

#### avg_pool3d.out（issue 11326）

- 社群審查：JakeStevens 於 2026-11-18 03:19:21 Asia/Taipei 提交新一輪 [CHANGES_REQUESTED](https://redirect.github.com/pytorch/executorch/pull/24126#pullrequestreview-5945020088)，確認上一輪四項要求已處理；PR 仍 open，`merged=false`、`mergeable=true`。
- [Dim-order pass 註冊](https://redirect.github.com/pytorch/executorch/pull/24126#discussion_r4604551485)：將 avg_pool3d 加入 `LegalizePortableDimOrderPass._target_ops`，並補 3D 測試。review 指出 `channels_last_3d` 輸入目前可匯出，卻因缺少轉換 copy 而在 runtime 回報 InvalidArgument；測試 module 應避免使用會先在 `to_edge` 失敗的 clone。
- [Padding 測試獨立性](https://redirect.github.com/pytorch/executorch/pull/24126#discussion_r4604551494)：`SingleElementPaddingExceedsHalfKernelOnOtherAxes` 共用未重設的 failure state，後續案例可能假通過；每個案例需拆成獨立 `TEST_F`。
- [Default dim-order 覆蓋](https://redirect.github.com/pytorch/executorch/pull/24126#discussion_r4604551501)：`NonDefaultDimOrder` 提早在輸入／輸出排列不一致時失敗，未測到 default-dim-order 檢查；需另測輸入與輸出皆為 channels-last 的案例。
- 其他要求：[簡化重複的輸出大小檢查](https://redirect.github.com/pytorch/executorch/pull/24126#discussion_r4604551521)，保留 input ≥ kernel 與 stride int32 上限；補 [max_pool2d_with_indices padding 回歸測試](https://redirect.github.com/pytorch/executorch/pull/24126#discussion_r4604551534)，並在 PR 說明 avg_pool2d 與 max_pool2d 的行為變更。
- 下一步：先完成前三項合併前必修問題，一併處理其餘 review，重新驗證後等待審查；CI 通過不代表 review 已核准。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

CI：2026/11/18; CI fail: 0; CI sucess: 28; Require fix: 0% (false); Evidence: 新 head 無 CI 失敗可歸因；但 layout 整合與兩項測試缺口仍須修正，通過 CI 不代表正確，本次未執行重現：[CI](https://redirect.github.com/pytorch/executorch/actions/runs/44065288490)、[審查](https://redirect.github.com/pytorch/executorch/pull/24126#pullrequestreview-5945020088)。

Require fix 為 executorch-dev 對目前 CI 失敗需修改程式碼的主觀判斷；目前失敗集合為空，0% 不代表程式碼沒有缺陷，上述 review 仍明確要求修正。

目前 head `0a11519e19`，測試 merge ref `39e48556e9`；按 workflow/event 的最新 run／attempt 統計，另有 1 個 skipped workflow。已核對完整 245 項最新 check：174 success、70 skipped、1 neutral；Meta 檢查成功，Dr.CI 為 neutral，不重複計入 workflow。CI 查核時間：2026-11-18 04:03:26 Asia/Taipei。

#### QNN 16a8w gather（issue 24125）

- 社群評論：原 issue 仍 open。[11/06 回報](https://redirect.github.com/pytorch/executorch/issues/24125#issuecomment-6676476340)指出 `index + mul` 在 HTP 16a8w 也出錯，是否受本修復涵蓋仍待驗證；未查得對應社群提交。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。

#### Vulkan per-token INT8（issue 22431）

- 社群狀態：原 issue 仍 open，未查得此實作的社群提交。
- 查核時間：2026-11-18 04:03:26 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。

#### col2im.out（issue 11327）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11327) 仍 open，沒有留言。以 issue 編號查詢用戶提交的社群 PR，未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 48](https://github.com/yenhao-huang/executorch/pull/48)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### scatter_reduce.two_out（issue 11330）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11330) 仍 open，沒有留言。以 issue 編號查詢用戶提交的社群 PR，未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 3](https://github.com/yenhao-huang/executorch/pull/3)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### adaptive_avg_pool1d.out（issue 11324）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11324) 仍 open，沒有留言。以 issue 編號查詢用戶提交的社群 PR，未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 50](https://github.com/yenhao-huang/executorch/pull/50)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### avg_pool2d_backward.grad_input（issue 11334）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11334) 仍 open，沒有留言。以 issue 編號查詢用戶提交的社群 PR，未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 49](https://github.com/yenhao-huang/executorch/pull/49)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### native_layer_norm_backward.out（issue 11337）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11337) 仍 open，沒有留言。以 issue 編號查詢用戶提交的社群 PR，未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 51](https://github.com/yenhao-huang/executorch/pull/51)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-18 11:07:42 Asia/Taipei。

CI：2026/11/18; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。
