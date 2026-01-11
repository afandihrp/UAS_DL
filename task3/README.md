# Fine-Tuning Phi-2 for Abstractive Summarization (Task 3)

This project focuses on adapting the **Phi-2** model (2.7 billion parameters) for the task of abstractive text summarization using the **XSum (Extreme Summarization)** dataset. The goal is to generate concise, one-sentence summaries from long news articles.

## 🛠️ Methodology & Optimization

Due to the model size and hardware constraints (specifically a **5.67GB GPU**), several memory-saving techniques were implemented:

* **4-bit Quantization:** Utilized the `BitsAndBytesConfig` (NF4 type) to load the model in a highly compressed format.
* **LoRA (Low-Rank Adaptation):** Only **0.37%** of the total parameters (approx. 10.48 million) were made trainable, focusing on the attention layers (`q_proj`, `k_proj`, `v_proj`, and `dense`).
* **Gradient Checkpointing:** Enabled to significantly reduce VRAM usage during the training process.
* **Instruction Prompting:** Formatted data into a specific "Instruction-Article-Summary" template to guide the model's causal language modeling toward summarization.

## 📊 Training Details

* **Dataset Size:** A subset of **5,000 training samples** and **500 validation samples** was used for efficiency.
* **Batch Configuration:** A per-device batch size of 1 with **8 gradient accumulation steps**, resulting in an effective batch size of 8.
* **Training Performance:** The model completed 1 epoch (625 steps) in approximately **1 hour and 38 minutes**.
* **Loss Metrics:** The training achieved a final validation loss of **2.118299**.
