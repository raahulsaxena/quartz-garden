---
title: Important Commands
tags:
    - conda
    - environment
    - setup
    - unity
---

# Important Commands

### To create a new environment:

```bash
conda create --name 696hw1 python=3.9.7 pip

# sample usage: conda create -p /work/pi_wenlongzhao_umass_edu/29/users --name 696-spotify
```

### To list the environments:

```bash
conda info --envs
```



### Work guidelines

You need to activate conda environment every time you login ( this can be automatically done by modifying your bash rc file too). Before you can activate the conda environment, you need to load the conda.

```bash
# load conda
module load conda/latest

# activate the conda env
conda activate 696ds-spotify
```

If you're starting the work for the first time (have not fetched the common environment ever), make sure to create the new environment using the environment.yml .  This command is **not** needed for subsequent logins in unity and you can just use the update command for pulling the changes.

```bash
conda env create -f environment.yml
```

**Important**: Every time a environment yaml is changed, below command is required to fetch the changes. This will fetch all the new libraries or packages that other users might have installed.

```bash

conda env update -f environment.yml

```


Whenever you are done working (if you've installed new packages), you export it as a yml file. This will enable you to capture a snapshot of all the existing and new libraries that you have currently in your environment.

```bash
conda env export > environment.yml
```


**Note:** Make sure when you're exporting the yaml file, you are in the correct env - 696ds-spotify, otherwise it will overwrite the yaml file with your home directory env, and not update the shared environment !!!


### Copying a file from your local to unity

```bash

scp /path/to/local/file username@remote_host:/path/to/remote/directory

```


