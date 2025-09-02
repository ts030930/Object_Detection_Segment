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

<img width="788" height="501" alt="image" src="https://github.com/user-attachments/assets/9877c49c-3dde-4040-89ad-9c3dc315a258" />


### Train 시

<img width="405" height="328" alt="image" src="https://github.com/user-attachments/assets/ad9783cd-0668-4ddb-be70-f7fc6f7a827d" />

위 사진과 같이 4가지 단계를 거쳐서 학습한다.

이때 BN을 적용하면 bias는 팔요없는데, 그 이유는 사진의 4번 요소에 있다.
4번 식에서 감마와 베타를 학습시키는데, 이때 베타를 더하기로 학습시키기 때문에 bias의 역할을 대신 해준다는 것을 알 수 있다.
또한 non-linearity를 부여해준다.

### Test 시

<img width="610" height="498" alt="image" src="https://github.com/user-attachments/assets/282af9fc-e9a7-49b4-a1a7-276a0b55250e" />

식을 살펴보면 각 배치 단위의 평균과 분산을 이용해서 전체 값을 구하는 것을 알 수 있는데,
그러므로 학습시 각 배치의 평균과 분산을 저장해둬야한다.

그리고 Test 시에는 두가지 방식이 존재하는데,

1. 모집단 추정 방식
<img width="349" height="139" alt="image" src="https://github.com/user-attachments/assets/53195c59-7c53-4392-a707-31dc7c055dbd" />

2. 이동 평균 
<img width="302" height="124" alt="image" src="https://github.com/user-attachments/assets/fa25db2d-efbb-4d8f-8da9-d9834ce91a69" />

이 두 방식 중에서 이동 평균이 주로 사용되는데 그 이유는 모집단 추정 방식은 저장소를 매우 많이 차지 하기 떄문에
이동평균으로 구해서 어느정도 정확한 예측을 가능하게 한 것이다.
실제로 이동평균의 식은 운영체제나 네트워크에서도 사용하는 방식이다.







