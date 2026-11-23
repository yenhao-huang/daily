更新時間：2026-11-24 04:02:56 Asia/Taipei

| 選擇的 issue | 選擇 issue stage | issue 開發 stage | 用戶在社群寄送 PR stage | 社群評論 stage | 該 PR 被 merge stage |
| --- | --- | --- | --- | --- | --- |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 已核准 | 完成 |
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

- 開發：[PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) 的最終 head 為 `2742b3d0b9`，已加入 dim-order pass、拆開 padding 失敗案例，並補輸入與輸出皆為 channels-last 的測試；同時簡化重複檢查並加入 max_pool2d padding 回歸測試。
- 驗證：審查者已核准並合併；上次 CI 查核留有一個 WebGPU models 失敗，今日無法重驗，詳見下方紀錄。本次只查核既有證據，未重跑測試。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### QNN 16a8w gather（issue 24125）

- 開發：[個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) 仍 open，head `214feb698e` 不變。已修正 LPAI 被誤套 GatherNd 的回歸，並補上重複／靜態索引測試。依既有紀錄已通過 Claude CLI 完整審查，無待修發現。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/214feb698e774626456546b1e942cc6d185cf714/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664。實體 SM8850／HTPv81 驗收仍受阻；fork 未回報 CI checks，Claude ACCEPT 不代表實機或社群驗收。
- 下一步：完成實體裝置驗收，確認 `index + mul` 回報是否在修復範圍內。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### Vulkan per-token INT8（issue 22431）

- 開發：[個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) 仍 open，head `11d7b00408` 不變。修正涵蓋 FP16、大 token dispatch、共用 Q/DQ 與既有 allowlist 融合回歸。依既有紀錄已於 2026-10-29 13:53 Asia/Taipei 通過 Claude CLI 完整審查，無待修的已確認問題。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/11d7b004085896ba69c31030862c5ab1c199da20/docs/howard/22431.md)記錄 72 項 Vulkan／WebGPU Python 測試通過，另保留 32 組 INT8 C++ 案例證據。僅驗證 llvmpipe；實體 GPU、WebGPU native、encoder 品質與延遲未測，fork 無 CI checks。Claude ACCEPT 不等於社群核准或合併。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### col2im.out（issue 11327）

- 開發：[個人 fork PR 48](https://github.com/yenhao-huang/executorch/pull/48) 為 open、未合併，head `f767beebd9`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/f767beebd9cf89365575b626bcb58d847811f659/docs/howard/11327.md)。
- 驗證：目前 head 的 PR 說明與[驗收報告](https://github.com/yenhao-huang/executorch/blob/f767beebd9cf89365575b626bcb58d847811f659/docs/howard/11327.md)記錄新測試 25/25；整個 `portable_kernels_test` 過／跳過／失敗為 1886 / 104 / 0。新增超出 SizesType 與整數溢位的防護及測試。本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### scatter_reduce.two_out（issue 11330）

- 開發：[個人 fork PR 3](https://github.com/yenhao-huang/executorch/pull/3) 為 open、未合併，head `e1a857eb68`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/e1a857eb68d453ee482bebe44208460df6ecd241/docs/howard/11330.md)。PR 3 為原地更新。
- 驗證：目前 head 的 PR 說明與[驗收報告](https://github.com/yenhao-huang/executorch/blob/e1a857eb68d453ee482bebe44208460df6ecd241/docs/howard/11330.md)記錄新測試 27/27；整個 `portable_kernels_test` 過／跳過／失敗為 1888 / 104 / 0。補上 Half／BFloat16 浮點累加與窄整數 mean 計數回繞處理。本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### adaptive_avg_pool1d.out（issue 11324）

- 開發：[個人 fork PR 50](https://github.com/yenhao-huang/executorch/pull/50) 為 open、未合併，head `09e5463aa3`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/09e5463aa3946a8b3a6f44af92074bea7848f24b/docs/howard/11324.md)。
- 驗證：目前 head 的 PR 說明與[驗收報告](https://github.com/yenhao-huang/executorch/blob/09e5463aa3946a8b3a6f44af92074bea7848f24b/docs/howard/11324.md)記錄新測試 24/24；整個 `portable_kernels_test` 過／跳過／失敗為 1885 / 104 / 0。補上 output_size 超出 SizesType 的檢查。本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### avg_pool2d_backward.grad_input（issue 11334）

- 開發：[個人 fork PR 49](https://github.com/yenhao-huang/executorch/pull/49) 為 open、未合併，head `5a9e2e2599`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/5a9e2e2599cca220df8924310f63b56bc68621d2/docs/howard/11334.md)。
- 驗證：目前 head 的 PR 說明與[驗收報告](https://github.com/yenhao-huang/executorch/blob/5a9e2e2599cca220df8924310f63b56bc68621d2/docs/howard/11334.md)記錄新測試 32/32；整個 `portable_kernels_test` 過／跳過／失敗為 1893 / 104 / 0。本次未重跑測試。
- 限制：Buck、ATen-mode 與完整 lintrunner 尚未驗證；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

#### native_layer_norm_backward.out（issue 11337）

- 開發：[個人 fork PR 51](https://github.com/yenhao-huang/executorch/pull/51) 為 open、未合併，head `767d3e23fc`。已附[驗收報告](https://github.com/yenhao-huang/executorch/blob/767d3e23fc243d5d0fb32c9411c0a056b6aca1f7/docs/howard/11337.md)。
- 驗證：目前 head 的 PR 說明與[驗收報告](https://github.com/yenhao-huang/executorch/blob/767d3e23fc243d5d0fb32c9411c0a056b6aca1f7/docs/howard/11337.md)記錄新測試 21 過、1 跳過；整個 `portable_kernels_test` 過／跳過／失敗為 1882 / 105 / 0。新增 dim-order 驗證；DynamicShapeUnbound 仍因需要 output_resize 而跳過。本次未重跑測試。
- 限制：Buck 與 ATen-mode 尚未驗證，完整 lintrunner 因本機權限錯誤受阻；fork 目前沒有 CI checks、review 或留言。本機測試結果不代表社群 CI 通過。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

### 社群評論 stage

#### avg_pool3d.out（issue 11326）

- 社群審查：JakeStevens 於 2026-11-19 00:09:25 Asia/Taipei [核准](https://redirect.github.com/pytorch/executorch/pull/24126#pullrequestreview-5960457167)，並於 00:09:37 合併；已確認 `merged=true`，合併 commit 為 `2531e0c0ef`。原 issue 也已關閉。
- 目前狀況：合併階段完成；保留這筆完成紀錄。最後提交的 WebGPU models 失敗保留上次紀錄；今日 CI 查詢不完整，合併狀態已另行確認。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: unknown; CI sucess: unknown; Require fix: 5% (false); Evidence: 今日 CI 清單仍為空、原 run 仍回傳 404；5% 沿用 11/20 審查，未重新驗證。[PR](https://redirect.github.com/pytorch/executorch/pull/24126) [原 run](https://redirect.github.com/pytorch/executorch/actions/runs/44233244844)

2026-11-20 的查核記錄顯示，[WebGPU operators job](https://redirect.github.com/pytorch/executorch/actions/runs/44233244844/job/134874036453) 雖回報 success，實際為 9 failed、384 passed、75 skipped、1 xfailed。三輪唯讀審查將九項失敗分為四組：2 項非最後維度的 amin／amax、4 項整數 floor_divide、2 項 replicate padding 的整數 clamp，以及 1 項不支援的 grouped conv1d。相關測試、runtime 限制、[分割器](https://redirect.github.com/pytorch/executorch/blob/2742b3d0b90148101510da0df2a4114e7e397a9a/backends/webgpu/partitioner/partitioner.py#L100)及 CI 來源與精確 base 相同；pytest 的退出碼 1 未傳遞至工作狀態。尚無同環境 base 實測，也未取得序列化圖核對 padding 至 clamp 的逐節點路徑。

[WebGPU models job](https://redirect.github.com/pytorch/executorch/actions/runs/44233244844/job/134874037006) 於 2026-11-20 確認 head、run、attempt、job 與失敗步驟未變，當時沿用 2026-11-19 的三輪診斷：套件下載 503 阻斷系統 libstdc++ 升級，隨後 Dawn 連結缺符號；SwiftShader 404 已恢復。實際連結庫路徑仍屬推論，models 未進入模型測試。

Require fix 5%（false）為 2026-11-20 涵蓋上述失敗的主觀判斷，今日保留該結論與限制，未完成新的因果審查。下一步為 WebGPU 維護者檢查分割器與 runtime 支援範圍，並修正套件安裝及測試退出碼的傳遞；本次未修改或重跑 CI。

目前 head 仍為 `2742b3d0b9`。上次成功查核（2026-11-20 04:03:30 Asia/Taipei）按 workflow/event 的最新 run／attempt 統計，共 30 個 workflow：28 success、1 failure、1 skipped。完整 252 項最新 check 為 180 success、1 failure、70 skipped、1 neutral；Meta 檢查成功，Dr.CI 為 neutral，均不重複計入 workflow。CI 清單查核時間：2026-11-20 04:03:30 Asia/Taipei；operators 因果查核時間：2026-11-20 04:05:34 Asia/Taipei；models 原審查時間：2026-11-19 04:05:49 Asia/Taipei。

今日 CI 查核（2026-11-24 04:01:39 Asia/Taipei）仍未能重驗：目前 head 的 workflows、check-runs 與 check-suites 均回傳空清單；分支清單中的 36 筆 run 均屬其他 head。原 WebGPU run 與 jobs 查詢回傳 404，原因未明，不能將空清單解讀為零失敗。保留上述最後成功查核數字及原始審查時間，待來源恢復後重新核對。

#### QNN 16a8w gather（issue 24125）

- 社群評論：原 issue 仍 open。[11/06 回報](https://redirect.github.com/pytorch/executorch/issues/24125#issuecomment-6676476340)指出 `index + mul` 在 HTP 16a8w 也出錯，是否受本修復涵蓋仍待驗證；未查得對應社群提交。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。

#### Vulkan per-token INT8（issue 22431）

- 社群狀態：原 issue 仍 open。搜尋找到已合併的[文件修正 PR 22432](https://redirect.github.com/pytorch/executorch/pull/22432)，僅更正 per-tensor 說明，未實作 per-token INT8；未查得 fork PR 46 對應的社群提交。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。

#### col2im.out（issue 11327）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11327) 仍 open，沒有留言。以 issue 編號及 fork 分支查詢社群 PR，均未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 48](https://github.com/yenhao-huang/executorch/pull/48)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### scatter_reduce.two_out（issue 11330）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11330) 仍 open，沒有留言。以 issue 編號及 fork 分支查詢社群 PR，均未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 3](https://github.com/yenhao-huang/executorch/pull/3)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### adaptive_avg_pool1d.out（issue 11324）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11324) 仍 open，沒有留言。以 issue 編號及 fork 分支查詢社群 PR，均未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 50](https://github.com/yenhao-huang/executorch/pull/50)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### avg_pool2d_backward.grad_input（issue 11334）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11334) 仍 open，沒有留言。以 issue 編號及 fork 分支查詢社群 PR，均未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 49](https://github.com/yenhao-huang/executorch/pull/49)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。

#### native_layer_norm_backward.out（issue 11337）

- 社群評論／審查：[原 issue](https://redirect.github.com/pytorch/executorch/issues/11337) 仍 open，沒有留言。以 issue 編號及 fork 分支查詢社群 PR，均未查得結果。
- PR 狀態／下一步：目前追蹤[個人 fork PR 51](https://github.com/yenhao-huang/executorch/pull/51)；待用戶提交對應社群 PR 後，再追蹤社群 CI、review 與 merge。
- 查核時間：2026-11-24 04:01:39 Asia/Taipei。

CI：2026/11/24; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；fork PR 僅作開發證據。
