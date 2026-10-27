# ExecuTorch Result

批次：999985_2026-10-27_041746
報告日期：2026-10-27 Asia/Taipei
更新時間：2026-10-27 04:17:46 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 2026/10/27; CI fail: 2; CI sucess: 22; Require fix: 5% (false); Evidence: [serving 測試斷言](https://redirect.github.com/pytorch/executorch/actions/runs/40264497846/job/121665658588)與 [KleidiAI 下載中斷](https://redirect.github.com/pytorch/executorch/actions/runs/40264497789/job/121665499031)傾向既有問題，仍有因果缺口。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 受阻 | 完成 | 未開始 | 2026/10/27; CI fail: 2; CI sucess: 21; Require fix: 5% (false); Evidence: [Vulkan](https://redirect.github.com/pytorch/executorch/actions/runs/40359376127/job/121758470625)等多項失敗涉及 workflow／checkout 版本不一致；[其餘失敗](https://redirect.github.com/pytorch/executorch/pull/24122#issuecomment-6370185843)中 emulator、NXP 仍待釐清。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 完成 | 未開始 | 2026/10/27; CI fail: 10; CI sucess: 14; Require fix: 30% (false); Evidence: [77 項 checkout 錯誤](https://redirect.github.com/pytorch/executorch/pull/24126#issuecomment-6370631065)傾向環境問題；舊日誌過期，[QNN ARM64](https://redirect.github.com/pytorch/executorch/actions/runs/39994118583/job/120654117695)等 5 項仍待釐清。 |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | 完成 | 完成 | 完成 | 完成 | 2026/10/27; CI fail: 0; CI sucess: 24; Require fix: 0% (false); Evidence: [WebGPU 第 3 次執行](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)已成功，目前無失敗，[社群 PR 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)。 |

查核 head：embedding_bag `da781bd2aa`；avg_pool1d `3266d77918`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

CI 計數已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。上述四個 PR 各另有 1 個 skipped；avg_pool1d 另有 1 個 periodic 待核准。非 Actions 的 Meta 檢查均成功，Dr.CI 為 neutral；另查得 embedding_bag 與 avg_pool1d 的 EasyCLA 成功，均未混入 workflow 數字。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。程式碼審查的修改要求另列於下表；傾向 false 不代表審查已通過。日誌不足的結論仍屬暫定。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false；mergeable=true。[最新審查](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6423738196)要求修正 sum 含 padding 時的 offset2bag 形狀、轉置 weight 存取與 max 最後一個 bag 的行為，並補測試；目前為 CHANGES_REQUESTED，待處理審查與 CI。 | 2026-10-27 04:11:27 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | [ExecuTorch PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | PR 未 merge | Open；merged=false；mergeable=true。新 head 已更新先前註解；[最新審查](https://redirect.github.com/pytorch/executorch/pull/24122#pullrequestreview-5657257545)指出 L=3、k=6、s=2、p=1、ceil_mode=true 應產生 1 個輸出，目前被拒絕，要求修正與回歸測試。[維護者另要求處理 CI](https://redirect.github.com/pytorch/executorch/pull/24122#issuecomment-6425672404)；開發階段改列受阻，待完成修改。 | 2026-10-27 04:11:27 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | PR 未 merge | Open；merged=false；mergeable=true；尚無正式 review。現有 82 個失敗 job 中，77 個在 checkout 階段失敗，另 5 個仍需釐清；待取得缺少的日誌、處理失敗及社群審查。 | 2026-10-27 04:11:27 Asia/Taipei |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | Done | 2026-10-27 03:29:11 Asia/Taipei 已合併；merged=true，merge commit `5c788db44c7`。原 issue 也已關閉為 completed。[WebGPU 第 3 次執行成功](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)，目前 head 無失敗；保留完成追蹤。 | 2026-10-27 04:11:27 Asia/Taipei |
| avg_pool3d 標題與內容不符的已關閉 PR | [ExecuTorch PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) | PR 未 merge | 2026-10-24 01:19:54 Asia/Taipei 已關閉，merged=false；head `a7fd1d87e0`，實際為 max_pool3d_with_indices。最新 workflow 為 21 failure、3 success、1 action_required，失敗 run 沒有可列出的 job；保留此撤回提交，avg_pool3d 正式追蹤 PR 24126。 | 2026-10-27 04:11:27 Asia/Taipei |

追蹤來源：用戶指定的社群 PR 與上述實際選題。個人 fork PR 僅作為開發證據；Done 以對應社群 PR 的合併狀態為準。
