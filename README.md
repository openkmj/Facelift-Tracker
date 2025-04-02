# Facelift Tracker 🚗📈

Tracks and analyzes social media sentiment before and after car model facelifts.

> This repository is a personal fork of the original [Softeer5th DE Track project](https://github.com/softeer5th/DE-theallnew-team3).

## Project Overview

When a car model receives a facelift, public opinion can shift dramatically—positively or negatively.  
**FaceliftTracker** is a data pipeline project designed to monitor and analyze how people react on social media before and after these design changes.

By collecting Youtube and community data related to specific car models, we visualize sentiment trends and explore the relationship between design updates and user perception.

## Key Contributions

- Built and managed Airflow workflows, including DAGs, scheduling, and task orchestration

- Implemented fault-tolerant logic with retry mechanisms, schema validation between stages, and basic monitoring for early error detection

- Set up the development environment, including AWS configuration and deployment/test scripts

## Demo

![Image](https://github.com/user-attachments/assets/1d745d96-ddc8-42d5-bb8f-c42657f07312)

### Youtube Link

https://youtu.be/Fyyahbjk9A8

### Slides

[Slide PDF](./slides/slides.pdf)

## System Architecture

![Image](https://github.com/user-attachments/assets/4e75aec1-37c3-4e8a-8ca8-be085f0cc95d)

## System Requirements & Design Considerations

The system was designed around key characteristics observed in social media data, which influenced both the architecture and the processing strategy.

### 1. Asymmetric Data Distribution

- **What we observed**:
  - Data volume differences across platforms
  - Concentration of reactions on a small number of popular posts
- **How we designed for it**:
  - A modular, load-balanced crawling system for handling uneven and platform-specific data flows

### 2. External System Uncertainty

- **What we observed**:
  - Changes in external APIs or HTML structures
  - Rate limits, network errors, and access restrictions (e.g., bot detection)
- **How we designed for it**:
  - Fault-tolerant pipeline with retry logic, loosely connected processing stages, and monitoring for early detection and recovery

### 3. Time-Dependent Data Fields

- **What we observed**:
  - Static fields (e.g., title, author, date)
  - Dynamic fields (e.g., view_count, like_count, comments) that change over time
- **How we designed for it**:
  - Daily ingestion pipeline for capturing and storing time-sensitive fields to enable time-series analysis

## System Components

### [Airflow](./airflow/README.md)

> Pipeline orchestration using Airflow(AWS MWAA)

### [EMR](./emr/README.md)

> Spark jobs executed on Amazon EMR

### [Lambda](./lambda_functions/README.md)

> AWS Lambda Functions for I/O-intensive tasks

### [ELT Process](./airflow/dags/sql/README.md)

> SQL scripts for ELT from S3 to Redshift

### [local](./local/)

> Prototypes and test scripts for local crawling and preprocessing
