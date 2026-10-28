# ExecuTorch Result

批次：999984_2026-10-28_041102
報告日期：2026-10-28 Asia/Taipei
更新時間：2026-10-28 20:45:07 Asia/Taipei（新增選題；既有 PR 查核時間維持各列原紀錄）
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 2026/10/28; CI fail: 1; CI sucess: 21; Require fix: 1% (false); Evidence: [Windows x64](https://redirect.github.com/pytorch/executorch/actions/runs/40505751519/job/122409660717)在 kernel 編譯前因 SDK 解壓失敗；[base 腳本相同](https://redirect.github.com/pytorch/executorch/blob/a519331f4b70429520b5b7d9a5a7e85349bb49f2/.ci/scripts/build-qnn-windows-msvc.ps1)，ZIP 成因未明。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 受阻 | 完成 | 未開始 | 2026/10/28; CI fail: 1; CI sucess: 21; Require fix: 1% (false); Evidence: [Windows x64](https://redirect.github.com/pytorch/executorch/actions/runs/40503300592/job/122409485714)因 SDK 解壓停止，與[另一 PR](https://redirect.github.com/pytorch/executorch/actions/runs/40505751519/job/122409660717)同錯；ZIP 成因未明，仍有待核准工作。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 完成 | 未開始 | 2026/10/28; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [77 項 checkout 失敗](https://redirect.github.com/pytorch/executorch/pull/24126#issuecomment-6370631065)與 kernel 無直接路徑；Vulkan／ARM 有版本不相容證據，[QNN ARM64](https://redirect.github.com/pytorch/executorch/actions/runs/39994118583/job/120654117695)等仍缺終止診斷。 |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | 完成 | 完成 | 完成 | 完成 | 2026/10/28; CI fail: 0; CI sucess: 24; Require fix: 0% (false); Evidence: [WebGPU 第 3 次執行](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)已成功，目前無失敗，[PR 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)。 |
| [ExecuTorch issue 24125](https://redirect.github.com/pytorch/executorch/issues/24125) QNN 16a8w gather | 完成 | 進行中 | 未開始 | 未開始 | 2026/10/28; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未提交社群 PR。 |
| [ExecuTorch issue 22431](https://redirect.github.com/pytorch/executorch/issues/22431) Vulkan per-token INT8 | 完成 | 進行中 | 未開始 | 未開始 | 2026/10/28; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未提交社群 PR。 |

查核 head：embedding_bag `5b0f8ff477`；avg_pool1d `b63d8204c9`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

CI 已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。
embedding_bag：2 個 in_progress、1 個 skipped；avg_pool1d：1 個 action_required、1 個 in_progress、1 個 skipped；avg_pool3d：1 個 skipped；Qwen：1 個 skipped。非 Actions 的 Meta 檢查均成功，Dr.CI 為 neutral；embedding_bag 與 avg_pool1d 的 EasyCLA 成功，均未混入 workflow 數字。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。程式碼審查的修改要求另列於下表；傾向 false 不代表審查已通過。日誌不足的結論仍屬暫定。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false；mergeable=true。已更新 head；[先前審查](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6423738196)要求處理 padding 的 offset2bag 形狀、轉置 weight 與 max 最後一個 bag，尚無新的核准；待確認修正涵蓋全部要求並完成 CI。 | 2026-10-28 04:08:51 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | [ExecuTorch PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | PR 未 merge | Open；merged=false；mergeable=true。[新提交](https://redirect.github.com/pytorch/executorch/pull/24122/commits/b63d8204c90fc726efb487b7aa4145fc1df603df)已加入 ceil_mode 驗證修正與回歸測試，[作者已回覆審查](https://redirect.github.com/pytorch/executorch/pull/24122#issuecomment-6442195837)；尚待重新審查及 CI 完成，開發階段維持受阻。 | 2026-10-28 04:08:51 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | PR 未 merge | Open；merged=false；mergeable=true；尚無正式 review。82 個失敗 job 中，77 個在 checkout 階段失敗；Vulkan／ARM 有版本不相容證據，docs、NXP 與 QNN ARM64 仍缺終止日誌。待補足證據、處理 CI 與社群審查。 | 2026-10-28 04:08:51 Asia/Taipei |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | Done | 2026-10-27 03:29:11 Asia/Taipei 已合併；merged=true，merge commit `5c788db44c7`。原 issue 已關閉為 completed；[WebGPU 第 3 次執行成功](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)，目前 head 無失敗，保留完成追蹤。 | 2026-10-28 04:08:06 Asia/Taipei |
| [ExecuTorch issue 24125](https://redirect.github.com/pytorch/executorch/issues/24125) QNN 16a8w gather | 尚未提交 | 未發 PR | 已建立獨立分支及 tmux，等待首次資料夾信任確認。先查核最小重現與 QNN lowering；QAIRT 2.47 及相容裝置尚未確認，實機驗證待補。 | 2026-10-28 20:45:07 Asia/Taipei |
| [ExecuTorch issue 22431](https://redirect.github.com/pytorch/executorch/issues/22431) Vulkan per-token INT8 | 尚未提交 | 未發 PR | 已建立獨立分支及 tmux，等待首次資料夾信任確認。先查核 per-token activation 搭配 INT8 weight 的圖轉換、runtime 與測試缺口；尚無修正驗收結果。 | 2026-10-28 20:45:07 Asia/Taipei |
| avg_pool3d 標題與內容不符的已關閉 PR | [ExecuTorch PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) | PR 未 merge | 2026-10-24 01:19:54 Asia/Taipei 已關閉，merged=false；head `a7fd1d87e0`，實際為 max_pool3d_with_indices。最新 workflow 為 21 failure、3 success、1 action_required，失敗 run 沒有可列出的 job；保留此撤回提交，avg_pool3d 正式追蹤 PR 24126。 | 2026-10-28 04:08:51 Asia/Taipei |

追蹤來源：用戶指定的社群 PR 與上述實際選題。個人 fork PR 僅作為開發證據；Done 以對應社群 PR 的合併狀態為準。
