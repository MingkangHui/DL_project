# A much more Closer Look at Few-shot Classification

This is based on the paper [A Closer Look at Few-shot Classification](https://arxiv.org/abs/1904.04232) in International Conference on Learning Representations (ICLR 2019). 
In this project, we do testing on baseline and baseline++ to see the performace of ResNet10, ResNet 18 and ResNet34 on different tasks.

This project could do the process of downloading and preprocessing, training and model saving, and testing for different tasks.

## Enviroment
 - Python3
 - [Pytorch](http://pytorch.org/) before 0.4 (for newer vesion, please see issue #3 )
 - json

## Getting started
### CUB
* Change directory to `./filelists/CUB`
* the download is deprecated so you need to download CUB dataset manually in `./filelists/CUB` 
* run `source ./download_CUB.sh` to do later works


### mini-ImageNet
* Change directory to `./filelists/miniImagenet`
* the download is deprecated so you need to download miniImagenet dataset manually in `./filelists/miniImagenet` 
* run `source ./download_miniImagenet.sh` to do later works

### mini-ImageNet->CUB (cross)
* Finish preparation for CUB and mini-ImageNet and you are done!

## Train
Run
```python ./train.py --dataset [DATASETNAME] --model [BACKBONENAME] --method [METHODNAME] [--OPTIONARG]```

For example, In our training, we run `sudo python3 ./train.py --dataset miniImagenet --model ResNet18 --method baseline --train_aug --stop_epoch 75`  to test on ResNet18.
Commands below follow this example, and please refer to io_utils.py for additional options.

## Save features
Save the extracted feature before the classifaction layer to increase test speed. 
Run
```python ./save_features.py --dataset miniImagenet --model ResNet18 --method baseline --train_aug --acc 30```
You need to specify acc to save models by training epochs, in this case ```--acc 30``` means that we save models for 30th epochs.


## Test
Run commands like
```sudo python3 ./test.py --dataset miniImagenet --model ResNet18 --method baseline --train_aug --split novel_30```
In this command ```split``` is used to track which model we want to test, novel_30 means the one of 30th epoch training.


## Results
* The test results will be recorded in `./record/results.txt`

* Here is the results for testing on miniImageNet

| Models|Baseline|Baseline++|
|  ---- |  ----  | ----  |
|ResNet10-30|73.82% +- 0.63%|72.92% +- 0.66%
|ResNet10-50|75.48% +- 0.63%|73.02% +- 0.64%
|ResNet10-70|75.22% +- 0.61%|73.57% +- 0.64%
|ResNet18-30|74.48% +- 0.64%|73.21% +- 0.67%
|ResNet18-50|73.84% +- 0.65%|74.20% +- 0.67%
|ResNet18-70|74.86% +- 0.66%|74.44% +- 0.70%
|ResNet34-30|72.92% +- 0.67%|71.66% +- 0.65%
|ResNet34-50|73.21% +- 0.62%|73.35% +- 0.65%
|ResNet34-70|74.35% +- 0.63%|73.22% +- 0.65%

* Here is the results for testing Accuracy on cross domain, MiniImagent -> CUB

  
| Models|Baseline|Baseline++|
|  ---- |  ----  | ----  |
|ResNet10-30|62.35% +- 0.74%|60.62% +- 0.75%
|ResNet10-50|65.07% +- 0.74%|60.80% +- 0.71%
|ResNet10-70|64.80% +- 0.73%|61.29% +- 0.74%
|ResNet18-30|64.67% +- 0.75%|62.46% +- 0.78%
|ResNet18-50|65.90% +- 0.70%|63.51% +- 0.77%
|ResNet18-70|66.38% +- 0.71%|63.42% +- 0.75%

* For other results you could reference our slides in the ```./record```.
