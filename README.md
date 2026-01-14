# NLP Task Suite: From Classification to LLM Fine-Tuning

This repository contains a comprehensive set of Natural Language Processing (NLP) projects, ranging from foundational text classification to advanced Large Language Model (LLM) fine-tuning using Parameter-Efficient Fine-Tuning (PEFT) techniques.

## 📋 Repository Overview

The projects are organized into three main categories:

1. **Discriminative NLP (Task 1):** Focuses on understanding and labeling text (Classification & Inference).
2. **Sequence-to-Sequence Modeling (Task 2):** Focuses on transforming text from one form to another (Translation).
3. **Generative AI & LLMs (Task 3):** Focuses on fine-tuning state-of-the-art causal language models for specific tasks (Summarization).

---

## 🛠️ Project Structure & Task Details

### **Task 1: Text Understanding**

* **1.1 News Category Classification (`task_1_1.ipynb`)**
* **Goal:** Classify news articles into four categories: World, Sports, Business, and Sci/Tech.
* **Model:** BERT (`bert-base-uncased`).
* **Dataset:** AG News.


* **1.2 Emotion Detection (`task_1_2.ipynb`)**
* **Goal:** Multi-label classification to identify various emotional states within a text snippet.
* **Model:** BERT-based architecture.


* **1.3 Natural Language Inference (`task_1_3.ipynb`)**
* **Goal:** Predict the relationship between a premise and a hypothesis (Entailment, Neutral, or Contradiction).
* **Model:** BERT.



### **Task 2: Machine Translation (`task_2.ipynb`)**

* **Goal:** Fine-tune a Sequence-to-Sequence (Seq2Seq) model for high-quality language translation.
* **Key Metric:** Evaluated using BLEU and ROUGE scores.

### **Task 3: Phi-2 Abstractive Summarization (`task_3.ipynb`)**

* **Goal:** Fine-tune Microsoft’s **Phi-2 (2.7B)** model to generate concise, abstractive summaries of news articles.
* **Dataset:** XSum (Extreme Summarization).
* **Advanced Techniques Used:**
* **QLoRA:** 4-bit quantization using `bitsandbytes` to reduce memory footprint.
* **LoRA (Low-Rank Adaptation):** Fine-tuning only 0.37% of total parameters (~10.4M).
* **Gradient Checkpointing:** Enabled to allow training on consumer-grade GPUs (e.g., NVIDIA T4).



---

## 🚀 Installation & Requirements

To run these notebooks, you will need a Python 3.10+ environment with a CUDA-enabled GPU (minimum 8GB VRAM recommended for Task 3).

### **1. Clone the repository**

```bash
git clone <repository-url>
cd <repository-directory>

```

### **2. Install Dependencies**

```bash
pip install torch transformers datasets evaluate peft bitsandbytes accelerate rouge_score nltk numpy tqdm

```

---

## 📈 NLP Task Evolution

## 🧪 Usage

1. **Task 1 & 2:** Standard fine-tuning notebooks. Simply open in Google Colab or Jupyter and run all cells to train and evaluate.
2. **Task 3 (LLM):** Ensure you have `bitsandbytes` installed correctly for 4-bit support. The notebook includes a "Troubleshooting" cell to verify library versions before training begins.

## 📊 Evaluation

The models are evaluated using standard NLP metrics:

* **Accuracy/F1-Score:** For classification tasks (Task 1).
* **ROUGE:** For summarization tasks (Task 3) to measure overlapping n-grams between generated and reference summaries.

---

## 📂 Repository Structure

The repository is organized into three primary task folders, each representing a milestone in the research journey:

- task1
  - agnews 
    - NOTEBOOK
      -   task_1_1.ipynb
    - REPORT
      -   README.md
    - README.md
  - goemotions
    - NOTEBOOK
      -   task_1_2.ipynb
    - REPORT
      -   README.md
    - README.md
  - mnli
    - NOTEBOOK
      -   task_1_3.ipynb
    - REPORT
      -   README.md
    - README.md
- task2
  - NOTEBOOK
    -   task_2.ipynb
  - REPORT
    -   README.md
  - README.md
- task3
  - NOTEBOOK
    -   task_3.ipynb
  - REPORT
    -   README.md
  - README.md
- README.md
