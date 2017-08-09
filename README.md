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
  
**3. Verify installation**

  * `nvidia-smi` and `nvcc -V` would be verify installed driver version.
  
  * Go to `NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery` and `make` files. After running file, when the driver information is shown property, graphic driver is properly installed!

//
//
## Install OpenCV 3.3

**1. Install OpenCV dependencies**

`sudo apt-get update`
`sudo apt-get upgrade`

`sudo apt-get install build-essential cmake pkg-config`

`sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev`

`sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev`
`sudo apt-get install libxvidcore-dev libx264-dev`

`sudo apt-get install libgtk-3-dev`

`sudo apt-get install libatlas-base-dev gfortran`


**2. Download the OpenCV source**

`cd ~
wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.3.0.zip
unzip opencv.zip`

`wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.3.0.zip
unzip opencv_contrib.zip`


**3. Configuring and compiling OpenCV**

`source activate cv
cd ~/opencv/
mkdir build
cd build`

`cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D WITH_CUDA=ON \
    -D ENABLE_FAST_MATH=1 \
    -D CUDA_FAST_MATH=1 \
    -D WITH_CUBLAS=1 \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.3.0/modules \
    -D PYTHON_EXECUTABLE=~/anaconda3/envs/cv/bin/python \
    -D WITH_GTK=ON \
    -D BUILD_EXAMPLES=ON ..`
    
`make -j4`

`make install`

`sudo ldconfig`


**4. Finish OpenCV install**

The file `cv2.cpython-35m-x86-_64-linux-gnu.so` needs to be renamed and sym-linked.

`cd ~/usr/local/lib/python3.5/site-packages/
sudo mv cv2.cpython-35m-x86-_64-linux-gnu.so cv2.so`

`cd ~/anaconda3/envs/cv/lib/python3.5/site-packages/
ln -s /usr/local/lib/python3.5/site-packages/cv2.so cv2.so`


At this stage, try import cv2 via python. If error message does not shown, then you have completely installed opencv.
In my case, `libstdc++.so.6: version GLIBCXX_3.4.21 not found` message was shown.
`conda install libgcc` can resolve this error.



## Reference
* http://blog.nelsonliu.me/2017/04/29/installing-and-updating-gtx-1080-ti-cuda-drivers-on-ubuntu/

* http://www.pyimagesearch.com/2016/10/24/ubuntu-16-04-how-to-install-opencv/

* https://github.com/BVLC/caffe/issues/4953
