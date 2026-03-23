# Hugging Face 本月新發表模型 Top 5（只看新發表）

更新時間：2026-03-23 08:00（Asia/Taipei）
篩選條件：createdAt 以 `2026-03-` 開頭（本月發表）
排序方式：按 Likes（熱度）排序；不使用下載量作為榜單依據
補充規則：若模型標示為 Uncensored，特徵需明確註記「移除 safety 限制」，並補充是否為 `claude-4.6-opus-dataset` finetune。

## 文字推理（text-generation）

### 1) Tesslate/OmniCoder-9B
- 發表時間：2026-03-12
- 熱度（Likes）：357
- 模型大小：約 9B（由名稱推估）
- 特徵：Qwen3.5-9B 微調、偏程式/代理任務、對話式
- 訓練資料集：未公開
- 連結：<https://huggingface.co/Tesslate/OmniCoder-9B>

### 2) nvidia/NVIDIA-Nemotron-3-Super-120B-A12B-BF16
- 發表時間：2026-03-10
- 熱度（Likes）：282
- 模型大小：120B（A12B MoE）
- 特徵：Nemotron-3 Super、MoE、BF16 版、推理/通用對話
- 訓練資料集：`nvidia/nemotron-post-training-v3`、`nvidia/nemotron-pre-training-datasets`
- 連結：<https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Super-120B-A12B-BF16>

### 3) sarvamai/sarvam-105b
- 發表時間：2026-03-03
- 熱度（Likes）：240
- 模型大小：105B
- 特徵：大型多語言（含印度語系）對話模型
- 訓練資料集：未公開
- 連結：<https://huggingface.co/sarvamai/sarvam-105b>

### 4) nvidia/Nemotron-Cascade-2-30B-A3B
- 發表時間：2026-03-18
- 熱度（Likes）：198
- 模型大小：30B（A3B）
- 特徵：Cascade 架構、reasoning/general-purpose、SFT+RL
- 訓練資料集：未公開
- 連結：<https://huggingface.co/nvidia/Nemotron-Cascade-2-30B-A3B>

### 5) nvidia/NVIDIA-Nemotron-3-Super-120B-A12B-NVFP4
- 發表時間：2026-03-10
- 熱度（Likes）：192
- 模型大小：120B（A12B MoE）
- 特徵：Nemotron-3 Super、NVFP4 量化版（推理成本較低）
- 訓練資料集：`nvidia/nemotron-post-training-v3`、`nvidia/nemotron-pre-training-datasets`
- 連結：<https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Super-120B-A12B-NVFP4>

## 圖形生成（text-to-image）

### 1) F16/z-image-turbo-sda
- 發表時間：2026-03-11
- 熱度（Likes）：56
- 模型大小：未知（LoRA/蒸餾系）
- 特徵：Z-Image-Turbo 系微調，含蒸餾與多樣性恢復標籤
- 訓練資料集：未公開
- 連結：<https://huggingface.co/F16/z-image-turbo-sda>

### 2) squirrelae/Z-Image-Turbo-GGUF
- 發表時間：2026-03-21
- 熱度（Likes）：1
- 模型大小：未知（GGUF 量化）
- 特徵：Z-Image-Turbo 的 GGUF 量化版本
- 訓練資料集：未公開
- 連結：<https://huggingface.co/squirrelae/Z-Image-Turbo-GGUF>

### 3) World1125/ArknightsMostima
- 發表時間：2026-03-21
- 熱度（Likes）：1
- 模型大小：未知（LoRA）
- 特徵：SDXL LoRA 角色/風格向微調
- 訓練資料集：未公開
- 連結：<https://huggingface.co/World1125/ArknightsMostima>

### 4) sololo-xyz/PicBook_SoloLoRA_ZITv3
- 發表時間：2026-03-20
- 熱度（Likes）：1
- 模型大小：未知（LoRA）
- 特徵：Z-Image-Turbo 基底 LoRA 微調
- 訓練資料集：未公開
- 連結：<https://huggingface.co/sololo-xyz/PicBook_SoloLoRA_ZITv3>

### 5) Kingstoun/domovoi_style_LoRA
- 發表時間：2026-03-22
- 熱度（Likes）：0
- 模型大小：未知（LoRA）
- 特徵：SDXL 風格 LoRA
- 訓練資料集：未公開
- 連結：<https://huggingface.co/Kingstoun/domovoi_style_LoRA>

## 音頻生成（text-to-audio）

### 1) artificialguybr/AceStep_Refine_Redmond
- 發表時間：2026-03-20
- 熱度（Likes）：3
- 模型大小：未知（LoRA/PEFT）
- 特徵：Ace-Step1.5 音樂生成方向微調，標示 DPO/LoRA
- 訓練資料集：未公開
- 連結：<https://huggingface.co/artificialguybr/AceStep_Refine_Redmond>

### 2) Davex256/Ace-Step1.5
- 發表時間：2026-03-03
- 熱度（Likes）：1
- 模型大小：未知
- 特徵：AceStep 音樂生成模型（text-to-music）
- 訓練資料集：未公開
- 連結：<https://huggingface.co/Davex256/Ace-Step1.5>

### 3) forkjoin-ai/qwen3-tts-12hz-1.7b-customvoice
- 發表時間：2026-03-09
- 熱度（Likes）：1
- 模型大小：約 1.7B
- 特徵：Qwen3-TTS CustomVoice 衍生版、語音合成
- 訓練資料集：未公開
- 連結：<https://huggingface.co/forkjoin-ai/qwen3-tts-12hz-1.7b-customvoice>

### 4) Makaveliai/acestep-v15-sft-turbo_0.5
- 發表時間：2026-03-10
- 熱度（Likes）：1
- 模型大小：未知
- 特徵：AceStep v1.5 SFT/Turbo 路線微調
- 訓練資料集：未公開
- 連結：<https://huggingface.co/Makaveliai/acestep-v15-sft-turbo_0.5>

### 5) xelsoftai/AfriVox_ST5_20260320_131108
- 發表時間：2026-03-20
- 熱度（Likes）：0
- 模型大小：約 0.14B（粗估）
- 特徵：SpeechT5 系列，偏 TTS
- 訓練資料集：未公開
- 連結：<https://huggingface.co/xelsoftai/AfriVox_ST5_20260320_131108>

## 備註
- 本次 Top5 名單未見明確標示 Uncensored 的模型。
