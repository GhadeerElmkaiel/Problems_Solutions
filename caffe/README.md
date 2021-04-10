# Installing and building caffe library

## Building Opencv

I installed caffe according to the following [link](https://qengineering.eu/install-caffe-on-ubuntu-20.04-with-opencv-4.4.html)  
While installing opencv I had multiple problems.  
one of them is that while building the opencv the following error:

```bash
fatal error: opencv2/core.hpp: No such file or directory
```

This error is because there is no **opencv2** foldinr in ***usr/inculde/*** folder.  
But the wanted folder **opencv2** is located in ***usr/inculde/opencv4/***. So this problem was fixed by copying the folder ***usr/inculde/opencv4/opencv2*** to the position ***usr/inculde/opencv2***.

Eventhough other problems were presented during the building process, but everything was working fine, and I could include cv2.

## Building caffe

When building the library using the code ```make -j$(nproc)```. I faced the error:  
```nvcc fatal : Unsupported gpu architecture 'compute_30```
This error is because I am using cuda 11.0.2 in which the support for architecture **compute_30** has been stopped.

So I needed to edit the Makefile.config file and remove the **compute_30** architecture from the following code-block:

```bash
CUDA_ARCH := -gencode arch=compute_30,code=sm_30 \
             -gencode arch=compute_35,code=sm_35 \
             -gencode arch=compute_50,code=sm_50 \
             -gencode arch=compute_52,code=sm_52 \
             -gencode arch=compute_60,code=sm_60 \
             -gencode arch=compute_61,code=sm_61 \
             -gencode arch=compute_70,code=sm_70 \
             -gencode arch=compute_80,code=sm_80
```
