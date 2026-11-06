# ExecuTorch Result

批次：999980_2026-11-01_040255
報告日期：2026-11-01 Asia/Taipei
更新時間：2026-11-01 04:10:12 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [embedding_bag 審查修正](https://redirect.github.com/pytorch/executorch/issues/11323) | 完成 | 進行中 · [PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | 完成 | 未開始 | 2026/11/01; CI fail: 0; CI sucess: 3; Require fix: 20% (false); Evidence: [新 head 已修舊 lint 與 dtype 問題](https://redirect.github.com/pytorch/executorch/compare/15eecb9d5b83feb69762e47f571e3d9d507bbde0...a62495a521f42582418cb453f662595a339fd323)；[27 項待核准](https://redirect.github.com/pytorch/executorch/pull/23871/checks)，動態 BF16 與 ATen 測試仍待驗證。 |
| [avg_pool1d.out](https://redirect.github.com/pytorch/executorch/issues/11325) | 完成 | 完成 · [PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | 完成 | 完成 | 2026/11/01; CI fail: 1; CI sucess: 23; Require fix: 1% (false); Evidence: [SDK 解壓失敗](https://redirect.github.com/pytorch/executorch/actions/runs/40503300592/job/122409485714)先於編譯；[安裝腳本](https://redirect.github.com/pytorch/executorch/blob/b63d8204c90fc726efb487b7aa4145fc1df603df/.ci/scripts/build-qnn-windows-msvc.ps1)無內容校驗，亦無 GitHub artifacts，仍缺舊 ZIP。 |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 完成 | 未開始 | 2026/11/01; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [82 個失敗 job](https://redirect.github.com/pytorch/executorch/pull/24126/checks)中有 77 個在 checkout 失敗；其餘 5 個仍缺終止診斷，[Vulkan／ARM](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925/attempts/2)的重試恢復假說尚未證實。 |
| [Qwen3.5 prefill／WebGPU CI](https://redirect.github.com/pytorch/executorch/issues/18832) | 完成 | 完成 · [PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | 完成 | 完成 | 2026/11/01; CI fail: unknown; CI sucess: unknown; Require fix: 49% (false); Evidence: [PR 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)，目前 CI 集合空、[舊 run 回 404](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015)；0 失敗／24 成功／1 skipped 與 0% 僅為歷史。 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 · [fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) | 未開始 | 未開始 | 2026/11/01; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 · [fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) | 未開始 | 未開始 | 2026/11/01; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |

查核 head：embedding_bag `a62495a521`；avg_pool1d `b63d8204c9`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

可讀取的 CI 已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。
embedding_bag 有 27 個 action_required workflow；3 個成功結果尚不足以驗證 kernel。avg_pool1d 與 avg_pool3d 各有 1 個 skipped workflow。這三個 PR 的非 Actions Meta 檢查均成功，Dr.CI 為 neutral；embedding_bag 的 EasyCLA status 也成功，均未混入 workflow 數字。Qwen 今日無法取得既有 CI，最後成功查核為 2026-10-31 04:12:10 Asia/Taipei；上表 unknown 表示無法重新確認，目前 Require fix 為證據不足下的 49% 暫定評估，並非發現新失敗；歷史 0% 僅代表當時結果。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。日誌不足的歸因仍屬暫定。
