---
layout: post
title: Pricing - Free tier - Instances
date: 2018-03-12 10:06
author: tmasabari
comments: true
categories: [AWS]
---
<ul>
 	<li>No, the AWS free tier <strong>does not include Amazon S3 RRS</strong> storage.</li>
 	<li>if you run an Amazon EC2 instance for only a portion of an hour, AWS counts that as an entire hour.</li>
 	<li>if you stop and start an Amazon EC2 instance three times in a single hour, you use up three hours of your monthly allotment.</li>
 	<li><strong>No Spot instances</strong></li>
 	<li>server, alarms, and database</li>
 	<li>AWS CodePipeline, AWS Data Pipeline, and AWS Device Farm</li>
 	<li>When you create an AWS account, you are automatically signed up for the free tier for 12 months. Your free tier eligibility expires at the end of the 12-month period. When your free tier expires, AWS starts charging the regular rates for any AWS services and resources that you are using.</li>
</ul>
<strong>31*24=744</strong> hours per month. So Amazon provide 750 hours per month
<ul>
 	<li>Plan to have one permenent AL 2 instance for rest of the year</li>
 	<li>create multiple windows machines as on when required</li>
 	<li>mumbai spot instances are 0.01$ per hour. request them if required.</li>
 	<li>Keep on RDS machine</li>
</ul>
&nbsp;
<ol>
 	<li><span style="font-size: 1rem;">15 GB of bandwidth out aggregated across all AWS services*</span></li>
 	<li>750 hours of <a href="https://aws.amazon.com/ec2">Amazon EC2</a> Linux or RHEL or SLES t2.micro instance usage (1 GiB of memory and 32-bit and 64-bit platform support) – enough hours to run continuously each month*</li>
 	<li><span style="font-size: 1rem;">750 hours of </span><a style="font-size: 1rem;" href="https://aws.amazon.com/ec2">Amazon EC2</a><span style="font-size: 1rem;"> Microsoft Windows Server† t2.micro instance usage (1 GiB of memory and 32-bit and 64-bit platform support) – enough hours to run continuously each month*</span></li>
 	<li>30 GB of <a href="https://aws.amazon.com/ebs">Amazon Elastic Block Storage</a> in any combination of General Purpose (SSD) or Magnetic, plus 2 million I/Os (with EBS Magnetic) and 1 GB of snapshot storage***</li>
 	<li>750 hours of <a href="https://aws.amazon.com/rds/">Amazon RDS</a> Single-AZ Micro DB Instances, running MySQL, MariaDB, PostgreSQL, Oracle BYOL or SQL Server Express Edition – enough hours to run a DB Instance continuously each month. You also get 20 GB of database storage and 20 GB of backup storage.*</li>
 	<li>
<div class="aws-text-box section">
<div class=" ">

25 GB of Storage, 25 Units of Read Capacity and 25 Units of Write Capacity, enough to handle up to 200M requests per month with <a href="https://aws.amazon.com/dynamodb/">Amazon DynamoDB</a>.**

</div>
</div></li>
 	<li>5 GB of <a href="https://aws.amazon.com/s3">Amazon S3</a> standard storage, 20,000 Get Requests, and 2,000 Put Requests*</li>
 	<li>750 hours of an <a href="https://aws.amazon.com/elasticloadbalancing/">Elastic Load Balancer</a> plus 15 GB data processing*</li>
 	<li>1,000 <a href="https://aws.amazon.com/swf">Amazon SWF</a> workflow executions can be initiated for free. A total of 10,000 activity tasks, signals, timers and markers, and 30,000 workflow-days can also be used for free**</li>
 	<li>750 hours of <a href="https://aws.amazon.com/elasticache/">Amazon ElastiCache</a> Micro Cache Node usage – enough hours to run continuously each month. *</li>
 	<li>100,000 Requests of <a href="https://aws.amazon.com/sqs">Amazon Simple Queue Service</a>**</li>
 	<li>10 <a href="https://aws.amazon.com/cloudwatch">Amazon Cloudwatch</a> metrics, 10 alarms, and 1,000,000 API requests**</li>
 	<li>50 GB Data Transfer Out, 2,000,000 HTTP and HTTPS Requests for <a href="https://aws.amazon.com/cloudfront/">Amazon CloudFront</a>*</li>
 	<li>Amazon QuickSight
1 GB of SPICE capacity 1 user perpetual free tier
10GB of SPICE capacity the first 2 months for free for a total of 4 users</li>
 	<li>AWS Lambda
1 Million free requests per month</li>
</ol>
References
<ul>
 	<li>https://aws.amazon.com/free/faqs/?ft=n</li>
 	<li>https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-limits.html</li>
</ul>
