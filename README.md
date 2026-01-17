# Analytical Data Modeling – NYC Yellow Taxi Trip Data (Python)

## Overview
This project focuses on **logical data modeling and dimensional dataset construction** using NYC Yellow Taxi trip data.

Instead of building dashboards or machine learning models, the emphasis is on:
- defining the analytical grain,
- separating facts from dimensions,
- designing a star-schema-style model,
- and validating the model using Python-based transformations and checks.

The project demonstrates how raw transactional data can be reshaped into analytics-ready fact and dimension datasets.

---

## Dataset
**Source:** NYC Yellow Taxi Trip Records (TLC)

The raw dataset contains trip-level transactional data including:
- pickup and drop-off timestamps
- passenger count
- trip distance
- fare components
- payment type
- pickup and drop-off locations

An official source data dictionary is provided with the dataset and was used as a reference for column meanings.

---

## Grain Definition
**Grain:**  
One row in the fact dataset represents **one completed taxi trip**.

All fact and dimension datasets are designed consistently at this level of detail.

---

## Data Model
The logical data model follows a **star schema** structure:

- One central fact dataset representing trips
- Multiple dimension datasets providing descriptive context

### Fact Dataset
**fact_trips**
- One row per completed trip
- Contains numeric, additive measures such as fare amount, tip amount, tolls amount, and total amount
- References dimension datasets via surrogate keys

### Dimension Datasets
- `datetime_dim` – pickup and drop-off timestamps with derived time attributes
- `passenger_count_dim` – passenger count categories
- `payment_type_dim` – payment method codes and descriptions
- `rate_code_dim` – rate code classifications
- `pickup_location_dim` – pickup location coordinates
- `drop_location_dim` – drop-off location coordinates

---

## Data Cleaning & Transformation
All data cleaning and transformations were performed using **Python (pandas)**.

Key steps include:
- handling missing and invalid values
- enforcing consistent data types
- removing duplicate dimension records
- generating surrogate keys for dimension datasets
- splitting the raw dataset into fact and dimension tables

The full transformation logic is available in the notebook:

notebooks/
└── data_cleaning_and_transformations.ipynb

---

## Data Quality & Validation
Since this project is Python-only, data quality validation is handled programmatically.

Checks include:
- ensuring no null values in surrogate keys
- validating non-negative monetary and distance values
- verifying pickup timestamps occur before drop-off timestamps
- confirming fact-to-dimension relationships using pandas joins
- ensuring row counts remain consistent after transformations

These checks help ensure the logical correctness of the data model.

---

## Analytical Validation
To validate that the model supports analytical use cases, Python-based aggregations were performed, such as:
- trip volume by hour and weekday
- average fare by passenger count
- revenue distribution by payment type
- pickup vs drop-off pattern summaries

These validations demonstrate that the schema supports common analytical questions.

---

## Scope Note
This project focuses on **logical data modeling and dimensional dataset construction using Python**.

Physical database implementation, SQL DDL, and SQL-based querying were intentionally excluded due to time constraints.  
The project is structured so that SQL-based implementation can be added later without changing the data model.

---

## Tools Used
- Python (pandas)
- Google Colab
- Lucidchart (schema design)

---

## Future Improvements
- Implement the model in a relational data warehouse using SQL
- Add primary and foreign key constraints at the database level
- Introduce Slowly Changing Dimensions (Type 2)
- Enrich location dimensions with zone and borough metadata

---

## Key Takeaway
This project demonstrates that **most analytical problems are modeling problems first**.  
A well-defined grain and a clean separation between facts and dimensions significantly simplify downstream analysis.
