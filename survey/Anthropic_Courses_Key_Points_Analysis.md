# Anthropic Skilljar 課程重點分析

資料來源：`https://anthropic.skilljar.com` 課程首頁公開清單（含課程簡介）

## 一、整體課程地圖（你可以這樣理解）

Anthropic 的課程大致可分成 5 條主線：

1. **入門與通用生產力**
   - Claude 101
   - AI Fluency: Framework & Foundations

2. **開發與工程實作**
   - Building with the Claude API
   - Claude Code in Action
   - Introduction to agent skills

3. **MCP（Model Context Protocol）專項能力**
   - Introduction to Model Context Protocol
   - Model Context Protocol: Advanced Topics

4. **雲平台落地（企業導入）**
   - Claude with Amazon Bedrock
   - Claude with Google Cloud Vertex AI

5. **教育與垂直場景應用**
   - AI Fluency for educators
   - AI Fluency for students
   - Teaching AI Fluency
   - AI Fluency for nonprofits

---

## 二、各課程重點（精簡版）

### 1) Claude 101
- **重點**：建立 Claude 使用基本功（任務拆解、提示清楚化、日常工作流程化）。
- **適合**：初學者、跨部門同事。
- **價值**：快速降低使用門檻，形成共通語言。

### 2) AI Fluency: Framework & Foundations
- **重點**：有效率、負責任、安全地與 AI 協作。
- **適合**：所有知識工作者。
- **價值**：把「會用工具」提升到「會設計 AI 協作流程」。

### 3) Building with the Claude API
- **重點**：Claude API 全流程開發（串接、調參、工程化）。
- **適合**：工程師、技術 PM。
- **價值**：從 prompt 使用者進階到產品/服務建置者。

### 4) Claude Code in Action
- **重點**：把 Claude Code 納入實際開發工作流。
- **適合**：軟體工程團隊。
- **價值**：提升開發效率與交付速度，落地到 daily coding。

### 5) Introduction to Model Context Protocol (MCP)
- **重點**：從零打造 MCP server/client；掌握 tools/resources/prompts 三大原語。
- **適合**：需要把模型連接外部系統的開發者。
- **價值**：建立可擴展、可重用的 AI 介面層。

### 6) MCP: Advanced Topics
- **重點**：sampling、notifications、檔案系統存取、transport 等進階模式。
- **適合**：要上 production 的團隊。
- **價值**：從 prototype 走向穩定可維運的架構。

### 7) Claude with Amazon Bedrock
- **重點**：在 AWS 生態中導入 Claude 的實作路徑。
- **適合**：AWS 使用者、企業 IT 團隊。
- **價值**：加速企業採用與治理整合。

### 8) Claude with Google Cloud Vertex AI
- **重點**：在 GCP/Vertex AI 上使用 Claude 的全流程。
- **適合**：GCP 團隊。
- **價值**：雲端原生整合、便於企業部署。

### 9) Introduction to agent skills
- **重點**：在 Claude Code 建立/配置/分享 Skills（可重用 markdown 指令）。
- **適合**：要團隊化標準化 AI 工作流的人。
- **價值**：把個人提示技巧產品化、資產化。

### 10) 教育與公益 AI Fluency 系列
- AI Fluency for educators / students / nonprofits + Teaching AI Fluency
- **重點**：針對不同受眾（教師、學生、非營利）制定 AI 協作與教學實作。
- **價值**：場景化落地，強調責任與實務成效。

---

## 三、我看到的「課程設計核心邏輯」

1. **先通識（AI Fluency）再專業（API/MCP/Cloud）**：
   Anthropic 不是只教模型操作，而是先建立協作與責任框架。

2. **從「使用者」到「建置者」的進階路徑清楚**：
   Claude 101 → API → MCP → Advanced/Cloud。

3. **高度重視可落地與可擴展**：
   MCP 與 Cloud 課程代表重點在「接入企業系統」與「生產環境可維運」。

4. **強調可傳播能力（Skills + Teaching）**：
   不只會做，還能把方法標準化並傳給團隊/學生。

---

## 四、建議學習順序（實戰導向）

### A. 工程師（你要做產品）
1. Claude 101（快速補齊共通操作）
2. AI Fluency Foundations（安全與方法）
3. Building with Claude API
4. Introduction to MCP
5. MCP Advanced Topics
6. Claude Code in Action
7. Introduction to agent skills
8. Bedrock / Vertex（二選一，依雲平台）

### B. 團隊導入負責人（你要推組織 adoption）
1. AI Fluency Foundations
2. Claude 101
3. Claude Code in Action
4. Introduction to agent skills
5. 雲平台課程（Bedrock/Vertex）
6. MCP Intro（需要系統整合時再上）

### C. 教育工作者
1. AI Fluency for educators
2. Teaching AI Fluency
3. Claude 101
4. （選修）MCP / API 作為進階能力

---

## 五、對你目前工作最有用的 3 門（優先）

1. **Building with the Claude API**
   - 直接強化你做 agent / workflow / benchmark tooling 的底層能力。

2. **Introduction to MCP**
   - 若你要把資料源、工具、檢索系統接進 agent，這門關鍵。

3. **Introduction to agent skills**
   - 能把你現有做法標準化，變成可複用「技能資產」。

---

## 六、可執行的 2 週學習計畫（精簡）

- **Week 1**：Claude 101 + AI Fluency + Claude API（理解 + 小 demo）
- **Week 2**：MCP Intro + agent skills（做一個可重用技能流程），最後補 Cloud 課程（依你用的雲）

產出建議：
- 1 份 API demo repo
- 1 個 MCP server PoC
- 1 套 team skills 模板

---

## 七、結論

Anthropic Skilljar 的價值不只在「教你用 Claude」，而是提供一條完整能力鏈：
**AI Fluency（方法與責任）→ API/MCP（工程化）→ Cloud（企業落地）→ Skills/Teaching（組織擴散）**。

如果你的目標是「把 AI 從個人工具升級為團隊生產系統」，這套課程結構是非常對位的。
