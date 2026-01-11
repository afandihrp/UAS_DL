# Fine-Tuning BERT for AG News Text Classification

---

## 📋 Project Overview

The goal of this project is to classify news articles into four distinct categories:

1. **World** (0)
2. **Sports** (1)
3. **Business** (2)
4. **Sci/Tech** (3)

The notebook walks through the entire pipeline, from data exploration and traditional baseline modeling to fine-tuning a pre-trained **BERT (Bidirectional Encoder Representations from Transformers)** model.

---

## 🛠️ Technology Stack

* **Language:** Python
* **Libraries:** `transformers`, `datasets`, `evaluate`, `scikit-learn`, `pandas`, `torch`
* **Deep Learning Model:** `bert-base-uncased`
* **Traditional Baseline:** Logistic Regression with TF-IDF vectorization

---

## 📊 Experimental Results

The models were evaluated based on their accuracy on the test set. Despite being trained on a small subset of the total data, the deep learning approach outperformed the traditional baseline.

| Model | Technique | Accuracy |
| --- | --- | --- |
| **Traditional Baseline** | Logistic Regression + TF-IDF | **90.57%** |
| **Fine-Tuned BERT** | `bert-base-uncased` (3 Epochs) | **94.50%** |

### Training Performance (BERT)

The BERT model was fine-tuned on a stratified sample of 2,000 training examples and evaluated on 200 validation examples.

| Epoch | Training Loss | Validation Loss | Accuracy |
| --- | --- | --- | --- |
| 1 | N/A | 0.3050 | 92.00% |
| 2 | N/A | 0.2431 | 94.50% |
| 3 | 0.3549 | 0.2538 | 94.00% |

> **Note:** The final model selected was the checkpoint from **Epoch 2**, as it achieved the highest validation accuracy () and the lowest validation loss ().

---

## 🚀 Key Features

* **Stratified Sampling:** Ensures that even with a reduced training size, all classes are represented proportionally.
* **Comparative Analysis:** Provides a clear benchmark by comparing modern Transformer architectures against classic statistical methods.
* **Inference Pipeline:** Includes a ready-to-use `transformers.pipeline` for making predictions on custom text.

### Example Inference

**Input:** *"The new spacecraft successfully landed on Mars today to search for life."* **Predicted Category:** `Sci/Tech`
