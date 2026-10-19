# ExecuTorch Result

批次：2026-10-20_071218
更新時間：2026-10-20 07:35:09 Asia/Taipei
報告日期：2026-10-20 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。其他候選仍未選定。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前進度與依據 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 已提交 [個人 fork PR 39](https://github.com/yenhao-huang/executorch/pull/39)，commit 2dab1b7b03。27 項針對測試及 ASan/UBSan 通過；相鄰測試 104 通過、6 跳過。個人 fork PR 39 已於 2026-10-18 20:19:19 Asia/Taipei merge（僅屬開發證據）；社群 PR 已更新至 head 9810885213，[用戶修正說明](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6250632981) 已刊登，本次檢查 CI 無失敗，等待審查；未代送任何社群操作。 |

四階段依序為「選擇 issue → issue 開發 → 用戶在社群寄送 PR → 該 PR 被 merge」。用戶選定後才新增資料列，狀態使用未開始、進行中、完成、受阻或待確認；阻礙與下一步記在同一列，不另增階段。

個人 fork PR 屬於 issue 開發；用戶送出的社群 PR 才算第三階段。第四階段必須確認同一社群 PR 已 merge，不能以 closed 或個人 fork merge 代替。社群 PR 由用戶手動送出，技能只做唯讀查核。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| Portable kernel：_embedding_bag.out | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；head 9810885213；reviewDecision=REVIEW_REQUIRED。已收到用戶修正更新；本次 CI 查核 203 success、35 skipped、1 neutral，無失敗項。下一步等待社群審查；尚未 merge。 | 2026-10-20 07:35:09 Asia/Taipei |
| Qwen3.5 static-shape prefill 修正 | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；head d2bc53d2b0；reviewDecision=APPROVED，尚未 merge。本次 statusCheckRollup 為空；[CI 留言](https://redirect.github.com/pytorch/executorch/pull/21873#issuecomment-5302859487) 顯示目前 head 有 21 個工作流程等待核准。下一步等待維護者核准 CI，再追蹤合併；不沿用先前 CI 計數。 | 2026-10-20 07:35:09 Asia/Taipei |

追蹤來源：用戶指定追蹤兩個 PR，並於 2026-10-16 明確授權 embedding_bag 的審查修正；Qwen3.5 僅追蹤。
進度僅使用「未發 PR／PR 未 merge／Done」；Done 必須確認社群 PR 已 merge。審查核准或 CI 成功不等於 Done，closed 未 merge 仍記為 PR 未 merge。
