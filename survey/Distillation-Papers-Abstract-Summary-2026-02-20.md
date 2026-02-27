# Distillation 論文 Abstract 整理（2026-02-20）

History: ensemble mlp -> bert -> llm

## 1) Distilling the Knowledge in a Neural Network (Hinton et al., 2015)
- **Abstract 重點：** 提出知識蒸餾核心概念：將大型集成模型（ensemble）的知識壓縮到單一小模型中，降低部署成本。論文顯示在 MNIST 與商用語音模型上可在顯著簡化模型的同時維持/提升效能。
- **啟示：** KD 的本質是用 teacher 的「軟目標分佈」傳遞類別間相對關係，不只是學 one-hot label。 
- **實驗介紹：** 1. 多個模型 (mlp models) 聚合再一起，在蒸餾到單一模型 (mlp models) 2. use case 手寫辨識, 語音辨認
- **連結：** https://arxiv.org/abs/1503.02531

## 2) DistilBERT (Sanh et al., 2019)
- **Abstract 重點：** 在 pretraining 階段做蒸餾，提出 triple loss（LM + distillation + cosine）。在 BERT 壓縮 40% 下，保留約 97% 語言理解能力，推理速度約快 60%。
- **啟示：** 先做 task-agnostic 蒸餾，再做下游 fine-tune，是小模型通用化的高性價比路線。
- **連結：** https://arxiv.org/abs/1910.01108

## 3) TinyBERT (Jiao et al., 2020)
- **Abstract 重點：** 為 Transformer 設計專用蒸餾法，並採兩階段蒸餾（pretraining + task-specific）。4 層學生模型在 GLUE 達 teacher 96.8% 表現，且更小更快。
- **啟示：** 中間層訊號（hidden/attention 等）對壓縮效果關鍵，不應只蒸餾 logits。
- **連結：** https://arxiv.org/abs/1909.10351

## 4) Patient Knowledge Distillation (Sun et al., 2019)
- **Abstract 重點：** 提出「耐心蒸餾」：學生模型從 teacher 多個中間層逐步學習（PKD-Last / PKD-Skip），提升訓練效率並維持精度。
- **啟示：** 對齊多層知識可改善 shallow student 的學習穩定性。
- **連結：** https://arxiv.org/abs/1908.09355

## 5) MiniLM (Wang et al., 2020)
- **Abstract 重點：** 以 deep self-attention distillation 壓縮 Transformer，不只學 attention 分佈，還學 value 關係；在約半參數/半計算下保留高任務精度。
- **啟示：** 蒸餾 attention 結構知識比純輸出層蒸餾更有效率。
- **連結：** https://arxiv.org/abs/2002.10957

## 6) MiniLMv2 (Wang et al., 2021)
- **Abstract 重點：** 推廣為 multi-head self-attention relation distillation，且不再強制 teacher/student head 數相同，擴展了可用性與壓縮彈性。
- **啟示：** 關係蒸餾（Q/K/V pair relations）可在不同架構間更穩定轉移知識。
- **連結：** https://arxiv.org/abs/2012.15828

## 7) Self-Instruct (Wang et al., 2022)
- **Abstract 重點：** 用模型自生成 instruction/input/output，再過濾去重後回訓，減少人工作標註依賴；對 instruction-following 能力有顯著提升。
- **啟示：** 合成資料 + 嚴格過濾可形成可擴張的指令蒸餾流水線。
- **評估結果：** 能媲美 InstructGPT 使用人類標注資料 finetune 的表現
- **連結：** https://arxiv.org/abs/2212.10560

## 8) LIMA (Zhou et al., 2023)
- **Abstract 重點：** 65B 模型僅用 1,000 筆高品質 SFT 資料就取得強對話表現，強調預訓練已學到大多知識，對齊階段重點是「行為格式」而非灌知識。
- **啟示：** 在高品質前提下，少量資料也能有效；quality 可能遠大於 quantity。
- **連結：** https://arxiv.org/abs/2305.11206

## 9) Orca (Mitra et al., 2023)
- **Abstract 重點：** 讓 13B 學生學習 GPT-4 的 explanation traces 與 step-by-step 訊號，不只模仿答案風格；在 BBH/AGIEval 等複雜推理 benchmark 顯著提升。
- **啟示：** 蒸餾「推理軌跡」比蒸餾「最終答案」更能提升小模型 reasoning。
- **連結：** https://arxiv.org/abs/2306.02707

## 10) Orca 2 (Mitra et al., 2023)
- **Abstract 重點：** 進一步強調小模型不該只模仿大模型輸出，而要學會依任務選擇不同解題策略（step-by-step、recall-then-generate 等），在多項推理任務上超越同級模型。
- **啟示：** 策略蒸餾（strategy learning）是小模型上限提升關鍵。
- **連結：** https://arxiv.org/abs/2311.11045

## 11) WizardLM / Evol-Instruct (Xu et al., 2023)
- **Abstract 重點：** 用 Evol-Instruct 自動把初始指令逐步演化成高複雜度指令，再混合訓練 LLaMA；人評與 GPT-4 評估顯示效果顯著。
- **啟示：** 自動生成「難度分層」資料可改善模型處理複雜指令能力。
- **連結：** https://arxiv.org/abs/2304.12244

## 12) Chinchilla (Hoffmann et al., 2022)
- **Abstract 重點：** 提出 compute-optimal scaling：給定算力時，模型大小與訓練 token 應同步擴張；指出許多大模型其實 undertrained。70B Chinchilla 在相同算力下可勝過更大參數模型。
- **啟示：** 蒸餾與 SFT 前，先確保 teacher/data 配比合理；資料不足會卡住上限。
- **連結：** https://arxiv.org/abs/2203.15556

---

## 橫向經驗結論（給 10w/100w/1000w 規劃）
1. **資料品質 > 資料數量**：LIMA 與 Self-Instruct 系列都支持這件事。
2. **蒸餾訊號深度很重要**：TinyBERT/PKD/MiniLM 系列顯示中間層與關係蒸餾可顯著增益。
3. **只模仿答案不夠**：Orca 系列顯示蒸餾推理過程/策略對小模型特別關鍵。
4. **擴量要看邊際效益**：從 100k 到 1M 常有明顯收益；再往上要靠去重、難例挖掘與資料評分，不然收益遞減。

## Insight
1. 學習分部 -> 學習合成式資料
