# gcp-playground

## General

**Fault Tolerant**: Fault tolerance is the property that enables a system to continue operating properly in the event of the failure of (or one or more faults within) some of its components

**High Availability**: High availability (HA) is a characteristic of a system which aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period

**Scalability** is the property of a system to handle a growing amount of work by adding resources to the system (Allows to grow when needed)

In cloud computing, **Elasticity** is defined as "the degree to which a system is able to adapt to workload changes by provisioning and de-provisioning resources in an autonomic manner, such that at each point in time the available resources match the current demand as closely as possible" (Allows to shrink when needed)

**Google Cloud Platform**:
1. Compute
   1. App Engine
   2. Compute Engine
   3. Container Engine
2. Storage
   1. Bigtable
   2. Cloud Storage
   3. Cloud SQL
   4. Cloud Datastore
3. Big Data
   1. Big Query
   2. Pub/Sub
   3. Dataflow
   4. Dataproc
   5. Datalab
4. Machine Learning
   1. Vision API
   2. Machine Learning
   3. Sppech API
   4. Translate API

A **“cloud instance”** refers to a virtual server instance from a public or private cloud network. In cloud instance computing, single hardware is implemented into software and run on top of multiple computers 

**Managed Service**: Google maanges OS installation, patches, updates, storage and I MANAGE: Loagind data, Accessing data, Using Data

**Zones**: Isolated DC
**Region**: Geographic group of Zones

**IAM**
Roles/Permissions like AWS

**Organizations**:
    Folders:
        Projects:
            Resources

GCP Activity <-?-> AWS CloudTrail        

**GCP Instances**:
1. E (Everyday - general cost efficient)
2. N (general - balanced price / performance)
3. M (Memory optimized - e.g. SAP HANA, In memory analytics)
4. C (Compute optimized - HPC, Gaming, Single Threaded apps)
5. A (Accelerator optimized - Machine Learning)



**Databases**:
**Structured Data - Relational DBs**
1. Clod SQL
2. Cloud Spanner
**Unstructured Data - Non-Relational DBs**
1. Big Table
2. Firestore
3. Memory Store

**Big Query** (Data Warehouse)
We can also query public or commercial datasets


**Google Dataflow**
A fully managed service for executing Apache Beam pipelines within the Google Cloud Platform ecosystem
Dataset may be bounded (file) or unbounded (subscription flow data received constantly)

**Google Pub/Sub**
A fully managed real-time messaging service that allows you to send and receive messages between independent applications

**Security:**
Security in Transit and at Rest and IAM
Cloud Monitoring provides monitoring of Resources and can monitor also AWS logs

TensorFlow open source library for computational calculations related with ML


## Billing

### Billing Account and Organizations
1 Organization can have 1-N Billing Accounts
1 Project is linked to 1 Billing Account

Roles assigned at Organization layer are inherited by all attached billing accounts 
Roles assigned to Billing account are applied only to that Billing account

Billing Account Roles:
1. Billing Account Administrator
2. Billing Account Creator
3. Billing Account User

Best Practices for Billing Account Roles
1. Principle of least privilege
2. Assign Multiple Administrators

**Billing Reports** help us answer the following questions:
1. How much are we spending?
2. What are our cost trends?
3. What products, SKU and other are driving our costs?

We can also **export these Billing data** to Big Query, to perform further in-depth analytics of billing data, by:
1. creating a big query dataset (needs BigQuery User role)
2. configure billing export to above dataset (needs BigQuery Administrator role)

Budget alerts help us understand problems and notifies us

**Budgets and Alerts**:
1. We configure a Budget for an entire account or limit it by project ID, product or label.
2. We configure Alert Thresholds for reaching different percentages of the monthly budget
3. Default == Billing admins are notified if threshold reached and no actions take place. We can configure notifications to Cloud Monitoring and Pub/Sub for further actions

**Cost Reduction Tools on GCP**:
1. **Rightsizing VMs** - Helps by recommending the ideal VM size to not over-provision or under-provision based on past usage
2. **Sustained Use Discounts** - When a set amount of compute is used for at least 25% of the month is used discount is applied - Up to 30% discount. Does not overlap with commited use
3. **Committed Use Discounts** (reserved instance) - Can save up to 70% with 1-3 year commitment
4. **Preemptible VMs** (Spot instance) - Can save up to 80%
5. **Cloud Storage Classes** - (Standard / Nearline / Coldline / Archive)
6. **Cloud Storage Lifecycle Policies** : Automatically delete
7. **Free tier Resources**: As long as i am in the Free tier


## Compute

### AppEngine (like AWS Elastic Beanstalk / Azure App Service)
PaaS, Minimal maangement overhead and no server setup or provisioning
Automatic Scaling and Load Balancing
Great for websites, mobile apps and business apps
Standard: More proprietary, Limited languages, Faster spin-up, Less expensive
Flexible: Standardized on Docker, Broader language/versions/slower spin up, more epxensive
1. Services: The microservices comprising the full app can communicate with RESTFUL APIs
2. Versions: Multiple versions for the app, directing traffic there at will
3. Instances: The specific instances running for the app
4. Task Queues: Push/Pull Queues and Cron Jobs
5. Security Scans: Cross site scripting etc
6. Firewall Rules: Default that can be changed
7. Quotas: Used quotas by the App so that i understand if there will be a problem 
8. Blobstore: Old way of storing files. Cloud Storage should be used instead
9. Memcache: Supports Memcache for the application
10. Search: Enable indexing
11. Settings: Permanently prohibit code downloads, disable application (costs will still apply), identity aware proxy to restrict access to services, custom domains, SSL certificates, emails senders

### Compute Engine (like AWS EC2 / Azure Virtual Machines)
IaaS, Scalable high performance VMs, completely customizable, public or private images, various storage options, works also with containers, VPC support, firewalls, complete routing 
1. VM Instances - List of instances
2. Instance Templates - Managed (identical instances, can load balance, health problems are fixagble etc - preferrable) and Unmanaged Instances (having different config - NO ASG, NO Templates). 
3. Disks - Max 65TB - can be SSD or Standard or Local SSD
4. Snapshots
5. Images
6. TPUs - Tensor Processing Unit
7. Committed Use Discounts
8. Metadata - (Tags)
9. Health CHecks - Health check on Instances
10. Zones - Per zone instances and disks
11. Operations 
12. Quotas
13. Security Scans
14. Settings - Daily Usage report, Microsoft License Mobility

### Kubernetes Engine ( like AWS EKS and ECS / Azure Kubernetes Service)
Managed Orchestrated environment for containerized applications, uses Compute Engine instances to form cluster, relies on open source Kubernetes cluster management, Docker containers supported, Integrated load balancing, node pools supported, automatic cluster and node scaling, automatic upgrades, automatic repair based on health reports, automatic logging and monitoring
Kubernetes Master orchestrate what is deployed / where

### Google Cloud FUnctions (AWS Lambda / Azure Functions Serverless Compute)
Serverless environment for executing code and connecting cloud services, fully managed, triggers Http Request . Cloud Storage event / Pub/Sub event, UseCases: webHooks / Data and Image processing / Mobile Back End / IoT respond to Sub/Pub from Devices


## Security

### Securing Cloud Identity (Amazon Cognito / Azure Active Directory B2C)
IDaaS, manage resources hirerchically, assign unmanaged accounts (outside your Organization / Google Cloud) to projects, allows Single Sign On.
Policy Inheritance flows down the hierarchy (Organization -> Folders -> Project -> Resources)

### Authorizing with Cloud IAM
Unified Resource Access Management system, for Users and Services, having 3 main Components: 
1. Policies (who can do what on which resources) - for Identities like Google Account / Service Account / Google Group / Google Apps Domain
2. Roles (list of permissions assigned to identities e.g. Google Account, Unmanaged account, Service account, Google Group, G-Suite domain )
3. Resources (projects and folders, cloud services, aspects of those services such as instances, buckets,topics etc)

### Cloud KMS
Cryptgraphic Key Management Systems, Keys are used to encrypt/decrypt files
Hierarchical like IAM (Project->Location->Key Ring -> Key-> Key Version)
Project-based resource
Location is specified (Regional, Multi Regional , Global)
Key ring is a collection of keys in a specified location for a specific project
Individual keys inherit permissions from key ring
Different key versions have different encryptuin/decryption values
Key version states: Enabled/Disabled/Scheduled for Destruction/Destroyed
Key versions can be rotated regularly and automatically or manually

### Cloud IAP (Identity Aware Proxy)
Application-level authorization service
Based in internal Google enterprise security model, BeyondCorp
Supplements network level firewalls
Ideal for line of business apps
No VPN Needed, Straight forward implementation for administrators, simple to use for remote workers, no additional charge
Restricts users to the one granted access only (if enabled)

## Storage and Databases

### Google Cloud Storage (AWS S3 / Azure Blob Storage)
Project based bucket, Globally Unique ID, Specific Location

**Storage**:
1. Where to store data (Region/Dual Region/Multi region)
2. Class (Standard/Nearline/Coldline/Archive)
3. Access control (Fine-grained / Uniform)
4. Encryption (Google managed key/Customer managed key)

The link to gsutil is where i upload via CLI

### Cloud DataStore (AWSDynamoDB, Azure CosmosDB)
NoSQL for semistructured data
ACID Transactions
HIghly Available and Scalable
Accessible Via Console, JSON API, GQL (like SQL)
Kinds - like tables
Entity - like row but can have different properties
Property - like field but can have multiple values
Key - like primary index

### Cloud Sql (AWS RDS-Aurora, Azure DB for MySQL and for PostgreSQL)
Fully managed relational database service
Supportes PostgreSQL 9.6 and MySQL 5.5, 5.6, 5.7
Robust scalability
Automatic replication and backup
Highly configurable SQL instances
Data automatically encrypted
Default firewals for each instance
Full integration with Google Cloud services

Non indexed properties do not return data on queries similar to where > "property"

### Cloud Big Table (AWS DynamoDB, Azure Cosmos DB)
Run large analytical and operational workloads using this fully managed scalable NoSQL database service for big data
Used for Gmail, Google Search, Maps and Analytics as well as eBay and Spotify
Differences from CloudStore:
1. Wide column database (vs document database)
2. There is No SQL like language available
3. Single key per row
4. Capable of holding PB of information
5. Consistent Low latency and high throughput
6. Dynamically change cluster size

Use Cases: graph data, financial data, marketing data

**CBT tool** allows to manage Cloud Big Tables

### Cloud Spanner (Amazon Aurora , Azure SqlDatabase)
CloudSpanner is a fully managed enterprise -grade relational database service
Is to Cloud SQL what CloudBigTable is to Cloud DataStore
5 Nine's Availability
Multiple Client Libraries
Scales Horizontaly like NoSql databases
Industry standard SQL and supports DDL
Use Cases: Call Centers, Financial Trading, Telecom, Transportation

### Cloud Memory Store (Amazon Elasticache, Azure Cache)
Fully managed, in-memory datastore service
Redis protocol compatible
Sub-milliseconds latency
Scales up to 300GB instance
Connects with AppEngine, Compute Engine and Kubernetes Engine
Service Tiers:
1. Basic - Basic Caching
2. Standard - HA Redis instance

Use cases: caching layer in gaming and analytical pipelines, stream processing
## Big Data

### Big Query (Amazon Athena/Redshift, Azure Synapse Analytics)
Fully managed data warehouse for big data
Near real-time interactive analysis of massive datasets (terrabytes in seconds)
Standard SQL
Storage and computing are separate
Query public or commerical dataset with my own
Can query external services (CloudStorage,CloudBigTable and Google Drive)
Automatic data replication
Comprised of Datasets and Queries
Use cases: Real time inventory, predictive digital marketing, analytical events

### Cloud DataFlow (Kinesis, Stream Analytics)
Based on Apache Beam, fully managed serverless service for creating pipelines to process data
Processes data on multiple machines in parallel
Handles both streaming and batch data
Best option if there is no current implementation with Apache Hadoop or SPark
Jobs can be created from templates
Use Cases: Analytical dashboards, forecasting sales trends, ETL Operations

### Cloud DataProc (AWS EMRm AWS Batch, AWS Glue, Azure Data Lake Analytics,HDInsight)
Fully managed CLUSTER data processing service
Compatible with Hadoop,Spark,Hive
Fast Cluster Creation, scales clusters up and down without stopping the jobs
Workflow templates supported
(For more advanced cases than DataProc)
Options: Single Node (1M - 0workers), Standard (1M - N workers), High Availability (3 M - N workers)


### Cloud Pub/Sub (AWS Kinesis, Azure Event Hubs)
Fully managed messaging middleware
Allows secure and HA messages between independent apps
Works with Google Cloud and external services
1-N, N-1, N-M communications
Both Push and Pull options
Encrypted and HIPAA compliant messaging
Use cases: Streaming data, event notifications, asynchronous workflow
Accepts FROM:
1. Cloud Logs
2. Cloud API
3. Cloud DataFlow
4. Cloud Storage
5. Compute Engine

Sends data TO:
1. Cloud networjung
2. compute engine
3. Cloud Dataflow
4. App Engine
5. Cloud monitoring

### Cloud DataLab 
Interactive data analysis and machine learning environment
Packaged as a container and runs in a VM Instance
Based on Jupyter Notebooks which can calculate results as well as visualize them in charts/bar graphs etc

### Cloud Data Studio
To create interactive Dashboards and BI Visualizers
Connects to Cloud BigQuery,Spanner, Data Storage, SQL
Process is -> connect to data source -> visualize data in report -> share report

## NEtworking


## Cutting Edge Google Cloud