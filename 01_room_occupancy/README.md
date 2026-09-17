# 🏠 Room Occupancy Prediction: Random Split vs. Time-Aware Evaluation

## Overview

This project examines how **train-test splitting strategy affects model evaluation** for time-dependent sensor data.

Using environmental sensor measurements such as temperature, light, sound, CO₂, and PIR motion signals, a Random Forest classifier was trained to predict the number of occupants in a room.

Rather than focusing only on predictive performance, the project compares two evaluation strategies:

- **Random Split** — observations are randomly divided into training and test sets.
- **Chronological Split** — earlier observations are used for training and later observations for testing.

The main goal is to determine whether a model that performs nearly perfectly under a conventional random split maintains the same performance when evaluated on a future time period.

---

## Dataset

**Source:** [UCI Machine Learning Repository — Room Occupancy Estimation](https://archive.ics.uci.edu/dataset/864/room+occupancy+estimation)

The dataset contains **10,129 observations** collected from multiple environmental sensors.

### Sensor Features

- Temperature
- Light
- Sound
- CO₂
- CO₂ slope
- PIR motion detection

### Target

`Room_Occupancy_Count`

The target represents four possible occupancy levels:

- 0 people
- 1 person
- 2 people
- 3 people

The target distribution is highly imbalanced, with the empty-room class accounting for approximately **81% of all observations**.

---

## Analysis Workflow

### 1. Data Preparation

- Combined `Date` and `Time` into a single `datetime` variable
- Sorted observations chronologically
- Checked missing values and duplicate records
- Examined target class distribution
- Explored correlations between sensor variables and room occupancy

Time-related variables such as `datetime`, `hour`, and `minute` were excluded from the model features.

Both evaluation strategies therefore used the same environmental sensor variables.

### 2. Baseline Model

A `DummyClassifier` predicting the most frequent class was used as a baseline.

Because the dataset is highly imbalanced, the baseline model achieved relatively high accuracy despite having little predictive value.

This demonstrates why **accuracy alone is not sufficient** for evaluating this dataset.

### 3. Random Split

The dataset was divided into training and test sets using an **80:20 stratified random split**.

A Random Forest classifier was then trained on the training set.

### 4. Chronological Split

The observations were first sorted by time and then divided into:

- First 80% → Training set
- Last 20% → Test set

The same Random Forest configuration and the same sensor features were used so that the main difference between the two experiments was the splitting strategy.

---

## Model

```python
RandomForestClassifier(
    n_estimators=300,
    random_state=42,
    n_jobs=-1
)
