Deep Learning 
====================

> 자료 : Deep Learning Book [도서](http://www.deeplearningbook.org/)
-------
> 참고자료1 : [오토인코더의 모든 것 - 1/3](https://tv.naver.com/v/3185672)<br>
> 2019-02-27
### 들어가기에 앞서 [참고자료1](https://tv.naver.com/v/3185672)을 통한 사전 공부
- 오토인코더의 4 가지 키워드 <br>
Unsupervised learning, Manifold learning, Generative model learning, ML density estimation <br>
>2019-03-05

- Backpropagation에서의 Loss Function 관점 - MSE, Cross Entropy 

- Maximum Likelihood에서의 Loss Function 관점 - 같은 얘긴데 다른 방식으로 해석
  Ex) 확률분포 값이 Maximize되고 싶다 - 네트워크 출력값은 우리가 정해놓은 확률 분포(가우시안, 베르누이)를 출력(정의)하기 위한 파라미터를 조정하는 것. 

- 확률 분포에서의 관점에서는 샘플링을 할 수 있다. → 가장 큰 장점

- 우리가 미리 정한 확률분포(가우시안 확률분포는 결국 MSE와 같고, 베르누이는 Cross-entropy와 같다. )

- 결국 MSE를 쓴다는 것은, y 즉, 네트워크 출력값에 대한 확률분포가 가우시안 분포에 가까우면 MSE 쓰는게 낫다. but Cross-entropy의 경우, 네트워크의 출력값이 베르누이 분포를 따르면 Cross-entropy를 쓰는 게 낫다. 따라서 Continuous에 대한 Loss function은 MSE를 쓴다 → 이 말은 'MSE를 왜쓰는데?' 에 대한 말은 결국 네트워크의 출력값이 가우시안 분포를 따르기 때문다고 가정할 것이기 때문에 그럴거야 라는 것. 항상 그렇다는 것은 아님. 

- 확률분포를 규정짓는 파라미터를 추정하는 것. 

- Let's see Yoshua Bengio's slide → 한 문장 한 문장 해석할 것.

- #### Manifold learning

- Autoencoder의 가장 중요한 기능 중 하나는 매니폴드를 학습 한다는 것이다.

- 고차원 데이터(몇 만 차원)를 축소(2D 등) 

- 학습 데이터에 대한 차원, 그 차원 자체를 고차원 데이터. 학습데이터를 에러없이 잘 어우르는 서브스페이스가 있을 것이다. 그 서브스페이스를 매니폴드라고 한다. 그 매니폴드를 잘 프로젝션(투영) 시키면 차원 축소를 시킬 수 있을 것이다 라는 것이 아이디어. 

- → 매니폴드는 원래 훈련 데이터가 있는 공간에 있는 서브 스페이스이고 가능하는 훈련 샘플들을 잘 아우르는 어떤 공간을 매니폴드라고 한다. 

- 결국 원래 데이터를 잘 유지하면서 차원을 줄이고 싶다 는 것.

- 차원의 저주  - 같은 데이터 샘플에 대해서 차원이 늘어날 수록 공간이 늘어날수록 차원의 공간이 충분히 늘어난다.

- 목적 1) Data Compression 2) Data visualization 3) Curse of dimensionality(차원의 저주에서 벗어나기 위해) 4) Dicovering most important features(피처 찾기)

- Curse of dimensionality
  1차원에서 10까지의 공간이 있는데 데이터는 8개라고 가정, 이 때 모델링을 하면 전체 공간 중 80%를 사용하게 되는 것. 그런데 2차원, 3차원으로 늘어나면 100, 1000의 공간으로 커지게 되고 8%, 0.8%를 사용하게 됨. 즉, 데이터의 차원이 증가할수록 해당 공간의 크기(부피)가 기하급수적으로 증가하기 때문에 동일한 개수의 데이터의 밀도는 차원이 증가할수록 급속도로 희박해진다. 따라서, 차원이 증가할수록 데이터의 분포 분석 또는 모델 추정에 필요한 샘플 데이터의 개수가 기하급수적으로 증가하게 된다. 

- Manifold Hypothesis (Assumption)
  Natural data in high dimensional spaces concentrates close to lower dimensional manifolds.
  고차원의 데이터의 밀도는 낮지만, 이들의 집합을 포함하는 저차원의 매니폴드가 있다.
  Probality density decrease very rapidly when moving away from the supporting manifold.
  이 저차원의 매니폴드를 벗어나는 순간 급격히 밀도는 낮아진다.

- 매니폴드를 잘 찾았다는 것은 관계성을 잘 찾았다는 것이고, 확률분포를 잘 찾았다면 샘플링하면 기존 DB에 없는 애들이 나온다(?) 

- Resonable distance metric
  의미적으로 가깝다고 생각되는 고차원 공간에서의 두 샘플들 간의 거리는 먼 경우가 많다. 고차원 공간에서 가까운 두 샘플들은 의미적으로는 굉장히 다를 수 있다. 차원의 저주로 인해 고차원에서의 유의미한 거리 측정 방식을 찾기 어렵다. 

- 캬.. 10/20장 미쳤..

- 오토인코더가 PCA를 포함하는 방법론이다 라는게 80년대에 증명되었다.

- Neighborhood based training!

- 고차원 데이터 간의 유클리디안 거리는 유의미한 거리 개념이 아닐 가능성이 높다.

- 오토인코더는 언제 쓰는게 좋아요? 
  DNN이기 때문에 데이터가 많으면 많을수록 좋아요. 고차원 데이터일수록 좋아요. 그 경계는 뭐예요? - 나야 모르죠. 다 해봐야죠. 요새는 워낙 많은 데이터를 다루니까 오토인코더를 다루는게 아닐까 싶다.

- Autoencoders = Auto-associators = Diabolo networks = Sandglass-shaped net

- activation 없이 쓰는걸 linear autoencoder라고 한다.

- Decoder가 최소한 학습 데이터는 생성해 낼 수 있게 된다. → 생성된 데이터가 학습 데이터 좀 닮아 있다.

- Encoder가 최소한 학습 데이터는 잘 latnet vector로 표현 할 수 있게 된다. → 데이터의 추상화를 위해 많이 사용된다. 

- #### Peformance - Pretraining

- Denoising AutoEncoder - noise 추가

- Stacked Denoising Auto-Encoders(SDAE)

- #### Performance - Generation

- Stochastic Contractive AutoEncoder(SCAE)

- Contractive AutoEncoder(CAE)




### Chapter 14 Autoencoders

#### 14.1 Undercomplete Autoencoders

#### 14.2 Regularized Autoencoders

#### 14.2.1 Sparse Autoencoders

#### 14.2.2 Denoising Autoencoders

#### 14.2.3 Regularizing by Penalizing Derivatives

#### 14.3 Representational Power, Layer Size and Depth

#### 14.4. Stochastic Encoders and Decoders

#### 14.5 Denoising Autoencoders

#### 14.5.1 Estimating the Score

#### 14.5.1.1 Historical Perspective

#### 14.6 Learning Manifolds with Autoencoders

#### 14.7 Contractive Autoencoders

#### 14.8 Predictive Sparse Decomposition

#### 14.9 Applications of Autoencoders

<!--stackedit_data:
eyJoaXN0b3J5IjpbODQyOTc0MzA1XX0=
-->