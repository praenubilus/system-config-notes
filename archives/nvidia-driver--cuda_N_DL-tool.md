# (Deprecated) Install and configure Deep Learning Env for Ubuntu 18.04 LTS (Bionic Beaver)

## update notes

This doc has already been deprecated. Refer to the latest one using apt and docker to configure and build the environment.

## old contents starts here

The Cuda and NV driver do not suppor 18.04 officially at this time(late August 2018), and the X11 frontend has been changed from Unity in 16.04 to GNOME. Also, the latest tensorflow(1.9) does not support CUDA 9.1 and 9.2 well. Here are some basic steps to make both tensorflow and pytorch work on 18.04.

## Check current NVidia Driver Version
To support and exploit GPU power for these two platforms, a supported NVidia driver version is the first step. Using the command to check the current version:
```bash
nvidia-smi
```
In default 18.04 PPA, there is a 390 version of NVidia Driver which has already been tested. For stable reason, this driver should be considered at first priority. To see more details, Open **Software & Updates**, then in **Additional Drivers**, apply the tested driver.

P.S. If you want to manually install the nvidia driver, the command to turn off the X11 UI has been changed from lightdm to gdm, using the following one:
```bash
sudo service gdm3 stop
```
Manually Uninstall Nvidia driver, if it's installed from **.run script, you can use the following command
```bash
sudo ./NVIDIA-Linux-x86-xxxx.run --uninstall
```
And expect that happens frequently after every kernel update (annoying), the driver may crashed.

## Install CUDA Toolkit and CUDNN (Optional)
**P.S. If you don't write your own cuda code, but just using the Tensorflow and PyTorch, this step actually can be skipped.**
### preinstall check
As mentioned at top, the most stable version currently is CUDA 9.0, and install from _**.run script_ is recommended. Before install, make sure there is no current CUDA version installed. Check using command:
```bash
nvcc --version
```
If there is old CUDA version, it may compatible with newer version(stay in the OS side by side), but it also may cause problem. If the previous CUDA is installed by run script, to uninstall is easy. There should be an uninstall script located at: 
```bash
/usr/local/cuda-9.0/bin/uninstall_cuda_9.0.pl
```
replace the 9.0 with the related cuda version, the old version should be completely uninstalled.

### Q: If it's installed through deb package, how to Uninstall?
The first attempt should using command like following
```bash
sudo apt remove --purge cuda*
```
If that not work, there is a manual workaround:
* delete the folder under `/usr/local/cuda-**`
* manually reinstall the cuda with run script again
* using the uninstall script mentioned in previous steps to completely uninstall

After completely delete the older versions, Download CUDA 9.0 from NVidia official website. Remember to download the run script version for Ubuntu 17.04 unless the official 18.04 version has been published. Steps here will be skipped since it's straight forward. 

Things to mention and notice:

* **DO NOT** install the NVidia driver come with the CUDA toolkits since it may be an older and incompatible version
* Technically the 9.0 driver and toolkits requires GCC 6.0 version, but the ubuntu come with GCC 7. Directly installation will cause the script fail the preinstall check. The work arround is using the `--override` parameter to run the script, which will skip the check step.

### Install CUDNN
Download the version 7 CUDNN for Linux version, which should work with CUDA 9.0. Unzip downloaded package and copy files to related folders:
```bash
# Unpack the archive
tar -zxvf cudnn-9.0-linux-x64-v7.1.tgz

# Move the unpacked contents to your CUDA directory
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
sudo cp cuda/include/cudnn.h /usr/local/cuda-9.0/include/

# Give read access to all users
sudo chmod a+r /usr/local/cuda-9.0/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

### Install CUDA Profiling Tools Interface
```bash
sudo apt install libcupti-dev
```

### CUDA post install configuration
add following commands to `.bashrc` or `.zshrc`:
```bash
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
Then source the bash or restart.

## Install Tensorflow and PyTorch
In this step, we will use Anaconda to install all these two tools in virtualenv, which can better isolate the dependencies and libs.

### Install Anaconda
1. Download Anaconda from [https://www.anaconda.com/download/](https://www.anaconda.com/download/), please choose the python 3.6 version

2. Add executing authorization to the script, then run the install to default location (by default, it's in `anaconda` folder under `home` folder).
    * Add anaconda to path, add following command to `.bashrc` or `.zshrc`: `export PATH=/home/xxxx/anaconda3/bin:$PATH`


3. (optional) Install vscode at the end when prompted.

### Install Tensorflow
1. Create a virtual environment through conda. **P.S. python version must be specified or the venv will use the python and pip in conda, which is not isolated.**
```bash
conda create -n tensorflow python=3.6 numpy scipy matplotlib jupyter
```
By default, the created virtual env resides in `/path/to/anaconda/envs`. Using command `conda env list` will show all venvs. If you want to specify where the venv files will be located, using `--prefix` parameter.

2. Activate the virtual env
```bash
source activate tensorflow
```

3. After the virtual env has been activated, use conda to install tensorflow for GPU
```bash
conda install tensorflow-gpu
conda upgrade tensorflow-gpu
```

4. to test whether the Tensorflow has been isntalled correctly, using following python statements:
```python
from tensorflow.python.client import device_lib

device_lib.list_local_devices()
```
If everything goes well, your CPU and GPU info will be printed.

5. to stop the environment, using the following command
```bash
source deactivate tensorflow
```

### Install PyTorch
To install pytorch, the steps is identical to install the tensorflow, just use following conda command to install:
```bash
conda install pytorch torchvision -c pytorch
```

To test the correctness of installation, using the following python scrpts:
```python
import torch
torch.cuda.is_available()
# Will print True 

import torch
torch.cuda.get_device_name(0)
# Will print 'GeForce xxxxxxx'

import torch
torch.cuda.device_count()
# will print the number of GPUs
```