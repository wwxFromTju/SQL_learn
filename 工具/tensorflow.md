# Macbook pro 下安装GPU版本的tensor flow

具体下载地址可能改变
 
 
Mac OS X, GPU enabled, Python 3.4 or 3.5,这步也可以直接在下面之后直接输入:


```
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow-0.10.0-py3-none-any.whl
```

使用pip3安装

```
# Python 3
$ sudo pip3 install --upgrade $TF_BINARY_URL
```

安装GPU版本需要的一些相关依赖（CPU）版本不需要

```
$ brew install bazel swig
```

```
$ brew install coreutils
$ brew tap caskroom/cask
$ brew cask install cuda
```

配置cuda

```
export CUDA_HOME=/usr/local/cuda
export DYLD_LIBRARY_PATH="$DYLD_LIBRARY_PATH:$CUDA_HOME/lib"
export PATH="$CUDA_HOME/bin:$PATH"
```

下载需要的cuDNN v5

```
$ sudo mv include/cudnn.h /Developer/NVIDIA/CUDA-7.5/include/
$ sudo mv lib/libcudnn* /Developer/NVIDIA/CUDA-7.5/lib
$ sudo ln -s /Developer/NVIDIA/CUDA-7.5/lib/libcudnn* /usr/local/cuda/lib/
```


在这里有个问题，如果现在启动的时候，会出现`segmentation fault`,这是一个问题，在安装教程中没有。
解决方案：

直接增加一个软链接即可

```
sudo ln -s /usr/local/cuda/lib/libcuda.dylib /usr/local/cuda/lib/libcuda.1.dylib
```


