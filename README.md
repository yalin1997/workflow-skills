# Workflow Skills v0.1

由 pstack 蒸餾的日常工程工作流，以 Markdown skills 與 playbooks 交付。適用公司 OpenCode／Opus 5.5、Windows、Azure DevOps，以及私人 Codex／Claude Code、GitHub。這是可編輯的第一版，尚未在你的 repo 與 Harness 實跑驗收。

## 使用方式

將 `skills/` 裡的四個資料夾整組複製到現有 Harness 的專案 skills 目錄，保留子目錄：

| Harness | 專案安裝位置 |
|---|---|
| OpenCode | `.opencode/skills/` |
| Codex | `.agents/skills/` |
| Claude Code | `.claude/skills/` |

若已有同名 skill，先比對再合併。重新載入 Harness 後確認能發現 `work-mode`。不同版本的呼叫介面以 Harness 為準；可直接說「使用 work-mode 執行以下任務」，Claude Code 可用 `/work-mode`。此套件不修改你的 Harness、模型設定、權限或工具。

```text
使用 work-mode。
任務：修復取消作業後仍寫入結果的問題。
完成條件：取消後不再寫入；正常作業不受影響；本機測試與必要 CI 通過。
範圍：沿用現有介面，不修改資料表。
交付：Azure PR、重現與修復證據、剩餘限制，最後由我審核。
```

其他入口範例：

```text
使用 work-mode，設計並實作批次匯入功能，包含架構、test cases、驗證與 PR。
使用 work-mode，以指定模組和 PR 為來源，撰寫可留存的深度技術 Markdown。
使用 work-mode，以本週指定任務與 PR 為來源，整理 1–2 頁工作週報。
使用 work-mode，為匯入服務產出可編輯的 draw.io UML component 圖與資料流圖。
```

## 四個 skills

| Skill | 責任 | 載入時機 |
|---|---|---|
| [work-mode](skills/work-mode/SKILL.md) | 選 playbook、設定完成條件、維持任務進度 | 主要入口 |
| [work-design](skills/work-design/SKILL.md) | 收斂架構、介面、資料形狀與重要取捨 | 有設計決策時 |
| [work-verify](skills/work-verify/SKILL.md) | 執行有辨識力的測試，對應行為與證據 | 開發交付前 |
| [work-pr](skills/work-pr/SKILL.md) | 檢查 diff、開 PR、追蹤必要 CI、交付人審 | 開發完成後 |

文件、週報與 draw.io 是 `work-mode` 的按需 playbooks，不會另外啟動 agent。

## 從 pstack 留下什麼

保留：完成條件與不變條件、按需載入流程、小步可審查變更、bug 先重現、測試與真實行為驗證、證據可追溯、跳過步驟有理由、明確的人類交接。

移出預設：多方案競賽、多模型交叉審查、多 agent 驗證群、常駐協調 agent、自動合併、無限 CI 輪詢、每次任務自動擴寫 skills。需要效能或形式驗證時再指定，不預先載入。

人類負責業務規則、優先順序、重要取捨與最終 PR 審核；AI 保留實作、自查、測試執行及證據整理。人類審核承接原本昂貴的獨立 AI reviewer，但不取代必要測試。由同一 agent 實作與驗證，不能宣稱已完成獨立審查。

## Harness 與工作流的分工

Harness 負責模型、工具、命令權限、網路與檔案隔離、session／worktree、用量記錄。這份工作流負責如何工作、檢查什麼、如何交付。

公司使用前，將已核准的 repo／檔案範圍、命令、模型端點、網站與 Azure 組織／專案範圍提供給 Harness；不必另外建立本套件專用設定檔。安全執行規則見 [principles.md](skills/work-mode/references/principles.md)。Markdown 不能提供硬隔離；未有實際限制時，不得宣稱已防止資料外洩。

多項任務由現有 Harness 配置獨立 session／工作目錄，或依序執行。本套件不加入排程器，也不自行啟動 subagents。

## 導入與調整

先用一個 bug、一個功能與一份週報試跑。檢查：人能否按證據重驗、PR 是否仍需大幅補充、文件是否追溯到來源、有沒有重複讀取與無效重試。用 Harness 的實際用量與人類審核時間衡量成本，不預設節省百分比。

持續發生且能自動檢查的錯誤，優先交給既有型別、lint、測試或 CI；只有需要判斷的步驟才放入 skill。一次性問題不擴成永久流程。

## 來源與設計界線

本套件是依你的需求重新撰寫的流程，沒有複製 pstack 的技能內容。

- [指定文章](https://warmwater.dev/blog/pstack-agent-engineering-workflow/)
- [pstack 官方說明](https://github.com/cursor/plugins/tree/main/pstack)：參考按需路由、可驗證交付，以及 PR 交由人處理的方向。
- [OpenCode skills](https://opencode.ai/docs/skills/)、[permissions](https://opencode.ai/docs/permissions/)
- [Codex skills](https://developers.openai.com/codex/skills/)、[Claude Code skills](https://code.claude.com/docs/en/skills)

上述連結是供人查閱的來源，不授權 agent 自動連線或傳送公司內容。
