更新時間：2026-11-12 04:06:27 Asia/Taipei

| 選擇的 issue | 選擇 issue stage | issue 開發 stage | 用戶在社群寄送 PR stage | 社群評論 stage | 該 PR 被 merge stage |
| --- | --- | --- | --- | --- | --- |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 待審查 | 未開始 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 | 未開始 | 回報待驗證 | 未開始 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 | 未開始 | 尚無社群 PR | 未開始 |

## Details

### issue 開發 stage

#### avg_pool3d.out（issue 11326）

- 開發：已完成，提交至 [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126)。查核 head：`c3b08504f2`。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

#### QNN 16a8w gather（issue 24125）

- 開發：[個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) 仍 open，head `214feb698e` 不變。已修正 LPAI 被誤套 GatherNd 的回歸，並補上重複／靜態索引測試。依既有紀錄已通過 Claude CLI 完整審查，無待修發現。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/214feb698e774626456546b1e942cc6d185cf714/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664。實體 SM8850／HTPv81 驗收仍受阻；fork 未回報 CI checks，Claude ACCEPT 不代表實機或社群驗收。
- 下一步：完成實體裝置驗收，確認 `index + mul` 回報是否在修復範圍內。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

#### Vulkan per-token INT8（issue 22431）

- 開發：[個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) 仍 open，head `11d7b00408` 不變。修正涵蓋 FP16、大 token dispatch、共用 Q/DQ 與既有 allowlist 融合回歸。依既有紀錄已於 2026-10-29 13:53 Asia/Taipei 通過 Claude CLI 完整審查，無待修的已確認問題。
- 驗證：[驗收報告](https://github.com/yenhao-huang/executorch/blob/11d7b004085896ba69c31030862c5ab1c199da20/docs/howard/22431.md)記錄 72 項 Vulkan／WebGPU Python 測試通過，另保留 32 組 INT8 C++ 案例證據。僅驗證 llvmpipe；實體 GPU、WebGPU native、encoder 品質與延遲未測，fork 無 CI checks。Claude ACCEPT 不等於社群核准或合併。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

### 社群評論 stage

#### avg_pool3d.out（issue 11326）

- 社群審查：PR 仍為 Open，`merged=false`、`mergeable=false`，尚無正式 review。
- 下一步：處理合併衝突、補足 CI 證據並完成社群審查。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

CI：2026/11/12; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [82 個失敗工作](https://redirect.github.com/pytorch/executorch/pull/24126/checks)身份未變，77 個止於 checkout；其餘五項 output 仍空、附註存取受限、無可用 artifacts，尚不能排除程式碼因素。

目前 head `c3b08504f2` 按 workflow/event 的最新 run／attempt 統計，另有 1 個 skipped workflow。完整分頁未發現清單外的 Actions check；Meta 檢查均成功，Dr.CI 為 neutral。CI 複核時間：2026-11-12 04:04:43 Asia/Taipei。

#### QNN 16a8w gather（issue 24125）

- 社群評論：原 issue 仍 open。[11/06 回報](https://redirect.github.com/pytorch/executorch/issues/24125#issuecomment-6676476340)指出 `index + mul` 在 HTP 16a8w 也出錯，是否受本修復涵蓋仍待驗證；未查得對應社群提交。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

CI：2026/11/12; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。

#### Vulkan per-token INT8（issue 22431）

- 社群狀態：原 issue 仍 open，未查得此實作的社群提交。
- 查核時間：2026-11-12 04:01:50 Asia/Taipei。

CI：2026/11/12; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。
