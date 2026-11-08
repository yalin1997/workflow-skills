---
name: work-pr
license: MIT
description: Prepare or update a reviewable PR with focused diff inspection, traceable validation evidence, and required CI results. Use Azure DevOps through the user's approved Chrome DevTools UI workflow, or approved GitHub MCP for personal repositories. Stop at human review; never approve, merge, bypass policies, or deploy.
---

# Work PR

直接呼叫本 skill 時，先讀 `../work-mode/references/principles.md`。沿用現有 PR；不要為同一任務重複建立。

## 準備

1. 確認 repo、帳號、source／target branch、依賴、目前 diff，以及必要檢查與觸發條件。保留使用者原有修改，不用 reset／force push 清掉問題；無關變更不混入 PR。
2. 做一次聚焦自查：是否滿足需求、是否有無關改動、介面／資料相容性、失敗路徑、測試及證據是否吻合。發現具體缺陷才修改，不預設追加 reviewer agent。
3. 使用既有專案提交規範，拆成能理解的小變更。Bug 的失敗測試與修復要能看出關係，不強制額外 commit 或 rebase 儀式。核對本機受測內容（含未提交修改）與最終 PR commit，不遺漏必要 fixture／設定依賴的交付或重建前提；有實質差異才回到 `work-verify` 補驗，僅建立 commit 不重跑相同內容。
4. 以問題與現在行為開頭寫 PR；說明必要設計、驗證、限制及人類應注意的取捨。詳細證據連到任務／報告，避免重複貼長 log。必要驗證未完成時，正文明標待驗證；平台是否設為草稿另依驗證觸發條件決定。

## 建立與檢查

5. 公司 Azure 依使用者現有的核准 Chrome DevTools UI 流程建立／更新；私人 GitHub 可用核准 MCP。已授權的開發任務涵蓋例行 push／PR 建立，但仍受 Harness 權限約束；不因缺工具自行切換到未核准的 API 或服務。
6. 提交前再次確認 repo、分支與正文；提交後回讀 PR URL、內容、diff、base／head 及 CI 狀態，不只以點擊成功作結。
7. 先確認必要 CI 的實際觸發方式：Azure Repos 草稿不觸發 branch-policy validation，需要時依既有授權啟用 PR，正文仍標待驗證；其他平台也不假設草稿必會執行檢查。若專案採手動 queue，使用既有核准流程，不修改 branch policy 或改走未核准工具。採 Harness 提供的通知／有界等待，回報目前狀態並保留恢復指標，不把 pending 當成功。
8. 保留 run URL、source commit、可取得的 target／實際受測提交與結果。PR validation 可能測試合成的 merge commit，不能只要求其 SHA 等於 source HEAD。CI 失敗只取相關資訊，區分產品、測試與環境問題，必要時回到實作及 `work-verify`。patch 或 target 更新後，依目前 policy、build expiration 與證據適用範圍判斷是否需補驗；不忽略失敗、移除必要檢查、繞過政策或一律全套重跑。

## 人類交接

交接前回讀目前 PR diff／head 與必要 policy 結果，確認本機及 CI 證據仍適用。只有完成條件已滿足、必要本機檢查及必要 CI 通過，且證據仍有效時，才交付「可交人審」。Draft／Active／Ready 是平台狀態，不能當作品質結論，也不能為等待 CI 而阻止必要觸發。尚在執行時標示待驗證；必要條件無法驗證時列為 blocked，附目前證據及下一步。

最終回覆包含 PR URL、結果摘要、驗證與限制、需人決定的事項。在支援任務附件的 Harness 中附上 PR。人類負責最後審核與 merge；不自動 approve、merge、產品發布或部署。

平台依據（供查閱）：[Azure Repos PR triggers](https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/azure-repos-git?view=azure-devops#pr-triggers)、[build validation／expiration](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops#build-validation)。
