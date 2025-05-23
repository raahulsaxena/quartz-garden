---
title: Fine Tuning Flow Chart
tags: [fine-tuning, LLM, LoRA, quantization, training]
created: 2024-06-07
updated: 2024-06-07
---


 Key Concepts Embedded in fine-tuning Script

| **Concept**            | **What It Does**                                               |
| ---------------------- | -------------------------------------------------------------- |
| **Prompt+Completion**  | Mimics OpenAI-style supervised instruction tuning              |
| **LoRA**               | Lightweight, efficient finetuning over select parameters       |
| **4-bit Quantization** | Dramatically reduces memory, makes 1B models fit in 10GB GPUs  |
| **Flash Attention 2**  | Faster training, reduced memory for long sequences             |
| **Trainer**            | Automates batching, logging, gradient accumulation, evaluation |
| **Validation Split**   | Lets you track generalization (prevents overfitting)           |
| **W&B Logging**        | Tracks metrics like loss across epochs                         |


```text
┌────────────────────┐
│ Load JSON Dataset  │   ←── BIRD mini_train_data.json
└────────┬───────────┘
         ↓
┌────────────────────────────────────┐
│ Format into Prompt + Completion    │
│ e.g.,                              │
│ Prompt:                            │
│   You are a helpful...             │
│   Question: ...                    │
│   Evidence: ...                    │
│   SQL:                             │
│ Completion: " SELECT ..."          │
└────────┬───────────────────────────┘
         ↓
┌────────────────────┐
│ Tokenize           │
│ (truncate + pad)   │
└────────┬───────────┘
         ↓
┌────────────────────────────┐
│ Add Labels = input_ids     │
│ (so model learns to        │
│ predict the full sequence) │
└────────┬───────────────────┘
         ↓
┌────────────────────┐
│ Train/Test Split   │
│ (90/10)            │
└────────┬───────────┘
         ↓
┌──────────────────────────────────────────┐
│ Load LLaMA 3.1B with Unsloth             │
│ → 4-bit quantization (bnb)               │
│ → Flash Attention 2                      │
│ → LoRA (r=8, dropout=0.05, alpha=16)     │
└────────┬─────────────────────────────────┘
         ↓
┌────────────────────────────────────────────┐
│ HuggingFace Trainer                        │
│ → Model trains on train_dataset            │
│ → Validates on val_dataset                 │
│ → Saves model every epoch                  │
│ → Logs to Weights & Biases                 │
└────────┬───────────────────────────────────┘
         ↓
┌────────────────────────────┐
│ Evaluate on validation set │
│ → Print final metrics      │
└────────┬───────────────────┘
         ↓
┌───────────────────────────┐
│ Save final model + tokenizer │
└───────────────────────────┘

```

