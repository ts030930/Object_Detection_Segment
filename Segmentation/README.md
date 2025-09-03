# FCN

FCN 이미지 분할 기법은 Conv 자체로써 semantic segmentation을 가능하게 하는 기술으로,
이 기술을 요약하면 임의의크기의 입력을 넣어서 효율적인 추론과 학습으로원하는 크기의 출력을 생성하는 
**"Fully Conv"** 를 구축하는 것이다.

이때 총 3가지 중요한 과정을 이용한다.

1. 완전한 콘볼루션화
2. 디콜볼루션
3. 스킵 아키텍쳐

## 완전한 콘볼루션화

완전한 Conv화라는 것은 기존 Layer들이 가지고 있건 FC Layer들을 모두 Conv로 바꾸는 작업으로,
**FC를 마지막에 사용시 receptive field의 개념이 사라진다.**
그리고 FC Layer의 치명적인 단점인 입력 이미지 크기의 고정문제도 있기 때문에 이를 해결하기 위해 완전한 콘볼루션화가 필요하다.

<img width="618" height="332" alt="image" src="https://github.com/user-attachments/assets/57c8750e-6159-403f-8c7e-97736d31cae5" />

위치 정보를 보존할 수 있으니 히트맵을 획득 할 수 있게 된다.

위와 같은 Conv 과정을 통해 Feature map을 추출해 나가는데 마지막 map의 channel 수는 훈련된 Class수와 동일하다.


## 디콘볼루션

<img width="946" height="402" alt="image" src="https://github.com/user-attachments/assets/320584e8-c147-4500-a2c5-98c6b0741cbe" />

위에서 얻은 Feature map은 매우 해상도가 낮춰진 상태의 Feature map을 Coarse Output map이라고한다. 
그리고 이러한 map은 **원본 크기에서 매우 축소된 상태이기 떄문에 픽셀단위의 예측을 하기에는 많이 부족하다**
그러므로 디콘볼루션을 통해 높은 해상도로 만들어주는 작업을 진행한다.

Down sampling -> Up sampling의 과정을 거치는 것이다.

## 스킵 구조
<img width="983" height="631" alt="image" src="https://github.com/user-attachments/assets/eec306e7-43cc-41df-a1fc-1aa74b82213d" />

이 Up Sampling 과정에서 그저 단순히 해상도만을 늘린다면, 여전히 Coarse한 채로 남을 것이다.
그러므로 FCN에서는 Skip Combining이라는 기법을 통해 Conv + Pooling의 결합으로 down sampling 시의 feature map을 참고해서 Up Sampling을 진행하는 것이다.
