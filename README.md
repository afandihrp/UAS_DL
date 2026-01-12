# Research Project: Fine-Tuning Phi-2 for Extreme Summarization

## 📋 Executive Summary

This research explores the viability of using small-scale Large Language Models (LLMs) for specific NLP tasks under significant hardware constraints. We successfully adapted **Microsoft’s Phi-2 (2.7B parameters)** to generate one-sentence summaries of news articles using the **XSum dataset**. By utilizing **QLoRA (Quantized Low-Rank Adaptation)**, we reduced memory requirements by over 70%, enabling high-performance training on consumer-grade GPU environments.

---

## 🔬 Research Phase 1: Data Engineering (Tasks 1.1 & 1.2 & 1.3)

The first phase focused on understanding the linguistic characteristics of the **EdinburghNLP/xsum** dataset and preparing it for a causal language modeling objective.

* **Dataset Objective:** Unlike standard summarization (which often results in a paragraph), XSum is "extreme"—it requires the model to synthesize a full news article into a single, punchy sentence.
* **Exploratory Data Analysis (EDA):** We analyzed document lengths and summary distributions to determine optimal sequence padding and truncation strategies.
* **Instruction Wrapper:** We engineered a specific template to transform the raw text into an instruction-following format:
> **Instruction:** Summarize the following news article in a concise and abstractive way.
> **Article:** [Full Text]
> **Summary:** [Target]


* **Tokenization Strategy:** We implemented a custom tokenization pipeline using the `AutoTokenizer` from Phi-2, handling padding tokens and sequence length limits (max 512 tokens) to ensure efficient GPU batching.

---

## 🏗️ Research Phase 2: Optimization & Architecture (Task 2)

In the second phase, we addressed the "Hardware Gap"—training a multi-billion parameter model on limited VRAM (approx. 5.67GB).

* **4-Bit Quantization:** We implemented **NF4 (NormalFloat 4)** quantization via the `bitsandbytes` library. This allowed us to load the model weights in a highly compressed 4-bit format while maintaining 16-bit precision for computation.
* **Memory Management:** * **Gradient Checkpointing:** Enabled to save memory by re-calculating activations during the backward pass.
* **Paged Optimizers:** Used `paged_adamw_8bit` to handle potential memory spikes.


* **Model Loading:** We verified the model's architecture, identifying the target layers (`q_proj`, `k_proj`, `v_proj`, `dense`) for the subsequent adaptation phase.

---

## 🚀 Research Phase 3: PEFT Training & Evaluation (Task 3)

The final phase involved the actual fine-tuning using **Parameter-Efficient Fine-Tuning (PEFT)**.

### 1. LoRA Configuration

Instead of updating all 2.7 billion parameters, we injected low-rank matrices into the attention layers.

* **Rank ():** 16
* **Alpha ():** 32
* **Trainable Parameters:** Only **10,485,760** parameters (0.37% of the model). This drastically reduced the computational overhead while preventing "catastrophic forgetting."

### 2. Training Execution

* **Optimization:** We trained for 1 epoch over a filtered subset of 5,000 samples.
* **Results:** The training loss decreased steadily, achieving a final validation loss of **2.11**.
* **Compute Time:** Total fine-tuning took approximately **1 hour and 38 minutes** on the target hardware.

### 3. Accomplishments & Inference

The project culminated in a functional summarization model. We implemented an inference pipeline utilizing:

* **Nucleus Sampling ():** To ensure varied and natural language generation.
* **Repetition Penalty ():** To prevent the model from getting stuck in infinite loops.
* **Result:** The model successfully transitions from a general-purpose conversationalist to a specialized summarizer capable of condensing complex legal, political, and social news into single sentences.

---

## 🛠️ Technology Stack

* **Base Model:** Microsoft Phi-2
* **Dataset:** Hugging Face `datasets` (XSum)
* **Fine-Tuning:** PEFT (LoRA)
* **Quantization:** BitsAndBytes (4-bit)
* **Environment:** Python, PyTorch, Jupyter Notebooks

## 🏁 Conclusion

This research demonstrates that through **Quantization** and **LoRA**, high-quality abstractive summarization is achievable even on constrained hardware. This project provides a blueprint for further specialized NLP tasks using small-but-mighty models like Phi-2.

---

## 📂 Repository Structure

The repository is organized into three primary task folders, each representing a milestone in the research journey:

- task1
  - agnews 
    - NOTEBOOK
      -   task_1_1.ipynb
    - REPORT
      -   README.md
    - README.md
  - goemotions
    - NOTEBOOK
      -   task_1_2.ipynb
    - REPORT
      -   README.md
    - README.md
  - mnli
    - NOTEBOOK
      -   task_1_3.ipynb
    - REPORT
      -   README.md
    - README.md
- task2
  - NOTEBOOK
    -   task_2.ipynb
  - REPORT
    -   README.md
  - README.md
- task3
  - NOTEBOOK
    -   task_3.ipynb
  - REPORT
    -   README.md
  - README.md
- README.md
