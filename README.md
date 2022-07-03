

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
4. __EC2 Instance Metadata__ - Very powerful feature.
	- Allows EC2 instances to "learn about themselves" without using an IAM Role for that purpose.
	- URL - http://169.254.169.254/latest/meta-data
	- You can retrieve the IAM Role, but not IAM Policy
	- ...and a lot of stuff about your ec2 instances. 




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


#### 2. Application Load Balancer ALB
- ALB is a Layer 7 load balancer.
- Why "Application"?
	- Load balancing to multiple HTTP applications across machines (__target groups*__ - groups of entities where LB can direct the traffic selectively.)
	- Load balancing to multiple  applications on the same machine (ex: containers)
- Support for HTTP/2 and Web Socket
- Support redirects (Ex: from HTTP -> HTTPS)
- Supports route routing to different target groups : _(diagram below)_
	- Routes based on URL paths (Ex: traffic will be distributed across _example.com/users_ and _example.com/posts_)
	- Routes based on hostname (Ex: _one.example.com_ and _other.example.com_)
	- Based on query string and headers (Ex: _example.com/users?id=123&order=false_)
- ALBs are great fit for micro services & container-based applications. 
- Enable Port mapping to a dynamic port in ECS.
- In comparison, we'd need multiple CLBs per application.

![Application Load Balancer](https://user-images.githubusercontent.com/12581835/172230494-e0d8d5ae-264d-487f-bd43-fda60b8a8dc4.png)

- What are target groups?
	- EC2 instances (can be managed by AutoScaling Group) - HTTP
	- EC2 Tasks (managed by ECS)
	- Lambda functions - HTTP request -> JSON
	- IP Addresses - must be private IPs
- Health Checks are done at Target Group level.
- ALM can route to multiple target groups.

- Important points : 
	- ALB provides a __fixed hostname__ like XXX.region.elb.amazonaws.com
	- Application servers (i.e. EC2 behind the ELBs) don't see the IP of the client (i.e. User) directly.
		- True IP and Port of the client is inserted in the _X-Forwarded-For_ & _X-Forwarded-Port_ header of the packet.

> TODO : All the Load Balancers need a 6-7 line Summary each.


#### 3. Network Load Balancer NLB
- NLB is a Layer 4 load balancer. Generally, ideal for extreme performance. 
	- Handle millions of request per sec. Less than 100ms latency (vs 400ms for ALB)
- NLB has __one static IP per AZ__,  and supports assigning Elastic IP.
- Not included in AWS Free Tier. :anguished:
- Since NLB accepts and redirects TCP and UDP traffic, we have to make sure that the Security Group for our EC2 instances accepts TCP traffic from anywhere.


#### 4. Gateway Load Balancer NLB
- GLB is a Layer 3 load balancer - Network Layer IP Packets. 
- Deploy, Scale and mange a fleet of 3rd party network virtual appliances in AWS.
- Example : Firewalls, intrusion detection, prevention systems, payload manipulation, etc.
- __Model Use Case :__ Let's say you want to analyse all the traffic before it reaches the application servers. GLB takes the traffic from the public and then sends it to your intermediary machines (say _appliances_) that analyse/pre-process the traffic. Once it's processed, then traffic is sent back to the GWL and GWL takes it to the Application servers. 
- Combines following functions:
	- Transparent network gateway - Single entry/exit for all traffic.
	- Load Balancer - distributes traffic to your virtual appliances.
- GWL - Target Groups
	- EC2 instances
	- IP Adresses (must be private IPs)


#### Sticky Sessions (Session Affinity) 
- __Issue:__ Since the ELBs distribute traffic to different machines, it might be possible that users lose their data (let's say a WIP code on repl.it) once they refresh the application cos they got re-assigned to a different EC2 machine.
- __Solution:__ Implement stickiness so that a client is always redirected to the same instance behind a load balancer. And doesn't lose his session data.
- Provided by CLB and ALB.
- Uses "cookie" for stickiness. Cookies have expiration date of stickiness.
- Enabling stickiness may bring imbalance too the load over the backend EC2 instances.
- :cookie:  Types :
	- Custom cookie
		- Generated by the target.
		- Can include any custom attributes required by the application.
		- Cookie name must be specified individually for each target group
	- Application cookie 
		- Generated by the load balancer.
	- Duration-based Cookies

#### Cross-Zone Load Balancing
1. __With Cross Zone Load balancing__ : Each ELB distributes traffic evenly across all instances in AZ. 
	- Traffic per instance = 100/(No. of instances in total)
	- Traffic per AZ = 100/(No. of AZ)
2. __Without Cross Zone Load Balancing__ : Requests are distributed in the instances of the node of the ELB. 
	- Traffic per instance = 100/(No. of instances in an AZ)
	- Traffic per AZ = 100/(No. of AZ)

ALB - Always ON. No charges for inter AZ data.

####  SSL Certificates
- WTF? - SSL certificates allows traffic between your clients and your load balancer to be encrypted in-transit. That's it. 
- __SSL__ refers to Secure Socket Layer. __TLS__ refers to Transport Layer Security, it's newer. SSL and TLS are often used interchangeably.
- Public SSL issued by Certificate Authorities (Ex : Go Daddy, etc.)
- Certificates can be managed by __ACM__ (AWS Certificate Manager) 
__SNI - Server Name Indication__
- Solves the problem of loading multiple SSL certificates on one web server (to serve multiple websites).
- As per SNI, we only need to indicate the hostname and the server will find the correct certificate, else the default one. 
- Works only with ALB & NLB and CloudFront. Not for CLB-only 1 certificate.
![How SNI works](https://user-images.githubusercontent.com/12581835/172464928-c87b25f3-ecfc-42e8-8a58-5310a670d564.png)


#### Connection Draining (aka Deregistration Delay)
- __Idea__ - Time to complete "in-flight requests" while the instance is de-registering or unhealthy. Wait for "existing" connections to complete.
- When the instance starts de-registering, any new requests will be assigned to the healthy/active instances.
- _What happens during a  sticky session?_ :shrug:
- Between 1 to 3600 seconds. 
- Can be disabled. Set to 0.

---

## AutoScaling Groups :left_right_arrow: :eight_spoked_asterisk:

- Helpful in manage the problem of "Variable load on the web application servers"
	- Ex: During Amazon's online sale or Uber's surge in ride requests, there might be too much load and we may need to scale out i.e. add more servers. Similarly, during the dull hours like midnight, the traffic reduces and we don't need that many servers soo why pay for them?
- In cloud, we can create and get rid of servers very quickly.
- __Idea:__
	- Scale out (add EC2) oor Scale in (reduce EC2) to match a increased or decreased load, respectively.
	- Ensure we have a min or max # of instances running (default settings)
	- Automatically register new instances to the Load Balancer.
	-![What is Amazon EC2 Auto Scaling? - Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/images/as-basic-diagram.png)

- __Features :__
	- Launch Config
		- AMI + Instance Type
		- EC2 User data
		- EBS Volumes
		- Security Groups
		- SSH Key Pair
	- Min / Max / Initial Capacity
	- Network + Subnets Information
	- Load Balancer Information
	- Scaling Policies - set of rules that tell ASG when to scale-out or scale-in.
- __Auto Scaling Alarms :__
	- Scale an ASG based on CloudWatch Alarm that monitors a metric (like Avg. CPU)
	- Alarms help in triggering any scale-out or scale-in policies.

- __Things to know :__
	- Scaling Policies can be on CPU, Network .. can be any custom metrics or based on a schedule (pre-defined peak and dull times)
	- ASGs use Launch config or Launch Templates (newer)
	- IAM roles attached to an ASG will get assigned to EC2 instances.
	- ASG are free. 
	- If ASG resources get terminated (for whatever reason, it will add new ones as a replacement. 

- __Auto-Scaling Policies :__
	1. Target Tracking Scaling
		- Easiest to setup. Ex: Want avg. ASG CPU to stay @ 40%.
	2. Simple/Step Scaling
		- When a Cloud Wathc alarm is triggered, add or remove units accordingly.
	3. Scheduled Actions
		- Anticipate a scaling based on known usage patterns. Ex: Increase the min capacity of Uber cab booking instances to 50 at 5pm on Fridays.
	4. Predictive Scaling 
		- Continuously forecast load and schedule scaling ahead. 
5. Scaling Cooldowns - After a scaling activity, you enter a cooldown period (default 300 seconds). No new termination or launch of EC2 happens during cool down. 
6. Note: Use ready-to-use AMI to reduce configuration time.

- Good Metrics:
	- CPUUtilization 
	- RequestCountPerTarget - # of requests per EC2 instance is stable. 
	- Avg Network In/Out - 
	- Any custom metric

##### Default Termination Policy
How they get terminated? 
1. Pick the AZ with the most number of instances. 
2. Delete the instances with the oldest launch config.
__Life Cycle Hooks__

![Screenshot 2022-06-08 at 23 59 35](https://user-images.githubusercontent.com/12581835/172724768-7beeb395-5f80-4652-972a-ea09117c4295.png)




# RDS
### Overview
- Relational Database Service. 
- Managed DB Service for DB that use SQL as a query language.
- Allows you to create databases in the cloud that are managed by AWS
	- Postgres
	- MySQL
	- MariaDB
	- Oracle
	- MS-SQL
	- Aurora
- __Confusion :__ RDS is just a service that provides us with installed DBMS software like oracle and postgres, rather than deploying it on our own .

- RDS vs "Deploying DB on EC2 yourself" i.e. _Out-of-the-box vs DIY_
	- Automated provisioning, OS patching
	- Continuous backups, restore to a point in time!
	- Monitoring dashboards
	- Read replicas to increase read performance.
	- Multi-AZ setups for DR (disaster REcovery)
	- Scaling capability (horizontal and vertical)
	- Storage backed by EBS (gp2 or io1)
	- *Can not SSH* into the instance that runs RDS. 

### RDS Backups
1. Automatically enabled
2. Automated Backups:
	- Daily full backup of the DB.
	- Txn Logs backups by RDS every 5 min.
	- Ability to restore to any point-in-time.
	- 7 days retention can be increased to 35 days.
3. DB Snapshots
	- Not the same as "Backup" as they are manually triggerd by the user. i.e. Not Automated.
	- Retention as long as we want.

### RDS - Storage Auto Scaling 
- Helps you increase storage on your RDS DB instance dynamically.
- When you are running out of free database storage, it scales automatically! _Manual scaling not required._
- __Max Storage Threshold__
- Modify storage if :
	- Free storage is less than 10% of allocated storage
	- Low-storage lasts at least 5 minutes.
	- 6 hours have passed since last modification.
- Useful for apps with unpredictable workloads. 

### Read Replicas :page_facing_up: 
They help in easing the load on the main DB in case of huge number of READ requests.
- Create another DB instances that servers can read data from. This replica can be reserved for READ requests.
- Max 5 read replicas allowed.
- Data between the read replicas and the main DB is __eventually consistent/ASYNC__ i.e. a read from Main DB and the read replicas may not be same. Data from read replicas may lag behind. 
- Read Replica can be promoted to become their own DB.
- Eg : Production DB is your main DB. But your reporting service can use a a read replica of the main db as reporting only requires READ operations. 
- __Network Costs__  : 
	- Data moving within the same Region is free. _Make sure to keep Read Replicas and Main DB in the same AZ to avoid high costs._
	- Data moving to different Regions is not free and has a cost. 
 

### RDS Multi-AZ (Disaster Recovery)
They help in maintaining an instantaneously consistent/SYNC backup DB to manage master DB failover in case of a disaster.
- SYNC replication
- One DNS name - automatic app failover to standby
- Increase __availability__
- Failover in case of loss of AZ, instance, storage, etc.
- No manual intervention in apps.
- Not used for scaling.

### RDS Security - Encryption
- __At rest Encryption__
	- Can encrypt master and read replicas using AWS KMS.
	- Encryption has to be defined at launch time. After that, you can't change the settings.
	- Transparent Data Encryption (TDE) available for Oracle and SQL server.
- __In-flight encryption__ (_data being send from clients to RDS_)
	- SSL Certificates to encrypt data into RDS in flight.
	- Provide SSL Options with trust certificate when connecting to DB.
- __Encryption Operations :__
	- Snapshots of un-encrypted RDS databases are un-encrypted.
	- Snapshots of encrypted RDS databases are encrypted.
	- __How to convert un-encrypted RDS to an encrypted one?__
		- Take it's snapshot. Enable Encryption on the snapshot. Restore the DB from the encrypted snapshot. 

### RDS Security - Network and IAM
- Network Security
	- RDS DBs are usually deployed within a private subnet, not in a public one.
	- RDS security works by leveraging SecGroups (similar to EC2) - it controls which IP/SecGroups can communicate with RDS.
- Access Mgmt
	- IAM Policies help control who can manage AWS RDS (through the RDS API)
	- Traditional UserName and Password can be used to login into the database.
	- IAM-based authentication can be used to login into RDS MySQL and PostgreSQL
- IAM Authentication
	- IAM  datbse authentication works with MySQL and PostgresSQL
	- No need of pwd, __just an authenticaltion token - valid for 15 mins.__
	- Benefits :
		- Network in/out must be encrypted
		- IAM to centrally manage users instead of DB.

### RDS Security - Summary 
<TBD>


## Amazon Aurora
:warning: Asked in Exam frequently
- Aurora is a proprietary technology from AWS. (not open sourced)
- Postgres and MySQL are both supported as Aurora DB (driver compatibility)
- Why Aurora?
	- It's 'cloud-optimised' and claims 5x performance over MySQL on RDS and 3x performance over PostgresSQL
	- Aurora storage automatically grows in increments of 10GB, upto 128 GB.
	- Can have 15 replicas, replication is faster.
	- Failover is instantaneous. It's highly available. (__Failover__ *is a backup operational mode that automatically switches to a standby database, server or network if the primary system fails, or is shut down for servicing*.)
	- Aurora costs more than RDS (20% more) - but is more efficient.

### Aurora High Availability and Read Scaling
- 6 copies of your data across 3 AZs
	- 4/6 needed for writes
	- 3/6 needed for reads
	- Self-healing with peer-to-peer replication
	- Storage is striped across 100s of volumes
- One Aurora instance takes writes i.e. __Master__
- Automated failover < 30 sec
- Master + upto 15 read replicas 
- Support for cross region replication

### Aurora DB cluster
- Writer Endpoint - The client talks to the writer end point. the Writer end point talks to the Master DB.
- Reader Endpoints - The client talks to the reader endpoint. The reader endpoint connects with one of the many read replicas of Aurora DB. Also does load balancing at a connection-level.
- Important stuff.

![screenshot-2022-06-26-at-21-25](https://user-images.githubusercontent.com/12581835/175830650-fd8659c5-7127-4f23-87c4-df997836d0b1.png)

#### Aurora Features
 - Automatic fail-over
 - Backup and Recovery
 - Isolation and security
 - Industry compliance
 - Push-button scaling
 - Automated Patching with Zero
 - Downtime Advanced Monitoring
 - Routine Maintenance
 - Backtrack: restore data at any point of time without using backups

#### Aurora Security
Similar to the RDS.
 - Encryption at rest using KMS.
 - Automated backups, replication.
 - Encryption in flight using SSL ...

#### Aurora Advanced Concepts
1. AutoScaling
	- How the autoscaling happens for upto 15 read replicas in Aurora?
	- As the ASG detects increased demand on the Aurora read replica instances, it increases the instances.
	- Similarly, the Reader Endpoint gets _extended_ to cover these new replicas.
2. Custom Endpoints
	- We can have different custom endpoints on different type of read replicas. 
	- For Eg : You can have bigger and more powerful instances to run some read replicas. These highly performant read replicas handle all the analytical queries.
	- Reader Endpoints not generally used once the Custom ones are defined.
	- Custom Endpoints for different workloads on subset of Aurora read replicas.

#### Aurora Serverless
1. Automated database instantiation with Auto-Scaling
2. Good for infrequent, intermittent or unpredictable workloads
3. No capacity planning needed
4. Pay per second, can be more cost-effective
Client talks to a "Proxy Fleet" managed by AWS. In the backed, many aurora instances will be created in a serverless fashion based on workload and not capacity planning is needed.

#### Aurora Multi-Master
:warning: Exam Question
- IN case you want immediate failover for write node (HA)
- Every node does R/W - vs promoting a RR as the new master.
![Let's see](https://user-images.githubusercontent.com/12581835/175878664-c8a63ef3-a6c6-4b10-a3d2-33f1d1572621.png)


#### Global Aurora
1. Aurora Cross region read replicas
	- Useful for disaster recovery
	- Easy to setup
2. Aurora Global Database
	- 1 Primary region
	- Upto 5 secondary read-only regions
	- Up to 16 read replicas per secondary region
	- Helps for decreasing latency
	- Promoting another region has an RTO < 1 minute

#### Aurora Machine Learning
- Supports ML services - SageMaker and Comprehend
- Simple, optimised and secure integrtion between Aurora and ML to your applications via SQL


## Amazon ElastiCache

ElastiCache helps to manage caching technologies(Redis and Memcahed), the same way RDS helps in managing Relational Databases.
- Caches are __in-memory databases__ with really high performance and low latency.
- Helps to reduce load off of databases for read intensive workloads.
	- If a client keeps logging into travel app to look for train tickets, keep them in the cache and don't perform a read operation on DB everytime.
- Helps make your application stateless.
- AWS takes care of OS maintenance, patching, optimization, etc.
- Using ElastiCache involves heavy application code changes. Not a simple plug-n-play.

#### Use Case 1 : DB Cache
Commonly queried data from DB is stored in the cache for quicker retrieval and reduce load on the DB.
Data is queried from DB, when the data isn't present in ElastiCache also known as a "Cache miss". 

#### Use Case 2 : User Session Store
- User logs into any instances of the application. 
- App writes the session data in ElastiCache
- User hits another instance running the App
- Instance retrieves the session data from Cache and is already logged in. 
- This leads to a "Stateless" application. 

#### Difference between Redis and Memcached
| Redis                                                   	| Memchached                                     	|
|---------------------------------------------------------	|------------------------------------------------	|
| Multi-AZ Failover                                       	| Multi-node for partitioning of data (sharding) 	|
| Read Replicas to scale reads and have high availability 	| No high availability (replication)             	|
| Data Durability using AOF                               	| Non persistent                                 	|
| Backup and restore features                             	| No backup and restore                          	|
|                                                         	| Multi-threaded architecture                    	|


#### Cache Security
- All caches in ElastiCache
	- Do not support IAM authentication
	- IAM policies are only used for AWS API-level security like creating and deleting a cache.
- Redis AUTH
	- Can set a "password/token" when creating a Redis cluster
	- Extra security on top of SecGroup
- Memcached 
	- Supports SASL-based authentication

#### ElastiCache Patterns
1. __Lazy Loading__ - All read data is cached. Becomes stale.
2. __Write Through__ - Adds or update data in the cache when written to a DB. 
3. __Session Store__ - Store temporary session data in a cache.

![Lazy Loading ElastiCache](https://user-images.githubusercontent.com/12581835/175893395-f6cd1c52-ec16-4b8f-b9d3-e29f54033c8a.png)

ElastiCache Redis UseCase
- Gaming leaderboards are complex
- Redis Sorted sets guarantee both uniqueness and element ordering
- Each time a new element added, it's ranked in real time, then added in correct order.


---

# Route 53 :spider_web:

What is DNS? 
- Translates an IP into a human readable format.
- Eg : www.google.com => 172.217.18.36
- DNS uses hierarchical naming structure like below : 
	> .com
	> example.com
	> www.example.com
	> api.example.com

Important Terms:
- Domain Registrar - Amazon Route 53, GoDaddy
- DNS Records - A, AAAA, CNAME
- Zone File - contains DNS Records
- Name Server - resolves DNS queries. Back and forth.
- Top-Level Domain - .com, .us, .in
- Second-Level Domain - amazon.com, google.com, etc. 
 <img width="658" alt="Screenshot 2022-06-28 at 22 40 25" src="https://user-images.githubusercontent.com/12581835/176282836-32445077-ab6a-4611-893e-fd90ad8b2b3a.png">

> DNS Name resolution starts from the "root". 


## Route 53
- Highly available, scalable, fully-managed service.
- Authoritative DNS , that means, the customer (you) can updated the DNS Records.
- Route 53 is also a Domain Registrar i.e. register your domain.
- Ability to check the health of your resources within Route 53.
- Only AWS Service to provide 100% availability SLA.


#### Route 53 - Records
- Define how you want to route traffic for a domain.
- Each records contains:
	- Domain/Subdomain name - Ex: example.com, 
	- Record Type - Ex: A or AAAA
	- Value - Eg: 12.34.56.78
	- Routing Policy - how Route 53 responds to queries
	- TTL - amount of time the record cached at DNS Resolvers. _Time to Live_
- Route 53 supports following records types :
	- A/AAAA/CNAME/NS (Exam)
	- CAA/DS/MX/NAPTR/PTR etc...

#### Route 53 - Record Types
- **A** - maps a hostname to IPv4
- **AAAA** - maps a hostname to IPv6
- **CNAME** - maps a hostname to anoother hostname
	- Target domain name must have an A or AAAA record
	- Can't create a CNAME records for the top node of a DNS namespace(Zone Apex)
- **NS** - Name servers for the hosted zones.

#### Route 53 - Hosted Zones
- Container of records that define how the traffic is routed to a domain and it's subdomains.
- Public Hosted Zones - specify how to route traffic on the internet.
- Private Hosted Zones - contain records that specify how you route traffic within one or more VPCs.
- Fees = $0.50 per month per hosted zone


#### Route 53 - Records TTL
For TTL = 300ms, the client can cache the result from the DNS Server and not send any new requests for that duration. 
As TTL increases, less traffic on Route 53 and everyone has outdated records, possibly.


#### CNAME vs ALIAS
- AWS Resources (Loadbalancer, CloudFront) expose an AWS hostname.
	- Maybe, you want to map the hostname lb1.us-east-e.alb.amazonaws.com to myapp.domain.com
1. __CNAME (Canonical Name)__
	- Points to a hostname to any other hostname. (app.mydomain.com => blabla.anything.com)
	- ONLY FOR NON ROOT DOMAIN (aka.something.mydomain.com)
 2. __Alias__
	 - Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com)
	 - WORKS FOR BOTH  ROOT DOMAIN AND  NON-ROOT DOMAIN (aka.something.mydomain.com)
	 - Native health check
	 - It's free.

#### Route 53 - Alias Records
- MAps a hostname to an aWS resource
- An extension to DNS functionality
- Automatically recognises changes in the resource's IP Addresses.
- Unlike CNAME, it can be used for the top node of a DNS Namespace. Ex; example.com
- Alias record is always of type A/AAAA for AWS resources.
- You can't set TTL.
- Targets : ELB, CloudFront, API GAteWay, BeanStalk, VPC Interface Endpoints, S3 Websites, Global Accelerator, Route 53 Records.
- Cannot set ALIAS records for an EC2 DNS name.

#### Route 53 - Routing Policies
- Define how Route 53 responds to DNS queries. Not really "routing" any traffic.
- Policies :
	- **Simple** - Route traffic to a singe resource. Can specify multiple values in the same record. One values chosed randomly by the client.
		- Eg : Client asks for foo.example.com. Route53 responds with [11.22.33.44.55 , 12.34.56.78, 110.20.30.40 ]. 
	- **Weighted** - Controls the % of requests that go to each specific resource. DNS Records must have the same name and type. 
		- Use cases : Load Balancing between different regions. A/B testing features.
		- One record is zero means 
	- **Latency based** - Redirect the resource that has the least latency to user.
		- Can use health checks.
		- useful when latency is a priority
		- Latency is based on traffic between users and AWS Regions. 
	- **Geolocation** - Routing based on user location. Should have a "Default" records in case there is no match on location.
		- Use cases : Website localization, restrict content distribution, load balancing.
		- Can use health checks.
		
	- Multi-Value answer - 
		- Not to be consufsed with ELB.
	- Geoproximity - 

#### Route 53 - Health Checks
- HTTP health checks are only for public resources
- Types:
	1. __Health checks that monitor an endpoint.__
		- 15 global health checkers will check the endpoint health. A 2xx and 3xx code response means "OK" 
		- Healthy/UnHealthy threshold - 3 default
		- Interval - 30 sec
		- Supported protocol : HTTP, HTTPS, TCP
		- If > 18% health checkas report healthy, then Route53 considers it healthy.
		- Health checks can be setup to pass/fail based on the text in the first 5120 bytes of the response. 
		
	2. __ Calculated health checks__
		- Health Checks that monitor other health checks. 
		- Combine the results of multiple health checks into a single health check.
		- You can use OR, AND, or NOT.
		- Can monitor upto 256 child health checks. Can specify the threshold to pass parent health check.
	3. __Private Hosted Zones Health Checks__
		- Route 53 are outside the VPC.
		- They can't access private endpoints (private VPC or on-premise resources)
		- You can create a CloudWatch Metric and attach an Alarm to it, then create a health check that checks the Alarm itself.


#### Domain Registrar vs DNS Service
- You buy or register your domain name with ANY Domain Registrar typically by paying annual charges (e.g. GoDaddy, Amazon Registrar, etc.) 
- Domain Registrar usually provides you with a DNS service too manage your DNS Records.
- But you can use another DNS Service to amange your DNS records.
- **Example** : purchase the domain from GoDaddy and use Route53 to manage your DNS Records.
- To use a 3rd party domain on Route 53, 
	1. Create a hosted Zone in Route 53
	2. Update NS records on 3rd party website to use Route 53 Name Servers




# Solutions Architectures - Best Practices
### 1. Instantiating Applications quickly
- EC2 instances
	- **Use a Golden EMI** : Install your applications, OS dependencies etc. beforehand and launch your EC2 instance from the Golden AMI
	- **Bootstrap using User Data**: For dynamic configuration, use USer Data scripts
	- __Hybrid__: mix Golden AMI and user data (Elastic Beanstalk)
- RDS Databases:
	- Restore from a snapshot : the databases will have schemas and data ready!
- EBS Volumes: 
	- Restore from a snapshot: the disk will already be formatted and have data! 


## Elastic BeanStalk :seedling:

##### Why? To solve common developers problems on AWS.
__Problems__
- Managing infra
- Deploying code
- Configuring all the DBs, ELBs, etc.
- Scaling concerns.

__Commonality__
- Most web apps have the same architecture (ALB+ASG)
- All the developers want is for their code to run.... 
- ...Possibly, consistently across different applications and environments.

### Elastic Beanstalk Overview
- Elastic Beanstalk is a developer centric view of deploying an app like D-R-Y, K-I-S-S, etc...
- It uses all the components we've seen before : EC2, ASG, ELB, RDS, etc...
- Managed Service:
	- Automatically handles capacity provisioning, load balancing, application health monitoring, instance configuration, ...
	- Just the __application code is the responsibility of the developer__
- We still have full control over the configuration 
- Beanstalk is free, but user pays for the  underlying instances

### Elastic Beanstalk Components
- __Application__: Collection of elastic beanstalk components (environments, versions, configs, etc..)
- __App Version__: An iteration of your application code. 
- __Environment__: 
	- Collection of AWS resources running an application version (only one app verion at a time)
	- Tiers : Web Server Environment Tier (clients accessing app, we use ELBs) and Worker Environment Tier (clients not accessing app, we use SQS queue)
	- You can create multiple environments (dev, test, prod, etc..)

![](https://user-images.githubusercontent.com/12581835/177007893-1d8cc3b5-c4ea-4f49-a5b5-19f3bb6b2404.png)

---

# Amazon S3 :bucket:

#### Overview
- "Storage" solution. Stores __objects__(files) in 'buckets' (directories)
- Buckets must have a _globally unique name_
- Region-level service.
- Naming convention:
	- No uppercase and underscore. 
	- 3-63 characters long. 
	- Not an IP.
	- Must start with lowercase or number.
- Instantly Consistent!!! 

#### Objects
- Objects (files) have a _key_
- __Key__ is the FULL path i.e. `s3://my-bucket/myfile.txt` or `s3://my-bucket/my_folder_1/myfile.txt` 
	- Key = Prefix (`s3://my-bucket/my_folder_1/`) + Object name (`myfile.txt`)
- No concept of 'directories' within buckets
- Max size of Object = 5TB. But cannot upload anything to bucket more than 5GB at a time - must use 'multi-part' upload. _Batches_
- __Metadata__ - List of  Key-Value pairs 
- __Tags__ (unicode key-value pair) - useful for security/lifecycle
- __Version ID__ 

#### S3 Versioning
- You can version your files in Amazon s3.
- Versioning enabled at bucket level.
- Same key(i.e. prefix+filename) overwrite will increment the "version":1,2,3..
- Best practise to use versioning :
	- Protect against unintended deletes.
	- Easy to rollback
- Files prior to versioning being enabled will have version "null"
- Suspending versioning doesn't delete the previous versions.
- Deleting while versioning creates "Delete Marker". 

#### S3 Encryption 
:warning: Exam asks questions on the apt type of encryption based on the situation.

S3 has "Default Encryption" Option.

There are 4 methods of encrypting objects in S3
1. __SSE-S3__ 
	- Using keys handled and managed _by Amazon S3_
	- Server-side encryption
	- AES-256
	- Header value : `"x-amz-server-side-encryption":"AES-256"`
	 
2. __SSE-KMS__
	- Leverage keys handled and managed _by Amazon Key Management Service_
	- Server-side encryption
	- KMS Advantages : Gives user control and auditing capability over usage i.e. _"Who has access to what keys?"_
	- Header value : `"x-amz-server-side-encryption":"aws-kms"`

3. __SSE-C__
	- Server side encryption fully managed by customer outside of AWS
	- Amazon S3 does not store the encryption keys
	- HTTPS must be used.
	- Encryption key must be provided in HTTP headers, for every HTTP request made

4. __Client-Side Encryption__
	- Encryption happens before sending to S3
	- Decryption happens when retrieving from S3
	- Use encryption library like Amazon S3 Encryption Client

Encryption in transit
- Amazon S3 exposes:
	- HTTP endpoint: non encrypted
	- HTTPS endpoint : encryption in flight
- You're free to use the endpoint you want, but HTTPS is recommended
- HTTPS mandatory for SSE-C
- Encryption-in-flight also called SSL/TLS

#### S3 Security and Bucket Policies
- User based
	- IAM Policies - _Which API calls should be allowed for a specific user from IAM console?_
- Resource based
	- Bucket Polices - bucket-wide rules from the S3 console
	- Object Access Control Lists - finer
	- Bucket Access Control Lists - granular access
- IAM principal (role, user,etc.) can access an S# object if either IAM permission OR resource policy allows it AND there is not explicit deny

__S3 Bucket Policy__
- JSON Document dictating the following : 
	- Resources : obj, buckets
	- Actions : set of APIs 
	- Effect : Alloow/Deny
	- Principal : The account or user to apply the policy to
- Use S3 buket policy :
	- grant public access
	- force objects to be encrypted at upload
	- grant access to another account

__Other __
- Networking: Supports VPC endpoints for instances in VPC without www access)
- Logging and Audit : S3 access can be stored in other S3 bucket. API calls can be logged in Cloud Trail
- Pre-signed URLs : URLs that are valid only for a limited time (ex: premium video, UFC live stream, prootected cloud photo sharing)


#### S3 Websites 
- S3 can host static websites and have them available to www
- Website URL will be :
	- `<bucket-name>:s3-website-<AWS-region>.amazonaws.com`
- If you get a 403 error, make sure to allow public reads.

	
#### CORS
- An origin is a scheme (protocol), host (domain) and port.
- CORS = Cross Origin Resource Sharing
- Example of Same origin browsing : `http://example.com/app1` to  `http://example.com/app2`
- Example of Different Origins : `http://www.example.com/` to `http://other.example.com/`
- Requests won't be fulfilled unless the other origin (i.e. `example.com`) allows for the requests, using __CORS Headers__
	- Ex: Access-Control-Allow-Origin
- Pre-flight request asks the other website if CORS is allowed or not. 
- What does mean for S3? :warning: very common exam question!
- Cross-Origin Resource Sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. To learn more about CORS, go here: https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html

#### S3 Access Logs
- Can log all access to S3 buckets for audit purposes
- Any request made to S3 from any acct. authorized or denied will be logged into another S3 bucket
- That data can be analyzed using data analysis tools or Amazon Athena
- :warning: Keep your application bucket and monitoring buckets separate to prevent an infinite loop where the bucket monitors itself and logs.


#### S3 Replication
- 2 types : CRR = Cross Region Replication and SRR = Same Region Replication
- Asynchronous Replication
- Must Enable versioning
-  CRR Use cases : compliance, lower latency access, replication across accounts
- SRR Use cases : log aggregation, live replication b/w prod and test accounts
- After activating, only new objects are replicated. Optionally, can replicate existing objects using __S3 Batch Replication__
- Delete Markers can be replicated. However, Deletions with a version Id are not replicated(to avoid malicious delete)
-  No "chaining" replication i.e. If B2 is replication of B1 and B3 is a replication of B2, then objects in B1 are not replicated in B3. Not transitive.
