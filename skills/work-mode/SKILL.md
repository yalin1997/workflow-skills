---
name: work-mode
license: MIT
description: Run a lean engineering workflow for software development through a verified human-reviewed PR, deep technical Markdown, concise weekly reports, or editable draw.io diagrams. Use for end-to-end tasks, multiple assigned tasks, and resuming this workflow. Route to only the necessary playbook and skills; do not merge PRs.
---

# Work mode

## 啟動

1. 讀取 `references/principles.md`；遵守使用者、專案與 Harness 已授權的範圍。
2. 先確認任務結果、可觀察的完成條件、不變條件與交付格式。能從現有內容得知的資訊不重問；只詢問會改變正確性、權限或重大取捨的缺口，並繼續不受影響的工作。
3. 沿用現有 issue、計畫、PR 或任務記錄，留下簡短契約。需要時使用 `references/templates.md`，不強制新增管理文件。
4. 只讀取本次適用的 playbook：

| 任務 | Playbook |
|---|---|
| 新功能、修改、bug、重構、整套系統開發 | `playbooks/develop.md` |
| 深度技術 Markdown | `playbooks/technical-document.md` |
| 1–2 頁工作週報 | `playbooks/weekly-report.md` |
| draw.io UML component、資料流或 sequence 圖 | `playbooks/drawio.md` |

混合任務先執行主要流程，其他只載入實際需要的部分。開發時已確認的設計與證據可直接供文件使用，避免重新調查。

## 執行方式

- 依 playbook 建立短 checklist，直接執行；例行任務不等待人批准計畫。
- 預設由同一 agent 完成任務。可用 Harness 提供的其他 skill 載入機制；若沒有，直接讀取同層 skill 目錄中的 `SKILL.md`。讀取 skill 不代表啟動新 agent。
- 不自動啟動 subagents、多模型 panel、平行競賽或背景輪詢。
- 多項任務先列出依賴、交付物及各自狀態。Harness 已提供工作目錄隔離，且會變動的測試資源也已隔離時，才並行相關寫入／驗證；否則將有衝突的步驟依序執行。沿用既有 DB／port／queue／輸出位置的隔離方式；共享 schema、介面與同一檔案的修改先協調順序。
- 不相關任務分開交付 PR；有依賴的工作先採可獨立審查的順序。只有必要且符合既有 repo 做法時才使用相依 PR，並註明 base 與驗證前提。
- 每個實質步驟標記進行中（含等待 CI）、完成、`skip: 原因` 或 blocked。跳過不等於驗證通過；必要條件缺證據不得宣稱完成。
- 已完成的檢查不重跑，除非變更、失敗或環境差異使其證據失效。同一失敗連續嘗試仍無新證據時，停止盲試，改查能區分原因的事實。

## 恢復與完成

長任務中斷時留下：原任務／契約連結（含完成條件與待決事項）、branch／工作目錄與 revision、PR／待完成 CI run 的連結、已完成項目與證據位置、未解問題及下一個動作。授權與設計引用既有紀錄。恢復後先讀這份記錄，再確認 working tree、revision 與目前 PR／CI 狀態；不從頭掃描 repo。

交付時說明結果、證據、限制與人類需要決定的事項。開發任務以完成條件滿足、必要檢查通過且證據有效、PR 可供人審為終點；平台 Draft／Active 狀態不代表驗證結果。文件任務以指定檔案可讀、可編輯且來源可追溯為終點。任何流程都不自動 merge、approve、產品發布、部署或另行發送內容給其他人。
