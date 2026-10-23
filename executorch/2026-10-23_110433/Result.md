# ExecuTorch Result

批次：2026-10-23_110433
報告日期：2026-10-23 Asia/Taipei
更新時間：2026-10-23 11:04:33 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。其他候選仍未選定。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前進度與依據 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | [個人 fork PR 39](https://github.com/yenhao-huang/executorch/pull/39) 已於 2026-10-18 20:19:19 Asia/Taipei merge。既有驗證：commit 2dab1b7b03，27 項針對測試及 ASan／UBSan 通過；相鄰測試 104 通過、6 跳過。社群 PR head 為 9810885213，[用戶修正說明](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6250632981) 已刊登；目前仍待社群審查。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 完成 | 未開始 | 未開始 | [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42) 仍為 open，head 99dbda5fd5。既有驗證：33 個正式測試及 ASan／UBSan 通過。尚未找到用戶提交的對應社群 PR；等待用戶檢視與提交。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 未開始 | 未開始 | [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43) 仍為 open，head d2fc222dc2，依賴 PR 42 的共用 helper。既有驗證：36 個正式測試通過；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。先處理 PR 42，再同步並確認 3D 差異；等待用戶提交社群 PR。 |

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false；head 9810885213。尚無正式 review；本次回傳的 22 個 PR 工作流程中，21 success、1 skipped，[CI 留言](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6177290334) 也顯示此 head 無失敗。等待社群審查與合併。 | 2026-10-23 11:04:33 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 尚未確認有社群 PR | 未發 PR | [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42) 仍為 open，head 99dbda5fd5。既有驗證：33 個正式測試及 ASan／UBSan 通過。尚未找到用戶提交的對應社群 PR；等待用戶檢視與提交。本次未查到此 head 的 PR 工作流程或新留言。 | 2026-10-23 11:04:33 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 尚未確認有社群 PR | 未發 PR | [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43) 仍為 open，head d2fc222dc2，依賴 PR 42 的共用 helper。既有驗證：36 個正式測試通過；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。先處理 PR 42，再同步並確認 3D 差異；等待用戶提交社群 PR。本次未查到此 head 的 PR 工作流程或新留言。 | 2026-10-23 11:04:33 Asia/Taipei |
| Qwen3.5 static-shape prefill 修正 | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；merged=false；head 141ecd06a0。已有 [核准 review](https://redirect.github.com/pytorch/executorch/pull/21873#pullrequestreview-5432734557)，3 個審查討論均已解決；API 回報 mergeable=false，需處理合併衝突。本次回傳的 22 個 PR 工作流程中，20 success、1 failure、1 skipped；WebGPU models／operators 兩個工作在連結 Dawn 時缺少 `_M_replace_cold` 符號，詳見下方日誌證據。下一步確認 Dawn 與 C++ 標準函式庫的相容性、處理衝突並由用戶或維護者重跑 CI。 | 2026-10-23 11:04:33 Asia/Taipei |

Qwen3.5 CI 證據：[models 日誌](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894833)、[operators 日誌](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894851)。兩者先遇到 SwiftShader 快取下載 404，改以原始碼建置後繼續執行，最後在 `libwebgpu_dawn.a` 連結時失敗。工具鏈或函式庫版本不相容是待驗證方向。

追蹤來源：用戶指定追蹤兩個社群 PR；2026-10-16 選定 embedding_bag 審查修正，2026-10-21 選定 avg_pool1d、avg_pool3d。Qwen3.5 僅追蹤。個人 fork 的合併屬於開發證據；Done 僅用於已確認合併的社群 PR。
