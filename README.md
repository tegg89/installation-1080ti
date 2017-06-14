# Installation-1080ti
This repository explains how to install NVIDIA graphic driver (GTX 1080 Ti) on Ubuntu 16.04.





## Target Environment
* Ubuntu 16.04
* CUDA 8.0
* Driver version 381.22





**1. Install CUDA without the driver**

After installed Ubuntu, main graphic driver would be default one. To capture NVIDIA graphic driver, CUDA toolkit should be installed.

  * Go to [here](https://developer.nvidia.com/cuda-downloads) and download CUDA. Make sure to check correct architecture and distribution types. I choosed `runfile(local)`.
  
  * Add following path location into system file (64-bit machine).
  
  > export PATH="/usr/local/cuda/bin:$PATH"
  
  > export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
  
  * After installed, reboot system.


**2. Install driver with apt-get**

  > sudo add-apt-repository ppa:graphics-drivers/ppa
  
  > sudo apt-get update
  
  > sudo apt-get install nvidia-381
  
  * After reboot, the NVIDIA graphic driver would be correctly captured.





## Reference
* http://blog.nelsonliu.me/2017/04/29/installing-and-updating-gtx-1080-ti-cuda-drivers-on-ubuntu/
