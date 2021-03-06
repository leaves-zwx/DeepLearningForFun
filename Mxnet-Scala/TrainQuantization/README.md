# MXNET-Scala TrainQuantization
Simpfly implementation of Quantization Aware Training[1][2] with MXNet-scala module. 


## Setup
Tested on Ubuntu 14.04

### Requirements

* sbt 0.13 http://www.scala-sbt.org/
* Mxnet v1.4 https://github.com/dmlc/mxnet

### Build steps

1, compile MXNet with CUDA, then compile the scala-pkg，doc： https://github.com/dmlc/mxnet/tree/master/scala-package

2, under the Mxnet-Scala/TrainQuantization folder:
```bash
 mkdir lib;
 ln -s $MXNET_HOME/scala-package/assembly/target/mxnet-full_2.11-INTERNAL.jar lib
```

3, run `sbt` and then compile the project

## Train vgg on Cifar10
Using the script `train_vgg16_cifar10.sh` under the scripts folder to train vgg from scratch on Cifar10:

```bash
FINETUNE_MODEL_EPOCH=-1
FINETUNE_MODEL_PREFIX=$ROOT/models/
```
Or you can finetune with the provided pretrain model:

```bash
FINETUNE_MODEL_EPOCH=46
FINETUNE_MODEL_PREFIX=$ROOT/models/cifar10_vgg16_acc_0.8772035
```

I did not use any data augmentation and carefully tune the hyper-parameters during training, the best accuracy I got was 0.877, worse than the best accracy 0.93 reported on Cifar10.

## Train vgg with fake quantization on Cifar10
Using the script `train_quantize_vgg16_cifar10.sh` under the scripts folder to train vgg with fake quantization on Cifar10,
you must provide the pretrained model:

```bash
FINETUNE_MODEL_EPOCH=46
FINETUNE_MODEL_PREFIX=$ROOT/models/cifar10_vgg16_acc_0.8772035
```

If everything goes right, you should get almost the same accuray with pretrained model after serveral epoch.

## Test vgg with simulated quantization on Cifar10
Using the script `test_quantize_vgg16_cifar10.sh` under the scripts folder to test pretrained fake quantization vgg with simulated quantization on Cifar10, you must provide the pretrained model:

```bash
FINETUNE_MODEL_EPOCH=57
FINETUNE_MODEL_PREFIX=$ROOT/models/cifar10_quantize_vgg16_acc_0.877504
```

## Reference
[1] Quantizing deep convolutional networks for efficient inference: A whitepaper. https://arxiv.org/pdf/1806.08342.pdf

[2] Quantization and Training of Neural Networks for Efficient Integer-Arithmetic-Only Inference. 
 https://arxiv.org/pdf/1712.05877.pdf
