# AWS Architecture


## Global Infrastructure

### Region

- A Region is a geographical area. each AWS Region has multiple, isolated locations known as Availability Zones.
- More Regions ?

	- Better Disaster Recovery
	- Availability
	- Application Responsiveness

### Availability Zones (AZ)

- is a Data Center.
- More AZs? More Fault Tolerance

### Edge Locations

- Are endpoints for AWS which are used for caching content.
- There are many more Edge Locations than Regions.
- Currently there are over 96 Edge Locations.
- Typically this consists of:

	- CloudFront,
	- Content Delivery Network (CDN)

### Tips

- Regions & AZ Codes Format
- Disaster recovery always looks at ensuring resources are created in another region, not another regions

## Identity and Access Management

### IAM

- Intro

	- AWS Identity and Access Management (IAM) enables you to manage access to AWS services and resources securely.
	- Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

- Key Terminology

	- Root Account
	- Users
	- Groups
	- Roles
	- Policies

- Features

	- Centralised control of your AWS account
	- Shared Access to your AWS account
	- Granular Permissions
	- Multifactor Authentication
	- Identity Federation (including Active Directory, Facebook, Linkedin etc)
	- Provide temporary access for users/devices and services where necessary
	- Allows you to set up your own password rotation policy
	- Integrates with many different AWS services
	- Supports PCI DSS Compliance

- Delegation

	- You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources.
	- It is not a best practice to use IAM credentials for any production based application. It is always a good practice to use IAM Roles.

- Cross-account

	- Cross-account IAM roles allow customers to securely grant access to AWS resources in their account to a third party, like an APN Partner, while retaining the ability to control and audit who is accessing their AWS account.
	- Cross-account roles reduce the amount of sensitive information APN Partners need to store for their customers, so that they can focus on their product instead of managing keys.
	- Cross-account Role is the right tool to comply with best practices and simplify the credential management, as it gets rid of the need for credential management for third parties.

- Tips

	- IAM Roles for Tasks
	- API Gateway,
	- To ensure secure access to AWS resources from EC2 Instances, always assign a role to the EC2 Instance.

### AWS Active Directory (AD)

- AWS Directory Service/ AWS Managed Microsoft AD

	- AWS Directory Service for Microsoft Active Directory, also known as AWS Managed Microsoft AD, enables your directory-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud.
	- You can use standard Active Directory administration tools and take advantage of built-in Active Directory features, such as Group Policy and single sign-on (SSO).
	- With AWS Managed Microsoft AD, you can easily join Amazon EC2 and Amazon RDS for SQL Server instances to your domain, and use AWS Enterprise IT applications such as Amazon WorkSpaces with Active Directory users and groups.
	- AWS Managed Microsoft AD is built on actual Microsoft Active Directory and does NOT require you to synchronize or replicate data from your existing Active Directory to the cloud.
	- AWS Managed Microsoft AD can be used as the Active Directory over VPN or Direct Connect

- Simple Active Directory

	- Simple AD provides a subset of the features offered by AWS Managed Microsoft AD, including the ability to manage user accounts and group memberships, create and apply group policies, securely connect to Amazon EC2 instances, and provide Kerberos-based single sign-on (SSO)
	- However, note that Simple AD does not support features such as trust relationships with other domains, Active Directory Administrative Center, PowerShell support ...etc

- AD Connector

	- AD Connector is a directory gateway with which you can redirect directory requests to your on-premises Microsoft Active Directory without caching any information in the cloud.
	- AD Connector offers the following benefits:
	- Tips

### Amazon Cognito

- Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily.
- Amazon Cognito scales to millions of users and supports sign-in with social identity providers, such as Facebook, Google, and Amazon, and enterprise identity providers via SAML 2.0.
- Amazon Cognito User Pools

	- Intro
	- Open ID Connect Providers (Identity Pools)

### AWS Single Sign-On (SSO)

- Intro

	- AWS Single Sign-On (SSO) is a cloud SSO service that makes it easy to centrally manage SSO access to multiple AWS accounts and business applications.
	- Enable a highly available SSO service without the upfront investment and on-going maintenance costs of operating your own SSO infrastructure.
	- Easily manage SSO access and user permissions to all of your accounts in AWS Organizations centrally.

- Verification Types

	- Context Two-step Verification
	- Always-on Verification

- Permission Sets

	- A permission set is a collection of administrator-defined policies that AWS SSO uses to determine a user's effective permissions to access a given AWS account.
	- Permission sets can contain either AWS managed policies or custom policies that are stored in AWS SSO. Policies are essentially documents that act as containers for one or more permission statements.
	- These statements represent individual access controls (allow or deny) for various tasks that determine what tasks users can or cannot perform within the AWS account.

## Security

### AWS Certificate Manager (SSL/TLS)

- AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources.

### AWS Key Management Service (KMS)

- AWS Key Management Service (KMS) makes it easy for you to create and manage keys and control the use of encryption across a wide range of AWS services and in your applications.
- AWS KMS is integrated with other AWS services including AWS EBS, S3, Redshift, RDS, and others, to make it simple to encrypt your data with encryption keys that you manage.
- Customer Master Keys (CMKs)

	- The primary resources in AWS KMS are customer master keys (CMKs).
	- You can use a CMK to encrypt and decrypt up to 4 KB (4096 bytes) of data. Typically, you use CMKs to generate, encrypt, and decrypt the data keys that you use outside of AWS KMS to encrypt your data. This strategy is known as envelope encryption.
	- Customer managed CMK will generate plain text Data Key & encrypted Data Keys. documents will be encrypted using these plain text Data Keys. After encryption , plain text Data keys needs to be deleted to avoid any inappropriate use & encrypted Data Keys along with encrypted Data is stored in S3 buckets.
	- While decryption, encrypted Data Key is decrypted using Customer CMK into plain text Key which is further used to decrypt documents. This Envelope Encryption ensures that Data is protected by Data key which is further protected by another key.

- Tips

	- Used to encrypt data at rest (i.e. EBS Volumes, S3)
	- KMS is offered in several regions, but keys are not transferrable out of the region they were created in (keys are region specific)
	- KMS will rotate keys annually and use the appropriate keys to perform cryptographic operations
	- in AWS, Data can be encrypted by KMS keys or keys provided by the my company

### AWS Security Token Service (STS)

- The AWS Security Token Service (STS) is a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or for users that you authenticate (federated users).

### AWS Web Application Firewall (WAF)

- Intro

	- AWS WAF is a web application firewall that helps protect your web applications from common web exploits that could affect application availability, compromise security, or consume excessive resources.
	- AWS WAF gives you control over which traffic to allow or block to your web applications by defining customizable web security rules.
	- You can use AWS WAF to create custom rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that are designed for your specific application.
	- New rules can be deployed within minutes, letting you respond quickly to changing traffic patterns. Also, AWS WAF includes a full-featured API that you can use to automate the creation, deployment, and maintenance of web security rules. With AWS WAF you pay only for what you use.

- Pricing

	- AWS WAF pricing is based on how many rules you deploy and how many web requests your web application receives. There are no upfront commitments. You can deploy AWS WAF on either Amazon CloudFront as part of your CDN solution, the Application Load Balancer (ALB) that fronts your web servers or origin servers running on EC2, or Amazon API Gateway for your APIs.

### AWS CloudHSM (Hardware Security Module)

- AWS CloudHSM is a cloud-based hardware security module (HSM) that enables you to easily generate and use your own encryption keys on the AWS Cloud.
- CloudHSM is standards-compliant and enables you to export all of your keys to most other commercially-available HSMs, subject to your configurations.
- It is a fully-managed service that automates time-consuming administrative tasks for you, such as hardware provisioning, software patching, high-availability, and backups.
- CloudHSM also enables you to scale quickly by adding and removing HSM capacity on-demand, with no up-front costs.

## Storage

### S3

- The Basics

	- Intro
	- Features
	- Data Consistency Model For S3
	- S3 - Charges charged for

- Buckets

	- Files are stored in Buckets.
	- S3 Buckets is a universal namespace. That is, names must be unique globally. https://s3-eu-west-1.amazonaws.com/acloudguru

- S3 - Storage Tiers/Classes

	- S3 Standard
	- S3 - IA (Infrequently Accessed)
	- S3 - IA One Zone

- S3 Glacier

	- Intro
	- Types

- Lifecycle Management

	- To manage your objects so that they are stored cost effectively throughout their lifecycle, configure their lifecycle.
	- A lifecycle configuration is a set of rules that define actions that Amazon S3 applies to a group of objects. There are two types of actions:
	- ples

- Security

	- By default, all newly created buckets are PRIVATE
	- You can setup access control to your buckets using;
	- S3 buckets can be configured to create access logs which log all requests made to the S3 bucket. This can be done to another bucket.

- Encryption

	- Server Side Encryption (At Rest)
	- In Transit

- Cross-Region Replication (CRR)

	- Cross-region replication provides design for high availability and fault tolerance in case of a disaster
	- Cross-region replication enables automatic, asynchronous copying of objects across buckets in different AWS Regions.
	- Buckets configured for cross-region replication can be owned by the same AWS account or by different accounts.
	- In the minimum configuration, you provide the following:
	- Versioning must be enabled on both the source and destination buckets.
	- Files in an existing bucket are not replicated automatically. but all subsequent updated files will be replicated automatically.
	- Deleting individual versions or delete markers will not be replicated, Delete markers are replicated.
	- Tips

- Configuring Amazon S3 Event Notifications

	- The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket.
	- To enable notifications, you must first add a notification configuration identifying the events you want Amazon S3 to publish, and the destinations where you want Amazon S3 to send the event notifications.
	- You store this configuration in the notification subresource (see Bucket Configuration Options) associated with a bucket. Amazon S3 provides an API for you to manage this subresource.

- Transfer Acceleration

	- S3 Transfer Acceleration utilises the CloudFront Edge Network to accelerate your uploads to S3.
	- Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an edge location which will then transfer that file to S3.
	- When using Transfer Acceleration, additional data transfer charges may apply.

- S3 Increased Request Rate

	- Amazon S3 now provides increased performance to support at least 3,500 requests per second to add data and 5,500 requests per second to retrieve data, which can save significant processing time for no additional charge.
	- Each S3 prefix can support these request rates, making it simple to increase performance significantly.
	- Amazon S3ï¿½s support for parallel requests means you can scale your S3 performance by the factor of your compute cluster, without making any customizations to your application.
	- Performance scales per prefix, so you can use as many prefixes as you need in parallel to achieve the required throughput. There are no limits to the number of prefixes.
	- More info

- MFA Delete

	- You can optionally add another layer of security by configuring a bucket to enable MFA Delete, which requires additional authentication for either of the following operations:
	- Versioning's MFA Delete uses multi-factor authentication, can be used to provide an additional layer of security.

- Uploading Objects to Buckets Using Presigned URLs

	- A presigned URL gives you access to the object identified in the URL, provided that the creator of the presigned URL has permissions to access that object.
	- That is, if you receive a presigned URL to upload an object, you can upload the object only if the creator of the presigned URL has the necessary permissions to upload that object.
	- All objects and buckets by default are private. The presigned URLs are useful if you want your user/customer to be able to upload a specific object to your bucket, but you don't require them to have AWS security credentials or permissions.
	- When you create a presigned URL, you must provide your security credentials and then specify a bucket name, an object key, an HTTP method (PUT for uploading objects), and an expiration date and time. The presigned URLs are valid only for the specified duration.

- Tips

	- Hosting a Static Website on Amazon S3
	- Hosting a Static Website on S3 using Your Own Domain

### Storage Gateway

- Introduction

	- AWS Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration between
	- The service enables you to securely store data to the AWS cloud for scalable and cost-effective storage.
	- AWS Storage Gateway's software appliance is available for download as a virtual machine (VM) image that you install on a host in your datacenter.
	- Storage Gateway supports either
	- Once you've installed your gateway and associated it with your AWS account through the activation process, you can use the AWS Management Console to create the storage gateway option that is right for you.

- Types

	- File Gateway Network File System (NFS)
	- Volumes Gateway/iSCSI (Stored/Cached)
	- Tape Gateway (VTL)

## Compute

### EC2

- Intro

	- Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.
	- Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.
	- Amazon EC2 changes the economics of computing by allowing you to pay only for capacity that you actually use.
	- Amazon EC2 provides developers the tools to build failure resilient applications and isolate them from common failure scenarios.

- Pricing Options

	- On Demand
	- Spot
	- Reserved
	- Dedicated Hosts

- EC2 Instance Types

	- Letters
	- Types
	- How to Remember

- Amazon Machine Image (AMI)

	- Intro
	- You can select your AMI based on;
	- If you need an AMI across multiple regions, you have to copy the AMI across regions. Note that by default, AMIs that you have created will not be available across all regions.

- EC2 Storage

	- EBS Volume
	- Elastic File System (EFS)

- Instance Metadata

	- To retrieve list of variables
	- to retrieve specific metadata variable

- EBS Snapshots

	- Snapshots on S3
	- Amazon Data Lifecycle Manager (DLM)

- EC2 Placement Groups

	- Types
	- Tips

- Tips

	- You can create an AMI from the EC2 Instances and then copy them to another region. In case of a disaster, an EC2 Instance can be created from the AMI.
	- Termination Protection
	- EC2 runs only inside VPC, hence EC2 Traffic is monitored by VPC Flow Logs
	- EC2 Instance States
	- You can run up to 20 On-Demand EC2 for most of the instance. If you need more, you have to complete a requisition form and submit it to AWS.

### Lambda Functions

- Intro

	- AWS Lambda is a compute service where you can upload your code and create a Lambda function.
	- AWS Lambda takes care of provisioning and managing the servers that you use to run the code.
	- You don't have to worry about operating systems, patching, scaling, etc. You can use Lambda in the following ways.
	- Provides auto scaling

- Lambda Triggers

	- API Gateway
	- AWS JOT
	- Alexa Skills Kit
	- Alexa Smart Home
	- CloudFront
	- CloudWatch Events
	- CloudWatch Logs
	- CodeCommit
	- Cognito Sync Trigger
	- DynamoDB
	- Kinesis
	- SNS

- Supported Languages

	- Node.js
	- Python
	- Java
	- C#

- Pricing

	- Number of requests
	- Duration
	- Memory
	- Additional Charges

- Lambda -  Tips

	- Lambda scales out (not up) automatically
	- Lambda functions are independent, 1 event = 1 function
	- Lambda is serverless
	- Lambda functions can trigger other lambda functions, 1 event can = x functions if functions trigger other functions
	- Architectures can get extremely complicated, AWS X-ray allows you to debug what is happening
	- Lambda can do things globally, you can use it to back up S3 buckets to other S3 buckets etc

- Environment variables

	- Environment variables for Lambda functions enable you to dynamically pass settings to your function code and libraries, without making changes to your code.
	- Environment variables are key-value pairs that you create and modify as part of your function configuration, using either the AWS Lambda Console, the AWS Lambda CLI or the AWS Lambda SDK.
	- AWS Lambda then makes these key value pairs available to your Lambda function code using standard APIs supported by the language, like process.env for Node.js functions.

- Tips

	- to ensure that the Lambda function has access to Amazon Aurora

### Contaners Services

- Amazon ECS (Docker)

	- Amazon Elastic Container Service (Amazon ECS) is a highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containers on a cluster.
	- Amazon ECS lets you launch and stop container-based applications with simple API calls, allows you to get the state of your cluster from a centralized service, and gives you access to many familiar Amazon EC2 features.
	- Tasks
	- Batch Job Workloads
	- Service Auto Scaling

- Amazon Elastic Container Registry (ECR)

	- is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images.
	- Amazon ECR is integrated with Amazon Elastic Container Service (ECS), simplifying your development to production workflow.
	- Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure.
	- Amazon ECR hosts your images in a highly available and scalable architecture, allowing you to reliably deploy containers for your applications.
	- Integration with AWS Identity and Access Management (IAM) provides resource-level control of each repository.
	- With Amazon ECR, there are no upfront fees or commitments. You pay only for the amount of data you store in your repositories and data transferred to the Internet

- AWS Fargate

	- AWS Fargate is a compute engine for Amazon ECS that allows you to run containers without having to manage servers or clusters

- Amazon Elastic Container Service for Kubernetes (EKS)

	- makes it easy to deploy, manage, and scale containerized applications using Kubernetes on AWS.
	- Amazon EKS runs the Kubernetes management infrastructure for you across multiple AWS availability zones to eliminate a single point of failure.
	- Amazon EKS is certified Kubernetes conformant so you can use existing tooling and plugins from partners and the Kubernetes community.
	- Applications running on any standard Kubernetes environment are fully compatible and can be easily migrated to Amazon EKS.

### AWS Batch

- AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS.
- AWS Batch dynamically provisions the optimal quantity and type of compute resources (e.g., CPU or memory optimized instances) based on the volume and specific resource requirements of the batch jobs submitted.
- With AWS Batch, there is no need to install and manage batch computing software or server clusters that you use to run your jobs, allowing you to focus on analyzing results and solving problems.
- AWS Batch plans, schedules, and executes your batch computing workloads across the full range of AWS compute services and features, such as Amazon EC2 and Spot Instances.

### AWS Auto Scaling

- Provides the following Benefits

	- Better fault tolerance
	- Better availability
	- Scalability

- EC2 Autoscaling Groups

	- EC2 Auto Scaling helps you ensure that you have the correct number of EC2 instances available to handle the load for your application.
	- You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size.
	- You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size.
	- Scaling Cooldown

- Scaling Options

	- Scale based on demand
	- Scale based on a schedule
	- Manual scaling

- Auto Scaling policy

	- Metric
	- If auto Scaling group's scale up policy has not yet been reached., instances can reach 100% CPU Utilization without scaling up

- Tips

	- If your scaling events are not based on the right metrics and do not have the right threshold defined, then the scaling will not occur as you want it to happen.

### Tips

- The public IP address of an EC2 Instance is released after the instance is stopped and started
- The following would be considered important when considering the specification for the components of the application architecture

	- Determine the required I/O operations
	- Determining the MINIMUM MEMORY requirements for an application

## Networking & Content Delivery

### Cloud Front CDN

- Intro

	- Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers DATA, VIDEOS, APPLICATIONS, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
	- Can be used to deliver your entire website, including dynamic, static, streaming, and interactive content using a global network of edge locations.
	- Requests for your content are automatically routed to the nearestedge location, so content is delivered with the best possible

- Key Terminology

	- Edge Location
	- Distribution
	- Origin
	-  Tips

- A content delivery network (CDN) is a system of distributed servers (network) that deliver webpages and other web content to a user based on

	- the geographic locations of the user,
	- the origin of the webpage
	- content delivery server.

- Amazon CloudFront is optimized to work with other AWS Services i.e.

	- Amazon Web Services, like S3
	- Amazon Elastic Compute Cloud (Amazon EC2),
	- Amazon Elastic Load Balancing,
	- Amazon Route 53.
	- Amazon CloudFront also works seamlessly with any non-AWS origin server, which stores the original, definitive versions of your files.

- Origin Access Identity (OAI)

	- If you're using an Amazon S3 bucket as the origin for a CloudFront distribution, you can either allow everyone to have access to the files there, or you can restrict access using OAI

- Caching Content Based on Query String Parameters

	- Only supports Web distribution not RTMP
	- Parameter names & values used in query string are CASE SENSITIVE.
	- Its recommended to cache based upon parameters which has higher probability of returning different versions.

- Tips

	- Increase the cache expiration time to enhance performance

### VPC

- Intro

	- Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the Amazon Web Services (AWS) Cloud where you can launch AWS resources in a virtual network that you define.
	- For example, you can create a public-facing subnet for your webservers that has access to the Internet, and place your backend systems such as databases or application servers in a private- facing subnet with no Internet access.
	- You have complete control over your virtual networking environment, including
	- You can leverage multiple layers of security, including security groups and network access control lists, to help control access to Amazon EC2 instances in each subnet.
	- Additionally, you can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage the AWS cloud as an extension of your corporate datacenter.
	- A VPC spans all the Availability Zones in the region (Not multiple regions).
	- After creating a VPC, you can add one or more subnets in each Availability Zone.
	- What can you do with a VPC?
	- Default VPC vs Custom VPC

- Key Terminology

	- Subnets
	- Security Groups
	- Network ACLs
	- Network ACL vs Security Groups
	- Route Tables
	- CIDR

- VPC Peering

	- Intro
	- Multiple VPC Peering Connections
	- You cannot create a VPC peering connection between VPCs with matching or overlapping IPv4 CIDR blocks.

- VPC Endpoints

	- A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring:
	- Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.
	- Before VPC EndPoints
	- After VPC EndPoints

- VPC Flow Logs

	- VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC.
	- Flow log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs.
	- Flow logs can be created at 3 levels;
	- VPC Flow Logs  Tips

- AWS VPN CloudHub

	- You can securely communicate from one site to another using the AWS VPN CloudHub. The AWS VPN CloudHub operates on a simple hub-and-spoke model that you can use with or without a VPC.
	- Use this design if you have multiple branch offices and existing internet connections and would like to implement a convenient, potentially low cost hub-and-spoke model for primary or backup connectivity between these remote offices.
	- The following figure depicts the AWS VPN CloudHub architecture, with blue dashed lines indicating network traffic between remote sites being routed over their AWS VPN connections.

- Gateways

	- NAT Gateways
	- Bastion Hosts
	- Internet Gateways

- VPC  Tips

	- Think of a VPC as a logical datacenter in AWS.
	- Consists of
	- 1 Subnet = 1 Availability Zone
	- Statefulness
	- NO TRANSITIVE PEERING

### ELB

- Elastic Load Balancing automatically distributes incoming application traffic across multiple targets such as:

	- Amazon EC2 instances
	- Containers
	- IP addresses
	- Lambda functions.

- It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones.
- Health Checks

	- To discover the availability of your EC2 instances, a load balancer periodically sends pings, attempts connections, or sends requests to test the EC2 instances.
	- These tests are called health checks. The status of the instances that are healthy at the time of the health check is InService. The status of any instances that are unhealthy at the time of the health check is OutOfService.
	- The load balancer performs health checks on all registered instances, whether the instance is in a healthy state or an unhealthy state. The load balancer routes requests only to the healthy instances.
	- When the load balancer determines that an instance is unhealthy, it stops routing requests to that instance. The load balancer resumes routing requests to the instance when it has been restored to a healthy state.

- Types

	- Application Load Balancer
	- Network Load Balancer
	- Classic Load Balancer

- Tips

	- Attaching a Load Balancer to Your Auto Scaling Group
	- ELB needs to be placed in the public subnet to allow access from the Internet
	- ELB distributes incoming application traffic across multiple EC2 Instances in multiple Availability Zones NOT MULTIPLE REGIONS !
	- ELB is for FAULT TOLERANCE, but cannot help completely in disaster recovery for the EC2 Instances.
	- It can handle the varying load of your application traffic in a SINGLE AVAILABILITY ZONE or across MULTIPLE AVAILABILITY ZONES in one region and NOT across multiple regions.

### Route 53

- Intro

	- Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service.
	- It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other.

- Routing Policies

	- Failover Routing
	- Simple Routing
	- Weighted Routing
	- Latency-based Routing
	- Geolocation Routing
	- Multivalue Answer Routing

- Uses

	- Connects user requests to infrastructure running in AWS ï¿½ such as
	- You can use Amazon Route 53 to configure DNS HEALTH CHECKS to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints.
	- Amazon Route 53 Traffic Flow makes it easy for you to manage traffic globally through a variety of routing types, including Latency Based Routing, Geo DNS, Geoproximity, and Weighted Round Robinï¿½all of which can be combined with DNS Failover in order to enable a variety of low-latency, fault-tolerant architectures

- Notes

	- While ordinary Amazon Route 53 records are standard DNS records, alias records provide a Route 53ï¿½specific extension to DNS functionality.

### ELB vs Route53

- 1

	- In summary, I believe ELBs are intended to load balance across EC2 instances in a 'single' region.
	- Whereas DNS load-balancing (Route 53) is intended to help balance traffic 'across' regions. Route53 policies like geolocation may help direct traffic to preferred regions, then ELBs route between instances within one region.
	- another difference is that DNS-based routing (e.g. Route 53) only changes the address that your clients' requests resolve to. On the other hand, an ELB actually reroutes traffic.

### API Gateway

- Intro

	- Amazon API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale.
	- With a few clicks in the AWS Management Console, you can create an API that acts as a "front door" for applications to access data, business logic, or functionality from your back-end services, such as

- APIs Caching

	- You can enable API caching in Amazon API Gateway to cache your endpoint's response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your API.
	- When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint.

- Features

	- Low Cost & Efficient
	- Scales Effortlessly
	- You can Throttle Requests to prevent attacks
	- Connect to CloudWatch to log all requests

- Cross Origin Resource Sharing (CORS)

	- Is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.
	- is a security feature of modern web browsers. It enables web browsers to negotiate which domains can make requests of external websites or services.
	- Only these methods are supported: GET, PUT, POST, DELETE, HEAD

### IP Addresses

- Elastic IP Addresses

	- An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
	- is reachable from the internet. If your instance does not have a public IPv4 address, you can associate an Elastic IP address with your instance to enable communication with the internet; for example, to connect to your instance from your local computer.

- Private IPv4 Addresses

	- A private IPv4 address is an IP address that's not reachable over the Internet. You can use private IPv4 addresses for communication between instances in the same VPC.

- Public IPv4 Addresses

	- A public IP address is an IPv4 address that's reachable from the Internet. You can use public addresses for communication between your instances and the Internet.

### Site-to-Site VPN VPN Connection

- Intro

	- Although the term VPN connection is a general term, in the documentation, a VPN connection refers to the connection between your VPC and your own on-premises network.
	- You can enable access to your remote network from your VPC by

- Components

	- Virtual Private Gateway (VPG)
	- Customer Gateway

- Key Terminology

	- Border Gateway Protocol (BGP)
	- Autonomous System Number (ASN)

- Data can be encrypted in transit, in contrast to Direct Connect which does not allow data encryption

### AWS Direct Connect

- Intro

	- AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection (THAT DOES NOT INVOLVE INTERNET) from your premises to AWS.
	- AWS Direct Connect is a network service that provides an alternative to using the Internet to connect customer's on premise sites to AWS.
	- Using AWS Direct Connect, you can establish private connectivity between AWS and your datacenter, office, or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connections.

- Benefits

	- Reduces Your Bandwidth Costs
	- Consistent Network Performance
	- Compatible with All Aws Services
	- Private Connectivity to Your Amazon Vpc
	- Elastic and Simple

- Does not encrypt traffic in connections between AWS VPCï¿½s and the On-premises network

### AWS PrivateLink

- AWS PrivateLink simplifies the security of data shared with cloud-based applications by eliminating the exposure of data to the public Internet.
- AWS PrivateLink provides private connectivity between VPCs, AWS services, and on-premises applications, securely on the Amazon network.
- AWS PrivateLink makes it easy to connect services across different accounts and VPCs to significantly simplify the network architecture.

### DNS

- Key Terminology

	- SOA Records
	- Domain Registrars
	- NS Records
	- A Records
	- CNAMES
	- Alias Records
	- TTL

-  Tips

	- ELBs do not have pre-defined IPv4 addresses; you resolve to them using a DNS name.
	- Understand the difference between an Alias Record and a CNAME.
	- Given the choice, always choose an Alias Record over a CNAME.
	- Common DNS Types

## Databases

### Amazon RDS

- Intro

	- Amazon Relational Database Service (RDS) makes it easy to set up, operate, and scale a relational database in the cloud.
	- It provides cost-efficient and resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching and backups.
	- It frees you to focus on your applications so you can give them the fast performance, high availability, security and compatibility they need.

- Amazon RDS database engines

	- SQL Server
	- Oracle
	- PostgreSQL
	- MySQL
	- Aurora
	- MariaDB

- RDS Multi-AZ

	- Intro
	- Multi-AZ Databases
	- Tips

- Read Replicas

	- Intro
	- Read Replica Databases
	- Notes

- DB Parameter Group

	- You manage your DB engine configuration through the use of parameters in a DB parameter group .
	- DB parameter groups act as a container for engine configuration values that are applied to one or more DB instances.
	- A default DB parameter group is created if you create a DB instance without specifying a customer-created DB parameter group.
	- Each default DB parameter group contains database engine defaults and Amazon RDS system defaults based on the engine, compute class, and allocated storage of the instance.
	- You cannot modify the parameter settings of a default DB parameter group; you must create your own DB parameter group to change parameter settings from their default value.
	- Note that not all DB engine parameters can be changed in a customer-created DB parameter group.

- Automated Backups

	- You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots.
	- Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved.
	- This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data.
	- When you delete a snapshot, only the data unique to that snapshot is removed. Each snapshot contains all of the information needed to restore your data (from the moment when the snapshot was taken) to a new EBS volume.
	- Disabling automated backups disables point-in-time recovery. If you disable and then re-enable automated backups, you are only able to restore starting from the time you re-enabled automated backups.

- Tips

	- Supports up to 16 TB of storage.
	- RDS is a transactional database works based on the OLTP, it's not intended to store analytical data coming out of Kinesis.
	- RDS Encryption

### Self Managed DB

- In contrast to RDS, is self managed DB installed on EC2
- Don't have the following features RDS features

	- Read Replicas
	- RDS Mulit-AZ

### DynamoDB

- Intro

	- Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale.
	- It is a fully managed database and supports both document and key-value data models.
	- Its flexible data model and reliable performance make it a great fit for
	- Stored on SSD storage
	- Spread Across 3 geographically distinct data centres

- Consistent Reads Types

	- Strongly Consistent Reads
	- Eventual Consistent Reads

- Pricing

	- Provisioned Throughput Capacity
	- Storage costs of $0.25Gb per month.

- Capturing Table Activity with DynamoDB Stream

	- DynamoDB Streams enables solutions such as these, and many others. DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table, and stores this information in a log for up to 24 hours.
	- Many applications can benefit from the ability to capture changes to items stored in a DynamoDB table, at the point in time when such changes occur.
	- ple use cases:

- DynamoDB Auto Scaling

	- DynamoDB auto scaling uses the AWS Application Auto Scaling service to dynamically adjust provisioned throughput capacity on your behalf, in response to actual traffic patterns.
	- This enables a table or a global secondary index to increase its provisioned read and write capacity to handle sudden increases in traffic, without throttling.
	- When the workload decreases, Application Auto Scaling decreases the throughput so that you don't pay for unused provisioned capacity.

- Tips

	- Amazon DynamoDB is schema-less, in that the data items in a table need not have the same attributes or even the same number of attributes.
	- The maximum item size in DynamoDB is 400KB.
	- Use Cases

- Partition Key

	- A simple primary key, composed of one attribute known as the partition key.
	- Recommendations for partition-keys

### Redshift

- Intro

	- Amazon Redshift is a fast and powerful, fully managed, petabyte-scale data warehouse service in the cloud.
	- Customers can start small for just $0.25 per hour with no commitments or upfront costs and scale to a petabyte or more for $1,000 per terabyte per year, less than a tenth of most other data warehousing solutions.

- Redshift Configuration

	- Single Node (160Gb)
	- Multi-Node (Cluster)
	- Tips

- Features

	- Faster
	- Massively Parallel Processing (MPP)
	- Advanced Compression
	- Redshift Availability
	- Security

- Pricing

	- Compute Node Hours
	- Backup
	- Data transfer (only within a VPC, not outside it)

- Amazon Redshift Enhanced VPC Routing

	- By using Enhanced VPC Routing, you can use standard VPC features, such as
	- You use these features to tightly manage the flow of data between your Amazon Redshift cluster and other resources.
	- When you use Enhanced VPC Routing to route traffic through your VPC, you can also use VPC flow logs to monitor COPY and UNLOAD traffic.

- Snapshots

	- You can take a manual snapshot any time. By default, manual snapshots are retained indefinitely, even after you delete your cluster. You can specify the retention period when you create a manual snapshot, or you can change the retention period by modifying the snapshot.
	- Manual snapshots are retained even after you delete your cluster. Because manual snapshots accrue storage charges, itï¿½s important that you manually delete them if you no longer need them.
	- Cross-Region Snapshot

- Tips

	- Redshift is not designed for high workloads. If you expect a high concurrency workload that generally involves reading and writing all of the columns for a small number of records at a Amazon RDS or Amazon, DynamoDB

### Elasticache

- Intro

	- ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud.
	- The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in- memory caches, instead of relying entirely on slower disk-based databases.
	- Amazon ElastiCache can be used to significantly improve latency and throughput for many READ-HEAVY application workloads (such as social networking, gaming, media sharing and Q&A portals) or compute- intensive workloads (such as a recommendation engine).
	- Caching improves application performance by storing critical pieces of data in memory for low-latency access.
	- Cached information may include the results of I/O intensive database queries or the results of computationally-intensive calculations.

- Types of Elasticache

	- Memcached
	- Redis

- Elasticache  Tips

	- Typically you will be given a scenario where a particular database is under a lot of stress/load.
	- Redshift is a good answer if the reason your database is feeling stress is because management keep runnin OLAP transactions on it etc.
	- You may be asked which service you should use to alleviate this.
	- Elasticache is a good choice if your database is particularly read heavy and not prone to frequent changing.

- Use Cases

	- Can be used in front of a database to cache the common queries issued against the database. This can reduce the overall load on the database.
	- Real-time transactions,
	- Chat
	- Cache
	- Session store
	- Bl and analytics
	- Gaming leaderboards

### Aurora

- Intro

	- Amazon Aurora (Aurora) is a fully managed relational database engine that's compatible with MySQL and PostgreSQL. it combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases.
	- Aurora can deliver up to five times the throughput of MySQL and up to three times the throughput of PostgreSQL without requiring changes to most of your existing applications.
	- Aurora has Read Replicas and Multi AZ features

- Aurora Scaling

	- Start with 10 GB, Scales in 10 GB increments to 64TB (Storage Autoscaling)
	- Compute resources can scale up to
	- 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones. 6 copies of your data.
	- Aurora is designed to transparently handle the loss of up to
	- Aurora storage is also self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.

- Aurora Replicas

	- 2 Types of Replicas are available.

- Tips

	- Aurora does support Schema changes.
	- Aurora supports up to 64TB of data.

### Automated Backups

- There are two different types of Backups for AWS

	- Automated Backups
	- Database Snapshots.

- Restoring Backups

	- Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.

- Encryption

	- Encryption at rest is supported for
	- Encryption is done using the AWS Key Management Service (KMS) service.
	- Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas, and snapshots.
	- Encrypting Existing DB Instance

### Amazon EMR (Bigdata)

- Easily Run and Scale Apache Spark, Hadoop, HBase, Presto, Hive, and other Big Data Frameworks
- Amazon EMR provides a managed Hadoop framework that makes it easy, fast, and cost-effective to process vast amounts of data across dynamically scalable Amazon EC2 instances.
- You can also run other popular distributed frameworks such as Apache Spark, HBase, Presto, and Flink in EMR,
- Use cases

	- Clickstream Analysis
	- Real-Time Analytics
	- Log Analysis
	- Extract Transform Load (ETL)
	- Predictive Analytics
	- Genomics

- EMR is not for receiving the real time data from thousands of sources, EMR is mainly used for Hadoop ecosystem based data used for Big data analysis.

### Tips

- If you expect a high concurrency workload that generally involves reading and writing all of the columns for a small number of records at a time you should instead consider using Amazon RDS or Amazon DynamoDB
- DynamoDB vs RDS

	- DynamoDB offers "push button" scaling, meaning that you can scale your database on the fly, without any down time.
	- RDS is not so easy and you usually have to use a bigger instance size or to add a read replica.

## Analytics & Search

### Kinesis

- Intro

	- Amazon Kinesis is a platform on AWS to send your streaming data to.
	- Kinesis makes it easy to load and analyze streaming data, and also providing the ability for you to build your own custom applications for you business needs.

- Key Terminology

	- Producer
	- Consumer

- What is streaming data

	- Streaming Data is data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes (order of Kilobytes).
	- ples

- Kinesis Services

	- Kinesis Data Streams (KDS)
	- Kinesis Firehose
	- Kinesis Analytics

-  Tips

	- Know the difference between Kinesis Streams and Kinesis Firehose. You will be given scenario questions and you must choose the most relevant service.
	- Understand what Kinesis Analytics is.

- Kinesis Streams vs Kinesis Firehose

	- Amazon Kinesis Data Firehose can send data to: Amazon S3 Amazon Redshift Amazon Elasticsearch Service Splunk To do the same thing with Amazon Kinesis Data Streams, you would need to write an application that consumes data from the stream and then connects to the destination to store data. So, think of Firehose as a pre-configured streaming application with a few specific options. Anything outside of those options would require you to write your own code.

- Use Cases

	- Build video analytics applications
	- Evolve from Batch to Real-time Analytics
	- Build Real-time Applications
	- Analyze IoT device data

- Interface VPC Endpoints

	- You can use an interface VPC endpoint to keep traffic between your Amazon VPC and Kinesis Data Streams from leaving the Amazon network.
	- Interface VPC endpoints don't require an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
	- Interface VPC endpoints are powered by AWS PrivateLink, an AWS technology that enables private communication between AWS services using an elastic network interface with private IPs in your Amazon VPC

### Amazon QuickSight

- Amazon QuickSight is a fast, cloud-powered business intelligence service that makes it easy to deliver insights to everyone in your organization.
- As a fully managed service, QuickSight lets you easily create and publish interactive dashboards that include ML Insights.
- Dashboards can then be accessed from any device, and embedded into your applications, portals, and websites.
- With our Pay-per-Session pricing, QuickSight allows you to give everyone access to the data they need, while only paying for what you use.

### AWS Glue (ETL)

- AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics. You can create and run an ETL job with a few clicks in the AWS Management Console.
- You simply point AWS Glue to your data stored on AWS, and AWS Glue discovers your data and stores the associated metadata (e.g. table definition and schema) in the AWS Glue Data Catalog. Once cataloged, your data is immediately searchable, queryable, and available for ETL.
- Glue Data Catalog

	- The AWS Glue Data Catalog contains references to data that is used as sources and targets of your extract, transform, and load (ETL) jobs in AWS Glue. To create your data warehouse, you must catalog this data.
	- The AWS Glue Data Catalog is an index to the location, schema, and runtime metrics of your data. You use the information in the Data Catalog to create and monitor your ETL jobs.
	- Typically, you run a crawler to take inventory of the data in your data stores, but there are other ways to add metadata tables into your Data Catalog.

- Job Bookmarks

	- AWS Glue tracks data that has already been processed during a previous run of an ETL job by persisting state information from the job run. This persisted state information is called a job bookmark.
	- Job bookmarks help AWS Glue maintain state information and prevent the reprocessing of old data. With job bookmarks, you can process new data when rerunning on a scheduled interval.

### Amazon Athena (SQL, S3)

- Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.
- Athena is easy to use. Simply point to your data in Amazon S3, define the schema, and start querying using standard SQL. Most results are delivered within seconds. With Athena, thereï¿½s no need for complex ETL jobs to prepare your data for analysis. This makes it easy for anyone with SQL skills to quickly analyze large-scale datasets.
- pricing

	- With Amazon Athena, you only pay for the queries that you run. You are charged based on the amount of data scanned by each query. You can get significant cost savings and performance gains by compressing, partitioning, or converting your data to a columnar format, because each of those operations reduces the amount of data that Athena needs to scan to execute a query.

### Amazon Elasticsearch

- Amazon Elasticsearch Service is a fully managed service that makes it easy for you to deploy, secure, and operate Elasticsearch at scale with zero down time.
- The service offers open-source Elasticsearch APIs,

### Amazon CloudSearch

- Amazon CloudSearch is a managed service in the AWS Cloud that makes it simple and cost-effective to set up, manage, and scale a search solution for your website or application.

## Desktop & App Streaming

### Amazon AppStream 2.0

- Amazon AppStream 2.0 is a fully managed application streaming service. You centrally manage your desktop applications on AppStream 2.0 and securely deliver them to any computer. You can easily scale to any number of users across the globe without acquiring, provisioning, and operating hardware or infrastructure. AppStream 2.0 is built on AWS, so you benefit from a data center and network architecture designed for the most security-sensitive organizations. Each user has a fluid and responsive experience with your applications, including GPU-intensive 3D design and engineering ones, because your applications run on virtual machines (VMs) optimized for specific use cases and each streaming session automatically adjusts to network conditions.

### AWS Workspaces

- Amazon WorkSpaces is a managed, secure cloud desktop service. You can use Amazon WorkSpaces to provision either Windows or Linux desktops in just a few minutes and quickly scale to provide thousands of desktops to workers across the globe.
- You can pay either monthly or hourly, just for the WorkSpaces you launch, which helps you save money when compared to traditional desktops and on-premises VDI solutions. Amazon WorkSpaces helps you eliminate the complexity in managing hardware inventory, OS versions and patches, and Virtual Desktop Infrastructure (VDI), which helps simplify your desktop delivery strategy.
- With Amazon WorkSpaces, your users get a fast, responsive desktop of their choice that they can access anywhere, anytime, from any supported device.

### Amazon WorkMail

- Amazon WorkMail is a secure, managed business email and calendar service with support for existing desktop and mobile email client applications.
- Amazon WorkMail gives users the ability to seamlessly access their eMAIL, CONTACTS, and CALENDARS using the client application of their choice, including:

	- Microsoft Outlook,
	- native iOS and Android email applications,
	- any client application supporting the IMAP protocol,
	- or directly through a web browser.

### Amazon WorkDocs

- Intro

	- Amazon WorkDocs is a fully managed, secure content creation, storage, and collaboration service.
	- With Amazon WorkDocs, you can easily create, edit, and share content, and because itï¿½s stored centrally on AWS, access it from anywhere on any device.
	- Amazon WorkDocs makes it easy to collaborate with others, and lets you:
	- You can use Amazon WorkDocs to retire legacy file share infrastructure by moving file shares to the cloud.
	- Amazon WorkDocs lets you integrate with your existing systems, and offers a rich API so that you can develop your own content-rich applications. Amazon WorkDocs is built on AWS, where your content is secured on the world's largest cloud infrastructure.

- Managing Security Settings

	- To restrict all users to invite external users & to share WorkDoc links publicly, you can create a Power user who will be responsible to perform this activity.

## Monitoring and Auditing

### AWS Config

- AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources.
- Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations.
- With Config, you can achieve the followings:

	- You can review changes in configurations and relationships between AWS resources,
	- Dive into detailed resource configuration histories,
	- Determine your overall compliance against the configurations specified in your internal guidelines.

- This enables you to simplify compliance auditing, security analysis, change management, and operational troubleshooting.

### AWS CloudTrail

- Intro

	- AWS CloudTrail is a service that enables governance, compliance, operational and risk auditing of your AWS account.
	- With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.
	- CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services.
	- This event history simplifies security analysis, resource change tracking, and troubleshooting.

- Use cases

	- Operational Issue Troubleshooting
	- Data Exfiltration
	- Compliance Aid
	- Security Analysis

- Track user activity and API usage

	- CloudTrail is a web service that records AWS API calls for your AWS account and delivers log files to an Amazon S3 bucket.
	- The recorded information includes the identity of the user, the start time of the AWS API call, the source IP address, the request parameters, and the response elements returned by the service.

- Logs Encryption

	- By default, the log files delivered by CloudTrail to your bucket are encrypted by Amazon server-side encryption with Amazon S3-managed encryption keys (SSE-S3). To provide a security layer that is directly manageable, you can instead use server-side encryption with AWS KMSï¿½managed keys (SSE-KMS) for your CloudTrail log files.

- Validating CloudTrail Log File Integrity

	- To determine whether a log file was modified, deleted, or unchanged after CloudTrail delivered it, you can use CloudTrail log file integrity validation.
	- This feature is built using industry standard algorithms: SHA-256 for hashing and SHA-256 with RSA for digital signing.
	- This makes it computationally infeasible to modify, delete or forge CloudTrail log files without detection.

- Changes to Global Service Event logs can be done via AWS CLI not AWS console

### AWS CloudWatch

- Intro

	- Amazon CloudWatch is a monitoring and management service built for developers, system operators, site reliability engineers (SRE), and IT managers.
	- CloudWatch provides you with data and actionable insights to monitor your applications, understand and respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health.

- How it works
- Use Cases

	- Infrastructure monitoring and troubleshooting
	- Resource optimization
	- Application monitoring
	- Log analytics

- Alarms

	- You can create a CloudWatch alarm that watches a single CloudWatch metric or the result of a math expression based on CloudWatch metrics.
	- The alarm performs one or more actions based on the value of the metric or expression relative to a threshold over a number of time periods.
	- The action can be an Amazon EC2 action, an Amazon EC2 Auto Scaling action, or a notification sent to an Amazon SNS topic.

- Events

	- Amazon CloudWatch Events delivers a near real-time stream of system events that describe changes in Amazon Web Services (AWS) resources.
	- Using simple rules that you can quickly set up, you can match events and route them to one or more target functions or streams.
	- CloudWatch Events becomes aware of operational changes as they occur. CloudWatch Events responds to these operational changes and takes corrective action as necessary, by sending messages to respond to the environment, activating functions, making changes, and capturing state information.
	- ple
	- You can configure the following AWS services as targets for CloudWatch Events:

- Rules

	- A rule matches incoming events and routes them to targets for processing. A single rule can route to multiple targets, all of which are processed in parallel. Rules are not processed in a particular order. This enables different parts of an organization to look for and process the events that are of interest to them. A rule can customize the JSON sent to the target, by passing only certain parts or by overwriting it with a constant.

- Targets

	- A target processes events. Targets can include Amazon EC2 instances, AWS Lambda functions, Kinesis streams, Amazon ECS tasks, Step Functions state machines, Amazon SNS topics, Amazon SQS queues, and built-in targets. A target receives events in JSON format.

- Metrics

	- A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor, and the data points as representing the values of that variable over time. For example, the CPU usage of a particular EC2 instance is one metric provided by Amazon EC2. The data points themselves can come from any application or business activity from which you collect data.
	- AWS services send metrics to CloudWatch, and you can send your own custom metrics to CloudWatch. You can add the data points in any order, and at any rate you choose. You can retrieve statistics about those data points as an ordered set of time-series data.
	- Metrics exist only in the region in which they are created.

### CloudTrail vs CloudWatch

- CloudTrail

	- CloudTrail is just used to audit changes to services.
	- How did an unauthorized user gain access to an S3 bucket?

- CloudWatch

	- CloudWatch is mostly used to monitor operational health and performance,
	- Can also provide automation via Rules which respond to state changes
	- ples

### Amazon Inspector

- Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS.
- Amazon Inspector automatically assesses applications for exposure, vulnerabilities, and deviations from best practices.
- After performing an assessment, Amazon Inspector produces a detailed list of security findings prioritized by level of severity. These findings can be reviewed directly or as part of detailed assessment reports which are available via the Amazon Inspector console or API.

### AWS X-Ray

- Intro

	- AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture.
	- With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors.
	- X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your applicationï¿½s underlying components.
	- You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of services.

- Sampling

	- To ensure efficient tracing and provide a representative sample of the requests that your application serves, the X-Ray SDK applies a sampling algorithm to determine which requests get traced.
	- By default, the X-Ray SDK records the first request each second, and five percent of any additional requests.
	- To avoid incurring service charges when you are getting started, the default sampling rate is conservative. You can configure X-Ray to modify the default sampling rule and configure additional rules that apply sampling based on properties of the service or request.

## Application Integration

### SQS

- Intro

	- Amazon SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them.
	- Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.
	- Using Amazon SQS, you can decouple the components of an application so they run independently, easing message management between components.
	- Any component of a distributed application can store messages in the queue. Messages can contain up to 256 KB of text in any format. Any component can later retrieve the messages programmatically using the Amazon SQS API.
	- The queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.

- Types

	- Standard Queues (default)
	- FIFO Queues (First-in-First-out)

- SQS Key Facts

	- SQS is pull-based, not pushed-based
	- Messages are 256 KB in size
	- SQS guarantees that your messages will be processed at least once.
	- Messages can be kept in the queue from 1 minute to 14 days
	- Default retention period is 4 days

- SQS Visibility Timeout

	- The Visibility Timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that message.
	- Provided the job is processed before the visibility time out expires, the message will then be deleted from the queue.
	- If the job is not processed within that time the message will become visible again and another reader will process it. This could result in the same message being delivered twice.
	- Default Visibility Timeout is 30 seconds
	- Increase it if your task takes >30 seconds
	- Maximum is 12 hours

- Message Group ID

	- Message which are part of a specific message group will be processed in a strict orderly manner using Message group ID. This message group ID helps to process messages by multiples consumers in FIFO manner while keeping session data of each trade initiated by users..

- Deduplication ID

	- The message deduplication ID is the token used for deduplication of sent messages.
	- If a message with a particular message deduplication ID is sent successfully, any messages sent with the same message deduplication ID are accepted successfully but aren't delivered during the 5-minute deduplication interval.

- Tips

	- The ideal approach is to scale the instances based on the size of queue.

- Polling Types

	- Long Polling
	- Short Polling

-  Tips

	- SQS is a distributed message queueing system
	- Allows you to decouple the components of an application so that they are independent
	- Pull-based, not push-based
	- Standard Queues (default) - best-effort ordering; message delivered at least once
	- FIFO Queues (First In First Out) - ordering strictly preserved, message delivered once, no duplicates. e.g. good for banking transactions which need to happen in strict order

### SWF

- Intro

	- Amazon Simple Workflow Service (Amazon SWF) is a web service that makes it easy to coordinate work across distributed application components.
	- Amazon SWF enables applications for a range of use cases, including
	- Tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.
	- Maximum Workflow can be 1 year and the value is always measured in seconds.

- SWF Workers

	- Workers are programs that interact with Amazon SWF to get tasks, process received tasks, and return the results.

- SWF Decider

	- The decider is a program that controls the coordination of tasks, i.e. their ordering, concurrency and scheduling according to the application logic.

- SWF Workers & Deciders

	- The workers and the decider can run on cloud infrastructure, such as Amazon EC2, or on machines behind firewalls. Amazon SWF brokers the interactions between workers and the decider. It allows the decider to get consistent views into the progress of tasks and to initiate new tasks in an ongoing mannen.
	- At the same time, Amazon SWF stores tasks, assigns them to workers when they are ready, and monitors their progress. It ensures that a task is assigned only once and is never duplicated. Since Amazon SWF maintains the application's state durably, workers and deciders don't have to keep track of execution state. They can run independently, and scale quickly.

- SWF Domains

	- Your workflow and activity types and the workflow execution itself are all scoped to a domain.
	- Domains isolate a set of types, executions, and task lists from others within the same account.
	- You can register a domain by using the AWS Management Console or by using the RegisterDomain action in the Amazon SWF API.

- SWF vs SQS

	- Amazon SWF presents a task-oriented API, whereas Amazon SQS offers a message-oriented API.
	- Amazon SWF ensures that a task is assigned only once and is never duplicated. With Amazon SQS, you need to handle duplicated messages and may also need to ensure that a message is processed only once.
	- Amazon SWF keeps track of all the tasks and events in an application. With Amazon SQS, you need to implement your own application-level tracking, especially if your application uses multiple queues.

### SNS

- Intro

	- Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud.
	- It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.
	- Push Provides instantaneous, push-based delivery (no polling) notifications to
	- Amazon SNS can also deliver notifications by SMS text message or email, to

- SNS vs SQS

	- Both Messaging Services in AWS
	- SNS - Push
	- SQS - Polls (Pulls)

- SNS Pricing

	- Users pay $0.50 per 1 million Amazon SNS
	- $0.06 per 100,000 Notification deliveries over HTTP
	- $0.75 per 100 Notification deliveries over SMS
	- $2.00 per 100,000 Notification deliveries over Email

- SNS Topics

	- Amazon SNS provides topics for high-throughput, push-based, many-to-many messaging. Using Amazon SNS topics, your publisher systems can fan out messages to a large number of subscriber endpoints for parallel processing
	- SNS allows you to group multiple recipients using topics.
	- A topic is an "access point" for allowing recipients to dynamically subscribe for identical copies of the same notification.
	- One topic can support deliveries to multiple endpoint types for example, you can group together iOS, Android and SMS recipients.
	- When you publish once to a topic, SNS delivers appropriately formatted copies of your message to each subscriber.
	- To prevent messages from being lost, all messages published to Amazon SNS are stored redundantly across multiple availability zones.

## Developer Tools

### AWS CodeBuild

- AWS CodeBuild is a fully managed CONTINUOUS INTEGRATION service that compiles source code, runs tests, and produces software packages that are ready to deploy.
- With CodeBuild, you donï¿½t need to provision, manage, and scale your own build servers.
- CodeBuild scales continuously and processes multiple builds concurrently, so your builds are not left waiting in a queue.
- You can get started quickly by using prepackaged build environments, or you can create custom build environments that use your own build tools.
- With CodeBuild, you are charged by the minute for the compute resources you use.

### AWS CodeDeploy

- AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as

	- Amazon EC2
	- AWS Fargate
	- On-premises servers
	- AWS Lambda

- AWS CodeDeploy makes it easier for you to rapidly release new features, helps you avoid downtime during application deployment, and handles the complexity of updating your applications.
- You can use AWS CodeDeploy to automate software deployments, eliminating the need for error-prone manual operations.
- The service scales to match your deployment needs.

### AWS CodePipeline

- Automate continuous delivery pipelines for fast and reliable updates
- AWS CodePipeline is a fully managed CONTINUOUS DELIVERY service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.
- CodePipeline automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define. This enables you to rapidly and reliably deliver features and updates.
- You can easily integrate AWS CodePipeline with third-party services such as GitHub or with your own custom plugin. With AWS CodePipeline, you only pay for what you use. There are no upfront fees or long-term commitments.

### Blue-Green Deployment on AWS

- This Quick Start automatically deploys a blue-green architecture on AWS using AWS CodePipeline. It creates a continuous integration/continuous deployment (CI/CD) pipeline in about 15 minutes.
- When an application is developed and deployed to an AWS Elastic Beanstalk environment, having two separate, but identical, environmentsï¿½blue and greenï¿½increases availability and reduces risk.
- In this Quick Start architecture, the blue environment is the production environment that normally handles live traffic. The CI/CD pipeline architecture creates a clone (green) of the live Elastic Beanstalk environment (blue). The pipeline then swaps the URLs between the two environments.

## Management Tools

### AWS Management Console

- Provides Everything you need to access and manage the AWS cloud ï¿½ in one web interface.
- The AWS Management Console* brings the unmatched breadth and depth of AWS right to your computer or mobile phone with a secure, easy-to-access, web-based portal. Discover new services, manage your entire account, build new applications, and learn how to do even more with AWS.

### AWS Command Line Interface

- The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

## Media Services

### Elastic Transcoder

- Media Transcoder in the cloud.
- Convert media files from their original source format in to different formats that will play on smartphones, tablets, PC's etc.
- Provides transcoding presets for popular output formats, which means that you don't need to guess about which settings work best on particular devices.
- Pay based on the minutes that you transcode and the resolution at which you transcode.

### Amazon Polly

- Amazon Polly is a service that turns text into lifelike speech, allowing you to create applications that talk, and build entirely new categories of speech-enabled products.
- Amazon Polly is a Text-to-Speech service that uses advanced deep learning technologies to synthesize speech that sounds like a human voice.
- Lexicons

	- Pronunciation lexicons enable you to customize the pronunciation of words. Amazon Polly provides API operations that you can use to store lexicons in an AWS region.
	- Lexicons are specific to a region. You will need to upload Lexicon in each region where you need to use. For a single text which appears multiple times in a content, you can create alias using multiple Lexicons to have different speech.

- SSML tags

	- Convert commas in content into period.
	- Add a pause using <break> SSML tag between appropriate words & paragraphs.
	- Add a <emphasis> tag as ï¿½Strongï¿½ for appropriate words & paragraphs.

## Migration Services

### AWS Server Migration Service (SMS)

- AWS Server Migration Service (SMS) is an agentless service which makes it easier and faster for you to migrate thousands of on-premises workloads to AWS.
- AWS SMS allows you to automate, schedule, and track incremental replications of live server volumes, making it easier for you to coordinate large-scale server migrations.

### VM Import/Export

- VM Import/Export enables you to easily import virtual machine images from your existing environment to Amazon EC2 instances and export them back to your on-premises environment.

### Snowball

- Intro

	- AWS Import/Export Disk accelerates moving large amounts of data into and out of the AWS cloud using portable storage devices for transport.
	- Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of AWS.
	- Using Snowball addresses common challenges with large-scale data transfers including high network costs, long transfer times, and security concerns.
	- Transferring data with Snowball is simple, fast, secure, and can be as little as one-fifth the cost of high-speed Internet.
	- 80TB snowball in all regions.
	- Snowball uses multiple layers of security designed to protect your data including tamper-resistant enclosures, 256-bit encryption, and an industry-standard Trusted Platform Module (TPM) designed to ensure both security and full chain-of-custody of your data.
	- Once the data transfer job has been processed and verified, AWS performs a software erasure of the Snowball appliance.

- Types Of Snowballs

	- Snowball
	- Snowball Edge
	- Snowmobile

- Use Cases

	- Cloud migration
	- Disaster recovery
	- Datacenter decommission
	- Content distribution

### AWS Direct Connect

## AWS Billing

### AWS Organizations

- Using AWS Organizations, you can automate account creation, create groups of accounts to reflect your business needs, and apply policies for these groups for governance.
- You can also simplify billing by setting up a single payment method for all of your AWS accounts.
- Through integrations with other AWS services, you can use Organizations to define central configurations and resource sharing across accounts in your organization. AWS Organizations is available to all AWS customers at no additional charge.
- Service Control Policies

	- Service control policies (SCPs) are one type of policy that you can use to manage your organization. SCPs offer central control over the maximum available permissions for all accounts in your organization, allowing you to ensure your accounts stay within your organizationï¿½s access control guidelines. SCPs are available only in an organization that has all features enabled. SCPs aren't available if your organization has enabled only the consolidated billing features
	- For example, you can apply service control policies (SCPs) across multiple AWS accounts that are members of an organization. SCPs allow you to define which AWS service APIs can and cannot be executed by AWS Identity and Access Management (IAM) entities (such as IAM users and roles) in your organizationï¿½s member AWS accounts. SCPs are created and applied from the master account, which is the AWS account that you used when you created your organization.

- Consolidated Billing for Organizations

	- You can use the consolidated billing feature in AWS Organizations to consolidate billing and payment for multiple AWS accounts or multiple Amazon Internet Services Pvt. Ltd (AISPL) accounts. Every organization in AWS Organizations has a master account that pays the charges of all the member accounts.
	- Consolidated billing has the following benefits:
	- Volume Discounts

### AWS Budgets

- AWS Budgets gives you the ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount.
- You can also use AWS Budgets to set RI utilization or coverage targets and receive alerts when your utilization drops below the threshold you define.
- RI alerts support Amazon EC2, Amazon RDS, Amazon Redshift, and Amazon ElastiCache reservations.

## The Well Architected Framework

### Best Practices

- Business Benefits of Cloud

	- Almost zero upfront infrastructure investment
	- Just-in-time Infrastructure
	- More efficient resource utilization
	- Usage-based costing
	- Reduced time to market

- Technical Benefits of Cloud

	- Automation ï¿½ "Scriptable infrastructure"
	- Auto-scaling
	- Proactive Scaling
	- More Efficient Development lifecycle
	- Improved Testability
	- Disaster Recovery and Business Continuity
	- "Overflow" the traffic to the cloud

- Understanding Elasticity
- Design For Failure

	- Rule of thumb: Be a pessimist when designing architectures in the cloud; assume things will fail. In other words, always design, implement and deploy for automated recovery from failure.
	- In particular, assume that your hardware will fail. Assume that outages will occur.
	- Assume that some disaster will strike your application.
	- Assume that you will be slammed with more than the expected number of requests per second some day.
	- Assume that with time your application software will fail too.
	- By being a pessimist, you end up thinking about recovery strategies during design time, which helps in designing an overall system better.

- Decouple Your Components

	- The key is to build components that do not have tight dependencies on each other, so that if one component were to die (fail), sleep (not respond) or remain busy (slow to respond) for some reason, the other components in the system are built so as to continue to work as if no failure is happening.
	- In essence, loose coupling isolates the various layers and components of your application so that each component interacts asynchronously with the others and treats them as a "black box".
	- For example, in the case of web application architecture, you can isolate the app server from the web server and from the database. The app server does not know about your web server and vice versa, this gives decoupling between these layers and there are no dependencies code-wise or functional perspectives. In the case of batch- processing architecture, you can create asynchronous components that are independent of each other.

- Implement Elasticity

	- The cloud brings a new concept of elasticity in your applications.
	- Elasticity can be implemented in three ways:

- Secure Your Application

### General Design Principles

- Stop guessing your capacity needs
- Test systems at production scale
- Automate to make architectural experimentation easier
- Allow for evolutionary architectures
- Data-Driven architectures
- Improve through game days

### The 5 Pillars of the Well-Architected Framework

- Security

	- Design Principles
	- Key Terminology
	- Best Practices
	- Key AWS Services
	-  Tips

- Reliability

	- Intro
	- Design Principles
	- Definition
	- Best Practices
	- Key AWS Services

- Performance Efficiency

	- Intro
	- Design Principles
	- Definition
	- Best Practices
	- Key AWS Services
	-  Tips

- Cost Optimization

	- Intro
	- Design Principles
	- Definition
	- Best Practices
	- Key AWS Services
	- Resources

- Operational Excellence

	- Intro
	- Design Principles
	- Definition
	- Best Practices
	- Key AWS Services
	- Resources

## Services

### AWS Data Pipeline

- AWS Data Pipeline is a web service that helps you reliably process and move data between different AWS compute and storage services, as well as on-premises data sources, at specified intervals.
- With AWS Data Pipeline, you can regularly access your data where itï¿½s stored, transform and process it at scale, and efficiently transfer the results to AWS services such as Amazon S3, Amazon RDS, Amazon DynamoDB, and Amazon EMR.

### AWS Elastic Beanstalk

- Intro

	- AWS Elastic Beanstalk is an easy-to-use service for deploying and SCALING web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.
	- You can simply upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.
	- At the same time, you retain full control over the AWS resources powering your application and can access the underlying resources at any time.
	- There is no additional charge for Elastic Beanstalk - you pay only for the AWS resources needed to store and run your applications.

- Use Cases

	- Worker Environments
	- Applications from Docker Containers

### AWS Opsworks

- AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet.
- Chef and Puppet are automation platforms that allow you to use code to automate the configurations of your servers.
- OpsWorks lets you use Chef and Puppet to automate how servers are configured, deployed, and managed across your Amazon EC2 instances or on-premises compute environments.
- OpsWorks has three offerings,

	- AWS Opsworks for Chef Automate,
	- AWS OpsWorks for Puppet Enterprise,
	- AWS OpsWorks Stacks.

### AWS Cloudformation

- Intro

	- AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment.
	- AWS CloudFormation is available at no additional charge, and you pay only for the AWS resources needed to run your applications.
	- CloudFormation allows you to use a simple text file to model and provision, in an automated and secure manner, all the resources needed for your applications across all regions and accounts.
	- This file serves as the single source of truth for your cloud environment.

- Sections

	- Resources
	- Parameters
	- Outputs
	- Mappings

### DevOps

- AWS provides a set of flexible services designed to enable companies to more rapidly and reliably build and deliver products using AWS and DevOps practices.
- These services simplify provisioning and managing infrastructure, deploying application code, automating software release processes, and monitoring your application and infrastructure performance.
- DevOps is the combination of cultural philosophies, practices, and tools that increases an organizationï¿½s ability to deliver applications and services at high velocity: evolving and improving products at a faster pace than organizations using traditional software development and infrastructure management processes. This speed enables organizations to better serve their customers and compete more effectively in the market.

### AWS Trusted Advisor

- AWS Trusted Advisor is your customized cloud expert! It helps you to observe best practices for the use of AWS by inspecting your AWS environment with an eye toward saving money, improving system performance and reliability, and closing security gaps
- AWS Organizations helps you centrally govern your environment as you grow and scale your workloads on AWS. Whether you are a growing startup or a large enterprise, Organizations helps you to centrally manage billing; control access, compliance, and security; and share resources across your AWS accounts.

### Amazon Managed Blockchain

- Amazon Managed Blockchain is a fully managed service that makes it easy to create and manage scalable blockchain networks using the popular open source frameworks Hyperledger Fabric and Ethereum*.
- Blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority.

### AWS Serverless Application Model (AWS SAM)

- Lamda
- DynamoDB
- S3
- API Gateway APIs,
- SQS Queue
- ECS

### Definition

- LAMP stack

	- A LAMP Stack is a set of open-source software that can be used to create websites and web applications. LAMP is an acronym, and these stacks typically consist of the Linux operating system, the Apache HTTP Server, the MySQL relational database management system, and the PHP programming language.

### Using Amazon Web Services for Disaster Recovery

- Backup and Restore
- Pilot Light
- Warm standby
- Multi-Site

