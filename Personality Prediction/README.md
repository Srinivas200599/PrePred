# Language Models and Automated Personality Prediction

This repository contains code for the paper [Bottom-Up and Top-Down: 
Predicting Personality with Psycholinguistic and Language Model Features](https://www.semanticscholar.org/paper/Bottom-Up-and-Top-Down%3A-Predicting-Personality-with-Mehta-Fatehi/a872c10eaba767f82ca0a2f474c5c8bcd05f0d44), published in **IEEE International Conference of Data Mining 2020**.

Here are a set of experiments written in tensorflow + pytorch to explore automated personality detection using Language Models on the Essays dataset (Big-Five personality labelled traits) and the Kaggle MBTI dataset.


## Installation


See the requirements.txt for the list of dependent packages which can be installed via:

```bash
pip -r requirements.txt
```

## Usage for MLP Algo
First run the LM extractor code which passes the dataset through the language model and stores the embeddings (of all layers) in a pickle file. Creating this 'new dataset' saves us a lot of compute time and allows effective searching of the hyperparameters for the finetuning network. Before running the code, create a pkl_data folder in the repo folder. All the arguments are optional and passing no arguments runs the extractor with the default values.

```bash
python LM_extractor.py -dataset_type 'essays' -token_length 512 -batch_size 32 -embed 'bert-base' -op_dir 'pkl_data'
```

Next run the finetuning network which is currently a MLP.

```bash
python finetuneNet.py
```


## Usage for CNN Algo

First run sent_bert.py in finetune_models folder to get sentence wise embeddings of all articles.

```bash
python3 finetune_models/sent_bert.py -g -l 100 data/bert_cnn.csv data/train_bert.tsv
```
next run the CNN_bert.py file to pass the embeddings through CNN algorithm.
Need to change index in line 31 of  CNN_bert.py (range 2-5) for predicting each category of MBTI.

```bash
python CNN_bert.py data/train_bert.tsv
```

## Citation

If you find this repo useful for your research, please cite it using the following BibTex entry:

```
@inproceedings{mehtabottom,
  title={Bottom-Up and Top-Down: Predicting Personality with Psycholinguistic and Language Model Features},
  author={Mehta, Yash and Fatehi, Samin and Kazameini, Amirmohammad and Stachl, Clemens and Cambria, Erik and Eetemadi, Sauleh},
  booktitle={Proceedings of the International Conference of Data Mining},
  Organization = {IEEE},
  year={2020}}
}
```
