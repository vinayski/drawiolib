#AWS Well-Architected Framework
## Intro
### The AWS Well-Architected Framework helps you understand the pros and cons of decisions you make while building systems on AWS. By using the Framework you will learn architectural best practices for designing and operating reliable, secure, efficient, and cost-effective systems in the cloud. It provides a way for you to consistently measure your architectures against best practices and identify areas for improvement.
## 5 Pillars
### Operational Excellence
#### The ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.

### Security
#### The ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies.

### Reliability
#### The ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions such as misconfigurations or transient network issues.

### Performance Efficiency
#### The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

### Cost Optimization
#### The ability to run systems to deliver business value at the lowest price point.

## Mindset
### â€œGood intentions never work, you need good mechanisms to make anything happenâ€ Jeff Bezos. This means replacing humans best efforts with mechanisms (often automated) that check for compliance with rules or process.
## TOGAF The TOGAFÂ® Standard, Version 9.2
## General Design Principles
### Stop guessing your capacity needs
#### With cloud computing, these problems can go away. You can use as much or as little capacity as you need, and scale up and down automatically.

### Test systems at production scale
#### In the cloud, you can create a production-scale test environment on demand, complete your testing, and then decommission the resources

### Automate to make architectural experimentation easier
#### Automation allows you to create and replicate your systems at low cost and avoid the expense of manual effort.

### Allow for evolutionary architectures
#### As a business and its context continue to change, initial decisions might hinder the systemâ€™s ability to deliver changing business requirements. In the cloud, the capability to automate and test on demand lowers the risk of impact from design changes.

### Drive architectures using data
#### In the cloud you can collect data on how your architectural choices affect the behavior of your workload. This lets you make fact-based decisions on how to improve your workload. Your cloud infrastructure is code, so you can use that data to inform your architecture choices and improvements over time.

### Improve through game days
#### Test how your architecture and processes perform by regularly scheduling game days to simulate events in production.

## Operational Excellence
### Design Principles
#### Perform operations as code

##### You can define your entire workload (applications, infrastructure) as code and update it with code.

##### You can script your operations procedures and automate their execution by triggering them in response to events.

#### Annotate documentation

##### In the cloud, you can automate the creation of annotated documentation after every build (or automatically annotate hand-crafted documentation). Annotated documentation can be used by people and systems. Use annotations as an input to your operations code.

#### Make frequent, small, reversible changes

##### Design workloads to allow components to be updated regularly. Make changes in small increments that can be reversed if they fail (without affecting customers when possible).

#### Refine operations procedures frequently

##### As you use operations procedures, look for opportunities to improve them. As you evolve your workload, evolve your procedures appropriately. Set up regular game days to review and validate that all procedures are effective and that teams are familiar with them.

#### Anticipate failure 

##### Test your failure scenarios and validate your understanding of their impact. Test your response procedures to ensure that they are effective, and that teams are familiar with their execution

#### Learn from all operational failures

##### Drive improvement through lessons learned from all operational events and failures. Share what is learned across teams and through the entire organization.

### Best practice areas
#### The AWS service that is essential to Operational Excellence is AWS CloudFormation

#### 1. Prepare

##### Mechanisms to monitor and gain insight ( application, platform, infrastructure components, customer experience andbehavior)

##### Validate through checklists to ensure a workload meets defined standards and capture it in runbooks

##### Using AWS CloudFormation enables you to have consistent, templated, sandbox development, test, and production environments

##### Implement the minimum number of architecture standards for your workloads

##### Balance the cost to implement a standard against the benefit to the workload and operations

##### Invest in scripting operations activities to maximize the productivity of operations personnel, minimize error rates, and enable automated responses

#### 2. Operate

##### Ðžperational health includes both the health of the workload and operations (for example, deployment and incident response).

##### Communicate the operational status of workloads through dashboards and notifications that are tailored to the target audience (for example, customer, business, developers, operations)

##### AWS provides workload insights through logging capabilities including AWS X-Ray, CloudWatch, CloudTrail, and VPC Flow Logs

##### Routine operations, responses to unplanned events, should be automated. NO manual processes for deployments, release management, changes, and rollbacks

##### Releases should NOT be large batches that are done infrequently.

##### Have a rollback plan, and the ability to mitigate failure impacts for continuity of operations

#### 3. Evolve 

##### Dedicate work cycles to making continuous incremental improvements.

##### Regularly evaluate and prioritize opportunities for improvement, including both the workload and operations procedures.

##### Share lessons learned across teams to share the benefits of those lessons.

##### Analyze metrics and trends within lessons learned and perform cross-team retrospective analysis

## Security
### Design Principles
#### Implement a strong identity foundation

##### Appropriate authorization for each interaction with your AWS resources. Centralize privilege management and reduce or even eliminate reliance on long-term credentials.

#### Enable traceability

##### Monitor, alert, and audit actions and changes to your environment in real time. Integrate logs and metrics with systems to automatically respond and take action.

#### Apply security at all layers

##### E.g., edge network, VPC, subnet, load balancer, every instance, operating system, and application)

#### Automate security best practices

##### Create secure architectures, including the implementation of controls that are defined and managed as code in version-controlled templates.

#### Protect data in transit and at rest 

##### Classify your data into sensitivity levels and use mechanisms, such as encryption, tokenization, and access control where appropriate.

#### Keep people away from data

##### Create mechanisms and tools to reduce or eliminate the need for direct access or manual processing of data

#### Prepare for security events

##### Have an incident management process. Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery.

### Best practice areas (Key AWS Services)
#### 1. Identity and Access Management

##### IAM enables you to securely control access to AWS services and resources.

##### MFA (multi-factor authentication) adds an additional layer of protection on user access.

##### AWS Organizations lets you centrally manage and enforce policies for multiple AWS accounts.

#### 2. Detective Controls

##### AWS CloudTrail records AWS API calls

##### AWS Config provides a detailed inventory of your AWS resources and configuration.

##### Amazon GuardDuty is a managed threat detection service that continuously monitors for malicious or unauthorized behavior.

##### Amazon CloudWatch is a monitoring service for AWS resources which can trigger CloudWatch Events to automate security responses.

#### 3. Infrastructure Protection

##### Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network

##### Amazon CloudFront is a global CDN that securely delivers data, videos, applications, and APIs to your viewers which integrates with AWS Shield for DDoS mitigation

##### AWS WAF is a web application firewall that is deployed on either Amazon CloudFront or Application Load Balancer to help protect your web applications from common web exploits.

#### 4. Data Protection

##### Services such as ELB, Amazon Elastic Block Store (Amazon EBS), Amazon S3, and Amazon Relational Database Service (Amazon RDS) include encryption capabilities to protect your data in transit and at rest.

##### Amazon Macie automatically discovers, classifies and protects sensitive data

##### AWS Key Management Service (AWS KMS) makes it easy for you to create and control keys used for encryption

#### 5. Incident Response

##### IAM should be used to grant appropriate authorization to incident response teams and response tools

##### AWS CloudFormation can be used to create a trusted environment or clean room for conducting investigations.

##### Amazon CloudWatch Events allows you to create rules that trigger automated responses including AWS Lambda

## Reliability
### Design principles
#### Test recovery procedures

##### In the cloud, you can test how your system fails, and you can validate your recovery procedures. You can use automation to simulate different failures or to recreate scenarios that led to failures before.

#### Automatically recover from failure

##### Trigger automation when a threshold is breached. This allows for automatic notification and tracking of failures, and for automated recovery processes that work around or repair the failure. With more sophisticated automation, it's possible to anticipate and remediate failures before they occur.

#### Scale horizontally to increase aggregate system availability

##### Replace one large resource with multiple small resources to reduce the impact of a single failure on the overall system

#### Stop guessing capacity

##### In the cloud, you can monitor demand and system utilization, and automate the addition or removal of resources to maintain the optimal level to satisfy demand without over or under- provisioning.

#### Manage change in automation

##### Changes to your infrastructure should be done using automation. The changes that need to be managed are changes to the automation.

### Best practice areas (Key AWS Services)
#### 1. Foundations

##### IAM enables you to securely control access to AWS services and resources.

##### Amazon VPC lets you provision a private, isolated section of the AWS Cloud where you can launch AWS resources in a virtual network

##### AWS Trusted Advisor provides visibility into service limits

##### AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards web applications running on AWS.

#### 2. Change Management

##### AWS CloudTrail records AWS API calls for your account and delivers log files to you for auditing

##### AWS Config provides a detailed inventory of your AWS resources and configuration, and continuously records configuration changes

##### Auto Scaling is a service that will provide an automated demand management for a deployed workload

##### CloudWatch provides the ability to alert on metrics, including custom metrics

##### CloudWatch also has a logging feature that can be used to aggregate log files from your resources

#### 3. Failure Management

##### AWS CloudFormation provides templates for the creation of AWS resources and provisions them in an orderly and predictable fashion

##### Amazon S3 provides a highly durable service to keep backups

##### Amazon Glacier provides highly durable archives

##### AWS KMS provides a reliable key management system that integrates with many AWS services

## Performance Efficiency
### Design principles
#### Democratize advanced technologies

##### Rather than having your IT team learn how to host and run a new technology (NoSQL databases, media transcoding, machine learning etc), they can simply consume it as a service focusing on product development rather than resource provisioning and management.

#### Go global in minutes

##### Easily deploy your system in multiple Regions around the world with just a few clicks.

#### Use serverless architectures

##### This not only removes the operational burden of managing servers, but also can lower transactional costs because these managed services operate at cloud scale.

#### Experiment more often

##### With virtual and automatable resources, you can quickly carry out comparative testing using different types of instances, storage, or configurations.

#### Mechanical sympathy

##### Use the technology approach that aligns best to what you are trying to achieve. For example, consider data access patterns when selecting database or storage approaches.

### Best practice areas (Key AWS Services)
#### 0

##### Take a data-driven approach to selecting a high-performance architecture

##### Your architecture will likely combine a number of different architectural approaches (for example, event-driven, ETL, or pipeline).

#### 1. Selection

##### Four main resource types that you should consider (compute, storage, database, and network)

##### Compute

###### In AWS, compute is available in three forms: instances, containers, and functions

###### Instances

###### Containers

###### Functions

##### Storage

###### The optimal storage solution for a particular system will vary based on the kind of

###### Access method (block, file, or object)

###### Patterns of access (random or sequential)

###### Throughput required 

###### Frequency of access (online, offline, archival)

###### Frequency of update (WORM, dynamic)

###### Availability and durability constraints

###### Well-architected systems use multiple storage solutions and enable different features to improve performance.

##### Database

###### The optimal database solution for a particular system can vary based on requirements for availability, consistency, partition tolerance, latency, durability, scalability, and query capability

##### Network

###### In AWS, networking is virtualized and is available in a number of different types and configurations.

###### AWS offers product features (for example, Enhanced Networking, Amazon EBS-optimized instances, Amazon S3 transfer acceleration, dynamic Amazon CloudFront) to optimize network traffic

###### AWS also offers networking features (for example, Amazon Route 53 latency routing, Amazon VPC endpoints, and AWS Direct Connect) to reduce network distance or jitter.

#### 2. Review

##### Over time new technologies and approaches become available that could improve the performance of your architecture.

#### 3. Monitoring

##### After you have implemented your architecture you will need to monitor its performance so that you can remediate any issues before your customers are aware.

##### Amazon CloudWatch provides the ability to monitor and send notification alarms. You can use automation to work around performance issues by triggering actions through Amazon Kinesis, Amazon Simple Queue Service (Amazon SQS), and AWS Lambda.

#### 4. Tradeoffs 

##### Depending on your situation you could trade consistency, durability, and space versus time or latency to deliver higher performance.

###### Using AWS, you can go global in minutes and deploy resources in multiple locations across the globe to be closer to your end users

###### You can also dynamically add readonly replicas to information stores such as database systems to reduce the load on the primary database

###### AWS also offers caching solutions such as Amazon ElastiCache, which provides an in-memory data store or cache

###### Amazon CloudFront, which caches copies of your static content closer to end users

###### Amazon DynamoDB Accelerator (DAX) provides a read-through/write-through distributed caching tier in front of Amazon DynamoDB, supporting the same API, but providing sub-millisecond latency for entities that are in the cache

##### Amazon ElastiCache, Amazon CloudFront, and AWS Snowball are services that allow you to improve performance. Read replicas in Amazon RDS can allow you to scale read-heavy workloads.

## Cost Optimization
### Design principles
#### Adopt a consumption model

##### Pay only for the computing resources that you require and increase or decrease usage depending on business requirements, not by using elaborate forecasting.

###### For example, development and test environments are typically only used for eight hours a day during the work week. You can stop these resources when they are not in use for a potential cost savings of 75% (40 hours versus 168 hours).

#### Measure overall efficiency

##### Measure the business output of the system and the costs associated with delivering it.

#### Stop spending money on data center operations

##### AWS does the heavy lifting of racking, stacking, and powering servers, so you can focus on your customers and business projects rather than on IT infrastructure.

#### Analyze and attribute expenditure

##### The cloud makes it easier to accurately identify the usage and cost of systems, which then allows transparent attribution of IT costs to individual business owners. This helps measure return on investment (ROI).

#### Use managed and application level services to reduce cost of ownership

##### In the cloud, managed and application level services remove the operational burden of maintaining servers for tasks such as sending email or managing databases.

### Best practice areas (Key AWS Services)
#### 0

##### There are tradeoffs to consider. For example, do you want to optimize for speed to market or for cost?

##### Design decisions are sometimes guided by haste as opposed to empirical data, as the temptation always exists to overcompensate â€œjust in caseâ€ rather than spend time benchmarking for the most cost-optimal system over time.

##### AWS Cost Explorer allows you to view and track your usage in detail. AWS Budgets will notify you if your usage or spend exceeds actual or forecast budgeted amounts.

#### 1. Cost-Effective Resources

##### Using the appropriate instances and resources for your system is key to cost savings.

###### For example, a reporting process might take five hours to run on a smaller server but one hour to run on a larger server that is twice as expensive. Both servers give you the same outcome, but the smaller server incurs more cost over time.

###### For example, rather than maintaining servers to deliver email, you can use a managed service that charges on a per-message basis.

##### Instance types

###### On-Demand Instances allow you to pay for compute capacity by the hour, with no minimum commitments required.

###### Reserved Instances allow you to reserve capacity and offer savings of up to 75% off On-Demand pricing

###### With Spot Instances individual servers can come and go dynamically, you can leverage unused Amazon EC2 capacity and offer savings of up to 90% off On-Demand pricing.

#### 2. Matching supply and demand

##### In AWS, you can automatically provision resources to match demand. Auto Scaling and demand, buffer, and time-based approaches allow you to add and remove resources as needed.

##### Demand can be fixed or variable, requiring metrics and automation to ensure that management does not become a significant cost.

#### 3. Expenditure Awareness

##### Ease of use and virtually unlimited on-demand capacity may require a new way of thinking about expenditures.

##### It eliminates the manual processes and time associated with provisioning on-premises infrastructure, including identifying hardware specifications, negotiating price quotations, managing purchase orders, scheduling shipments, and then deploying the resources.

##### The capability to attribute resource costs to the individual business or product owners drives efficient usage behavior and helps reduce waste.

#### 4. Optimizing Over Time

##### When regularly reviewing your deployments, assess how newer services can help save you money

## The Review Process
### The review of architectures needs to be done in a consistent manner, with a blamefree approach that encourages diving deep. It should be a light-weight process (hours not days) that is a conversation and not an audit. The purpose of reviewing an architecture is to identify any critical issues that might need addressing or areas that could be improved. The outcome of the review is a set of actions that should improve the experience of a customer using the workload.
