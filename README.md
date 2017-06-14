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

Compatible driver version for GTX 1080 Ti is 381 series. Previous trial was directly installing driver using `sudo apt-get`. However with this method, OS cannot properly capture driver for unknown reason. Therefore I downloaded the latest version of driver runfile from NVIDIA homepage.

  * Go to [here](http://www.nvidia.com/Download/index.aspx) and selected the appropriate graphic driver version. Make sure the version is same or upper than 381 series. 
  
  * Stop the X server and install driver.
  
  * After reboot, the NVIDIA graphic driver would be correctly captured.
  
**3. Verify installation

  * `nvidia-smi` and `nvcc -V` would be verify installed driver version.
  
  * Go to `NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery` and `make` files. After running file, when the driver information is shown property, graphic driver is properly installed!






## Reference
* http://blog.nelsonliu.me/2017/04/29/installing-and-updating-gtx-1080-ti-cuda-drivers-on-ubuntu/
