---
title: Fine-tuning process on BIRD Benchmark
tags:
    - fine-tuning
    - machine-learning
    - model-optimization
created: 2025-05-10
---

## Instructions

- Use conda env llama-finetune for fine-tuning
- Try smaller learning rate like: e-6 order
- Try increasing the batch size
- Use label masking so that the model **doesn’t predict the prompt** (just the completion).
- Add compute_metrics() for things like **SQL exact match** or **execution accuracy**.
- Consider saving in .safetensors format (safer for upload).


## Weights and Biases

For visualization of model performance and check the training loss and validation loss curves.
- https://docs.wandb.ai/quickstart/
- https://wandb.ai/rahulsaxena-umass-amherst/huggingface/table?nw=nwuserrahulsaxena
- API Key: <hidden> (Check wandb or notes for the API Key)

https://github.com/huggingface/transformers/issues/7974


### Effect of prompt alignment on fine-tuning

- I experimented with multiple different prompts while training and ultimately decided to go ahead with tagging everything like [SCHEMA] {schema_str}, [QUESTION] {Question_str}

- I also noticed that there was improvement in EX scores of finetuned model when I finetuned with inclusion of columns data type.

- I also tried training without quantization but that just resulted in the trianing loss being increased, and no substantial improvement in EX score on the downstream task. 

### Reducing max_length

- Prompt length reduced to 512, and completion reduced to 128, and max_length became 640
- Slightly bumps up the training loss across similar steps (0.8 vs 0.9)

- Try same prompt on inference which you used during fine-tuning
In Inference time, try giving the prompt with Database ID as well. 

- Try with giving column types as well. 

The above both did have small impact on the EX score on the downstream task. 