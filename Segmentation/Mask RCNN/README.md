# Mask RCNN

<img width="1236" height="535" alt="image" src="https://github.com/user-attachments/assets/184ab55b-bc2f-48a1-a89b-8dc3bf5ee89d" />


Faster RCNN과 FCN 기법의 결합으로

ROI-Align과 Bounding bos regression과 classification에 Binary Mask Prediction을 추가했다.

## FCN 
<img width="772" height="413" alt="image" src="https://github.com/user-attachments/assets/421a9ac6-0940-44f8-9a4b-20205f7d3c3a" />

기존에 우리가 알던 Fully Connected Layer에서 dense layer들을 Conv Layer로 바꿔주는 것이다.

그리고 각 구간마다 down,upsampling을 진행한다.

<img width="1181" height="288" alt="image" src="https://github.com/user-attachments/assets/739edb93-1c11-49ac-b059-b8b15a22dba0" />

마지막으로 좀 더 정확한 segment를 위해서 각 계층의 정보를 결합하여 공간 정확도를 향상시킨다.


## ROI Allign

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/4981f3dc-ed9a-4368-83f0-eb4b0841e458" />

ROI Pooling의 문제점으로는 각 사이즈를 줄일때 픽셀이 소수점으로 떨어지게 되는데
이러한 소수점을 버리는 과정에서 정보손실이 일어나고 이러한 영향이 크다는 문제점이 있다는 것이다.

<img width="1986" height="886" alt="image" src="https://github.com/user-attachments/assets/579117a4-94d3-4486-bfa0-da247f4ba8f4" />

해결책으로 소수점을 그대로 인용하되, Bilinear Interpolation을 이용한 ROI Allign을 진행하는 것이다.
그 후 max pooling을 진행해줌으로써 문제를 해결할 수 있다.


## Feature Extractor








