# Fine-Tuning BERT for GoEmotions Multi-Label Classification

---

## 📋 Project Overview

The objective is to classify Reddit comments into **28 different emotion categories** (e.g., admiration, amusement, anger, realization, etc.). Unlike standard classification, each text sample can be associated with multiple labels simultaneously.

### 📊 Dataset Summary

* **Name:** GoEmotions (Simplified version).
* **Content:** 58k Reddit comments.
* **Labels:** 28 emotion categories.
* **Structure:** Includes `text` and a list of `labels` (e.g., `[4, 27]`).

---

## 🛠️ Methodology

### 1. Traditional ML Baseline

* **Features:** TF-IDF Vectorization with a maximum of 5,000 features.
* **Model:** Logistic Regression wrapped in a `OneVsRestClassifier` to handle multi-label outputs.
* **Pre-processing:** Labels were transformed using `MultiLabelBinarizer`.

### 2. Deep Learning (Fine-Tuning BERT)

* **Model:** `bert-base-uncased`.
* **Configuration:** Configured for `multi_label_classification` using `BCEWithLogitsLoss` internally.
* **Sampling:** Used **Stratified Sampling** to create a demonstration subset of 2,000 training samples and 200 validation samples while maintaining label distribution.
* **Training Hyperparameters:**
* Learning Rate: .
* Epochs: 2.
* Batch Size: 16.



---

## 📈 Results Comparison

The models were evaluated primarily using the **Micro-F1 Score**, which is standard for multi-label tasks where class imbalance may exist.

| Model | Technique | Micro-F1 Score |
| --- | --- | --- |
| **Baseline** | TF-IDF + Logistic Regression | **0.4242** |
| **Deep Learning** | Fine-Tuned BERT | **0.0000*** |

> [!IMPORTANT]
> **Observation on BERT Results:** In this specific run, the BERT model returned a 0.0000 F1 score during its 2-epoch training on the small subset. This often occurs in multi-label tasks with many classes (28) when using a very high classification threshold (0.5) before the model has fully converged.

### Training Progress (BERT)

| Epoch | Training Loss | Validation Loss |
| --- | --- | --- |
| 1 | N/A | 0.1890 |
| 2 | 0.2355 | 0.1703 |

---

## 🔍 Inference Example

The notebook includes a pipeline for testing custom text.

**Input:** *"I'm so happy that I finally passed the deep learning exam!"*
**Top Predictions:**

1. **LABEL_27** (Neutral) - Score: 0.245
2. **LABEL_0** (Admiration) - Score: 0.138
3. **LABEL_4** (Approval) - Score: 0.093
