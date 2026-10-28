# ExecuTorch Result

批次：999983_2026-10-29_041240
報告日期：2026-10-29 Asia/Taipei
更新時間：2026-10-29 04:12:40 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 2026/10/29; CI fail: 1; CI sucess: 23; Require fix: 1% (false); Evidence: [Windows x64](https://redirect.github.com/pytorch/executorch/actions/runs/40505751519/job/122409660717)仍是同次 SDK 解壓失敗，發生於編譯前；[base 腳本相同](https://redirect.github.com/pytorch/executorch/blob/a519331f4b70429520b5b7d9a5a7e85349bb49f2/.ci/scripts/build-qnn-windows-msvc.ps1)，ZIP 成因未明。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 完成 | 完成 | 完成 | 2026/10/29; CI fail: 1; CI sucess: 23; Require fix: 1% (false); Evidence: [PR 已合併](https://redirect.github.com/pytorch/executorch/pull/24122)，但[同次 x64 失敗](https://redirect.github.com/pytorch/executorch/actions/runs/40503300592/job/122409485714)仍在；SDK 解壓早於 kernel 編譯，ZIP 成因未明。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 完成 | 未開始 | 2026/10/29; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: 77 項 checkout 失敗；[Vulkan／ARM](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925/attempts/2)含依賴與憑證錯誤，版本不相容未確診；[QNN ARM64](https://redirect.github.com/pytorch/executorch/actions/runs/39994118583/job/120654117695)等缺終止診斷。 |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | 完成 | 完成 | 完成 | 完成 | 2026/10/29; CI fail: 0; CI sucess: 24; Require fix: 0% (false); Evidence: [WebGPU attempt 3](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)仍成功，目前無失敗，[PR 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)。 |
| [ExecuTorch issue 24125](https://redirect.github.com/pytorch/executorch/issues/24125) QNN 16a8w gather | 完成 | 受阻 | 未開始 | 未開始 | 2026/10/29; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |
| [ExecuTorch issue 22431](https://redirect.github.com/pytorch/executorch/issues/22431) Vulkan per-token INT8 | 完成 | 完成 | 未開始 | 未開始 | 2026/10/29; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |

查核 head：embedding_bag `5b0f8ff477`；avg_pool1d `b63d8204c9`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

CI 已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。
上述四個社群 PR 各有 1 個 skipped workflow，沒有執行中或待核准的 workflow。非 Actions 的 Meta 檢查均成功，Dr.CI 為 neutral；embedding_bag 與 avg_pool1d 的 EasyCLA 成功，均未混入 workflow 數字。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。程式碼審查要求另列於下表；日誌不足的歸因仍屬暫定。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false；mergeable=true。[先前審查](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6423738196)要求修正 padding 的 offset2bag 形狀、轉置 weight 與 max 最後一個 bag；目前仍無新的核准。待確認現有提交涵蓋全部要求並完成審查；Windows QNN 失敗歸因見上表。 | 2026-10-29 04:12:40 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | [ExecuTorch PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | Done | 2026-10-28 23:36:23 Asia/Taipei 已合併；merged=true，merge commit `a6390b4cc5e`；[審查已核准](https://redirect.github.com/pytorch/executorch/pull/24122#pullrequestreview-5685355024)，原 issue 已關閉為 completed。保留目前 head 的 Windows QNN 失敗紀錄，合併不代表所有 CI 均成功。 | 2026-10-29 04:12:40 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | PR 未 merge | Open；merged=false；mergeable=false；尚無正式 review。82 個失敗 job 的原因與限制見上表；待處理合併衝突、補足 CI 證據及完成社群審查。 | 2026-10-29 04:12:40 Asia/Taipei |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | Done | 2026-10-27 03:29:11 Asia/Taipei 已合併；merged=true，merge commit `5c788db44c7`。原 issue 已關閉為 completed；[WebGPU 第 3 次執行成功](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)，目前 head 無失敗，保留完成追蹤。 | 2026-10-29 04:12:40 Asia/Taipei |
| [ExecuTorch issue 24125](https://redirect.github.com/pytorch/executorch/issues/24125) QNN 16a8w gather | 尚未查得 | 未發 PR | [個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45)已提交；[驗收報告](https://github.com/yenhao-huang/executorch/blob/6348763a18dd5511b293cbbe87fa7315c8930888/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664，回歸與相鄰測試通過。實體 SM8850／HTPv81 驗收仍受阻，待取得裝置驗證。 | 2026-10-29 04:12:40 Asia/Taipei |
| [ExecuTorch issue 22431](https://redirect.github.com/pytorch/executorch/issues/22431) Vulkan per-token INT8 | 尚未查得 | 未發 PR | [個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46)已提交；[驗收報告](https://github.com/yenhao-huang/executorch/blob/00f4af4228501c60ca97b4cf036d3d0ae459013e/docs/howard/22431.md)記錄六項必要驗收完成，含 40 組序列化 runtime 與 16 組 C++ 案例。驗證使用 llvmpipe 軟體 Vulkan；實體 GPU、encoder 品質與延遲尚未測量，待用戶審閱及決定社群提交。 | 2026-10-29 04:12:40 Asia/Taipei |
| avg_pool3d 標題與內容不符的已關閉 PR | [ExecuTorch PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) | PR 未 merge | 2026-10-24 01:19:54 Asia/Taipei 已關閉，merged=false；head `a7fd1d87e0`，實際為 max_pool3d_with_indices。最新 workflow 為 21 failure、3 success、1 action_required，失敗 run 沒有可列出的 job；保留此撤回提交，avg_pool3d 正式追蹤 PR 24126。 | 2026-10-29 04:12:40 Asia/Taipei |

追蹤來源：用戶指定的社群 PR 與上述實際選題。個人 fork PR 僅作為開發證據；Done 以對應社群 PR 的合併狀態為準。
