# NYC Yellow Taxi – Analytical Data Modeling Project

## Overview
This project focuses on designing an analytical data model for NYC Yellow Taxi trip data.
The goal is to demonstrate strong data modeling fundamentals rather than dashboards or machine learning.

The model is designed to support analytical queries related to trip volume, revenue, time-based patterns,
payment behavior, and pickup/drop-off analysis.

---

## Dataset
Source: NYC Yellow Taxi Trip Records  
The dataset contains trip-level information including timestamps, locations, fares, payment types,
and passenger counts.

---

## Grain Definition
**Grain:** One row in the fact table represents one completed taxi trip.

All facts and dimensions are designed consistently at this level of detail.

---

## Data Model
The model follows a **star schema** with one central fact table and multiple dimension tables.

![Star Schema](diagrams/star_schema.png)

---

## Fact Table
**fact_trips**
- One row per completed trip
- Contains additive measures such as fare_amount, tip_amount, tolls_amount, and total_amount
- References dimension tables via surrogate keys

---

## Dimension Tables
- datetime_dim
- pickup_location_dim
- dropoff_location_dim
- payment_type_dim
- rate_code_dim
- passenger_count_dim

Dimensions provide descriptive context for analysis and filtering.

---

## Data Cleaning & Quality Checks
Data cleaning and validation were performed using Python in Google Colab.
Key checks include:
- Null validation on primary and foreign keys
- Non-negative fare and distance values
- Pickup time occurring before drop-off time
- Referential integrity between fact and dimension tables

Notebook: `notebooks/data_cleaning_and_quality_checks.ipynb`

---

## SQL Implementation
- Table creation: `sql/create_tables.sql`
- Data loading: `sql/load_data.sql`
- Analytical queries: `sql/analytical_queries.sql`

Example analyses include:
- Revenue by hour of day
- Average fare by passenger count
- Payment type distribution
- Pickup vs drop-off location patterns

---

## Assumptions & Limitations
Key assumptions and known limitations are documented in:
`docs/assumptions_and_limitations.md`

---

## Tools Used
- Python (Google Colab)
- SQL
- Lucidchart

---

## Future Improvements
- Implement Slowly Changing Dimensions (Type 2)
- Enrich location dimensions with zone and borough metadata
- Add partitioning strategies for large-scale data
