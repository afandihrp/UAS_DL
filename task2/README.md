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

## 📊 Performance Results

The training process showed a sharp improvement in the model's ability to minimize error by the second epoch.

| Epoch | Training Loss | Validation Loss |
| --- | --- | --- |
| **1** | N/A | **5.0874** |
| **2** | N/A | **0.3351** |

---

## 🔍 Inference Implementation

The notebook includes a **`text2text-generation`** pipeline, allowing users to input custom context and questions to receive generated answers directly from the fine-tuned model.
