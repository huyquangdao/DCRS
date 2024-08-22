# Broadening the View: Demonstration-augmented Prompt Learning for Conversational Recommendation

This repo contains code and data for the paper: "Broadening the View: Demonstration-augmented Prompt
Learning for Conversational Recommendation".

## 1. Setup

Please install the libraries, and packages listed in the conv/requirements.txt file. Make sure that you are using CUDA 11.6. Otherwise, some unexpected behaviors might happen.

## 2. Data Preprocessing

You can download the processed data (including conv, rec, and retrieval data) from the following <a href = 'https://drive.google.com/drive/folders/1kEOn-lDQ9L5NgBhohg4Upwo9Kr4T01a6?usp=share_link'>link</a>.

For a fair comparison, we adopted the code from <a href='https://github.com/zxd-octopus/VRICR/tree/master'>VRICR</a> and <a href = 'https://github.com/wxl1999/UniCRS/tree/main'>UNICRS </a> to process data for the recommendation engine and dialogue module respectively. 

## 3. Training Retrieval Module:

We build our retrieval module based on <a href='https://github.com/princeton-nlp/SimCSE'>SimCSE </a>. First, you need to generate data which is utilized to train our retrieval model.
```
python gen_data_for_retrieval.py
```
To train our retrieval module, please run
```
cd retrieval
sh run_unsup_example.sh
```
To generate retrieval data, please run

```
python test.py
```

## 4. Training Response Generation Model

For the ReDial dataset, to train our response generation model, please run:

```
cd conv
sh scripts/train_conv_retrieval_redial.sh
```

To produce generated responses, please run the following command:

```
sh scripts/infer_retrieval.sh
```

## 5. Training Recommendation Engine

To train our recommendation engine, you need to first pre-train neural embeddings of demonstrations. 

```
cd rec
sh scripts/pretrain.sh
```

To finetune our recommendation engine, please following commands:

```
sh scripts/train_rec.sh
```

## Acknowledgement
We thank <a href='https://github.com/zxd-octopus/VRICR/tree/master'>VRICR</a> and <a href = 'https://github.com/wxl1999/UniCRS/tree/main'>UNICRS </a> for providing the useful source code for the data preprocessing and prompt learning steps.

Please cite the following our paper as references if you use our codes or the processed datasets.

```bibtex
@inproceedings{10.1145/3626772.3657755,
author = {Dao, Huy and Deng, Yang and Le, Dung D. and Liao, Lizi},
title = {Broadening the View: Demonstration-augmented Prompt Learning for Conversational Recommendation},
year = {2024},
isbn = {9798400704314},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3626772.3657755},
doi = {10.1145/3626772.3657755},
booktitle = {Proceedings of the 47th International ACM SIGIR Conference on Research and Development in Information Retrieval},
pages = {785–795},
numpages = {11},
keywords = {conversational recommendation, demonstration-based learning},
location = {Washington DC, USA},
series = {SIGIR '24}
}
```
