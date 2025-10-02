# Bookings Data Pipeline

## 📌 Project Overview

This repository contains a sample data pipeline.  There was a limited amount of time available, so not everything was perfect, but it is meant to be a showcase of building an end to end data pipeline in a limited amount of time. The goal was to build a scalable and efficient architecture that ingests raw booking records, generates a curated customer master table and then transforms the bookings and customer data into a business insights analytics-ready dataset.

---

## 🛠️ Files in This Repository

- [📊 Bookings Data Pipeline Architecture.png](./Bookings%20Data%20Pipeline%20Architecture.png)  
  Visual representation of the end-to-end data pipeline, including data sources and ETL processing

- [📓 Bookings Data Pipeline.ipynb](./Bookings%20Data%20Pipeline.ipynb)  
  Jupyter notebook containing the full implementation of the pipeline.

---

## 📈 Summary of Approach
- **Modular**:  The Pipeline is broken into 3 independent modules that can be run independently or in sequence.
- **Coded for readability and resuse**:  Create functions for reuse, organization, and readability of code.
- **Automatic Schema Evolution**:  Raw Data Pipeline is enabled for automatic schema evolution.
- **Validate and Cleanse data**:  Highlight places to validate or cleanse data throughout the process.
  
- **File Ingestion**: File processing allows for processing of multiple files, performs validation of files, adds admin columns, and consolidates data to remove duplicates across files before merging data into bronze table.
                      Invalid files are moved to a separate folder for review.   Good files are processed, merged into the raw data table, and then archived.
                      Allows for processing of incremental files or full files.
- **Customer Aggregate**: Customer Aggregation aggregates data at the email level, and enhances data by adding additional data points.   Configuration allows for incremental or full calculation.
                      Validation steps can be added to this flow as well.
- **Business Insights**:  Leverages Bookings Bronze Raw Data and Customer Aggregate to build a Business Insights table to support OLAP processing.   
- **Future Enhancements**: Add a Data Observability Framework to run periodic validations across all data sources and alert team if any issues.
                           Build a Bronze -> Silver -> Gold (FCT and DIMs) style pipeline to further improve data quality even further if needed.

---

## ⚙️ Assumptions

- Unique customers are defined by their email address (based on data profiling).
- Booking number is a reliable key for the booking.
- Based on Data Profiling - assumed state data was accurate and email addresses did not have any duplicates based on case.
- Based on Data Profiling - dates were properly formatted and always populated.
- Created one table for Business Insights for performance instead of a dimensional / fct model.

---

## 🚧 Challenges Encountered

- Installing spark and java locally with right versions to support delta tables took time.
- Automatic schema evolution .
- Lazy Evaluations when loading a df from file need to run archive of file after df is no longer referenced, or load df into memory.
