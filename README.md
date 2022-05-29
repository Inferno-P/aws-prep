
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
 
 Sample Codes used :
 ```
#!/bin/bash
# Use this script for user data
# install httpd 
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1> Hello World from $(hostname -f)</h1>" > /var/www/html/index.html

```
 
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
  - Bootstrap Script (configure at first launch) : ``EC2 User data``
    - Bootstrapping means launching commands when a machine starts
    - The boostrap script is only run once at the instance first start. 
    - Commands like : *Installing Updates, Softwares, Downloading files from internet, etc.*
    - ``root user`` used too execute bootstraping script.
  
### EC2 Pricing :receipt:
1. On-Demand Instance (OD)
	-	__Pay for what you use.__ _Linux/Windows - pay per second, after 1st min. Other OSs - billing per hour._
	-	Highest Cost, but no upfront payment.
	-	`Short-term, irregular and un-interrupted workloads`
	-	No long term commitment.

2. Reserved Instance (RI)
	- 72% cheaper vs On-Demand. Reserve specific instance attributes __(Instance Types, Region, Tenancy, OS)__
	- __Reservation Features__:
		- Period - 1 year or 3 years ('Standard' Reserved)
		- Payment Options - No Upfront(+), Partial Upfront(++), All Upfront(+++)
		- Scope - Regional or Zonal (reserved capacity in an AZ)
	- `Recommended for steady-state usage applications (think database)`
	- Can buy and sell in the reserved instance market place when not in use anymore.
	- Post the Reserved instance usage, pricing returns to On-Demand rates.
	- 'Convertible' Reserved : Flexible on EC2 instance type, family OS, scope and tenancy. Less Discount - 66%.
	
3. Saving Plan Instance (SP)
	- Discount on Long-term usage. (upto 72% - same as RIs) 
	- Commitment required : Consistent usage $10/Hr for 1 or 3 years
	- Usage beyond commitment is priced @ On-Demand Rates.
	- Locked to instance family & AWS Region. (Eg. M5 in us-east-1). Flexible on Instance Size, OS and Tenancy (Hst Dedicated, Default)

4. Spot Instance 
	- Discount upto 90% vs On-Demand
	- Most cost efficient.
	- `Workloads with flexible start and end times that can withstand interruptions.`
	- Eg : Batch Jobs, Img Processing. Not recommended for Databases.

5. Dedicated Host and Instance (DH)
	- HOST
		- A physical servers with EC2 instance capacity fully dedicated to your use.
		- Useful to address __compliance requirements__ and use your existing server-bound software licences (per-socket, per-core, per VM S/W Licenses) 
		- Purchasing Options : __On-Demand__ pay per second for active dedicated host. __Reserved__ 1 or 3 years (All upfront only)
		- Most Expensive.
		- Useful for software that have complicated licensing model. (BYOL - Bring Your Own License).  _Eg: Oracle Netsuite, Adobe Photoshop, etc.
	- INSTANCE
		- Instances run on h/w that's dedicated to you.
		- May share h/w with other instances in same account.
		- No control over instance placement. 
6.  Capacity Reservation Instances
	- Reserved On-Demand instances capacity in a specific AZ for any duration.
	- No time commitment. No billing discounts.
	- Combine w/ Regional Reserved 
	 - Charged @ On-Demand rates whether use or not.

__Which room is right for me?__
<img width="1037" alt="Screenshot 2022-05-29 at 16 11 32" src="https://user-images.githubusercontent.com/12581835/170873487-d57402ca-0aa7-4565-915d-587c3ffa4923.png">
__CheatSheet__
<img width="1595" alt="Screenshot 2022-05-29 at 16 12 46" src="https://user-images.githubusercontent.com/12581835/170873555-11465219-3dae-4a3a-816b-d96317977d12.png">



# Security Groups 👮
- Kinda like 'Firewalls' on EC@ instances.
- Important for network security in AWS
- Security groups only contain __ALLOW__ rules.
- __Rules__ : Control how traffic is allowed into or out of our EC2 instances.
  - Access to ports.
  - Authorised IP ranges - IPv4 and IPv6
  - Control of inbound network (outside to instance).
  - Control of outbound network (instance to outside).
  - Default Rules : All inboound traffic is blocked. All outbound traffic is allowed.
- __Important Points__
  - Can be attached to multiple instance. An instance can have multiple security groups attached.
  - Locked to a region/VPC comobination. If we change regions, we will have to create different SG.
  - SGs do not run on EC2. They lie outside and if they block some data, then the underlying EC2 won't see it.
- __Example :__
 There is a EC2 machine called `X1` with 2 security groups attached to it called `SG1` and `SG2`. 
 Denoted by `X1[SG1, SG2]`.
 There are other EC2 machines called `X2` and `X3` with security groups SG1 and SG2 attached, respectively.
 Denoted by `X2[SG1]`, `X3[SG2]`.
 
 The EC2 machines with same SG can intereact with each other. i.e. `X2` and `X3` can signal `X1` since they have same SGs.
 
`X2[SG1] -> X1[SG1, SG2]` and `X3[SG2] -> X1[SG1, SG2]`

- Ports :
   - 22 = SSH into Linux
   - 21 = FTP
   - 22 = SFTP 
   - 80 = HTTP
   - 443 = HTTPS
   - 3389 = RDP into Windows instance
 
 






