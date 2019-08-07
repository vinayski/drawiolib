# AWS
## Networking
### VPC
#### Default VPC

##### All subnets are public

##### If delete public VPC, you have to contact to AWS to get it back

#### VPC Peering

##### connect 1 VPC with another

##### don't give access to internet

##### don't give access to third VPC via another VPC

#### Tenancy

##### Default

##### Dedicated

###### If you set dedicated while creating new VPC, all instances in the VPC will be automatically dedicated

#### Route Tables

##### Default route table will be created for VPC automatically

#### Subnetworks

##### 1 subnet = 1 AZ

##### Amazon reserves 3 IP addresses in every subnet

#### IGW

##### 1 IGW per VPC

#### NAT Instance

##### Disable Source/Destination check

##### larger instance provide more network performance

#### Access Control List (ACLs)

##### It is a Firewall for entire subnet

##### If you create subnet, it will be associated with Default ACL

##### stateless

##### New ACLs is denied by default

##### Subnet can ONLY have 1 ACL (no more, no less)

##### operating of rules begins from lowest rule number

### Direct Connect
#### Provide dedicated link to AWS

### Route53
#### Always choose Alias Record over CNAME http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html

#### ELB is domain

#### Routing Policies

##### Simple

##### Weighted

###### Allow split traffic based on different weight assigned

##### Latency

###### based on lowest network latency for your end user (ie. which region gave the fastest response time)

##### Failover

###### Will monitor primary web site using health checks and if failed switch to DR site

##### Geolocation

###### based on Geo location of end users

## Compute
### EC2
#### Price

##### On Demand

###### Low price and flexibility without long term commitments

###### Application with short term and cannot be interrupted

###### development or testing

##### Reserved (1 or 3 Year)

###### Steady state or predictable usage

###### require reserved capacity

###### User is able to do upfront payment

##### Spot

###### Application can flexible start and end

###### very low compute price

###### user need urgent large computing needs

###### NOTE: If AWS terminate instance by itself you will not pay for part hour usage. But I you terminate, you will pay

#### Types

##### t2 - Low cost, General Purpose

##### M4, M3 - General purpose

##### C3, C4 - Computer optimised

##### R3 - Memory optimised

##### G2 - GPU

##### I2 - High Speed Storage (NoSQL...)

##### D2 - Dense storage (hadoop ..)

#### EBS

##### Type

###### General Purpose SSD (GP2)

###### Provisioned IOPS SSD (IO1)

###### Magnetic (Standard)

##### Encription

###### Root volume (where is OS) is NOT encrypted. You can use THIRD tools to encrypt Root volume

###### Addition volumes can be encrypted

#### SG

##### All Inbound traffic is blocked by default

##### All Outbound traffic is allowed by default

##### Changes to SG take effect immediately

##### SGs are STATEFUL

###### If you create Inbound rule allowing traffic in, that traffic is allowed back out again

#### Volume

##### exist on EBS

##### Virtual Hard Disk

##### Volume restored from encrypted snapshot is encrypted

##### RAID

###### AWS does NOT recommend to use RAID5

###### RAID0 - no redundancy and good performance

###### RAID10 provide redundancy and good performance

###### Creating Snapshot of RAID

#### Snapshot

##### exist on S3

##### is incremental. Only changed block will be upload to s3

##### Snapshot of encrypted volume is encrypted automatically

##### You can share snapshot, if the snapshot is NOT encrypted

##### To create snapshot of Root volume, you need to stop instance (or the instance will be stopped by AWS). If an instance was not stopped at all, integrity of filesystem can not be guaranteed

##### You can NOT remove snapshot if the snapshot is in AMI

#### AMI

##### EBS root volume

###### Root volume is EBS volume that created from EBS snapshot

##### Instance Store

###### Root device launched from AMI is instance store volume created from template stored on S3. (takes a bit more time to launch)

###### can not be stopped

###### if the underling host fails you will lose your data

#### ELB

##### only has own DNS name, NOT IPs

#### IAM Role

##### You can NOT change role for created instance

##### You can change role itself and it will be applied immediately

##### Roles are easier to manage

#### Instance Metadata

##### http://169.254.169.254/latest/meta-data/

##### You can NOT to get user-data using the URL. Only meta-data

#### Placement Group

##### Single AZ

##### Low latency

##### 10 Gbps

##### Name of Placement Group should be unique accoss AWS account

##### Only certain type of instances can be launched in PG (CPU, GPU, RAM and Storage optimised)

##### AWS recommend to use homogeneous instance type (same family and same size)

##### can NOT merge PGs

##### can NOT move created instance to PG

### EC2 Container Service
### Elastic Beanstalk
### Lambda
#### is event driven compute service, where Lambda runs your code in responce to event

## Storage
### S3
#### Object base storage. Key, value storage. Consist:

##### Key (name of the object)

##### Value

##### Version ID (Important for versioning)

##### Metadata

##### Subresources

##### Access Control List

#### File size can be from 1 Byte to 5 Tb

#### Universal namespace: https://s3-us-east-1.amazonaws.com/bucketname

#### Name for bucket does not support Capital characters

#### Read after  Write consistency for PUTS of new Objects

#### Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

#### Availability: 99.99%

#### Durability: 99,999999999 (11 x 9's)

#### New objects in Bucket are Private

#### Tiered Storage Availability (can be set/change for entire Bucket or objects in the Bucket)

##### S3

###### Availability: 99.99%

###### Durability: 99,999999999 (11 x 9's)

##### S3 - IA (Infrequently Access)

###### Lower fee than S3

###### Retrieval fee

###### Standard - IA has a minimum object size of 128KB. Smaller objects will be charged for 128KB of storage.

###### Minimum Storage Duration: 30days

##### Reduced Redundancy Storage

###### Availability: 99.99%

###### Durability: 99,99

#### Lifecycle Management

##### can be applied to whole bucket or prefix

##### Actions (without versioning)

###### Transition to S3-IA (minimum 30 after creating)

###### Archive to Glacier

###### Permanent Delete

##### Actions (with versioning)

###### Actions for current version

###### Action for previous versions

#### Versioning

##### Can't turn it off

##### Versioning's MFA Delete capability

##### Doesn't deduplicate (S3 keeps all versions of a file as separate files)

#### Security

##### Bucket is PRIVATE by default

##### Access Controle

###### Bucket Policies (applied to whole bucket)

###### Access Control List (can be applied to individual items in bucket)

##### Encriptions

###### In Transite

###### At Rest

#### Transfer Acceleration

##### Allow to upload files to S3 via CloudFront Edge

#### Cross Region Replication

##### Doesn't replicate existing files

##### Requires Versioning

### Cloud Front
#### Edge Location

##### supports READ and WRITE

##### around the world, more than 50

##### TTL

##### Can clear cached objects (you will be charged )

#### Origin

##### S3 bucket

##### EC2 instance

##### ELB

##### Route53

##### None AWS server

#### Distribution

##### Web Distribution

##### RTMP - media streaming

#### Geo Restrictions

##### White list

##### Black list

#### Invalidation

##### to remove objects from cache

### Glacier
#### Archive data

#### Takes 3-5 hours to restore

#### Extremely low-cost (0.01$ per 1Gb per 1 month)

#### Minimum Storage Duration: 90 days

### EFS
#### Supports NFSv4

#### pay only for storage

#### scale up to petabytes

#### supports thousands NFS concurrency connections

#### cross AZ within single region

#### READ after WRITE concistency

### Import/Export
#### Import/Export Disk

##### Import

###### S3

###### EBS

###### Glasier

##### Export

###### S3

#### Import/Export Snowball

##### Only S3

### Storage Gateway
#### is a service that connect an on premises software appliance with cloud based storage to provide seamless and secure integration between organisation's on-premises IT env and AWS cloud

#### Types

##### Gateway Store Volume

###### Entire Dataset is stored on site and is asynchronously backed up to S3

##### Gateway Cached Volume

###### Data in on S3 but the most frequent accessed data is stored locally

###### if you lose internet, you will not have access to all data

##### Gateway Virtual Tape Libary (VTL)

###### Provide a Virtual Tape Shelf to backup to S3 or Glacier

## Databases
### Elasticache - In memory caching
#### Memcached

#### Redis

### DMS
### RDS - OLTP (Online Transaction Processing)
#### Aurora

##### Autoscaling Storage (start from 10Gb, scales in 10Gb increment Up to 64Tb)

##### Compute resources scale up to 32 vCPU and 244 Gb RAM

##### 2 copies of data in each AZ within 3 minimum AZs (6 copies of data)

##### can loss up to 2 copies without effecting Write availability

##### can loss up to 3 copies without effecting Read availability

##### self-healing (disk is continuously scanning for error and repairing)

##### Replicas

###### Aurora Replica (up to 15)

###### MySQL Replica (up to 5)

#### Types

##### MSSQL

##### MySQL

##### Postgres

##### Oracle

##### Aurora

##### MarinaDB

#### Automated Backups

##### from 0 up to 35 days

##### Storage IO may be suspended

##### you will get free place on S3 equals DB volume

#### Snapshots

##### manually

##### will be stored even if you remove source DB (unlike Automated Backup)

#### Restoring is always new RDS instance with new endpoint

#### Encryption

##### supports by MySQL, Postgres, Oracle, mariaDB and SQL Server

##### Can NOT be enabled for existing instances

#### MultyAZ

##### For Disaster Recovery ONLY

##### Automatic

##### synchronous

#### Read Replica

##### Asynchronous replication

##### MySQL, Postgres, MariaDB

##### Use for Scaling. NOT for DR

##### Require Automatic Backup

##### Up to 5 Read REplicas

##### can have Read Replica of Read replica (Latency!!)

##### Read Replica can NOT be MultyAZ

##### Read replica in Second Region (for MySQL and MariaDB)

#### NOTES

##### DB Security Group: you don't need to specify  port/protocol only source IP range / security group http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html#Overview.RDSSecurityGroups.DBSec

### DynamoDB - No SQL
#### Automatic Scaling on FLY vs

#### Stored on SSD

#### Spread across 3 geographically distinct data centers

#### Eventual consistency Reads (default)

##### Consistency across all copies of data is usually reached within 1 second

#### Strong Consistency Reads

##### returns a result of all writes

#### Pricing

##### Read Throughput 0.0065 per hour for every 50 units

##### Write Throughput 0.0065 per hour for every 10 units

##### Storage const of 0.25$ per Gb per month

### Redshift - OLAP (Online Analytic Processing)
#### data warehouse service in a cloud

#### Single Node (160Gb)

#### Multi-Node

##### Leader Node (handle queries)

##### Compute Node (store data, perform queries) up to 128 nodes

#### Price

##### Leader node is free

##### Compute node: charge for hours instances running

##### Backup

##### Data transfer (within VPC)

#### Encryption

##### SSL/TSL for data transfer

##### Encrypted at rest using AES-256

##### By default Redshift handle key by it self

###### But you can use KMS or

###### Manage your own keys using HSM

#### Availability

##### only 1 AZ

###### you can restore snapshot to New AZ

## Analytics
### EMR
### Data Pipeline
### ElasticSearch
### Kinesis
### Machine Learning
### Quick Sight
## Security & Identity
### IAM
#### Users

#### Groups

#### Roles

#### Policies

#### Notes

##### IAM items are shared globally

##### New users don't have any permissions

##### Root account has complete Admin access by default

##### Power User Access allows access to all AWS services except for management of groups and users within IAM

### Directory Service
### Inspector
### WAF
### Cloud HSM
### KMS
## Management Tools
### CloudWatch
#### Basic Monitoring

##### Every 5 min

##### Free

#### Detailed Monitoring

##### Every 1 min

##### Additional charge

#### Dashboard

#### Metrics

##### CPU

##### Disk

##### Network

#### Events

##### Allow to react on changes

#### Alarms

##### Allow to react if metrics cross thresholds

#### Logs

##### Allow to aggregate, monitor and store logs

### CloudFormation
### CloudTrail
### Opsworks
### Config
### Service Catalog
### Trusted Advisor
## Application Services
### API Gateway
### AppStream
### CloudSearch
### Elastic Transcoder
### SES
### SQS
#### Distributed queue system

#### Message is up to 256KB text in any format

#### Billed at 64KB "Chunks"

#### first 1 million requests are free. 0.5$ per million

#### 1 request can have up to 10 messages

#### Messages can be retrieved using SQS API

#### Has Buffer

#### SQS ensures delivering at least once

#### It is NOT FIFO

#### Asynchronously PULL messages from a QUEUE

#### Visibility Period starts when Message was picked up

#### If Application is failed, message will be in a queue. After Visibility Period, Message will be consumed another application

#### When application finishes, message will be removed from Queue

#### Visibility Timeout is 30s by default.

#### Retention period is up to 14 days

### SWF
#### Simple WorkFlow Service

#### Retention Period is up to 1 year

#### task oriented API (vs SQS is message oriented)

#### task is assigned ONLY ONCE

#### SWF tracks all tasks in application (for SQS you need implement your own application level )

#### SWF Actors (can be Code or Humans)

##### Workflow Starter - start workflow

##### Deciders - control workflow

##### Activity Workers

## WhitePapers
### Security
#### Shared Security Model

#### Storage Decommissioning

##### DoD 5220.22-M or NST 800-88

#### Amazon Corporate Segregation

#### Network monitoring & Protection

##### DDOS

##### Man in the middle attack (MITM)

##### IP spoofing

##### Port scanning

###### you should request permission for vulnerable port scanning in advance

##### Port sniffing by other tenants

#### Instance Isolation

##### instances on the same host  are isolated by Xen hypervisor

##### AWS firewall resides on hypervisor so instances on the same host don;t have more permissions than other

##### RAM is separated

##### disk and RAM are zeroing

#### AWS doesn't have a write/read access to your guest OS

#### Strategic Busyness Plan at least biannually (every 6 month)

#### AWS scans Public Services for vulnerability

#### Compliances

##### SOC1,2,3

##### FISMA, DIACAP, REDRAMP

##### PCI DSS level1 (only infrastructure)

##### ISO27001

##### ISO 9001

##### ITAR

##### FIPS 140-2

##### Industrial Standarts

###### HIPAA

###### Cloud Security Alliance

###### Motion Picture Association of America

## Development Tools
### CodeCommit
### CodeDeploy
### CodePipeline
## Basic
### Support
#### Basic, Developer, Business, Enterprise

## Mobile Services
### Mobile Hub
### Cognito
### Device Farm
### Mobile Analytics
### SNS
#### Sends notifications from a cloud

#### Can push notification to mobile devices

#### push to SQS

#### send email

#### trigger Lambda function

#### messages are redundantly stored across multy AZ

## Enterprise Applications
### WorksSpaces
### WorkDocs
### WorkMail
## Internet Of Things
