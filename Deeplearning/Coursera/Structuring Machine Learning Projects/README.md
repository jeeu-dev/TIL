Deep Learning 
====================

> 자료 : Coursera [강의](https://www.coursera.org/learn/machine-learning-projects/)<br>
-------
> 2019-02-11
> Convolutional Neural Networks
- Computer Vision
→ 이미지가 크면 w가 너무 많고 무거워진다.

- Edge Detection Example
→ 별표는 곱하기가 아니라 컨볼루션이다. 


-------
> 2019-02-04
> Structuring Machine Learning Projects <br>
> Transfer learning
- When transfer learning makes sense <br>
- Task A and B have the same input x. <br>
- You have a lot more data for Task A than Task B. <br>
- Low level features from A could be helpful for learning B. <br>
- 요약하자면, transfer은 특정 B라고 하는 업무를 잘하려고 할 때 가장 도움이 된다. 이런 B 업무는 보통 데이터가 많이 없는 경우. 예를 들어 좋은 방사선 판단 시스템을 만들기 위해서 x-ray 이미지를 수집하기는 어렵다(수집 자체가 어렵다). 이런 경우, 관련된 약간은 다른 업무를 찾을 수 있다. 이미지 인식과 같은 분야에서 백만개의 이미지를 가지고 와서 여러 특성들을 배울 수 있을 것이다. 그렇게 배운 이후에, B업무에서 잘하려고 할 수 있을 것이다. 방사선학 업무에서(데이터가 많이 없어도). <br>

> Multi-task learning
- Transfer learning에서는 순차적(A 업무 다음에 B업무 학습)으로 학습시켰다면 여기서는 동시에 시작한다. <br>
- When multi-task learning makes sense?
- Traing on a set of tasks that could benefit from having shared lower-level features. <br>
- Usually : Amount of data you have for each task is quite similar. <br>
- Can train a big enough neural network to do well on all the tasks. <br>
- 멀티 태스크 러닝은 1개의 신경망이 여러 업무를 처리 할 수 있도록 해준다. 이러한 특성은 따로 업무를 진행하는 것보다 더 좋은 성능을 가질 수 있도록 해준다. / Transfer learning이 multi-task learning보다 더 자주 쓰인다. <br>

> end-to-end deep learning
>> what is end-to-end deep learning?

>> Whether to use end-to-end deep learning
- Pros and cons of end-to-end deep learning <br>
-- Pros : <br>
--  Let the data speak <br>
--  Less hand-designing of components needed <br>
-- Cons: <br>
--  May need large amount of data <br>
--  Excludes potentially usefull hand-designed components <br>
- Applying end-to-end deep learning <br>
-- Key question : Do you have sufficient data to learn a function of the complexity needed to map x to y? <br>





-------
> 2019-01-29
> Structuring Machine Learning Projects <br>
>> Addressing data mismatch
- Carry out manual error analysis to try to understand difference between training and dev/test sets
- Make training data more similar; or collect more data similar to dev/test sets
- 인공데이터 통합, 자동차 소음 문제를 해결하는 맥락에서 보자.
- Artificial data synthesis <br>
- "The quick brown fox jumps over the lazy dog." + Car noise = Synthesized in-car audio <br>
- Car recognition : <br>
- 요약하면, 데이터 불일치 문제가 있다고 생각한다면, 오류 분석을 하라. <br>
아니면 training set을 보는 것을 권하며, 이 수치를 test해보려면 dev set을 해봐라. <br>
이 두 데이터 분포가 어떻게 다를 수 있는지에 대한 통찰력을 얻으려면 다른 방법을 시도하여 training set과 유사한 데이터를 수집할 방법을 찾으라. <br>
→ 우리가 논의하는 방법은 인공데이터 합성이었다. 효과가 좋음. but 조심해야함 - 가능한 모든 예제 공간의 작은 하위 집합에서만 데이터를 시뮬레이션하라.

-------
> 2019-01-28
> Structuring Machine Learning Projects <br>
>> Training and testing on different distributions
>> Bias and Variance with mismatched data distributions
- train / training-dev / dev / test로 나눔 
- train & training-dev는 같은 분포 / dev랑 test 같은 분포
- More general formulation <br>

 ＃| General speech recognition  |  Rear view mirror speech data | ＃
:---:| :---: | :---: | :---: 
Human level | "Human level" 4% | 6% | ↑↓ Avoiable bias
Error on example trained on | "Traing Eror" 7% | 6% | ↑↓ Variance
Error on example not trained on| "Traing-dev error" 10% |  "Dev/Test error" 6% | ＃
＃| ＃ | ↔ data mismatch | ＃