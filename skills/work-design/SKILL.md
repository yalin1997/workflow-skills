---
name: work-design
license: MIT
description: Settle the minimal architecture, component responsibilities, interfaces, data shapes, and failure behavior needed for an engineering task. Use for new systems or changes to module boundaries, public APIs, schemas, or concurrency. Prefer one justified design and human decisions over parallel design competitions.
---

# Work design

直接呼叫本 skill 時，先讀 `../work-mode/references/principles.md`，確認範圍及完成條件。

1. 從呼叫者與資料開始：誰使用、輸入輸出、成功／失敗代表什麼、哪些既有行為要維持。
2. 閱讀必要的現況，找出最小可行變更。提出一個推薦方案；只有真正影響決策時才列少量替代方案及取捨，不跑多 agent 設計競賽。
3. 設計只保留會影響實作與審核的內容：元件責任、介面／型別或資料契約、資料流、不變條件、錯誤與恢復方式，以及相容／遷移策略。沒有影響的欄位省略。
4. 同時指出如何驗證：哪些案例證明設計成立、哪條整合路徑要實跑、外部依賴如何控制。複雜系統先選一條垂直切片，不先搭建通用框架。
5. 業務不變條件與不可推得的重要取捨由人類確認。先完成具體方案再提問，繼續不依賴答案的工作；已授權且能自行判斷的例行設計直接記錄並實作，不增加逐層審批。
6. 設計放在既有任務／PR 即可；只有長期重要決策或使用者要求才留獨立 Markdown／ADR。要求圖時依 `../work-mode/playbooks/drawio.md` 產出。

完成時，實作者應能清楚知道改哪些邊界、為什麼，以及用什麼證據判斷完成。
