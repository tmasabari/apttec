---
layout: post
title: AWS - Databases Analytics
date: 2018-03-26 10:23
author: tmasabari
comments: true
categories: [Analytics, AWS, Databases]
---
<h3>Databases</h3>
<ul>
 	<li>profitable resizable capcity for dbs</li>
 	<li>time consuming tiresome administrative tasks</li>
 	<li>6 vendors
<ol>
 	<li>oracle</li>
 	<li>sql server</li>
 	<li>my sql</li>
 	<li>postgresql</li>
 	<li>maria db</li>
 	<li>amazon aurora</li>
</ol>
</li>
 	<li>reasons -
<ol>
 	<li>easy scaling
<ol>
 	<li>storage memory cpu , or even to new server</li>
 	<li><strong>without downtime</strong></li>
</ol>
</li>
 	<li>service panel
<ol>
 	<li>software pathcing</li>
 	<li>failure detection</li>
 	<li>recovery</li>
 	<li>backups</li>
</ol>
</li>
 	<li>Fast service
<ol>
 	<li>different sizing options- <strong>upto 244 gb 32 Vcpus</strong></li>
 	<li>several storage
<ol>
 	<li>magnetic</li>
 	<li>ssd</li>
</ol>
</li>
</ol>
</li>
 	<li>choose familiar db engine</li>
 	<li>high availability
<ol>
 	<li>synchronously copies data to on reserved instance on another AZ</li>
 	<li>allows taking snapshots and backups whenever you want</li>
</ol>
</li>
 	<li>reliability</li>
 	<li>Tracking performance
<ol>
 	<li>using cloudwatch metrics for free</li>
 	<li>operational metrics
<ol>
 	<li>input output load</li>
 	<li>cpu load</li>
 	<li>memory load</li>
 	<li>storage usage</li>
</ol>
</li>
</ol>
</li>
 	<li>Pay for what you use</li>
 	<li>Security and full control
<ol>
 	<li>who can use what can be used = IAM - for free</li>
 	<li>put your DB in VPC - free of cost</li>
 	<li>restrict access to certain tables and System procedures which needs advanced previleges</li>
</ol>
</li>
</ol>
</li>
 	<li>4 Components
<ol>
 	<li>db instances</li>
 	<li>security groups</li>
 	<li>parmeter groups</li>
 	<li>option groups</li>
</ol>
</li>
 	<li>DB instances
<ul>
 	<li>5 GB to 6 TeraBytes of data</li>
 	<li>control DB engine with parameters</li>
 	<li>based up on the engine version features are available</li>
 	<li>DB instance class - to identify the CPU, storage, network and RAM requirements <strong>db</strong>.t2.micro, <strong>db</strong>.t2.large etc</li>
 	<li>3 types of storages
<ul>
 	<li>General purpose SSD</li>
 	<li>Provisioned IOPS SSD</li>
 	<li>Magnetic disk</li>
</ul>
</li>
 	<li>Multi AZ deployment option to load the DB to multiple AZs
<ul>
 	<li>maintains synchronous replica of data</li>
 	<li>least latency spikes</li>
 	<li>failure recovery</li>
 	<li>redunduncy</li>
 	<li>no io congestion</li>
</ul>
</li>
</ul>
</li>
 	<li><a href="https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html">Security groups</a>
<ul>
 	<li>
<table id="w163aac21c21c13b4" style="width: 645px;">
<tbody>
<tr>
<th style="width: 288.157px;"><b>DB Security Group</b></th>
<th style="width: 332.843px;"><b>VPC Security Group</b></th>
</tr>
<tr>
<td style="width: 288.157px;">Targets to provide restricted access whole account or external to account</td>
<td style="width: 332.843px;">Targets to provide restricted access to the resources with in in a VPC</td>
</tr>
<tr>
<td style="width: 288.157px;">Controls access to DB instances outside a VPC.</td>
<td style="width: 332.843px;">Controls access to DB instances in VPC.</td>
</tr>
<tr>
<td style="width: 288.157px;">Uses Amazon <strong>RDS</strong> API actions or the Amazon<strong> RDS page</strong> of the AWS Management Console to create and manage group and rules.</td>
<td style="width: 332.843px;">Uses Amazon <strong>EC2</strong> API actions or the Amazon <strong>VPC page</strong> of the AWS Management Console to create and manage group and rules.</td>
</tr>
<tr>
<td style="width: 288.157px;">When you add a rule to a group, you don't need to specify port number or protocol.</td>
<td style="width: 332.843px;">When you add a rule to a group, specify the <strong>protocol as TCP</strong>. In addition, specify the same <strong>port number</strong> that you used to create the DB instances (or options) that you plan to add as members to the group.</td>
</tr>
<tr>
<td style="width: 288.157px;">Groups allow access from EC2 security groups in your AWS account or other accounts.</td>
<td style="width: 332.843px;">Groups allow access from other VPC security groups in your VPC only.</td>
</tr>
<tr>
<td style="width: 288.157px;">
<p id="TrLQHDB"></p>
</td>
<td style="width: 332.843px;"><img class="alignnone size-full wp-image-1236 " src="/wp-content/uploads/2018/03/img_5ab349b50f95b.png" alt="" /></td>
</tr>
</tbody>
</table>
</li>
 	<li>uses 3 differnt security groups
<ul>
 	<li class="listitem">A DB security group controls access to EC2-Classic DB instances that are not in a VPC.
<ul>
 	<li>controls the network inbound traffic to DB instances, outbound trafffic is currently prohibited</li>
 	<li></li>
</ul>
</li>
 	<li class="listitem">A VPC security group controls access to DB instances and EC2 instances inside a VPC.</li>
 	<li class="listitem">An EC2 security group controls access to an EC2 instance</li>
</ul>
</li>
</ul>
</li>
 	<li>DB Parameter Group
<ul>
 	<li>configuration of db engine</li>
 	<li>one or more db engies of same type</li>
 	<li>default parameter is applied is not supplied at the time of creation. (so at least 1 should be there)
<ul>
 	<li>default parameters are based up on the db engine and instance class</li>
</ul>
</li>
</ul>
</li>
 	<li>Option groups
<ul>
 	<li>tools provided by db engines</li>
 	<li>applicable only for sql server, oracle, My SQL 6.5</li>
</ul>
</li>
</ul>
