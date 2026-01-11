# Fine-Tuning Phi-2 for Abstractive Summarization (XSum)

This project demonstrates an end-to-end pipeline for fine-tuning the **Phi-2** (2.7 billion parameter) language model. The model is specifically optimized to transform long-form news articles into concise, one-sentence abstractive summaries using the **XSum (Extreme Summarization)** dataset.

## 🚀 Project Overview

The goal was to adapt a general-purpose causal language model for a specific sequence-to-sequence task (summarization) while operating within significant memory constraints (approx. **5.67GB GPU VRAM**).

### Key Components:

* **Base Model:** Microsoft Phi-2.
* **Dataset:** `EdinburghNLP/xsum` (A subset of 5,000 training and 500 validation samples was used for efficiency).
* **Methodology:** Parameter-Efficient Fine-Tuning (**PEFT**) using **LoRA** (Low-Rank Adaptation) and **4-bit Quantization**.

---

## 🛠️ Technical Implementation

### 1. Memory Optimization

To enable training on consumer-grade or entry-level cloud GPUs (like the NVIDIA T4), the following techniques were applied:

* **4-bit Quantization:** Utilized `bitsandbytes` with NF4 (NormalFloat 4) and Double Quantization.
* **LoRA:** Instead of updating 2.7B parameters, only **10.48M parameters** (0.37% of the total) were made trainable.
* **Gradient Checkpointing:** Enabled to reduce memory footprint by not storing all intermediate activations during the forward pass.
* **Optimizer:** Used `paged_adamw_8bit` to handle memory spikes during optimization.

### 2. Prompt Engineering

The model was trained using an **instruction-style format** to guide the generation process:

> **### Instruction:** Summarize the following news article in a concise and abstractive way.
> **### Article:** [Full Article Text]
> **### Summary:** [Ground Truth Summary]

### 3. Training Configuration

* **Epochs:** 1
* **Effective Batch Size:** 8 (Batch size 1 per device × 8 Gradient Accumulation steps).
* **Sequence Length:** 512 tokens.
* **Learning Rate:**  with a cosine scheduler.

---

## 📊 Results and Evaluation

### Training Metrics

The model was trained for **625 steps**. The loss curves indicated stable convergence:

| Metric | Value |
| --- | --- |
| **Initial Training Loss** | ~2.21 |
| **Final Validation Loss** | **2.11** |
| **Total Trainable Params** | 10,485,760 |

### Qualitative Example

In testing, the model successfully generated summaries that captured the core intent of the articles:

* **Article Excerpt:** A story regarding the Sodje brothers and fraudulent charges related to their sports foundation.
* **Ground Truth:** Former Premier League footballer Sam Sodje has appeared in court alongside three brothers accused of charity fraud.
* **Generated Summary:** A former Reading defender was cleared of fraud accusations related to a charity called the Sodje Sports Foundation... [The model also generated additional context about the trial].

> **Note:** As a causal LM, the model occasionally continues generating text (such as "Vocabulary Exercises") after the summary. This can be mitigated in production by using stopping criteria or post-processing the output at the first newline or specific token.

---

## 📦 Requirements

To reproduce this result, the following libraries are required:

* `transformers` (v4.57.3 or later)
* `peft` (v0.18.0)
* `bitsandbytes` (v0.49.0)
* `accelerate`
* `datasets`
* `torch`

---

## 🏁 Conclusion

This project successfully demonstrates that a relatively small but powerful model like **Phi-2** can be fine-tuned for complex NLP tasks like abstractive summarization using PEFT techniques. The resulting model provides a balance between performance and computational efficiency, making it suitable for deployment in resource-constrained environments.
