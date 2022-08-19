---
layout: post
title: AWS Interview questions
date: 2018-03-27 15:50
author: tmasabari
comments: true
categories: [AWS, Interview Preparation]
---
<ul>
 	<li>https://www.edureka.co/blog/interview-questions/top-aws-architect-interview-questions-2016/</li>
 	<li><a href="http://www.spiritsofts.com/tag/aws-technical-interview-questions-pdf-download">http://www.spiritsofts.com/tag/aws-technical-interview-questions-pdf-download</a></li>
 	<li>https://intellipaat.com/interview-question/amazon-aws-interview-questions/</li>
 	<li>https://www.whizlabs.com/blog/aws-solution-architect-interview-questions/</li>
 	<li>https://www.svrtechnologies.com/aws-interview-questions/top-50-aws-interview-questions-and-answers-pdf</li>
</ul>
<div>Cloud</div>
<div>

<strong>1) Have you worked on containers ?</strong>
Containers are form of lightweight virtualization, more heavy than chroot but lighter than hypervisors. They provide isolation among processes while using same kernel as the host machine, and cgroups functionality within kernel. But container formats differ among themselves in a way that some provide more VM-like experience while other containerize only application.

LXC containers are most VM-like and most heavy weight, while Docker used to be more light weight and was initially designed for single application container. But in more recent releases Docker introduced whole machine containerization features so now Docker can be used both ways. There is also rkt from CoreOS and LXD from Canonical, which builds upon LXC.

<strong>2) What is Kubernetes? Explain</strong>
It is massively scalable tool for managing containers, made by Google. It is used internally on huge deployments and because of that it is maybe the best option for production use of containers. It supports self healing by restating non responsive containers, it pack containers in a way that they take less resources and has many other great features.

<strong>3) What is the function of CI (Continuous Integration) server ?</strong>
CI server function is to continuously integrate all changes being made and committed to repository by different developers and check for compile errors. It needs to build code several times a day, preferably after every commit so it can detect which commit made the breakage if the breakage happens.

Note: Other available and popular CI tools are Jenkins, TeamCity, CircleCI , Hudson, Buildbot etc

<strong>4) What is Continuous Delivery ?</strong>
Is it practice of delivering the software for testing as soon as it is build by CI (Continuous Integration) server’s. It requires heavy use of Versioning Control System for so always available to developers and testers alike.

<strong>5) What is Vagrant and what is it used for ?</strong>
Vagrant is a tool that can create and manage virtualized (or containerized) environments for testing and developing software. At first, Vagrant used virtualbox as the hypervisor for virtual environments, but now it supports also KVM.

<strong>6) Do you ever used any scripting language ?</strong>
As far as scripting languages go, the simpler the better. In fact, the language itself isn’t as important as understanding design patterns and development paradigms such as procedural, object-oriented, or functional programming.

Currently, several scripting languages are available so the question arises : what is the most appropriate language for DevOps approach? Simply everything , it depends on the context of the project and tools used for example if Ansible used its good have knowledge in Python and if its for Chef its on Ruby.

<strong>7) What is the role of a configuration management tool in devops ?</strong>
Automation plays an essential role in server configuration management. For that purpose we use CM tools , they store information about versions and builds of the software and testware and provide the traceability between software and testware.

<strong>8) What is the purpose of CM tools and which one you have used ?</strong>
Configuration Management tools’ purpose is to automatize deployment and configuration of software on big number of servers. Most CM tools usually use agent architecture which means that every machine being manged needs to have agent installed. My favorite tool is one that uses agentless architecture – Ansible. It only requires SSH and Python. And if raw module is being used, not even Python is required because it can run raw bash commands. Other available and popular CM tools are Puppet, Chef, SaltStack.

<strong>9) What is OpenStack ?</strong>
OpenStack is often called Cloud Operating System, and that is not far from the truth. It is the complete environment for deploying IaaS which gives you possibility of making your own cloud similar to AWS. It is highly modular and consists of many sub-projects so you can pick and chose which functionality you need. OpenStack distribution are available from Red Hat, Mirantis, HPE, Oracle, Canonical and many others. It is completely open source project but some vendors make proprietary distributions.

<strong>10) Classify Cloud Platforms anategory ?</strong>
Cloud Computing software can be classified as Software as a Service or SaaS, Infrastructure as a Service or IaaS and Platform as a Service or PaaS.

SaaS is peace of software that runs over network on remote server and has only user interface exposed to users, usually in web browser. For example salesforce.com.

Infrastructure as a service is a cloud environment that exposes VM to user to use as entire OS or container where you could install anything you would install on your server. Example for this would be OpenStack, AWS, Eucalyptus.
PaaS allows users to deploy their own application on the preinstalled platform, usually framework of application server and suite of developer tools. Examples for this would be OpenShHeroku.

<strong>11) What are easiest ways to build a small cloud ?</strong>
VMfest is one one of the options for making IaaS cloud from VirtualBox VMs in no time. If you want a lightweight PaaS there is Dokku which is basically a bash script that makes PaaS out of Dokku containers.

<strong>12) What is AWS (Amazon Web Services)? Did got chance to work on Amazon tools ?</strong>
AWS provides a set of flexible services designed to enable companies to create and deliver products with greater speed and reliability using AWS and DevOps practices . These services simplify commissioning and infrastructure management , application code deployment , automated software release process and monitoring of the application and infrastructure performance. Amazon used tools like AWS CodeCommit, AWS CodeDeploy, AWS CodePipeline etc, that helps to make devops easier.

<strong>13) What is EC2 ?</strong>
Amazon EC2 Container Service (ECS) is a highly scalable container management service and high performance that supports the Docker containers and allows you to easily run applications on a cluster managed by Amazon EC2 instances.

The EC2 service is inseparable from the concept of Amazon Machine Image – AMI . The May is Indeed the image of a virtual machine That Will Be Executed . EC2 based on XEN virtualization , that’s why it is quite easy to move XEN servers to EC2 .

<strong>14) Do you find any advantage of using NoSQL database over RDBMS ?</strong>
Typical web applications are built with a three-tier architecture. To carry the load, more Web servers are simply added behind a load balancer to support more users. The ability to scale out is a key principle in the world of cloud computing, more and more important in which VM instances can be easily added or removed to meet demand.

However, when it comes to the data layer, relational databases (RDBMS) does not allow a passage to the simple scale and do not provide a flexible data model. Manage more users means adding more servers and large servers are very complex, owners and disproportionately expensive, in contrast to low-cost hardware, the “commodity hardware”, architectures in the cloud. Organizations are beginning to see performance issues with their relational databases for existing or new applications. Especially as the number of users increases, they realize the need for a faster and more flexible basis. This is the time to begin to assess and adopt NoSQL database like in their Web applications.

<strong>15) What are the main SQL migration difficulties NoSQL ?</strong>
Each record in a relational database according to a schema – with a fixed number of fields (columns) each having a specified object and a data type. Each record is the same. The data is denormalized in several tables. The advantage is that there is less of duplicate data in the database. The downside is that a change in the pattern means performing several “alter table” that require expensive to lock multiple tables simultaneously to ensure that change does not leave the database in an inconsistent state.

With databases data, on the other hand, each document can have a completely different structure from other documents. No additional management is required on the database to manage changes in the schemes

</div>
<div></div>
<div></div>
<div id="Section_1" class="accordion-parent">
<div id="Section_1" class="accord-heading active">1. Compare AWS and OpenStack</div>
<div id="Section_1" class="accord-panel showpanel">
<table class="table table-bordered">
<tbody>
<tr>
<td><strong>Criteria</strong></td>
<td><strong>AWS</strong></td>
<td><strong>OpenStack</strong></td>
</tr>
<tr>
<td>License</td>
<td>Amazon proprietary</td>
<td>Open Source</td>
</tr>
<tr>
<td>Operating System</td>
<td>Whatever cloud administrator provides</td>
<td>Whatever AMIs provided by AWS</td>
</tr>
<tr>
<td>Performing repeatable operations</td>
<td>Through templates</td>
<td>Through text files</td>
</tr>
</tbody>
</table>
</div>
</div>
<div id="Section_2" class="accordion-parent">
<div id="Section_2" class="accord-heading">2. What is AWS?</div>
<div id="Section_2" class="accord-panel">

AWS (Amazon Web Services) is a platform to provide secure cloud services, database storage, offerings to compute power, content delivery, and other services to help business level and develop.

Learn more about AWS in this insightful <em><a href="https://intellipaat.com/tutorial/amazon-web-services-aws-tutorial/" target="_blank" rel="noopener">AWS Tutorial</a>!</em>

</div>
</div>
<div id="Section_3" class="accordion-parent">
<div id="Section_3" class="accord-heading">3. What is the importance of buffer in Amazon Web Services?</div>
<div id="Section_3" class="accord-panel">

An Elastic Load Balancer ensures that the incoming traffic is distributed optimally across various AWS instances.  A buffer will synchronize different components and makes the arrangement additional elastic to a burst of load or traffic. The components are prone to work in an unstable way of receiving and processing the requests. The buffer creates the equilibrium linking various apparatus and crafts them effort at the identical rate to supply more rapid services.

</div>
</div>
<div id="Section_4" class="accordion-parent">
<div id="Section_4" class="accord-heading">4. What is the way to secure data for carrying in the cloud?</div>
<div id="Section_4" class="accord-panel">

One thing must be ensured that no one should seize the information in the cloud while data is moving from point one to another and also there should not be any leakage with the security key from several storerooms in the cloud. Segregation of information from additional companies’ information and then encrypting it by means of approved methods is one of the options.

Amazon Web Services offers you a secure way of carrying data in the cloud. Looking to master AWS platform? Check this comprehensive <em><a href="https://intellipaat.com/aws-certification-training-online/" target="_blank" rel="noopener">AWS Certification Training</a>.</em>

</div>
</div>
<div id="Section_5" class="accordion-parent">
<div id="Section_5" class="accord-heading">5. Name the several layers of Cloud Computing.</div>
<div id="Section_5" class="accord-panel">

Here is the list of layers of the cloud computing
<ul>
 	<li><b>PaaS</b> – Platform as a Service</li>
 	<li><b>IaaS</b> – Infrastructure as a Service</li>
 	<li><b>SaaS</b> – Software as a Service</li>
</ul>
</div>
</div>
<div id="Section_6" class="accordion-parent">
<div id="Section_6" class="accord-heading">6. What are the components involved in Amazon Web Services?</div>
<div id="Section_6" class="accord-panel">

There are 4 components involved and are as below.<b>Amazon S3</b>: with this, one can retrieve the key information which are occupied in creating cloud structural design and amount of produced information also can be stored in this component that is the consequence of the key specified.<b>Amazon EC2 <strong>instance</strong></b>: helpful to run a large distributed system on the Hadoop cluster. Automatic parallelization and job scheduling can be achieved by this component.<b>Amazon SQS</b>: this component acts as a mediator between different controllers. Also worn for cushioning requirements those are obtained by the manager of Amazon.<b>Amazon SimpleDB</b>: helps in storing the transitional position log and the errands executed by the consumers.

</div>
<h4><span lang="EN-US">These are some common AWS Solution Architect Interview Questions to be answered by an AWS Enterprise Solution Architect, without order predefined:</span></h4>
<table border="1" width="632" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="311"><b><span lang="EN-US">Interview Questions: Business Perspective</span></b></td>
<td valign="top" width="311"><b><span lang="EN-US">Recommended Answer</span></b></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">If an organization is facing a major change, what is your approach as AWS Solution Architect to suggest to face it?</span>

<span lang="EN-US">What steps will you perform to resolve this situation?</span></td>
<td valign="top" width="311"><span lang="EN-US">This reveals if the candidate for AWS Solution Architect position possesses an open interest in a future customer, understand their business model, and recognize actual changes and challenges.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">From your point of view, what are the relevant responsibilities of an AWS Solution Architect?</span></td>
<td valign="top" width="311"><span lang="EN-US">Describe relevant responsibilities, duties, and challenges for an AWS Solution Architect.</span>

<span lang="EN-US">Refer to above job description.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">How do you normally take AWS architecture requirements to design?</span></td>
<td valign="top" width="311"><span lang="EN-US">Describe your procedures and methodology for establishing relationships and how to understand business requirements from customer. </span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">What are key considerations/guidelines when you’re going to make some AWS Architecture recommendations?</span></td>
<td valign="top" width="311"><span lang="EN-US">Demonstrate with some examples, how you make decisions and recommendations about AWS Architecture topics.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">How do you approach a pre-sales engagement as AWS Solution Architect? How do you establish a relationship with AWS salespeople? Please describe…</span></td>
<td valign="top" width="311"><span lang="EN-US">It makes interviewers understand how the candidate creates a relationship and collaborate with other AWS work teams.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">What challenges are you looking for the position as an AWS Solution Architect?</span></td>
<td valign="top" width="311"><span lang="EN-US">Discover and explain what is the candidate/job purpose and objective into the company on this role.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">How do you share (describe) your ideas and knowledge about AWS services/products to customers or other people of your team? Please describe…</span>

<span lang="EN-US">Could you please show us?</span></td>
<td valign="top" width="311"><span lang="EN-US">This will reveal if the candidate has excellent communication and presentation skills and really enjoy sharing his/her expertise and knowledge as an advocate.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">Could you please describe a situation, where you interacted with CxOs people or other business leaders?</span></td>
<td valign="top" width="311"><span lang="EN-US">Understand if the candidate has had communication and relationship with C-level people, and how has managed those relationships.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">Please describe a successful project that reflects your design/ implementation/ consulting experience about AWS Solution Architecture?</span></td>
<td valign="top" width="311"><span lang="EN-US">Discover practical experience based at project executed before around AWS Solution Architecture.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">What enterprise architecture and management frameworks do you know? And how you have used them?</span></td>
<td valign="top" width="311"><span lang="EN-US">Reveal the knowledge of candidate about enterprise architecture, business architecture, architecture, and management frameworks. Also, reveals how the candidate has used them based on the experience.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">Please describe a problem or issue during your career as an AWS Solution Architect? How did you handle them?</span></td>
<td valign="top" width="311"><span lang="EN-US">Understand how the candidate handles issues and problems.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">What have you done to improve your AWS knowledge within last year?</span></td>
<td valign="top" width="311"><span lang="EN-US">Discover if the candidate has invested into his/her personal and professional growth by himself/herself.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">What are most important characteristics of an AWS Cloud solution that you need to take into account when you design it?</span></td>
<td valign="top" width="311"><span lang="EN-US">Understand if the candidate uses the AWS well-Architected framework and has a holistic view of a business solution.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">Please describe or tell us about a special contribution you have made to your last employer?</span><span lang="EN-US"> </span></td>
<td valign="top" width="311"><span lang="EN-US">Explain clearly what contributions you did in the past, which was his contribution to the success of the previous company and satisfaction of its customers. Share some past experiences.</span></td>
</tr>
<tr>
<td valign="top" width="311"><span lang="EN-US">Who are you? Please tell us about yourself?</span></td>
<td valign="top" width="311"><span lang="EN-US">Describe your principal values and characteristics as a human being. Explain why you’re the best candidate for that job position and what differentiates you from others.</span></td>
</tr>
</tbody>
</table>
<p align="center"><b><i><span lang="EN-US">Table #1 Typical general AWS Solution Architect Interview Questions</span></i></b></p>
<span lang="EN-US">Normally, the above questions are complemented with specific AWS technical questions that evaluate if the candidate has required qualifications from the AWS services and technology perspective like following:</span>
<table style="width: 788px;" border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td style="width: 183.657px;" valign="top"><b><span lang="EN-US">Interview Questions: Technical Perspective</span></b></td>
<td style="width: 580.343px;" valign="top"><b><span lang="EN-US">Recommended Answer</span></b></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is Cloud Computing?
What are their principal characteristics and benefits?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain the meaning of cloud computing, talk about characteristics as flexibility, elasticity, pay on demand. Describe each different cloud models as IaaS, PaaS, and SaaS. Reflect on the benefits and myths of the cloud.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is AWS?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Highlight AWS leadership in the cloud. Describe briefly some of the AWS services with which you feel at ease, for example, EC2, RDS, DynamoDB, Cloudformation etc…</span><span lang="EN-US">Note that AWS has comprehensive security capabilities that support virtually any cloud workload.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is the AWS free tier?
What is included in it?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain how the AWS Free Tier is designed to enable you to get hands-on experience with AWS cloud services; and what AWS services are freely available for 12 months following your AWS sign-up date, as well as additional service offers that do not automatically expire at the end of your 12-month AWS Free Tier term.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is an EC2 instance? How to protect and reuse it?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain that EC2 is a web service that provides resizable computing capacity in the cloud. Describe how to create an AMI, taking EC2 snapshot to backup, and reuse EC2 instance</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What kind of instances does AWS offer?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe all EC2 instance types. Each EC2 instance type comprises varying combinations of CPU, memory, storage, and networking capacity giving you the flexibility to choose the appropriate mix of resources for your applications. For more information refers to </span><a href="https://aws.amazon.com/ec2/instance-types/" rel="nofollow external noopener noreferrer" data-wpel-link="external"><span lang="EN-US">https://aws.amazon.com/ec2/instance-types/</span></a></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to increase the availability of your applications? </span><span lang="EN-US">How to avoid bottlenecks in the performance of your applications?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe AWS load balancing solutions. Remember that services like Elastic Load Balancing automatically distributes incoming application traffic across multiple Amazon EC2 instances in the cloud. It enables you to achieve greater levels of fault tolerance in your applications, seamlessly providing the required amount of load balancing capacity required to distribute application traffic.</span><span lang="EN-US">Describe ELB services, the difference between application and classic load balancing service.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to enable an automatic scaling solution according to the user demand?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain about Auto scaling features of AWS. Remember that Auto Scaling allows you to scale your Amazon EC2 capacity up or down automatically according to conditions you define, and it is particularly well suited for applications that experience hourly, daily, or weekly variability in usage.</span><span lang="EN-US">Describe how to create a launch configuration, an auto-scaling group including common limits and how to monitor it using Cloudwatch and how to establish automatic alerts and actions.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to create your own resources into the AWS Cloud?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe Amazon VPC service. Notice that Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud, where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including the selection of your own IP address range, the creation of subnets, and the configuration of route tables and network gateways.</span><span lang="EN-US">Highlight VPC security settings using security groups and ACLs for subnets.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How cloud you implement a DNS service in AWS?  How could you register a new domain name? How could you implement a low-latency, fault-tolerant architectures managing Web application traffic?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain services like Amazon Route 53, a highly available and scalable Domain Name System (DNS) web service. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints. Amazon Route 53 makes it possible for you to manage traffic globally through a variety of routing types, including Latency Based Routing, Geo DNS, and Weighted Round Robin—all of which can be combined with DNS Failover to enable a variety of low-latency, fault-tolerant architectures. Don’t forget that Amazon Route 53 also offers Domain Name Registration – you can purchase and manage domain names such as example.com and Amazon Route 53 will automatically configure DNS settings for your domains.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to implement a private connection to AWS Services?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">AWS offers a service called AWS Direct Connect that lets you establish a dedicated network connection between your network and one of the AWS Direct Connect locations. This dedicated connection can be partitioned into multiple virtual interfaces as a VLAN. This allows you to use the same</span><span lang="EN-US"> </span><span lang="EN-US">connection to access public resources using public IP address space, and private resources using private IP space while maintaining network separation between the public and private environments.</span><span lang="EN-US">Describe advantages and disadvantages of using private network connections.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What do you know about the Shared Responsibility Model established with AWS?</span><span lang="EN-US">Could you please explain more about what is the responsibility of a customer?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Because you’re building systems on top of the AWS platform, the security responsibilities will be shared. While AWS manages the security of the cloud, security in the cloud is the responsibility of the customer. Customers retain control of the security they choose to implement to protect their own content, platform, applications, systems, and networks, no differently than they would have for the applications in an on-site datacenter.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to control the access to your resources located at AWS?</span><span lang="EN-US">How could you protect your data at rest?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">There is a service called AWS Identity and Access Management (IAM) that enables you to securely control access to AWS services and resources for your users. Using IAM, you can create and manage AWS users and groups and use permissions to allow and deny their access to AWS resources.</span><span lang="EN-US">For protecting your data, there is AWS Key Management Service (KMS), it is a managed service that helps make it easy for you to create and control the encryption keys used to encrypt your data.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What are storage options provided by AWS?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe in detail all the storage options provided by AWS like EBS, S3, Glacier etc. Remember that AWS offers many different storage services, including Amazon S3, Amazon EBS, Amazon EFS, and Amazon Glacier. Amazon S3 is an object storage service, Amazon EBS is a block storage service, Amazon EFS is a file storage service, and Amazon Glacier is a long-term archive storage service.</span><span lang="EN-US">Refer depending on scenario what is the best storage option.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is the AWS Storage Gateway?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">The AWS Storage Gateway is a service connecting an on-premises software appliance with cloud-based storage, to provide seamless and secure integration between an organization’s on-premises IT environment and AWS storage infrastructure.</span><span lang="EN-US">Notice when to use it, and how to use it for recovery or backup storage option.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How to deliver content faster?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe in detail the service like Amazon CloudFront which is a content delivery web service. It integrates with other AWS services to give developers and businesses an easy way to distribute content to end users with low latency, high data transfer speeds, and no minimum usage commitments.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What are the managed database services provided by AWS?</span><span lang="EN-US">What kind of SQL databases are supported by AWS?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Answer with the Amazon Relational Database Service (Amazon RDS). It is a web service that makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while managing time-consuming database management tasks, allowing you to focus on your applications and business.</span><span lang="EN-US">It gives you access to the capabilities of a MySQL, Oracle, SQL Server, or PostgreSQL database engines running on your own Amazon RDS cloud-based database instance with high availability configurations.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What is the difference between SQL and NoSQL Database in AWS?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Explain about RDS options and DynamoDB characteristics, their differences, benefits, and purpose of each related to AWS service.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">Which option exists to accelerate the performance of a web application?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe how to improve the performance of web applications by allowing you to retrieve information from a fast, managed, in-memory system, instead of relying entirely on slower disk-based databases. AWS offers a service called Amazon ElastiCache, it can not only improve load and response time to user actions and queries but also reduce the cost associated with scaling web applications.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">Which AWS services are offered for business intelligence?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe each AWS related service, highlight Amazon Redshift as a fast, fully managed, petabyte-scale data warehouse solution that makes it simple and cost-effective to efficiently analyze all your data using your existing business intelligence tools.</span><span lang="EN-US">From the end-user analytic point of view, there exists a service named Amazon QuickSight which is a very fast, easy-to-use, and cloud-powered business intelligence (BI) service. It makes it easy for all employees within an organization to build visualizations, perform ad-hoc analysis, and quickly get business insights from their data. Amazon QuickSight integrates automatically with AWS data services, enables organizations to scale to hundreds of thousands of users, and delivers fast and responsive query performance to them via the SPICE engine.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">What other AWS services do you use at the application level?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe in detail all the application services provided by AWS like SNS, SES, SQS, and Workflow.</span><span lang="EN-US">Remember that Amazon Simple Email Service (Amazon SES) is a highly scalable and cost-effective email-sending service for businesses and developers. On the other hand, Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud. It provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications. Finally, Amazon Simple Queue Service offers a reliable, highly scalable hosted queue for storing messages as they travel between computers. By using Amazon SQS, developers can simply move data between distributed application components performing different tasks, without losing messages or requiring each component to be always available. Amazon SQS makes it easy to build an automated workflow.</span>

<span lang="EN-US">Don’t forget that Amazon Simple Workflow Service (Amazon SWF) is a web service that makes it easy to coordinate work across distributed application components. Amazon SWF enables applications for a range of use cases, including media processing, web application back-ends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks.</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">How will you improve the deployment and management of AWS services?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">Describe how AWS services as AWS Elastic Beanstalk, AWS OpsWorks, and Cloudformation contribute to improving the deployment and management of AWS services?</span></td>
</tr>
<tr>
<td style="width: 183.657px;" valign="top"><span lang="EN-US">As an AWS Solution Architect, how could you implement Disaster recovery on AWS?</span></td>
<td style="width: 580.343px;" valign="top"><span lang="EN-US">If you want to enable faster disaster recovery of their critical IT systems without incurring the infrastructure expense of a second physical site, you should use AWS services. Remember, that the AWS platform supports many popular disaster recovery (DR) architectures, from “pilot light” environments that are ready to scale up at a moment’s notice, to “hot standby” environments that enable rapid failover and enable rapid recovery of your IT infrastructure and data.</span></td>
</tr>
</tbody>
</table>
<span lang="EN-US"> </span><b><i><span lang="EN-US">Table #2. Typical technical AWS Solution Architect Interview Questions</span></i></b>

</div>
&nbsp;
<h2><b>Section 1: What is Cloud Computing</b></h2>
For a detailed discussion on this topic, please refer our <a href="https://www.edureka.co/blog/what-is-cloud-computing/" target="_blank" rel="noopener noreferrer"><b>Cloud Computing</b></a> blog.
<h3><b>1. I have some private servers on my premises, also I have distributed some of my workload on the public cloud, what is this architecture called?</b></h3>
<ol>
 	<li>Virtual Private Network</li>
 	<li>Private Cloud</li>
 	<li>Virtual Private Cloud</li>
 	<li>Hybrid Cloud</li>
</ol>
<b>Answer D.</b>

<b>Explanation: </b>This type of architecture would be a hybrid cloud. Why? Because we are using both, the public cloud, and your on premises servers i.e the private cloud. To make this hybrid architecture easy to use, wouldn’t it be better if your private and public cloud were all on the same network(virtually). This is established by including your public cloud servers in a virtual private cloud, and connecting this virtual cloud with your on premise servers using a VPN(Virtual Private Network).
<h2><b>Section 2: Amazon EC2 Interview Questions</b></h2>
For a detailed discussion on this topic, please refer our <a href="https://www.edureka.co/blog/ec2-aws-tutorial-elastic-compute-cloud/" target="_blank" rel="noopener noreferrer"><b>EC2 AWS</b></a> blog.
<h3><b>2. What does the following command do with respect to the Amazon EC2 security groups?</b></h3>
<b>ec2-create-group CreateSecurityGroup</b>
<ol>
 	<li>Groups the user created security groups into a new group for easy access.</li>
 	<li>Creates a new security group for use with your account.</li>
 	<li>Creates a new group inside the security group.</li>
 	<li>Creates a new rule inside the security group.</li>
</ol>
<b>Answer B.</b>

<strong>Explanation: </strong>A Security group is just like a firewall, it controls the traffic in and out of your instance. In AWS terms, the inbound and outbound traffic. The command mentioned is pretty straight forward, it says create security group, and does the same. Moving along, once your security group is created, you can add different rules in it. For example, you have an RDS instance, to access it, you have to add the public IP address of the machine from which you want access the instance  in its security group.
<h3><strong>3. You have a video trans-coding application. The videos are processed according to a queue. If the processing of a video is interrupted in one instance, it is resumed in another instance. Currently there is a huge back-log of videos which needs to be processed, for this you need to add more instances, but you need these instances only until your backlog is reduced. Which of these would be an efficient way to do it?</strong></h3>
You should be using an <b>On Demand</b> instance for the same. Why? First of all, the workload has to be processed now, meaning it is urgent, secondly you don’t need them once your backlog is cleared, therefore Reserved Instance is out of the picture, and since the work is urgent, you cannot stop the work on your instance just because the spot price spiked, therefore Spot Instances shall also not be used. Hence On-Demand instances shall be the right choice in this case.
<h3><b>4. You have a distributed application that periodically processes large volumes of data across multiple Amazon EC2 Instances. The application is designed to recover gracefully from Amazon EC2 instance failures. You are required to accomplish this task in the most cost effective way.</b></h3>
<b>Which of the following will meet your requirements?</b>
<ol>
 	<li>Spot Instances</li>
 	<li>Reserved instances</li>
 	<li>Dedicated instances</li>
 	<li>On-Demand instances</li>
</ol>
<strong>Answer: A</strong>

<b>Explanation: </b>Since the work we are addressing here is not continuous, a reserved instance shall be idle at times, same goes with On Demand instances. Also it does not make sense to launch an On Demand instance whenever work comes up, since it is expensive. Hence Spot Instances will be the right fit because of their low rates and no long term commitments.
<h3><strong>5. How is stopping and terminating an instance different from each other?</strong></h3>
Starting, stopping and terminating are the three states in an EC2 instance, let’s discuss them in detail:
<ul>
 	<li><b>Stopping and Starting</b> an instance: When an instance is stopped, the instance performs a normal shutdown and then transitions to a stopped state. All of its Amazon EBS volumes remain attached, and you can start the instance again at a later time. You are not charged for additional instance hours while the instance is in a stopped state.</li>
 	<li><b>Terminating</b> an instance: When an instance is terminated, the instance performs a normal shutdown, then the attached Amazon EBS volumes are deleted unless the volume’s<i>deleteOnTermination</i> attribute is set to false. The instance itself is also deleted, and you can’t start the instance again at a later time.</li>
</ul>
<h3><strong>6. If I want my instance to run on a single-tenant hardware, which value do I have to set the instance’s tenancy attribute to?</strong></h3>
<ol>
 	<li>Dedicated</li>
 	<li>Isolated</li>
 	<li>One</li>
 	<li>Reserved</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation: </b>The Instance tenancy attribute should be set to Dedicated Instance. The rest of the values are invalid.
<h3><b>7. When will you incur costs with an Elastic IP address (EIP)?</b></h3>
<ol>
 	<li>When an EIP is allocated.</li>
 	<li>When it is allocated and associated with a running instance.</li>
 	<li>When it is allocated and associated with a stopped instance.</li>
 	<li>Costs are incurred regardless of whether the EIP is associated with a running instance.</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation: </b>You are not charged, if only one Elastic IP address is attached with your running instance. But you do get charged in the following conditions:
<ul>
 	<li>When you use more than one Elastic IPs with your instance.</li>
 	<li>When your Elastic IP is attached to a stopped instance.</li>
 	<li>When your Elastic IP is not attached to any instance.</li>
</ul>
<h3><strong>8. How is a Spot instance different from an On-Demand instance or Reserved Instance?</strong></h3>
First of all, let’s understand that Spot Instance, On-Demand instance and Reserved Instances are all models for pricing. Moving along, spot instances provide the ability for customers to purchase compute capacity with no upfront commitment, at hourly rates usually lower than the On-Demand rate in each region. Spot instances are just like bidding, the bidding price is called Spot Price. The Spot Price fluctuates based on supply and demand for instances, but customers will never pay more than the maximum price they have specified. If the Spot Price moves higher than a customer’s maximum price, the customer’s EC2 instance will be shut down automatically. But the reverse is not true, if the Spot prices come down again, your EC2 instance will not be launched automatically, one has to do that manually.  In Spot and On demand instance, there is no commitment for the duration from the user side, however in reserved instances one has to stick to the time period that he has chosen.
<h3><strong>9. Are the Reserved Instances available for Multi-AZ Deployments?</strong></h3>
<ol>
 	<li>Multi-AZ Deployments are only available for Cluster Compute instances types</li>
 	<li>Available for all instance types</li>
 	<li>Only available for M3 instance types</li>
 	<li>D. Not Available for Reserved Instances</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation:</b> Reserved Instances is a pricing model, which is available for all instance types in EC2.
<h3><strong>10. How to use the processor state control feature available on the  c4.8xlarge instance?</strong></h3>
The processor state control consists of 2 states:
<ul>
 	<li>The C state – Sleep state varying from c0 to c6. C6 being the deepest sleep state for a processor</li>
 	<li>The P state – Performance state p0 being the highest and p15 being the lowest possible frequency.</li>
</ul>
Now, why the C state and P state. Processors have cores, these cores need thermal headroom to boost their performance. Now since all the cores are on the processor the temperature should be kept at an optimal state so that all the cores can perform at the highest performance.

Now how will these states help in that? If a core is put into sleep state it will reduce the overall temperature of the processor and hence other cores can perform better. Now the same can be  synchronized with other cores, so that the processor can boost as many cores it can by timely putting other cores to sleep, and thus get an overall performance boost.

Concluding, the C and P state can be customized in some EC2 instances like the c4.8xlarge instance and thus you can customize the processor according to your workload.

How to do it? You can refer this <a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/processor_state_control.html" target="_blank" rel="noopener noreferrer">tutorial</a> for the same.
<h3><strong>11. What kind of network performance parameters can you expect when you launch instances in cluster placement group?</strong></h3>
The network performance depends on the instance type and network performance specification, if launched in a placement group you can expect up to
<ul>
 	<li>10 Gbps in a single-flow,</li>
 	<li>20 Gbps in multiflow i.e full duplex</li>
 	<li>Network traffic outside the placement group will be limited to 5 Gbps(full duplex).</li>
</ul>
<h3><b>12. To deploy a 4 node cluster of Hadoop in AWS which instance type can be used?</b></h3>
First let’s understand what actually happens in a Hadoop cluster, the Hadoop cluster follows a master slave concept. The master machine processes all the data, slave machines store the data and act as data nodes. Since all the storage happens at the slave, a higher capacity hard disk would be recommended and since master does all the processing, a higher RAM and a much better CPU is required. Therefore, you can select the configuration of your machine depending on your workload. For e.g. – In this case c4.8xlarge will be preferred for master machine whereas for slave machine we can select i2.large instance. If you don’t want to deal with configuring your instance and installing hadoop cluster manually, you can straight away launch an Amazon EMR (Elastic Map Reduce) instance which automatically configures the servers for you. You dump your data to be processed in S3, EMR picks it from there, processes it, and dumps it back into S3.
<h3><b>13. Where do you think an AMI fits, when you are designing an architecture for a solution?</b></h3>
AMIs(Amazon Machine Images) are like templates of virtual machines and an instance is derived from an AMI. AWS offers pre-baked AMIs which you can choose while you are launching an instance, some AMIs are not free, therefore can be bought from the AWS Marketplace. You can also choose to create your own custom AMI which would help you save space on AWS. For example if you don’t need a set of software on your installation, you can customize your AMI to do that. This makes it cost efficient, since you are removing the unwanted things.
<h3><b>14. How do you choose an Availability Zone?</b></h3>
Let’s understand this through an example, consider there’s a company which has user base in India as well as in the US.

Let us see how we will choose the region for this use case :

<img class="aligncenter wp-image-34340" src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/regions-s3-aws.png" sizes="(max-width: 559px) 100vw, 559px" srcset="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/regions-s3-aws.png 678w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/regions-s3-aws-300x124.png 300w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/regions-s3-aws-528x218.png 528w" alt="Location - AWS Interview Questions - Edureka" width="559" height="231" />

So, with reference to the above figure the regions to choose between are, Mumbai and North Virginia. Now let us first compare the pricing, you have hourly prices, which can be converted to your per month figure. Here North Virginia emerges as a winner. But, pricing cannot be the only parameter to consider. Performance should also be kept in mind hence, let’s look at latency as well. Latency basically is the time that a server takes to respond to your requests i.e the response time. North Virginia wins again!

So concluding, North Virginia should be chosen for this use case.
<h3><b>15. Is one Elastic IP address enough for every instance that I have running?</b></h3>
Depends! Every instance comes with its own private and public address. The private address is associated exclusively with the instance and is returned  to Amazon EC2 only when it is stopped or terminated. Similarly, the public address is associated exclusively with the instance until it is stopped or terminated. However, this can be replaced by the Elastic IP address, which stays with the instance as long as the user doesn’t manually detach it. But what if you are hosting multiple websites on your EC2 server, in that case you may require more than one Elastic IP address.
<h3><b>16. What are the best practices for Security in Amazon EC2?</b></h3>
There are several best practices to secure Amazon EC2. A few of them are given below:
<ul>
 	<li>Use AWS Identity and Access Management (IAM) to control access to your AWS resources.</li>
 	<li>Restrict access by only allowing trusted hosts or networks to access ports on your instance.</li>
 	<li>Review the rules in your security groups regularly, and ensure that you apply the principle of least</li>
 	<li>Privilege – only open up permissions that you require.</li>
 	<li>Disable password-based logins for instances launched from your AMI. Passwords can be found or cracked, and are a security risk.</li>
</ul>
<h2><a class="maxbutton-16 maxbutton maxbutton-enroll-yellow-big" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn To Use AWS Tools</span></a></h2>
<h2><b>Section 3: Amazon Storage</b></h2>
<h3><b>17. You need to configure an Amazon S3 bucket to serve static assets for your public-facing web application. Which method will ensure that all objects uploaded to the bucket are set to public read?</b></h3>
<ol>
 	<li>Set permissions on the object to public read during upload.</li>
 	<li>Configure the bucket policy to set all objects to public read.</li>
 	<li>Use AWS Identity and Access Management roles to set the bucket to public read.</li>
 	<li>Amazon S3 objects default to public read, so no action is needed.</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation:</b> Rather than making changes to every object, its better to set the policy for the whole bucket. IAM is used to give more granular permissions, since this is a website, all objects would be public by default.
<h3><b>18. A customer wants to leverage Amazon Simple Storage Service (S3) and Amazon Glacier as part of their backup and archive infrastructure. The customer plans to use third-party software to support this integration. Which approach will limit the access of the third party software to only the Amazon S3 bucket named “company-backup”?</b></h3>
<ol>
 	<li>A custom bucket policy limited to the Amazon S3 API in three Amazon Glacier archive “company-backup”</li>
 	<li>A custom bucket policy limited to the Amazon S3 API in “company-backup”</li>
 	<li>A custom IAM user policy limited to the Amazon S3 API for the Amazon Glacier archive “company-backup”.</li>
 	<li>A custom IAM user policy limited to the Amazon S3 API in “company-backup”.</li>
</ol>
<strong>Answer D.</strong>

<b>Explanation:</b> Taking queue from the previous questions, this use case involves more granular permissions, hence IAM would be used here.
<h3><strong>19. Can S3 be used with EC2 instances, if yes, how?</strong></h3>
Yes, it can be used for instances with root devices backed by local instance storage. By using Amazon S3, developers have access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites. In order to execute systems in the Amazon EC2 environment, developers use the tools provided to load their Amazon Machine Images (AMIs) into Amazon S3 and to move them between Amazon S3 and Amazon EC2.

Another use case could be for websites hosted on EC2 to load their static content from S3.

For a detailed discussion on S3, please refer our <a href="https://www.edureka.co/blog/s3-aws-amazon-simple-storage-service/" target="_blank" rel="noopener noreferrer"><b>S3 AWS </b></a>blog.
<h3><b>20. A customer implemented AWS Storage Gateway with a gateway-cached volume at their main office. An event takes the link between the main and branch office offline. Which methods will enable the branch office to access their data?</b></h3>
<ol>
 	<li>Restore by implementing a lifecycle policy on the Amazon S3 bucket.</li>
 	<li>Make an Amazon Glacier Restore API call to load the files into another Amazon S3 bucket within four to six hours.</li>
 	<li>Launch a new AWS Storage Gateway instance AMI in Amazon EC2, and restore from a gateway snapshot.</li>
 	<li>Create an Amazon EBS volume from a gateway snapshot, and mount it to an Amazon EC2 instance.</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation: </b>The fastest way to do it would be launching a new storage gateway instance. Why? Since time is the key factor which drives every business, troubleshooting this problem will take more time. Rather than we can just restore the previous working state of the storage gateway on a new instance.
<h3><b>21. When you need to move data over long distances using the internet, for instance across countries or continents to your Amazon S3 bucket, which method or service will you use?</b></h3>
<ol>
 	<li>Amazon Glacier</li>
 	<li>Amazon CloudFront</li>
 	<li>Amazon Transfer Acceleration</li>
 	<li>Amazon Snowball</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation:</b> You would not use Snowball, because for now, the snowball service does not support cross region data transfer, and since, we are transferring across countries, Snowball cannot be used. Transfer Acceleration shall be the right choice here as it throttles your data transfer with the use of optimized network paths and Amazon’s content delivery network upto 300% compared to normal data transfer speed.
<h3><b>22. How can you speed up data transfer in Snowball?</b></h3>
The data transfer can be increased in the following way:
<ul>
 	<li>By performing multiple copy operations at one time i.e. if the workstation is powerful enough, you can initiate multiple cp commands each from different terminals, on the same Snowball device.</li>
 	<li>Copying from multiple workstations to the same snowball.</li>
 	<li>Transferring large files or by creating a batch of small file, this will reduce the encryption overhead.</li>
 	<li>Eliminating unnecessary hops i.e. make a setup where the source machine(s) and the snowball are the only machines active on the switch being used, this can hugely improve performance.</li>
</ul>
<h2><a class="maxbutton-12 maxbutton maxbutton-enroll-green-big" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn AWS from our Experts!</span></a></h2>
<h2><b>Section 4: AWS VPC</b></h2>
<h3><b>23. If you want to launch Amazon Elastic Compute Cloud (EC2) instances and assign each instance a predetermined private IP address you should:</b></h3>
<ol>
 	<li>Launch the instance from a private Amazon Machine Image (AMI).</li>
 	<li>Assign a group of sequential Elastic IP address to the instances.</li>
 	<li>Launch the instances in the Amazon Virtual Private Cloud (VPC).</li>
 	<li>Launch the instances in a Placement Group.</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation:</b> The best way of connecting to your cloud resources (for ex- ec2 instances) from your own data center (for eg- private cloud) is a VPC. Once you connect your datacenter to the VPC in which your instances are present, each instance is assigned a private IP address which can be accessed from your datacenter. Hence, you can access your public cloud resources, as if they were on your own network.
<h3><strong>24. Can I connect my corporate datacenter to the Amazon Cloud?</strong></h3>
Yes, you can do this by establishing a VPN(Virtual Private Network) connection between your company’s network and your VPC (Virtual Private Cloud), this will allow you to interact with your EC2 instances as if they were within your existing network.
<h3><strong>25. Is it possible to change the private IP addresses of an EC2 while it is running/stopped in a VPC?</strong></h3>
Primary private IP address is attached with the instance throughout its lifetime and cannot be changed, however secondary private addresses can be unassigned, assigned or moved between interfaces or instances at any point.
<h3><b>26. Why do you make subnets?</b></h3>
<ol>
 	<li>Because there is a shortage of networks</li>
 	<li>To efficiently utilize networks that have a large no. of hosts.</li>
 	<li>Because there is a shortage of hosts.</li>
 	<li>To efficiently utilize networks that have a small no. of hosts.</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>If there is a network which has a large no. of hosts, managing all these hosts can be a tedious job. Therefore we divide this network into subnets (sub-networks) so that managing these hosts becomes simpler.
<h3><b>27. Which of the following is true?</b></h3>
<ol>
 	<li>You can attach multiple route tables to a subnet</li>
 	<li>You can attach multiple subnets to a route table</li>
 	<li>Both A and B</li>
 	<li>None of these.</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>Route Tables are used to route network packets, therefore in a subnet having multiple route tables will lead to confusion as to where the packet has to go. Therefore, there is only one route table in a subnet, and since a route table can have any no. of records or information, hence attaching multiple subnets to a route table is possible.
<h3><b>28. In CloudFront what happens when content is NOT present at an Edge location and a request is made to it?</b></h3>
<ol>
 	<li>An Error “404 not found” is returned</li>
 	<li>CloudFront delivers the content directly from the origin server and stores it in the cache of the edge location</li>
 	<li>The request is kept on hold till content is delivered to the edge location</li>
 	<li>The request is routed to the next closest edge location</li>
</ol>
<strong>Answer B. </strong>

<b>Explanation:</b> CloudFront is a content delivery system, which caches data to the nearest edge location from the user, to reduce latency. If data is not present at an edge location, the first time the data may get transferred from the original server, but from the next time, it will be served from the cached edge.
<h3><b>29. If I’m using Amazon CloudFront, can I use Direct Connect to transfer objects from my own data center?</b></h3>
Yes. Amazon CloudFront supports custom origins including origins from outside of AWS. With AWS Direct Connect, you will be charged with the respective data transfer rates.
<h3><strong>30. If my AWS Direct Connect fails, will I lose my connectivity?</strong></h3>
If a backup AWS Direct connect has been configured, in the event of a failure it will switch over to the second one. It is recommended to enable Bidirectional Forwarding Detection (BFD) when configuring your connections to ensure faster detection and failover. On the other hand, if you have configured a backup IPsec VPN connection instead, all VPC traffic will failover to the backup VPN connection automatically. Traffic to/from public resources such as Amazon S3 will be routed over the Internet. If you do not have a backup AWS Direct Connect link or a IPsec VPN link, then Amazon VPC traffic will be dropped in the event of a failure.
<h2><a class="maxbutton-22 maxbutton maxbutton-certification-blue-big" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn VPC from our Experts!</span></a></h2>
<h2><b>Section 5: Amazon Database</b></h2>
<h3><b>31. If I launch a standby RDS instance, will it be in the same Availability Zone as my primary?</b></h3>
<ol>
 	<li>Only for Oracle RDS types</li>
 	<li>Yes</li>
 	<li>Only if it is configured at launch</li>
 	<li>No</li>
</ol>
<strong>Answer D.</strong>

<b>Explanation: </b>No, since the purpose of having a standby instance is to avoid an infrastructure failure (if it happens), therefore the standby instance is stored in a different availability zone, which is a physically different independent infrastructure.
<h3><b>32. When would I prefer Provisioned IOPS over Standard RDS storage?</b></h3>
<ol>
 	<li><b>If you have batch-oriented workloads</b></li>
 	<li>If you use production online transaction processing (OLTP) workloads.</li>
 	<li>If you have workloads that are not sensitive to consistent performance</li>
 	<li>All of the above</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation: </b> Provisioned IOPS deliver high IO rates but on the other hand it is expensive as well. Batch processing workloads do not require manual intervention they enable full utilization of systems, therefore a provisioned IOPS will be preferred for batch oriented workload.
<h3><strong>33. How is Amazon RDS, DynamoDB and Redshift different?</strong></h3>
<ul>
 	<li>Amazon RDS is a database management service for relational databases,  it manages patching, upgrading, backing up of data etc. of databases for you without your intervention. RDS  is a Db management service for structured data only.</li>
 	<li>DynamoDB, on the other hand, is a NoSQL database service, NoSQL deals with unstructured data.</li>
 	<li>Redshift, is an entirely different service, it is a data warehouse product and is used in data analysis.</li>
</ul>
<h3><b>34. If I am running my DB Instance as a Multi-AZ deployment, can I use the standby DB Instance for read or write operations along with primary DB instance?</b></h3>
<ol>
 	<li>Yes</li>
 	<li>Only with MySQL based RDS</li>
 	<li>Only for Oracle RDS instances</li>
 	<li>No</li>
</ol>
<strong>Answer D.</strong>

<b>Explanation: </b>No,<b> </b>Standby DB instance cannot be used with primary DB instance in parallel, as the former is solely used for standby purposes, it cannot be used unless the primary instance goes down.
<h3><b>35. Your company’s branch offices are all over the world, they use a software with a multi-regional deployment on AWS, they use MySQL 5.6 for data persistence.</b></h3>
<b>The task is to run an hourly batch process and read data from every region to compute cross-regional reports which will be distributed to all the branches. This should be done in the shortest time possible. How will you build the DB architecture in order to meet the requirements?</b>
<ol>
 	<li>For each regional deployment, use RDS MySQL with a master in the region and a read replica in the HQ region</li>
 	<li>For each regional deployment, use MySQL on EC2 with a master in the region and send hourly EBS snapshots to the HQ region</li>
 	<li>For each regional deployment, use RDS MySQL with a master in the region and send hourly RDS snapshots to the HQ region</li>
 	<li>For each regional deployment, use MySQL on EC2 with a master in the region and use S3 to copy data files hourly to the HQ region</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation: </b>For this we will take an RDS instance as a master, because it will manage our database for us and since we have to read from every region, we’ll put a read replica of this instance in every region where the data has to be read from. Option C is not correct since putting a read replica would be more efficient than putting a snapshot, a read replica can be promoted if needed  to an independent DB instance, but with a Db snapshot it becomes mandatory to launch a separate DB Instance.
<h3><strong>36. Can I run more than one DB instance for Amazon RDS for free?</strong></h3>
Yes. You can run more than one Single-AZ Micro database instance, that too for free! However, any use exceeding 750 instance hours, across all Amazon RDS Single-AZ Micro DB instances, across all eligible database engines and regions, will be billed at standard Amazon RDS prices. For example: if you run two Single-AZ Micro DB instances for 400 hours each in a single month, you will accumulate 800 instance hours of usage, of which 750 hours will be free. You will be billed for the remaining 50 hours at the standard Amazon RDS price.

For a detailed discussion on this topic, please refer our<a href="https://www.edureka.co/blog/rds-aws-tutorial/" target="_blank" rel="noopener noreferrer"><b> RDS AWS</b></a> blog.
<h3><b>37. Which AWS services will you use to collect and process e-commerce data for near real-time analysis?</b></h3>
<ol>
 	<li>Amazon ElastiCache</li>
 	<li>Amazon DynamoDB</li>
 	<li>Amazon Redshift</li>
 	<li>Amazon Elastic MapReduce</li>
</ol>
<strong>Answer B,C.</strong>

<b>Explanation:</b> DynamoDB is a fully managed NoSQL database service. DynamoDB, therefore can be fed any type of unstructured data, which can be data from e-commerce websites as well, and later, an analysis can be done on them using Amazon Redshift. We are not using Elastic MapReduce, since a near real time analyses is needed.
<h3><strong>38. Can I retrieve only a specific element of the data, if I have a nested JSON data in DynamoDB?</strong></h3>
Yes. When using the GetItem, BatchGetItem, Query or Scan APIs, you can define a Projection Expression to determine which attributes should be retrieved from the table. Those attributes can include scalars, sets, or elements of a JSON document.
<h3><b>39. A company is deploying a new two-tier web application in AWS. The company has limited staff and requires high availability, and the application requires complex queries and table joins. Which configuration provides the solution for the company’s requirements?</b></h3>
<ol>
 	<li>MySQL Installed on two Amazon EC2 Instances in a single Availability Zone</li>
 	<li>Amazon RDS for MySQL with Multi-AZ</li>
 	<li>Amazon ElastiCache</li>
 	<li>Amazon DynamoDB</li>
</ol>
<strong>Answer D.</strong>

<b>Explanation: </b>DynamoDB has the ability to scale more than RDS or any other relational database service, therefore DynamoDB would be the apt choice.
<h3><b>40. What happens to my backups and DB Snapshots if I delete my DB Instance?</b></h3>
When you delete a DB instance, you have an option of creating a final DB snapshot, if you do that you can restore your database from that snapshot. RDS retains this user-created DB snapshot along with all other manually created DB snapshots after the instance is deleted, also automated backups are deleted and only manually created DB Snapshots are retained.
<h3><b>41. Which of the following use cases are suitable for Amazon DynamoDB? Choose 2 answers</b></h3>
<ol>
 	<li>Managing web sessions.</li>
 	<li>Storing JSON documents.</li>
 	<li>Storing metadata for Amazon S3 objects.</li>
 	<li>Running relational joins and complex updates.</li>
</ol>
<strong>Answer C,D.</strong>

<b>Explanation: </b>If all your JSON data have the same fields eg [id,name,age] then it would be better to store it in a relational database, the metadata on the other hand is unstructured, also running relational joins or complex updates would work on DynamoDB as well.
<h3><strong>42. How can I load my data to Amazon Redshift from different data sources like Amazon RDS, Amazon DynamoDB and Amazon EC2?</strong></h3>
You can load the data in the following two ways:
<ul>
 	<li>You can use the COPY command to load data in parallel directly to Amazon Redshift from Amazon EMR, Amazon DynamoDB, or any SSH-enabled host.</li>
 	<li>AWS Data Pipeline provides a high performance, reliable, fault tolerant solution to load data from a variety of AWS data sources. You can use AWS Data Pipeline to specify the data source, desired data transformations, and then execute a pre-written import script to load your data into Amazon Redshift.</li>
</ul>
<h3><b>43. Your application has to retrieve data from your user’s mobile every 5 minutes and the data is stored in DynamoDB, later every day at a particular time the data is extracted into S3 on a per user basis and then your application is later used to visualize the data to the user. You are asked to optimize the architecture of the backend system to lower cost, what would you recommend?</b></h3>
<ol>
 	<li>Create a new Amazon DynamoDB (able each day and drop the one for the previous day after its data is on Amazon S3.</li>
 	<li>Introduce an Amazon SQS queue to buffer writes to the Amazon DynamoDB table and reduce provisioned write throughput.</li>
 	<li>Introduce Amazon Elasticache to cache reads from the Amazon DynamoDB table and reduce provisioned read throughput.</li>
 	<li>Write data directly into an Amazon Redshift cluster replacing both Amazon DynamoDB and Amazon S3.</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation: </b>Since our work requires the data to be extracted and analyzed, to optimize this process a person would use provisioned IO, but since it is expensive, using a ElastiCache memoryinsread to cache the results in the memory can reduce the provisioned read throughput and hence reduce cost without affecting the performance.
<h3><b>44. You are running a website on EC2 instances deployed across multiple Availability Zones with a Multi-AZ RDS MySQL Extra Large DB Instance. The site performs a high number of small reads and writes per second and relies on an eventual consistency model. After comprehensive tests you discover that there is read contention on RDS MySQL. Which are the best approaches to meet these requirements? (Choose 2 answers)</b></h3>
<ol>
 	<li>Deploy ElastiCache in-memory cache running in each availability zone</li>
 	<li>Implement sharding to distribute load to multiple RDS MySQL instances</li>
 	<li>Increase the RDS MySQL Instance size and Implement provisioned IOPS</li>
 	<li>Add an RDS MySQL read replica in each availability zone</li>
</ol>
<strong>Answer A,C.</strong>

<b>Explanation:  </b>Since it does a lot of read writes, provisioned IO may become expensive. But we need high performance as well, therefore the data can be cached using ElastiCache which can be used for frequently reading the data. As for RDS since read contention is happening, the instance size should be increased and provisioned IO should be introduced to increase the performance.
<h3><b>45. A startup is running a pilot deployment of around 100 sensors to measure street noise and air quality in urban areas for 3 months. It was noted that every month around 4GB of sensor data is generated. The company uses a load balanced auto scaled layer of EC2 instances and a RDS database with 500 GB standard storage. The pilot was a success and now they want to deploy at least  100K sensors which need to be supported by the backend. You need to store the data for at least 2 years to analyze it. Which setup of the following would you prefer?</b></h3>
<ol>
 	<li>Add an SQS queue to the ingestion layer to buffer writes to the RDS instance</li>
 	<li>Ingest data into a DynamoDB table and move old data to a Redshift cluster</li>
 	<li>Replace the RDS instance with a 6 node Redshift cluster with 96TB of storage</li>
 	<li>Keep the current architecture but upgrade RDS storage to 3TB and 10K provisioned IOPS</li>
</ol>
<strong>Answer C.</strong>
<b>Explanation: </b>A Redshift cluster would be preferred because it easy to scale, also the work would be done in parallel through the nodes, therefore is perfect for a bigger workload like our use case.Since each month 4 GB of data is generated, therefore in 2 year, it should be around 96 GB. And since the servers will be increased to 100K in number, 96 GB will approximately become 96TB. Hence option C is the right answer.
<h2><a class="maxbutton-16 maxbutton maxbutton-enroll-yellow-big" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn AWS from Industry Leaders!</span></a></h2>
<h2><b>Section 6: AWS Auto Scaling, AWS Load Balancer</b></h2>
<h3><b>46. Suppose you have an application where you have to render images and also do some general computing. From the following  services which service will best fit your need?</b></h3>
<ol>
 	<li>Classic Load Balancer</li>
 	<li>Application Load Balancer</li>
 	<li>Both of them</li>
 	<li>None of these</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>You will choose an application load balancer, since it supports path based routing, which means it can take decisions based on the URL, therefore if your task needs image rendering it will route it to a different instance, and for general computing it will route it to a different instance.
<h3><b>47. What is the difference between Scalability and Elasticity?</b></h3>
Scalability is the ability of a system to increase its hardware resources to handle the increase in demand. It can be done by increasing the hardware specifications or increasing the processing nodes.

Elasticity is the ability of a system to handle increase in the workload by adding additional hardware resources when the demand increases(same as scaling) but also rolling back the scaled resources, when the resources are no longer needed. This is particularly helpful in Cloud environments, where a pay per use model is followed.
<h3><b>48. How will you change the instance type for instances which are running in your application tier and are using Auto Scaling. Where will you change it from the following areas?</b></h3>
<ol>
 	<li>  Auto Scaling policy configuration</li>
 	<li>  Auto Scaling group</li>
 	<li>  Auto Scaling tags configuration</li>
 	<li>  Auto Scaling launch configuration</li>
</ol>
<strong>Answer D.</strong>

<b>Explanation: </b>Auto scaling tags configuration, is used to attach metadata to your instances, to change the instance type you have to use auto scaling launch configuration.
<h3><b>49. You have a content management system running on an Amazon EC2 instance that is approaching 100% CPU utilization. Which option will reduce load on the Amazon EC2 instance?</b></h3>
<ol>
 	<li><b>  </b>Create a load balancer, and register the Amazon EC2 instance with it</li>
 	<li>  Create a CloudFront distribution, and configure the Amazon EC2 instance as the origin</li>
 	<li>  Create an Auto Scaling group from the instance using the CreateAutoScalingGroup action</li>
 	<li>  Create a launch configuration from the instance using the CreateLaunchConfigurationAction</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation:</b>Creating alone an autoscaling group will not solve the issue, until you attach a load balancer to it. Once you attach a load balancer to an autoscaling group, it will efficiently distribute the load among all the instances. Option B – CloudFront is a CDN, it is a data transfer tool therefore will not help reduce load on the EC2 instance. Similarly the other option – Launch configuration is a template for configuration which has no connection with reducing loads.
<h3><b>50. When should I use a Classic Load Balancer and when should I use an Application load balancer?</b></h3>
A Classic Load Balancer is ideal for simple load balancing of traffic across multiple EC2 instances, while an Application Load Balancer is ideal for microservices or container-based architectures where there is a need to route traffic to multiple services or load balance across multiple ports on the same EC2 instance.

For a detailed discussion on Auto Scaling and Load Balancer, please refer our <a href="https://www.edureka.co/blog/ec2-aws-tutorial-elastic-compute-cloud/" target="_blank" rel="noopener noreferrer"><b>EC2 AWS</b></a> blog.
<h3><b>51. What does Connection draining do?</b></h3>
<ol>
 	<li> Terminates instances which are not in use.</li>
 	<li> <b>Re-routes traffic from instances which are to be updated or failed a health check.</b></li>
 	<li> Re-routes traffic from instances which have more workload to instances which have less workload.</li>
 	<li> Drains all the connections from an instance, with one click.</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>Connection draining is a service under ELB which constantly monitors the health of the instances. If any instance fails a health check or if any instance has to be patched with a software update, it  pulls all the traffic from that instance and re routes them to other instances.
<h3><b>52.</b> <b>When an instance is unhealthy, it is terminated and replaced with a new one, which of the following services does that?</b></h3>
<ol>
 	<li> Sticky Sessions</li>
 	<li> Fault Tolerance</li>
 	<li> Connection Draining</li>
 	<li> Monitoring</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>When ELB detects that an instance is unhealthy, it starts routing incoming traffic to other healthy instances in the region. If all the instances in a region becomes unhealthy, and if you have instances in some other availability zone/region, your traffic is directed to them. Once your instances become healthy again, they are re routed back to the original instances.
<h3><b>53. What are lifecycle hooks used for in AutoScaling?</b></h3>
<ol>
 	<li>  They are used to do health checks on instances</li>
 	<li> They are used to put an additional wait time to a scale in or scale out event.</li>
 	<li> They are used to shorten the wait time to a scale in or scale out event</li>
 	<li> None of these</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>Lifecycle hooks are used for putting wait time before any lifecycle action i.e launching or terminating an instance happens. The purpose of this wait time, can be anything from extracting log files before terminating an instance or installing the necessary softwares in an instance before launching it.
<h3><strong>54. A user has setup an Auto Scaling group. Due to some issue the group has failed to launch a single instance for more than 24 hours. What will happen to Auto Scaling in this condition?</strong></h3>
<ol>
 	<li>Auto Scaling will keep trying to launch the instance for 72 hours</li>
 	<li>Auto Scaling will suspend the scaling process</li>
 	<li>Auto Scaling will start an instance in a separate region</li>
 	<li>The Auto Scaling group will be terminated automatically</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation:</b> Auto Scaling allows you to suspend and then resume one or more of the Auto Scaling processes in your Auto Scaling group. This can be very useful when you want to investigate a configuration problem or other issue with your web application, and then make changes to your application, without triggering the Auto Scaling process.
<h2><a class="maxbutton-10 maxbutton maxbutton-enroll-blue-medium" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Enroll NOW!</span></a></h2>
<h2><b>Section 7: CloudTrail, Route 53</b></h2>
<h3><b>55. You have an EC2 Security Group with several running EC2 instances. You changed the Security Group rules to allow inbound traffic on a new port and protocol, and then launched several new instances in the same Security Group. The new rules apply:</b></h3>
<ol>
 	<li>Immediately to all instances in the security group.</li>
 	<li>Immediately to the new instances only.</li>
 	<li>Immediately to the new instances, but old instances must be stopped and restarted before the new rules apply.</li>
 	<li>To all instances, but it may take several minutes for old instances to see the changes.</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation:</b> Any rule specified in an EC2 Security Group applies immediately to all the instances, irrespective of when they are launched before or after adding a rule.
<h3><b>56. To create a mirror image of your environment in another region for disaster recovery, which of the following AWS resources do not need to be recreated in the second region? ( Choose 2 answers )</b></h3>
<ol>
 	<li>Route 53 Record Sets</li>
 	<li>Elastic IP Addresses (EIP)</li>
 	<li>EC2 Key Pairs</li>
 	<li>Launch configurations</li>
 	<li>Security Groups</li>
</ol>
<strong>Answer A,B.</strong>

<b>Explanation: </b>Elastic IPs and Route 53 record sets are common assets therefore there is no need to replicate them, since Elastic IPs and Route 53 are valid across regions
<h3><b>57. A customer wants to capture all client connection information from his load balancer at an interval of 5 minutes, which of the following options should he choose for his application?</b></h3>
<ol>
 	<li>Enable AWS CloudTrail for the loadbalancer.</li>
 	<li>Enable access logs on the load balancer.</li>
 	<li>Install the Amazon CloudWatch Logs agent on the load balancer.</li>
 	<li>Enable Amazon CloudWatch metrics on the load balancer.</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation: </b>AWS CloudTrail provides inexpensive logging information for load balancer and other AWS resources This logging information can be used for analyses and other administrative work, therefore is perfect for this use case.
<h3><b>58. A customer wants to track access to their Amazon Simple Storage Service (S3) buckets and also use this information for their internal security and access audits. Which of the following will meet the Customer requirement?</b></h3>
<ol>
 	<li>Enable AWS CloudTrail to audit all Amazon S3 bucket access.</li>
 	<li>Enable server access logging for all required Amazon S3 buckets.</li>
 	<li>Enable the Requester Pays option to track access via AWS Billing</li>
 	<li>Enable Amazon S3 event notifications for Put and Post.</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation: </b>AWS CloudTrail has been designed for logging and tracking API calls. Also this service is available for storage, therefore should be used in this use case.
<h3><b>59. Which of the following are true regarding AWS CloudTrail? (Choose 2 answers)</b></h3>
<ol>
 	<li>CloudTrail is enabled globally</li>
 	<li>CloudTrail is enabled on a per-region and service basis</li>
 	<li>Logs can be delivered to a single Amazon S3 bucket for aggregation.</li>
 	<li>CloudTrail is enabled for all available services within a region.</li>
</ol>
<strong>Answer B,C.</strong>

<b>Explanation:</b> Cloudtrail is not enabled for all the services and is also not available for all the regions. Therefore option B is correct, also the logs can be delivered to your S3 bucket, hence C is also correct.
<h3><strong>60. What happens if CloudTrail is turned on for my account but my Amazon S3 bucket is not configured with the correct policy?</strong></h3>
CloudTrail files are delivered according to S3 bucket policies. If the bucket is not configured or is misconfigured, CloudTrail might not be able to deliver the log files.
<h3><strong>61. How do I transfer my existing domain name registration to Amazon Route 53 without disrupting my existing web traffic?</strong></h3>
You will need to get a list of the DNS record data for your domain name first, it is generally available in the form of a “zone file” that you can get from your existing DNS provider. Once you receive the DNS record data, you can use Route 53’s Management Console or simple web-services interface to create a hosted zone that will store your DNS records for your domain name and follow its transfer process. It also includes steps such as updating the nameservers for your domain name to the ones associated with your hosted zone. For completing the process you have to contact the registrar with whom you registered your domain name and follow the transfer process. As soon as your registrar propagates the new name server delegations, your DNS queries will start to get answered.
<h2><a class="maxbutton-10 maxbutton maxbutton-enroll-blue-medium" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn AWS Now!</span></a></h2>
<h2><b>Section 8: AWS SQS, AWS SNS, AWS SES, AWS ElasticBeanstalk</b></h2>
<h3><b>62. Which of the following services you would not use to deploy an app?</b></h3>
<ol>
 	<li>Elastic Beanstalk</li>
 	<li>Lambda</li>
 	<li>Opsworks</li>
 	<li>CloudFormation</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation:</b> Lambda is used for running server-less applications. It can be used to deploy functions triggered by events. When we say serverless, we mean without you worrying about the computing resources running in the background. It is not designed for creating applications which are publicly accessed.
<h3><b>63. How does Elastic Beanstalk apply updates?</b></h3>
<ol>
 	<li>By having a duplicate ready with updates before swapping.</li>
 	<li>By updating on the instance while it is running</li>
 	<li>By taking the instance down in the maintenance window</li>
 	<li>Updates should be installed manually</li>
</ol>
<strong>Answer A.</strong>

<b>Explanation:</b> Elastic Beanstalk prepares a duplicate copy of the instance, before updating the original instance, and routes your traffic to the duplicate instance, so that, incase your updated application fails, it will switch back to the original instance, and there will be no downtime experienced by the users who are using your application.
<h3><strong>64. How is AWS Elastic Beanstalk different than AWS OpsWorks?</strong></h3>
AWS Elastic Beanstalk is an application management platform while OpsWorks is a configuration management platform. BeanStalk is an easy to use service which is used for deploying and scaling web applications developed with Java, .Net, PHP, Node.js, Python, Ruby, Go and Docker. Customers upload their code and Elastic Beanstalk automatically handles the deployment. The application will be ready to use without any infrastructure or resource configuration.

In contrast, AWS Opsworks is an integrated configuration management platform for IT administrators or DevOps engineers who want a high degree of customization and control over operations.
<h3><b>65. What happens if my application stops responding to requests in beanstalk?</b></h3>
AWS Beanstalk applications have a system in place for avoiding failures in the underlying infrastructure. If an Amazon EC2 instance fails for any reason, Beanstalk will use Auto Scaling to automatically launch a new instance. Beanstalk can also detect if your application is not responding on the custom link, even though the infrastructure appears healthy, it will be logged as an environmental event( e.g a bad version was deployed) so you can take an appropriate action.

For a detailed discussion on this topic, please refer <a href="https://www.edureka.co/blog/aws-lambda-tutorial" target="_blank" rel="noopener noreferrer"><b>Lambda AWS</b> </a>blog.
<h2><a class="maxbutton-22 maxbutton maxbutton-certification-blue-big" href="https://www.edureka.co/cloudcomputing" target="_blank" rel="noopener"><span class="mb-text">Learn AWS from our Experts!</span></a></h2>
<h2><b>Section 9: AWS OpsWorks, AWS KMS</b></h2>
<h3><strong>66. How is AWS OpsWorks different than AWS CloudFormation?</strong></h3>
OpsWorks and CloudFormation both support application modelling, deployment, configuration, management and related activities. Both support a wide variety of architectural patterns, from simple web applications to highly complex applications. AWS OpsWorks and AWS CloudFormation differ in abstraction level and areas of focus.

AWS CloudFormation is a building block service which enables customer to manage almost any AWS resource via JSON-based domain specific language. It provides foundational capabilities for the full breadth of AWS, without prescribing a particular model for development and operations. Customers define templates and use them to provision and manage AWS resources, operating systems and application code.

In contrast, AWS OpsWorks is a higher level service that focuses on providing highly productive and reliable DevOps experiences for IT administrators and ops-minded developers. To do this, AWS OpsWorks employs a configuration management model based on concepts such as stacks and layers, and provides integrated experiences for key activities like deployment, monitoring, auto-scaling, and automation. Compared to AWS CloudFormation, AWS OpsWorks supports a narrower range of application-oriented AWS resource types including Amazon EC2 instances, Amazon EBS volumes, Elastic IPs, and Amazon CloudWatch metrics.
<h3><strong>67.</strong><b> I created a key in Oregon region to encrypt my data in North Virginia region for security purposes. I added two users to the key and an external AWS account. I wanted to encrypt an object in S3, so when I tried, the key that I just created was not listed.  What could be the reason?  </b></h3>
<ol>
 	<li>External aws accounts are not supported.</li>
 	<li>AWS S3 cannot be integrated KMS.</li>
 	<li>The Key should be in the same region.</li>
 	<li>New keys take some time to reflect in the list.</li>
</ol>
<strong>Answer C.</strong>

<b>Explanation: </b>The key created and the data to be encrypted should be in the same region. Hence the approach taken here to secure the data is incorrect.
<h3><b>68.  A company needs to monitor the read and write IOPS for their AWS MySQL RDS instance and send real-time alerts to their operations team. Which AWS services can accomplish this?</b></h3>
<ol>
 	<li>Amazon Simple Email Service</li>
 	<li>Amazon CloudWatch</li>
 	<li>Amazon Simple Queue Service</li>
 	<li>Amazon Route 53</li>
</ol>
<strong>Answer B.</strong>

<b>Explanation: </b>Amazon CloudWatch is a cloud monitoring tool and hence this is the right service for the mentioned use case. The other options listed here are used for other purposes for example route 53 is used for DNS services, therefore CloudWatch will be the apt choice.
<h3><b>69. What happens when one of the resources in a stack cannot be created successfully in AWS OpsWorks?</b></h3>
When an event like this occurs, the “automatic rollback on error” feature is enabled, which causes all the AWS resources which were created successfully till the point where the error occurred to be deleted. This is helpful since it does not leave behind any erroneous data, it ensures the fact that stacks are either created fully or not created at all. It is useful in events where you may accidentally exceed your limit of the no. of Elastic IP addresses or maybe you may not have access to an EC2 AMI that you are trying to run etc.
<h3><b>70. What automation tools can you use to spinup servers?</b></h3>
Any of the following tools can be used:
<ul>
 	<li>Roll-your-own scripts, and use the AWS API tools.  Such scripts could be written in bash, perl or other language of your choice.</li>
 	<li>Use a configuration management and provisioning tool like puppet or its successor Opscode Chef.  You can also use a tool like Scalr.</li>
 	<li>Use a managed solution such as Rightscale.</li>
</ul>
&nbsp;

<hr />

<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">
<h1 data-inline-fontsize="true" data-inline-lineheight="true" data-fontsize="22" data-lineheight="26">1. Explain what is AWS ?</h1>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> AWS attains as Amazon Web Service; this is a gathering of remote computing settings also identified as cloud computing policies. This unique realm of cloud computing is also recognized as IaaS or Infrastructure as a Service.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

2. What are the key components of AWS ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> The fundamental elements of AWS are
<ul>
 	<li>Route 53: A DNS web service</li>
 	<li>Easy E-mail Service: It permits addressing e-mail utilizing RESTFUL API request or through normal SMTP</li>
 	<li>Identity and Access Management: It gives heightened protection and identity control for your AWS account</li>
 	<li>Simple Storage Device or (S3): It is a warehouse equipment and the well-known widely utilized AWS service</li>
 	<li>Elastic Compute Cloud (EC2): It affords on-demand computing sources for hosting purposes. It is extremely valuable in trouble of variable workloads</li>
 	<li>Elastic Block Store (EBS): It presents persistent storage masses that connect to EC2 to enable you to endure data beyond the lifespan of a particular EC2</li>
 	<li>CloudWatch: To observe AWS sources, It permits managers to inspect and obtain key Additionally, one can produce a notification alert in the state of crisis.</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

3. Explain what is S3 ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> S3 holds for Simple Storage Service. You can utilize S3 interface to save and recover the unspecified volume of data, at any time and from everywhere on the web. For S3, the payment type is “pay as you go”.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

4. What does an AMI include ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> An AMI comprises the following elements
<ul>
 	<li>A template to the source quantity concerning the instance</li>
 	<li>Launch authorities determine which AWS accounts can avail the AMI to drive instances</li>
 	<li>A base design mapping that defines the amounts to join to the instance while it is originated.</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

5. How can you send request to Amazon S3 ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Amazon S3 is a REST service, you can transmit the appeal by applying the REST API or the AWS SDK wrapper archives that envelop the underlying Amazon S3 REST API.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

6. How many buckets can you create in AWS by default ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> In each of your AWS accounts, by default, You can produce up to 100 buckets.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

7. Explain can you vertically scale an Amazon instance ? How ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>Surely, you can vertically estimate on Amazon instance. During that
<ul>
 	<li>Twist up a fresh massive instance than the one you are currently governing</li>
 	<li>Delay that instance and separate the source webs mass of server and dispatch</li>
 	<li>Next, quit your existing instance and separate its source quantity</li>
 	<li>Note the different machine ID and connect that source mass to your fresh server</li>
 	<li>Also, begin it repeatedly Study <a href="https://svrtechnologies.com/amazon-web-services-training" target="_blank" rel="noopener">AWS Training Online</a> From Real Time Experts</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

8. Explain what is T2 instances ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> T2 instances are outlined to present average baseline execution and the ability to explode to powerful execution as needed by the workload.<strong>
</strong>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

9. In VPC with private and public subnets, database servers should ideally be launched into which subnet ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Among private and public subnets in VPC, database servers should ideally originate toward separate subnets.<strong>
</strong>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

10. Explain how the buffer is used in Amazon web services ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> The buffer is utilized to deliver the system further robust to handle traffic or load by synchronizing different component. Usually, elements sustain and process the demands in an unreliable mode, With the aid of buffer, the elements will be (<a href="https://svrtechnologies.com/sap-training" target="_blank" rel="noopener">sap training</a>) equivalent and will operate at the similar speed to accommodate high-speed services.

</div>
</div>
</div>
</div>
</div>
&nbsp;

&nbsp;

11. While connecting to your instance what are the possible connection issues one might face ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> The possible connection errors one might encounter while connecting instances are
<ul>
 	<li>Connection timed out</li>
 	<li>User key not recognized by the server</li>
 	<li>Host key not found, permission denied</li>
 	<li>Unprotected private key file</li>
 	<li>Server refused our key or No supported authentication method available</li>
 	<li>Error using MindTerm on Safari Browser</li>
 	<li>Error using Mac OS X RDP Client</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

12. Explain Elastic Block Storage ? What type of performance can you expect ? How do you back it up? How do you improve performance ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> That indicates it is RAID warehouse to begin with, so it’s irrelevant and faults tolerant. If disks expire in the RAID you don’t miss data. Excellent! It is more virtualized, therefore you can provision and designate warehouse, and connect it to your server with multiple API appeals. No calling the storage specialist and asking him or her to operate specific requests from the hardware vendor.

Execution on EBS can manifest variability. Such signifies that can run above the SLA enforcement level, suddenly descend under it. The SLA gives you among a medium disk I/O speed you can foresee. That can prevent any groups particularly performance specialists who suspect stable and compatible disk throughput on a server. Common physically entertained servers perform that direction. Pragmatic AWS cases do not.

Backup EBS masses by utilizing the snap convenience through API proposal or by a GUI interface same elasticfox.

Progress execution by practicing Linux software invasion and striping over four extents.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

13. What is S3 ? What is it used for ? Should encryption be used ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>S3 implies for Simple Storage Service. You can believe it similar ftp warehouse, wherever you can transfer records to and from beyond, merely not uprise it similar to a filesystem. AWS automatically places your snaps there, at the same time AMIs there. sensitive data is treated with Encryption, as S3 is an exclusive technology promoted by Amazon themselves, and as still unproven vis-a-vis a protection viewpoint.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

14. What is an AMI ? How do I build one ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> AMI holds for Amazon Machine Image. It is efficiently a snap of the source filesystem. Products appliance servers have a bio that shows the master drive report of the initial slice on a disk. A disk form though can lie anyplace physically on a disc, so Linux can boot from an absolute position on the EBS warehouse interface.

Create a unique AMI at beginning rotating up and instance from a granted AMI. Later uniting combinations and components as needed. Comprise wary of setting delicate data over an AMI (<a href="https://www.svrtechnologies.com/salesforce/learn-salesforce-online" target="_blank" rel="noopener">learn salesforce online</a>). For instance, your way credentials should be joined to an instance later spinup. Among a database, mount an external volume that carries your MySQL data next spinup actually enough.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

15. What is auto-scaling ? How does it work ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>AWS enables you to configure and automatically store and twist up fresh instances outwardly the necessary for your invasion because of the characteristic feature of Autoscaling. You do this with establishing thresholds and metrics to observe. When these thresholds are intersected a fresh instance of your choice will be turned up, configured, and flowed toward the load balancer provisions. Voila, you’ve mounted horizontally without unspecified operator interruption!

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

16. What automation tools can I use to spinup servers ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>The common visible step is to roll-your-own scripts and adopts the AWS API tools. Such scripts could be drafted in bash, Perl or another language or your preference. Following possibility is to practice a configuration supervision and provisioning devices like puppet or excellent its follower Opscode Chef. Your strength also looks towards a device same as Scalr. Finally, you can quit with a guided solution such as RightScale.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

17. What is configuration management ? Why would I want to use it with cloud provisioning of resources ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>Configuration authority has been throughout for a prolonged period in network services and systems control. Yet the rising reputation of it has been confined. Maximum systems managers configure computers as the software was improved before version controller – that is manually performing modifications on servers. Every server can later and customarily is slightingly modified. Troubleshooting though is outspoken as you log in to the case and work on it instantly. Configuration authority delivers a massive computerization equipment into the picture, managing servers similar twines of a puppet. This drives regularity, excellent works, and reproducibility as all configs are maintained and versioned. It also proposes a distinct way of operating which is the hugest barrier to its adoption.

Join the cloud, and configuration administration becomes equivalent major critical. That’s because pragmatic servers such as amazons EC2 instances are enormously limited reliable than physical ones. You surely need a tool to reconstruct them as-is at any consequence. This promotes vigorous practices like computerization, reproducibility and failure restoration into the internal frame.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

18. Explain how you would simulate perimeter security using Amazon Web Services model ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Conventional boundary security that previously familiar with utilizing firewalls and so hence is not recommended in the Amazon EC2 environment. AWS helps security associations. One can build a protection group toward a jump box with ssh way – barely port 22 open. From where a webserver association and database association are formed. The webserver group concedes 80 and 443 from the system, but port 22 *only* of the jump box assembly. Additional, the database association provides port 3306 of the webserver assembly and port 22 from the jump box group. Attach several devices to the web server group and they can all hit the database. No one from the environment can, and no one can straight ssh to any of your cases.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

19. What is the importance of buffer in Amazon Web Services ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>Across multiple AWS instances, an Elastic Load Balancer guarantees that the incoming traffic is distributed optimally. A buffer will synchronize various elements and builds the pattern additional flexible to a burst of load or transactions. The elements are inclined to work in an unbalanced way of acquiring and processing the appeals. The buffer forms the stability associating multiple types of equipment and crafts them work at the identical speed to fulfill increased accelerated services.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

20. What is the way to secure data for carrying in the cloud ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> One thing need be assured that no one should seize the data in the cloud. while information is migrating from one place to another and besides there should not be unspecified leakage by the safety key from various storerooms in the cloud. Dissociation of data of supplementary organizations’ data and next encrypting it by medians of validated techniques is one of the alternatives.

</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

21. Name the several layers of Cloud Computing ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> the list of layers of the cloud computing is given below
<ul>
 	<li>PaaS: – Platform as a Service</li>
 	<li>IaaS:– Infrastructure as a Service</li>
 	<li>SaaS:– Software as a Service</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

22. What are the components involved in Amazon Web Services ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> There are mainly four components included that are addressed here.
<ul>
 	<li><strong>Amazon S3:</strong> by this, one can recover the fundamental data which is conquered in formulating cloud architectural pattern and volume of exhibited data also can be saved in this segment that is the result of the key designated.</li>
 	<li><strong>Amazon EC2 instance:</strong> accommodating to drive a large distributed system on the Hadoop group. Computerized parallelization and work schedule can be performed by this segment.</li>
 	<li><strong>Amazon SQS:</strong> this element acts as a negotiator among various controllers. Further worn for cushioning wants these are achieved by the administrator of Amazon.</li>
 	<li><strong>Amazon SimpleDB:</strong> accommodates for depositing the transitional state log and the tasks executed by the users.</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

23. Distinguish between scalability and flexibility ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> The capacity of any scheme to intensify the responsibilities on hand on its existing appliance devices to seize variance in the unit is known as scalability. The aptitude of a scheme to enlarge the responsibilities on hand on its grant and additional device resources is identified as versatility, therefore allowing the business to assemble command externally of putting in the foundation at all. AWS has several configuration management solutions for AWS scalability, flexibility, availability and management.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

24. Name the various layers of the cloud architecture ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> There are mainly five layers and they are as follows
<ol>
 	<li>CC:- Cluster Controller</li>
 	<li>SC:- Storage Controller</li>
 	<li>CLC:- Cloud Controller</li>
 	<li>NC:- Node Controller</li>
 	<li>Walrus <a href="https://www.svrtechnologies.video/p/amazon-web-services-training-video-tutorials" target="_blank" rel="noopener">AWS Video Training</a></li>
</ol>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

25. Define Auto Scaling ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Auto-scaling is one of the conspicuous characteristics feature of AWS anywhere it authorizes you to systematize and robotically obligation and twist up new models externally that necessary for your entanglement. This can be accomplished by initiating brims and metrics to view. If these approaches are defeated, a new example of your choice will be configured, twisted up and cloned into the weight planner gathering.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

26. Which automation gears can help with spinup services ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> For the written scripts we can use spinup services with the help of API tools.These scripts could be coded in bash, Perl, or any another language of your choice.There is one more alternative that is patterned control and stipulating devices before-mentioned as a dummy or advanced descendant. A machine termed as Scalar can likewise be utilized and ultimately we can proceed with a constrained expression like a RightScale.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

27. Is it possible to scale an Amazon instance vertically ? How ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Yes, it is possible to scale an Amazon instance vertically because of an unbelievable characteristic of cloud virtualization and AWS. Spinup is a huge case while correlated to the one which you are working with. Let up the case and distribute the source EBS bulk of this server and eliminate. Subsequent, end your existing instance, exclude its root volume. Enter down the peculiar device ID and join source volume to your fresh server and begin it repeatedly. This is the way to scaling vertically in position.

Find out how AWS can scale vertically by going through the <em><a href="https://intellipaat.com/tutorial/amazon-web-services-aws-tutorial/" target="_blank" rel="noopener">AWS Tutorial</a>.</em>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

28. How the processes start, stop and terminate works ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>
<ul>
 	<li><strong>Starting and stopping of an instance:</strong> If an instance goes arrested or died, the instance performs a normal power cut and then transfer over to a sealed area. You can build the case then for all the EBS masses of Amazon persist and associated. If an instance is in ending state, suddenly you will not get charged to the additional instance</li>
 	<li><strong>Finishing the instance:</strong> If an instance goes stopped it serves to perform a standard blackout, therefore the EBS capacities which are connected will get excluded save the volume’s delete On Termination feature is fixed to zero. In such instances, the instance will get eliminated and cannot set it up afterward.</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

29. Explain in detail the function of Amazon Machine Image (AMI) ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> An Amazon Machine Image AMI is a pattern that comprises a software conformation (for instance, an operative system, a request server, and applications). From an AMI, we present an example, which is a duplicate of the AMI successively as a virtual server in the cloud. We can even offer plentiful examples of an AMI.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

30. If I’m expending Amazon Cloud Front, can I custom Direct Connect to handover objects from my own data centre ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Certainly. Amazon Cloud Front stipulations culture rises computing sources of separate AWS. By AWS Direct Connect, you will be accelerating with the appropriate information substitution rates.

</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

31. If my AWS Direct Connect flops, will I lose my connection ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> If a gridlock AWS Direct connects has been transposed, in the event of a let-down, it will convert over to the next one. It is voluntary to allow Bidirectional Forwarding Detection (BFD) while systematizing your rules to safeguard quicker identification and failover. Proceeding the opposite hand, if you have built a backup IPsec VPN connecting as an option, all VPC transactions will failover to the backup VPN association routinely.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

32. What is AWS Certificate Manager ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> AWS Certificate Manager (ACM) manages the complexity of extending, provisioning, and regulating certificates granted over ACM (ACM Certificates) to your AWS-based websites and forms. You work ACM to petition and maintain the certificate and later practice other AWS services to provision the ACM Certificate for your website or purpose. As designated in the subsequent instance, ACM Certificates are currently ready for performance with only Elastic Load Balancing and Amazon CloudFront. You cannot handle ACM Certificates outside of AWS.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

33. Explain What is Redshift ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> The executes it easy and cost-effective to efficiently investigate all your data employing your current marketing intelligence devices which is a completely controlled, high-speed, it is petabyte-scale data repository service known as Redshift.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

34. Mention what are the differences between Amazon S3 and EC2 ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer</strong>:<strong> S3:</strong> Amazon S3 is simply a storage aid, typically applied to save huge binary records. Amazon too has additional warehouse and database settings, same as RDS to relational databases and DynamoDB concerning NoSQL.

<strong>EC2:</strong> An EC2 instance is similar to a foreign computer working Linux or Windows and on which you can install whatever software you need, including a Network server operating PHP <strong>code</strong> and a database server.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

35. Explain what is C4 instances ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> C4 instances are absolute for compute-bound purposes that serve from powerful-performance processors. <a href="https://svrtechnologies.com/aws-interview-questions/aws-interview-questions-and-answers" target="_blank" rel="noopener">AWS Interview Questions and Answers</a>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

36. Explain what is DynamoDB in AWS ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Amazon DynamoDB is a completely controlled NoSQL database aid that renders quick and anticipated execution with seamless scalability. You can perform Amazon DynamoDB to formulate a database table that can save and reclaim any quantity of data, and help any level of application transactions. Amazon DynamoDB automatically increases the data and transactions for the table above an adequate number of servers to supervise the inquiry function designated by the customer and the volume of data saved, while keeping constant and quick execution.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

37. Explain what is ElastiCache ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> A web service that executes it comfortable to set up, maintain, and scale classified in-memory cache settings in the cloud is known as ElastiCache.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

38. What is the AWS Key Management Service ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> A managed service that makes it easy for you to create and control the encryption keys used to encrypt your data is known as the AWS Key Management Service (AWS KMS).

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

39. What is AWS WAF ? What are the potential benefits of using WAF ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS applications that are promoted to Amazon CloudFront and gives you regulate path to your content. Based on circumstances that you stipulate, such as the IP addresses that grants originate from or the consequences of query series, CloudFront returns to applications either with the petitioned content or with an HTTP 403 situation code (Forbidden). You can further configure CloudFront to restore a pattern failure page when an application is obstructed.

<strong>Advantages of utilizing WAF:</strong>
<ul>
 	<li>Further security versus web initiatives relating circumstances that you designate. You can describe situations by managing characteristics of web inquiries such as the IP address that the applications originate from, the rates in headers, chains that rise in the applications, and the presence of hateful SQL code in the call, which is recognized as SQL injection.</li>
 	<li>Rules that you can reuse for various network appeals</li>
 	<li>Real-time metrics and examined web demands</li>
 	<li>Computerized command practicing the AWS WAF API</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

40. What is Amazon EMR ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Amazon Elastic MapReduce (Amazon EMR) is a survived cluster stage that interprets working big data structures, before-mentioned as Apache Spark and Apache Hadoop, on AWS to treat and investigate enormous volumes of data. By adopting these structures and relevant open-source designs, such as Apache Pig and Apache Hive, you can prepare data for analytics goals and marketing intellect workloads. Additionally, you can use Amazon EMR to convert and migrate vast masses of information into and of other AWS data repositories and databases, such as Amazon DynamoDB and Amazon Simple Storage Service (Amazon S3).

</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

41. What is AWS Data Pipeline ? and what are the components of AWS Data Pipeline ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> A network service that you can apply to automate the migration and alteration of information are called AWS Data Pipeline. With <a href="https://aws.amazon.com/" target="_blank" rel="noopener">AWS</a> you can specify data-driven workflows so that businesses can be reliant on the auspicious achievement of early tasks.

<strong>The subsequent elements of AWS Data Pipeline act collectively to obtain your data:</strong>

⦁ A pipeline key designates the market thought of your data supervision. For extra data, view Pipeline Definition File Syntax.

⦁ A pipeline inventories and tracks assignments. You upload your pipeline clarity to the pipeline and when stimulate the pipeline. You can regulate the pipeline description for a working pipeline and stimulate the pipeline repeatedly for it to get the result. You can deactivate the pipeline, change a data reservoir, and before initiate the pipeline newly. If you are ceased with your pipeline, you can eliminate it.

⦁ Task Runner surveys for duties and then executes those responsibilities. For example, Task Runner could duplicate log records to Amazon S3 and drive Amazon EMR groups. Task Runner is uns automatically on devices designed by your pipeline keys. You can compose a custom task runner form, or you can do the Task Runner application that is presented by AWS Data Pipeline.<a href="https://svrtechnologies.com/aws-interview-questions/aws-ec2-interview-questions" target="_blank" rel="noopener">AWS EC2 Interview Questions</a>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

42. What is Amazon Kinesis Firehose ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> A fully managed service for delivering real-time streaming data to destinations such as Amazon Simple Storage Service (Amazon S3) and Amazon Redshift is known as Amazon Kinesis Firehose.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

43. What Is Amazon CloudSearch and its features ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>A thoroughly managed service in the cloud that creates it simple to set up, maintain, and estimate a search solution for your website or application is called Amazon CloudSearch.

we can use Amazon CloudSearch to catalog and explore both plain text and structured data. Amazon CloudSearch characteristics:
<ul>
 	<li>Entire text search with language-specific text processing</li>
 	<li>Range searches</li>
 	<li>Prefix searches</li>
 	<li>Boolean search</li>
 	<li>FacetingTerm boosting</li>
 	<li>Highlighting</li>
 	<li>Autocomplete Advices</li>
</ul>
</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

44. Explain what is Regions and Endpoints in AWS ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> An endpoint is a URL that is the entry point for a web service.To reduce data latency in your applications, most Amazon Web Services products allow you to select a regional endpoint to make your requests.

A few services, such as Amazon EC2, let you specify an endpoint that does not include a specific region. Amazon Web Services TutorialsSome services, such as IAM, do not support regions; their endpoints, therefore, do not include a region.
<a href="https://svrtechnologies.com/amazon-web-services-training" target="_blank" rel="noopener">Amazon Web Services Tutorials</a>

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

45. What are the different types of cloud services ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Infrastructure as a Service (IaaS), Software as a Service (SaaS), Platform as a Service (PaaS), and Data as a Service (DaaS).

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

46. What is SimpleDB ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> A structured records or data repository that encourages indexing and data doubts to both EC2 and S3 is known as SimpleDB.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

47. What is the type of architecture, where half of the workload is on the public load while at the same time half of it is on the local storage ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Hybrid cloud architecture.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

48. Should encryption be used for S3 ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Encryption should be examined for delicate information or data as S3 is a proprietary technology.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

49. What are the various AMI design options ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong>Fully Baked AMI, JeOS (just enough operating system) AMI, and Hybrid AMI.

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
</div>
</div>
<div class="fusion-fullwidth fullwidth-box nonhundred-percent-fullwidth non-hundred-percent-height-scrolling">
<div class="fusion-builder-row fusion-row ">
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-blend-mode 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

50. What is Geo Restriction in CloudFront ?

</div>
<div class="fusion-clearfix"></div>
</div>
</div>
<div class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last 1_1">
<div class="fusion-column-wrapper" data-bg-url="">
<div class="fusion-text">

<strong>Answer:</strong> Geo restriction, also known as geoblocking, is used to prevent users in specific geographic locations from accessing content that you’re distributing through a CloudFront web distribution.

</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
