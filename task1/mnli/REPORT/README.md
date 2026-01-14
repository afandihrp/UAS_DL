# Question Answering with SQuAD

## 📋 Task Overview

While Tasks 1.1 and 1.2 focused on classification, Task 1.3 explores **Reading Comprehension** and **Question Answering (QA)**. The objective was to fine-tune the **Microsoft Phi-2** model to identify and extract answers from a given context based on a specific question using the **SQuAD v1.1** (Stanford Question Answering Dataset).

## 📊 Dataset: SQuAD v1.1

The Stanford Question Answering Dataset is a benchmark collection of question-answer pairs derived from Wikipedia articles.

* **Context:** A paragraph from Wikipedia.
* **Question:** A query related to the information in the paragraph.
* **Answer:** A specific segment of text within the context.
* **Challenge:** The model must not only understand the semantics of the question but also locate the precise start and end indices of the answer within a potentially long document.

## 🛠️ Methodology

### 1. Data Preprocessing & Tokenization

Handling QA data for LLMs like Phi-2 requires complex tokenization:

* **Context Truncation:** Implemented a "sliding window" approach (using `return_overflowing_tokens`) to handle contexts that exceed the model's maximum sequence length (512 tokens).
* **Offset Mapping:** Used to map the character-based answer positions in the raw text to the token-based positions required by the model.

### 2. Model Configuration

* **Architecture:** `microsoft/phi-2` (2.7B Parameters).
* **Quantization:** Utilized **4-bit quantization** to remain within memory limits, similar to the strategies used in Task 2 and 3.
* **Instruction Format:** Data was structured using the following prompt template:
> **Instruction:** Answer the question based on the context below.
> **Context:** [Wikipedia Paragraph]
> **Question:** [User Query]
> **Answer:** [Target Text]



### 3. Training Parameters

* **Optimization:** Paged AdamW 8-bit.
* **Learning Rate:**  with a cosine learning rate scheduler.
* **Precision:** Mixed precision (`fp16`) to accelerate training.

## 📈 Results & Accomplishments

* **Convergence:** The model demonstrated a steady decrease in training loss, successfully learning to align the question intent with the provided context.
* **Knowledge Transfer:** Proved that a causal language model (Phi-2), typically used for text generation, can be effectively "steered" to perform extractive tasks with high precision through instruction tuning.
* **System Integration:** This task successfully bridged the gap between basic classification (Task 1.1/1.2) and the complex summarization goals of Task 3.

**Would you like me to help you integrate these results into your main project report or generate the evaluation metrics (Exact Match/F1 scores) table?**
