# Deep-HM-SORT

This is the unofficial code for paper "Deep HM-SORT: Enhancing Multi-Object Tracking in Sports with Deep Features, Harmonic Mean, and Expansion IOU". [Paper](https://arxiv.org/abs/2406.12081)

The code is originally modified from [Deep_EIOU](https://github.com/hsiangwei0903/Deep-EIoU)

## Setup Instructions

* Clone this repo, and we'll call the directory that you cloned as {Deep-EIoU Root}
* Install dependencies.
```
conda create -n DeepEIoU python=3.7
conda activate DeepEIoU

# Install pytorch with the proper cuda version to suit your machine
# We are using torch==1.13.0 torchvision==0.14.0 torchaudio==0.13.0 with cuda==11.6

cd Deep-EIoU/reid
pip install -r requirements.txt
pip install cython_bbox
python setup.py develop
cd ..
```

## Reproduce on SportsMOT dataset

### 1. Data preparation for reproduce on SportsMOT dataset

To reproduce on the SportsMOT dataset, you need to download the detection and embedding files from [drive](https://drive.google.com/drive/folders/14gh9e5nQhqHsw77EfxZaUyn9NgPP0-Tq?usp=sharing)

Please download these files and put them in the corresponding folder.

```
{Deep-EIoU Root}
   |——————Deep-EIoU
   └——————detection
   |        └——————v_-9kabh1K8UA_c008.npy
   |        └——————v_-9kabh1K8UA_c009.npy
   |        └——————...
   └——————embedding
            └——————v_-9kabh1K8UA_c008.npy
            └——————v_-9kabh1K8UA_c009.npy
            └——————...
```

### 2. Run tracking on SportsMOT dataset
Run the following commands, you should see the tracking result for each sequences in the interpolation folder.
Please directly zip the tracking results and submit to the [SportsMOT evaluation server](https://codalab.lisn.upsaclay.fr/competitions/12424#participate).

```
python tools/sport_track.py --root_path <Deep-EIoU Root>
python tools/sport_interpolation.py --root_path <Deep-EIoU Root>
```

## Demo on custom dataset

### 1. Model preparation for demo on custom dataset
To demo on your custom dataset, download the detector and ReID model from [drive](https://drive.google.com/drive/folders/1wItcb0yeGaxOS08_G9yRWBTnpVf0vZ2w) and put them in the corresponding folder.

```
{Deep-EIoU Root}
   └——————Deep-EIoU
            └——————checkpoints
                └——————best_ckpt.pth.tar (YOLOX Detector)
                └——————sports_model.pth.tar-60 (OSNet ReID Model)
```

### 2. Demo on custom dataset
Demo on our provided video
```
python tools/demo.py
```
Demo on your custom video
```
python tools/demo.py --path <your video path>
```

Demo on your custom image
```
python tools/demo_image.py --path <your image path>
```

## Modified Part

### Deep_HM_SORT.py
The tracking algorithm of Deep_HM_SORT

### demo_image.py
Demo on the images by using Deep_HM_SORT

## Acknowledgements
The code is based on [ByteTrack](https://github.com/ifzhang/ByteTrack), [Torchreid](https://github.com/KaiyangZhou/deep-person-reid), [BoT-SORT](https://github.com/NirAharon/BoT-SORT) and [Deep_EIOU](https://github.com/hsiangwei0903/Deep-EIoU), thanks for their wonderful work!

## Contact
Kuang-Ming Chen(kmchen@uw.edu)
