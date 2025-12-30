# Pneumonia X-ray Image Classification

## 1. 프로젝트 개요
본 프로젝트는 흉부 X-ray 이미지를 활용하여  
폐렴(Pneumonia) 여부를 분류하는 이미지 분류 문제를 다뤘습니다.

CNN 기반 딥러닝 모델을 활용하여  
정상(NORMAL)과 폐렴(PNEUMONIA) 이미지를 분류하고,  
전이학습을 통해 성능 개선 가능성을 확인하는 것을 목표로 했습니다.

---

## 2. 데이터셋 설명
- 데이터 출처: Kaggle – Chest X-Ray (Pneumonia)
- 데이터 구성:
  - `train/`: 학습용 이미지
  - `val/`: 검증용 이미지
  - `test/`: 테스트용 이미지

각 이미지는 흉부 X-ray 이미지이며,
정상(NORMAL)과 폐렴(PNEUMONIA) 두 클래스로 구성되어 있습니다.

---

## 3. 데이터 전처리

### 이미지 전처리
- 이미지 크기 통일
- Tensor 변환
- 정규화(Normalization) 적용

### 데이터 로딩
- PyTorch `ImageFolder`를 사용하여 디렉터리 기반 데이터 로딩
- `DataLoader`를 통해 배치 단위 학습 구성

---

## 4. 모델 구조

### 사용 모델
- **ResNet18 (Pretrained)**
  - ImageNet으로 사전 학습된 가중치 활용
  - 마지막 Fully Connected Layer를 이진 분류에 맞게 수정

### 모델 선택 이유
- 비교적 가벼운 구조로 학습 안정성이 높음
- 전이학습 효과를 실험하기에 적합
- 의료 영상 분류에서 널리 사용되는 구조

---

## 5. 학습 과정

### 학습 설정
- Loss Function: CrossEntropyLoss  
- Optimizer: Adam  
- Learning Rate: 기본 설정 사용  
- Device: GPU 사용 가능 시 CUDA 활용  

### 학습 흐름
- Train / Validation 데이터를 분리하여 학습 진행
- Epoch별 loss 및 accuracy 추적
- 학습 과정 중 과적합 여부 관찰

---

## 6. 평가 방법

### 평가 지표
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

모델 성능은 단순 정확도뿐만 아니라  
폐렴 검출 성능을 중심으로 종합적으로 평가했습다.

---

## 7. 결과 분석
- 학습이 진행됨에 따라 손실 값이 안정적으로 감소하는 경향을 확인했습니다.
- 전이학습을 적용한 모델이 초기 학습 속도 및 성능 면에서 효과적이었습니다.
- 일부 클래스 간 오분류가 발생했으며, 데이터 불균형의 영향을 확인할 수 있었습니다.

---

## 8. 한계점
- 데이터셋 크기가 제한적이어서 일반화에 한계가 있음
- 클래스 불균형 문제에 대한 별도 보정 미적용
- 단일 모델 기반 실험으로 구조적 비교가 부족함

---

## 9. 향후 개선 방향
- Data Augmentation 기법 추가 적용
- Class imbalance 보정을 위한 가중치 조정 또는 샘플링 기법 도입
- EfficientNet, DenseNet 등 다양한 모델 비교
- Grad-CAM 기반 시각화로 모델 판단 근거 분석

---

## 10. 프로젝트 의의
본 프로젝트는 의료 영상 데이터를 활용한 이진 분류 문제를 다루며,  
딥러닝 기반 이미지 분류 파이프라인 전반을 직접 구현해본 경험이라는 점에서 의미가 있었습니다.

또한 전이학습을 활용해 제한된 데이터 환경에서도  
실질적인 성능 개선이 가능함을 확인할 수 있었습니다.
