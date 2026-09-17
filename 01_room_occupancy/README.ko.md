# 🏠 Room Occupancy Prediction: Random Split vs. Time-Aware Evaluation

## 프로젝트 개요

이 프로젝트는 **시간 의존성이 있는 센서 데이터에서 train-test split 방식이 모델 평가 결과에 어떤 영향을 주는지** 살펴보는 것을 목표로 합니다.

온도, 조도, 소리, CO₂, PIR 움직임 센서 데이터를 이용해 방 안의 재실 인원 수를 예측하는 Random Forest 분류 모델을 구축했습니다.

단순히 모델의 예측 성능만 확인하는 것이 아니라, 아래 두 가지 평가 방식을 비교했습니다.

- **Random Split**: 전체 데이터를 무작위로 train/test로 분할
- **Chronological Split**: 시간 순서를 유지한 채 과거 데이터를 train, 이후 데이터를 test로 분할

핵심 질문은 다음과 같습니다.

> 일반적인 Random Split에서 매우 높은 성능을 보이는 모델이 실제 미래 시점의 데이터에서도 동일한 성능을 유지할 수 있는가?

---

## Dataset

**데이터 출처:** [UCI Machine Learning Repository — Room Occupancy Estimation](https://archive.ics.uci.edu/dataset/864/room+occupancy+estimation)

데이터는 총 **10,129개의 관측치**로 구성되어 있으며, 여러 환경 센서에서 수집된 값들을 포함합니다.

### 주요 센서 변수

- Temperature
- Light
- Sound
- CO₂
- CO₂ slope
- PIR motion detection

### Target

`Room_Occupancy_Count`

방 안의 인원 수를 나타내며 다음 4개의 클래스로 구성된다.

- 0명
- 1명
- 2명
- 3명

전체 데이터에서 빈 방을 의미하는 `0` 클래스가 약 **81%**를 차지하고 있어 클래스 불균형이 심각했습니다.

---

## 분석 과정

### 1. 데이터 전처리

- `Date`와 `Time`을 결합하여 `datetime` 변수 생성
- 시간 순서대로 데이터 정렬
- 결측치 및 중복값 확인
- Target 클래스 분포 확인
- 센서 변수와 재실 인원 수 간의 상관관계 탐색

모델 입력 변수에서는 `datetime`, `hour`, `minute`과 같은 시간 관련 변수를 제외했습니다.

따라서 Random Split과 Chronological Split 모두 동일한 센서 변수만 사용했습니다.

### 2. Baseline Model

가장 빈도가 높은 클래스만 예측하는 `DummyClassifier`를 baseline으로 사용했습니다.

데이터의 대부분이 빈 방(`0`)이기 때문에 단순한 baseline 모델도 비교적 높은 Accuracy를 기록할 수 있었습니다.

따라서 본 프로젝트에서는 Accuracy뿐 아니라 **Macro F1 Score**를 함께 사용해 모델 성능을 평가했습니다.

### 3. Random Split

전체 데이터를 **80:20 비율의 stratified random split**으로 나누었습니다.

이후 Random Forest 분류 모델을 학습했습니다.

### 4. Chronological Split

전체 데이터를 시간 순서대로 정렬한 뒤 다음과 같이 분할했습니다.

- 앞쪽 80% → Training set
- 뒤쪽 20% → Test set

두 실험 모두 동일한 Random Forest 설정과 동일한 센서 변수를 사용해, 데이터 분할 방식의 차이에 초점을 맞췄습니다.

---

## Model

```python
RandomForestClassifier(
    n_estimators=300,
    random_state=42,
    n_jobs=-1
)
