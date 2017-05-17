## DLInfBench

### Introduction
Benchmarks of the CNN inference task over some popular deep learning frameworks.

Currently, we support four deep learning frameworks: [Caffe](https://github.com/BVLC/caffe), [Caffe2](https://github.com/caffe2/caffe2), [PyTorch](https://github.com/pytorch/pytorch), [MXNet](https://github.com/dmlc/mxnet). Four commonly used imagenet models, namely alexnet, resnet50, resnet101 and resnet152, are ready to test. For convenience, we provide all the code or network definition files here. There is no need to download pre-trained weights because we will randomly initialize them. A few other networks like inception-v3, vgg19 are also supported in MXNet's and PyTorch's testing scripts. You can try them as you want.

I may add benchmark code for more networks (i.e. inception-bn, inception-v3) and deep learning frameworks (i.e. Tensorflow) in the future but no specific plans have been made yet. Thus, anyone is welcomed to submit PRs.

### Usage
1. Install Caffe, Caffe2, PyTorch and MXNet in your machine and make sure you can import them in python. Turn on CUDNN support if possible. If you only want to test a part of them, please modify "DLLIB_LIST" in `run.sh`.
2. Modify the "GPU" variable in `run.sh` to the gpu device you want to use. (In order to get accurate results, please select a GPU without any other process running on it.)
3. Start benchmark experiments by executing `sh run.sh`.
4. The results of network's inference speed and gpu memory cost will be saved to `cache/results/${DLLIB}_${NETWORK}_${BATCH_SIZE}.txt`. Columns in these files represent "framework name", "network", "batch size", "speed(images/s)", "gpu memory(MB)" respectively.
5. We also plot the benchmark results in pictures as it could make them more straightforward. `cache/results/${NETWORK}_speed.png` demonstrates the network's inference speed of different batch size in different frameworks. `cache/results/${NETWORK}_gpu_memory.png` demonstrates the network's gpu memory cost of different batch size in different frameworks.

----------

### Known Issues
1. There is a problem when I try to run alexnet with CUDNN in caffe2(check the code [here](https://github.com/nicklhy/DLInfBench/blob/master/inference_caffe2.py#L214)). Thus, CUDNN is turned off temporally in caffe2's alexnet benchmarks. If you know how to fix this bug, a PR is welcomed.

----------

### Results

#### Titan X (Pascal)
GPU: Titan X (Pascal)
CPU: Intel(R) Xeon(R) CPU E5-2630 v4 @ 2.20GHz
OS: Ubuntu 16.04 LTS
Nvidia Driver: 375.26
CUDA: 8.0.61
CUDNN: 5.1.5

**AlexNet**

![Speed Benchmark](results/titan_x_pascal/alexnet_speed.png)

![GPU Memory Benchmark](results/titan_x_pascal/alexnet_gpu_memory.png)

**ResNet50**

![Speed Benchmark](results/titan_x_pascal/resnet50_speed.png)

![GPU Memory Benchmark](results/titan_x_pascal/resnet50_gpu_memory.png)

**ResNet101**

![Speed Benchmark](results/titan_x_pascal/resnet101_speed.png)

![GPU Memory Benchmark](results/titan_x_pascal/resnet101_gpu_memory.png)

**ResNet152**

![Speed Benchmark](results/titan_x_pascal/resnet152_speed.png)

![GPU Memory Benchmark](results/titan_x_pascal/resnet152_gpu_memory.png)

----------

### License
This project is licensed under an [Apache-2.0](LICENSE) license.
