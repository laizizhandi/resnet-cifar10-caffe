# ResNet 20/32/44/56/110 for CIFAR10 with caffe 
1. create 4 pixel padded training LMDB and testing LMDB, then create a soft link `ln -s cifar-10-batches-py` in this folder.
- directly download it [here](https://github.com/yihui-he/resnet-cifar10-caffe/releases/tag/1.0).
- or you can generate it as follow:
  - get [cifar10 python version](https://www.cs.toronto.edu/~kriz/cifar.html)
  - use [data_utils.py](data_utils.py) to generate 4 pixel padded training data and testing data. Horizontal flip and random crop are performed on the fly while training.
3. use [net_generator.py](net_generator.py) to generate `solver.prototxt` and `trainval.prototxt`, you can generate resnet or plain net of depth 20/32/44/56/110, or even deeper if you want. you just need to change `n` according to `depth=6n+2`  
4. specify caffe path in [train.sh](train.sh), then train networks with `./train.sh [GPUs] [NET]` (eg., `./train.sh 0,1,2,3 resnet-20`, logs can be accessed from 'resnet-20/logs').
5. specify caffe path in [cfgs.py](cfgs.py) and use [plot.py](plot.py) to generate beautful loss plots.

### results are consistent with original paper
seems there's no much difference between resnet-20 and plain-20. However, from the second plot, you can see that plain-110 have difficulty to converge.
![a](plots/resnet-20__2016-08-14_00-25-56plain_orth20__2016-08-14_15-34-29.png)
![b](plots/resnet-110__2016-08-15_10-12-25plain110__2016-08-15_10-11-55.png)

### links
[resnet-imagenet-caffe](https://github.com/yihui-he/resnet-imagenet-caffe)

