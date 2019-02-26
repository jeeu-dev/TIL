Deep Learning 
====================

> 자료 : Coursera [강의](https://www.coursera.org/learn/convolutional-neural-networks/)<br>
-------
> 2019-02-11
## Convolutional Neural Networks

### 1 Week

#### Computer Vision
→ 이미지가 크면 w가 너무 많고 무거워진다. <br>

-------
> 2019-02-12
#### Edge Detection Example
→ 별표는 곱하기가 아니라 컨볼루션이다. <br>
→ Vertical edge detection <br>
→ 커널을 통해 컨볼루션을 해준 결과 가운데 영역을 detection 할 수 있다. <br>

#### More Edge Detection
→ Vertical edge detection examples <br>
→ Vertical and Horizontal edge Detection <br>
→ Learning to detect edges (sober filter, schorr filteer) <br>
→ filter를 배울 필요없다 → backprop이 어차피 학습해준다. <br>

#### Padding
→ Valid and Same convolutions <br>
: "Valid" - no padding → nxn fxf = (n-f+1) x (n-f+1) <br>
: "Same" - Pad so that output size is the same as the input size. <br> 
→ 필터는 왠만하면(대부분) 홀수이다. 짝수일 경우 불규칙적이기 때문 p = (f-1)/2
→ 관행적으로 홀수(컴퓨터 비전 관행)를 사용한다. 홀수 사용을 추천.


-------
> 2019-02-14

#### Strided Convolutions
→ ((n+2p-f)/s + 1) x ((n+2p-f)/s + 1) <br>
→ Summary of convolutions <br>
→ : nxn image, fxf filter, padding p, stride s → [(n+2p-f)/s + 1] x [(n+2p-f)/s + 1] <br>
→ 정수가 되게 하는 것도 좋지만 내림해도 된다.

#### Convolutions Over Volume
→ 부피 있는 것 즉, 6x6x3과 같은 3D이미지(RGB)도 3D filter로 결과값을 낼 수 있다. <br>
→ 수직 필터, 수평 필터로 각각 특징을 검출할 수도 있다. (전에 했던 얘기) <br>
→ 서로 다른 필터를 쓰게 되면 결과값 또한 3D 결과값을 가질 수 있다. <br>
→ Multiple filters - Summary : n x n x n_c * f x f x n_c → (n-f+1)/4 x (n-f+1)/4 x n'c <br>
→ n은 이미지의 크기, n_c는 channles(혹은 depth라고도 한다), f는 필터의 크기, n'c는 filter의 갯수 <br>

-------
> 2019-02-24

#### One Layer of a Convolutional Network
- 컨볼루션 연산에서는 필터가 w와 같은 역할을 하게 된다. <br>
- Number of parameters in one layer <br>
: If you have 10 filters that are 3x3x3 in one layer of a neural network, how many parameters does that layer have? <br>
→ 각각의 필터가 3x3x3의 볼륨이므로 27개의 파라미터로 채워질 것이다. 거기에 바이어스가 있으므로 28개. 필터가 10개 이므로 28 x 10 이므로 280개. <br>
- Summary of notation <br>
: If layer l is a convolution layer <br>
f^[l] = fiilter size <br>
p^[l] = padding <br>
s^[l] = stride <br>
Input : n x n x n_c(number of channel : c)<br>
→ n_H^[l-1] x n_W^[l-1] x n_c^[l-1] <br>
Output : n_H^[l] x n_W^[l] x n_c^[l]  <br>
n_H^[l] = [(n_H^[l-1]+2p^[l]-f^[l]/s^[l]) + 1] <br>
n_c^[l] = number of filters <br>
Each filter is : f^[l] x f^[l] x n_c^[l-1]<br>
Activations : a^[l] → n_H^[l] x n_w^[l] x n_c^[l] <br>
Weights : f^[l] x f^[l] x n_c^[l-1] x n_c^[l] <br>
bias : n_c^[l] <br>

#### Simple Convolutional Network Example
- Types of layer in a convolutional network <br>
→ Convolution (CONV) <br>
→ Pooling (POOL) <br>
→ Fully connected (FC) <br>

#### Pooling Layers
- Pooling layer : Max Pooling <br>
: 이게 왜 잘 작동하는지 정확히 아는 사람은 없다. <br>
- Pooling layer : Average Pooling <br>
- 풀링할 때 패딩은 쓰지 않는다. <br>

#### CNN Example
- Neural network example : LeNet-5 <br>

#### Why convolutions
- Parameter sharing : A feature detector(such as a vertical edge detector) that's useful in one part of the image is probably useful in another part of the image. <br>
: 수직 엣지 감지기 같은 feature 감지기가 이미지의 한 부분에서 유용하다면 이미지의 다른 부분에서도 유용할 것이라는 견해에 따라 사용된다. 즉, 수직 모서리를 감지하기 위해 3x3 필터를 사용했다면, 다른 곳에도 이 필터를 계속해서 사용해나간다는걸 말한다. 말그대로 한 필터를 다른 곳에도 지속적으로 적용해나가며 학습해나간다는 것.<br>

- Sparsity of connections : In each layer, each output value depends only on a small number of inputs. <br>
: 한 부분의 아웃풋의 결과가 입력값의 일정 부분에만 영향을 받는다. (당연한 말..)<br>

#### Quiz - The basics of ConvNets

-------
> 2019-02-25

### 2 Week

#### Why look at case studies?
- Outline - Classic network: <br>
-- LeNet-5 <br>
-- AlexNet <br>
-- VGG <br>
-- ResNet(Conv Residual Network) <br>
-- Inception <br>

#### Classic Networks
- LeNet-5 <br>
32x32x1 → 28x28x6 → 14x14x6 → 10x10x16 → 5x5x16 → 120 → 84 → y^ softmax 10 <br>
[LeCun et al., 1998. Gradient-based learning applied to document recognition] <br>
- AlexNet <br>
227x227x3 → 55x55x96 → 27x27x96 → 27x27x256 → 13x13x256 → 13x13x384 → 13x13x256 → 6x6x256 → 9216 → 4096 → Softmax 1000 <br>
[Krizhevsky et al., 2012. ImageNet classification with deep convolutional neural networks] <br>
- VGG-16
224x224x3 → 224x224x64 → 112x112x64 → 112x112x128 → 56x56x128 → 56x56x256 → 28x28x256 → 28x28x512 → 14x14x512 → 14x14x512 → 7x7x512 → 4096 → 4096 → Softmax 1000 <br> 
[Simonyan & Zisserman 2015. Very deep convolutional networks for large-scale image recognition] <br>

#### ResNets
- Residual block <br>
: 중간 과정을 skip하고(short cut/skip connection) 활성화 함수를 통해 계산할 때 더해준다. <br>
→ 잔류 블록 → 신경망에 더 깊이 들어갈 수 있게 해주고, 사라지거나 폭발적으로 증가하는 gradient 문제들을 처리하도록 도와주며, 눈에 띄는 손실 없이 신경망을 훨씬 깊게 훈련하도록 도와준다. <br> 
[He et al., 2015. Deep residual networks for image recognition] <br>

#### Why ResNets Work

#### Networks in Networks and 1x1 Convolutions
- Why does a 1x1 convolution do? <br>
: Network in Network <br>

#### Inception Network Motivation

#### Inception Network
- Inception module <br>

#### Using Open-Source Implementation

#### Transfer Learning
- 이미 훈련된 네트워크가 많다. 다운받으면 됨. <br>

#### Data Augmentation
- Mirroring <br>
- Random Croppping <br>
- Color shifting <br>
- Implementing distortions during training <br>

#### State of Computer Vision
Tips for doing well on benchmarks/winning competitions <br>
- Ensembling <br>
: Train several networks independently and average their outputs <br>
- Multi-crop at test time <br>
: Run classifier on multiple versions of test images and average results <br>
Use open source code
- Use architectures of networks published in the literature <br>
- Use open source implementations if possible <br>
- Use pretrained models and fine-tune on your dataset <br>



### 3 Week

#### Object Localization

#### Landmark Detection
- 레이블들은 다른 이미지를 통틀어 일관적이어야 한다. <br>

#### Object Detection
- 스트라이드를 아주 작게 하지 않는 이상 이미지 내에서 객체를 잡는건 불가능하다. - 계산 문제 <br>

#### Convolutional Implementation of Sliding Windows









