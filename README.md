## Supervised finetuning of instruction-following LLMs

[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](https://github.com/daniel-furman/Polyglot-or-Not/blob/main/LICENSE) 
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/release/python-390/) 
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black) 

This repo includes lightweight demos for supervised finetuning (SFT) of large language models (LLMs), like MosaicML's [MPT-7B](https://huggingface.co/mosaicml/mpt-7b).

### Code assets

* See the `./sft` folder for finetuning scripts and postprocessing notebooks.
* See the `./runs` folder for the raw results from each sft experiment.
* See the `./inf_tests` folder for runtime tests on different models.

## Documentation

### SFT is the second step in a typical GPT training pipeline

Below image from "[State of GPTs](https://www.youtube.com/watch?v=bZQun8Y4L2A)" by Andrej Karpathy. 

Key points for SFT:

* Collect small but high-quality datasets in the form of "prompt" and "ideal responses". 
* Do language modeling on this data, nothing changes algorithmically from pretraining. 
* After training we get an SFT model which can be deployed as assistants (and it works to some extent).
* The scripts herein perform full-parameter sft (updates each weight in the network). Other options include parameter-efficient finetuning, see HuggingFace's [peft](https://github.com/huggingface/peft).

![training_pipeline](assets/assistant_training_pipeline.png)

### Models and datasets employed

In this repo, we finetuned small- to medium-sized LLMs on various instruction-following datasets. 

* [MPT-7B](https://huggingface.co/mosaicml/mpt-7b) (Apache 2.0) 

Several instruction-following datasets are tested herein. Each is open-source and licensed for commercial use.

* [timdettmers/openassistant-guanaco](https://huggingface.co/datasets/timdettmers/openassistant-guanaco) (Apache 2.0)
* [ehartford/dolphin](https://huggingface.co/datasets/ehartford/dolphin) (Apache 2.0)

### Runs

1. `runs/jul_5_23_3_15_00_sft-instruction-mpt-7b-orca` ([dfurman/mpt-7b-instruct-orca](https://huggingface.co/dfurman/mpt-7b-instruct-orca))
    * run args: {'lr': 2e-5, 'num_epochs': 1, 'seed': 43}
    * log summary: {'train_runtime': 61098.1062, 'train_samples_per_second': 1.637, 'train_steps_per_second': 0.409, 'train_loss': 1.4058428125, 'epoch': 1.0}

![loss_curves](assets/jul_5_23_3_15_00_log_loss_curves.png)

