# ExecuTorch Result

批次：999996_2026-10-18_040002
更新時間：2026-10-18 04:00:02 Asia/Taipei
報告日期：2026-10-18 Asia/Taipei
前次紀錄：[前次 Result.md](https://github.com/yenhao-huang/daily/blob/main/executorch/999997_2026-10-17_040002/Result.md)
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。其他候選仍未選定。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前進度與依據 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 已提交 [個人 fork PR 39](https://github.com/yenhao-huang/executorch/pull/39)，commit 2dab1b7b03。27 項針對測試及 ASan/UBSan 通過；相鄰測試 104 通過、6 跳過。待用戶套用至既有社群 PR 並完成 CI 驗證；未代送任何社群操作。 |

四階段依序為「選擇 issue → issue 開發 → 用戶在社群寄送 PR → 該 PR 被 merge」。用戶選定後才新增資料列，狀態使用未開始、進行中、完成、受阻或待確認；阻礙與下一步記在同一列，不另增階段。

個人 fork PR 屬於 issue 開發；用戶送出的社群 PR 才算第三階段。第四階段必須確認同一社群 PR 已 merge，不能以 closed 或個人 fork merge 代替。社群 PR 由用戶手動送出，技能只做唯讀查核。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| Portable kernel：_embedding_bag.out | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；尚未 merge，持續追蹤審查與合併狀態。〔前次紀錄：2026-10-16 13:46:07 Asia/Taipei；已完成本機審查修正，見 [fork PR 39](https://github.com/yenhao-huang/executorch/pull/39)。社群 PR head 仍為 4d616fec1b；待用戶套用並重跑 CI。原 lint 格式已修正；NXP 失敗為 GitLab 過載造成 Eigen clone 失敗。〕 | 2026-10-18 04:00:02 Asia/Taipei |
| Qwen3.5 static-shape prefill 修正 | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；尚未 merge，持續追蹤審查與合併狀態。〔前次紀錄：2026-10-15 16:04:14 Asia/Taipei；Open；reviewDecision=APPROVED。檢查摘要：198 success、30 skipped、1 neutral；尚未 merge，持續追蹤合併狀態。〕 | 2026-10-18 04:00:02 Asia/Taipei |

追蹤來源：用戶指定追蹤兩個 PR，並於 2026-10-16 明確授權 embedding_bag 的審查修正；Qwen3.5 僅追蹤。
進度僅使用「未發 PR／PR 未 merge／Done」；Done 必須確認社群 PR 已 merge。審查核准或 CI 成功不等於 Done，closed 未 merge 仍記為 PR 未 merge。
