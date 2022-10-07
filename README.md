# DeepLabCut-Installation-and-Use
Learn how to install DeepLabCut on a Windows device and use it to label novel videos.

This is a condensed installation summary that worked for the following system:
Windows 10, Geforce RTX 2080
Installation through Anaconda environment is recommended

## Step 1: Prerequisite
Install Anaconda and Python 3.7 or higher (https://www.anaconda.com/distribution/)

## Step 2: Installing Cuda
There is a CPU and a GPU version, these steps are for the GPU version which requires you to install a nvidia cuda and driver.

For this system, first install cuda 9.0.176 (https://developer.nvidia.com/cuda-downloads) and then nvidia driver 462.31 (https://www.nvidia.com/Download/index.aspx)
for cuda and driver compatibility see https://github.com/DeepLabCut/DeepLabCut/blob/master/docs/installation.md#troubleshooting

In the command prompt, use nvidia-smi and nvcc -V to check what driver and cuda are installed.

## Step 3: clone the DeepLabCut github, for example with git bash

## Step 4: create conda environment
Open anaconda prompt in administrative mode.

In the anaconda prompt:

cd C:\Users\LabMi\Documents\GitHub\DeepLabCut\conda-environments

The .yaml file has the environment setup instructions.
conda env create -f DLC-GPU.yaml

conda activate DLC-GPU

This is a fix to a known bug, (https://github.com/DeepLabCut/DeepLabCut/issues/1106)
conda install -c conda-forge ffmpeg

## Step 5: update DeepLabCut version
The .yaml file will install an old version of deeplabcut ‘2.1.10.4’. The updated version is ‘2.2rc1’ (https://github.com/DeepLabCut/DeepLabCut/wiki/How-to-use-the-latest-GitHub-code).

To check current deeplabcut version:

python

import deeplabcut

deeplabcut.__version__ 

exit()

To update deeplabcut version on windows (for mac and linux use the given ./reinstall.sh file):

pip uninstall deeplabcut 

python setup.py sdist bdist_wheel

pip install C:\Users\LabMi\Documents\GitHub\DeepLabCut\dist\deeplabcut-2.2rc1-py3-none-any.whl 

Recheck deeplabcut version is correct

## Step 6: run testscript.py
After this, running the testscript.py file should hopefully work!

cd C:\Users\LabMi\Documents\GitHub\DeepLabCut\examples

python testscript.py

## Final Environment Details Following Installation 
Using command: conda list cudnn
Name                      Version              Build  Channel
cudnn                     7.6.5.32             h37a4af2_1    conda-forge

Using command: nvcc -V
Cuda compilation tools, release 9.0, V9.0.176

tensorflow version
1.15.5
