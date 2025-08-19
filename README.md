# Object Detection의 주요 구성 요소

- Region Proposal

- Detecting Layer 

# Obhect Localization이란?

<img width="528" height="239" alt="image" src="https://github.com/user-attachments/assets/046a1274-5c0a-4f64-94be-243f92520379" />

한 이미지 내부에 하나의 object만 존재 할때,

image classify와 bounding box를 적용하여 해당 영역 내부에서 Detection을 수행하게 한다.


# 만약 Object가 여러개라면?

만약 feature extract를 먼저한다면 어떻게 될까?
그러면 오브젝트들의 위치는 각 이미지마다 다 다를텐데 각 이미지마다 다른 feature를 반영하지 못하게 될것이다.
그러므로 Detect하려는 Object의 위치를 먼저 정하는 게 (예상하는것)이 가장 첫번째가 되야한다.

방식 1 : Sliding Window 방식 

다양한 형태의 Window를 Sliding하며 오브젝트의 위치를 탐지한다.

이때 오브젝트가 없는 영역도 모두 살펴야하고, 슬라이딩 윈도우의 사이즈에 따라 다르게 판단되므로 초기 이후에는 사용되지 않았다.

방식 2 : Region Proposal 방식 (Selective Search)

Object가 있을만한 후보 영역을 탐색해보는 알고리즘이다.
색,무늬,크기와 같은 정보를 이용하여 알고리즘의 형태로 후보 영역을 선정해준다.
이떄 모든 부분을 bounding box로 처리한뒤 위에서 얻은 정보를 바탕으로 비슷한 부분끼리 묶어서 그룹화시켜가며 처리한다.


# IOU ( Intersection Over Union)

즉 IOU란 모델이 예측한 결과와 실제 BOx가 얼마나 겹치는 지를 나타내는 지표이다.

식으로는 iou = area of overlap / area of union이 된다.

즉 겹치는 영역의 크기를 두 영역의 합집합의 크기로 나누는 것이다.
완벽하게 겹친다면 1이 될것이다.

보통 0.4 이하면 Poor, o.7이상이면 Good이된다.


# NMS ( Non Max Suppression )

주변 바운딩 박스 후보들 중에서 가장 확실한 박스 하나만 남기고 나머지를 Suppression하는 방법이다.

이떄 제거하는 것이 아닌 눌러주는 것이다.

알고리즘의 개요는 다음과 같다. 

<img width="1012" height="465" alt="image" src="https://github.com/user-attachments/assets/c1920a80-8872-4363-afdf-3c302890dc0d" />

여기서 confidence score란 해당 box에서 오브젝트가 발견될 softmax 값이다.
즉 confidence threshold가 높을 수록, IOU threshold가 낮을 수록 많은 BOX들이 제거 된다.
왜냐하면 이때 구하는 IOU는 높은 confidenc score의 box와 비교되는 box의 iou값이기 때문에 실제 정답과 비슷한것과 상관없다.


# map 

재현율(recall)의 변화에 따른 정밀도(precision)의 값의 평균 수치로

<img width="430" height="242" alt="image" src="https://github.com/user-attachments/assets/bb692d36-9a55-4f15-806a-21ce464d0e92" />

여기서 재현율이란 실제값이 positive인 대상 중에서 예측과 실제값이 Positive로 일치한 데이터의 비율이고
정밀도란 예측을 positive로 한 대상중에서 예측과 실제값이 positive로 일치하는 데이터의 비율을 의미한다.

<img width="1905" height="922" alt="image" src="https://github.com/user-attachments/assets/c804d54f-34b0-48a6-8b85-56bfcb02a10a" />


# Segmentation

Object Detection과 Segmentation의 차이점을 설명하자면,
먼저 Segmentation의 용어에 대해서 알아봐야한다. 

Segmentation 즉, 의미가 있는 분할이라는 뜻으로 같은 클래스더라도 분할해러 Detect하겠다는것이다.

<img width="1942" height="414" alt="image" src="https://github.com/user-attachments/assets/dbf8e19d-786b-4d1c-a137-a9eb546a37bf" />

그중에서도 semantic과 instance 방식이 존재하다.


## Semantic

<img width="311" height="162" alt="image" src="https://github.com/user-attachments/assets/ca1d09df-69d6-4e82-8934-ae4a986ab16c" />
<img width="1734" height="597" alt="image" src="https://github.com/user-attachments/assets/1c3af467-2683-4a6e-8c5d-cd2b8a640068" />


다른 말로 Pixel Wise Classification으로 불리며 Pixel 단위로 각 클래스를 정의함으로써 Segmentation을 진행하는 것이다.

<img width="427" height="118" alt="image" src="https://github.com/user-attachments/assets/90efba34-eab0-4e92-b5fc-d97553cbb649" />











