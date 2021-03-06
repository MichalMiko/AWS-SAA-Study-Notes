# Overview of Amazon Web Services

## Compute (SAA)

- **EC2** - Elastic Compute; Virtual Machines
- **EC2 Container Service** - Docker -> AWS
- **Elastic Beanstalk** - upload only the code (Important in Developer and DevOps Exams)
- **Lambda** - Upload Code, run when needed
- **Lightsail** - VPS service - SSH / RDP server - Virtual Private Server
- **Batch** - batch computing

## Storage (SAA)

- **S3 - Simple Storage Service**, object based storage, upload files to buckets ()
- **EFS - Elastic File System** - Network Attached Storage, store files and mount to multiple EC2 instances
- **Glacier** - archive data
- **Snowball** - bring data to AWS
- **Storage Gateway** - VM installed in your datacentre that replicate data to S3

## Databases (SAA)

- **RDS - Relational Database Service**; MySQL, Aurora (MySQL compatible), Oracle, etc
- **DynamoDB** - non relational DB,
- **Elasticache** - cache commonly queried data
- **Red Shift** - Data Warehouse / BI

## Migration (SAA)

- **AWS Migration HUB** - tracking service, track apps migrated to AWS
- **Application Discovery Service** - track dependencies for your application
- **Database Migration Service** - Migrate databases from On premise -> AWS
- **Server Migration Service** - Migrate Virtual and Physical Servers to AWS
- **Snowball** - migrate data to cloud

## Networking and Content Delivery (SAA)

- **VPC - Virtual Private Cloud** - Virtual Data Center, configure firewalls, AZ's, Network ACL's - very important and fundamental
- **CloudFront - Content Delivery Network**; Provide Media Files for users in different regions (Edge locations)
- **Route53** - DNS service; 
- **API Gateway** - create own APIs for other services
- **Direct Connect** - Dedicated line form your company to VPC in AWS

## Developer Tools

- **CodeStar** - Project Managing your code; Continuous Delivery Toolchain
- **CodeCommit** - store code, private GIT Repo
- **CodeBuild** - Compile and Test your Code -> CodeDeploy
- **CodeDeploy** - Automate code deployment to EC2 instances, OnPremise, Lambda
- **CodePipeline** - automate steps for releasing software - CD Software
- **X-Ray** - Debug and analyse serverless applications
- **Cloud9** - IDE inside AWS console

## Management Tools (SAA)

- **CloudWatch** - monitoring and management service - very important in SysOps exam, 
- **CloudFormation** - scripting infrastucture, important in Solutions Architect, infrastructure architect, deploy WordPress site, infrastructure into code, reuse code
- **CloudTrail** - log changes on **AWS console**, turned on by default (1-week), should turn on on all AWS accounts
- **Config** - monitor the configuration of AWS environment, snapshots etc.
- **OpsWorks** - like ElasticBeanstalk; more robust with Chef and Puppet
- **Service Catalog** - catalogue of IT services approved for use (used in SP500 companies)
- **Systems Manager** - interface for managing AWS resources, EC2, for example roll out security patches, group resources important for System Administrator)
- **Trusted Advisor** - != Inspector, advices for security (open ports) or how to save money, 
- **Managed Services** - manage EC2 etc.

## Media Services

- Elastic Transcoder - f.e. upload video -> resize to look good on Android
- MediaConvert - convert media for broadcasting nad streaming
- MedeiaLive - live video processing 
- MediaPackgae - prepare and protect media for broadcasting
- MediaStore - storage service optimized for media
- MediaTailor - targeted advertising for media

## Machine Learning

- SageMaker - deep learning
- Comprehend - analysis of data, what people are saying about your products (like Brand24)
- DeepLens - Artificial Aware Camera, camera can figure out at what it's looking, physical piece of hardware
- Lex - powers Amazon Alexa, chat with customers
- Machine Learning - simpler form of SageMaker - robust
- Polly - convert text -> speech
- Rekognition - image & video, recognize things on media
- Amazon Translate - machine translator like Google Translate
- Transcribe - automatic speech recognition, video / mp3 to text

## Analytics (SAA)

- Athena - sql queries against  spreadsheets stored in S3 bucket, serverless
- EMR - Elastic Map Reduce, processing large data, chop data for analysis
- CloudSearch - search engine
- ElasticSearch Service - search engine
- Kinesis - big data, store data from SocialNetworks -> AWS, follow a hashtag
- Kinesis Video Streams - ingest an process (analyse) Video from web
- QuickSight - BI Tool
- Data Pipeline - move data between AWS services
- Glue - ETL, extract, transform & load data

## Security & Identity & Compliance (SAA)

- **IAM** , Identity Access Management - 
- **Cognito** - device authentication & temporary access to AWS, iPhone app, store data in DynamoDB,
- **GuardDuty** - monitor for malicious activity on AWS accounts
- **Inspector** - agent installed on VM, EC2, run test against it, schedule it, report
- **Macie** - scan S3 Bucket for personal identifiable information, names, adresses, social security numbers
- **Certificate Manager** - SSL Certificates for free (Route 53)
- **CloudHSM (Hardware Security Module)** - store private and public keys
- **Directory Service** - integrate MS AD with AWS
- **WAF, Web Application Firewall** - stop sql injection etc - application layer
- **Shield** - prevent DDoS attacks
- **Artifact** - audit and compliance reports 

## Mobile Services

- Mobile Hub - manage console for mobile app, create mobile hub, import to app, app gets to connect to AWS resources
- Pinpoint - push notifications  using geolocalisation
- AWS AppSync - update data in web and mobile apps in real time
- Device Farm - test apps on real live devices
- Mobile Analytics - analytics for mobiles

## AR/VR - Augmented/Virtual Reality

- Sumerian - common set of tools

## Application Integration (SAA)

- Step Functions - managing Lambda functions
- Amazon MQ - Message Queues
- SNS - notification service, f.e. billing alarm
- SQS - first aws service, queuing jobs for app on EC2
- SWF - Simple Workflow Service - managing orders

## Customer Engagement

- Connect - Contact Center as a Service, 
- Simple Email Service - send large amount of emails

## Business Productivity

- Alexa for Business - dial to a meeting room, reorder ink, etc
- Chime - like Skype and Google Hangouts
- Work Docs - like Dropbox for AWS
- WorkMail - like Office 365

## Desktop & App Streaming (SAA)

- Workspaces - run desktop environments on AWS and stream to end device
- AppStream 2.0 - stream app form cloud to device (Citrix)

## Internet of Things IOT

- iOT - log temp, humidity etc.
- iOT Device Management 
- Amazon FreeRTOS - OS for IOT microcontrollers - free
- Greengrass - machine learning using iOT

## Game Development

- GameLift - develop games on AWS

Next: [Services tested by the AWS Certified Solutions Architect - Associate examination](03-aws-csaa-services.md)