# Batch Normalization 

## 기존 방식의 문제

### Gradient Vanishing / Exploding 문제
기본적으로 Banshing Gradient는 머신러닝 및 딥러닝에 있어서 중요한 문제다.
Layer를 깊게 만드는 것이 가장 간단한 성능향상 방법이지만, 역설적이게도 Layer이 깊어질수록 gradient가 사라져버리는 문제가 발생한다.
이러한 해결책으로 여러 Active Func들이 나왔지만 근본적으로 해결해주지는 못했다.

### Internal Covariance Shift
<img width="409" height="261" alt="image" src="https://github.com/user-attachments/assets/c3b026e4-63b4-4a6d-996c-131400434344" />

또 BN을 처음 소개한 논문에서는 Internal Covariance Shift를 주요한 불안정성의 원인으로 꼽았다.
Layer을 거치면서 분포가 계속 변화하여 학습에 방해를 준다는 것이다.


## Batch Normalization의 동작

<img width="405" height="328" alt="image" src="https://github.com/user-attachments/assets/ad9783cd-0668-4ddb-be70-f7fc6f7a827d" />

위 사진과 같이 4가지 단계를 거쳐서 학습한다.

이때 BN을 적용하면 bias는 팔요없는데, 그 이유는 사진의 4번 요소에 있다.
4번 식에서 감마와 베타를 학습시키는데, 이때 베타를 더하기로 학습시키기 때문에 bias의 역할을 대신 해준다는 것을 알 수 있다.
