# data-analyst-pranaw
Portfolio Project: AWS-Based Data Analytics Platform for Vancouver Parking Tickets
________________________________________
Project Description
Project Title: Descriptive Analysis of Parking Violations in Vancouver Using AWS
 
Objective: The objective is to build a cloud-native Data Analytics Platform (DAP) using AWS services to analyze parking violation trends and derive actionable insights for the City of Vancouver. This analysis supports better policy enforcement, city planning, and public compliance.
Dataset:
•	Source: City of Vancouver Open Data Portal
•	File: Parking Tickets dataset in CSV format
•	Key Fields: Block, Street, EntryDate, Bylaw, Section, Status, InfractionText
Methodology: The project involved designing and deploying a serverless analytics pipeline on AWS to ingest, clean, catalog, analyze, govern, and monitor parking violation data. The process involved 8 key steps:


1.	Data Ingestion (S3 Raw Bucket)
What I Did: In Data Ingestion step, Parking Tickets dataset, which is in CSV format, was ingested into the AWS platform by using the Amazon S3 service. 
On AWS: I have created an Amazon S3 bucket (Raw) which is a data lake container and can store any type of data (structured, unstructured, or semi-structured). S3 buckets have no storage capacity, and therefore, they are best suited for storing large data. Within the bucket, I designed an organized folder structure to manage and store the dataset effectively. Next, I uploaded the Parking Ticket CSV file to this folder hierarchy, where it can be accessed by AWS services such as AWS Glue, Glue DataBrew, and Amazon Athena.

 
 

2.	Data Profiling and Cleaning (Glue DataBrew)
What I Did: 
I utilized the AWS Glue DataBrew service in the Data Profiling phase to execute the full profiling of the Parking Tickets data on Amazon S3 bucket.Firstly,I have created a new bucket (Cleaned) to keep profiling outputs. By using DataBrew, I defined the profiling job in DataBrew and then ran the profiling job that read and examined the full dataset.

 
 
 
3.	Data Cataloging (AWS Glue, Data Catalog)
What I Did: 
Data Catalog is defined as a collection of data schemas or metadata. In step 4, first, I have used the AWS crawler that takes the ParkingTickets csv file from the cleaned bucket and converts it to a table and puts it in the Data catalog, which is a database containing the ParkingTickets table. A data catalog in the AWS platform is created by using an AWS service called AWS Glue. Once I had the Parking Tickets table in the data catalog (Database), I proceeded with the ETL process. In the ETL process, first, I have extracted the cleaned Parking Ticket data from the database. Here, since I have only one dataset, no enrichment is needed, which involves joining multiple tables using primary keys and foreign keys to make one big table. I have then created the new bucket (curated). I have then loaded the parking ticket cleaned data to two folder locations, /user and /system, in the newly created bucket (curated). This completes the ETL process, generates a Single source of truth (SSOT) that can be queried using the Athena AWS service by issuing SQL queries.

 
      Parking Ticket Schema
  	
      Visual ETL
 


5.	Data Querying (Amazon Athena)
 
 
 
6.	Data Security (KMS, S3 Versioning, Replication)
What I Did on AWS:
Here I have used the Key Management Service on AWS, and I have created the key.Once the key is created, we are attaching this key with a bucket under the S3 service so that when uploading and downloading the file to the S3 bucket, the content of the file is encrypted at the sender's end and then it can be decrypted at the receiver's end. Also, I have attached the versioning to the S3 buckets. Also, I have implemented the replication on AWS, which involves copying the bucket to the new bucket to solve the availability issue.I have done all the above procedures for all three buckets raw bucket, cleaned bucket, and curated bucket on the AWS Data Analytics Platform created for the City of Vancouver.


       Encryption
                
6.	Data Governance (Glue Data Quality, Transform Bucket)
Data Governance is done for the purposes of ensuring data quality, accountability, and compliance for data to be stored, accessed. 
What I Did On AWS:
Here, I am implementing data governance on the data analysis platform built with AWS, such as setting a set of rules and enforcing them. I am specifically conducting a data quality check on the files that are loaded into the S3 raw bucket with AWS Glue Data Quality rules.I have created following three ruleset in AWS and created a Glue job to transform according to the rules. On execution of the job, it verifies data against the given conditions. It outputs to the transform bucket in two folders:The passed folder contains files that meet all quality standards.The failed folder contains those records that don't meet one or more of the rules. So here in the viewetl by using the AWS Glue service, I am extracting the data from the S3 raw bucket, then doing the quality checking by defining three rules, and then loading the passed and failed data under the passed and failed folders under the S3 transform bucket.
 

      Failed
 

      View ETL
 


7.	Data Monitoring (CloudWatch, CloudTrail)
To monitor, watch, and notify on your data pipeline and infrastructure's behavior.
 What I did on AWS:
Here I am monitoring the various metrics for various resources on AWS for the Data Analytics Platform that I have created, related to Vancouver parking tickets by using the AWS cloud service. Here I am creating a dashboard and adding various widgets or graphs by using the AWS CloudWatch service to measure various metrics. Here I am monitoring two resources. First, I am monitoring the storage metric called bucketsizebytes for the bucket size on the S3 raw bucket. Also, I want to see how long it takes to run a given job on the AWS Glue service. This metric is called resource usage metrics. These metrics are used for measuring the resource usage on AWS.In order to have the controlling action we need to have the threshold and alarm. Here I am creating an alarm on AWS under the AWS Cloud Watch and creating a threshold “115k Bytes” on the AWS S3 bucket on its bucket size metrics. Here, I will be notified on my UCW email once this threshold is crossed.So I have added bucket size byte metric on AWS S3 raw bucket, resource usage metrics for AWS Glue service for job run time, and also AWS S3 threshold alarm in the centre dashboard.I have also used the AWS Cloud Trail service to track user activity, such as who logged in to my account on AWS, and  see who accessed my data on the AWS Data Analytics platform in the Event History tab under AWS Cloud Trail.

    AWS Clows Watch
 

    AWS cloud Trail
 



Tools and Technologies:
•	AWS S3, Glue, Glue DataBrew, Athena, CloudWatch, CloudTrail, KMS
•	SQL, Python (for optional visualization)
Deliverables:
•	AWS-based Data Analytics Pipeline
•	Dashboard and Queries for Parking Analysis
•	AWS Monitoring, Governance, and Security Implementation
________________________________________
AWS Deployment and Service Models

Module 1 Case Study: Traditional vs Cloud Computing
Case Study: Traditional Computing Model vs Cloud Computing Model
Result & Explanation:
•	Traditional Model: The finance department uses an on-premises server in the UCW data center located in Vancouver. Data is accessed only by the internal finance team via LAN or VPN, and privacy is managed using local Active Directory.
•	Cloud Model: AWS Data Center (e.g., Virginia) hosts the transaction dataset using services like EBS/EC2 and Elastic Beanstalk. Access is controlled using IAM-based policies and roles (e.g., Finance Business User), and privacy is secured using AWS KMS and IAM roles.
•	Conclusion: The cloud model offers better scalability, centralized access, and improved data protection via encryption and IAM.

________________________________________
AWS Cost Analysis
Module 2 Case Study: TCO - Delaware North
Case Study: TCO (Total Cost of Ownership) - Delaware North
Result & Explanation:
•	Migrating to AWS reduced hardware maintenance, improved application performance, and allowed auto-scaling based on demand.
•	AWS pricing models (pay-as-you-go, reserved instances) contributed to significant cost savings.
•	Conclusion: AWS provided a lower TCO compared to traditional infrastructure, optimizing both CapEx and OpEx.
________________________________________
AWS Global Infrastructure
Module 3 Case Study: Using AWS Regions & Availability Zones
Case Study: AWS Global Reach for UCW Finance Department
Result & Explanation:
•	By migrating to AWS regions (e.g., us-east-1), the UCW Finance team benefits from high availability and disaster recovery.
•	AWS uses Availability Zones to ensure resilience, and Edge Locations to improve latency for global access.
•	Conclusion: Global infrastructure allows reliable, scalable, and low-latency access to critical datasets.

________________________________________
AWS IAM
Module 4 Case Study: Role-Based Access Control
Case Study: IAM Policy Design for Finance Team
Result & Explanation:
•	Roles and policies were defined to restrict access based on job function. For example, Finance Analysts can read-only transaction logs, while Admins have full access.
•	Multi-factor authentication (MFA) and IAM password policies were enforced.
•	Conclusion: IAM helps implement the principle of least privilege and strong access controls, ensuring secure and auditable operations.
________________________________________
AWS VPC
Module 5 Case Study: Network Isolation
Case Study: Isolating Financial Workloads
Result & Explanation:
•	A custom VPC was created with private subnets for databases and public subnets for web servers.
•	Security Groups and NACLs were configured to control traffic flow.
•	Conclusion: VPC allowed fine-grained network segmentation and control, improving security and availability.
________________________________________
AWS Lambda
Module 6 Case Study: Serverless Alerts for Violations
Case Study: Serverless Automation for Finance Alerts
Result & Explanation:
•	AWS Lambda functions were set up to trigger alerts when large financial transactions were recorded in the logs.
•	Events were triggered via CloudWatch and processed in real time.
•	Conclusion: Serverless architecture improved automation, scalability, and reduced operational overhead.
________________________________________

AWS EBS
Module 7 Case Study: Secure EC2 Storage
Case Study: Storage for Financial Transactions
Result & Explanation:
•	Financial application EC2 instances were backed by EBS volumes (gp3).
•	Snapshots were scheduled for backup and disaster recovery.
•	Volumes were encrypted using EBS encryption and monitored using CloudWatch metrics.
•	Conclusion: EBS provided durable, secure, and performant storage for critical financial applications.
________________________________________
Conclusion
This Project includes the successful deployment of the AWS-based Data Analytics Platform for the City of Vancouver demonstrates the power of cloud-native solutions in modern municipal operations. By integrating various AWS services—such as S3 for storage, Glue for data transformation, Athena for querying, and CloudWatch for monitoring—the platform efficiently handled the entire data lifecycle, from ingestion to governance. The project not only provided meaningful insights into parking violation trends using descriptive analysis but also ensured secure, scalable, and cost-effective infrastructure. The layered approach to security using KMS, IAM, and versioning, combined with robust data quality checks and monitoring, ensures high data integrity and operational resilience. This portfolio showcases practical expertise in cloud computing, real-world data analysis, and AWS architecture—all contributing toward data-driven governance and smart city initiatives.


