# 💳 German Credit: 기본 임계값 vs. 비용 고려 임계값

## 프로젝트 개요

이 프로젝트는 이진 분류 모델의 **의사결정 임계값(Decision Threshold)** 설정이 실제 의사결정 비용에 어떤 영향을 주는지 살펴보는 실험입니다.

**South German Credit** 데이터를 이용하여 Logistic Regression 모델로 고객의 신용 위험을 다음과 같이 분류했습니다.

- `0` → Good Credit
- `1` → Bad Credit

일반적으로 사용하는 기본 임계값 `0.5`의 성능만 확인하는 것이 아니라, 서로 다른 오분류가 발생시키는 비용의 차이를 반영한 **비용 고려 임계값(Cost-Aware Threshold)**을 탐색했습니다.

핵심 질문은 다음과 같습니다.

> **기본 임계값 0.5가 실제 오분류 비용까지 최소화하는 기준일까?**

---

## Dataset

**데이터 출처:** UCI Machine Learning Repository — South German Credit

데이터는 다음과 같이 구성되어 있습니다.

- 1,000개 관측치
- 20개 독립변수
- 1개 타겟 변수: `credit_risk`

이번 실험에서는 해석을 명확하게 하기 위해 기존 타겟 라벨을 다음과 같이 재정의했습니다.

```text
0 = Good Credit
1 = Bad Credit
