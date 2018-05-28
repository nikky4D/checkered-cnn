Checkered Convolutional Neural Networks
===========================================

<center>

Traditional          |  Checkered
:-------------------------:|:-------------------------:
![Traditional subsampling](visualize_output/traditional_animation.gif)  |  ![Checkered subsampling](visualize_output/lattice_animation.gif)

</center>

- Paper: TBA
- Slides: https://docs.google.com/presentation/d/1LU467UZQmdr9Vzfv39myZ7Ys4JVjIYiGiReDoTGdDPQ/edit?usp=sharing

We present a new technique for increasing the receptive field of CNNs, checkered subsampling. Checkered subsampling layers generate drastically more informative feature maps than traditional subsampling layers and significantly improve the accuracy of modern CNNs in our experiments. Unlike dilation, checkered subsampling performs subsampling and reduces the complexity of deep layers. Checkered subsampling is part of a wider range of techniques we call multisampling.

This repository contains:
- Implementations of checkered layers and a conversion script for converting traditional CNNs into checkered CNNs (CCNNs) in **checkered_layers.py**. 
- A script for visualizing the patterns created by checkered subsampling in **visualizer.py**. 
- Scripts for training our toy CCNN on MNIST (**demo_mnist.py**) and modern models on CIFAR (**demo_cifar.py**).
- The implementations of DenseNet, ResNet, and VGG that we used in our paper under **models/**.
- Our implementation of tiny ResNet under models/ and our toy CCNN defined in demo_mnist.py.

Checkered subsampling improves the accuracy of every architecture we test (VGG, DenseNet, Wide-ResNet, ResNet). Our tiny ResNet CCNNs achieve accuracy competitive with their full-sized CNN counterparts. Our toy CCNN model trained on MNIST achieves accuracy competitive with capsule networks (8.2 million parameters) and beyond the baseline CNN used in the CapsNet paper (35.4 million parameters) with just 93,833 parameters. 

![Traditional subsampling](visualize_output/figure1.png)
![Checkered subsampling](visualize_output/figure2.png)

## Requirements
- Python 3
- Pytorch 0.4
- Numpy
- Fire ('pip install fire' or 'conda install fire -c conda-forge')
- Pillow ('pip install pillow' or 'conda install pillow')

## How to run
After you have cloned the repository, you can either visualize checkered subsampling or train networks on MNIST and CIFAR.

To visualize a 64x64 image after 3 subsampling steps using the regularly spaced lattice method:
```bash
python visualize.py --im_size 64 --steps 3 --method lattice
```
To train our tiny CCNN on MNIST (replace data_path with your own path to MNIST, will automatically be downloaded if you don't have it):
```bash
python demo_mnist.py --data_path ../data/mnist
```
To train ResNet18 as a CNN on CIFAR10 (replace data_path with your own path to CIFAR, will automatically be downloaded if you don't have it):
```bash
python demo_cifar.py --data_path ../data/cifar
```

To train ResNet18 as a CCNN on CIFAR10:
```bash
python demo_cifar.py --data_path ../data/cifar --convert
```

See each file for more information and arguments.
