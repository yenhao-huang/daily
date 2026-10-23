# ExecuTorch Result

批次：2026-10-23_110433
報告日期：2026-10-23 Asia/Taipei
更新時間：2026-10-23 11:27:10 Asia/Taipei
選擇紀錄：用戶於 2026-10-16 在本對話指示「開始處理問題」，授權處理 embedding_bag 審查修正（原 issue 11323／社群 PR 23871）。用戶於 2026-10-21 明確指示「決定實作 avg_pool1d、avg_pool3d」，新增 issue 11325／11326。用戶於 2026-10-23 在討論 Dawn 連結失敗後指示「處理問題」，授權 Qwen3.5 的 WebGPU CI 修復。其他候選仍未選定。

| 選擇的 issue | 選擇 issue | issue 開發 | 用戶在社群寄送 PR | 該 PR 被 merge | 目前進度與依據 |
| --- | --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | 完成 | 進行中 | 完成 | 未開始 | [個人 fork PR 39](https://github.com/yenhao-huang/executorch/pull/39) 已於 2026-10-18 20:19:19 Asia/Taipei merge。既有驗證：commit 2dab1b7b03，27 項針對測試及 ASan／UBSan 通過；相鄰測試 104 通過、6 跳過。社群 PR head 為 9810885213，[用戶修正說明](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6250632981) 已刊登；目前仍待社群審查。 |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 完成 | 完成 | 未開始 | 未開始 | [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42) 仍為 open，head 99dbda5fd5。既有驗證：33 個正式測試及 ASan／UBSan 通過。尚未找到用戶提交的對應社群 PR；等待用戶檢視與提交。 |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 完成 | 完成 | 未開始 | 未開始 | [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43) 仍為 open，head d2fc222dc2，依賴 PR 42 的共用 helper。既有驗證：36 個正式測試通過；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。先處理 PR 42，再同步並確認 3D 差異；等待用戶提交社群 PR。 |

| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | 完成 | 完成 | 完成 | 未開始 | WebGPU CI 修復已交付 [個人 fork PR 44](https://github.com/yenhao-huang/executorch/pull/44)，commit 1ab6777。6 個回歸測試通過；固定版本 Dawn 的連結與 instance 建立測試通過。原社群 PR 已存在；這次 CI 修復尚未整合至其分支，完整 models／operators CI 尚待重跑。 |

## PR 追蹤表

| 追蹤項目 | 社群 PR | 進度 | 目前狀況／下一步 | 查核時間 |
| --- | --- | --- | --- | --- |
| [ExecuTorch issue 11323](https://redirect.github.com/pytorch/executorch/issues/11323) 審查修正 | [ExecuTorch PR 23871](https://redirect.github.com/pytorch/executorch/pull/23871) | PR 未 merge | Open；merged=false；head 9810885213。尚無正式 review；本次回傳的 22 個 PR 工作流程中，21 success、1 skipped，[CI 留言](https://redirect.github.com/pytorch/executorch/pull/23871#issuecomment-6177290334) 也顯示此 head 無失敗。等待社群審查與合併。 | 2026-10-23 11:04:33 Asia/Taipei |
| [ExecuTorch issue 11325](https://redirect.github.com/pytorch/executorch/issues/11325) avg_pool1d.out | 尚未確認有社群 PR | 未發 PR | [個人 fork PR 42](https://github.com/yenhao-huang/executorch/pull/42) 仍為 open，head 99dbda5fd5。既有驗證：33 個正式測試及 ASan／UBSan 通過。尚未找到用戶提交的對應社群 PR；等待用戶檢視與提交。本次未查到此 head 的 PR 工作流程或新留言。 | 2026-10-23 11:04:33 Asia/Taipei |
| [ExecuTorch issue 11326](https://redirect.github.com/pytorch/executorch/issues/11326) avg_pool3d.out | 尚未確認有社群 PR | 未發 PR | [個人 fork PR 43](https://github.com/yenhao-huang/executorch/pull/43) 仍為 open，head d2fc222dc2，依賴 PR 42 的共用 helper。既有驗證：36 個正式測試通過；sanitizer 首次啟動異常，原 binary 重跑 36 個測試通過。先處理 PR 42，再同步並確認 3D 差異；等待用戶提交社群 PR。本次未查到此 head 的 PR 工作流程或新留言。 | 2026-10-23 11:04:33 Asia/Taipei |
| [ExecuTorch issue 18832](https://redirect.github.com/pytorch/executorch/issues/18832) Qwen3.5 prefill／WebGPU CI | [ExecuTorch PR 21873](https://redirect.github.com/pytorch/executorch/pull/21873) | PR 未 merge | Open；merged=false；head 141ecd06a0；本次確認 mergeable=true。已有核准 review，3 個審查討論已解決。WebGPU 的 `_M_replace_cold` 連結問題已在 [個人 fork PR 44](https://github.com/yenhao-huang/executorch/pull/44) 修正並通過本機驗證；fork PR 為 open、可合併，未啟動 CI。待檢視修復並整合至原分支，再由用戶或維護者重跑完整 CI；原社群 CI 的失敗狀態尚未解除。 | 2026-10-23 11:27:10 Asia/Taipei |

Qwen3.5 CI 證據：[models 日誌](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894833)、[operators 日誌](https://redirect.github.com/pytorch/executorch/actions/runs/39601542015/job/119424894851)。兩者先遇到 SwiftShader 快取下載 404，改以原始碼建置後繼續執行，最後在 `libwebgpu_dawn.a` 連結時失敗。已確認 PPA 503 使系統 runtime 停留在舊版，而連結器未選用 Conda 新版 runtime；本機使用同一 Dawn archive 已重現並驗證修復。

追蹤來源：用戶指定追蹤兩個社群 PR；2026-10-16 選定 embedding_bag 審查修正，2026-10-21 選定 avg_pool1d、avg_pool3d。2026-10-23 另選定 Qwen3.5 的 WebGPU CI 修復。個人 fork 的合併屬於開發證據；Done 僅用於已確認合併的社群 PR。
