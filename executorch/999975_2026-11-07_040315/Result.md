# ExecuTorch Result

批次：999975_2026-11-07_040315
報告日期：2026-11-07 Asia/Taipei
更新時間：2026-11-07 04:12:36 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。用戶於 2026-10-28 指示「這周選擇 03、04 開啟 tmux 幫我處理」，選定 10/26 批次的 issue 24125（QNN gather）及 issue 22431（Vulkan per-token INT8）；20:45 記錄，兩題均已確認仍為 open。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前社群 CI 情況 |
| --- | --- | --- | --- | --- | --- |
| [embedding_bag 審查修正](https://redirect.github.com/pytorch/executorch/issues/11323) | 完成 | 完成 · [PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | 完成 | 完成 | 2026/11/07; CI fail: 2; CI sucess: 26; Require fix: 1% (false); Evidence: Vulkan 缺指定套件，Android 解鎖失敗，皆早於測試；外部成因細節未明。[Vulkan](https://redirect.github.com/pytorch/executorch/actions/runs/42248087674/job/127997564522)／[Android](https://redirect.github.com/pytorch/executorch/actions/runs/42248087877/job/128004080397)。 |
| [avg_pool1d.out](https://redirect.github.com/pytorch/executorch/issues/11325) | 完成 | 完成 · [PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | 完成 | 完成 | 2026/11/07; CI fail: 1; CI sucess: 23; Require fix: 1% (false); Evidence: [QNN Windows 在 SDK 解壓與目錄檢查失敗](https://redirect.github.com/pytorch/executorch/actions/runs/40503300592/job/122409485714)，早於 kernel 建置；今日檢查輸出仍空、無產出檔案，壓縮檔問題的根因未解。 |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | 完成 | 完成 · [PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | 完成 | 未開始 | 2026/11/07; CI fail: 10; CI sucess: 14; Require fix: 25% (false); Evidence: [82 個失敗 job](https://redirect.github.com/pytorch/executorch/pull/24126/checks)中 77 個止於 checkout；[另五項](https://redirect.github.com/pytorch/executorch/actions/runs/39994118925)的檢查輸出仍空白，失敗原因尚未確認。 |
| [Qwen3.5 prefill／WebGPU CI](https://redirect.github.com/pytorch/executorch/issues/18832) | 完成 | 完成 · [PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | 完成 | 完成 | 2026/11/07; CI fail: unknown; CI sucess: unknown; Require fix: 49% (false); Evidence: [Qwen 已合併](https://redirect.github.com/pytorch/executorch/pull/21873)，但今日 workflow／check 清單仍為空；保留 10/31 最後成功查核紀錄，今日 CI 無法重新確認。 |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 完成 | 受阻 · [fork PR 45](https://github.com/yenhao-huang/executorch/pull/45) | 未開始 | 未開始 | 2026/11/07; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 完成 | 完成 · [fork PR 46](https://github.com/yenhao-huang/executorch/pull/46) | 未開始 | 未開始 | 2026/11/07; CI fail: n/a; CI sucess: n/a; Require fix: n/a; Evidence: 尚未查得對應社群 PR；個人 fork PR 僅作開發證據。 |

查核 head：embedding_bag `20caea0b83`；avg_pool1d `b63d8204c9`；avg_pool3d `c3b08504f2`；Qwen `141ecd06a0`。

可讀取的 CI 已讀完所有分頁，以目前 head 的 Actions workflow 為單位，每個 workflow/event 只取最新 run／attempt；不重複計算 matrix job 或 Dr.CI 彙總。
embedding_bag、avg_pool1d 與 avg_pool3d 各有 1 個 skipped workflow；非 Actions Meta 檢查與 embedding_bag 的 EasyCLA status 均成功，Dr.CI 為 neutral，未混入 workflow 數字。
Qwen 今日 workflow／check 清單仍為空；最後成功查核為 2026-10-31 04:12:10 Asia/Taipei，當時為 0 fail／24 success／1 skipped。今日 CI 無法重新確認，以 unknown 表示；暫定 Require fix 的證據有限，不能據此認定 CI 通過或出現新失敗。

`Require fix` 是 executorch-dev 對「至少一項目前 CI 失敗需要修改本 PR」的主觀估計，並非 CI 通過率。日誌不足的歸因仍屬暫定。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [embedding_bag 審查修正](https://redirect.github.com/pytorch/executorch/issues/11323) | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | Done | 2026-11-07 03:19:54 Asia/Taipei 已合併；merged=true，merge commit `a0d6be8f7ae`；[最新審查已核准](https://redirect.github.com/pytorch/executorch/pull/23871#pullrequestreview-5805723618)，原 issue 已關閉為 completed。新 head `20caea0b83` 仍有 Vulkan 與 Android CI 失敗，歸因見上表；保留失敗紀錄。 | 2026-11-07 04:07:41 Asia/Taipei |
| [avg_pool1d.out](https://redirect.github.com/pytorch/executorch/issues/11325) | [ExecuTorch PR 24122](https://redirect.github.com/pytorch/executorch/pull/24122) | Done | 2026-10-28 23:36:23 Asia/Taipei 已合併；merged=true，merge commit `a6390b4cc5e`；[審查已核准](https://redirect.github.com/pytorch/executorch/pull/24122#pullrequestreview-5685355024)，原 issue 已關閉為 completed。保留目前 head 的 Windows QNN 失敗紀錄，合併不代表所有 CI 均成功。 | 2026-11-07 04:07:41 Asia/Taipei |
| [avg_pool3d.out](https://redirect.github.com/pytorch/executorch/issues/11326) | [ExecuTorch PR 24126](https://redirect.github.com/pytorch/executorch/pull/24126) | PR 未 merge | Open；merged=false；mergeable=false；尚無正式 review。82 個失敗 job 的原因與限制見上表；待處理合併衝突、補足 CI 證據及完成社群審查。 | 2026-11-07 04:07:41 Asia/Taipei |
| [Qwen3.5 prefill／WebGPU CI](https://redirect.github.com/pytorch/executorch/issues/18832) | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | Done | 2026-10-27 03:29:11 Asia/Taipei 已合併；merged=true，merge commit `5c788db44c7`，原 issue 已關閉為 completed。今日 head 的 workflow／check 清單仍為空，CI 無法重新確認；保留最後成功查核的 0 fail／24 success／1 skipped 與 [WebGPU attempt 3 成功紀錄](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/attempts/3)。 | PR：2026-11-07 04:07:41 Asia/Taipei；CI 最後成功：2026-10-31 04:12:10 Asia/Taipei |
| [QNN 16a8w gather](https://redirect.github.com/pytorch/executorch/issues/24125) | 尚未查得 | 未發 PR | [個人 fork PR 45](https://github.com/yenhao-huang/executorch/pull/45)的 `214feb698e` 已通過 Claude CLI 完整審查，無待修發現；修正 LPAI 被誤套 GatherNd 的回歸，並補重複／靜態索引測試。[驗收報告](https://github.com/yenhao-huang/executorch/blob/214feb698e774626456546b1e942cc6d185cf714/docs/howard/24125.md)記錄 QAIRT 2.47／2.51 HTP 模擬器相對 L2 誤差由 0.7683 降至 0.001664。實體 SM8850／HTPv81 驗收仍受阻；fork 未回報 CI checks，Claude ACCEPT 不代表實機或社群驗收。 | 2026-11-07 04:04:10 Asia/Taipei |
| [Vulkan per-token INT8](https://redirect.github.com/pytorch/executorch/issues/22431) | 尚未查得 | 未發 PR | [個人 fork PR 46](https://github.com/yenhao-huang/executorch/pull/46)的最終版本 `11d7b00408` 已於 2026-10-29 13:53 Asia/Taipei 通過 Claude CLI 完整審查，無待修的已確認問題；修正涵蓋 FP16、大 token dispatch、共用 Q/DQ 與既有 allowlist 融合回歸。[驗收報告](https://github.com/yenhao-huang/executorch/blob/11d7b004085896ba69c31030862c5ab1c199da20/docs/howard/22431.md)記錄 72 項 Vulkan／WebGPU Python 測試通過，另保留 32 組 INT8 C++ 案例證據。僅驗證 llvmpipe；實體 GPU、WebGPU native、encoder 品質與延遲未測，fork 無 CI checks。Claude ACCEPT 不等於社群核准或合併。 | 2026-11-07 04:04:10 Asia/Taipei |
| avg_pool3d 標題與內容不符的已關閉 PR | [ExecuTorch PR 24123](https://redirect.github.com/pytorch/executorch/pull/24123) | PR 未 merge | 2026-10-24 01:19:54 Asia/Taipei 已關閉，merged=false；head `a7fd1d87e0`，實際為 max_pool3d_with_indices。最新 workflow 為 21 failure、3 success、1 action_required，失敗 run 沒有可列出的 job，根因仍不明，Require fix 暫定 49% (false)；保留此撤回提交，avg_pool3d 正式追蹤 PR 24126。 | 2026-11-07 04:07:41 Asia/Taipei |

追蹤來源：用戶指定的社群 PR 與上述實際選題。個人 fork PR 僅作為開發證據；Done 以對應社群 PR 的合併狀態為準。
