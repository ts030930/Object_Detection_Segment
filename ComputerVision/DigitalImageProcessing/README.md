# 빛과 EM 스펙트럼

사람이 볼 수 있는 영역은 EM 스펙트럼의 극히 일부이다.


<img width="35" height="39" alt="image" src="https://github.com/user-attachments/assets/c7776efe-3be4-430a-a4b6-163223bfd3d6" />

<img width="57" height="34" alt="image" src="https://github.com/user-attachments/assets/a9a11cac-72c2-4446-8f06-1b3a6b853d27" />

주파수(v)는 파장과 반비례 관계이고 에너지와는 정비례 관계이다.

<img width="587" height="335" alt="image" src="https://github.com/user-attachments/assets/e46d3347-d8d7-42e1-b628-86541603c262" />

**레이디언스(radiance)** : 광원으로부터 흘러나오는 총 에너지양이며 와트(W) 단위로 측정된다.
 
**루미넌스(luminance)** : 광원으로부터 관찰자가 인지하는 에너지양에 대한 척도를 제공하며 루메(lm)단위로 측정된다.

**명도(brightness)** : 실제로는 측정이 불가능한 빛 인지에 관한 주관적인 측도이다.

# 영상 형성 모델

영상을 f(x,y) 형태의 2D 함수로 표기하고, 공간좌표 (x,y)에서의 f값 또는 진폭은 물리적 의미가 영상의 광원에 의해 결정되는 스칼라양이다.
그러므로 f(x,y)는 음수가 아니고 유한해야한다.

<img width="153" height="37" alt="image" src="https://github.com/user-attachments/assets/faa013c2-c6db-4f40-a8a7-65a17ff6afaf" />

<img width="207" height="194" alt="image" src="https://github.com/user-attachments/assets/99aafa14-aa04-4f3c-88d1-1b858b4d668a" />


이때 f(x,y)는 두 성분, 1) 관찰되는 장면에 입사하는 광원 조명의 양, 2) 장면의 객체에 의해 반사되는 조명의 양에 의해 특정지어 진다.
이떄 각각을 **조명(illumination) 성분**과 **반사(reflection) 성분**이라고 하며 두 값을 곱해서 모델을 형성한다.

# 샘플링(Sampling)과 양자화(Quantization)

**샘플링(Sampling)** : 좌표값을 x,y로 디지털화 하는 것
**양자화(Quantization)** : 진폭값을 디지털화하는 것

# 디지털 영상 표현

<img width="542" height="161" alt="image" src="https://github.com/user-attachments/assets/a14a4073-af6b-4c2a-8fe2-ac9397803c57" />

**이산적인 강도 수준 (Discrete Intensity Levels)**

<img width="756" height="125" alt="image" src="https://github.com/user-attachments/assets/4a44aeb8-62c4-4551-accd-4eec37eabe44" />

K = 1 : (0,1) 흑백
K = 8 : (0,255) 그레이 스케일
k = 3 * 8 = 24 : RGB 스케일

이떄 차지하는 Storage의 크기는 
<img width="187" height="86" alt="image" src="https://github.com/user-attachments/assets/04b80eab-08ef-48b4-8bac-7b25cfa0319c" />
과 같다.

M.N 배열이 채널이 k 만큼 있다고 생각해보면 이해가 쉽다.





