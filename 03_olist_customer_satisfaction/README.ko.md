# 🛒 Olist Customer Satisfaction: 실제 배송 소요일 vs. 예상 배송일 대비 차이

## 프로젝트 개요

이 프로젝트는 **동일한 배송 경험을 서로 다른 방식의 변수로 표현했을 때 머신러닝 모델의 결과가 어떻게 달라지는지** 확인하는 실험입니다.

Brazilian E-Commerce Public Dataset by Olist를 이용하여 고객의 배송 경험을 두 가지 방식으로 표현했습니다.

- **실제 배송 소요일(Delivery Time)** → 주문 후 실제 배송까지 얼마나 오래 걸렸는가
- **예상 배송일 대비 차이(Delivery Expectation Gap)** → 실제 배송일이 안내된 예상 배송일보다 얼마나 빠르거나 늦었는가

이번 실험의 핵심 질문은 다음과 같습니다.

> **고객 불만족은 실제 배송에 걸린 시간 자체와 예상 배송일을 지켰는지 여부 중 어떤 정보와 더 강하게 연결될까?**

모델 자체를 변경하기보다는 동일한 모델링 조건에서 **배송 정보를 표현하는 feature만 변경하여 비교**했습니다.

---

## Dataset

**데이터 출처:** Brazilian E-Commerce Public Dataset by Olist

Olist 데이터셋은 브라질 이커머스의 실제 거래 데이터를 익명화하여 공개한 데이터로, 주문, 배송, 결제, 상품, 고객, 리뷰 등 다양한 정보를 포함하고 있습니다.

이번 실험에서는 다음 두 개의 파일을 사용했습니다.

```text
olist_orders_dataset.csv
olist_order_reviews_dataset.csv
