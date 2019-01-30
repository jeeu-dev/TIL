Deep Learning 
====================

> 자료 : Coursera [강의](https://www.coursera.org/learn/machine-learning-projects/)<br>
-------
> 2019-01-29
* Structuring Machine Learning Projects <br>
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
* Structuring Machine Learning Projects <br>
>> Training and testing on different distributions
>> Bias and Variance with mismatched data distributions
- train / training-dev / dev / test로 나눔 
- train & training-dev는 같은 분포 / dev랑 test 같은 분포
- More general formulation <br>

|| General speech recognition  |  Rear view mirror speech data ||
|------
| Human level | "Human level" 4% | 6% | ↑↓ Avoiable bias |
| Error on example trained on | "Traing Eror" 7% | 6% | ↑↓ Variance |
| Error on example not trained on| "Traing-dev error" 10% |  "Dev/Test error" 6% ||
|| ↔ data mismatch |||