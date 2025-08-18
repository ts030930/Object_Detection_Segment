# RetinaNet

기존의 One Stage Detector들은 빠른 Detection 시간을 보유하고 있지만, 성능적인 문제가 rcnn 계열에 비해서 컸고,
이를 Focal loss와 FPN으로 해결하였다.

그리고 Detection에는 class imbalance 이슈가 존재한다.

## Class Imbalance

Detect해야할 대상보다 background(negative)들이 훨씬 많이 영역을 차지한다.
그리고 그 많은 영역에 모두 앵커 박스가 존재하는데, 그러므로 이러한 앵커박스들이 background(negative)를 기반으로 학습을 진행하게 된다.

즉 탐지하기 여럽거나 학습해야하는 hard example가 적어서 class Imbalance 문제가 생긴다는 것이다.
왜냐하면 2 stage의 경우 region proposal을 따로 적용하기 때문에 일정한 필터가 가능하지만,
1 stage의 경우 region proposal을 동시에 진행하기 때문에 모든 앵커박스를 학습해야만 한다.


## Focal Loss

<img width="369" height="179" alt="image" src="https://github.com/user-attachments/assets/b3fea0c1-e9f3-49b0-a6f2-e65064ab4caa" />

기존의 cross entropy는 다음과 같이 정의되어있고, 이러한 Loss를 줄이는 방향으로 학습하게 된다.

<img width="1993" height="824" alt="image" src="https://github.com/user-attachments/assets/cc4ec701-9421-4cdf-9cb9-950d4e486237" />

그리고 cross entropy는 위와 같은 문제가 있다.
일종의 물량공세에는 이길 수 없다는 것이다.

이에 대한 해결법은 

1. positive와 negative 비율 맞추기
2. cross entrpy 조절하기 이다.

2.에 대한 해답이 Focal Loss이다.

<img width="256" height="86" alt="image" src="https://github.com/user-attachments/assets/76881576-1bfc-4502-a95d-29f3a4ea0d7d" />
<img width="1026" height="626" alt="image" src="https://github.com/user-attachments/assets/5c4fa45e-2fba-4798-b2f3-85b52bc07182" />


## FPN

<img width="1280" height="339" alt="image" src="https://github.com/user-attachments/assets/d3717a4e-a0d9-40c0-97ac-d2dd1c50ded8" />
<img width="754" height="882" alt="image" src="https://github.com/user-attachments/assets/23ec454a-fe44-488c-847a-3f2bc60c3187" />

기본적으로 FPN은 서로 다른 크기를 가지는 Object들을 효과적으로 Detection하기 위해서 bottom up - top down 방식으로 feature map을 처리하는 방식이다.

fpn layer에서 나온 layer는 conv 3,3을 진행한 결과를 classification, box regression을 진행한다.

















