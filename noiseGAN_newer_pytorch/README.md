# Synthesizing Camera Noise using Generative Adversarial Networks

## noiseGAN

We provide this implementation adapted to a newer PyTorch version.

This code is based on the [original CycleGAN implementation](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix/).


**Disclaimer:** *The trained models provided for this implementation are not the same used for the manuscript reports. This was done because the models trained in PyTorch 0.3.1 could not be loaded in newer version (PyTorch version > 0.4). Please check the [implementation using PyTorch 0.3.1](../noiseGAN) if you wish to replicate our results.*

## Prerequisites
- Python 3
- NVIDIA GPU + CUDA CuDNN

## Getting Started

### Installation
Please, use a PyTorch version greater or equal to 0.4.1. In the ```requirements.txt``` we specify PyTorch=1.14

You can install the requirements in ```requirements.txt``` using:
```
pip install -r requirements.txt
```

### Training a model
- Run ```python -m visdom.server``` in a console and enter http://localhost:8097 in order to view training results and loss plots.
- Run the train script:
```
python train.py --dataroot_A <path-to-lower-ISO> --dataroot_B <path-to-higher-ISO> --name <name-of-model> --model cycle_gan --no_dropout --lambda_std 10 --lambda_low_freq 10 --n_epochs 50 --n_epochs_decay 0
```
For checking the parameters, please check the files in ```options``` folder.


### Testing our models
- The models used in our TVCG paper were trained using PyTorch 0.3.1. For replicating those results, please check [this directory](../noiseGAN).

- We couldn't load the checkpoints from PyTorch 0.3.1 into 1.14, thus, we have trained new models using PyTorch 1.14 (following the same training strategy). If you wish, you can download the [new trained models](https://drive.google.com/file/d/1INIqDRjVP1n0fvz8T8F55IvGc1znXv_G/) and extract them into the ```checkpoints``` folder; or run the following batch:
```bash
bash ./download_trained_models.sh
```

The following code takes one of the trained models and generates noise for the sample images:
```
python generate_noise.py --dataroot_A ./sample_imgs/SIDD_N_S6_clean --dataroot_B None --name SIDD_cleanTo3200_S6_new_pytorch --model test --dataset_mode single --no_dropout --crop_size 256
```
