<h1> Human Falling Detection and Tracking </h1>

Using Tiny-YOLO oneclass to detect each person in the frame and use 
[AlphaPose](https://github.com/MVIG-SJTU/AlphaPose) to get skeleton-pose and then use
[ST-GCN](https://github.com/yysijie/st-gcn) model to predict action from every 30 frames 
of each person tracks.

Which now support 7 actions: Standing, Walking, Sitting, Lying Down, Stand up, Sit down, Fall Down.

<div align="center">
    <img src="sample1.gif" width="416">
</div>

## Prerequisites

- Python > 3.6
- Pytorch > 1.3.1

 test run on: Jetson-Nano, Maxwell, CUDA 10.2

## Data

This project has trained a new Tiny-YOLO oneclass model to detect only person objects and to reducing 
model size. Train with rotation augmented [COCO](http://cocodataset.org/#home) person keypoints dataset 
for more robust person detection in a variant of angle pose.

For actions recognition used data from [Le2i](http://le2i.cnrs.fr/Fall-detection-Dataset?lang=fr)
Fall detection Dataset (Coffee room, Home) extract skeleton-pose by AlphaPose and labeled each action 
frames by hand for training ST-GCN model.

## Pre-Trained Models

- Tiny-YOLO oneclass - [.pth](https://drive.google.com/file/d/1obEbWBSm9bXeg10FriJ7R2cGLRsg-AfP/view?usp=sharing),
[.cfg](https://drive.google.com/file/d/19sPzBZjAjuJQ3emRteHybm2SG25w9Wn5/view?usp=sharing)
- SPPE FastPose (AlphaPose) - [resnet101](https://drive.google.com/file/d/1N2MgE1Esq6CKYA6FyZVKpPwHRyOCrzA0/view?usp=sharing),
[resnet50](https://drive.google.com/file/d/1IPfCDRwCmQDnQy94nT1V-_NVtTEi4VmU/view?usp=sharing)
- ST-GCN action recognition - [tsstg](https://drive.google.com/file/d/1mQQ4JHe58ylKbBqTjuKzpwN2nwKOWJ9u/view?usp=sharing)

## Basic Use

1. Download all pre-trained models into ./Models folder.
2. Run main.py
```
    python main.py ${video file or camera source}
```

## At Jetson

if you have a trouble that illegal instruction


```
    export OPENBLAS_CORETYPE=ARMV8 python
``` 
I installed pytorch 1.10.2 relate with CUDA 10.2
It has a error

import torch
#####  Returns a bool indicating if CUDA is currently available.
torch.cuda.is_available()
#####  False

So I find this Page

https://blog.naver.com/PostView.naver?blogId=sonyi&logNo=222288776176&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView

## Reference

- AlphaPose : https://github.com/Amanbhandula/AlphaPose
- ST-GCN : https://github.com/yysijie/st-gcn
- Troule&Shooting
  https://forums.developer.nvidia.com/t/illegal-instruction-core-dumped-xavier/166278
