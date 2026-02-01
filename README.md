# 🔬 Object Detection Model Comparison: Faster R-CNN vs YOLOv5

## 1. 프로젝트 개요 (Overview)
본 프로젝트는 딥러닝 객체 탐지(Object Detection) 분야의 대표적인 두 가지 접근 방식인 **2-Stage Detector**(**Faster R-CNN**)와 **1-Stage Detector**(**YOLOv5**)의 성능과 효율성을 비교 분석하기 위한 연구입니다.

* **연구 목적:** * 정밀도 중심의 Baseline 모델(Faster R-CNN)과 속도 중심의 Target 모델(YOLOv5) 비교.
    * 최신 경량화 모델이 과거의 고성능 모델을 얼마나 대체할 수 있는지 검증.
* **비교 모델:**
    * **Baseline:** Faster R-CNN (ResNet50) - *2015 SOTA*
    * **Target:** YOLOv5s (Small version) - *2020 Real-time SOTA*

---

## 2. 모델 배경 조사 (Background Investigation)

### 2.1. Faster R-CNN (2-Stage Detector)
* **특징:** RPN(Region Proposal Network)을 통해 물체 후보 영역을 먼저 추출하고, 이후 정밀 분류를 수행하는 2단계 구조.
* **장점:** 높은 정확도와 신뢰성 (작은 객체 탐지에 강함).
* **단점:** 연산량이 많아 추론 속도가 느림.

### 2.2. YOLOv5 (1-Stage Detector)
* **특징:** 이미지 전체를 한 번의 CNN 연산으로 처리하여 위치와 클래스를 동시에 예측.
* **장점:** 압도적인 연산 속도와 효율성.
* **단점:** (과거 버전 기준) 2-Stage 대비 정확도가 떨어지는 경향이 있었음.

---

## 3. 실험 환경 및 결과 (Experiment & Results)

### 3.1. 환경 (Environment)
* **Dataset:** PASCAL VOC 2007
* **Hardware:** NVIDIA A100 GPU
* **Epochs:** Faster R-CNN (10), YOLOv5s (50)

### 3.2. 정량적 평가 (Quantitative Evaluation)

| 비교 항목 (Metric) | **Faster R-CNN** (ResNet50) | **YOLOv5s** (Small) | **결과 분석** |
| :--- | :--- | :--- | :--- |
| **mAP@0.5** (정확도) | **83.31%** | 79.30% | Faster R-CNN 약 4% 우세 |
| **mAP@0.5:0.95** (정밀도) | **52.99%** | 52.20% | **차이 0.79% (동등 수준)** |
| **Inference Time** (속도) | 10.43 ms | **1.60 ms** | **YOLO가 6.5배 빠름** 🚀 |
| **FPS** (초당 프레임) | ~95 FPS | **~625 FPS** | 압도적인 속도 차이 |

---

## 4. 고찰 및 심층 분석 (Discussion) : 왜 차이가 적은가?

본 실험에서 가장 주목할 점은 "**가장 작은 모델인 YOLOv5s가 무거운 모델인 Faster R-CNN의 성능을 거의 따라잡았다**"는 것입니다.

### 4.1. 시대적 배경과 기술의 진화 (Generational Evolution)
두 모델은 출시 시기에 상당한 차이가 있습니다.
* **Faster R-CNN (2015년):** 딥러닝 태동기의 고성능 모델.
* **YOLOv5 (2020년):** 약 5년 간의 최적화 기술이 집약된 모델.

만약 Faster R-CNN과 동시대 모델인 **YOLOv1**(2016)을 비교했다면 정확도 격차가 매우 컸을 것입니다. (당시 YOLOv1 mAP는 63.4% 수준).

### 4.2. YOLOv5가 격차를 줄인 비결
YOLOv5s는 비록 모델 크기(Parameter)는 작지만, 다음과 같은 최신 딥러닝 기법들을 적용하여 성능을 극대화했습니다.
1.  **Mosaic Augmentation:** 4장의 이미지를 합쳐 학습하여 작은 객체 탐지 능력을 보완.
2.  **Auto Anchor:** 데이터셋 분포에 맞춰 앵커 박스 크기를 자동 최적화.
3.  **Backbone 개선:** CSPNet 및 SiLU 활성화 함수를 사용하여 연산 효율성 증대.

> **결론:** 기술의 발전 덕분에, 이제는 **"경량화 모델(Small)"을 사용하더라도 과거의 "고성능 모델(SOTA)" 수준의 정확도를 확보하면서 압도적인 속도 이점**을 누릴 수 있음이 증명되었습니다.

---

## 5. 결과 시각화 (Visualization)

동일한 Test Set 이미지에 대한 두 모델의 탐지 결과를 시각적으로 비교했습니다.

| **Faster R-CNN Result** | **YOLOv5s Result** |
| :---: | :---: |
| ![Faster R-CNN](images/Faster_R-CNN.png) | ![YOLOv5s](images/YOLOv5s.png) |
| *높은 신뢰도, 정밀한 박스* | *빠른 속도, 준수한 탐지력* |

---

## 6. 결론 (Conclusion)

1.  **정확도:** 정밀 지표(mAP@0.5:0.95) 기준 차이는 **1% 미만**으로, 실사용 환경에서 큰 차이가 없습니다.
2.  **속도:** YOLOv5s가 **약 6.5배 더 빠릅니다.**
3.  **선정:** 실시간성(Real-time)이 중요한 어플리케이션이나 엣지 디바이스 환경에서는, 5년 간의 기술 진보가 반영된 **YOLOv5s를 사용하는 것이 가장 합리적인 선택**입니다.

---
*Created by GrabIT Team*
