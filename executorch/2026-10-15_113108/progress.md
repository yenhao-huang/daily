# ExecuTorch 管理流程初始化

時區：Asia/Taipei。

- 已建立 executorch-pm 與 executorch-dev；沒有 executorch-notice。
- 每週一 04:00：收集 20 個候選 issues，等待使用者選定，再交給 executorch-dev。
- 每天 04:00：唯讀檢查 PR 與 CI、review 進度，只對有意義的變化通知。
- 排程狀態：not_enabled。目前沒有可用的 Codex automation 設定工具。
- 本次僅初始化設定，尚未執行候選收集或 PR 檢查，也未開始任何 issue 開發。
- 社群留言模板只可起草，禁止發送；社群 repository 禁止直接寫入與間接 cross-reference。
- 開發 PR 限 yenhao-huang/executorch；進度與資料限 yenhao-huang/daily。
- dev 複製來源：mcp-skills-package commit cfda1628e8df56bc177f05599d90121413cf6e06 的 solve-issue，保留授權，等待後續特化。

本目錄是初始化紀錄，不是每週候選批次。首次收集時另建時間目錄與 selection.json。
