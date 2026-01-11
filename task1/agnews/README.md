## 📌 Project Objectives

The notebook aims to evaluate the performance of two distinct natural language processing (NLP) approaches:

* **Traditional Machine Learning**: Establishing a performance baseline using Logistic Regression.
* **Deep Learning (Transformers)**: Fine-tuning a pre-trained **BERT-base-uncased** model for multi-class classification.

## 📊 Dataset: AG News

The dataset contains news articles categorized into four classes:

1. **World**
2. **Sports**
3. **Business**
4. **Sci/Tech**

To optimize training time, the notebook utilizes a stratified sampling approach, selecting 2,000 samples for training and 200 samples for evaluation.
