---
name: work-pr
license: MIT
description: Prepare or update a reviewable PR with focused diff inspection, traceable validation evidence, and required CI results. Use Azure DevOps through the user's approved Chrome DevTools UI workflow, or approved GitHub MCP for personal repositories. Stop at human review; never approve, merge, bypass policies, or deploy.
---

# Work PR

直接呼叫本 skill 時，先讀 `../work-mode/references/principles.md`。沿用現有 PR；不要為同一任務重複建立。

## 準備

1. 確認 repo、帳號、source／target branch、依賴及目前 diff。保留使用者原有修改，不用 reset／force push 清掉問題；無關變更不混入 PR。
2. 做一次聚焦自查：是否滿足需求、是否有無關改動、介面／資料相容性、失敗路徑、測試及證據是否吻合。發現具體缺陷才修改，不預設追加 reviewer agent。
3. 使用既有專案提交規範，拆成能理解的小變更。Bug 的失敗測試與修復要能看出關係，不強制額外 commit 或 rebase 儀式。
4. 以問題與現在行為開頭寫 PR；說明必要設計、驗證、限制及人類應注意的取捨。詳細證據連到任務／報告，避免重複貼長 log。必要驗證未完成則明標草稿／待驗證。

## 建立與檢查

5. 公司 Azure 依使用者現有的核准 Chrome DevTools UI 流程建立／更新；私人 GitHub 可用核准 MCP。已授權的開發任務涵蓋例行 push／PR 建立，但仍受 Harness 權限約束；不因缺工具自行切換到未核准的 API 或服務。
6. 提交前再次確認 repo、分支與正文；提交後回讀 PR URL、內容、diff、base／head 及 CI 狀態，不只以點擊成功作結。
7. 取得目前 revision 的必要 CI 結果。採 Harness 提供的通知／有界等待，避免高頻無限輪詢；等待時回報目前狀態，必要時留下可恢復的待辦，不把 pending 當成功。
8. CI 失敗只取相關失敗資訊，區分產品缺陷、測試缺陷與環境問題。必要時回到實作與 `work-verify`；更新 patch 後確認必要檢查對應新的 revision。不忽略失敗、移除必要檢查或繞過政策。

## 人類交接

只有完成條件、必要本機檢查及必要 CI 都有有效證據時，才交付「可交人審」；依 repo 慣例設定 Ready。否則保留草稿／待驗證，列出阻擋、目前證據與下一步。

最終回覆包含 PR URL、結果摘要、驗證與限制、需人決定的事項。在支援任務附件的 Harness 中附上 PR。人類負責最後審核與 merge；不自動 approve、merge、發布或部署。
