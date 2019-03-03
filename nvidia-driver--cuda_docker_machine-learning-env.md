# Install and configure Machine Learning Env for Ubuntu 18.04 LTS (Bionic Beaver)

## Before Start

This doc requires Ubuntu 18.04 LTS (Bionic Beaver), GPU supports driver 410+ (recommend 1080Ti and up) Docker and Nvidia Docker.

### Check current NVidia Driver Version

A supported NVidia driver version is the first step. Using the command to check the current version:

```bash
nvidia-smi
```

In default 18.04 PPA, there is a 390 version and an open source version from Xorg (Nouveau) of NVidia Driver. To see more details, Open **Software & Updates**, then in **Additional Drivers**, apply the tested driver.

P.S. If you want to manually install the nvidia driver, the command to turn off the X11 UI has been changed from lightdm to gdm, using the following one, which will not work!!!:

```bash
sudo service gdm3 stop
```

The correct way is to forbid Nouveau driver, update with command `update-initramfs -u`, then change telinit level with command `telinit 3`.

### Uninstall Existing Drivers

#### Manually Installed Driver

If the driver is installed through bash script, e.g. xxxxx.run, you should manually Uninstall NVidia driver with following command

```bash
sudo ./NVIDIA-Linux-x86-xxxx.run --uninstall
```

### Using Apt to uninstall

If the previous driver is installed from dpkg or apt, using the command:

```bash
# remove GPU Driver
sudo apt remove --purge nvidia-driver-xxx
```

```bash
# remove CUDA
sudo apt remove --purge cuda
```

And expect that happens frequently after every kernel update (annoying), the driver may crashed.

## Install CUDA Toolkit

TODO

### CUDA post install configuration

add following commands to `.bashrc` or `.zshrc`:

```bash
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
Then source the bash or restart.

## Install Docker and NVidia-docker

TODO

## Using PyTorch and Tensorflow/Keras from Docker
In this section, we will cover how to use Docker Images from Tensorflow and PyTorch to build machine learning environments.

TODO

### Using Tensorflow

### Using PyTorch

## Troubleshooting

### Black screen after installing NVidia Driver 4xx

There are many possible reasons to fail the NVidia driver installation. We still recommend using NVidia repository to install both driver and cuda. The common sympton is, after installation, the screen turns to a black screen after login, and all TTY stop working at login(cannot switch throw `ctrl`+`alt`+`Fxx`).

#### Temporary workaround

1. Completely uninstall all previous Cuda and NVidia driver
2. reboot
3. Turnoff GUI through `telinit` mentioned in previous sections
4. Install NVidia driver through apt.
5.  edit GRUB at `/etc/default/grub`, append `nvidia-drm.modeset=1` at the end of `GRUB_CMDLINE_LINUX_DEFAULT` configuration
6. update grub through `sudo update-grub`
7. reboot
8. install cuda through apt
