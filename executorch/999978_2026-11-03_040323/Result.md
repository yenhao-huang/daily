# ExecuTorch Result

批次：999978_2026-11-03_040323
報告日期：2026-11-03 Asia/Taipei
更新時間：2026-11-03 04:09:28 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [embedding_bag 審查修正](https://redirect.github.com/pytorch/executorch/issues/11323) | 完成 | 進行中 · [PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | 完成 | 未開始 | 2026/11/03; CI fail: unknown; CI sucess: unknown; Require fix: 49% (false); Evidence: [合併衝突已確認](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6586401657)；[昨日 Lint run 今日回 404](https://redirect.github.com/pytorch/executorch/actions/runs/41157564676)，CI 數量未知，Actions 故障僅為推測。 |
| [avg_pool1d.out](https://redirect.github.com/pytorch/executorch/issues/11325) | 完成 | 完成 · [PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | 完成 | 完成 | 2026/11/03; CI fail: 1; CI sucess: 23; Require fix: 1% (false); Evidence: [QNN Windows 失敗發生於 SDK 解壓與目錄檢查](https://redirect.github.com/pytorch/executorch/actions/runs/40503300592/job/122409485714)，尚未建置 kernel；缺 archive 證據，已合併不代表 CI 全綠。 |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 完成 | 未開始 | 2026/11/03; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [77 項在 checkout 階段失敗](https://redirect.github.com/pytorch/executorch/pull/24126/checks)；[另五項仍缺終止根因](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925)，今日查無 artifacts，暫維持 25%。 |
| [Qwen3.5 prefill／WebGPU CI](https://redirect.github.com/pytorch/executorch/issues/18832) | 完成 | 完成 · [PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | 完成 | 完成 | 2026/11/03; CI fail: unknown; CI sucess: unknown; Require fix: 49% (false); Evidence: [PR 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)，但上游 CI 集合仍空；fork 僅見其他 App suites，無法恢復目前 CI 判斷。 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 · [fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) | 未開始 | 未開始 | 2026/11/03; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 · [fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) | 未開始 | 未開始 | 2026/11/03; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |

查核 head：embedding_bag `a62495a521`；avg_pool1d `b63d8204c9`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

可讀取的 CI 已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。
avg_pool1d 與 avg_pool3d 各有 1 個 skipped workflow；非 Actions Meta 檢查均成功，Dr.CI 為 neutral，未混入 workflow 數字。
embedding_bag 今日 workflow／check 清單為空；最後成功查核為 2026-11-02 04:12:36 Asia/Taipei，當時為 0 fail／3 success／27 action_required，這些是歷史結果。Qwen 目前也無法取得既有 CI，最後成功查核為 2026-10-31 04:12:10 Asia/Taipei。兩者以 unknown 表示今日無法重新確認；暫定 Require fix 評估的證據有限，不能據此認定 CI 通過或出現新失敗。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。日誌不足的歸因仍屬暫定。
