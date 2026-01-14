# Question Answering with SQuAD (1.3)

## 📖 Introduction

In Task 1.3, the focus shifts to **Reading Comprehension**. Unlike the previous classification tasks, Question Answering requires the model to have a deeper semantic understanding of both a query and a source text to identify specific factual information.

## 🎯 Objectives

* **Model Adaptation:** Fine-tune the **Microsoft Phi-2** model to function as an extractive QA system.
* **Complex Data Mapping:** Handle the **SQuAD v1.1** dataset, which requires mapping character-level answer spans to token-level positions.
* **Context Management:** Implement sliding window techniques to process long Wikipedia articles that exceed the model's token limit.

---

## 🛠️ Technical Workflow

### 1. Dataset: SQuAD v1.1

We utilize the **Stanford Question Answering Dataset**, a collection of over 100,000 question-answer pairs. The model is trained to predict the "start" and "end" of the answer within a provided context.

### 2. The QA Pipeline

To transform the causal language model (Phi-2) into a QA assistant, we use a structured instruction prompt:

> **### Instruction:** Read the context below and provide a concise answer to the question.
> **### Context:** [Wikipedia Paragraph]
> **### Question:** [User Query]
> **### Answer:** [The segment extracted by the model]

### 3. Handling Long Sequences

Because LLMs have a fixed context window (512 tokens for this task), we implement **DocStride**. If a context is too long, it is split into overlapping chunks, ensuring that the answer is never "cut off" at the boundary of a chunk.

---

## 📊 Evaluation Metrics

The performance of the model in this notebook is discussed based on two primary industry-standard metrics:

* **Exact Match (EM):** Measures the percentage of predictions that match the ground truth answers exactly.
* **F1 Score:** Measures the average overlap between the prediction and the ground truth, providing a more lenient and realistic assessment of model performance.

## ✅ Requirements
This notebook evaluates relationships (entailment, neutral, contradiction) between premises and hypotheses.
- torch
- transformers
- datasets
- evaluate
- numpy
