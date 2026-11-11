# ExecuTorch Result

批次：999971_2026-11-11_040120
報告日期：2026-11-11 Asia/Taipei
更新時間：2026-11-11 10:05:46 Asia/Taipei（調整追蹤範圍；其餘查核時間沿用）

追蹤範圍：用戶於 2026-11-11 明確要求「停止這三項的每日追蹤」：embedding_bag（issue 11323／[PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871)）、avg_pool1d（issue 11325／[PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122)）、Qwen3.5（issue 18832／[PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873)）。三項皆已合併，自即日起移出目前追蹤表，不再每日查核 PR、CI 或 review，也不從舊報告補回；僅在用戶明確要求後恢復。avg_pool3d、QNN gather、Vulkan per-token INT8 繼續追蹤。用戶同日另要求停止 [PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) 的追蹤；該 PR 已關閉且未合併，移出追蹤表後不再查核，也不從舊報告補回。avg_pool3d 正式追蹤 PR 24126。

選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。
| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 完成 · [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126)；Open；merged=false；mergeable=false；尚無正式 review。82 個失敗 job 的原因與限制見 CI 欄；待處理合併衝突、補足 CI 證據及完成社群審查。；查核：2026-11-11 04:02:26 Asia/Taipei | 未開始 | 2026/11/11; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [82 個失敗工作](https://redirect.github.com/pytorch/executorch/pull/24126/checks)身份未變，77 個止於 checkout；其餘五項 output 仍空且無 artifacts，不能排除程式碼因素。 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 · [fork PR 45](https://github.com/yenhao-huang/executorch/pull/45)；[個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45)仍 open，head `214feb698e` 不變；依既有紀錄已通過 Claude CLI 完整審查，無待修發現；修正 LPAI 被誤套 GatherNd 的回歸，並補重複／靜態索引測試。[驗收報告](https://github.com/yenhao-huang/executorch/blob/214feb698e774626456546b1e942cc6d185cf714/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664。實體 SM8850／HTPv81 驗收仍受阻；fork 未回報 CI checks，Claude ACCEPT 不代表實機或社群驗收。原 issue 仍 open；[11/06 回報](https://redirect.github.com/pytorch/executorch/issues/24125#issuecomment-6676476340)指出 `index + mul` 在 HTP 16a8w 也出錯，是否受本修復涵蓋仍待驗證；未查得對應社群提交。；查核：2026-11-11 04:03:40 Asia/Taipei | 未開始 | 未開始 | 2026/11/11; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 · [fork PR 46](https://github.com/yenhao-huang/executorch/pull/46)；[個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46)仍 open，head `11d7b00408` 不變；依既有紀錄已於 2026-10-29 13:53 Asia/Taipei 通過 Claude CLI 完整審查，無待修的已確認問題；修正涵蓋 FP16、大 token dispatch、共用 Q/DQ 與既有 allowlist 融合回歸。[驗收報告](https://github.com/yenhao-huang/executorch/blob/11d7b004085896ba69c31030862c5ab1c199da20/docs/howard/22431.md)記錄 72 項 Vulkan／WebGPU Python 測試通過，另保留 32 組 INT8 C++ 案例證據。僅驗證 llvmpipe；實體 GPU、WebGPU native、encoder 品質與延遲未測，fork 無 CI checks。Claude ACCEPT 不等於社群核准或合併。原 issue 仍 open，未查得此實作的社群提交。；查核：2026-11-11 04:03:40 Asia/Taipei | 未開始 | 未開始 | 2026/11/11; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |

查核 head：avg_pool3d `c3b08504f2`。

avg_pool3d 已讀完目前 head 的 Actions runs、check-runs、statuses 全部分頁。以 workflow/event 為單位，只取最新 run／attempt；matrix job、Dr.CI 與其他外部檢查不混入 workflow 數字。avg_pool3d 有 1 個 skipped workflow。可讀取的非 Actions Meta 檢查均成功；avg_pool3d 的 Dr.CI 為 neutral，未發現清單外的 Actions check。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。日誌不足的歸因仍屬暫定。
