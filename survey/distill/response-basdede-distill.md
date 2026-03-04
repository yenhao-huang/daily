# Response-based Distillation / Data Generation Survey

> 主題：整理與 Orca 類似、以強 teacher 生成 richer supervision（explanations / traces / refinement）來訓練 student 的方法。
> 
> 兩段式對照：
> 1. **Phase A：`input → teacher → response`**
> 2. **Phase B：`input + response → teacher`**（做 refinement / critique / trace augmentation）

---

## 1) Self-Instruct (Wang et al., ACL 2023)
- 連結：<https://aclanthology.org/2023.acl-long.754/>
- 核心流程：
  - 先由模型自產 instruction
  - 再視需要產生 input
  - 接著產生 output
  - 經過過濾後做 instruction tuning
- 蒸餾/資料生成特徵：
  - teacher 不只回答，還會「造題（instruction/input）」
  - 以自生成資料擴充監督訊號
- 兩段式對應：
  - **Phase A：高度對應**（input 可由 teacher 合成，再產 response）
  - **Phase B：弱對應**（主要不是對既有 response 再精修）

## 2) WizardLM / Evol-Instruct (Xu et al., 2023)
- 連結：<https://arxiv.org/abs/2304.12244>
- 核心流程：
  - 用強 teacher 將 instruction 逐步「進化」成更複雜任務
  - 由 teacher 產生對應答案
  - 形成高難度 instruction-tuning 資料
- 蒸餾/資料生成特徵：
  - 本質是 curriculum/progressive data construction
  - 強調把任務難度與推理需求往上拉
- 兩段式對應：
  - **Phase A：高度對應**（teacher 針對 input/進化後 input 產生 response）
  - **Phase B：中度對應**（進化指令可視為對原任務的再加工）

## 3) STaR (Zelikman et al., 2022)
- 連結：<https://arxiv.org/abs/2203.14465>
- 核心流程：
  - 先產 chain-of-thought
  - 用答案正確性做篩選
  - 把有效 rationale 反覆用於再訓練
- 蒸餾/資料生成特徵：
  - 把「推理過程」當監督訊號，而非只看最終答案
  - 透過迭代過濾提升 trace 品質
- 兩段式對應：
  - **Phase A：對應**（input 生成 answer+trace）
  - **Phase B：中高度對應**（可視為對既有解答進行 rationale 再生成/校正）

## 4) Symbolic Chain-of-Thought Distillation (SCoTD, 2024)
- 連結：<https://arxiv.org/html/2306.14050v2>
- 核心流程：
  - 大 teacher 產生偏結構化/符號化 rationales
  - student 學習可遷移的解題步驟
- 蒸餾/資料生成特徵：
  - 強化 rationale 的結構性，降低只模仿語氣的風險
- 兩段式對應：
  - **Phase A：高度對應**（input → teacher trace/response）
  - **Phase B：中度對應**（若在既有 response 上補符號化解釋，則更貼近）

## 5) ELAD (Zhang et al., Findings ACL 2024)
- 連結：<https://aclanthology.org/2024.findings-acl.264.pdf>
- 核心流程：
  - 以 explanation-guided distillation 為主
  - 用 active learning 挑選「最值得再次問 teacher」的樣本
- 蒸餾/資料生成特徵：
  - 同時優化 supervision 品質與 teacher query 成本
  - 解釋訊號是主 supervision，不是附屬資訊
- 兩段式對應：
  - **Phase A：對應**（teacher 產答案與解釋）
  - **Phase B：高度對應**（針對既有樣本二次詢問 teacher 做 refinement/augmentation）

## 6) Curriculum Distillation 系列（EMNLP/ACM 2025）
- 連結（例）：<https://aclanthology.org/2025.emnlp-main.376.pdf>
- 核心流程：
  - 將長鏈推理 trace 依難度、步驟或長度切分
  - 以課程式學習安排 student 訓練順序
- 蒸餾/資料生成特徵：
  - 把 Orca 的 progressive learning 系統化
  - 強化小模型長鏈推理穩定度
- 兩段式對應：
  - **Phase A：對應**（teacher trace 作為主資料）
  - **Phase B：高度對應**（對 trace 進行切段、重排、分級即是再加工）

## 7) Quality/Contrastive Rationale Distillation（QCRD 等, 2025）
- 連結（例）：<https://aclanthology.org/2025.emnlp-main.724.pdf>
- 核心流程：
  - 對 rationales 做品質評分
  - 以對比學習或品質導向目標訓練 student
- 蒸餾/資料生成特徵：
  - 核心不是「有沒有 trace」，而是「用高品質 trace 訓練」
  - 減少 student 只學到表面文風
- 兩段式對應：
  - **Phase A：中度對應**（可直接吃 teacher traces）
  - **Phase B：高度對應**（input+response 後追加 teacher 評語/優化 trace 非常契合）

---

## 與 Orca 最貼近的優先閱讀路線
1. **Orca**：<https://arxiv.org/abs/2306.02707>
2. **ELAD**（explanation + active sample selection）
3. **Curriculum Distillation 系列**（progressive / staged trace learning）
4. **QCRD 類方法**（quality-guided rationale optimization）

原因：以上方法都把 **第二段再加工（refinement/critique/quality signal）** 當成主要 supervision，最接近你的兩段式蒸餾設計。

---

## 一句話總結
這批工作可視為同一演進脈絡：
**從「teacher 直接給答案」→「teacher 給答案 + 解釋」→「對既有答案/解釋做二次精修與品質控管」**；
而你的兩段式流程正好落在這條主線上，且與 Orca/ELAD/Curriculum/QCRD 的方法論高度同構。