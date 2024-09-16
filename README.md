# CSFF-MGDH

SAR Ship Detector Using Cross-stage Feature Fusion and Decoupled Head with Mutual Guidance.

# Preparation work

We have used the following versions of OS and softwares:

- OS:  Windows10
- Python: 3.8
- GPU: RTX3060Ti
- CUDA: 11.2
- PyTorch: 1.9.0+cu111
- TorchVision: 0.10.0+cu111
- TorchAudio: 0.9.0
- MMCV-FULL: 1.3.17
- MMDetection: 2.20.0

## Install

#### a. Create a conda virtual environment and activate it.

```shell
conda create -n csff python=3.8
conda activate csff
```

#### b. Install pytorch, torchvision and torchaudio following the [official instructions](https://pytorch.org/), e.g.,

```shell
pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
```

#### Install mmcv-full(we used mmcv-full==1.3.17)

```shell
pip install openmim
mim install mmcv-full==1.3.17
```

#### d. Install COCOAPI-AITOD for Evaluating on AI-TOD dataset(The VisDrone2019 dataset does not require it)

```shell
pip install "git+https://github.com/jwwangchn/cocoapi-aitod.git#subdirectory=aitodpycocotools"
```

You can also refer to [official instruction](https://github.com/jwwangchn/cocoapi-aitod) for installing COCOAPI-AITOD.

#### e. Install SOD-DEDDH

```shell
git clone https://github.com/SYLan2019/CSFF-MGDH.git
cd CSFF-MGDH
pip install -r requirements.txt
pip install -v -e .
# or "python setup.py install"
```

## Prepare datasets

- [SSDD download link](https://github.com/TianwenZhang0825/Official-SSDD) 

Our data folder structure is as follows:

```shell
SOD-DEDDH
├── mmdet
├── tools
├── configs
├── data
│   ├── coco
│   │   ├── annotations
│   │   │    │─── train.json
│   │   │    │─── test.json
│   │   ├── images
|   |   |    |___train
|   |   |    |    |─── ***.jpg
|   |   |    |    |─── ***.jpg
│   │   │    │─── test
|   |   |    |    |─── ***.jpg
│   │   │    │    |─── ***.jpg
```

If your data folder structure is different, you may need to change the corresponding paths in config files (configs/\_base\_/datasets/coco_detection.py).

## Run

The SOD-DEDDH's config files are in .

Please see MMDetection full tutorials [with existing dataset](docs/1_exist_data_model.md) for beginners.

#### Training(on a single GPU)

```shell
python tools/train.py configs/CSFF_MGDH/
```

#### Testing 

```shell
python tools/test.py configs/CSFF_MGDH/ your_training_weight.pth --eval bbox
```
