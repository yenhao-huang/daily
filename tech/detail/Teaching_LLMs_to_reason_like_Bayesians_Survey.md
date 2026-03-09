# Teaching LLMs to Reason Like Bayesians — Survey Notes

日期：2026-03-09

## 1) 問題定義

目標不是只看最終答案，而是看 LLM 是否能：
- 表示不確定性（uncertainty）
- 根據新證據更新信念（belief update）
- 做機率一致的決策（coherent probabilistic decision）

## 2) 三大路線

### A. Prompting-based Bayesian behavior
- CoT / self-consistency / debate / verifier
- 優點：成本低、上手快
- 侷限：常有「看起來像 Bayesian」但不保證機率校準

### B. Training-time alignment
- SFT / RL 直接教 posterior update、likelihood weighting、decision under uncertainty
- 可用合成資料（已知真實 posterior）做監督
- 優點：可把 Bayesian 更新內化到模型參數

### C. Inference-time scaffolding
- 外掛 probabilistic tools（MCMC、PPL、symbolic Bayes net）
- LLM 負責語意解析與工具調用，工具負責嚴格 Bayesian 計算
- 優點：可驗證性高、可控性較好

## 3) 評估基準（Survey 核心）

- Calibration：ECE、Brier score、NLL
- Update correctness：posterior 與真值之 KL divergence
- Sequential evidence：多輪證據更新是否一致
- Decision quality：expected utility / regret
- Robustness：distribution shift / adversarial evidence

## 4) 常見失敗模式

- Base-rate neglect
- Likelihood 誤用
- Evidence double-counting
- Overconfidence after weak evidence
- Order effects（證據順序改變答案）

## 5) 核心洞見

LLM 的語言推理能力不等於 Bayesian coherence。
實務上更可靠的方案通常是：
- LLM（語意拆解 + 程式/工具編排）
- Probabilistic module（嚴格更新與不確定性計算）

## 6) 可執行計畫（建議）

1. 先蒐集 20 篇文獻：
   - Bayesian prompting
   - Uncertainty calibration
   - Tool-augmented probabilistic reasoning

2. 建立 2x2 taxonomy：
   - Prompt-only vs Tool-augmented
   - Single-step vs Sequential evidence update

3. 統一比較表欄位：
   - Task
   - Posterior GT 是否可得
   - Metrics
   - 是否支援多輪 evidence
   - 是否可重現

## 7) 下一步可直接產出

- 20 篇候選 paper 清單
- 可貼 Notion 的 survey 表格模板
- 論文大綱（含 related work 草稿）
