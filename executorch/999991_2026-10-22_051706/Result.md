# ExecuTorch Result

批次：999991_2026-10-22_051706
更新時間：2026-10-22 05:17:06 Asia/Taipei
報告日期：2026-10-22 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。其他候選仍未選定。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前進度與依據 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | 已提交 [個人 fork PR 39](https://github.com/yenhao-huang/executorch/pull/39)，commit 2dab1b7b03。27 項針對測試及 ASan/UBSan 通過；相鄰測試 104 通過、6 跳過。個人 fork PR 39 已於 2026-10-18 20:19:19 Asia/Taipei merge（僅屬開發證據）；社群 PR 已更新至 head 9810885213，[用戶修正說明](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6250632981) 已刊登，本次檢查 CI 無失敗，等待審查；未代送任何社群操作。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 完成 | 未開始 | 未開始 | 已拆成獨立 [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42)；33 個正式測試通過。ASan／UBSan 同樣通過；等待檢視與社群提交。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 未開始 | 未開始 | 已拆成獨立 [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43)；36 個正式測試通過。依賴 PR 42 的共用 helper，須先處理 PR 42；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。 |

四階段依序為「選擇 issue → issue 開發 → 用戶在社群寄送 PR → 該 PR 被 merge」。用戶選定後才新增資料列，狀態使用未開始、進行中、完成、受阻或待確認；阻礙與下一步記在同一列，不另增階段。

個人 fork PR 屬於 issue 開發；用戶送出的社群 PR 才算第三階段。第四階段必須確認同一社群 PR 已 merge，不能以 closed 或個人 fork merge 代替。社群 PR 由用戶手動送出，技能只做唯讀查核。

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；head 9810885213；待審查。本次 CI：202 success、35 skipped、1 neutral，無失敗項；等待審查與合併。 | 2026-10-22 05:17:06 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 尚未送出 | 未發 PR | 已拆成獨立 [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42)；33 個正式測試通過。ASan／UBSan 同樣通過；等待檢視與社群提交。 | 2026-10-22 05:17:06 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 尚未送出 | 未發 PR | 已拆成獨立 [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43)；36 個正式測試通過。依賴 PR 42 的共用 helper，須先處理 PR 42；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。 | 2026-10-22 05:17:06 Asia/Taipei |
| Qwen3.5 static-shape prefill 修正 | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；head d2bc53d2b0；已獲核准，尚未 merge。本次 CI：197 success、38 skipped、2 failure、1 neutral。WebGPU 的 models／operators Linux jobs 失敗，下一步確認失敗原因後再追蹤合併。 | 2026-10-22 05:17:06 Asia/Taipei |

追蹤來源：用戶指定追蹤兩個 PR，並於 2026-10-16 明確授權 embedding_bag 的審查修正；Qwen3.5 僅追蹤；2026-10-21 新增用戶選定的 avg_pool1d、avg_pool3d。
進度僅使用「未發 PR／PR 未 merge／Done」；Done 必須確認社群 PR 已 merge。審查核准或 CI 成功不等於 Done，closed 未 merge 仍記為 PR 未 merge。
