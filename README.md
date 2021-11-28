# GAN---Generative-Adversarial-Network-
Implementation of GAN - Generative Adversarial Network

Framework: Pytorch and Pytorch Lightning

Full report at: [Notion site](https://github.com/Huy1711/GAN)

**Task list**

- [x] Implementation of GAN with Pytorch and Pytorch Lightning.
- [x] Improved GAN with One-sided label smoothing, batchnorm1d.
- [x] Implementation of DCGAN with Pytorch and Pytorch Lightning.
- [x] Implementation of CGAN with Pytorch Lightning.
- [x] Interpolation between 2 samples
- [ ] Parzen window implementation

## Dataset

[MNIST](http://yann.lecun.com/exdb/mnist/) and [Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist)

## GAN (Generative Adversarial Network)

Implementation of [GAN Original Paper](https://arxiv.org/abs/1406.2661)

### Models

![GAN architecture drawio (3)](https://user-images.githubusercontent.com/41891935/143758681-275e152c-623e-4b82-a939-0d41f057de19.png)

Dropout and BatchNorm1D are used in this implementation

### Training

Loss function: Binary Cross Entropy

Optimizers: 2 Adam optimizers for Discriminator and Generator

Training loss of Discriminator and Generator

![GAN training loss](https://user-images.githubusercontent.com/41891935/143762866-7b935364-9255-457d-9fc6-3ce0e59710a7.png)

Sample from training

![GAN training samples](https://user-images.githubusercontent.com/41891935/143762886-0fb037f8-1099-4b27-b441-aa4e1731cc08.png)

### Sample result

**MNIST**

![GAN MNIST](https://user-images.githubusercontent.com/41891935/143762945-4a5b76d0-e386-4d59-a756-c69175cdc52b.PNG)

Interpolation

![GAN interpolation](https://user-images.githubusercontent.com/41891935/143762960-82d4e5f3-ccbe-407f-882d-fe19a50ec674.PNG)

**Fashion-MNIST**

![GAN Fashion-MNIST](https://user-images.githubusercontent.com/41891935/143762967-736bfd3f-f112-4a83-88b3-da335f1c5aa0.PNG)

## DCGAN (Deep Convolution GAN)

Implementation of [DCGAN Paper](https://arxiv.org/abs/1511.06434)

### Models

![Discriminator drawio (1)](https://user-images.githubusercontent.com/41891935/143759200-6f4258ca-077c-4d5d-beb0-b5efbe5fdb7f.png)

### Training

DCGAN's training is similar to GAN

Training loss of Discriminator and Generator

![image](https://user-images.githubusercontent.com/41891935/143763045-6b223b0e-9cfe-4c12-97ae-644325b1b44f.png)

### Sample Result

**MNIST**

![DCGAN MNIST](https://user-images.githubusercontent.com/41891935/143763060-7d0bb4b2-5fd4-461e-80f0-79ee407778b9.png)

Interpolation

![DCGAN interpolation](https://user-images.githubusercontent.com/41891935/143763068-819d96b4-c861-499c-80d5-f8fbb22e5ef3.PNG)

## CGAN (Conditional GAN)

Implementation of [CGAN Paper](https://arxiv.org/abs/1411.1784)

### Models

![CGAN models](https://user-images.githubusercontent.com/41891935/143769442-5ff5ffc1-661b-42d1-afbc-f0e855a11c04.png)

**Idea**

GAN can be extended to a conditional model if both the generator and discriminator are conditioned on some extra information **y**. **y** could be any kind of auxiliary information, such as class labels or data from other modalities (Here i am using **y** as class labels). We can perform the conditioning by feeding y into the both the discriminator and generator as additional input layer.

### Training

Training loss of Discriminator and Generator

![image](https://user-images.githubusercontent.com/41891935/143763100-b4273ea8-cfc3-4eab-a45a-4fdafc3e989e.png)

### Sample Result

**MNIST**

Samples with label '1'

![CGAN MNIST_1](https://user-images.githubusercontent.com/41891935/143763111-bbc4d55b-b7f4-47c7-9ca8-76aa61a5be5b.png)

Samples with label '5'

![CGAN MNIST_5](https://user-images.githubusercontent.com/41891935/143763118-7014b030-bdf7-45ec-bd74-2f650ac5a526.png)

Interpolation

![CGAN interpolation](https://user-images.githubusercontent.com/41891935/143763121-db75a602-b9e1-42d7-a92b-992145a580eb.PNG)

