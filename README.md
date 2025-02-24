# Airline Data Ingestion Project ✈️
### Automated Data Pipeline using AWS Glue, Redshift & Step Functions
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
1. A file named 'airport_codes.csv' will already made available in S3 and associated dimension table also made available in AWS Redshift.
2. Whenever client uploads the raw flight data on daily basis with information like airport state, originid, destinationid, arrival delay, departure delay, etc. to a S3 bucket, a put object event will get triggered to EventBridge Rule.
3. EventBridge Rule in turn triggers a step function to orchestrate some workflow.
4. AWS Step Function now will start the crawler to crawl the data which just arrived to the S3 bucket and the dimension table in Redshift, preapre metadata and store it in the catalog database.
5. Once the crawler completes it crawling, Step Function will now trigger the Glue job to process daily flight data with dimension table already available in Redshift.
6. Once the processing completed, Glue will write the result in Redshift for further analysis.
7. Now again crawler will crwal the processed table in the Redshift to make th metadata available in a centralized database.
8. Step Function will also keeps track of each task and will send Glue status to a SNS topic to notify the user.
