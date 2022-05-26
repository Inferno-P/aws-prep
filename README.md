# AWS Solutions Architect Prep :rocket:
Courses taken : 
- Andrew Brown from Exam Pro - https://www.youtube.com/watch?v=Ia-UEYYR44s

- Stephan Maarek's AWS Solution Architect on Udemy 

[Course Slides](https://media.datacumulus.com/aws-saa/AWS%20Certified%20Solutions%20Architect%20Slides%20v4.7.1.pdf)

## Exam Details 
```
* 65 Questions - MCQ (1 out of 4) and Multiple Response (any out of 4)
* 130 Mins (2h 10 Mins)
* ~72% Passing Score (Max points : 1000, Min. Points : 720) equivalent to a C- grade. 
* 3 year Valididity
* 150 USD
* Scoring : Unanswered questions are scored as incorrect; there is no penalty for guessing. 
```
----
## Exam Guide 
Content Outline of the Exam Syllabu with weightage and services hinted at. 
[Link to PDF](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)


### Domain 1 : Design RESILIENT Architectures (34%)
#### 1.1 Choose reliable/resilient storage
- Elastic Block Storage, S3 and other storage options.
- 
#### 1.2 How to design de-coupling mechanisms 
- Application integration like SQS and SNS

#### 1.3 Hot to design a multi-tier architecture solution
- Generally, solutions have 3 layers : 
  - Data Layer
  - Web Layer
  - Load Balancing Layer

#### 1.4 How to deign high availability and/or fault tolerant architectures
- Route53, Loadbalancing, AutoScaling Groups. 
- What happens when an AZ goes out?
- What happens when a Region goes out? 


### Domain 2 : Design PERFORMANT Architectures (24%)
#### 2.1 Choose performant storage and databases
- DynamoDB vs RedShift vs RDS

#### 2.2 Apply Caching to improve performance
- ElasticCache
- CloudFront

#### 2.3 Design for Elasticity and Architectures
- AutoScaling Groups


### Domain 3 : Design SECURE Applications and Architectures (26%)
#### 3.1 How to secure aaplication tiers
- How and when to secure the 3 layers : Data, Web and Network(Load Balancing)
#### 3.2 How to secure data
- Data at Rest or
- Data at Transit

#### 3.3 Define networking infrastructure for a single VPC application
- Knowing VPCs inside and out.

### Domain 4 : Design COST-OPTIMISED Architecture (10%)
#### 4.1 How to design cost-optimised Storage.
- Mainly S3 service. 
- S3 has a bunch of classes that we can use with different pricing. Knowing when to use which. 
#### 4.1 How to design cost-optimised Compute.
- When to use different type of EC2 instances?
- When to use AutoScaling groups?

### Domain 5 : Design OPERATIONALLY-EXCELLENT Architecture (6%)
- Choose design features that enable operational excellence


## Recommended Whitepapers :
* AWS Best Practises
* AWS Well-Architected Framework

--

![Important AWS Services covered](https://user-images.githubusercontent.com/12581835/169692436-2098dbc5-fdd9-49b7-85bd-90435c3f67a0.png)


----

## IAM Summary :closed_lock_with_key:
- Users : Mapped to a physical user. Has a password.
- Groups : Logical entities that contain User. One user can be in more than one group.
- Policies : Set of rules (like a JSON Document) describing the access privileges of a Group/User/Role.
  - A statement in an IAM Policy consists of `Sid, Effect, Principal, Action, Resource, and Condition`. 
  - Version is part of the IAM Policy itself, not the statement. :warning:
 
![Screenshot 2022-05-23 at 21 17 15](https://user-images.githubusercontent.com/12581835/169890660-a85b3a58-b3fe-4bf7-94fb-ca60556dd85d.png)

- Roles : An _IAM Entity_ that defines a set of permissions for making requests to AWS Services, and will be used by an AWS Service. 
  - Provide access privileges to AWS services to perform actions on behalf of Users.
   
- Security : MFA + Password policy 
- Access Keys : Need these keys to access AWS via CLI or SDK.
  - Access Key is like your username 
  - Secret access key is like your password
- Auditing :
  - IAM Credentials Report (account level info)
  - IAM Access Advisor (user level info)
- __Other Important Stuff :__ :sparkle:
  - _Principle of Least Privileges._
 
 ---
 
 
## Amazon EC2 Summary 💻
- Solving the 'compute' problem.
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- Not just 1 service, it's a collection of services :
  - Renting virtual machines (EC2)
  - Storing data ono virtual drives (EBS)
  - Distributing load across machines (ELB)
  - Scaling the services (ASG)
- EC2 Sizing and Config Options 
  - OS - Linux, Windows, Mac OS
  - CPU
  - RAM
  - Storage Space:
    - Network Attached (EBS and EFS)
    - Hardware (EC2 instance store)
  - Network : Speed, Public IP Address
  - Firewall Rules : ```Security Groups```
  - Boootstrap Script (configure at first launch) : EC2 User data


 
