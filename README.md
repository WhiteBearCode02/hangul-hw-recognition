# ✍️ 한글 손글씨 인식 및 전이학습 성능 비교 프로젝트 
> **Korean Handwritten Character Recognition & Transfer Learning Analysis**

<br>

## 📝 Abstract (프로젝트 요약)
This project aims to build an efficient deep learning pipeline for recognizing Korean handwritten characters (5 target syllables). To resolve the heavy I/O bottleneck often encountered in cloud environments with massive datasets (over 990,000 raw images), a local SSD extraction and **O(1) Hash Map-based preprocessing algorithm** was engineered. Furthermore, the project demonstrates a comparative analysis between a scratch-built `SimpleCNN` and a pre-trained `ResNet18` (Transfer Learning), highlighting a significant performance leap from **68.15% to 98.52%** in validation accuracy.

본 프로젝트는 방대한 한글 필기체 이미지 데이터(약 99만 장)의 클라우드 병목 현상을 해결하기 위한 **초고속 데이터 전처리 파이프라인 구축**과, 합성곱 신경망(CNN) 기반의 손글씨 인식 모델 성능 비교를 목적으로 합니다. 베이스라인 모델(SimpleCNN)과 사전 학습된 전이학습 모델(ResNet18)의 결과를 정량적/시각적으로 비교 분석합니다.

<br>

## 🚀 핵심 엔지니어링 성과 (Key Features)
- **Data Lake to Local I/O 최적화:** 클라우드 스토리지(Google Drive)의 네트워크 지연을 방지하기 위해 로컬 NVMe SSD 환경으로 대용량 `.zip` 파일을 일원화하여 압축 해제 및 연산 속도 극대화
- **Hash Map 기반 O(1) 초고속 필터링:** 복잡한 계층 구조를 가진 원천 데이터에서 타겟 라벨과 이미지를 매칭할 때, 선형 탐색(O(N)) 대신 파일명 기반의 해시 맵(Hash Map) 알고리즘을 도입하여 전처리 시간 단축
- **Transfer Learning (전이학습) 검증:** 밑바닥부터 학습하는 얕은 신경망(SimpleCNN) 구조의 시각적 특징 추출 한계를 분석하고, ImageNet으로 사전 학습된 `ResNet18`을 도입하여 인식 정확도를 비약적으로 향상

<br>

## 🛠️ 기술 스택 (Tech Stack)
- **Framework:** `PyTorch`, `Torchvision`
- **Data Preprocessing:** `os`, `json`, `shutil`, `zipfile`
- **Visualization:** `Matplotlib`, `Seaborn`, `Scikit-learn (Confusion Matrix)`
- **Environment:** `Google Colab (GPU/CPU)`

<br>

## 📊 실험 결과 (Results)
| 모델 (Model) | 학습 기법 | 최종 Train Loss | 검증 정확도 (Val Accuracy) |
| :--- | :--- | :--- | :--- |
| **SimpleCNN** | Baseline (Scratch) | 0.0405 | **68.15%** |
| **ResNet18** | Transfer Learning | 0.0036 | **98.52%** |

*(※ 모델별 오분류 패턴은 하단의 Confusion Matrix 시각화 자료를 참고하세요.)*

<br>

## 📂 파일 구조 및 실행 방법 (How to Run)
1. `Step1_Data_Load.py` : 구글 드라이브의 원천 데이터를 Colab 로컬 환경으로 고속 복사
2. `Step2_Preprocessing.py` : Hash Map 알고리즘을 이용한 특정 음절('가~마') 고속 추출 및 정제
3. `Step3_Model_Training.py` : PyTorch DataLoader 구성 및 8:2 데이터 분할을 통한 학습 파이프라인
4. `Step4_Evaluation.py` : 검증 데이터를 활용한 Confusion Matrix 생성 및 결과 시각화

> **Note:** 실행 전 AI-Hub의 '한글 필기체 데이터셋' 원천/라벨 `.zip` 파일이 경로에 존재하는지 확인해 주십시오.
