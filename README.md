# BEVformer
The baseline of this repository is BEVformer, you can follow the instructions to setup the pre-processed nuScenes dataset.
## Installation
### Create a conda virtual environment and activate it.
```
conda create -n open-mmlab python=3.8 -y
conda activate open-mmlab
```
### Install PyTorch and torchvision following the [official instructions](https://pytorch.org/).
```
pip install h5py
pip install typing-extensions
pip install wheel
pip install torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html
```
### Install gcc>=5 in conda env and mmcv-full.
```
conda install -c omgarcia gcc-5.4
pip install -U openmim
mim install mmengine
mim install 'mmcv>=2.0.0rc4'
mim install 'mmdet>=3.0.0'
```
### Install mmdet and mmseg.
```
pip install mmdet==2.14.0
pip install mmsegmentation==0.14.1
```
### Install mmdet3d from source code.
```
git clone https://github.com/open-mmlab/mmdetection3d.git -b dev-1.x
cd mmdetection3d
pip install -v -e .
```
### Install timm.
```
pip install timm
```
### Clone BEVFormer.
```
git clone https://github.com/fundamentalvision/BEVFormer.git
```
###  Prepare pretrained models.
```
cd BEVFormer
mkdir ckpts
cd ckpts & wget https://github.com/zhiqi-li/storage/releases/download/v1.0/r101_dcn_fcos3d_pretrain.pth
```
## Dataset

Download nuScenes V1.0 full dataset data and CAN bus expansion data [HERE](https://www.nuscenes.org/download). Prepare nuscenes data by running Download CAN bus expansion
```
#create data folder
mkdir data
# download 'can_bus.zip' on data folder and unzip it
unzip can_bus.zip 
#rename can_bus to nuscene
mv can_bus nuscenes
```
##Prepare nuScenes data

We genetate custom annotation files which are different from mmdet3d's
```
cd BEVFormer
python tools/create_data.py nuscenes --root-path ./data/nuscenes --out-dir ./data/nuscenes --extra-tag nuscenes --version v1.0 --canbus ./data
```
