---
layout: post
title: Azure Vs AWS 2018 Mar
date: 2018-03-09 15:48
author: tmasabari
comments: true
categories: [Uncategorized]
---
Todo
<ul>
 	<li>https://docs.microsoft.com/en-us/azure/architecture/aws-professional/index</li>
 	<li>https://docs.microsoft.com/en-us/azure/architecture/aws-professional/services</li>
 	<li>http://www.tomsitpro.com/articles/azure-vs-aws-cloud-comparison,2-870-2.html</li>
 	<li>https://www.upguard.com/articles/aws-vs-azure</li>
 	<li>https://www.sitepoint.com/a-side-by-side-comparison-of-aws-google-cloud-and-azure/</li>
 	<li>http://resource.onlinetech.com/key-differences-between-aws-and-microsoft-azure/</li>
</ul>
Background

Services
<ul>
 	<li>Not all Azure products and services are available in all regions.</li>
 	<li>Unlike AWS' per second billing, Azure on-demand VMs are billed by the minute.</li>
 	<li>Azure has no equivalent to EC2 Spot Instances or Dedicated Hosts.</li>
 	<li>Storages
<ul>
 	<li>Durable data storage for Azure VMs is provided by data disks residing in blob storage. This is similar to how EC2 instances store disk volumes on Elastic Block Store (EBS).</li>
 	<li>Azure temporary storage also provides VMs the same low-latency temporary read-write storage as EC2 Instance Storage (also called ephemeral storage).</li>
 	<li>Higher performance disk IO is supported using Azure premium storage. This is similar to the Provisioned IOPS storage options provided by AWS.</li>
 	<li>[table id=1 /]</li>
</ul>
</li>
 	<li>AWS Lambda
<ul>
 	<li><a href="https://azure.microsoft.com/services/functions/" data-linktype="external">Azure Functions</a> is the primary equivalent of AWS Lambda in providing serverless, on-demand code.</li>
 	<li><a href="https://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/" data-linktype="external">WebJobs</a> - allow you to create scheduled or continuously running background tasks.</li>
 	<li><a href="https://azure.microsoft.com/services/logic-apps/" data-linktype="external">Logic Apps</a> - provides communications, integration, and business rule management services.</li>
</ul>
</li>
 	<li>do not have direct equivalents in AWS
<ul>
 	<li><a href="https://azure.microsoft.com/documentation/articles/batch-technical-overview/" data-linktype="external">Azure Batch</a> - allows you to manage compute-intensive work across a scalable collection of virtual machines.</li>
 	<li><a href="https://azure.microsoft.com/documentation/articles/service-fabric-overview/" data-linktype="external">Service Fabric</a> - platform for developing and hosting scalable <a href="https://azure.microsoft.com/documentation/articles/service-fabric-overview-microservices/" data-linktype="external">microservice</a> solutions.</li>
</ul>
</li>
 	<li></li>
</ul>
Billing

Performance

&nbsp;

References
<ul>
 	<li>https://docs.microsoft.com/en-us/azure/architecture/aws-professional/index</li>
 	<li></li>
</ul>
