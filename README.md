# pi-HelixNovo
pi-HelixNovo is a de novo sequencing model based on the Transformer architecture, using a MS2 spectrum and its complementary spectrum as inputs and generating the corresponding peptides. The model weights we have trained are avaliable at https://zenodo.org/records/10405582. If you use pi-HelixNovo in your work, please cite the following publication: 

Tingpeng Yang, Tianze Ling, Boyan Sun, Zhendong Liang, Fan Xu, Xiansong Huang, Linhai Xie, Yonghong He, Leyuan Li, Fuchu He, Yu Wang, Cheng Chang, Introducing π-HelixNovo for practical large-scale de novo peptide sequencing, Briefings in Bioinformatics, Volume 25, Issue 2, March 2024, bbae021, https://doi.org/10.1093/bib/bbae021
# The usage of our code
## Preparation:  
Enter the code folder

```
conda env create -f main_env.yaml
conda activate main_env 
```


## Train a model from scratch:

```
python main.py --mode=train --gpu=0 --config=./config.yaml --output=train.log --peak_path=./sample_data/training_set/*.mgf --peak_path_val=./sample_data/validation_set/*.mgf
```

## Evaluate a pretrained model

```
python main.py --mode=eval --gpu=0 --config=./config.yaml --output=evaluate.log --peak_path=./sample_data/validation_set/*.mgf --model=the_path_of_your_model
```

## De novo sequencing

```
python main.py --mode=denovo --config=./config.yaml --gpu=0 --output=denovo.log --peak_path=./sample_data/denovo_sample/*.mgf --model=the_path_of_your_model
```
The results will be shown in the current folder as **denovo**_denovo.txt because --output=**denovo**.log
| TITLE | Peptide | p |  
| :--: | :--: | :--: |  
| 27 | VLEGHAEK | 0.95 |  
| 28 | LQHEAATATQK | 0.93 |  
| 29 | KEAAPPPK | 0.96 |

"TITLE" is the TITLE information of the MS spectrum in the corresponding mgf file, and "p" is the confidence score of the peptide sequence.

## The config.yaml used in pi-HelixNovo
To train models on the nine-species benchmark dataset, please use config.yaml  

To train models on the merged dataset of PXD008808, PXD011246, PXD012645 and PXD012979, please use merge-config.yaml.

To  train models on the MSV000081142 dataset, please use config.yaml


# Recommendation
For practical large-scale de novo peptide sequencing, we highly recommend utilizing the model weight "MSV000081142-epoch-5-step-800000.ckpt", which was trained on the MSV000081142 dataset, while employing the "config.yaml" configuration file.
