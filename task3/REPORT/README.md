# Fine-Tuning GPT-2 for Sentiment Analysis (Task 3)

---

## 📋 Project Overview

The primary goal is to classify movie reviews into **Positive** or **Negative** sentiments. Unlike BERT or T5, GPT-2 is traditionally used for text generation; this notebook explores the configuration necessary to use it as a classifier.

### 🛠️ Technology Stack

* **Model:** `gpt2` (pre-trained).
* **Libraries:** `transformers`, `datasets`, `evaluate`, `scikit-learn`, and `pandas`.
* **Platform:** Developed and tested in a **Google Colab** environment.

---

## ⚙️ Methodology

### 1. Model Configuration

* **Padding Token:** Since GPT-2 does not have a default padding token, the **End-of-Sequence (EOS) token** was assigned as the `pad_token` to ensure consistent input lengths.
* **Classification Head:** An `AutoModelForSequenceClassification` was used to add a linear layer on top of the transformer for binary sentiment labels.

### 2. Data Preprocessing

* **Proportional Stratified Sampling:** To manage computational resources, the notebook uses a stratified sampling function to select a representative subset of **1,000 training samples** and **200 validation samples** while maintaining a balanced distribution of positive and negative reviews.
* **Tokenization:** Inputs are tokenized with a maximum length of **512 tokens**, with truncation and padding enabled.

### 3. Training Hyperparameters

* **Learning Rate:** .
* **Batch Size:** 8.
* **Epochs:** 2.
* **Weight Decay:** 0.01.

---

## 📊 Results Summary

The training progress indicates that the model successfully converged, achieving high accuracy on the validation set after two epochs.

| Epoch | Training Loss | Validation Loss | Accuracy |
| --- | --- | --- | --- |
| **1** | N/A | **0.4611** | **83.50%** |
| **2** | **0.4132** | **0.3150** | **89.50%** |

* **Final Training Loss:** 0.4132.
* **Total Runtime:** ~3,121 seconds.

---

## 🔍 Inference and Testing

A `sentiment-analysis` pipeline was established using the fine-tuned GPT-2 weights.

* **Example Input:** *"I absolutely loved this movie! The acting was superb and the plot was very engaging."*
* **Result:** Correctly classified as **POSITIVE**.
