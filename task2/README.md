# Generative Question Answering with T5 (Task 2)

---

## 📋 Project Overview

The goal is to train a sequence-to-sequence model that can read a context paragraph and a question, then generate the correct answer. The project utilizes the **Hugging Face** ecosystem for model training and data management.

---

## 🛠️ Key Technical Steps

* **Format Transformation**: Inputs are converted into the specific T5 format: `question: [QUESTION] context: [CONTEXT]`.
* **Proportional Stratified Sampling**: To maintain class balance in smaller subsets, the notebook selects **500 training** and **100 validation** samples proportionally based on the 'title' field.
* **Model Selection**: The **`t5-small`** architecture is used to balance training efficiency with generative performance.
* **Training Configuration**: The model is fine-tuned for **2 epochs** with a learning rate of  and weight decay of .

---

## 🔍 Inference Implementation

The notebook includes a **`text2text-generation`** pipeline, allowing users to input custom context and questions to receive generated answers directly from the fine-tuned model.

---

## ✅ Requirements

This notebook fine-tunes a model for sequence-to-sequence translation tasks.
- torch
- transformers
- datasets
- evaluate
- rouge_score (used for evaluation metrics)
- numpy
