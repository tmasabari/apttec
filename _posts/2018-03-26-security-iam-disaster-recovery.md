---
layout: post
title: Security, IAM & Disaster recovery
date: 2018-03-26 10:03
author: tmasabari
comments: true
categories: [AWS, Disaster recovery, Security]
---
<h2>Security</h2>
<ul>
 	<li>visibility</li>
 	<li>Auditability</li>
 	<li>Manageability</li>
 	<li>Alertness</li>
 	<li>Publish implemented security through different mediums - to gain the trust
<ul>
 	<li>papers</li>
 	<li>reports</li>
 	<li>certifications</li>
 	<li>Third party attestations</li>
</ul>
</li>
 	<li>Security benefits
<ul>
 	<li>security manager
<ul>
 	<li>review and verify components on daily basis</li>
 	<li>highly automated
<ul>
 	<li>employ less time on routine tasks</li>
 	<li>focus on security measures to increase security</li>
</ul>
</li>
 	<li>Free access to documents
<ul>
 	<li>products &amp; Servies</li>
 	<li>to solve ongoing issues</li>
</ul>
</li>
</ul>
</li>
 	<li>Trusted advisor
<ul>
 	<li>online tool - examine customer's environment</li>
 	<li>identify security gaps and fill them</li>
</ul>
</li>
 	<li>Technical Account Manager (TAM)
<ul>
 	<li>single point of contact to the technical queries</li>
</ul>
</li>
</ul>
</li>
 	<li>security tools
<ul>
 	<li>infrastructure security
<ul>
 	<li>data encryption</li>
 	<li>network firewalls</li>
</ul>
</li>
 	<li>Amazon inspector
<ul>
 	<li>evaluating applications for weaknesses or deviations</li>
</ul>
</li>
 	<li>account permissions
<ul>
 	<li>hardware based authenticators</li>
 	<li>IAM</li>
 	<li>multi factor authentication</li>
</ul>
</li>
 	<li>Monitoring and maintaining logs of access and changes in the AWS environment</li>
</ul>
</li>
 	<li>Compliance
<ul>
 	<li>cater to different industries, each have their own compliance and audit standards</li>
 	<li>share the compliance responsibilities</li>
 	<li><span style="background-color: #ff0000;">Key compliance programs</span></li>
</ul>
</li>
 	<li>most common question - Data security
<ul>
 	<li>shared responsibility model</li>
 	<li>AWS Security of the cloud, Customers - Security in the cloud
<p id="fDBAtJs"><img class="wp-image-1281 alignleft" src="/wp-content/uploads/2018/03/img_5ab5c83a056cb.png" alt="" width="285" height="70" /><img class="alignnone wp-image-1282 " src="/wp-content/uploads/2018/03/img_5ab5c84c63a32.png" alt="" width="305" height="63" /></p>
</li>
 	<li>AWS
<ul>
 	<li>operates / manages / controls - physical infra/data centers, host OS, Virtualization lab</li>
</ul>
</li>
 	<li>Customers
<ul>
 	<li>use data protection services - deploy, configure and maintain security</li>
</ul>
</li>
</ul>
</li>
 	<li>Monitoring tools
<ul>
 	<li>usage of network server</li>
 	<li>port scanning activities</li>
 	<li>applications</li>
 	<li> unauthorized intrusion
<ul>
 	<li>DOS attacks</li>
 	<li>Flooding</li>
 	<li>Software or Logic attacks</li>
</ul>
</li>
</ul>
</li>
 	<li>Compliance tools
<ul>
 	<li>encrypted transmission over HTTPS
<ul>
 	<li>uses SSL and secured API end points (customer end points)</li>
</ul>
</li>
 	<li>Access to AWS API
<ul>
 	<li>users &amp; software with cryptographic keys can only access</li>
</ul>
</li>
 	<li>IAM tool
<ul>
 	<li>individual user accounts</li>
</ul>
</li>
 	<li>MFA - hardware toke / software app</li>
 	<li>Services offer data encryption of objects and files
<ul>
 	<li>S3, Glacier, RedShift, Oracle RDS etc</li>
</ul>
</li>
 	<li>security groups - built in firewalls
<ul>
 	<li>access to EC2 instances</li>
</ul>
</li>
 	<li>VPC
<ul>
 	<li>logically isolate a section of AWS cloud</li>
 	<li>network security layer over the data instances</li>
 	<li>virtual network settings
<ul>
 	<li>ip address range</li>
 	<li>creating subnets - public / private</li>
 	<li>configure routing tables</li>
 	<li>configure network gateways</li>
 	<li>virtual private gateways</li>
</ul>
</li>
 	<li>IPsec VPN tunnel
<ul>
 	<li>to connect home network to VPC</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
Security and Identity - summary
<ul>
 	<li>IAM
<ul>
 	<li>create users
<ul>
 	<li>persons - used id and password for each user</li>
 	<li>Client applications - access key and secret key</li>
</ul>
</li>
 	<li>groups - collections of users</li>
 	<li>policy - permissions</li>
 	<li>roles - service accounts</li>
</ul>
</li>
 	<li>Amazon inspector
<ul>
 	<li>vulnerabilitys of applications inside the aws</li>
 	<li>install agent on VM, perform typical checks on the vm</li>
 	<li>Trusted advisor doesnot check the internals of VM, it checks settings from outside of the resources</li>
</ul>
</li>
 	<li>CloudHSM - Hardware Security Module
<ul>
 	<li>data security - corporate, contractural and regulatory compliance</li>
 	<li>data can be saved in encrypted format
<ul>
 	<li>software management
<ul>
 	<li>you can let aws manage the keys or</li>
 	<li>you can store the keys in key management service (KMS)</li>
</ul>
</li>
 	<li>many software requires the hardware module for data encryption
<ul>
 	<li>dedicated hardware policy module will be provided</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>Directory Service
<ul>
 	<li>MSAD- if you have windows VMS</li>
 	<li>hosted active directory services with in aws</li>
 	<li>AD in your on premiese environment
<ul>
 	<li>connect with MSAD service</li>
</ul>
</li>
</ul>
</li>
 	<li>KMS
<ul>
 	<li>aws own internal keys or manage volumes, data</li>
 	<li>or your kms to manage the keys</li>
</ul>
</li>
 	<li>WAF - Web Application Firewall
<ul>
 	<li>more security to web sites</li>
 	<li>create rules for -  ip address range, sql injection etc which is not possible security group / ACL - which allow/disallow certain ports / inboud outbound rules</li>
 	<li>blocks bad requests</li>
</ul>
</li>
 	<li>Shield
<ul>
 	<li>similar to WAF - firewall</li>
 	<li>only covers distributed DOS shielding</li>
 	<li>standard
<ul>
 	<li>comes free with you</li>
</ul>
</li>
 	<li>advanced
<ul>
 	<li>included WAF - free</li>
</ul>
</li>
</ul>
</li>
 	<li>Certificate Manager
<ul>
 	<li>buy, renew existing certiicates etc</li>
</ul>
</li>
 	<li>Artifact
<ul>
 	<li>on demand access to AWS security and compliance documents known as audit artificats</li>
</ul>
</li>
</ul>
load balancer and cloud front provides 95 % coverage

australia has rule that data must be stored with in australia. as per aws, data stored in region never transferred to other regions

&nbsp;
<h3>AWS IAM - free to use</h3>
<ol>
 	<li>allow other to use without sharing password</li>
 	<li>granular permissions - different permissions to users to different resources</li>
 	<li>it uses <strong>least privileged model</strong> to <strong>aggregate permissions</strong> and <strong>maintains a deny bias</strong></li>
 	<li>all applications in AWS to secure access resources (similar to service accounts)</li>
 	<li>multi factor authentication - MFA for users or account. should submit temp codes delivered to devices</li>
 	<li>identity federation
<ol>
 	<li>temp access to organiational accounts or internet accounts</li>
</ol>
</li>
 	<li>obtain logs of access resources</li>
 	<li>PCIDSSA credit card data standard - storiing transmitting and processing</li>
 	<li>IAM intergatoin to all AWS services</li>
</ol>
&nbsp;

&nbsp;

IAM
<ul>
 	<li>By creating IAM users, can we give specific permissions / fine grain control to various services</li>
 	<li>one account has only one root user. root user<span style="background-color: #ffcc00;"> email id and password.</span> other users have <span style="background-color: #ffcc99;">user id and password</span></li>
 	<li>users are common to all regions</li>
 	<li>root credentials should be avoided for normal operations</li>
 	<li>create necessary IAM users - can be people or programs</li>
 	<li>2 types of identity / accesses can be selected
<ul>
 	<li>console id - management console access
<ul>
 	<li>combination of userid and password is known as identity</li>
 	<li>password can be generated or admin entered</li>
 	<li>There is separate account specific url available</li>
 	<li>user can login with the url</li>
 	<li>iam user can enter account id or alias</li>
 	<li>if there is no permissions provided user can only login can't even see existing resources / modify</li>
 	<li>permissions are provided by policies</li>
</ul>
</li>
 	<li>programmatic access
<ul>
 	<li>secret key and access key are automatically generated</li>
 	<li>this can't be used to login to the web console</li>
 	<li>used for applications to access the services
<ul>
 	<li>you can use website, java/.net program with sdk, cli to call appropriate services(s23,ec2 etc) to perform operations</li>
 	<li>cli - sample - using <span style="background-color: #ffcc00;">aws s3 ls</span></li>
 	<li>cli needs to pre configured with access and secret keys</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>granular access - specific type of service , specific resource and specific permissions on the resources</li>
 	<li>identity federation
<ul>
 	<li>ios, AD etc</li>
</ul>
</li>
 	<li>identity information
<ul>
 	<li>log, monitor and track the users</li>
</ul>
</li>
 	<li>MFA
<ul>
 	<li>physical or virtual device like google authenticator for one time code</li>
</ul>
</li>
 	<li>password policies
<ul>
 	<li>one alpha numeric, one numeric, capital etc</li>
</ul>
</li>
 	<li>groups can't be nested</li>
 	<li>Group
<ul>
 	<li>set of users who share common set of permissions</li>
 	<li>Developer group , admin group, operations group etc</li>
</ul>
</li>
 	<li>IAM policy
<ul>
 	<li>json document</li>
 	<li>attached to users, groups and roles</li>
 	<li>2 types built in / user selected</li>
 	<li>pre defined (orange) or custom</li>
 	<li>important pre-defined
<ul>
 	<li>administrator - *.*.* all permissions</li>
 	<li>AmazonEC2FullAccess - full access to the EC2, load balancer, cloud watch, auto scaling</li>
 	<li>AmazonS3ReadOnlyAccess</li>
</ul>
</li>
 	<li>user can use visual editor or json editor</li>
 	<li> <img class="wp-image-1393 alignnone" style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5abe64dfcf51a.png" alt="" width="509" height="183" />
<ul>
 	<li>policies are just json group of statments</li>
 	<li>choose service - S3 etc</li>
 	<li>Effect - Allow / Deny</li>
 	<li>action - changed based on service (S3:ListBucket)
<ul>
 	<li>list read write, permission management</li>
</ul>
</li>
 	<li>Resources
<ul>
 	<li>particulr bucket or all bucket</li>
 	<li>particular object or all object within the bucket etc</li>
</ul>
</li>
 	<li>Request conditions
<ul>
 	<li>is MFA is required</li>
 	<li>is allowed from specific ip address etc</li>
</ul>
</li>
 	<li>name of policy</li>
 	<li>description</li>
 	<li>review the summary and create policy</li>
</ul>
</li>
 	<li>https://docs.aws.amazon.com/general/latest/gr/rande.html provides list of regions and endpoints</li>
 	<li>aws configure
<ul>
 	<li>provide access key, secret key and region from the available list</li>
 	<li>default format is json</li>
</ul>
</li>
 	<li>
<pre class="EnlighterJSRAW" data-enlighter-language="null">aws configure
AWS Access Key ID [****************GWJA]:
AWS Secret Access Key [****************4+6J]:
Default region name [None]: ap-south-1
Default output format [None]:

aws s3 ls
2018-03-28 12:47:26 loggingbucketforproject3
2018-03-28 12:15:54 staticwebsiteproject3</pre>
</li>
 	<li>CLI can be created for different profiles</li>
 	<li>and the above is default profile</li>
</ul>
</li>
 	<li>role
<ul>
 	<li>way of providing permissions to aws resources to access other resources</li>
 	<li>not password protected and dont require access keys</li>
 	<li>role - cross account roles
<ul>
 	<li>can be assigned to other aws user account to grant permissions</li>
</ul>
</li>
 	<li>similar to user but can't be assigned to aws services like ec2 instance</li>
 	<li>system level account - giving permission at the infrastructure level - credentials are not needed</li>
 	<li>normally credentials needs to be stored in config files of application which is visible to people whoever access to code
<ul>
 	<li>in case of credentials change you have to change code/configurations</li>
 	<li>this is avoided using role</li>
</ul>
</li>
 	<li>Create role
<ul>
 	<li>type of service</li>
 	<li>permissions</li>
</ul>
</li>
 	<li>EC2 list - select instance - action - instance settings- attach/replace iam role - &gt; select iam role</li>
 	<li>now ec2 is configured with role</li>
 	<li>the cli and sdk runs within the ec2 doesn't need secret key or access key to perform the operations</li>
 	<li>using redshift command
<ul>
 	<li>by copy command you can copy the files from s3</li>
 	<li>configure redshift with role, so that it can access s3</li>
</ul>
</li>
 	<li>role keys are hidden keeps changing in every 20 minutes. so its abstracted</li>
</ul>
</li>
 	<li>Grant least previlege
<ul>
 	<li>grant only require permissions</li>
 	<li>more secure to stat with min permissions</li>
 	<li>protect assets</li>
 	<li>easier to grant permission than to revoke permission with out side affects</li>
</ul>
</li>
 	<li>Credential report
<ul>
 	<li>all the aws users and their account activities</li>
 	<li>remove all the unnecessary users</li>
</ul>
</li>
</ul>
IAM roles
<ul>
 	<li>identities associated with permission policies similar to users</li>
 	<li>but no credentials are associated with it</li>
 	<li>when you associate role to user, access keys are generated automatically and sent to the users</li>
 	<li>delegate access to applications, servers or users that don't have access to AWS resources
<ul>
 	<li>mobile app to use cloud resources, without embedding credentials in the application</li>
 	<li>access to users in business directory (AD)</li>
 	<li>access to external parties for auditing</li>
</ul>
</li>
</ul>
&nbsp;

reasons
<ul>
 	<li>prevent users from accessing the root account</li>
 	<li>to access aws CLI</li>
 	<li>to use a role</li>
 	<li>or revoke the access of users when they change the organization by simply move them to new group</li>
 	<li>to provide access to different type of users
<ol>
 	<li>IAM users / adminstrators
<ol>
 	<li>individual user, passwords, MFA</li>
 	<li>manage cloud resources</li>
</ol>
</li>
 	<li>Systems
<ol>
 	<li>Programmatic cloud data access</li>
</ol>
</li>
 	<li>IAM roles and permissions</li>
 	<li>Federated users
<ol>
 	<li>Identity users</li>
 	<li>call APIs</li>
</ol>
</li>
 	<li>end users
<ol>
 	<li>access to content such as S3</li>
</ol>
</li>
</ol>
</li>
</ul>
By default users dont have any access
<ul>
 	<li>permit by creating policy</li>
</ul>
policy
<ul>
 	<li>document contains actions to be performed &amp; resources that can be allowed to access</li>
 	<li>any access not mentioned in policy is prohibited</li>
</ul>
Group - set of IAM users
<ul>
 	<li>common permissions assigned to group policy</li>
</ul>
&nbsp;

steps
<ol>
 	<li>1.create single or multiple IAM usres</li>
 	<li>assign credentials</li>
 	<li>assign to one or more groups</li>
 	<li>Permissions</li>
</ol>
