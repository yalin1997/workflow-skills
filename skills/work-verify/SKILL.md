---
name: work-verify
license: MIT
description: Execute focused tests and real behavior checks for an engineering change, mapping acceptance criteria to revision-specific evidence. Use before PR handoff and after changes invalidate evidence. Distinguish local Windows results, cloud CI, and unverified behavior; never claim an unrun check passed.
---

# Work verify

直接呼叫本 skill 時，先讀 `../work-mode/references/principles.md`，取得任務完成條件及已完成的證據。

## 先選有辨識力的檢查

1. 從 repo 與核准環境確認實際 runner、測試入口及必要命令；不假設測試目錄、PyBuilder task 名稱、CI 平台或 shell 語法。
2. 對應每個完成條件：最小有用的測試／操作、輸入、獨立預期值與證據位置。只為實際風險增加案例，不寫鏡像實作或無意義測試。
3. Bug 保留原本會失敗的輸入，修復後跑相同路徑；重構比較不變行為；功能涵蓋主要成功、重要失敗、邊界及受影響回歸。
4. 跨元件、外部介面、檔案／資料庫等持久化行為需要適當整合或實際入口檢查。必要時從讀取端確認輸出，不能把 mock 寫入成功當成真實持久化成功。

## 執行與判斷

- 使用既有工具執行 unittest、PyBuilder、lint／type checks 及必要行為驗證；工具／網路權限不足時不自行擴權。
- 確認必要案例確實被選取並執行，核對執行／跳過摘要及原因；程序 exit 0 或 OK 不足以證明完成。必要案例未執行（含未選取或 skipped）時，其完成條件維持 BLOCKED，不要求在 PR 重貼完整計數報告。
- 對失敗提出能以證據區分的原因，再做最小修復或補查。不因測試不方便而改預期結果。
- 效能宣稱才增加一致工作量、正確性、重複量測與端到端影響檢查；未量測不報加速比。高風險不變條件增加對應案例；形式驗證不列為例行步驟。
- 對 diff 做一次必要自查：程式與測試是否共同依賴同一錯誤假設、是否只有 mock 路徑、是否破壞未變更的契約。同一作者自查不稱為獨立驗證。

## 留下足夠重跑的證據

記錄 revision、環境、命令／操作、實際結果及核准的 log／報告位置。摘要可沿用 `../work-mode/references/templates.md`。原始輸出不灌滿對話，敏感資料不放入交付。

本機測試若含未提交修改，以當時的 commit 加相關 patch／既有變更紀錄識別受測內容；交接前核對最終 PR commit，確認未依賴未交付也未聲明的 fixture、設定或使用者原有修改。測試前置條件可引用既有重建方式；敏感設定只記所需前提，不複製值。也可在待交付內容提交後做最終驗證，不強制新增 manifest 或額外 commit。內容相同、只建立 commit 時不用重跑；內容不一致才依影響補驗。

各完成條件標記 PASS／FAIL／BLOCKED；不適用項目附 `skip: 原因`。必要條件缺證據則整體仍為 blocked，不以其他測試數量抵銷。

本機結果與必要雲端 CI 分開列。若 CI 需 PR 才能觸發，交由 `work-pr` 依平台與專案的實際觸發條件建立／啟用 PR；不得一律先開草稿等待 CI。Azure Repos 草稿不觸發 branch-policy validation，平台 Active 不代表證據已齊；必要 CI 尚未通過或證據已失效時不得宣布最終可審。

必要 CI 記錄 run URL、source commit，以及平台可取得的 target／實際受測提交。Azure PR validation 可能測試合成的 merge commit，不要求其 SHA 等於 source HEAD。交接前回讀目前必要 policy 結果；source／target 更新後，依既有 policy、build expiration 與證據適用範圍判斷是否需補驗，不自行改 policy 或一律全套重跑。

變更後依影響更新相關證據。無關檢查可保留，但要能解釋適用範圍，不能把舊 head 的整體結論直接沿用。
