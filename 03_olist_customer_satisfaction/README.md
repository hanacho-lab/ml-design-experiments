# 🛒 Olist Customer Satisfaction: Delivery Time vs. Delivery Expectation

## Overview

This project explores how **different representations of the same delivery experience** affect a machine learning model's ability to identify dissatisfied customers.

Using the Brazilian E-Commerce Public Dataset by Olist, customer dissatisfaction was modeled from two different perspectives:

- **Delivery Time** → How long the order actually took to arrive
- **Delivery Expectation Gap** → How early or late the order arrived compared with the estimated delivery date

The main question is:

> **Is customer dissatisfaction more strongly associated with absolute delivery time, or with whether the delivery met the customer's expected delivery date?**

Rather than changing the model itself, this experiment keeps the modeling conditions fixed and changes only the way delivery performance is represented.

---

## Dataset

**Source:** Brazilian E-Commerce Public Dataset by Olist

The dataset contains anonymized real-world e-commerce transactions from Brazil, including information on orders, delivery, payments, products, customers, and reviews.

For this experiment, two files were used:

```text
olist_orders_dataset.csv
olist_order_reviews_dataset.csv
