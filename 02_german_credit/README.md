# 💳 German Credit: Default Threshold vs. Cost-Aware Threshold

## Overview

This project explores how the **decision threshold** of a binary classification model affects real-world decision cost.

Using the **South German Credit** dataset, a Logistic Regression model was trained to classify customers as:

- `0` → Good Credit
- `1` → Bad Credit

Instead of evaluating the model only with the default classification threshold of `0.5`, this experiment searches for a **Cost-Aware Threshold** that reflects the asymmetric cost of different classification errors.

The main question is:

> **Does the default threshold of 0.5 also minimize the actual cost of misclassification?**

---

## Dataset

**Source:** UCI Machine Learning Repository — South German Credit

The dataset contains:

- 1,000 observations
- 20 predictor variables
- 1 target variable: `credit_risk`

The original target coding was reversed for this experiment so that:

```text
0 = Good Credit
1 = Bad Credit
