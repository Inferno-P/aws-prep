

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
Questions : "Which type of instance is the best given the nature of workloads?"

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
	- Most cost efficient. Can lose the instance anytime.
	- `Workloads with flexible start and end times that can withstand interruptions.`
	- Eg : Batch Jobs, Img Processing. Not recommended for Databases.
	- __Interesting :__
		- User defines max spot price that they are willing to pay, then get the instance while `current price < user-defined max price`.
		- If  `current price > user-defined max price`, then _stop_ or _terminate_ your instance with a 2 min grace period.
	- __Spot Fleets__: _Ultimate way to save money._
		- Fleet = set of Spot Instances _ optional On-Demand Instance.
		- Fleet tries to meet the target capacity with price constraints:
			- Define possible launch pools : instance type, OS, AZ
			- Can have multiple launch pools, so the Fleet can choose.
			- Fleet stops launching new instances when reaching capacity or max cost.
		- Fleet Strategies:
			- lowestPrice - pick from pool with the lowest price. (cost optimize, short workload)
			- diversified - distributed across all pools (great for availability, long workloads)
			- capacityOptimized: pool with optimal capacity

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

#### Placement Groups
Use to control _where_ and _how_ my EC2 instances get deployed(or _placed_).
	-   **Cluster** : Clusters instances into a low-latency network. `Same Rack. Same AZ`
		- Great Network. But, if the rack fails, then all the instances go down.
		- Use Case : Big data jobs that need to complete fast. App that needs extremely low latency and high network throughput. `high performance`
-	**Spread** : Instances spread across different hardware (in a server rack).
	-	Reduced risk of simultaneous failure. If H/W in AZ1 fails, then less likely h/w will fail in AZ2.
	-	Limited to only 7 instances per AZ per placement group. 
	-	Use Case : Apps that need high availability. Critical apps where each instance must be isolated from failures of each other. `critical`
-	**Partition** : Instances spread  across different partitions (i.e. server racks) within an AZ.
	-	Reduced risk of 'rack failure'. If rack in AZ1 fails, then less likely h/w will fail in AZ2.Upto 100s of EC2 instances. 
	- A partition failure will affect EC2 instances on that rack only.
	- Use Case : HDFS, HBase, Cassandra, etc. `distributed`

### AMI
- Amazon Machine Image : Customization of an EC2 instance.
	- Add your own OS, Software, config, etc.
	- Faster boot times since all the software is pre-packaged.
- Built for a specific region. Can be copied though.
- EC2 instances can be launched from : 
	- Public AMI
	- Your own AMI
	- An AWS Mktplace AMI : Other people create and sell these AMIs.

### EC2 Instance Store
- 'Store' as in storage.
- EC2 instance is a virtual machine, but it is attached to real hardware in a server. Sometimes, these servers have a hard disk attached to them. 
- Use EC2 Instance Store if you need a high performance hardware disk.
- Better I/O performance
- EC2 Instance Store lose their storage, when the instance is stopped. _ephemeral storage_
- Good for buffer/cache/scratch data/temp content.
- Risk of data loss, if hardware fails.
- Backup and Replication of data on Instance Store is _our responsibility_. 


#### Advanced Topics
1. __EC2 Nitro__ - Underlying platform for the next-gen EC2 instances. New virtualisation tech. Better performance (64k IOPS on EBS) and security.
2. __vCPU__ - EC2 instances come with a combination of RAM and vCPU. 1 thread on a CPU = 1 vCPU. _If a CPU has 2 cores with 2 threads per core, then it means 4 vCPU._
If you are being charged by a licensing s/w on the basis of #of vCPUs, then you can reduce the number of threads or cores  that run on a EC2 instance. This configuration happens only at the instance launch.
3. __Capacity Reservations__ - Ensure you have capacity when you need it. Reservations have a manual or planned ending date. No need oof 1 or 3 year commitment. You are billed as soon as the capacity is reserved. AZ, Instance Type, OS must be specified.




# Security Groups 👮
- Kinda like 'Firewalls' on EC2 instances.
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
 
 ---



 # Networking :globe_with_meridians:
###### Crash Course in IP Addresses
- Two sorts of IP formats : 
	- IPv4- `1.160.212.240`, most common form. Format : [0-255].[0-255].[0-255].[0-255] - 3.7 Bn addresses.
	- IPv6 - `1900:4231:3:204:g8he:ir59:40ge`, usually meant for IoT.
- Types : 
| **Public IP**                        | **Private IP**                                                             |
|--------------------------------------|----------------------------------------------------------------------------|
| Machines can be ID'd on the internet | Can be ID'd on a private n/w only.                                         |
| Must be unique across the whole web  | IP must be uniques across a private network (2 pvt n/w can have some IPs) |
| Can be geo-located                   | Machines connect to Internet via an internet gateway.                      |

- Elastic IPs
	-  The IP of an EC2 instance changes whenever we restart it. Elastic IP provides a fixed IP for your instance. 
	- Can be attached to only 1 instance at a time. _If that EC2 instance fails, we can rapidly remap it to another functional instance._
	- Only 5 Elastic IP in your account.
	> Best Practices
	> __Try to avoid using Elastic IP__
	> - Instead, use a random public IP and register a DNS name to it.
	> - Better, use a Load Balancer and don't use a public IP.

### Elastic Network Interface
- Logical component in a VPC that represents a _virtual network card_ (A NIC (Network Interface Card) provides the hardware interface between a computer and a network).
- ENI have 4 attributes :
	- Primary private IPv4, one or more secondary IPv4.
	- One Elastic IP(Public) per private IPv4.
	- One or more security groups.
	- A MAC Address
- ENI can be created independently and attach and detach them to instances on the fly. 
- __ENIs are AZ-bound__ so an ENI in AZ1 can't be attached to a EC2 in AZ2.


---
# Storage :file_cabinet:
## Elastic Block Storage (EBS)

- It's a _network drive_ (kinda like "a network pendrive") you attach to your instances.
- Allows your instance to persist data, even after termination.
- Can be mounted/attached to only one EC2 instance at a time. 
	- Can be detached and attached to other EC2 instance.
- AZ-Bound.
- EBS volumes can exist in the unattached to any EC2 instance.
	- Connected via network so there will be some latency.
	- Storage must be provisioned. Define the capacity at the time of initialisation.
	- You will be billed for the provisioned capacity.
- __Delete on termination__ attribute:
	- By default, the __root EBS volume is deleted__ when an EC2 gets terminated.
	- But, the attached EBS volume doesn't get deleted.  

- __EBS Snapshots - __
	- Make a backup of EBS volume at a point in time. Recommended to detach before snapshotting.
	- Can copy across AZ or Region.
	- __Snapshot Archive__ Snapshots can be archived to "archived tier". 75% cheaper. Restoring takes 24 - 72 hours.
	- __Recycle Bin__ to retain the deleted EBS volumes for 1 day till 1 year to recover any accidental deletions.

- __EBS Volume Types__
	- EBS classification basis - Size | Throughput | IOPS
	- __gp2/gp3 (SSD)__ : General purpose SSD volume. Balances price and performance. `Boot Volume`.
	- __io1/io2 (SSD)__ : Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads. `Boot Volume` . `Provisioned IOPS` `Multi-Attach`
	- __st1 (HDD)__ : Low cost HDD. Frequently accessed, throughput-intensive workloads.
	- __sc1 (HDD)__ : Lowest cost HDD. Less frequently accessed workloads.
	
- __EBS Encryption__
	- What is encrypted? _Data at rest, Data inflight between instance and volume, snapshots, all volumes created from the snapshot._
	- Encryption is recommended due to minimal impact on latency.
	- Uses KMS keys (AES-256).
	- Copying an unencrypted snapshot can be encrypted.
	- __How to encrypt an un-encrypted EBS volume?__ Create a snapshot -> Encrypt the snapshot -> Create a volume using the snapshot. -> The volume will be encrypted.


## Elastic File System (EFS) :file_folder:
- Managed NFS(Network File System) that can be mounted on multiple EC2.
- Works with multi-AZ. An EFS can be connected to EC2 instances in multiple AZs.
- Highly available, scalable, expensive, pay-per-use. 
- __Use cases:__ Content Mgmt, Web serving, data sharing, wordpress. 
- __Security :__ Uses NFSv4.1 protocol. Uses Security Group to control access. Encryption at rest using KMS. 
- __Compatible with only Linux based AMIs.__
- Uses POSIX file system (same as Linux). 
- __File system scales automatically, so no need to provision and plan capacity!__

__Scale__:
- 1000s of concurrent NFS clients, 10GB+/s throughput
- Grows to petabyte-scale file network file system, automatically.
__Performance Mode__: (configured at creation time)
- General purpose(default): latency-sensitive use cases (web server, CMS, etc.)
- Max I/O - higher latency, throughput, highly parallel (big data, media processing..)
__Throughput Mode__: 
- Bursting (1TB = 50MBps + burts oof uto 100MBps) _Scales with the size of file system._
- Provision: set a throughput regardless of storage size.
__Storage Tiers__:
- Standard : Frequently accessed files.
- Infrequest Access (EFS-IA) : Cheap storage, retrieval. Enable EFS-IA with a Lifecycle Policy. 
	- Lifecycle Policy is a set oof rules to define the scope of storage of data based on it's usage pattern.
__Availability__:
- Regional : muti-AZ, great for production.
- One Zone : great for dev, backup enabled by default. Compatible with IA. 90% cheaper.

EFS Exam Questions: `When should you use EFS? How to configure it to maintain compliance?`

---

:godmode:
---
> __Scalability and Availability__
> Scalability means "Application can handle greater load by adapting." 
> There are two kinds of scalability:
> - __Vertical Scalability__- _Increasing the size of the instance eg - add more RAM, etc._
> 	- Instance sizes can vary from `t2.nano` (0.5GB ram/1vCPU) to `12tb1.metal` – 12.3 TB of RAM, 448 vCPUs.
> - __Horizontal Scalability (= elasticity)__ - _Increasing the number of instances / systems. Implies distributed systems._
> 	- AutoScaling Group
> 	- Load Balancer
> 
> __Availability__ means "Application can survive a data center loss". Achieved by running instances for the same application across multiple
> AZs. Availability and Horizontal Scalability go hand in hand.
> - Auto Scaling Group multi AZ 
> - Load Balancer multi AZ
---

## Elastic Load Balancer :balance_scale:

__What is Load Balancer?__
Load Balancers are servers that forward and distribute traffic to multiple servers (e.g. EC2 instances) downstream. 
In other words, as the web traffic increases, the ELB will redirect the traffic to the different instances to distribute the traffic(load) evenly across the instances. 

<img width="506" alt="Hnet com-image" src="https://user-images.githubusercontent.com/12581835/172000085-84e24238-dbd7-4321-90aa-16c9b0892c9b.png">

__Why use ELB?__
- Spread load across multiple downstream instances. 
- Expose single point of access (DNS) to your application.
- Seamlessly handle failures of downstream to your instances.
- Regular health checks on instances.
- Provide SSL termination (HTTPS) for your websites.
- Enforce stickiness with cookies.
- High availability across zones.
- Separate public traffic from private traffic.

__Features__
- ELB is a _managed service._ i.e. 
	- Managed Services mean AWS handles availability, upgrade, maintenance, etc.
- Costs less to setup your own Load Balancer, but too much hassle to manage it.
- AWS ELB comes integrated with many AWS offerings / services :
	- EC2, EC2 Auto Scaling Groups, Amazon ECS
	- AWS Certificate Manager, Cloud Watch.
	- Route 53, AWS WAF, AWS Global Accelerator.

__Health Checks :sweat:__
- Crucial for ELBs.
- Notify Load Balancers if the instances are available to reply to requests.
- Health Check is done on a port and a route (/health is common)
- If the response is not 200 (OK), then the instance is unhealthy and the load balancer won't send traffic to that instance.
<img width="354" alt="Health Check" src="https://user-images.githubusercontent.com/12581835/172000869-844b8cd8-f294-4307-8208-0dddd12f9de5.png">

### Load Balancer Security Groups
If the EC2 instances and the Load Balancers communicate toogether, how do they secure the traffic?
<img width="398" alt="Load Balance Security Rules" src="https://user-images.githubusercontent.com/12581835/172003939-0799adf3-4368-4410-9bc5-667908942e09.png">

Since the ELB _fronts_ the EC2 instances, it faces all the traffic from outside. So, it's security group rules will look like below:
```
SG-ELB-1 : Security Group Rules for ELB 
Allow HTTP from 0.0.0.0, Port 80.
Allow HTTPS from 0.0.0.0 , Port 443.
```
Whereas, the instance talks to only the ELB as it receives the outside traffic from it. So, it security group rules will look like below : 
```
SG-Ec2-A : Security Group Rules for an EC2 instance connected to ELB. 
Allow HTTP from SG-ELB-1. Port 80
```


### Types of Load Balancers
AWS has 4 kinds of Load Balancers:

| **Load Balancer**         	| **Year** 	| **Protocol**                                     	|
|---------------------------	|----------	|---------------------------------------------------	|
| Classic Load Balancer     	| 2009     	|  HTTP, HTTPS, TCP, SSL                            	|
| Application Load Balancer 	| 2016     	| HTTP, HTTPS, WebSocket                            	|
| Network Load Balancer     	| 2017     	| TCP, TLS(Secure TCP), UDP                         	|
| Gateway Load Balancer     	| 2020     	| Operates at layer 3 (Network Layer) - IP Protocol 	|

Recommended to use the newer generation Load Balancers. Some LBs can also be setup as internal or private ELBs.

#### 1. Classic Load Balancer CLB
- Supports TCP (Layer 4), HTTP & HTTPS (Layer 7)
- Health Checks - TCP or HTTP based.
- Fixed hostname XXX.region.elb.amazonaws.com


![Hnet com-image (4)](https://user-images.githubusercontent.com/12581835/172464928-c87b25f3-ecfc-42e8-8a58-5310a670d564.png)

