# The Well Architected Framework 

The whitepaper discussed in this section are available for download at https://aws.amazon.com/architecture/well-architected/ or in the `whitepapers` folder.

**There are 5 pillars:**

- **Security**
- **Reliability**
- **Performance Efficiency**
- **Cost Optimization**
- **Operational Excellence**



**Structure of each pillar**

* Design Principles
* Definition
* Best Practises - the most importnant part in the whitepapers
* Key AWS Services
* Resources

**General Design Principles**

- Stop guessing your capacity needs - know your traffic etc.
- Test systems at production scale - do quick test with on-demand resources
- Automate to make architectural experimentation easier - use CloudFormation as much as you can
- Allow for evolutionary architectures - allow your architecture to be dynamic
- Data-Driven architectures - log usage data to CloudWatch and take decisions from this data
- Improve through game days - test the copy of your production environment with simulations of big events like "Black Friday". Pay only for the resources



## I Security

### Design Principles

* Apply security at all layers - don't focus only on your firewall, remeber about Subnets, ACL's, Ports, Anti-Virus on Instances
* Enable traceability
* Automate responses to security events - SNS notification where port 22 is bruteforced
* Focus on securing your system
* Automate security best practises - take a default AMI and harden the OS (bullet-proof it), then use your Hardened AMI, more at https://www.cisecurity.org/services/hardened-virtual-images/

![Image result for aws shared responsibility model](images/shared_responsibility.jpg) 

### Definition

Security in the cloud consists of 4 areas;

* **Data protection**
* **Privilege management**
* **Infrastructure protection**
* **Detective controls**

### Data Protection

Before you begin to architect security practices across your environment, basic data classification should be in place. You should organise and classify your data in to segments such as publicly available, available to only members of your organisation, available to only certain members of your organisation, available only to the board etc. You should also implement a least privilege access system so that people are only able to access what they need. However most importantly, you should encrypt everything where possible, whether it be at rest or in transit (https).

#### Data Protection - Best Practises

In AWS the following practices help to protect your data; 

* AWS customers maintain full control over their data. 
* AWS makes it easier for you to encrypt your data and manage keys, including regular key rotation, which can be easily automated natively by AWS or maintained by a customer. (Key Management Tools )
* Detailed logging is available that contains important content, such as file access and changes. (CloudTrail - changes in environment)
* AWS has designed storage systems for exceptional resiliency. As an example, Amazon Simple Storage Service (S3) is designed for 11 nines of durability. (For example, if you store 10,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000,000 years.)
* Versioning, which can be a part of a larger data lifecycle-management process, can protect against accidental overwrites, deletes and similar harm.
* AWS never initiates the movement of data between regions. Content placed in region will remain in that region unless the customer explicitly enables a feature or leverages a service that provides that functionality.

#### Best Practises - Data Protection Questions

- How are you encrypting and protecting your data at rest? 
- How are you encrypting and protecting your data at transit? (SSL)



### Privilege management

#### Privilege management - Best Practises

Privilege management ensures that only authorized and authenticated users are able to access your resources, and only in a manner that is intended. It can include:

* Access Control Lists (ACLs) - who can access this data?
* Role Based Access Controls - S3 Role for and EC2, lets the instance access S3 but not other services
* Password Management (such as password rotation policies)

#### Best Practises - Privilege management Questions

* How are you protecting access to and use of the AWS root account credentials?
  * MFA
* How are you defining roles and responsibilities of system users to control human access to the AWS Management Console and APIs?
  * Groups of SysAdmins, Level2Admins, HR, etc.
* How are you limiting automated access (such as from applications, scripts, or third-party tolls or services) to AWS resources?
  * DynamoDB accessec only form inside the VPC
* How are you managing keys and credentials?

### Infrastructure protection

#### Infrastructure protection - Best Practises

Outside of Cloud, this is how you protect your data centre. RFID controls, security, lockable cabinets, CCTV, etc. Within AWS they handle this, so really Infrastructure protections exists at VPC level.

#### Best Practises - Infrastructure protection Questions

* How are you enforcing network and host-level boundary protection?
  * VPC: security groups, ACLs, public/private subnets, what users do you use to login to EC2 instances, are EC2 instances in public/private subnets, do you use bastions hosts
* How are you enforcing AWS service level protection?
  * Multiple users to the console? IAM? MFA? Password policies, Different privileges
* How are you protecting the integrity of the operating systems on your Amazon EC2 instances?
  * Anti-Virus etc.

### Detective controls

#### Detective controls - Best Practises

You can use detective controls to detect or identify a security breach.

AWS Services to achieve this include:

- AWS CloudTrail - log changes in AWS environment
- Amazon CoudWatch - monitor CPU/RAM utilization etc.
- AWS Config
- Amazon Simple Storage Service (S3)
- Amazon Glacier

#### Best Practises - Detective controls Questions

- How are you capturing and analysing AWS logs?
  - is CloudTrail is on in every Region? - it's regional
  - IDS/IPS log management service; AlertLogic



### Key AWS Services

- Data protection
  - You can encrypt your data both in transit and at rest using:
    - ELB, EBS, S3 & RDS
- Privilege management
  - IAM (Identity Access Management), MFA (Multi-Factor Authentication)
- Infrastructure protection
  - VPC - think that a VPC is your private data centre
    - security groups, open/ closed ports for individual IP's
- Detective Controls
  - AWS CloudTrail
  - AWS Config
  - Amazon Cloud Watch

 

## II Reliability

The reliability pillar covers  the ability of a system to recover from service or infrastructure outages/disruptions as well as the ability to dynamically acquire computing resources to meet demand.

### Design Principles

- Test recovery procedures 
  - Netflix and testing failure - SimianArmy, ChaosMonkey
- Automatically recover from failure
  - notifications, tracking failures and repairing them
- Scale horizontally to increase aggregate system availability
  - replace 1 large resource with multiple small resources
  - Scale Out rather than Scale Up
- Stop guessing capacity



### Definition

Reliability in the cloud consists of 3 areas:

- Foundations
- Change Management
- Failure Management



### Foundations

#### Foundations - Best Practises

Before architecting any system, you need to make sure you have the prerequisite foundations. In traditional IT one of the first things you should consider is the size of the comms link between your HQ and your Datacentre. If you misprovision this link, it can take 3-6 months to upgrade which can cause a huge disruption to your traditional IT estate

With AWS they handle most of the foundations for you. The cloud is designed to be essentially limitless meaning that AWS handle the networking and compute requirements themselves. However they do set service limits to stop customers from accidentally over-provisioning resources.

To change a default service limit you have to contact AWS and ask for raising your service limit.

More about the default service limits at https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html

#### Best Practises - Foundations Questions

- How are you managing AWS service limits for your account?
  - who is in charge of that, who raises the tickets to AWS
- How are you planning your network topology on AWS?
- Do you have an escalation path to deal with technical issues?
  - Do you have a technical account manager with AWS?



### Change Management

#### Change Management - Best Practises

You need to be aware of how change affects a system so that you can plan proactively around it. Monitoring allows you to detect any changes to your environment and react. In traditional systems, change control is done manually and are carefully co-ordinated with auditing

With AWS things are a lot easier, you can use CloudWatch to monitor your environment and services such as autoscaling to automate change in response to changes on your production environment.

You can migrate servers in matter of minutes not days



#### Best Practises - Change Management Questions

- How does your system adapt to changes in demand?
- How are you monitoring AWS resources?
- How are you executing change management?
  - Auto Scaling



### Failure Management

#### Failure Management - Best Practises

With cloud you should always architect your systems with the assumptions that failure will occur. You should become aware of these failures, how they occurred, how to respond to them and then plan on how to prevent these from happening again.

#### Best Practises - Failure Management Questions

- How are you backing up your data?
- How does your system withstand component failures?
- How are you planning for recovery?



### Key AWS Services

- Foundations
  - IAM, VPC
- Change Management
  - AWS CloudTrail
- Failure Management
  - AWS CloudFormation



## III Performance Efficiency

The Performance Efficiency pillar focuses on how to use computing resources efficiently to meet requirements and how to maintain that efficiency as demand changes and technology evolves



### Design Principles

- Democratize advanced technologies
  - Use technologies as you need (as a Service), you don't have to be provisioning new environments and becoming an expert in these technologies (NoSQL DBA etc.)
- Go global in minutes
  - easily deploy your system around multiple regions (CloudFormation)
- Use server-less architectures
  - S3, CDN, Lambda, no EC2
- Experiment more often
  - Test new configurations because you pay only for what you use

### Definition

Performance Efficiency in the cloud consists of 4 areas;

- Compute
- Storage
- Database
- Space-time trade-off



### Compute

#### Compute - Best Practises

When architecting a system it is very important to choose the right kind of server - CPU/ Memory Optimized

With AWS the servers are virtualized, and with one click of a button (or API call) you can change the type of the server. You can even replace servers with Lambda.

#### Best Practises - Compute Questions

* How do you select the appropriate instance type for your system?
* How do you ensure that you continue to have the most appropriate instance type as new instance types and features are introduced?
  * Which type of EC2 type to use?
* How do you monitor your instances post launch to ensure they are performing as expected?
* How do you ensure that the quantity of your instances matches demand?



### Storage

#### Storage - Best Practises

The optimal storage solutions for your environment depends on a number of factors. For example:

- Access Method - Block, File or Object
- Patterns of Access - Random (S3) or Sequential (MySQL on EBS)
- Throughput Required
- Frequency of Access - Online, Offline or Archival
- Frequency of Update - Worm, Dynamic
- Availability Constraints
- Durability Constraints

AWS Storage is virtualized, 

S3 gives you:

* 11x9's durability 
* Cross Region Replication 

EBS gives you:

- different storage mediums (SSD, Magnetic, PIOPS, etc.)
- you can easily move volumes between the different types of storage mediums
  - Take a snapshot form magnetic and move it to SSD, then if needed upgrade to Provision IOPS



#### Best Practises - Storage Questions

- How do you select the appropriate storage solution for your system?
- How do you ensure that you continue to have the most appropriate storage solution as new storage solutions and features are launched?
- How do you monitor your storage solution to ensure it is performing as expected?
- How do you ensure that the capacity and throughput of your storage solutions matches demand?



### Database

#### Database - Best Practises

Optimal Database solution depends on:

- do you need database consistency
- do you need high availability
- do you need No-SQL
- do you need DR

Multiple options: RDS (Aurora), DynamoDB (NoSQL), Redshift (Data Warehouse)

#### Best Practises - Database Questions

- How do you select the appropriate database solution for our system?
- How do you ensure that you continue to have the most appropriate database solution and features as new database solution and features are launched?
- How do you monitor your databases to ensure performance is as expected?
- How do you ensure the capacity and throughput of your databases matches demand?



### Space-time trade-off

When building an infrstructure there is a trade-off where space (memory / storage) is reduced to reduce processing time (compute)

You can cache data to reduce time (CloudFront, ElastiCache)

#### Space-time trade-off - Best Practises

Examples:

- RDS
  - add read replicas for reducing the load on your database and creating multiple copies to help lower latency
- Direct Connect
  - provide predictable latency between HQ and AWS
- Global Infrastructure
  - have multiple copies of your system in regions closest to your customers
  - use ElastiCache and CloudFront to reduce latency

#### Best Practises - Space-time trade-off Questions

- How do you select the appropriate proximity and caching solutions for your system?
- How do you ensure that you continue to have the most appropriate proximity and caching solutions as new solutions are launched?
- How do you monitor your proximity and caching solutions to ensure performance is as expected?
- How do you ensure that the proximity and caching solutions you have matches demand?

### Key AWS Services

- Compute
  - AutoScaling
- Storage
  - EBS (Elastic Block Storage), S3, Glacier
- Database
  - RDS, DynamoDB, Redshift
- Space-Time Trade-Off (lower the latency)
  - CloudFront, ElastiCache, Direct Connect, RDS Read Replicas



## IV Cost Optimization

Use the Cost Optimization pillar to reduce your costs to a minimum and use those savings for other parts of your business. Pass the cost saving on to customers (cheaper services/ products)

### Design Principles

- Transparently attribute expenditure
  - Identify the costs of the system individual components and who generated them
  - This cost was consumed by the HR department
- Use managed services to reduce cost of ownership
- Trade capital expense for operating expense
  - Pay as you use resources (test/dev environments used only 8h/day)
- Benefit from economies of scale
- Stop spending money on data center operations (stacking, racking, powering of new servers)

### Definition

Cost optimization in the cloud consists of 4 areas:

- Matched supply and demand
- Cost-effective resources
- Expenditure awareness
- Optimizing over time

### Matched supply and demand

#### Matched supply and demand - Best Practises

- Don't under/over provision. As demand grows, supply new compute resources
- Autoscaling that scale's with demand
- Use Lambda to pay only for number of executions
- CloudWatch can help with keeping track of your demand

#### Best Practises - Matched supply and demand Questions

- How do you make sure your capacity matches but does not substantially exceed what you need?
- How are you optimizing your usage of AWS services?



### Cost-effective resources

#### Cost-effective resources - Best Practises

- Using the correct instance type is key to cost savings
  - t2.micro - 7hours to complete (more cost because used longer)
  - m.2xlarge - minutes to complete
- A well architected system will use the most cost efficient resources to reach the end business goal

#### Best Practises - Cost-effective resources Questions

- Have you selected the appropriate resources types to meet our cost targets?
- Have you selected the appropriate pricing model to meet your cost targets?
- Are there manged services (higher-level services than EC2, EBS, S3) that you can use to improve your ROI (Return on Investment)



### Expenditure awareness

#### Expenditure awareness - Best Practises

- In the cloud you don't have to: get quotes, choose suppliers, deliver, install servers etc.
- Provision things in seconds
- You have to be aware which team in the company spends on what (different AWS accounts)
  - use cost allocation tags to track this
  - use billing alerts
  - use consolidated billing

#### Best Practises - Expenditure awareness Questions

- What access controls and procedures do you have in place to govern AWS costs?
- How are you monitoring usage and spending?
- How do you decommission resources that you no longer need, or stop resources that are temporarily not needed? (DEV env runs for 8h)
- How do you consider data-transfer charges when designing your architecture?



### Optimizing over time

#### Optimizing over time - Best Practises

- AWS deploy hundreds of new services
  - Consider upgrading from MySQL RDS to Aurora
- Keep rack of the changes made to AWS
- Read the AWS Blog
- Use AWS Trusted Advisor

#### Best Practises - Optimizing over time Questions

- How do you manage and/or consider the adoption of new services?



### Key AWS Services

- Matched supply and demand
  - Autoscaling
- Cost-effective resources
  - EC2 (reserved instances)
  - AWS Trusted Advisor
- Expenditure awareness
  - CloudWatch Alarms,
  - SNS
- Optimizing over time
  - AWS Blog, AWS Trusted Advisor



## V Operational Excellence

Operational practises and procedures used to manage production workloads. 

How planned changes are executed, as well as responses to unexpected operational events.

Change execution and responses should be automated. All processes and procedures of operational excellence should be documented, tested, and regularly reviewed.

### Design Principles

- Perform operations with code
- Align operations processes to business objectives - collect metrics that indicate your business objectives are being met
- Make regular small, incremental changes (Windows 10 - small updates)
- Test responses to unexpected events (Netflix and the SimianArmy)
- Learn from operational events and failures
- Keep operations procurers current (up-to-date documentation and procedures)

### Definition

There are three best practise areas for Operational Excellence in the cloud:

- Preparation
- Operation
- Response

### Preparation

#### Preparation - Best Practises

Operations checklists ensure that workloads are ready for production operation, and prevent unintentional production promotion without effective preparation

Workload should have:

- Runbooks - operations guidance that operations teams can refer to so they can perform normal daily tasks.
- Playbooks - Guidance for responding to unexpected operational events. Playbooks should include response plans, as well as escalation paths and stakeholder notifications.
  - RDS goes down -> notify a stakeholder (CTO)

In AWS there ae several methods, services and features that can be used to support day-to-day operations and unexpected events

- **CloudFormation** can be used to ensure that environments contain all required resources when deployed in production, and that the configuration of the environment is based on tested best practises, which reduces the opportunity for human error.
- **Auto Scaling** or other scaling mechanism will allow workloads to automatically respond when business-related events affect operational needs.
- **AWS Config** you can create rules which  feature create mechanisms to automatically track and respond to changes in your AWS workloads and environments
- **Tagging** can be used to easily identify all resources in a workload



### Best Practises - Preparation Questions

- What best practises for cloud operations are you using?
- How are you doing configuration management for your workload?
- Be sure that your documentation is thorough and up-to-date
  - Application desings
  - Environment configurations
  - Resource configurations
  - Response plans
  - Mitigtion plans

### Operation

#### Operation - Best Practises

Operations should be standardized and manageable on routine basis. Focus should be on **automation, small frequent changes, regular quality assurance testing**, and defined mechanisms to track, audit, roll back, and review changes. 

There shouldn't be, large changes which require scheduled downtime and manual execution.

A wide range of logs and metrics that are based on key operational indicators for workload should be collected and reviewed to ensure continuous operations.

In AWS you can set up CI/CD pipelines (continuous integration/deployment) for software development automation (GIT -> Build -> Testing -> Deployment)

### Best Practises - Operation Questions

- How are you evolving your workload while minimizing the impact of change?
- How do you monitor your workload to ensure it is operating as expected?



### Response

Response to unexpected operational event should be automated.

This is not only for alerting but also for mitigation, remediation, rollback and recovery

Alerts should invoke escalations functional and hierarchical, hierarchical ones should send notification to stakeholders.

#### Response - Best Practises

In AWS, CloudWatch can have an alarm which will trigger a SNS notification to an Admin who will check the problem.

#### Best Practises - Response Questions

- How do you respond to an unplanned operational events?
  - What happens when a RDS goes down?
- How is escalation managed when responding to unplanned operational events?
  - Who (DBA) gets notified when the RDS doesn't get back on-line after couple minutes?

### Key AWS Services

- **Preparation**
  - **AWS Config**  - detailed inventory of your AWS resources and configuration, continuously records configuration changes
  - **AWS Service Catalog** - create a standardized set of service offerings that are aligned with best practises
  - Design Workloads that use automation with **Auto Scaling, Amazon SQS**
- **Operation**
  - **AWS CodeCommit, CodeDeploy, CodePipeline** - manage and automate code changes to AWS workloads
  - **AWS SDKs or third-party librariers** - automate operational changes
  - **AWS CloudTrail** - audit and track changes made to AWS environments
- **Response**
  - CloudWatch - effective and automated responses, alarms that trigger SNS notifications 



## Summary
