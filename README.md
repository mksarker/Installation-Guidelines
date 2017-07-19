# Installation-Guidelines
Installation instructions for Deep Learning Environments on Ubuntu 14.04

Links:
https://github.com/saiprashanths/dl-setup

Please modified as per library as below;

NVIDIA Driver and CUDA

Instruction:
Download nvidia.run file for the relevant GPU.
Once there type: Ctrl + Alt + F1, and login to your user.
sudo apt-get install build-essential
sudo service lightdm stop 
	The top line is a necessary step for installing the driver.
Go to the directory where you have the Nvidia driver, and run
	$ cd Downloads
	$ chmod a+x nvidia.run
	$ sudo ./nvidia.run
	$ after finish then reboot 
After installing Nvidia driver then download cuda.run file the relevant version.
	$ cd Downloads
	$ chmod a+x cuda.run 
	$ sudo ./cuda.run 
=> Press Enter for loong time to Accept EULA conditions
=> Say NO to installing the NVIDIA driver
=>SAY YES to installing CUDA Toolkit + Driver
=>Say YES to installing CUDA Samples
Set Environment path variables:
$ gedit ~/.bashrc
export PATH=/usr/local/cuda-8.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH
*Change depending on your cuda version.
$ after finish then reboot 
Verify the driver version:
$ cat /proc/driver/nvidia/version
Check CUDA driver version:
$ nvcc -V
Test cuda:. Go to your Cuda_Samples folder and type    $make
Go to Cuda_Samples/bin/x86_64/linux/release/ for the demos, and do the two standard checks:
$ ./deviceQuery
to see your graphics card specs and
$ ./bandwidthTest
to check if its operating correctly. Both tests should ultimately output a 'PASS' in your terminal.
[Note: if the Black screen or  login-loops  problem occur the please use ;
$ sudo ./cuda.run --no-opengl-files (for NVIDIA)
$ sudo ./cuda.run --no-opengl-libs (for cuda)]

$ nvidia-smi

Reboot. Everything should be ok. 

⇒> CUDA UNinstall:  s
udo /usr/local/cuda-7.5/bin/uninstall_cuda_7.5.pl
######################################################

Install CUDNN:
cd   /path to the cudNN lib folder/
sudo cp include/cudnn.h /usr/local/cuda/include
sudo cp lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
sudo chmod a+r /usr/local/cuda/include/cudnn.h

Version Test;
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2

###################################################################################

########################################################################
 Caffe

Follow links:
http://sungyulkim11.blogspot.kr/2016/01/how-to-install-caffe-cuda-and-fast-rcnn.html

http://gear.github.io/2017-03-30-caffe-gpu-installation/



And also use some tricks for install perfectly;
Install requirements for python’
$ git clone https://github.com/BVLC/caffe.git
$ cd caffe/python
$ for req in $(cat requirements.txt); do pip install $req; done
$ cd ..
$ cp Makefile.config.example Makefile.config
# Adjust Makefile.config (for example, if using Anaconda Python, or if cuDNN is desired)
$ make all -j $(($(nproc) + 1))
$ make test -j $(($(nproc) + 1))
$ make runtest -j $(($(nproc) + 1))
$ make pycaffe
$ make distribute
#if you make own path for it
mkdir pycaffe
mv distribute/python/caffe pycaffe
# set PYTHONPATH (this should go in your .bashrc or whatever (Please use this)
PYTHONPATH=${HOME}/pycaffe:$PYTHONPATH
or
# u can use by default one (not very effective)
export PYTHONPATH=~/caffe/python:$PYTHONPATH

#build using cmake
cd caffe-master
mkdir build
cd build
cmake ..
#####################################################################################
