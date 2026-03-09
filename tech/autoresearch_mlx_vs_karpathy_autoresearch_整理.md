# autoresearch-mlx 整理與差異分析

日期：2026-03-09
比較對象：
- 上游：https://github.com/karpathy/autoresearch
- 分支：https://github.com/trevin-creator/autoresearch-mlx

## 1) autoresearch-mlx 在做什麼

`autoresearch-mlx` 是 Karpathy `autoresearch` 的 Apple Silicon 版本移植，核心概念維持不變：
- 讓 AI agent 自動修改 `train.py`
- 每輪固定時間訓練（核心是 5 分鐘訓練預算）
- 用 `val_bpb` 判斷好壞
- 透過 git keep/revert 做實驗管理

但訓練後端從 NVIDIA/PyTorch 轉成 Apple MLX，目標是讓 Mac（M1/M2/M3/M4）也能跑同樣的 autonomous research loop。

## 2) 核心機制（兩者共通）

兩邊都保留同樣的研究 loop 思想：
- 人類主要改 `program.md`（研究策略 / agent 指令）
- agent 主要改 `train.py`
- 每輪跑固定短時訓練，快速迭代
- 以同一個指標（`val_bpb`）做 keep/revert

共通的最重要設計哲學：
- 用固定時間窗而不是固定步數，讓「不同模型配置」在同一時間成本下公平競爭。

## 3) 主要差異（重點）

### A. 硬體與框架
- `karpathy/autoresearch`：
  - 目標平台：單張 NVIDIA GPU（README 提到 H100 測試）
  - 框架：PyTorch + CUDA
- `trevin-creator/autoresearch-mlx`：
  - 目標平台：Apple Silicon（M 系列）
  - 框架：MLX（不需 PyTorch/CUDA）

### B. 實驗節奏（每輪耗時）
- 上游：主打 5 分鐘訓練時間窗，整體迴圈更接近高吞吐（README 描述可達 ~12 exp/hr）
- MLX 版：雖維持 5 分鐘訓練預算概念，但加上 compile + eval 後，完整週期常見約 6–7 分鐘（文中也提 8–9 exp/hr）

### C. Optimizer 支援重點
- 上游：提到 Muon + AdamW
- MLX 版：初期內容曾提 AdamW-only（Muon future work）；後續內容提到已納入 Muon 可選（`USE_MUON=True`）
- 解讀：`autoresearch-mlx` README 內容有版本演進痕跡，實務上以 repo 當前程式碼為準

### D. 評估與效能指標實務
- MLX 版提到：
  - eval token budget 有縮小（為加快迭代）
  - MFU 指標在 Apple 上是 placeholder（缺少對齊 H100 的 FLOPs benchmark）
- 上游在 NVIDIA 生態下，效能度量生態較成熟

### E. 實驗發現（平台導向）
- MLX 版強調固定時間窗下，Apple 上常自動收斂到：
  - 較淺層（例如 DEPTH 4）
  - 較小 batch
  - 更重視「單位時間可做的 optimizer steps」
- 上游也同意固定時間窗是核心，但 MLX 版給了較多 Mac 實測案例

## 4) 實務上怎麼選

### 選 `karpathy/autoresearch`，如果你：
- 有 NVIDIA GPU（特別是資料中心卡）
- 想貼近原始 baseline 與社群主線
- 想較直接比較高性能環境下結果

### 選 `autoresearch-mlx`，如果你：
- 主要設備是 Mac（M 系列）
- 想本地低門檻跑 autonomous research loop
- 想研究「硬體差異如何改變最優超參」

## 5) 對你「Survey auto research」項目的啟發

這兩個 repo 很適合當成你 Survey auto research 的方法學起點：

1. **把研究流程程式化**
   - 將研究者經驗寫進 `program.md`，讓 agent 可重複執行

2. **固定時間窗評估**
   - 比固定 step 更接近真實算力預算下的最佳化

3. **硬體感知研究策略**
   - 同一份 loop 在不同硬體會收斂到不同最優配置（這點很有研究價值）

4. **可擴展成你的 Auto Survey pipeline**
   - 文獻解析（paper）→ 產生假說（program.md）→ 自動實驗 → 報告回填（Notion）

## 6) 一句話總結（TL;DR）

`autoresearch-mlx` 不是重寫研究方法，而是把 Karpathy 的 autoresearch 方法，成功搬到 Apple Silicon 生態，並展示了「固定時間窗 + agent loop」在不同硬體下會長出不同最優解。

---

## 參考連結
- https://github.com/karpathy/autoresearch
- https://github.com/trevin-creator/autoresearch-mlx
