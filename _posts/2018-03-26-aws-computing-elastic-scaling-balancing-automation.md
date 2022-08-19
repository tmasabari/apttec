---
layout: post
title: AWS Computing, Elastic scaling & balancing, Automation
date: 2018-03-26 10:20
author: tmasabari
comments: true
categories: [Automation, AWS, Elasticity]
---
<h2>Computing, Elastic scaling &amp; balancing</h2>
<ul>
 	<li>Virtual servers</li>
 	<li>internet access</li>
 	<li>firewall</li>
 	<li>distributing and routing ip</li>
 	<li>scaling infra</li>
</ul>
8 Services
<ol>
 	<li>Elastic Compute Cloud - EC2
<ol>
 	<li>EC2 instance - Virtual machine in one of the virtual server of data center</li>
 	<li>re-sizable compute capacity - increase decrease capacity in minutes</li>
 	<li>launches 1000s of instances in less time</li>
 	<li>launch numerous os, instance type = hardware sizes(cpu, ram, storage, network), softwares ec</li>
 	<li>integrated with other services</li>
 	<li>99.95 % availability - 4 hours downtime in a year</li>
 	<li>with VPC create secure network</li>
 	<li>cost -pay by hour, rates are lower then on premises infra</li>
</ol>
</li>
 	<li>AWS Lambda
<ol>
 	<li>auto respond to triggered event</li>
 	<li>executes the independent code</li>
 	<li>from EC2 instances on virtual servers</li>
</ol>
</li>
 	<li>ECS - EC2 container service
<ol>
 	<li>docker containers on cluster of virtual servers from EC2</li>
</ol>
</li>
 	<li>Auto Scaling - group of servers based up on demand</li>
 	<li>Elastic Load balancing - distribute traffic across servers</li>
 	<li>Route 53 - DNS service to route the traffic to resources (web sites, virtual servers, load balancer)</li>
 	<li>VPC - isolated virtual network</li>
 	<li>AWS Direct Connect - dedicated connection from corporate premises (data centers or office)</li>
</ol>
<h3>6 Key concepts</h3>
<ol>
 	<li>Instances and AMI
<ol>
 	<li>AMI - Amazon machine image. <strong>template for the root volume of the instance</strong> -
<ol>
 	<li>contains software configuration details
<ol>
 	<li>OS</li>
 	<li>additional applications</li>
</ol>
</li>
 	<li>public ami - any one can access</li>
 	<li>private ami - users of paritcular accounts, group of accounts only access the image</li>
 	<li>Marketplace
<ol>
 	<li>customized images from vendors</li>
</ol>
</li>
 	<li>2 types of virtualization (AMI)
<ol>
 	<li>PV - ParaVirtual - earlier amazon recommended this - specialized drivers installed in AMI. improves the performances network.</li>
 	<li>HVM - Hardware Virtual Machine - now the drivers included here as well. So most of the AMIs are available in this format.</li>
</ol>
</li>
 	<li>AMIs can create ec2 instances</li>
 	<li>From EC2 instance we can create AMIs</li>
 	<li>Customized AMI</li>
 	<li>community AMIs</li>
 	<li>Licensed AMIs
<ol>
 	<li>purchase license from amazon
<ol>
 	<li>check the marketplace to check the cost</li>
</ol>
</li>
 	<li>Bring your own license</li>
</ol>
</li>
</ol>
</li>
 	<li>root storage
<ol>
 	<li>instance store - connected as an <strong>internal storage device to the host physical machine. </strong>(historically it was the only option available, so instance could not restart all. So Amazon introduced EBS). has to be created while creating instance. it can't be assigned later</li>
 	<li>ebs -connected as an <strong>external storage device to the host physical machine.</strong></li>
</ol>
</li>
 	<li>Contains launch permissions
<ol>
 	<li>identify AWS Account which has permissons to launch instances</li>
</ol>
</li>
 	<li>Instance - Copy of AMI operates <strong>as a virtual server</strong> on host computer in AWS data center</li>
 	<li>Choose AMI, configure additional settings - Save and launch the instance</li>
</ol>
</li>
 	<li>VPC and subnets
<ol>
 	<li>virtual network for your account</li>
 	<li>Every account has default VPC</li>
 	<li>subnet is <strong>range of IP address in a VPC</strong> in an Availability Zone</li>
</ol>
</li>
 	<li>Security groups
<ol>
 	<li>Functions like a firewall</li>
 	<li>controls incoming and outgoing traffic</li>
 	<li></li>
</ol>
</li>
 	<li>Amazon Route 53 hosted zones
<ol>
 	<li>Route 53 translates domain name to ip address
<p id="aMUHltw"><img class=" wp-image-1260 alignright" src="/wp-content/uploads/2018/03/img_5ab3898b1dc01.png" alt="" width="297" height="114" /></p>
</li>
 	<li>Search for a domain name and register a name on route 53</li>
 	<li>Transfer existing domain names</li>
 	<li>Hosted zone
<ol>
 	<li>similar to DNS Zone file-contains its own configuration and meta data information</li>
 	<li>While creating a hosted zone, you get four name servers to ensure high availability.</li>
 	<li>allows organizing the DNS records</li>
 	<li>group of dns records for main domain and subdomains that route 53 use to register</li>
</ol>
</li>
</ol>
</li>
 	<li>Auto scaling groups
<ol>
 	<li>ensures availability and performance</li>
 	<li>increases the instances during peak load and decreases instances on non peak hours to save cost</li>
 	<li>Auto scaling group
<ol>
 	<li>group of EC2 instances which can grow or shrink based on demand</li>
 	<li>you can specify minimum instances required, preferred capacity , maximum instances and criteria</li>
 	<li>ensures minimum instances always available</li>
</ol>
</li>
 	<li>Set policies
<ol>
 	<li>scale out policy
<ol>
 	<li>example average cpu utilization &gt; 70%</li>
</ol>
</li>
 	<li>scale in
<ol>
 	<li>Example average cpu utilization &lt; 20 %</li>
 	<li>trafffic draining is used to wait for specific duration before terminating instances</li>
</ol>
</li>
</ol>
</li>
</ol>
</li>
 	<li>Load balancer
<ol>
 	<li>Load balancer can point to multiple regions or AZs to ensure high availability</li>
 	<li>high fault tolerance - automatically transfer the traffic from unhealthy instances to healthy instances</li>
 	<li>Depending up on load when auto scaling groups launches or terminates the instances, load balancer automatically makes necessary arrangements</li>
</ol>
</li>
</ol>
<h4>EC2 concepts</h4>
<ul>
 	<li style="box-sizing: border-box; font-family: AmazonEmber, 'Helvetica Neue', Helvetica, Arial, sans-serif; font-size: 14px;">An <span style="box-sizing: border-box; font-family: AmazonEmberBold, 'Helvetica Neue Bold', 'Helvetica Neue', Helvetica, Arial, sans-serif;">Amazon Machine Image</span> (AMI) is a template that defines your operating environment, including the operating system. A single AMI can be used to launch one or thousands of instances.</li>
 	<li>Instances are created by launching an Amazon Machine Image (AMI) on a particular instance type.scale the number of instances you are running up or down on demand, either manually or automatically, using <a href="http://aws.amazon.com/autoscaling/" target="_self">Auto Scaling</a>.</li>
 	<li><strong>Instance Types</strong> comprise various combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type has one or more size options that address different workload sizes.</li>
 	<li><strong>Instance Families</strong> are collections of instance types designed to meet a common goal. To make it easier for you to select the best option for your applications, Amazon EC2 instance types are grouped together into families based on target application profiles.</li>
 	<li>A <strong>vCPU</strong> is a virtual Central Processing Unit (CPU). A multicore processor has two or more vCPUs.
<ul>
 	<li>CPU can have multiple cores
<ul>
 	<li>1 cores - 1 thread</li>
</ul>
</li>
 	<li>multiple cores - hyper thread
<ul>
 	<li>1 core - 2 or multiple threads</li>
</ul>
</li>
 	<li>1 vCPU is <strong>not</strong> equivalent to <strong>physical CPU or Core</strong> but <strong>equivalent to 1 thread</strong>.</li>
</ul>
</li>
 	<li>Tag-some times developers forget to delete VMS. Tag your VMs as TEMP/DEV and delete them at night using scripts.</li>
 	<li>Prevent accidental termination (checkbox)
<ul>
 	<li>protects from scripts terminating this instance</li>
 	<li>you have to uncheck to delete the instances</li>
</ul>
</li>
 	<li>Detailed monitoring - Enable cloudwatch detailed monitoring checkbox
<ul>
 	<li>by default metrics of 5 minutes duration is free</li>
 	<li>If you enable this 5 dollar per month will be charged for metrics collected for each minute.</li>
</ul>
</li>
 	<li>Tenancy
<ul>
 	<li>Shared</li>
 	<li>Dedicated - in a physical server, only VMs belongs to the same acccount will be placed - 0.2$ per hour as dedicated rent fees</li>
 	<li>Dedicated host - rent a physical server host from amazon, you can have multiiple instances</li>
</ul>
</li>
 	<li>Placement groups
<ul>
 	<li>if a requirement instances should be with in a same physical area for <strong>low network latency and high network throughput</strong></li>
 	<li>in a same availlability zones, aws tried to find closer hosts
<ul>
 	<li>can't span multiple AZ</li>
</ul>
</li>
 	<li>speed up to 10 Gbps. your instance should also support this speed</li>
 	<li>at the time of creation of instance only placement group can be specified</li>
</ul>
</li>
 	<li>T2 unlimited
<ul>
 	<li>additional computing power (bursted)</li>
 	<li>additional charges apply</li>
</ul>
</li>
 	<li>user data
<ul>
 	<li>additional data/scripts.</li>
 	<li>This will execute automatically after instance creation</li>
 	<li>google "ec 2 user data" for your AMI/Os type.
<ul>
 	<li>for windows power shell script for various operations like IIS are already available</li>
 	<li>just copy paste the script to the user data</li>
</ul>
</li>
</ul>
</li>
 	<li>key pair
<ul>
 	<li>linux - all the transmission is encrypted using public key private key mechanism
<ul>
 	<li>use ssh client famous ony putty</li>
 	<li>ssh username = ec2_user@publicip</li>
 	<li>username depends up on the AMI. check the documentation</li>
</ul>
</li>
 	<li>windows - required to decrypt the windows administrator password
<ul>
 	<li>rdp - remote desktop - connection</li>
 	<li>actions - instance - GetWindows password</li>
</ul>
</li>
</ul>
</li>
 	<li>Status check Tab of instance
<ul>
 	<li>host status - system status checks</li>
 	<li>VM status - private status checks</li>
</ul>
</li>
 	<li>Monitoring
<ul>
 	<li>memory / RAM utilization is not displayed. aws gets the status  at hypervisior level so it could not provide</li>
 	<li>hypervisior vendors- hyper-v from MicroSoft, vmware, Oracle VirtualBox etc.</li>
 	<li>aws uses xen hypervisior from Citrix</li>
 	<li>scripts are available in web sites which create custom metrics. install in your os and sends to cloud watch</li>
</ul>
</li>
 	<li>Create AMI
<ul>
 	<li>select instance</li>
 	<li>Action -&gt; create image</li>
 	<li>created images are displayed in AMIs page within EC2</li>
</ul>
</li>
</ul>
<ul>
 	<li><a href="http://www.apttec.com/cloud-aws-network-basics-vpc/">VPC</a></li>
 	<li>EC2 instance</li>
 	<li>AMI - template</li>
 	<li>Select instance type
<ul>
 	<li>Compute / CPU - irrespective of underlying hardware provides the specified computing capacity</li>
 	<li>Memory</li>
 	<li>Storage - disk subsystem is shared across instances . only the specified storage is allocated</li>
</ul>
</li>
 	<li>in case if shared resource is not fully utilized, instance get higher share of the resource</li>
 	<li>Additional types
<ul>
 	<li>on demand - pay per hour</li>
 	<li>reserved - 1month to 3 years considerable discount</li>
 	<li>schedueld - available for one year, as per specific recurring schedule</li>
 	<li>spot instances - availale over bid. use as long as available. if application is flexible about the timings to run the applications
<ul>
 	<li>spot instances price can go over the on demand price as well</li>
 	<li>you can set the max price as well. once the price goes above the max bid the instance will be automatically terminated</li>
 	<li>notification 2 minutes before the termination</li>
 	<li>if bid price lower down the instance will not be started again</li>
 	<li>queues which process the messages in seconds</li>
 	<li>spot blocks
<ul>
 	<li>you can say no of instances and no of hours</li>
 	<li>the moment the prices is with in the range, instances will be created and will be executing for the duration</li>
 	<li>but you dont know when the instances will be created</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>Supports 2 platforms</li>
</ul>
<ol>
 	<li>EC2 classic- Flat platform shared with other customers</li>
 	<li>EC2 VPC - runs all instances in VPC. Some accounts support only EC2 VPC,</li>
</ol>
<ul>
 	<li>Computing Power</li>
 	<li>AWS uses two different units of measure for processing power. Amazon’s own compute unit, the ECU, is its own benchmark measurement designed to give users a consistent and predictable amount of CPU capacity</li>
 	<li>AWS uses different processors for different instance types, two instances with the same number of vCPUs may not necessarily offer the same compute capability.</li>
 	<li>Bursting</li>
 	<li>It also offers bursting capabilities, based on a credit system, where you accrue credits when your vCPUs are idle and consume credits when they’re active.</li>
 	<li><strong>Instance Store or an EBS-Backed Instance?</strong></li>
 	<li>Storage can kept at instance storage or EBS</li>
 	<li>if instance failed / terminated</li>
</ul>
<ol>
 	<li>instance with instance storage can't be recovered</li>
 	<li>instance with EBS instance can be recovered</li>
</ol>
<ol>
 	<li> instance store is both ephemeral and less durable. Amazon EBS is the recommended storage option when you run a database on Amazon EC2. Amazon EBS volumes persist independently from the running life of an Amazon EC2 instance. Once a volume is attached to an instance you can use it like any other physical hard drive.</li>
 	<li>Most EBS-backed instances now offer dedicated bandwidth, known as <strong>EBS Optimization</strong>, which reduces latency between your different EBS volumes.</li>
 	<li>Unlike their instance store counterparts, you can stop and start them to reduce cost whenever your applications aren’t needed.</li>
 	<li>You can resize them dynamically without having to migrate your applications.</li>
 	<li>You can create point-in-time snapshots of both your running instances and your mountable EBS data volumes.And you can also use instance snapshots to create template machine images.</li>
 	<li>They also have built-in redundancy and boot more quickly.</li>
</ol>
<ul>
 	<li>On-demand Vs Spot Vs RI</li>
 	<li>Even though it’s important to be aware of the cost-saving potential of Reserved and Spot Instances, it makes sense to <strong>start with the on-demand model</strong> until you have a better idea of your utilization.</li>
 	<li>Once you’ve <strong>established a clear pattern of your on-demand resource usage</strong> you’ll be able to make informed decisions on the likely RI capacity you’ll need and have a clearer picture of the potential savings.</li>
 	<li><a href="https://aws.amazon.com/answers/account-management/cost-optimization-ec2-right-sizing/">Sizing</a></li>
 	<li style="font-size: 16px;"><img class="wp-image-1351 alignright" src="/wp-content/uploads/2018/03/img_5ab9d4d1660e7.png" alt="" width="315" height="230" /></li>
 	<li>AWS offers the Cost Optimization: EC2 Right Sizing (EC2 Right Sizing) solution, which uses managed services to perform a right-sizing analysis and offer detailed recommendations for more cost-effective instances.</li>
</ul>
<ol>
 	<li>The instance hosts a series of Python scripts that upload utilization data from Amazon CloudWatch to Amazon Redshift for right-sizing analysis.</li>
 	<li>The results are delivered in CSV format to the Amazon S3 bucket, and include instance-by-instance recommendations and related cost savings.</li>
</ol>
<ul>
 	<li><b>How does this solution differ from the AWS Trusted Advisor Cost Optimization check?</b></li>
 	<li>Both the EC2 Right Sizing solution and <a href="https://aws.amazon.com/premiumsupport/trustedadvisor/best-practices/">AWS Trusted Advisor</a> analyze utilization on EC2 instances running any time during the last two weeks. The EC2 Right Sizing solution analyzes all instances with a max CPU utilization lower than 50% and determines a more cost-effective instance type for that workload, if available. In comparison, AWS Trusted Advisor can alert you to low utilization thresholds such as daily CPU utilization of 10% or less and network I/O of 5 MB or less on 4 or more days during the two-week period.</li>
 	<li></li>
 	<li></li>
 	<li><a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html">ECR &amp; ECS</a></li>
 	<li id="EiywyMw"><img class="wp-image-1334 alignnone" src="/wp-content/uploads/2018/03/img_5ab8b00677624.png" alt="" width="514" height="578" /></li>
 	<li id="LXSgkyP"><img class="alignnone wp-image-1333 " src="/wp-content/uploads/2018/03/img_5ab8ad9671a22.png" alt="" width="394" height="180" /><img class="alignnone wp-image-1336 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5ab8b1a1dae28.png" alt="" width="384" height="350" /></li>
 	<li></li>
 	<li id="SFYCWOm"><img class="alignnone size-full wp-image-1337 " src="/wp-content/uploads/2018/03/img_5ab8b289cf75f.png" alt="" /></li>
 	<li>
<p id="tchHPSX"><img class=" wp-image-1338 alignright" src="/wp-content/uploads/2018/03/img_5ab8b35c75b5f.png" alt="" width="232" height="258" /></p>
To prepare your application to run on Amazon ECS, you create a <em>task definition</em>. The task definition is a text file, in JSON format, that describes one or more containers, up to a maximum of ten, that form your application. It can be thought of as a <strong>blueprint for your application.</strong>
<ul>
 	<li>Task definitions specify various parameters for your application. Examples of task definition parameters are <strong>which containers</strong> to use, which <strong>launch type</strong> to use, which <strong>ports should be opened</strong> for your application, and what <strong>data volumes should be used</strong> with the containers in the task.</li>
</ul>
</li>
 	<li>A <em>task</em> is the instantiation of a task definition within a cluster. After you have created a task definition for your application within Amazon ECS, you can specify the number of tasks that will run on your cluster.</li>
 	<li>The Amazon ECS task scheduler is responsible for placing tasks within your cluster.</li>
 	<li>When you run tasks using Amazon ECS, you place them on a <em>cluster</em>, which is a logical grouping of resources.</li>
 	<li>The <em>container agent</em> runs on each infrastructure resource within an Amazon ECS cluster. It sends information about the resource's current running tasks and resource utilization to Amazon ECS, and starts and stops tasks whenever it receives a request from Amazon ECS.</li>
 	<li><a href="https://aws.amazon.com/elasticbeanstalk/faqs/">Beanstalk - PaaS</a></li>
</ul>
<ol>
 	<li>
<p id="NBMRbob"><img class="alignnone wp-image-1297 " src="/wp-content/uploads/2018/03/img_5ab83cf4a3ea8.png" alt="" width="395" height="108" /></p>
Elastic Beanstalk is an AWS PAAS platform. All you have to do is upload your application code, and Elastic Beanstalk takes care of the deployment, load balancing, and capacity provisioning.</li>
 	<li>Elastic Beanstalk automatically handles the deployment details of <strong>capacity provisioning, load balancing, auto-scaling, and application health monitoring</strong>.</li>
 	<li>Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on</li>
 	<li>familiar servers such as Apache, Nginx, Passenger, and IIS.</li>
 	<li>There is no additional charge for Elastic Beanstalk - you pay only for the AWS resources needed to store and run your applications.</li>
 	<li>Easy to begin – Elastic Beanstalk is a quick and simple way to deploy your application to AWS. You simply use the AWS Management Console, <strong>Git deployment, or an integrated development environment (IDE)</strong> such as Eclipse or Visual Studio to upload your application</li>
 	<li>Impossible to outgrow – Elastic Beanstalk <strong>automatically scales your application up and down</strong> based on default Auto Scaling settings
<ol>
 	<li>Select the operating system that matches your application requirements (e.g., Amazon Linux or Windows Server 2012 R2)</li>
 	<li>Choose from several available database and storage options</li>
 	<li>Enable login access to Amazon EC2 instances for immediate and direct troubleshooting</li>
 	<li>Quickly improve application reliability by running in more than one Availability Zone</li>
 	<li>Enhance application security by enabling HTTPS protocol on the load balancer</li>
 	<li>Access built-in Amazon CloudWatch monitoring and getting notifications on application health and other important events</li>
 	<li>Adjust application server settings (e.g., JVM settings) and pass environment variables</li>
 	<li>Run other application components, such as a memory caching service, side-by-side in Amazon EC2</li>
 	<li>Access log files without logging in to the application servers</li>
</ol>
</li>
 	<li>
<p id="iLaQtLF"><img class="alignnone wp-image-986 " src="/wp-content/uploads/2018/03/img_5aab153961666.png" alt="" width="292" height="182" /></p>
</li>
 	<li>https://fortyft.com/posts/elastic-beanstalk-vs-ecs-vs-kubernetes/</li>
 	<li>The Docker platform for Elastic Beanstalk has <a href="https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.html">two generic configurations</a> (single container and multicontainer), and several preconfigured containers.
<ol>
 	<li>Use the single container configuration when you only need to run one container per instance.</li>
 	<li>The other basic configuration, Multicontainer Docker, uses the Amazon Elastic Container Service to coordinate a deployment of<strong> multiple Docker containers to an Amazon ECS cluster in an Elastic Beanstalk environment.</strong> The instances in the environment each run the same set of containers, which are defined in a <code class="code">Dockerrun.aws.json</code> file. Use the multicontainer configuration when you need to deploy <strong>multiple Docker containers to each instance.</strong></li>
</ol>
</li>
 	<li><a href="https://cloudacademy.com/blog/amazon-ec2-container-service-docker-aws/">and ECS</a></li>
 	<li><a href="https://stackoverflow.com/questions/25832554/amazon-elastic-beanstalk-vs-ec2-instance-with-docker-containers">AWS has integrated Elastic Beanstalk (EB) with the EC2 Container Service (ECS)</a> to support <a href="http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html">multi-container Docker environments</a>. An EB environment composed of multiple instances in an autoscaling group can run multiple containers per instance, managed through the ECS agent and its API. Use <code>.ebextensions</code> to map multiple ELB listeners to the containers running on EC2 instances.</li>
</ol>
<ol>
 	<li>AWS Lambda - serverless
<ol>
 	<li>consider weekends have no traffic still infra is charged 2 out of 7 days of charges wasted</li>
 	<li>run code without provisioning or managing servers.  you only pay for execution time.</li>
 	<li>whenever a hit to the service endpoint executes the piece of code. Example whenever there is an upload in S3 runs a lambda function to execute java code.
<p id="HSTSXXT"><img class="alignnone wp-image-987 " src="/wp-content/uploads/2018/03/img_5aab15c7bf2cf.png" alt="" width="436" height="122" /></p>
</li>
</ol>
</li>
 	<li>Amazon ECS
<ol>
 	<li>EC2 container management service
<ol>
 	<li>container - software based. kernels of base OS will be used</li>
 	<li>in microservices architectures multiple containers will be used in a single physical server</li>
</ol>
</li>
 	<li>supports docker containers</li>
 	<li>deployment of VM containers to the EC2 instances.</li>
 	<li>fail over provision in case of failures</li>
 	<li>
<p id="EYDjGGR"><img class="alignnone wp-image-985 " src="/wp-content/uploads/2018/03/img_5aab1439eb8b8.png" alt="" width="423" height="169" /></p>
</li>
</ol>
</li>
 	<li>Elastic Load Balancing is a networking service that automatically spreads out incoming application traffic across several available EC2 instances.</li>
 	<li>Amazon Lightsail is a new service that allows you to quickly and easily create your own Virtual Private Server, or VPS, for as little as $5 per month.
<ol>
 	<li>Vm, Storage, data transfer, load balancer, route 53 for dns all are charged</li>
 	<li>in lightsail everything put in a bundle and charged</li>
</ol>
</li>
 	<li>AWS Batch
<ol>
 	<li>huge quantities batch computing jobs</li>
 	<li>to eliminate third-party commercials or open source batch
processing solutions in aws</li>
 	<li>dynamically provisions the optimal quantity and type of compute (VMs)
required to run your batch jobs</li>
</ol>
</li>
</ol>
<ul>
 	<li><a href="https://www.sumologic.com/aws/"><span id="Elastic_Load_Balancing_Scalable_performance">Elastic Load Balancing: Scalable performance</span></a>
<ul>
 	<li>Amazon includes a powerful, scalable load balancing solution in <a href="https://aws.amazon.com/elasticloadbalancing/" target="_blank" rel="noopener">AWS Elastic Load Balancer (ELB)</a>.</li>
 	<li>elastic - multiple nodes of load balancers are used by aws to make it highly available</li>
 	<li>ELB ensures that client requests are sent to the appropriate servers and avoiding any server hotspots (over-utilizing one server and under utilizing others)</li>
 	<li>AWS supports two types of load balancing: classic Load balancing and Application Load Balancing.
<ul>
 	<li><strong>Classic Load Balancing</strong>, which analyzes basic network and application data and <strong>ensure fault tolerance</strong> if one of the EC2 instances running web application happens to fail.</li>
 	<li><strong>Application Load Balancing</strong>, which <strong>looks at content request and routes traffic</strong> to the appropriate container or microservice <strong>based on the Application content information</strong>.</li>
</ul>
</li>
 	<li>In case of ELB service, you pay for by an hour and by the amount of data processed.</li>
</ul>
</li>
 	<li>Automation</li>
 	<li>Cloud formation - Free of cost</li>
 	<li>can ony take the actions allowed the user to perform</li>
 	<li>administrators/developers design manage and update collection of associated AWS resources (eBS, EC2, Auto scaling and elastic ELB)
<ul>
 	<li>creates and providison AWS</li>
 	<li>administrators/developers concentrate on running resources instead of creating</li>
</ul>
</li>
 	<li>Automatically configures the resources</li>
 	<li>automatically identifies the dependent resources</li>
 	<li>develop highly scalabel, reliable &amp; lucrative applications without configuring underlying cloud infrastructure</li>
 	<li>simplified infrasturcure management
<ul>
 	<li>not individual</li>
</ul>
</li>
 	<li>replicate the same infra on multiple regions</li>
 	<li>easy control and track changes</li>
 	<li>AWS cloud formation</li>
 	<li>manage templates and stacks</li>
 	<li>
<p id="sjhushJ"><img class="alignnone size-full wp-image-1234 " src="/wp-content/uploads/2018/03/img_5ab306c60c4a4.png" alt="" /></p>
</li>
 	<li>Templates</li>
 	<li>json document
<ul>
 	<li>json editor - text editor</li>
 	<li>designer tool to edit graphically</li>
</ul>
</li>
 	<li>describe
<ul>
 	<li> resources</li>
 	<li>properties</li>
 	<li>runtime parameters</li>
</ul>
</li>
 	<li>text file .txt .json or .template</li>
 	<li>blueprint for resources</li>
 	<li>reuse
<ul>
 	<li>template can have the input parameters which can be given at the time of creating stacks</li>
</ul>
</li>
 	<li>Parts
<ol>
 	<li>version</li>
 	<li>description of template</li>
 	<li>meta data  - extra desciption /info about the templates or individual resources</li>
 	<li>parameters
<ol>
 	<li>values to be passed at runtime</li>
 	<li>passed while creating or updating stack</li>
 	<li>can specify - data type, default value, allowed values(enum), desciption etc</li>
 	<li>Ex Type of environment DEV, QA, PROD</li>
</ol>
</li>
 	<li>mappings
<ol>
 	<li>mappings of keys similar to look up table</li>
 	<li>Ex AWSInstanceType2Arch</li>
</ol>
</li>
 	<li> conditions
<ol>
 	<li>to be fulfilled to take action</li>
 	<li>ex create resources only on test env</li>
</ol>
</li>
 	<li>resources - only mandatory secion
<ol>
 	<li>type of resources (logical id)</li>
 	<li>properties of resource</li>
</ol>
</li>
 	<li>output section
<ol>
 	<li>returned values while observing stack's proerties</li>
 	<li>logical id of resoures</li>
</ol>
</li>
</ol>
</li>
 	<li>Stack</li>
 	<li>array of resources managable as single unit. for example all resources to run web applications (web server, db server etc)</li>
 	<li>handled as a single unit</li>
 	<li>during creation, if any one failed whole stack will be rolled back or deleted</li>
 	<li>during deletion, if any one not deleted, whole stack is retained.</li>
 	<li>Creating resources</li>
</ul>
<ol>
 	<li>Create template (with parameters)
<ol>
 	<li>saved to amazon s3 ticket accessible from the cloudformation</li>
</ol>
</li>
 	<li>Form a stack
<ol>
 	<li>mention the template location
<ol>
 	<li>upload from local machine</li>
 	<li>access from amazon s3</li>
</ol>
</li>
</ol>
</li>
 	<li>configure resources based up on parameters</li>
</ol>
<ul>
 	<li>Updating stack</li>
 	<li>modify/updae the resources</li>
 	<li>make necessary changes to the template</li>
 	<li>resubmit template</li>
 	<li></li>
 	<li>while creating stack</li>
</ul>
<ol>
 	<li>invoke underlying stack to configure resources</li>
</ol>
<ul>
 	<li></li>
 	<li>AWS OpsWorks &amp; Chef</li>
 	<li><img class="wp-image-1341 alignright" src="/wp-content/uploads/2018/03/img_5ab8cc0edfa2f.png" alt="" width="317" height="269" />Chef is a configuration management tool for dealing with machine setup on physical servers, virtual machines and in the cloud. Many companies use Chef software to control and manage their infrastructure including Facebook, Etsy, Cheezburger, and Indiegogo.</li>
 	<li>Chef helps solve this problem by treating infrastructure as code. Rather than manually changing anything, the machine setup is described in a Chef recipe.</li>
 	<li>When your infrastructure scales up into the thousands we need a better way of doing things than manual.</li>
 	<li>Collections of recipes are stored in a cookbook. One cookbook should relate to a single task, but can have a number of different server configurations involved (for example a web application with a database, will have two recipes, one for each part, stored together in a cookbook).</li>
 	<li>There is a Chef server which stores each of these cookbooks and as a new chef client node checks in with the server, recipes are sent to tell the node how to configure itself.</li>
 	<li>The client will then check in every now and again to make sure that no changes have occurred, and nothing needs to change. If it does, then the client deals with it. Patches and updates can be rolled out over your entire infrastructure by changing the recipe. No need to interact with each machine individually.</li>
 	<li>
<h3>why is it awesome?</h3>
</li>
 	<li>
<h3></h3>
<b>Chef Analytics</b> - the ability to visualise everything going on in real time. It will check if something is going wrong and notify you before the problem becomes noticeable to your clients.

&nbsp;</li>
 	<li>The <b>Chef development kit</b> allows you to write and manage your chef infrastructure from any machine and any operating system.</li>
 	<li><b>Chef's Knife</b> allows you to manage the interface between your Chef bookshelf (the repository) and your chef server. The high availability and replication feature allows you to ensure that even if something goes wrong, the chef server is able to adapt and recreate your infrastructure as required, without outside help. ®</li>
</ul>
&nbsp;
<h2>LAB</h2>
<h3>EC2</h3>
<ul>
 	<li id="qlrjkIG"><span style="font-size: 1rem;">instance must have a private ip</span></li>
</ul>
<img class=" wp-image-1434 alignright" src="/wp-content/uploads/2018/04/img_5ac584fa8d7df.png" alt="" width="281" height="232" />
<ul>
 	<li>it have a public ip - optional
<ul>
 	<li>it can be dynamic from aws</li>
 	<li>static - elastic ip</li>
</ul>
</li>
 	<li>instances can be connected
<ul>
 	<li>via private ip or</li>
 	<li>public ip</li>
</ul>
</li>
 	<li>spot instances
<ul>
 	<li>pricing history
<ul>
 	<li>product-linux&amp;unix / windows etc</li>
 	<li>instance type - family</li>
 	<li>Date range - 3 hours, days, 3months etc</li>
</ul>
</li>
</ul>
</li>
 	<li>todo
<ul>
 	<li>create group</li>
</ul>
</li>
</ul>
load balancer demo
<ul>
 	<li>create 2 instances in 2 availability zones</li>
 	<li>EC2 dashboard</li>
 	<li>load balancing -&gt; load balancers Create load balancers</li>
 	<li>types
<ul>
 	<li>
<p id="ZNYmItP"><img class=" wp-image-1440 alignright" src="/wp-content/uploads/2018/04/img_5ac6332d47ecd.png" alt="" width="264" height="176" /></p>
Choose an Application Load Balancer when you need a flexible feature set for your web applications with <strong>HTTP and HTTPS</strong> traffic. Operating at the request level, Application Load Balancers provide <strong>advanced routing, TLS termination</strong> and <strong>visibility features</strong> targeted at application architectures, <strong>including microservices and containers</strong>.
<ul>
 	<li>operates on layer 7 of osi</li>
 	<li>Example in a business application, there will be multiple web sites for checkout, blog, announcements etc.</li>
 	<li>critical web sites will have separate farm and</li>
 	<li>less critical web sites like announcements will have separate farm.</li>
 	<li>application load balancer will route based up on the path ex. site.com/checkout or site.com/blog</li>
</ul>
</li>
 	<li>Choose a Network Load Balancer when you need ultra-high performance and static IP addresses for your application. Operating at the connection level, Network Load Balancers are capable of <strong>handling millions of requests per second</strong> while maintaining <strong>ultra-low latencies</strong>.
<ul>
 	<li>similar to classic layer 4</li>
 	<li>all classic load balancer users are asked to use network load balancer</li>
 	<li>public ip to route request</li>
 	<li>probably classic will be discontinued in future</li>
</ul>
</li>
 	<li>Choose a Classic Load Balancer when you have an existing application running in the EC2-Classic network.
<ul>
 	<li>
<div class="elb-PKF">PREVIOUS GENERATION for HTTP, HTTPS, and TCP</div></li>
</ul>
</li>
</ul>
</li>
 	<li>Step 1 - define load balancer
<ul>
 	<li>name</li>
 	<li>choose vpc (default or custom)</li>
 	<li><a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-internal-load-balancers.html?icmpid=docs_elb_console">internal</a> (connecting web servers and application servers)
<ul>
 	<li>The nodes of an internal load balancer have only private IP addresses. The DNS name of an internal load balancer is publicly resolvable to the private IP addresses of the nodes. Therefore, internal load balancers can only <strong>route requests from clients with access to the VPC for the load balancer</strong>.
<p id="TZCILdV"><img class="alignnone wp-image-1438 " src="/wp-content/uploads/2018/04/img_5ac6183dc7ddf.png" alt="" width="274" height="302" /></p>
</li>
</ul>
</li>
 	<li><a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-internet-facing-load-balancers.html">external</a> (connecting users and web servers/end points)
<ul>
 	<li>The <strong>nodes</strong> of an Internet-facing load balancer<strong> have public IP</strong> addresses. The <strong>DNS name</strong> of an Internet-facing load balancer is <strong>publicly resolvable</strong> to the public IP addresses of the nodes. Therefore, Internet-facing load balancers can<strong> route requests from clients over the Internet</strong>.
<p id="hhyUaRP"><img class="alignnone wp-image-1439 " src="/wp-content/uploads/2018/04/img_5ac618594f066.png" alt="" width="289" height="272" /></p>
</li>
</ul>
</li>
 	<li>enable advanced VPC configuraton
<ul>
 	<li>select subnets for high availability</li>
 	<li>You will need to select a Subnet <strong>for each Availability Zone</strong> where you wish t<strong>raffic to be routed by your load balancer</strong>. If you have instances in only one Availability Zone, please select <strong>at least two Subnets in different Availability Zones</strong> to provide higher availability for your load balancer.</li>
</ul>
</li>
 	<li>map load balancer ports to internal instance ports
<ul>
 	<li>Load balancer protocol and instance protocol must be at the same layer.</li>
 	<li>You may not have duplicate load balancer ports defined. (dont use same port for multiple protocols)</li>
 	<li>If your traffic to the load balancer<strong> needs to be secure, use either the HTTPS or the SSL protocol</strong> for your front-end connection. You</li>
 	<li>http 80</li>
 	<li>https 443</li>
 	<li>TCP 80</li>
 	<li>SSL (Secure TCP) 443</li>
</ul>
</li>
 	<li>Step 2: Assign Security Groups - firewall in front of load balancer
<ul>
 	<li>enable all the ports which are facing / enabled for users</li>
</ul>
</li>
 	<li>Step 3: Configure Security Settings - Select Certificate
<ul>
 	<li>AWS Certificate Manager (ACM) is the preferred tool to provision and store server certificates. If you previously stored a server certificate using IAM, you can deploy it to your load balancer. Learn more about HTTPS listeners and certificate management. Select a Cipher</li>
 	<li>Configure SSL negotiation settings for the HTTPS/SSL listeners of your load balancer. <strong>must select certificate in case HTTPS/SSL listener is selected</strong></li>
 	<li><strong>ACM (AWS Certificate Manager)</strong> makes it easy to provision, manage, deploy, and renew SSL Certificates on the AWS platform. ACM manages certificate renewals for you.</li>
 	<li>You may select one of the Security Policies listed below, or customize your own settings.</li>
 	<li>SSL Protocols
<ul>
 	<li>Protocol-TLSv1</li>
 	<li>Protocol-SSLv3</li>
 	<li>Protocol-TLSv1.1</li>
 	<li>Protocol-TLSv1.2</li>
</ul>
</li>
 	<li>SSL Options</li>
 	<li>Server Order Preference</li>
 	<li>SSL Ciphers
<ul>
 	<li>ECDHE-ECDSA-AES256-SHA</li>
 	<li>AES128-SHA256</li>
 	<li>AES256-GCM-SHA384</li>
 	<li>AES256-SHA256</li>
 	<li>AES256-SHA etc</li>
</ul>
</li>
</ul>
</li>
 	<li>Configure Health Check
<ul>
 	<li>Your load balancer will <strong>automatically</strong> perform health checks on your EC2 instances and <strong>only route traffic to instances that pass the health check</strong>. If an <strong>instance fails</strong> the health check, it is <strong>automatically removed from the load balancer</strong>. Customize the health check to meet your specific needs.</li>
 	<li>Ping Protocol - http / https / tcp / ssl</li>
 	<li>Ping Port  80</li>
 	<li>Ping Path (page path) /index.html</li>
 	<li>Advanced Details
<ul>
 	<li>Response Timeout - Time to wait when receiving a response from the health check (2 sec - 60 sec).</li>
 	<li>Interval -Amount of time between health checks (5 sec - 300 sec).</li>
 	<li>Unhealthy threshold - Number of consecutive health check failures before declaring an EC2 instance unhealthy.</li>
 	<li>Healthy threshold- Number of consecutive health check successes before declaring an EC2 instance healthy.</li>
</ul>
</li>
</ul>
</li>
 	<li>Step 5: Add EC2 Instances
<ul>
 	<li>The table lists all your running <strong>EC2 Instances in a particular VPC.</strong> Check the boxes in the Select column to add those instances to this load balancer. Instances are optional. They can be added later.</li>
 	<li><a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-disable-crosszone-lb.html"><strong>Cross-zone load balancing</strong> </a>distributes traffic evenly across all targets in the Availability Zones enabled for the load balancer. With <em>cross-zone load balancing</em>, each load balancer node for your Classic Load Balancer distributes requests evenly across the registered instances in all enabled Availability Zones. If cross-zone load balancing is <strong>disabled</strong>, each load balancer node distributes requests evenly across the registered <strong>instances in its Availability Zone only</strong>.</li>
 	<li>Cross-zone load balancing reduces the need to maintain equivalent numbers of instances in each enabled Availability Zone, and improves your application's ability to handle the loss of one or more instances. However, we <strong>still recommend that you maintain approximately equivalent numbers of instances in each enabled Availability Zone</strong> for higher fault tolerance.</li>
 	<li><a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/config-conn-drain.html"><strong>Enable Connection Draining</strong></a> The number of seconds to allow existing traffic to continue flowing</li>
 	<li>To ensure that a Classic Load Balancer stops sending requests to instances that are de-registering or unhealthy, while keeping the existing connections  open, use <em>connection draining</em>. This enables the load balancer to complete in-flight requests made to instances that are de-registering or unhealthy.</li>
</ul>
</li>
 	<li>Step 6: Add Tags
<ul>
 	<li>Apply tags to your resources to help organize and identify them. A tag consists of a case-sensitive key-value pair. For example, you could define a tag with key = Name and value = Webserver.</li>
</ul>
</li>
 	<li>Review and create</li>
</ul>
</li>
 	<li>Monitoring
<ul>
 	<li>healthy nodes</li>
 	<li>unhealthy nodes</li>
 	<li>notification can be created in case unhealthy nodes greater than 0</li>
 	<li>to simulate the failure, just rename health checking page.</li>
 	<li>instance status in load balancer become outofservice. normal-inservice</li>
 	<li>traffic routed to healthy node only</li>
 	<li>make the web site normal status</li>
 	<li>traffic routed to all nodes</li>
</ul>
</li>
</ul>
Auto scaling
<ul>
 	<li>You can use Auto Scaling to manage Amazon EC2 capacity automatically, maintain the right number of instances for your application, operate a healthy group of instances, and scale it according to your needs.</li>
 	<li>Provision instances based on a reusable template you define, called a launch configuration.</li>
 	<li>Automated Provisioning
<ul>
 	<li>Keep your Auto Scaling group healthy and balanced, whether you need one instance or 1,000.</li>
</ul>
</li>
 	<li>Adjustable Capacity
<ul>
 	<li>Maintain a fixed group size or adjust dynamically based on Amazon CloudWatch metrics.</li>
</ul>
</li>
 	<li>
<div class="gwt-Label MH">To create an Auto Scaling group, you will first need to choose a template that your Auto Scaling group will use when it launches instances for you, called a launch configuration. Choose a launch configuration or create a new one, and then apply it to your group.</div>
<div class="gwt-Label LH">Later, if you want to use a different template, you can create another launch configuration and apply it to this group, even if you already have instances running in it. Using this method, you can update the software that your group uses when it launches new instances.</div></li>
 	<li>Auto scaling group in EC2 user
<ul>
 	<li>instance launch configuration
<ul>
 	<li>new configuration similar to ec2 instance crateion</li>
 	<li>launch configuration is just an information it will not create instances</li>
 	<li>Choose configuration name
<ul>
 	<li>kernal id</li>
 	<li>ram disk id</li>
 	<li>Amazon EC2 Detailed Monitoring metrics, which are provided at 1 minute frequency, can be enabled for the launch configuration Auto scale launch config.</li>
 	<li>Instances launched from Basic Monitoring metrics, provided at 5 minute frequency.</li>
 	<li>ip address
<ul>
 	<li>Only assign a public IP address to instances launched in the default VPC and subnet. (default)</li>
 	<li>Assign a public IP address to every instance.</li>
 	<li>Do not assign a public IP address to any instances.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>Create auto scaling group
<ul>
 	<li>name the group</li>
 	<li>choose number of instances to start with</li>
 	<li>network - select VPC default / custom</li>
 	<li>select subnet
<ul>
 	<li>provide as much subnets as possible</li>
 	<li>for high availability</li>
</ul>
</li>
 	<li>Advanced details
<ul>
 	<li>check receive traffic from load balancer</li>
 	<li>select load balancer</li>
 	<li>capable of checking health and <strong>capable of terminating them</strong></li>
 	<li>Health check grace period  -The length of time that Auto Scaling waits before checking an instance's health status. The grace period begins when an instance comes into service. If no value is provided a default of 300 seconds will be used. Enter zero for no grace period.</li>
 	<li>Instance Protection - If protect from scale in is set, newly launched instances will be protected from scale in by default. Auto Scaling will not select protected instances for termination during scale in.</li>
 	<li>Service-Linked Role -</li>
</ul>
</li>
 	<li>Scaling config
<ul>
 	<li>minimum instances</li>
 	<li>maximum instances</li>
 	<li>based up on metrics
<ul>
 	<li>cpu utilization</li>
 	<li>you can scale based up on specific time of a day as well</li>
 	<li>Example : 8 AM to 8 PM</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>CPU Stress tool - free - windows tool
<ul>
 	<li>simulate the stress in remote machine</li>
</ul>
</li>
</ul>
</li>
</ul>
&nbsp;
<h3>Lambda</h3>
<ul>
 	<li>serverless - servers are managed by the user</li>
 	<li>for each event instance of code will be used</li>
 	<li>automatically scaled - no auto scaling configuration is required</li>
 	<li>charged for duration of execution in milli seconds</li>
 	<li>Seatle times web site provides option to upload images from devices</li>
 	<li>resize the images</li>
 	<li>normally polling is used to check the image is uploaded or not</li>
 	<li>so ec2 instances 24/7 even there is no uploads
<ul>
 	<li>developer provides application code</li>
 	<li>associate the code with an event</li>
 	<li>specify the infra to execute the code</li>
</ul>
</li>
 	<li>images are uploaded to S3 bucket (can be rds or dynamodb etc)</li>
 	<li>bucket has event to execute the lambda code</li>
 	<li>make use of lambdas as much as possible wherever applicable</li>
</ul>
&nbsp;
<h3>BeanStalk</h3>
<ul>
 	<li>developer productivity - in agile projects, everyday one developer has to provide golden image (daily build) to qa team to be deployed on testing machines for testing purpose. half of the day is wasted for this. to avoid this beanstalk is used</li>
 	<li>Along with the instances specification you specify the code &amp; software to be installed on the instances</li>
 	<li>beanstalk deploy the code to all instances at once. - Paas- Platform as a service</li>
 	<li>complete control - you can even login to the instances using rdp or ssh</li>
</ul>
<img class=" wp-image-1441 alignright" src="/wp-content/uploads/2018/04/img_5ac654f95d977.png" alt="" width="246" height="280" />
<h3>MetaData</h3>
<ul>
 	<li>alternative to CLI</li>
 	<li>to get the meta data, use url <strong>from instance</strong> <strong>only</strong> http://<span style="background-color: #ff9900;">169.254</span>.169.254/latest
<ul>
 	<li>/metadata</li>
 	<li>/user-data</li>
</ul>
</li>
</ul>
&nbsp;

EC2 Best Practices
<ul>
 	<li>Security
<ul>
 	<li>manage access to resources by users, roles, Identity federation</li>
 	<li>implement least permissive rules</li>
 	<li>update and patch OS, driver, softwares</li>
</ul>
</li>
 	<li>Storage
<ul>
 	<li>persistance - instance store, ebs etc</li>
 	<li>backup - snapshots</li>
 	<li>recovery</li>
</ul>
</li>
 	<li>Resource mangement
<ul>
 	<li>metadata</li>
 	<li>view your current limits of region</li>
</ul>
</li>
 	<li>Backup &amp; recovery
<ul>
 	<li>regularly backup ebs snapshots / backup tool of enterprse</li>
 	<li>replicate data and deploy in multiple AZ</li>
 	<li>public ip are dynamic handle the dynamic addressing when your instance restarts</li>
 	<li>fail over plan - cloud infra also fail</li>
</ul>
</li>
 	<li>Costs
<ul>
 	<li>EC2
<ul>
 	<li>- hourly pricing
<ul>
 	<li>linux - minute basis</li>
 	<li>windows - hours basis</li>
</ul>
</li>
 	<li>instance size &amp; OS license</li>
 	<li>pricing model - spot / RI etc</li>
</ul>
</li>
 	<li>EBS
<ul>
 	<li>cost per GB per month</li>
 	<li>Snapshot storage cost on S3 equivalent to S#</li>
</ul>
</li>
 	<li>Data transfer
<ul>
 	<li>IN to EC2 instance from internet -not charged</li>
 	<li>OUT from EC2 to AWS Services - charged</li>
 	<li>OUT from EC2 to Internet - charged</li>
</ul>
</li>
 	<li>ELB
<ul>
 	<li>Cost per hour</li>
 	<li>Cost per GB of data processed by ELB</li>
</ul>
</li>
 	<li>EIP
<ul>
 	<li>charged if you not allocated or instance is not running</li>
</ul>
</li>
</ul>
</li>
</ul>
