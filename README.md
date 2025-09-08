
# 🌾 Paddy-VLM
Large multimodal models (LMMs) have demonstrated impressive capabilities in
vision-language reasoning, yet they often struggle when applied to specialized
domains such as agriculture. Crop disease diagnosis, in particular, demands fine4 grained expertise that general-purpose LMMs fail to capture. In this work, we
present PaddyVLM, a domain-adapted vision-language model designed for paddy
disease analysis. Building on LLaVA-v1.5-7B-LoRA, we construct PaddyInstruct,
a domain-specific instruction-tuning dataset derived from a curated Paddy Disease
dataset of 10,407 images spanning 10 categories, including both healthy and dis9 eased conditions. To develop PaddyInstruct, we generate image descriptions with
LLaVA-13B, create Q&A pairs and multi-turn dialogues using Mistral-7B (via an
Ollama setup), and enrich them with knowledge from agricultural repositories. Fine12 tuning with this data enables PaddyVLM to not only recognize diseases with high
accuracy but also assess severity and provide actionable recommendations in con14 versational form. Experimental results demonstrate that PaddyVLM substantially
outperforms general-purpose multimodal models in fine-grained recognition and
domain-specific reasoning, positioning it as a promising expert assistant for farmers
and agricultural researchers.
This repository contains code, resources, and instructions to reproduce the experiments and fine-tune the model.  

---

## 📂 Dataset Setup

1. Download the dataset from Kaggle:  
   👉 [Paddy Disease Classification Dataset](https://www.kaggle.com/competitions/paddy-disease-classification/data)

2. Arrange the dataset in the following structure:

Arrange the dataset in the following structure:

```bash
dataset/
 └── paddy_disease/
      ├── blast/
      ├── tungro/
      ├── dead_heart/
      ├── brown_spot/
      ├── hispa/
      ├── bacterial_leaf_blight/
      └── healthy/

```

---

## 📦 Additional Resources

1. Download the **Other_Resource.zip** available above.  
2. Extract and arrange it as follows:
```
other_resource/
├── attributes/
│ └── paddy_disease/
│ ├───── blast/
│ ├───── tungro/
│ ├───── dead_heart/
│ └── ...
└── external_resource/
└── paddy_disease/
├───── blast/
├───── tungro/
├───── dead_heart/
└── ...

```
---

## Installation

### 1. Install Ollama
Download and install **Ollama** from [ollama.com](https://ollama.com/).  
Make sure your system meets the requirements before proceeding.

---

### 2. Data Preparation

Run the following scripts in order:
# Generate question-answer pairs
data_generation.ipynb

# Convert into LLaVA-compatible format
data_format_converter.ipynb

Model Fine-tuning
⚠️ Important: Only Linux is supported. For macOS/Windows, follow instructions in the LLaVA repo.
```
# Clone the LLaVA repository
git clone https://github.com/haotian-liu/LLaVA.git
cd LLaVA

# Create and activate environment
conda create -n llava python=3.10 -y
conda activate llava

# Install dependencies
pip install --upgrade pip
pip install -e .
pip install -e ".[train]"
pip install flash-attn --no-build-isolation

# (Optional) If upgrading:
git pull
pip install -e .

# If errors occur, try:
# pip install flash-attn --no-build-isolation --no-cache-dir
```

Fine-tuning Command
scripts/v1_5/finetune_task_lora.sh
Move your dataset and JSON/JSONL files into the playground directory and adjust paths inside the script:
```
--data_path ./playground/data/llava_v1_5_mix665k.json \
--image_folder ./playground/data/dataset
```
✅ Done!

References
- [LLaVA Official Repository](https://github.com/haotian-liu/LLaVA)
- [Ollama](https://ollama.com/)
- [Kaggle Dataset](https://www.kaggle.com/competitions/paddy-disease-classification/data)
