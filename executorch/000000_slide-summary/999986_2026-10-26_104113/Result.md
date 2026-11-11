# ExecuTorch Result

批次：999986_2026-10-26_104113
報告日期：2026-10-26 Asia/Taipei
更新時間：2026-10-26 12:22:32 Asia/Taipei（社群 CI 查核預覽；skill PR 111 尚未合併）
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。本週候選已依用戶要求改為 quantization／speculative decoding，等待用戶從 issue-disptach.pdf 指定議題；既有選題及 PR 追蹤維持不變。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 2026/10/26; CI fail: 0; CI sucess: 3; Require fix: 49% (false); Evidence: 22 項[待核准](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6177290334)，尚無實測失敗；僅極弱傾向不需修正。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 完成 | 完成 | 未開始 | 2026/10/26; CI fail: 2; CI sucess: 21; Require fix: 35% (false); Evidence: [核心 unit 通過](https://redirect.github.com/pytorch/executorch/actions/runs/39990873155/job/120584920448)；[6 項失敗](https://redirect.github.com/pytorch/executorch/pull/24122#issuecomment-6370185843)缺終止日誌，暫傾向環境問題。另 1 cancelled、1 skipped。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 完成 | 未開始 | 2026/10/26; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [77 項 checkout 環境錯誤](https://redirect.github.com/pytorch/executorch/pull/24126#issuecomment-6370631065)；[核心 unit 通過](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925/job/120654223347)，另 5 項根因待驗。另 1 skipped。 |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | 完成 | 完成 | 完成 | 未開始 | 2026/10/26; CI fail: 1; CI sucess: 23; Require fix: 5% (false); Evidence: 沿用同 job 查核：[Dawn／libstdc++ 連結錯誤](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894833)，傾向與 Python prefill 修改無關。另 1 skipped。 |

查核 head：embedding_bag `da781bd2aa`；avg_pool1d `e46a8ec574`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

計數口徑：目前 PR head 的 GitHub Actions workflow，每個 workflow/event 取最新 run 與 attempt；已分頁取得全部紀錄。未將 DrCI 彙總或 matrix job 重複計入；非 Actions 的外部檢查不納入此數字。`Require fix` 百分比為 executorch-dev 主觀估計「我們的修改需要修正」的機率；大於 50% 傾向 true，小於 50% 傾向 false，並非實測機率或 CI 通過率。

查核方式：executorch-dev 已完成失敗清單／錯誤、變更路徑／反證、同 head 成功 job／殘餘風險三輪查核與反思；詳細記錄留在內部。embedding_bag 尚待核准，沒有已執行失敗可作根因查核。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false。2026/10/26; CI fail: 0; CI sucess: 3; Require fix: 49% (false); Evidence: 22 項[待核准](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6177290334)，尚無實測失敗；僅極弱傾向不需修正。 | 2026-10-26 12:22:32 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | [ExecuTorch PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | PR 未 merge | Open；merged=false。2026/10/26; CI fail: 2; CI sucess: 21; Require fix: 35% (false); Evidence: [核心 unit 通過](https://redirect.github.com/pytorch/executorch/actions/runs/39990873155/job/120584920448)；[6 項失敗](https://redirect.github.com/pytorch/executorch/pull/24122#issuecomment-6370185843)缺終止日誌，暫傾向環境問題。另 1 cancelled、1 skipped。 | 2026-10-26 12:22:32 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | PR 未 merge | Open；merged=false。2026/10/26; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [77 項 checkout 環境錯誤](https://redirect.github.com/pytorch/executorch/pull/24126#issuecomment-6370631065)；[核心 unit 通過](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925/job/120654223347)，另 5 項根因待驗。另 1 skipped。 | 2026-10-26 12:22:32 Asia/Taipei |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；merged=false。2026/10/26; CI fail: 1; CI sucess: 23; Require fix: 5% (false); Evidence: 沿用同 job 查核：[Dawn／libstdc++ 連結錯誤](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894833)，傾向與 Python prefill 修改無關。另 1 skipped。 | 2026-10-26 12:22:32 Asia/Taipei |
| avg_pool3d 標題與內容不符的已關閉 PR | [ExecuTorch PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) | PR 未 merge | 已關閉、merged=false；head a7fd1d87e0，實際為 max_pool3d_with_indices。最新 workflow 計 21 failure、3 success、1 action_required；此為撤回的錯誤提交，不納入目前 avg_pool3d PR 24126 的因果判定。 | 2026-10-26 12:22:32 Asia/Taipei |


追蹤來源：用戶原指定兩個社群 PR，並於 2026-10-16、2026-10-21、2026-10-23 選定上列工作。pooling 社群 PR 均由 yenhao-huang 提交。個人 fork 的合併屬於開發證據；Done 僅用於已確認合併的社群 PR。
