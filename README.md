# Airline Data Ingestion Project ✈️
### Automated Data Pipeline using AWS Glue, Redshift & Step Functions
![project-banner.png](https://github.com/user-attachments/assets/b83ff96c-a732-434a-85c0-ed8b6c8e29b4)
(https://raw.githubusercontent.com/Ganesh-200/Airline_Data_Ingestion_Project/main/project-banner.png)

## 📌 Overview
This project builds a scalable data ingestion pipeline for airline-related datasets using AWS services. The pipeline automatically extracts, transforms, and loads (ETL) data into Amazon Redshift, enabling efficient querying and analysis. This data pipeline is mainly designed to respond quickly for a customer queries about their flight booking information by a customer care executive effectively with the valuable insights like arrival delay time, daparture delay time, etc.

## 🚀 Key Features
✅ **AWS Glue** – ETL processing and data transformation  
✅ **Amazon Redshift** – Centralized data warehousing  
✅ **Amazon S3** – Storage for raw and processed data  
✅ **AWS Glue Crawlers** – Schema inference and metadata cataloging  
✅ **AWS Step Functions** – Workflow automation for end-to-end orchestration  
✅ **Amazon SNS** – Notifications for pipeline execution updates 

## 🛠️ Tech Stack
🔹 **AWS Services:** Glue, Redshift, S3, Step Functions, Crawlers, SNS  
🔹 **ETL Framework:** AWS Glue Jobs (PySpark, Python)  
🔹 **Orchestration:** AWS Step Functions  
🔹 **Data Storage:** Amazon S3 (Raw & Processed Data), Redshift  
🔹 **Monitoring & Alerts:** Amazon SNS  

## Workflow
![Airline_Data_Ingestion_Project_workflow](https://github.com/user-attachments/assets/520887a7-124e-44fc-9afc-47278f48e5c7)
1. A file named airport_codes.csv is already available in Amazon S3, and the associated dimension table is also present in Amazon Redshift.
2. Whenever the client uploads raw flight data on daily basis—including details like airport state, origin ID, destination ID, arrival delay, and departure delay—to an S3 bucket, an S3 PutObject event triggers an Amazon EventBridge rule.
3. The EventBridge rule then triggers an AWS Step Function, which orchestrates the workflow.
4. The Step Function starts an AWS Glue Crawler to scan the newly arrived data in S3 and the dimension table in Redshift, prepares metadata, and stores it in the AWS Glue Data Catalog.
5. Once the crawler completes its execution, the Step Function triggers an AWS Glue Job to process the daily flight data using the existing dimension table in Redshift.
6. After the processing is complete, AWS Glue writes the results back to Redshift for further analysis.
7. The crawler then scans the processed table in Redshift to update the metadata in the centralized catalog database.
8. The Step Function tracks each task and sends the Glue job status to an Amazon SNS topic, notifying the user.
