# RCNN

## selective search로 찾는 경우의 문제점

selective search로 찾은 2000개의 후보 공간들을 뽑는 것까지는 문제가 없지만
이 공간들의 크기가 다르다면 CNN에 넣을때 Dense Layer에서 오류가 생기게 된다.
그러므로 search로 찾은 공간들을 일정한 크기로 wraped 처리해야 한다.

## 구조

<img width="842" height="858" alt="image" src="https://github.com/user-attachments/assets/1f939965-486a-4a22-940f-d424e4342303" />

특이하게 마지막에 softmax로 처리하는 것이 아닌 svm classifier를 따로 추가하여 주었다.

<img width="1037" height="778" alt="image" src="https://github.com/user-attachments/assets/797e8773-f498-4437-843b-4b94bbecd72b" />

## bounding box regression

<img width="467" height="403" alt="image" src="https://github.com/user-attachments/assets/3e96812d-e4d5-4c39-9fd6-bb5dcb0d4ea7" />
<img width="200" height="121" alt="image" src="https://github.com/user-attachments/assets/74a207f9-8c89-49a5-bfdb-09b23b2118ed" />
<img width="311" height="58" alt="image" src="https://github.com/user-attachments/assets/2cbd2395-b194-4c95-9a80-eee65289424f" />


# SPPNET

## SPP layer

<img width="614" height="108" alt="image" src="https://github.com/user-attachments/assets/f28e243c-6e52-4f31-8759-ce166a30f8d5" />


기존 rcnn에서는 뽑은 region들을 같은 사이즈를 가지게 조절했어야했다.
이로 인해 Detection 시간이 크게 증가하여서 이를 보완하기 위해
spp layer라는 개념을 도입하여 고정크기로 바꿔주는 layer를 만들어주는 것이다.

이떄 SPM(Spatial Pyramid Matching)이라는 기술을 이용한다.

## SPM
<img width="1484" height="731" alt="image" src="https://github.com/user-attachments/assets/6467ae69-9a82-4cb8-ab0f-ceaa2d9be25a" />

위치를 기반으로 feature들을 매핑시키는 기법이다.

위와 같은 방식으로 매핑한다면 이미지의 크기와는 상관없이 같은 수의 분할수로 나눠지기 때문에 같은 크기의 vector로 표현가능해진다.

<img width="633" height="529" alt="image" src="https://github.com/user-attachments/assets/4e14dabf-bcd1-4b83-9444-0d4474783edf" />

결론적으로 위완같은 형태의 구조가 만들어진다.



