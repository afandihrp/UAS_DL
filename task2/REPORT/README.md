# README: Fine-Tuning T5 for Question Answering (SQuAD)

This repository contains a Jupyter Notebook (`task_2.ipynb`) demonstrating the fine-tuning of the **T5-small** model for generative **Question Answering** using the **SQuAD v1.1** dataset.

---

## 📋 Project Overview

The project focuses on teaching a sequence-to-sequence model to extract or generate answers based on a provided context and question. The **Stanford Question Answering Dataset (SQuAD)** is used, which includes context paragraphs, related questions, and their ground-truth answers.

### 🛠️ Technology Stack

* **Model:** `t5-small`.
* **Libraries:** `transformers`, `datasets`, `accelerate`, `evaluate`, and `rouge_score`.
* **Framework:** Hugging Face **Trainer API** and **Seq2Seq** pipelines.

---

## ⚙️ Methodology

### 1. Data Preprocessing

* **Input Formatting:** T5 requires a specific prefix-based format: `question: [QUESTION]  context: [CONTEXT]`.
* **Tokenization:** Inputs are tokenized to a maximum length of **512 tokens**, while target answers are tokenized to **128 tokens**.
* **Proportional Stratified Sampling:** To ensure representative subsets, the notebook uses stratified sampling to select **500 training samples** and **100 validation samples** proportionally across different titles in the dataset.

### 2. Training Configuration

The model was fine-tuned using the following hyperparameters:

* **Learning Rate:** .
* **Batch Size:** 8 for both training and evaluation.
* **Epochs:** 2.
* **Weight Decay:** 0.01.

---

## 📊 Results Summary

The model showed a significant decrease in validation loss during the second epoch, indicating successful adaptation to the QA task.

| Epoch | Training Loss | Validation Loss |
| --- | --- | --- |
| **1** | N/A | **5.0874** |
| **2** | N/A | **0.3351** |

* **Final Training Loss:** 6.6125.
* **Total Training Time:** Approximately 3,128 seconds.

---

## 🔍 Inference and Testing

A `text2text-generation` pipeline was implemented to allow for custom inference.

* **Sample Context:** *"The University of Notre Dame is a Catholic research university located in South Bend, Indiana."*
* **Sample Question:** *"Where is the University of Notre Dame located?"*
* **Model Task:** The model generates the predicted answer text based on these inputs.

Would you like me to help you evaluate this model using **Exact Match (EM)** and **F1 scores** on the full validation set?
