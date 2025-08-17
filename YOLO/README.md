# YOLO

## YOLO V1

<img width="627" height="401" alt="image" src="https://github.com/user-attachments/assets/b4847e05-f8ed-403a-bdcc-e1ce27ffe3b2" />


2 Stage Detector들은 일단 그 곳에 오브젝트가 있을까?에 대한 예측을 진행 후 그에 기반해서 detect를 진행했지만,

YOLO V1은 입력 이미지를 S x S grid로 나눈뒤 각 grid의 Cell이 하나의 object에 대해 detection을 진행하는 방식으로 설계되었다.
그리고 각 Cell은 2개의 Bounding Box후보를 기반으로 예측한다.

예를들어, S= 7인 grid에는 box가 98개 존재하는것이다.

<img width="1018" height="338" alt="image" src="https://github.com/user-attachments/assets/73cf1db6-2f13-4260-96f2-1729ad5fd1c2" />

위 사진을 보면 7x7x30인데 7은 S이고
각 Cell별로 Bounding Box의 정규화된 x,y,w,h와 confidenc score( Object일 확률 * IOU ) 해서 2개의 Box가 있으니
10개를 차지하고 Pascal VOC 기준 class가 20개가 존재하므로 두개를 더해서 30개의 요소를 가지는 것을 알 수 있다.

그러면 궁금증이 여기서 Box가 두개면 20개의 요소도 각 Box마다 가져야된다고 생각되지만, 
내부 설계에서 두개의 Box 중에서 Ground Truth와 Box가 더 많이 겹치는 Box에 해당하는 요소들로 나타내게 설계되었다.
