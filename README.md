# 🌾 Paddy-VLM
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


Fine-tuning Command
scripts/v1_5/finetune_task_lora.sh
Move your dataset and JSON/JSONL files into the playground directory and adjust paths inside the script:
--data_path ./playground/data/llava_v1_5_mix665k.json \
--image_folder ./playground/data/dataset
✅ Done!

References
- [LLaVA Official Repository](https://github.com/haotian-liu/LLaVA)
- [Ollama](https://ollama.com/)
- [Kaggle Dataset](https://www.kaggle.com/competitions/paddy-disease-classification/data)
