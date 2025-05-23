---
title: Unity Guidelines
tags:
    - unity
created: 2025-05-09
---

### General Guidelines
- Really useful - https://docs.unity.rc.umass.edu/documentation/connecting/ssh/
- [Conda on Unity](https://docs.unity.rc.umass.edu/documentation/software/conda/)
- Work directory is fast/ project is slow. Don’t use home for anything really.
- [Guide to Unity SSH connection](https://docs.unity.rc.umass.edu/documentation/connecting/ssh/)

### Creating and activating the conda env

```bash
Conda create —name unity-env python=3.10 -y
Conda activate unity-env
```

### Steps to open an Interactive Session on Unity node in VS Code

- ssh unity
- tmux
- salloc -t 6:00:00 
	- salloc --gres=gpu:a100:2 --time=4:00:00 --mem=32G
- Request GPU Node: salloc --partition=gpu --gres=gpu:1 --mem=64G --cpus-per-task=8 --time=4:00:00
- Request 2080ti for better fine-tuning times

```bash
salloc --gres=gpu:2080ti:1 --mem=24G --cpus-per-task=4 --time=08:00:00 --partition=gpu
```

- squeue —me
- use the job id from tasklist to connect 
- command shift p
- Remote-ssh: <job_id_from_tasklist>.[unity.rc.umass.edu](http://unity.rc.umass.edu)
-  cd 

```bash

cd /work/pi_wenlongzhao_umass_edu/29/users/rahulsaxena 

```


- We can use Dspy for prompt optimization

## Trainer
- Adding evaluation_strategy will also monitor validation loss at the end of every epoch

```py
evaluation_strategy="epoch"
```



