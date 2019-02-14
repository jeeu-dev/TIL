Deep Learning 
====================

> 자료 : Coursera [강의](https://www.coursera.org/learn/convolutional-neural-networks/)<br>
-------
> 2019-02-11
> Convolutional Neural Networks
- Computer Vision <br>
→ 이미지가 크면 w가 너무 많고 무거워진다. <br>

-------
> 2019-02-12
- Edge Detection Example <br>
→ 별표는 곱하기가 아니라 컨볼루션이다. <br>
→ Vertical edge detection <br>
→ 커널을 통해 컨볼루션을 해준 결과 가운데 영역을 detection 할 수 있다. <br>

- More Edge Detection <br>
→ Vertical edge detection examples <br>
→ Vertical and Horizontal edge Detection <br>
→ Learning to detect edges (sober filter, schorr filteer) <br>
→ filter를 배울 필요없다 → backprop이 어차피 학습해준다. <br>

- Padding
→ Valid and Same convolutions <br>
: "Valid" - no padding → nxn fxf = (n-f+1) x (n-f+1) <br>
: "Same" - Pad so that output size is the same as the input size. <br> 
→ 필터는 왠만하면(대부분) 홀수이다. 짝수일 경우 불규칙적이기 때문 p = (f-1)/2
→ 관행적으로 홀수(컴퓨터 비전 관행)를 사용한다. 홀수 사용을 추천.


-------
> 2019-02-14

- Strided Convolutions <br>
→ ((n+2p-f)/s + 1) x ((n+2p-f)/s + 1) <br>
→ Summary of convolutions <br>
→ : nxn image, fxf filter, padding p, stride s → [(n+2p-f)/s + 1] x [(n+2p-f)/s + 1] <br>
→ 정수가 되게 하는 것도 좋지만 내림해도 된다.

- Convolutions Over Volume <br>
→ 부피 있는 것 즉, 6x6x3과 같은 3D이미지(RGB)도 3D filter로 결과값을 낼 수 있다. <br>
→ 수직 필터, 수평 필터로 각각 특징을 검출할 수도 있다. (전에 했던 얘기) <br>
→ 서로 다른 필터를 쓰게 되면 결과값 또한 3D 결과값을 가질 수 있다. <br>
→ Multiple filters - Summary : n x n x n_c * f x f x n_c → (n-f+1)/4 x (n-f+1)/4 x n'c <br>
→ n은 이미지의 크기, n_c는 channles(혹은 depth라고도 한다), f는 필터의 크기, n'c는 filter의 갯수 <br>


