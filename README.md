# GolfDB: A Video Database for Golf Swing Sequencing

The code in this repository is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/). 

## Introduction

GolfDB는 골프 스포츠의 general recognition applications, 특히 골프 스윙 sequencing 작업을 위해 생성된 고품질 비디오 데이터 세트입니다.

이 repo에는 [paper](https://arxiv.org/abs/1903.06528)에 제시된  SwingNet baseline model의 간단한 PyTorch 구현이 포함되어 있습니다.

이 모델은 **without any data augmentation** split 1에서 훈련되었으며 평균 PCE 71.5%를 달성했습니다 (논문에 보고된 76.1%의 PCE는 horizontal flipping 및 affine 
transformations을 포함한 데이터 확대에 기여함).

이 repo를 사용하는 경우 GolfDB 논문을 인용하세요:

```
@InProceedings{McNally_2019_CVPR_Workshops,
author = {McNally, William and Vats, Kanav and Pinto, Tyler and Dulhanty, Chris and McPhee, John and Wong, Alexander},
title = {GolfDB: A Video Database for Golf Swing Sequencing},
booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR) Workshops},
month = {June},
year = {2019}
}
```

## Dependencies
* [PyTorch](https://pytorch.org/)

* 먼저 아래 명령어를 통해 코드를 실행할 준비를 해주세요. 

```
pip install -r requirements.txt
```

## Getting Started

[generate_splits.py](./data/generate_splits.py)를 실행하여 .mat dataset file을 dataframe으로 변환하고 4 splits을 생성합니다.

### Train

* 160x160의 프레임 크기에 대해 사전 처리된 비디오 클립을 제공했습니다([여기에서 다운로드](https://drive.google.com/file/d/1uBwRxFxW04EqG87VCoX3l6vXeV5T5JYJ/view?usp=sharing)). 사전에 다운받은 'videos_160.zip'을 풀어 'videos_160'폴더를 [data](./data/)에 넣는다. 다른 입력 구성을 사용하려면 YouTube 비디오(데이터 세트에 제공된 URL)를 다운로드하고 비디오를 직접 전처리해야 합니다. 이를 돕기위해 [preprocess_videos.py](./data/preprocess_videos.py)가 제공됩니다.

* 이 [repository](https://github.com/tonylins/pytorch-mobilenet-v2)에서 weights가 pretrained된 MobileNetV2를 다운받고 root directory에 'mobilenet_v2.pth.tar'를 놓으세여

* Run [train.py](train.py)

### Evaluate

* 위의 단계에 따라 자신의 모델을 훈련시키거나 [여기에서](https://drive.google.com/file/d/1MBIDwHSM8OKRbxS8YfyRLnUBAdt0nupW/view?usp=sharing) 사전 훈련된 가중치를 다운로드하십시오. 'models' directory를 만들지 않았다면 만들고 이 directory에 'swingnet_1800.pth.tar'를 두세요.

* Run [eval.py](eval.py). If using the pre-trained weights provided, the PCE should be 0.715.  

### Test your own video

* pre-trained weights를 다운로드하려면 위의 단계를 따르십시오. 그런다음 터미널에 다음과 같이 입력하세요: `python3 test_video.py -p test_video.mp4`

* **Note:** 이 코드를 사용하려면 샘플 비디오를 crop하고 single golf swing을 바인딩해야 합니다.

I used online video [cropping](https://ezgif.com/crop-video) and [cutting](https://online-video-cutter.com/) 
tools for my golf swing video. See test_video.mp4 for reference.

Good luck!
