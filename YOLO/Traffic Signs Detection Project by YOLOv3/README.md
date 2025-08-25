# Why YOLOv3?

YOLOv3 (You Only Look Once version 3) is one of the most popular real-time object detection algorithms.  
It balances **speed** and **accuracy**, making it highly suitable for applications like traffic sign detection.

---

### 🔹 Key Features of YOLOv3
1. **Multi-scale prediction**  
   - Uses 3 different scales for bounding box prediction (small, medium, large objects).  
   - Improves detection of small objects like traffic signs.  

2. **Darknet-53 backbone**  
   - A powerful CNN with 53 convolutional layers.  
   - Combines **residual connections** (like ResNet) for better gradient flow and feature extraction.  

3. **Anchor boxes**  
   - Utilizes predefined anchor boxes similar to Faster R-CNN and SSD.  
   - Improves localization of objects with varying aspect ratios.  

4. **Logistic regression for objectness**  
   - Each bounding box predicts objectness score (how likely the box contains an object).  
   - Reduces false positives.  

5. **Class prediction as independent logistic classifiers**  
   - Unlike softmax, YOLOv3 uses multiple independent logistic classifiers.  
   - Helps in detecting overlapping classes and multi-label cases.  

6. **Speed and efficiency**  
   - Capable of real-time detection (30–45 FPS on GPU).  
   - Lightweight compared to two-stage detectors like Faster R-CNN.  

---

### 🔹 YOLOv3의 주요 특징 (한국어)
1. **다중 스케일 예측**  
   - 세 가지 다른 크기의 특성 맵에서 예측 수행 (작은 물체, 중간 크기, 큰 물체).  
   - 교통 표지판 같은 작은 객체 탐지 성능 향상.  

2. **Darknet-53 백본**  
   - 53개 합성곱 계층으로 구성된 강력한 CNN 구조.  
   - ResNet처럼 **잔차 연결(Residual Connection)** 을 활용해 학습 안정성과 표현력 강화.  

3. **앵커 박스(Anchor Box) 사용**  
   - 미리 정의된 여러 비율/크기의 박스를 기반으로 예측.  
   - 다양한 비율의 물체를 더 정확히 탐지 가능.  

4. **로지스틱 회귀 기반 Objectness 점수**  
   - 각 박스마다 객체가 존재할 확률(Objectness) 예측.  
   - 잘못된 탐지(오탐)를 줄임.  

5. **독립적인 로지스틱 분류기 기반 클래스 예측**  
   - Softmax 대신 여러 독립 로지스틱 분류기를 사용.  
   - 중첩되거나 다중 클래스 상황에서도 잘 작동.  

6. **속도와 효율성**  
   - GPU 환경에서 실시간 탐지 가능 (약 30~45 FPS).  
   - Faster R-CNN 같은 2단계 검출기보다 가볍고 빠름.  

---

결론적으로, YOLOv3는 **실시간성, 정확도, 작은 객체 탐지 성능**을 동시에 갖춘 모델이기 때문에  
교통 표지판과 같은 작고 큰 여러 크기의 객체 탐지가 중요한 **Traffic Sign Detection Project**에 사용하기로 했다.



## Interpreting the output

YOLO V3에서는 추출된 **특징 맵(Feature Map)** 을 이용하여 1x1 Conv를 적용해 픽셀 하나하나마다
**Cell**단위로 Object를 탐지 할 수 있게 했는데, 
Grid size=S×S, Bounding boxes per cell=N,C = 클래스 개수 일때
각 바운딩 박스가 예측하는 값의 차원 = D=(4+1+C)이고,
<img width="600" height="819" alt="image" src="https://github.com/user-attachments/assets/e9ec8026-e223-472b-a36a-3bad4c954e02" />

최종 Output 텐서는 다음과 같아진다.


## Anchor Box

YOLOV3에는 3개의 anchor Box가 존재한다.
그러므로 각 Cell당 3개의 Box를 가지는 것이다.
또 YOLO 모델은 각 Cell마다 **책임** Box를 가지는데, 이떄 GT와 IOU가 가장 높은 BOX가 책임 Box로 선정되어서 학습이 진행된다.

<img width="655" height="419" alt="image" src="https://github.com/user-attachments/assets/578f7f1c-43cc-4ff1-98a7-a0ebf8a43d8b" />

<img width="369" height="272" alt="image" src="https://github.com/user-attachments/assets/36ba1109-9fa8-424b-908a-b002499cea94" />

---


### Objective Score & Class Confidences
<img width="600" height="819" alt="image" src="https://github.com/user-attachments/assets/e9ec8026-e223-472b-a36a-3bad4c954e02" />

-**Objective Score**
Objectness Score는 예측된 바운딩 박스 안에 **실제로 객체가 존재할 확률**을 의미한다.  
  - 객체와 겹치는 셀 → 값이 1에 가까움  
  - 객체가 없는 배경 셀 → 값이 0에 가까움  
  이 값은 확률처럼 해석되므로 **시그모이드 함수(sigmoid)** 를 거쳐 출력된다.


-**Objective Score**
Objectness Score는 예측된 바운딩 박스 안에 **실제로 객체가 존재할 확률**을 의미한다.  
  - 객체와 겹치는 셀 → 값이 1에 가까움  
  - 객체가 없는 배경 셀 → 값이 0에 가까움  
  이 값은 확률처럼 해석되므로 **시그모이드 함수(sigmoid)** 를 거쳐 출력된다.


-**Class Confidences**
Class Confidence는 탐지된 객체가 각 클래스(예: 개, 고양이, 자동차, 바나나 등)에 속할 **확률 분포**를 의미합니다.  
  - YOLOv1, v2 → Softmax를 사용해 클래스 점수를 정규화함.  
  - YOLOv3 → Softmax 대신 **Sigmoid 함수**를 사용.

이때 왜 Sigmoid를 사용하냐면, Softmax의 경우에는 전체 확률의 합이 1이라
멀티 클래스예측에 약간의 제약이 생기기 떄문에 Sigmoid를 이용하여 유연한 구조를 채택했다고 한다.

---










## Feature Extracter (Darknet -53)

YOLOv3는 **Darknet-53**이라는 새로운 Feature Extractor(백본 네트워크)를 사용합니다.  
이 네트워크는 **Darknet-19**의 효율성과 **ResNet**의 residual connection 아이디어를 결합한 구조.


###  네트워크 구조
<img width="285" height="406" alt="image" src="https://github.com/user-attachments/assets/19bcc5f5-ad65-450b-b793-06180a2a6f26" />

- 총 **53개의 Convolutional Layer**로 구성
- **3×3, 1×1 Convolution** 반복
- **Residual Block**(Shortcut Connection) 도입 → 깊은 네트워크에서도 학습 안정화
- **Downsampling (stride=2 conv)** 으로 점진적 Feature Map 축소




##  YOLOv3 Detection Layers

YOLOv3는 한 이미지에서 **3개의 Detection Layer**를 사용하여 서로 다른 크기의 물체를 탐지합니다.  
이를 위해 총 **9개의 Anchor Box**를 정의하고, 각 Detection Layer에서 **3개씩(mask로 지정)** 사용합니다.

---

###  Detection 흐름
1. **Feature Extraction (Darknet-53)**
   - 입력 이미지(예: 416×416)를 Backbone(Darknet-53)에 통과시켜  
     **3개의 Feature Map**을 얻음: 52×52, 26×26, 13×13

2. **Anchor Box 분배 (mask 사용)**
   - 총 9개 anchor 중, 각 scale에서 3개씩만 사용  
   - `mask=0,1,2` → 작은 anchor (10×13, 16×30, 33×23) → 52×52 grid (작은 물체)  
   - `mask=3,4,5` → 중간 anchor (30×61, 62×45, 59×119) → 26×26 grid (중간 물체)  
   - `mask=6,7,8` → 큰 anchor (116×90, 156×198, 373×326) → 13×13 grid (큰 물체)  

3. **Bounding Box 예측**
   - 각 grid cell이 **3개의 anchor box**를 기준으로 (x, y, w, h), objectness, class probability 예측  
   - 예측 개수:
     - 52×52×3 = 8112  
     - 26×26×3 = 2028  
     - 13×13×3 = 507  
     - **총 10647 box 후보**

4. **후처리**
   - 낮은 objectness score 제거 (Thresholding)  
   - 겹치는 박스 제거 (Non-Max Suppression, NMS)  
   - 최종적으로 실제 물체 수만큼의 Bounding Box만 남음

---


이후에는 각 파일 폴더의 README.md에 자세히 작성했다.




