# Multi-Label Emotion Classification (Task 1.2)

---

## 📋 Workflow Summary

* **Environment Setup**: Installation of Hugging Face `transformers`, `datasets`, and `evaluate` libraries.
* **Data Loading**: Utilizing the `go_emotions` simplified dataset containing 58,000 comments.
* **Pre-processing**:
* Converting list-style labels into binary vectors using `MultiLabelBinarizer`.
* Implementing **Stratified Sampling** to create representative subsets (2,000 train / 200 eval) for efficient training.


* **Baseline Modeling**: Training a `OneVsRestClassifier` with **Logistic Regression** and TF-IDF vectorization.
* **Deep Learning**: Fine-tuning a `bert-base-uncased` model specifically configured for multi-label loss ().

---

## 🔍 Implementation Highlights

* **Loss Function**: The model uses multi-label classification logic, applying a sigmoid layer to the outputs.
* **Inference**: A Hugging Face `pipeline` is provided to predict the top 3 emotions for custom text inputs.
* **Model Storage**: The final weights and tokenizer are saved to `./goemotions-bert-model`.
