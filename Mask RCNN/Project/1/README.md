# MS COCO를 이용한 Segmentation

## MS COCO의 DATASET 구조

<img width="1615" height="744" alt="image" src="https://github.com/user-attachments/assets/addbf869-e107-4ec7-bfb2-e9742501992a" />

여러 이미지들이 존재하고 "하나의" Json Annotation 파일이 이를 설명한다.

Annotaion 딕셔너리에는 Segmentation 정보와 bbox등의 정보가 포함되어있다.

## pycocotools 이용

