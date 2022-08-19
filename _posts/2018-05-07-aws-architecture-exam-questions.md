---
layout: post
title: AWS Architecture exam questions
date: 2018-05-07 09:42
author: tmasabari
comments: true
categories: [AWS, Exam Preparation]
---
&nbsp;
<ul>
 	<li>videos on Mency Woo's SA Pro prep playlist. (<a href="https://acloud.guru/course/aws-certified-solutions-architect-professional/discuss/-KEAY5AHdre2DzoI-H99/passed-sa-pro-today" target="_blank" rel="noopener">Here's a link to her post</a>. <a href="https://www.youtube.com/playlist?list=PL_RVC-cMNyYTz8zlxq117O1bfji-knooI" target="_blank" rel="noopener">Here's a direct link to her playlist.</a> I love 2x playback!)</li>
 	<li>I just <em>also</em> got a lot of value out of going through dozens of diverse QwikLabs. As one example, the flexibility of EBS was really locked in for me when a QwikLab had me snapshot and create a second EBS volume to avoid re-downloading a large installer on a second EC2 instance. For those who are interested in doing the same labs I did--or just knowing which they were--<a href="https://qwiklabs.com/public_profiles/29328464-b41a-4419-9669-d9815b90c8f9" target="_blank" rel="noopener">here is a link to my QwikLabs profile</a>.  <a href="https://qwiklabs.com/catalog?cloud=AWS#quests">https://qwiklabs.com/catalog?cloud=AWS#quests</a></li>
 	<li><a href="https://acloud.guru/forums/aws-certified-solutions-architect-associate/top?p=1">https://acloud.guru/forums/aws-certified-solutions-architect-associate/top?p=1</a></li>
 	<li>Free practice test <a href="https://www.simplilearn.com/aws-solutions-architect-exam-free-practice-test">simplilearn </a></li>
</ul>

<hr />

tips

<a href="https://acloud.guru/forums/aws-certified-solutions-architect-professional/discussion/-KOcf6vWIq2mQTP-xmGC/-">https://acloud.guru/forums/aws-certified-solutions-architect-professional/discussion/-KOcf6vWIq2mQTP-xmGC/-</a>
<ul>
 	<li>my exam was mostly about auto-scaling, API/web development, Containers/ECS, Lambda and Cloudfront. I feel that this course covered maybe 20%-30% of what was in the exam.</li>
 	<li>My exam questions required me to understand features and use cases of: VPC peering, cross-account access, DirectConnect, snapshotting EBS RAID arrays, DynamoDB, spot instances, Glacier, AWS/user security responsibilities, etc.</li>
 	<li>My suggested tips for the exam is to understand VPC’s and how each of the services work within the VPC and reading the FAQ’s. Additionally, I found it helpful to take a practice exam before going through the course/labs and once again before reading the FAQ’s. The FAQ’s definitely helps you answer a lot of questions you may have. Thanks to Ryan, the A Cloud Guru team, and Tricia's exam feedback.</li>
 	<li>I had a large number of questions involving EBS and encryption (e.g., what instance types supported encryption, migrating from unencrypted EBS volume =&gt; encrypted EBS volume) http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html</li>
 	<li>I had several questions on EBS - snapshots, encryption, attaching and detaching (and how that relates to snapshot lifecycle), storage of snapshots, etc.</li>
 	<li>Storage services whitepaper</li>
 	<li>Here are my more-traditional exam tips:
<ul>
 	<li>Spot instances are good for cost optimization, even if it seems you might need to fall back to On-Demand instances if you wind up getting kicked off them and the timeline grows tighter. The primary (but still not only) factor seems to be whether you can gracefully handle instances that die on you--which is pretty much how you should always design everything, anyway!</li>
 	<li>The term "use case" is not the same as "function" or "capability". A use case is something that your app/system will need to accomplish, not just behaviour that you will get from that service. In particular, a use case doesn't require that the service be a 100% turnkey solution for that situation, just that the service plays a valuable role in enabling it.</li>
 	<li>There might be extra, unnecessary information in some of the questions (red herrings), so try not to get thrown off by them. Understand what services can and can't do, but don't ignore "obvious"-but-still-correct answers in favour of super-tricky ones.</li>
 	<li>If you don't know what they're trying to ask, in a question, just move on and come back to it later (by using the helpful "mark this question" feature in the exam tool). You could easily spend way more time than you should on a single confusing question if you don't triage and move on.</li>
 	<li>My exam questions required me to understand features and use cases of: VPC peering, cross-account access, DirectConnect, snapshotting EBS RAID arrays, DynamoDB, spot instances, Glacier, AWS/user security responsibilities, etc.</li>
</ul>
</li>
</ul>
pro
<ul>
 	<li>There were several questions where the right architectures should certainly include Cognito, DynamoDB Streams, and Lambda, but the right answers in the exam used custom identity brokers, Data Pipeline, and autoscaled EC2 instances. Also, there were still some response options that involved buying Medium or Light Utilization Reserved Instances.</li>
 	<li>Anyway, here are a few more specific things I remember from my exam:
<ul>
 	<li>Route tables for Direct Connect, including which end(s) should have route propagation set.</li>
 	<li>Specific instructions for bringing on a new DirectConnect connection because the VPN is overloaded. This included more <em>details</em> about BGP than I had expected.</li>
 	<li>One (and only one) question about EMR, regarding how to fix low CPU utilization and thereby reduce costs.</li>
 	<li>Cross account access for several different scenarios--including within a company and with its partners or vendors.</li>
</ul>
</li>
</ul>
Here's a key time-saving and score-boosting tip: Study all the sample questions, then take the practice test and study all of those questions, too. A handful of those questions appeared verbatim on my test, so I got free points <em>and</em> extra time by recognizing them and confirming their answers rather than having to work them out from scratch. This allowed me to spend a couple more minutes on some particularly tough questions.

Actually, I should clarify; you should study:
<ul>
 	<li>Everything from 2014.</li>
</ul>

<hr />

&nbsp;

<a href="https://help.acloud.guru/hc/en-us/articles/115002526813-How-to-correctly-answer-AWS-exam-questions">https://help.acloud.guru/hc/en-us/articles/115002526813-How-to-correctly-answer-AWS-exam-questions </a>

<em>The AWS exams are a challenge. Many students struggle with how to answer AWS questions. They are very well written questions that require you to both understand the questions and know the technical detail of the offered answers to determine which are not valid. There is a method for approaching the questions which I refer to as dissection. The key is to know your material very well so that you can spot the falsehood and mismatches in the offered answers.</em>

<span class="wysiwyg-font-size-large"><u>The Questions:</u></span>

Identify every piece of information or hint in the question.
<ul>
 	<li>If they give you information it is relevant to choosing between options.  This is particularly true of the associate exams.  For the Professional exams some information may be 'less' relevant not not misleading.</li>
 	<li>If they don't give you a piece of information you don't needed it. Don't assume and do not add information that is not there. <em>The only exception is that you can assume that any service will function as advertised</em>.</li>
</ul>
<span class="wysiwyg-font-size-large"><u>The Answers:</u></span>

Read the answers very carefully. Do not assume the answer based on the 1st and last word.
<ul>
 	<li>You must choose an offered answer. You cannot add an answer your would prefer. This sound silly but I have had candidates argue that the question is wrong because it does not offer the answer they want to give. As an engineer you cannot always do the "technically best solution" you must work with what you have. The same here.</li>
 	<li>You cannot assume additional services or configurations if not given. (See note above about default or as designed functions). If the questions is about a VPC and no mention is made of nACLs, then assume that they are there and properly configured. However if the questions describes one nACL you cannot assume a 2nd that suits your purposes better.</li>
 	<li>Look for how the answers self-eliminate. To do this you need to really know your material. Know how things work, not just the names and definitions.  For every component and service be able to quote a dozen or more things about what it does and does not do. Compare similar solutions and research how they are different and when you might use one over another. It is never that one is better than another, they all have their place and you need to understand what each is 'best' and 'worst' for. When you know what an object or service cannot do, then you will be able to spot the nonsense in the offered answers.</li>
</ul>
I suggest that you practice dissecting questions and answers with our practice exams. IGNORE the score and our opinion about what answer is correct. Use each questions as a research opportunity to prove to yourself why each answer is correct or incorrect.

Do the labs over a few times. but focus on why you are doing each step. Mix it up and alter the lab and then figure out how to fix it.

Note:  Accept that you will miss a few questions in the exam because that is how the exam is designed. When you hit a question you cannot make sense of, move on quickly and do well on all the others.  Then come back to puzzle them out (or guess) for the extra points.

&nbsp;

<span class="wysiwyg-font-size-large">Finally</span>

You can do this !

<span style="background-color: #ffcc00;">Don't rush into the exam.</span> There are no bonus for how fast you study. But there are bragging rights for how well you did. We have one candidate who <span style="background-color: #ffcc00;">studied all the courses over an extended period without sitting one exam. Then sat all of them in a few days and score high 90% on all.</span>

<span class="wysiwyg-font-size-medium"><span class="wysiwyg-underline">Take you time</span>. <span class="wysiwyg-underline">Know the material</span>.</span>

<hr />

<a href="https://acloud.guru/forums/aws-certified-solutions-architect-associate/discussion/-KSDNs4nfg5ikp6yBN9l/exam_feedback">https://acloud.guru/forums/aws-certified-solutions-architect-associate/discussion/-KSDNs4nfg5ikp6yBN9l/exam_feedback</a>

&nbsp;

I recently passed my SA Associate exam (thanks Ryan and team!) and wanted to share some topics that I wish I had studied more before taking the exam.

1. Know what instance types can be launched from which types of AMIs, and which instance types require an HVM AMI.

<a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/t2-instances.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/t2-instances.html</a>

<a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html</a>

2. Understand bastion hosts, and which subnet one might live on. Here's a good, brief summary of bastion hosts taken from http://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/ - "Bastion hosts are instances that sit within your public subnet and are typically accessed using SSH or RDP. Once remote connectivity has been established with the bastion host, it then acts as a ‘jump’ server, allowing you to use SSH or RDP to login to other instances (within private subnets) deeper within your network. When properly configured through the use of security groups and Network ACLs, the bastion essentially acts as a bridge to your private instances via the Internet."

<a href="http://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/" target="_blank" rel="noopener">http://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/</a>

3. Know the difference between Directory Service's AD Connector and Simple AD. "Use Simple AD if you need an inexpensive Active Directory–compatible service with the common directory features. AD Connector lets you simply connect your existing on-premises Active Directory to AWS."

<a href="http://docs.aws.amazon.com/directoryservice/latest/admin-guide/what_is.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/directoryservice/latest/admin-guide/what_is.html</a>

4. Know how to enable cross-account access with IAM. "To delegate permission to access a resource, you create an IAM role that has two policies attached. The permissions policy grants the user of the role the needed permissions to carry out the desired tasks on the resource. The trust policy specifies which trusted accounts are allowed to grant its users permissions to assume the role. The trust policy on the role in the trusting account is one-half of the permissions. The other half is a permissions policy attached to the user in the trusted account that allows that user to switch to, or assume the role."

<a href="http://docs.aws.amazon.com/IAM/latest/UserGuide/idrolesterms-and-concepts.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/IAM/latest/UserGuide/id<em>roles</em>terms-and-concepts.html</a>

5. Have a good understanding of how Route53 supports all of the different DNS record types, and when you would use certain ones over others.

<a href="http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html</a>

<a href="https://aws.amazon.com/route53/faqs/" target="_blank" rel="noopener">https://aws.amazon.com/route53/faqs/</a>

6. Know which services have native encryption at rest within the region, and which do not.

<a href="http://jayendrapatil.com/aws-storage-gateway/" target="_blank" rel="noopener">http://jayendrapatil.com/aws-storage-gateway/</a>

7. Know which services allow you to retain full admin privileges of the underlying EC2 instances, or conversely know which ones definitely do not. For question 7: http://jayendrapatil.com/aws-root-access-enabled-services/

8. Know When Elastic IPs are free or not. "If you associate additional EIPs with that instance, you will be charged for each additional EIP associated with that instance per hour on a pro rata basis. Additional EIPs are only available in Amazon VPC. To ensure efficient use of Elastic IP addresses, we impose a small hourly charge when these IP addresses are not associated with a running instance or when they are associated with a stopped instance or unattached network interface."

<a href="https://aws.amazon.com/ec2/pricing/" target="_blank" rel="noopener">https://aws.amazon.com/ec2/pricing/</a>

9. Know what four high level categories of information Trusted Advisor supplies.

<a href="https://aws.amazon.com/premiumsupport/trustedadvisor/" target="_blank" rel="noopener">https://aws.amazon.com/premiumsupport/trustedadvisor/</a>

10. Know how to troubleshoot a connection time out error when trying to connect to an instance in your VPC. "You need a security group rule that allows inbound traffic from your public IP address on the proper port, you need a route that sends all traffic destined outside the VPC (0.0.0.0/0) to the Internet gateway for the VPC, the network ACLs must allow inbound and outbound traffic from your public IP address on the proper port," etc.

<a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html#TroubleshootingInstancesConnectionTimeout" target="_blank" rel="noopener">http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html#TroubleshootingInstancesConnectionTimeout</a>

11. Be able to identify multiple possible use cases and eliminate non-use cases for SWF.

<a href="https://aws.amazon.com/swf/faqs/" target="_blank" rel="noopener">https://aws.amazon.com/swf/faqs/</a>

12. Understand how you might set up consolidated billing and cross-account access such that individual divisions' resources are isolated from each other, but corporate IT can oversee all of it.

<a href="http://jayendrapatil.com/aws-consolidated-billing/" target="_blank" rel="noopener">http://jayendrapatil.com/aws-consolidated-billing/</a>

13. Know how you would go about making changes to an Auto Scaling group, fully understanding what you can and can't change. "You can only specify one launch configuration for an Auto Scaling group at a time, and you can't modify a launch configuration after you've created it. Therefore, if you want to change the launch configuration for your Auto Scaling group, you must create a launch configuration and then update your Auto Scaling group with the new launch configuration. When you change the launch configuration for your Auto Scaling group, any new instances are launched using the new configuration parameters, but existing instances are not affected."

<a href="http://docs.aws.amazon.com/autoscaling/latest/userguide/LaunchConfiguration.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/autoscaling/latest/userguide/LaunchConfiguration.html</a>

14. Know which field you use to run a script upon launching your instance.

<a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html#user-data-shell-scripts" target="_blank" rel="noopener">http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html#user-data-shell-scripts</a>

15. Know how DynamoDB (durable, and you can pay for strong consistency), Elasticache (great for speed, not so durable), and S3 (eventual consistency results in lower latency) compare to each other in terms of durability and low latency.

<a href="https://d0.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf" target="_blank" rel="noopener">https://d0.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf</a>

16. Know the difference between bucket policies, IAM policies, and ACLs for use with S3, and examples of when you would use each. "With IAM policies, companies can grant IAM users fine-grained control to their Amazon S3 bucket or objects while also retaining full control over everything the users do. With bucket policies, companies can define rules which apply broadly across all requests to their Amazon S3 resources, such as granting write privileges to a subset of Amazon S3 resources. Customers can also restrict access based on an aspect of the request, such as HTTP referrer and IP address. With ACLs, customers can grant specific permissions (i.e. READ, WRITE, FULL_CONTROL) to specific users for an individual bucket or object."

<a href="https://aws.amazon.com/s3/faqs/" target="_blank" rel="noopener">https://aws.amazon.com/s3/faqs/</a>

17. Know when and how you can encrypt snapshots. "Public snapshots of encrypted volumes are not supported, but you can share an encrypted snapshot with specific accounts."

<a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html" target="_blank" rel="noopener">http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html</a>

18. Understand how you can use ELB cross-zone load balancing to ensure even distribution of traffic to EC2 instances in multiple AZs registered with a load balancer.

<a href="http://jayendrapatil.com/tag/elastic-load-balancer/" target="_blank" rel="noopener">http://jayendrapatil.com/tag/elastic-load-balancer/</a>

<a href="http://jayendrapatil.com/tag/fault-tolearance/">http://jayendrapatil.com/tag/fault-tolearance/</a>

<hr />

<div class="thread-comments-item text-xs animate-show" aria-hidden="false"></div>
<div class="thread-comments-item text-xs animate-show" aria-hidden="false">
<ul>
 	<li><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html">https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html</a></li>
 	<li>/32 subnet is valid - it just points to a single host IP address- generally yes but in AWS there are 5 IPs reserved in any subnet by default so you can not create a subnet less then /28 https://aws.amazon.com/vpc/faqs/ Q. Is there a limit on how large or small a subnet can be? The minimum size of a subnet is a /28 (or 14 IP addresses.) for IPv4. Subnets cannot be larger than the VPC in which they are created. For IPv6, the subnet size is fixed to be a /64. Only one IPv6 CIDR block can be allocated to a subnet.</li>
 	<li>When you create a VPC, you must specify an IPv4 CIDR block for the VPC. <span style="background-color: #ffcc00;">The allowed block size is between a <code class="code">/16</code>netmask (65,536 IP addresses) and <code class="code">/28</code> netmask (16 IP addresses).</span></li>
</ul>
</div>
There are many tools available to help you calculate subnet CIDR blocks; for example, see <a href="http://www.subnet-calculator.com/cidr.php" target="_blank" rel="noopener">http://www.subnet-calculator.com/cidr.php</a>. Also, your network engineering group can help you determine the CIDR blocks to specify for your subnets.

The first four IP addresses and the last IP address in each subnet CIDR block are not available for you to use, and cannot be assigned to an instance. For example, in a subnet with CIDR block <code class="code">10.0.0.0/24</code>, the following five IP addresses are reserved:
<div class="itemizedlist">
<ul class="itemizedlist" type="disc">
 	<li class="listitem"><code class="code">10.0.0.0</code>: Network address.</li>
 	<li class="listitem"><code class="code">10.0.0.1</code>: Reserved by AWS for the VPC router.</li>
 	<li class="listitem"><code class="code">10.0.0.2</code>: Reserved by AWS. The IP address of the DNS server is always the base of the VPC network range plus two; however, we also reserve the base of each subnet range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR. For more information, see <a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS">Amazon DNS Server</a>.</li>
 	<li class="listitem"><code class="code">10.0.0.3</code>: Reserved by AWS for future use.</li>
 	<li class="listitem"><code class="code">10.0.0.255</code>: Network broadcast address. We do not support broadcast in a VPC, therefore we reserve this address.</li>
</ul>
</div>

<hr />

<div class="thread-comments-item text-xs animate-show" aria-hidden="false">
<div></div>
</div>
Read replica VS Multi Az deployment <a href="http://jayendrapatil.com/aws-rds-replication-multi-az-read-replica/">http://jayendrapatil.com/aws-rds-replication-multi-az-read-replica/</a>
<ul>
 	<li><strong>Multi-AZ is a High Availability feature is not a scaling solution for read-only scenarios; standby replica can’t be used to serve read traffic. To service read-only traffic, use a Read Replica.</strong></li>
 	<li><strong>Multi-AZ deployments for Oracle, PostgreSQL, MySQL, and MariaDB DB instances use Amazon technology, while SQL Server DB instances use SQL Server Mirroring.</strong></li>
</ul>
&nbsp;

<hr />

<a href="https://en.wikipedia.org/wiki/Block_contention"><u>https://en.wikipedia.org/wiki/Block_contention</u></a>

<a href="https://en.wikipedia.org/wiki/Reverse_index"><u>https://en.wikipedia.org/wiki/Reverse_index</u></a>

<a href="https://acloud.guru/forums/aws-certified-solutions-architect-associate/discussion/-KLEFR58RnNTW-Nd7znZ/is-the-final-exam-for-this-course-for-associate-or-professional-exam"><u>https://acloud.guru/forums/aws-certified-solutions-architect-associate/discussion/-KLEFR58RnNTW-Nd7znZ/is-the-final-exam-for-this-course-for-associate-or-professional-exam</u></a>

Sharding is like data-partitioning. If the same data (about the celeb in this context) is going to be read, the single sub-set would be hammered. So that sounds pointless.

Multi-AZ is for fail-over, not scaling.

Not to say that CDN is a bad idea at all for static content. But the question looks to be more in the context of <strong><b>DB read contention</b></strong> where caching sounds more suitable to me at least.

<hr />

<a href="http://jayendrapatil.com/tag/elastic-load-balancer/">http://jayendrapatil.com/tag/elastic-load-balancer/</a>

<a href="http://jayendrapatil.com/tag/fault-tolearance/">http://jayendrapatil.com/tag/fault-tolearance/</a>

<a href="http://jayendrapatil.com/aws-rds-replication-multi-az-read-replica/">http://jayendrapatil.com/aws-rds-replication-multi-az-read-replica/</a>

<a href="http://jayendrapatil.com/aws-elastic-transcoder/">http://jayendrapatil.com/aws-elastic-transcoder/</a>

<a href="http://jayendrapatil.com/aws-elastic-transcoder/"><span style="font-weight: 400;">http://jayendrapatil.com/aws-elastic-transcoder/</span></a> <a href="https://acloud.guru/forums/aws-certified-solutions-architect-professional/discussion/-KXAqspylf73XCYOjlki/video-transcoding"><span style="font-weight: 400;">https://acloud.guru/forums/aws-certified-solutions-architect-professional/discussion/-KXAqspylf73XCYOjlki/video-transcoding</span></a>

&nbsp;
