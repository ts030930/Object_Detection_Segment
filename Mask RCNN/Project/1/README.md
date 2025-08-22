# MS COCO를 이용한 Segmentation

## MS COCO의 DATASET 구조

<img width="1615" height="744" alt="image" src="https://github.com/user-attachments/assets/addbf869-e107-4ec7-bfb2-e9742501992a" />

여러 이미지들이 존재하고 "하나의" Json Annotation 파일이 이를 설명한다.

Annotaion 딕셔너리에는 Segmentation 정보와 bbox등의 정보가 포함되어있다.

<img width="1193" height="567" alt="image" src="https://github.com/user-attachments/assets/95719225-fee3-4657-86c8-d51ab11de3a1" />

image 딕셔너리 내부에는 다음과같이 개별 이미지에 대한 정보를 지니고 있다.

<img width="1196" height="554" alt="image" src="https://github.com/user-attachments/assets/ff756861-5487-4bbf-92c8-99d3b88e1fdc" />

annotation 딕셔너리에는 개별 object에 대한 정보가 각 이미지에 대해서 나타내있다.

