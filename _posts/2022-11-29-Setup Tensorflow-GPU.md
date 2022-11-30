# Before We Started

Deep Learning has been widely applied into Computer Vision tasks like segmentation and object detection. There are a lot of things for an non-CS major to learn if you want to deploy them in your field of study. As a geologist, learning the algorithms and coding skills can be rewarding and fun. However, setting up the device functionally to run deep learning task is sort of painful. It's frustrating when you're eager to try your ideas but your device hasn't ready for that. If you have a light task to run, you can use [Goolge Colab](https://colab.research.google.com/), and use their free GPU for a while. Nonetheless, when you have a heavy task which needs more than half day to run, it's better to have it run on your own device or upgrade your Google Colab to Pro, so you can sleep well without worrying the runtime in google Colab is interrupted or something. I tried several tutorials and always struggled with the compatible issues among the stuff I need to download. Here's the one I found which is the easiest and require the least efforts finding compatible versions. Modified from [Reference](https://blog.csdn.net/weixin_56197703/article/details/125192385?spm=1001.2014.3001.5506).

# Overview of My Device

- Windows 10 x64
- NVIDA GeForce RTX 3050Ti

# Packages/Tools need to be downloaded

- Driver for NVIDA GPU(Usually included in the CUDA package)
- CUDA
- cuDNN
- `tensorflow-gpu`

# Steps
## Figure out the version bundle you'll install
I have NVIDA Geforce RTX 3050Ti, so I need the relatively latest driver to make my GPU work. Accordingly, I can't choose CUDA whose version is too low, and CUDA 11.6 is a good choice. Based on the CUDA version I chose, the version of cuDNN I need is v8.6.0. 

## Install CUDA 11.6
[Download CUDA 11.6](https://developer.nvidia.com/cuda-11-6-0-download-archive)

- Uncheck Visual Studio Integration while installing

![](https://raw.githubusercontent.com/ZJ-Gao/ZJ-Gao.github.io/main/_images/image-20221130140759534.png)

- Test if CUDA has been sucessfully installed
  - Open cmd, and type `nvcc --version`. 
  - If information about cuda 11.6 shows up, the installation of CUDA is successful.

## Install cuDNN

### Download

[Download cuDNN v 8.6.0](https://developer.nvidia.com/rdp/cudnn-archive)
- You will need to register an NVIDIA account to download cuDNN
- Attention! I accidently downloaded cuDNN v8.1.0 for CUDA 11.2, but that still worked. Not sure why...

### Paste the files in the cuDNN folder you downloaded into CUDA 11.6 folder
- Copy the folders inside the cuDNN, and then paste them into the CUDA 11.6 folder in the Program Files([C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6](C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6)). You goal is to merge the folders with the same name. 
- Add environment variables under the system variables

![](https://raw.githubusercontent.com/ZJ-Gao/ZJ-Gao.github.io/main/_images/image-20221130141735873.png)

You may need admin username and password to access that.

![](https://raw.githubusercontent.com/ZJ-Gao/ZJ-Gao.github.io/main/_images/image-20221130142250712.png)



Click `New` and add the following paths in one by one.

![](https://raw.githubusercontent.com/ZJ-Gao/ZJ-Gao.github.io/main/_images/image-20221130142740920.png)

`
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\bin
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\libnvvp
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\lib
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\include
`

Here's how it will look after you add all the environment variables.

![](https://raw.githubusercontent.com/ZJ-Gao/ZJ-Gao.github.io/main/_images/image-20221130142708127.png)

### Test if the environment variables have been successfully embedded in

1. Open the cmd

```
cd C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6\extras\demo_suite
```

2. Execute the following two commands

```
bandwidthTest.exe
```

```
deviceQuery.exe
```

If you see the `Result = PASS` in the response, great!

## Install `tensorflow-gpu`

You can create a `conda` virtual environment to install the package, or install that in the base environment.

1. Open the cmd

```
pip install -U tensorflow-gpu
```

2. Test if the package has successfully installed

Stay in the cmd and type `python`, then execute the following two commands:

```
import tensorflow as tf
```

```
tf.test.is_gpu_available()
```

If the feedback is `True`, congratulations!! Have fun diving into deep learning!
