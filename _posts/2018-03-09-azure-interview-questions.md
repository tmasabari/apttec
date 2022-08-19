---
layout: post
title: Azure interview questions
date: 2018-03-09 19:35
author: tmasabari
comments: true
categories: [Azure, Interview Preparation]
---
<a href="https://www.whizlabs.com/blog/azure-solution-architect-interview-questions/"><span lang="EN-US">unified job description:</span><span lang="EN-US"> </span></a>

[table id=6 /]

<a href="https://www.edureka.co/blog/interview-questions/azure-interview-questions/#cloud">Section 1: General Cloud Questions</a>

<a href="https://www.edureka.co/blog/interview-questions/azure-interview-questions/#azure">Section 2: Basic Azure Questions</a>

<a href="https://www.edureka.co/blog/interview-questions/azure-interview-questions/#interview">Section 3: Azure Interview Questions</a>
<h2><strong>Section 1: General Cloud Questions</strong></h2>
<h3><b>1. What is </b><b>Cloud</b><b> Computing?</b></h3>
<strong>Explanation:</strong> It is the use of servers on the internet to “store”, “manage” and “process” data. The difference is, instead of using your own servers, you are using someone else’s servers to do your task, paying them for the amount of time you use it for.
<h3><b>2. What are the different type of services offered in the cloud?</b></h3>
<strong>Explanation:  </strong>The different type of services offered in the cloud are:
<ol>
 	<li>IaaS</li>
 	<li>PaaS</li>
 	<li>SaaS</li>
</ol>
<b>IaaS:</b> In infrastructure as a service, you get the raw hardware from your cloud provider as a service i.e you get a server which you can configure with your own qill.

<b>PaaS: </b>Platform as a Service, gives you a platform to publish without giving the access to the underlying software or OS. For example: Web Apps, Mobile Apps in Azure.

<b>SaaS:</b> You get software as a service in Azure, i.e no infrastructure, no platform, simple software that you can use without purchasing it. For example: when you launch a VM on Azure, you are not buying the OS, you are basically renting it for the time you will be running that instance.
<h3><b>3. What are the different cloud deployment models?</b></h3>
<strong>Explanation:</strong> Following are the three cloud deployment models:

<b>Public Cloud:</b> The infrastructure is owned by your cloud provider and the server that you are using could be a multi-tenant system.

<b>Private Cloud: </b>The infrastructure is owned by you or your cloud provider gives you that service exclusively. For eg: Hosting your website on your servers, or hosting your website with the cloud provider on a dedicated server.

<b>Hybrid Cloud: </b>When you use both Public Cloud, Private Cloud together, it is called Hybrid Cloud. For Example: Using your in-house servers for confidential data, and the public cloud for hosting your company’s public facing website. This type of setup would be a hybrid cloud.
<h3><b>4. I have some private servers on my premises, also I have distributed some of my workload on the public cloud, what is this architecture called?</b></h3>
<ol>
 	<li>Virtual Private Network</li>
 	<li>Private Cloud</li>
 	<li>Virtual Private Cloud</li>
 	<li>Hybrid Cloud</li>
</ol>
<b>Answer: D. Hybrid Cloud</b>
<a name="azure"></a>
<b>Explanation: </b>This type of architecture would be a hybrid cloud. Why? Because we are using both, the public cloud, and on premises servers i.e the private cloud. To make this hybrid architecture easy to use, wouldn’t it be better if your private and public cloud were all on the same network (virtually). This is established by including your public cloud servers in a virtual private cloud, and connecting virtual cloud with your on premise servers using a VPN (Virtual Private Network).

Apart from this Azure Interview Questions Blog, if you want to get trained from professionals on this technology, you can opt for a structured training from edureka! Click below to know more.

&nbsp;
<h2><strong>Section 2: Basic Azure Questions</strong></h2>
<h3><b>5. What is Microsoft Azure and why is it used?</b></h3>
<b>Explanation: </b>As discussed above, the companies which provide the cloud service are called the Cloud Providers. There are a lot of cloud providers out there, out of them one is Microsoft Azure. It is used for accessing Microsoft’s infrastructure for cloud.
<h3><b>6. Which service in Azure is used to manage resources in Azure?</b></h3>
<ol>
 	<li>Application Insights</li>
 	<li>Azure Resource Manager</li>
 	<li>Azure Portal</li>
 	<li>Log Analytics</li>
</ol>
<b>Answer: B Azure Resource Manager</b>

<b>Explanation: </b>Azure Resource Manager is used to “manage” infrastructures which involve a no. of azure services. It can be used to deploy, manage and delete all the resources together using a simple JSON script.
<h3><b>7. Which of the following web applications can be deployed with Azure?</b></h3>
<ol>
 	<li>ASP.NET</li>
 	<li>PHP</li>
 	<li>WCF</li>
 	<li>All of the mentioned</li>
</ol>
<b>Answer: D All of the mentioned</b>
<a name="interview"></a>
<b>Explanation: </b>Microsoft also has released SDKs for both Java and Ruby to allow applications written in those languages to place calls to the Azure Service Platform API to the AppFabric Service.
<h2><strong>Section 3: Azure Interview Questions</strong></h2>
<h3><b>8. What are Roles and why do we use them?</b></h3>
<b>Explanation: </b>Roles are nothing servers in layman terms. These servers are managed, load balanced, Platform as a Service virtual machines that work together to achieve a common goal.

There are 3 types of roles in Microsoft Azure:
<ul>
 	<li>Web Role</li>
 	<li>Worker Role</li>
 	<li>VM  Role</li>
</ul>
Let’s discuss each of these roles in detail:
<ul>
 	<li><b>Web Role –</b> A web role is basically used to deploy a website, using languages supported by the IIS platform like, PHP, .NET etc. It is configured and customized to run web applications.</li>
 	<li><b>Worker Role – </b>A worker role is more like an help to the Web role, it used to execute background processes unlike the Web Role which is used to deploy the website.</li>
 	<li><b>VM Role – </b>The VM role is used by a user to schedule tasks and other windows services. This role can be used to customize the machines on which the web and worker role is running.</li>
</ul>
<h3><b>9. A _________ role is a virtual machine instance running Microsoft IIS Web server that can accept and respond to HTTP or HTTPS requests.</b></h3>
<ol>
 	<li>Web</li>
 	<li>Server</li>
 	<li>Worker</li>
 	<li>Client</li>
</ol>
<b>Answer: A. Web </b>

<b>Explanation: </b>The answer should be Web Roles, there are no roles such as Server or Client roles. Also, Worker roles can only communicate with Azure Storage or through direct connections to clients.

Apart from this Azure Interview Questions Blog, if you want to get trained from professionals on this technology, you can opt for a structured training from edureka! Click below to know more.

&nbsp;
<h3><b>10. Is it possible to create a Virtual Machine using Azure Resource Manager in a Virtual Network that was created using classic deployment?</b></h3>
<b>Explanation: </b>This is not supported. You cannot use Azure Resource Manager to deploy a virtual machine into a virtual network that was created using classic deployment.
<h3><b>11. What are virtual machine scale sets in Azure?</b></h3>
<b>Explanation: </b>Virtual machine scale sets are Azure compute resource that you can use to deploy and manage a set of identical VMs. With all the VMs configured the same, scale sets are designed to support true autoscale, and no pre-provisioning of VMs is required. So it’s easier to build large-scale services that target big compute, big data, and containerized workloads.
<h3><b>12. Are data disks supported within scale sets?</b></h3>
<b>Explanation: </b>Yes. A scale set can define an attached data disk configuration that applies to all VMs in the set. Other options for storing data include:
<ul>
 	<li>Azure files (SMB shared drives)</li>
 	<li>OS drive</li>
 	<li>Temp drive (local, not backed by Azure Storage)</li>
 	<li>Azure data service (for example, Azure tables, Azure blobs)</li>
 	<li>External data service (for example, remote database)</li>
</ul>
<h3><strong>13. What is an Availability Set?</strong></h3>
<strong>Explanation:</strong> An availability set is a logical grouping of VMs that allows Azure to understand how your application is built to provide redundancy and availability. It is recommended that two or more VMs are created within an availability set to provide for a highly available application and to meet the 99.95% Azure SLA. When a single VM is used with Azure Premium Storage, the Azure SLA applies for unplanned maintenance events.
<h3><strong>14. What are Fault Domains?</strong></h3>
<strong>Explanation:</strong> A fault domain is a logical group of underlying hardware that share a common power source and network switch, similar to a rack within an on-premise data-centers. As you create VMs within an availability set, the Azure platform automatically distributes your VMs across these fault domains. This approach limits the impact of potential physical hardware failures, network outages, or power interruptions.
<h3><strong>15. What are Update Domains?</strong></h3>
<strong>Explanation:</strong> An update domain is a logical group of underlying hardware that can undergo maintenance or can be rebooted at the same time. As you create VMs within an availability set, the Azure platform automatically distributes your VMs across these update domains. This approach ensures that at least one instance of your application always remains running as the Azure platform undergoes periodic maintenance. The order of update domains being rebooted may not proceed sequentially during planned maintenance, but only one update domain is rebooted at a time.
<h3><strong>16. What are Network Security Groups?</strong></h3>
<strong>Explanation: </strong>A network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to subnets, NICs, or both. NSGs can be associated with either subnets or individual NICs connected to a subnet. When an NSG is associated with a subnet, the ACL rules apply to all the VMs in that subnet. In addition, traffic to an individual NIC can be restricted by associating an NSG directly to a NIC.
<h3><b>17. Do scale sets work with Azure availability sets?</b></h3>
<b>Explanation: </b>Yes. A scale set is an implicit availability set with 5 fault domains and 5 update domains. Scale sets of more than 100 VMs span multiple <i>placement groups</i>, which are equivalent to multiple availability sets. An availability set of VMs can exist in the same virtual network as a scale set of VMs. A common configuration is to put control node VMs (which often require unique configuration) in an availability set and put data nodes in the scale set.
<h3><b>18. What is a break-fix issue?</b></h3>
<b>Explanation: </b>Technical problems are called break-fix issue, it is an industry term which refers to “work involved in supporting a technology when it fails in the normal course of its function, which requires intervention by a support organization to be restored to working order”.
<h3><b>19. Why is Azure Active Directory used?</b></h3>
<b>Explanation: </b>Azure Active Directory is an Identity and Access Management system. It is used to grant access to your employees to specific products and services in your network. For example: Salesforce.com, twitter etc. Azure AD has some in-built support for applications in its gallery which can be added directly.
<h3><b>20. What happens when you exhaust the maximum failed attempts for authenticating yourself via Azure AD?</b></h3>
<b>Explanation: </b>We use a more sophisticated strategy to lock accounts. This is based on the IP address of the request and the passwords entered. The duration of the lockout also increases based on the likelihood that it is an attack.
<h3><b>21. Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?</b></h3>
<b>Explanation: </b>Azure AD has around 2600 pre-integrated applications. All pre-integrated applications support single sign-on (SSO). SSO let you use your organizational credentials to access your apps. Some of the applications also support automated provisioning and de-provisioning.

&nbsp;
<h3><b>22. How can I use applications with Azure AD that I’m using on-premises?</b></h3>
<b>Explanation: </b>Azure AD gives you an easy and secure way to connect to the web applications you choose. You can access these applications in the same way you access your SaaS apps in Azure AD, no need for a VPN to change your network infrastructure.
<h3><b>23. What is Azure Service Fabric?</b></h3>
<b>Explanation: </b>Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable micro-services. Service Fabric also addresses the significant challenges in developing and managing cloud applications. Developers and administrators can avoid complex infrastructure problems and focus on implementing mission-critical, demanding workloads that are scalable, reliable, and manageable. Service Fabric represents the next-generation middleware platform for building and managing these enterprise-class, tier-1, cloud-scale applications.
<h3><b>24. What is a </b><b>VNet</b><b>?</b></h3>
<b>Explanation: </b>VNet is a representation of your own network in the cloud. It logically isolates your instances launched in the cloud, from the rest of your resources.
<h3><b>25. What are the differences between Subscription Administrator and Directory Administrator?</b></h3>
<b>Explanation: </b>By default, one is assigned the Subscription Administrator role when he/she signs up for Azure. A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with. This role is authorized to manage services in the Azure portal. If others need to sign in and access services by using the same subscription, you can add them as co-admins.

Azure AD has a different set of admin roles to manage the directory and identity-related features. These admins will have access to various features in the Azure portal or the Azure classic portal. The admin’s role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.
<h3><b>26. Are there any scale limitations for customers using managed disks?</b></h3>
<b>Explanation:</b> Managed Disks eliminates the limits associated with storage accounts. However, the number of managed disks per subscription is limited to 2000 by default.
<h3><b>27. What is the difference between Service Bus Queues and Storage Queues?</b></h3>
<b>Explanation: </b>The Azure Storage Queue is simple and the developer experience is quite good. It uses the local Azure Storage Emulator and debugging is made quite easy. The tooling for Azure Storage Queues allows you to easily peek at the top 32 messages and if the messages are in XML or Json, you’re able to visualize their contents directly from Visual Studio Furthermore, these queues can be purged of their contents, which is especially useful during development and QA efforts.

The Azure Service Bus Queues are evolved and surrounded by many useful mechanisms that make it enterprise worthy! They are built into the Service Bus and are able to forward messages to other Queues and Topics. They have a built-in dead-letter queue and messages have a time to live that you control, hence messages don’t automatically disappear after 7 days.

Furthermore, Azure Service Bus Queues have the ability of deleting themselves after a configurable amount of idle time. This feature is very practical when you create Queues for each user, because if a user hasn’t interacted with a Queue for the past month, it automatically gets clean it up. Its also a great way to drive costs down. You shouldn’t have to pay for storage that you don’t need. These Queues are limited to a maximum of 80gb. Once you’ve reached this limit your application will start receiving exceptions.
<h3><b>28. What is Azure </b><b>Redis</b><b> Cache?</b></h3>
<b>Redis</b> is an open source (BSD licensed), in-memory data structure store, used as a database,<b>cache</b> and message broker. Azure Redis Cache is based on the popular open-source Redis cache. It gives you access to a secure, dedicated Redis cache, managed by Microsoft, and accessible from any application within Azure.  It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries.

&nbsp;
<h3><b>29. Why doesn’t Azure </b><b>Redis</b><b> Cache have an MSDN class library reference like some of the other Azure services?</b></h3>
<b>Explanation: </b>Microsoft Azure Redis Cache is based on the popular open source Redis Cache and can be accessed by a wide variety of Redis clients for many programming languages. Each client has its own API that makes calls to the Redis cache instance using Redis commands.

Because each client is different, there is not one centralized class reference on MSDN, and each client maintains its own reference documentation. In addition to the reference documentation, there are several tutorials showing how to get started with Azure Redis Cache using different languages and cache clients. To access these tutorials, see How to use Azure Redis Cache and click the desired language from the language switcher at the top of the article.
<h3><b>30. What are </b><b>Redis</b><b> databases?</b></h3>
<b>Explanation: </b>Redis Databases are just a logical separation of data within the same Redis instance. The cache memory is shared between all the databases and actual memory consumption of a given database depends on the keys/values stored in that database. For example, a C6 cache has 53 GB of memory. You can choose to put all 53 GB into one database or you can split it up between multiple databases.
<h3 id="can-i-add-an-existing-vm-to-an-availability-set"><strong>31. Is it possible to add an existing VM to an availability set?</strong></h3>
<strong>Explanation:</strong> No. If you want your VM to be part of an availability set, you need to create the VM within the set. There currently no way to add a VM to an availability set after it has been created.
<h3 id="what-are-the-username-requirements-when-creating-a-vm"><strong>32. What are the username requirements when creating a VM?</strong></h3>
<strong>Explanation:</strong> Usernames can be a maximum of 20 characters in length and cannot end in a period (“.”).
<p class="lf-text-block lf-block">The following usernames are not allowed:</p>
<b><img class="size-full wp-image-51002 aligncenter" src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User.png" sizes="(max-width: 720px) 100vw, 720px" srcset="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User.png 720w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User-150x76.png 150w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User-300x153.png 300w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User-528x269.png 528w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/User-353x180.png 353w" alt="Prohibited Users - Azure Interview Questions - Edureka" width="720" height="367" /></b>
<h3><strong>33. What are the password requirements when creating a VM?</strong></h3>
<p class="lf-text-block lf-block"><strong>Explanation:</strong> Passwords must be 12 – 123 characters in length and meet 3 out of the following 4 complexity requirements:</p>

<ul class="lf-text-block lf-block">
 	<li>Have lower characters</li>
 	<li>Have upper characters</li>
 	<li>Have a digit</li>
 	<li>Have a special character (Regex match [\W_])</li>
</ul>
<p class="lf-text-block lf-block">The following passwords are not allowed:</p>
<b><img class="size-full wp-image-51004 aligncenter" src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass.png" sizes="(max-width: 726px) 100vw, 726px" srcset="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass.png 726w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass-150x21.png 150w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass-300x43.png 300w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass-528x76.png 528w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/pass-590x85.png 590w" alt="Passwords Permitted - Azure Interview Questions - Edureka" width="726" height="104" /></b>
<h3><strong>34. How much storage can I use with a virtual machine?</strong></h3>
<strong>Explanation: </strong>Each data disk can be up to 1 TB. The number of data disks which you can use depends on the size of the virtual machine.

Azure Managed Disks are the new and recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data. You can use multiple Managed Disks with each Virtual Machine. Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.

Azure storage accounts can also provide storage for the operating system disk and any data disks. Each disk is a .vhd file stored as a page blob.
<h3><strong>35. How can one create a Virtual Machine in Powershell?</strong></h3>
<pre># Define a credential object 
$cred = Get-Credential 
# Create a virtual machine configuration 
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 |
` Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | 
` Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer ` 
-Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id</pre>
<h3><strong>36. How to create a Network Security Group and a Network Security Group Rule?</strong></h3>
<pre># Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP -Protocol Tcp `
 -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
 -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW -Protocol Tcp `
 -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
 -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
 -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb

</pre>
<h3><strong>37. How to create a new storage account and container using Power Shell?</strong></h3>
<pre>$storageName = "st" + (Get-Random)
New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
$accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
$context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
New-AzureStorageContainer -Name "templates" -Context $context -Permission Container</pre>
<h3><strong>38. How can one create a VM in Azure CLI?</strong></h3>
<pre>az vm create ` --resource-group myResourceGroup ` --name myVM --image win2016datacenter ` --admin-username azureuser ` --admin-password myPassword12</pre>
&nbsp;
<h3><strong>39. What are the various power states of a VM?</strong><img class="size-full wp-image-51018 aligncenter" src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States.png" sizes="(max-width: 740px) 100vw, 740px" srcset="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States.png 740w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States-150x101.png 150w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States-300x202.png 300w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States-446x300.png 446w, https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/08/Power-States-267x180.png 267w" alt="Power States - Azure Interview Questions - Edureka" width="740" height="498" /></h3>
<h3><strong>40. How can you retrieve the state of a particular VM?</strong></h3>
<pre>Get-AzureRmVM `
 -ResourceGroupName myResourceGroup `
 -Name myVM `
 -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}</pre>
<h3><strong>41. How can you stop a VM using Power Shell?</strong></h3>
<pre>Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force</pre>
<h3><b>42. Why was my client disconnected from the cache?</b></h3>
<b>Explanation: </b>The following are some common reason for a cache disconnect.
<ul>
 	<li>Client-side causes
<ul>
 	<li>The client application was redeployed.</li>
 	<li>The client application performed a scaling operation.</li>
 	<li>In the case of Cloud Services or Web Apps, this may be due to auto-scaling.</li>
 	<li>The networking layer on the client side changed.</li>
 	<li>Transient errors occurred in the client or in the network nodes between the client and the server.</li>
 	<li>The bandwidth threshold limits were reached.</li>
 	<li>CPU bound operations took too long to complete.</li>
</ul>
</li>
 	<li>Server-side causes
<ul>
 	<li>On the standard cache offering, the Azure Redis Cache service initiated a fail-over from the primary node to the secondary node.</li>
 	<li>Azure was patching the instance where the cache was deployed</li>
 	<li>This can be for Redis server updates or general VM maintenance.</li>
</ul>
</li>
</ul>
<h3><b>43. What is Azure Search?</b></h3>
<b>Explanation: </b>Azure Search is a cloud search-as-a-service solution that delegates server and infrastructure management to Microsoft, leaving you with a ready-to-use service that you can populate with your data and then use to add search to your web or mobile application. Azure Search allows you to easily add a robust search experience to your applications using a simple REST API or .NET SDK without managing search infrastructure or becoming an expert in search.
<h3><b>44. My web app still uses an old Docker container image after I’ve updated the image on Docker Hub. Does Azure support continuous integration/deployment of custom containers?</b></h3>
<b>Explanation: </b>Yes, it does. For private registries, you can update the container by stopping and then re-starting your web app. Alternatively, you can also change or add a dummy application setting to force an update of your container.

&nbsp;
<h3><b>45. What are the expected values for the Startup File section when I configure the runtime stack?</b></h3>
<b>Explanation: </b>For Node.Js, you specify the PM2 configuration file or your script file. For .NET Core, specify your compiled DLL name. For Ruby, you can specify the Ruby script that you want to initialize your app with.
<h3><b>46. How are Azure Marketplace subscriptions priced?</b></h3>
<b>Explanation:</b>

Pricing will vary based on product types. ISV software charges and Azure infrastructure costs are charged separately through your Azure subscription. Pricing models include:

<b>BYOL Model:</b> Bring-your-own-license. You obtain outside of the Azure Marketplace, the right to access or use the offering and are not charged Azure Marketplace fees for use of the offering in the Azure Marketplace.

<b>Free: </b>Free SKU. Customers are not charged Azure Marketplace fees for use of the offering.

<b>Free Software Trial:</b> Full-featured version of the offer that is promotionally free for a limited period of time. You will not be charged Azure Marketplace fees for use of the offering during a trial period. Upon expiration of the trial period, customers will automatically be charged based on standard rates for use of the offering.

<b>Usage-Based: </b>You are charged or billed based on the extent of your use of the offering. For Virtual Machines Images, you are charged an hourly Azure Marketplace fee. For Data Services, Developer services, and APIs, you are charged per unit of measurement as defined by the offering.

<b>Monthly Fee: </b>You are charged or billed a fixed monthly fee for a subscription to the offering (from the date of subscription start for that particular plan). The monthly fee is not prorated for mid-month cancellations or unused services.
<h3><b>47. What is the difference between “price,” “software price,” and “total price” in the cost structure for Virtual Machine offers in the Azure Marketplace?</b></h3>
<b>Explanation: </b>“Price” refers to the cost of the Azure Virtual Machine to run the software. “Software price” refers to the cost of the publisher software running on an Azure Virtual Machine. “Total price” refers to the combined total cost of the Azure Virtual Machine and the publisher software running on an Azure Virtual Machine.
<h3><b>48. What are </b><b>stateful</b><b> and stateless microservices for Service Fabric?</b></h3>
<b>Explanation: </b>Service Fabric enables you to build applications that consist of microservices. Stateless microservices (such as protocol gateways and web proxies) do not maintain a mutable state outside a request and its response from the service. Azure Cloud Services worker roles are an example of a stateless service. Stateful microservices (such as user accounts, databases, devices, shopping carts, and queues) maintain a mutable, authoritative state beyond the request and its response. Today’s Internet-scale applications consist of a combination of stateless and stateful microservices.
<h3><b>49. What is the meaning of application partitions?</b></h3>
<b>Explanation: </b>The application partitions are a part of the Active Directory system and having said so, they are directory partitions which are replicated to domain controllers. Usually, domain controllers that are included in the process of directory partitions hold a replica of that directory partition. The attributes and values of application partitions is that you can replicated them to any specific domain controller in a forest, meaning that it could lessen replication traffic. While the domain directory partitions transfer all their data to all of the domains, the application partitions can focus on only one in the domain area. This makes application partitions redundant and more available.
<h3><strong>50. What are special Azure Regions?</strong></h3>
<strong>Explanation: </strong>Azure has some special regions that you may wish to use when buildingyour applications for compliance or legal purposes. These special regions include:
<ul class="lf-text-block lf-block">
 	<li><strong>US Gov Virginia</strong> and <strong>US Gov Iowa</strong>
<ul>
 	<li>A physical and logical network-isolated instance of Azure for US government agencies and partners, operated by screened US persons. Includes additional compliance certifications such as <a href="https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP">FedRAMP</a> and <a href="https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA">DISA</a>.</li>
</ul>
</li>
 	<li><strong>China East</strong> and <strong>China North</strong>
<ul>
 	<li>These regions are available through a unique partnership between Microsoft and 21Vianet, whereby Microsoft does not directly maintain the datacenters.</li>
</ul>
</li>
 	<li><strong>Germany Central</strong> and <strong>Germany Northeast</strong>
<ul>
 	<li>These regions are available via a data trustee model whereby customer data remains in Germany under control of T-Systems, a Deutsche Telekom company, acting as the German data trustee.</li>
</ul>
</li>
</ul>
&nbsp;

<strong>Q. What is Azure Cloud Service?</strong>
By creating a cloud service, you can deploy a multi-tier web application in Azure, defining multiple roles to distribute processing and allow flexible scaling of your application. A cloud service consists of one or more web roles and/or worker roles, each with its own application files and configuration. Azure Websites and Virtual Machines also enable web applications on Azure. The main advantage of cloud services is the ability to support more complex multi-tier architectures

<strong>Q. What is a cloud service role?</strong>
A cloud service role is comprised of application files and a configuration. A cloud service can have two types of roles.

<strong>Q. What is link a resource?</strong>
To show your cloud service’s dependencies on other resources, such as an Azure SQL Database instance, you can “link” the resource to the cloud service. In the Preview Management Portal, you can view linked resources on the Linked Resources page, view their status on the dashboard, and scale a linked SQL Database instance along with the service roles on the Scale page. Linking a resource in this sense does not connect the resource to the application; you must configure the connections in the application code.

<strong>Q. What is scale a cloud service?</strong>
A cloud service is scaled out by increasing the number of role instances (virtual machines) deployed for a role. A cloud service is scaled in by decreasing role instances. In the Preview Management Portal, you can also scale a linked SQL Database instance, by changing the SQL Database edition and the maximum database size, when you scale your service roles.

<strong>Q. What is a web role?</strong>
A web role provides a dedicated Internet Information Services (IIS) web-server used for hosting front-end web applications.

<strong>Q.What is a worker role?</strong>
Applications hosted within worker roles can run asynchronous, long-running or perpetual tasks independent of user interaction or input.

<strong>Q. What is a role instance?</strong>
A role instance is a virtual machine on which the application code and role configuration run. A role can have multiple instances, defined in the service configuration file.

<strong>Q. What is a guest operating system?</strong>
The guest operating system for a cloud service is the operating system installed on the role instances (virtual machines) on which your application code runs.

<strong>Q. What is a cloud service components?</strong>
Three components are required in order to deploy an application as a cloud service in Azure:

<strong>Q. What is deployment environments?</strong>
Azure offers two deployment environments for cloud services: a staging environment in which you can test your deployment before you promote it to the production environment. The two environments are distinguished only by the virtual IP addresses (VIPs) by which the cloud service is accessed. In the staging environment, the cloud service’s globally unique identifier (GUID) identifies it in URLs (GUID.cloudapp.net). In the production environment, the URL is based on the friendlier DNS prefix assigned to the cloud service (for example, myservice.cloudapp.net).

<strong>Related Page: <a href="https://mindmajix.com/azure-automation">Azure Automation - Benefits And Special Features</a></strong>

<strong>Q. What is swap deployments?</strong>
To promote a deployment in the Azure staging environment to the production environment, you can “swap” the deployments by switching the VIPs by which the two deployments are accessed. After the deployment, the DNS name for the cloud service points to the deployment that had been in the staging environment.

<strong>Q. What is minimal vs. verbose monitoring?</strong>
Minimal monitoring, which is configured by default for a cloud service, uses performance counters gathered from the host operating systems for role instances (virtual machines). Verbose monitoring gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing. For more information

<strong>Q. What is a service definition file?</strong>
The cloud service definition file (.csdef) defines the service model, including the number of roles.

<strong>Q. What is a service configuration file?</strong>
The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.

<strong>Q. What is a service package?</strong>
The service package (.cspkg) contains the application code and the service definition file.

<strong>Q. What is a cloud service deployment?</strong>
A cloud service deployment is an instance of a cloud service deployed to the Azure staging or production environment. You can maintain deployments in both staging and production.

<strong>Q. What is Azure Diagnostics?</strong>
Azure Diagnostics is the API that enables you to collect diagnostic data from applications running in Azure. Azure Diagnostics must be enabled for cloud service roles in order for verbose monitoring to be turned on.

<strong>Q. What is Azure Service Level Agreement (SLA)?</strong>
The Azure Compute SLA guarantees that, when you deploy two or more role instances for every role, access to your cloud service will be maintained at least 99.95 percent of the time. Also, detection and corrective action will be initiated 99.9 percent of the time when a role instance’s process is not running.

<strong>Q. What is Cloud Computing?</strong>
Cloud computing is the use of computing resources (hardware and software) that are delivered
as a service over a network (typically the Internet).

<strong>Q. What are the Service Model in Cloud Computing?</strong>
Cloud computing providers offer their services according to three fundamental models: Infrastructure as a service (IaaS), platform as a service (PaaS), and software as a service (SaaS) where IaaS is the most basic and each higher model abstracts from the details of the lower models.
Examples of IaaS include: Amazon CloudFormation (and underlying services such as Amazon EC2), Rackspace Cloud, Terremark, Windows Azure Virtual Machines, Google Compute Engine. and Joyent.
Examples of PaaS include: Amazon Elastic Beanstalk, Cloud Foundry, Heroku, Force.com, EngineYard, Mendix, Google App Engine, Windows Azure Compute and OrangeScape.
Examples of SaaS include: Google Apps, Microsoft Office 365, and Onlive. Source from : HTTP://EN.WIKIPEDIA.ORG/WIKI/CLOUD_COMPUTING

<strong>Q. How many types of deployment models are used in cloud?</strong>
There are 4 types of deployment models used in cloud:
1. Public cloud
2. Private cloud
3. Community cloud
4. Hybrid cloud

&nbsp;

<strong>Q. What is Windows Azure Platform?</strong>
A collective name of Microsoft’s Platform as a Service (PaaS) offering which provides a programming platform, a deployment vehicle, and a runtime environment of cloud computing hosted in Microsoft datacenters.

<strong>Q. What are the roles available in Windows Azure?</strong>
All three roles (web, worker, VM) are essentially Windows Server 2008. Web and Worker roles are nearly identical: With Web and Worker roles, the OS and related patches are taken care for you; you build your app’s components without having to manage a VM

<strong>Q. What is difference between Windows Azure Platform and Windows Azure?</strong>
The former is Microsoft’s PaaS offering including Windows Azure, SQL Azure, and Appfabric; while the latter is part of the offering and the Microsoft’s cloud OS.

<strong>Q. What are the three main components of Windows Azure Platform?</strong>
1. Compute
2. Storage
3. AppFabric

<strong>Q. What is Windows Azure compute emulator?</strong>
The compute emulator is a local emulator of Windows Azure that you can use to build and test your application before deploying it to Windows Azure.

<strong>Q. What is fabric?</strong>
In the Windows Azure cloud fabric is nothing but a combination of many virtualized instances which run client application

<strong>Q. How many instances of a Role should be deployed to satisfy Azure SLA (service level agreement) ? And what’s the benefit of Azure SLA?</strong>
TWO. And if we do so, the role would have external connectivity at least 99.95% of the time.

<strong>Q. What are the options to manage session state in Windows Azure?     </strong>
Windows Azure Caching
SQL Azure
Azure Table

<strong>Q. What is cspack?</strong>
It is a command-line tool that generates a service package file (.cspkg) and prepares an application for deployment, either to Windows Azure or to the compute emulator.

<strong>Q. What is csrun?</strong>
It is a command-line tool that deploys a packaged application to the Windows Azure compute emulator and manages the running service.

<strong>Q. What is guest OS?</strong>
It is the operating system that runs on the virtual machine that hosts an instance of a role.

<strong>Q. How to programmatically scale out Azure Worker Role instances?</strong>
Using AutoScaling Application Block

&nbsp;

<strong>Q. What is the difference between Public Cloud and Private Cloud?</strong>
Public cloud is used as a service via Internet by the users, whereas a private cloud, as the name conveys is deployed within certain boundaries like firewall settings and is completely managed and monitored by the users working on it in an organization.

<strong>Q. How to design applications to handle connection failure in windows Azure?</strong>
The Transient Fault Handling Application Block supports various standard ways of generating the retry delay time interval, including fixed interval, incremental interval (the interval increases by a standard amount), and exponential back-off (the interval doubles with some random variation).
static RetryPolicy policy = new RetryPolicy(5, TimeSpan.FromSeconds(2), TimeSpan.FromSeconds(2)); policy.ExecuteAction(() =&gt; { try { string federationCmdText = @”USE FEDERATION Customer_Federation(ShardId =” + shardId + “) WITH RESET, FILTERING=ON”; customerEntity.Connection.Open(); customerEntity.ExecuteStoreCommand(federationCmdText); } catch (Exception e) { customerEntity.Connection.Close(); SqlConnection.ClearAllPools(); } });

<strong>Q. What is windows Azure Diagnostics?</strong>
Windows Azure Diagnostics enables you to collect diagnostic data from an application running in Windows Azure. You can use diagnostic data for debugging and troubleshooting, measuring performance, monitoring resource usage, traffic analysis and capacity planning, and auditing. HTTP://WWW.WINDOWSAZURE.COM/EN-US/DEVELOP/NET/COMMON-TASKS/DIAGNOSTICS/

<strong>Q. What is Blob?</strong>
BLOB stands for Binary Large Object. Blob is file of any type and size.
The Azure Blob Storage offers two types of blobs –
1. Block Blob
2. Page Blob
URL format: Blobs are addressable using the following URL format:

<strong>Q. What is the difference between Block Blob vs Page Blob?</strong>
Block blobs are comprised of blocks, each of which is identified by a block ID.
You create or modify a block blob by uploading a set of blocks and committing them by their block IDs.
If you are uploading a block blob that is no more than 64 MB in size, you can also upload it in its entirety with a single Put Blob operation. -Each block can be a maximum of 4 MB in size. The maximum size for a block blob in version 2009-09-19 is 200 GB, or up to 50,000 blocks.
Page blobs are a collection of pages. A page is a range of data that is identified by its offset from the start of the blob. To create a page blob, you initialize the page blob by calling Put Blob and specifying its maximum size.
-The maximum size for a page blob is 1 TB. A page written to a page blob may be up to 1 TB in size.
what to use block blobs for: streaming video. “The application must provide random read/write access” which is supported by Page Blobs

<strong>Q. What is the difference between Windows Azure Queues and Windows Azure Service Bus Queues?</strong>
Windows Azure supports two types of queue mechanisms: Windows Azure Queues and Service Bus Queues.
Windows Azure Queues, which are part of the Windows Azure storage infrastructure, feature a simple REST-based Get/Put/Peek interface, providing reliable, persistent messaging within and between services.
Service Bus Queues are part of a broader Windows Azure messaging infrastructure that supports queuing as well as publish/subscribe, Web service remoting, and integration patterns.
HTTP://WCFPRO.WORDPRESS.COM/2010/12/06/COMMUNICATION-IN-WINDOWS-AZURE/
HTTP://MSDN.MICROSOFT.COM/EN-US/LIBRARY/WINDOWSAZURE/HH767287.ASPX

<strong>Q. What is DeadLetter queue?</strong>
1. Messages are placed on the deadletter sub-queue by the messaging system in the following scenarios.
2. When a message expires and deadlettering for expired messages is set to true in a queue or subscription.
3. When the max delivery count for a message is exceeded on a queue or subscription.
4. When a filter evaluation exception occurs in a subscription and deadlettering is enabled on filter evaluation exceptions.

<strong>Q. What are instance sizes of Azure?</strong>
Windows Azure will handle the load balancing for all of the instances that are created. The VM sizes are as follows:
Compute Instance Size CPU Memory Instance Storage I/O Performance
Extra Small 1.0 Ghz 768 MB 20 GB Low
Small 1.6 GHz 1.75 GB 225 GB Moderate
Medium 2 x 1.6 GHz 3.5 GB 490 GB High
Large 4 x 1.6 GHz 7 GB 1,000 GB High
Extra large 8 x 1.6 GHz 14 GB 2,040 GB High

<strong>Related Page: <a href="https://mindmajix.com/azure-active-directory">Azure Active Directory</a></strong>

<strong>Q. What is table storage in Windows Azure?</strong>
The Windows Azure Table storage service stores large amounts of structured data.
The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Windows Azure cloud.
Windows Azure tables are ideal for storing structured, non-relational data
<strong>Table:</strong> A table is a collection of entities. Tables don’t enforce a schema on entities, which means a single table can contain entities that have different sets of properties. An account can contain many tables
<strong>Entity: </strong>An entity is a set of properties, similar to a database row. An entity can be up to 1MB in size.
<strong>Properties:</strong> A property is a name-value pair. Each entity can include up to 252 properties to store data. Each entity also has 3 system properties that specify a partition key, a row key, and a timestamp.
Entities with the same partition key can be queried more quickly, and inserted/updated in atomic operations. An entity’s row key is its unique identifier within a partition.
HTTP://MSDN.MICROSOFT.COM/EN-US/LIBRARY/WINDOWSAZURE/HH508997.ASPX

&nbsp;

Refernces
<ul>
 	<li>https://www.whizlabs.com/blog/azure-solution-architect-interview-questions/</li>
 	<li>https://www.edureka.co/blog/interview-questions/azure-interview-questions/</li>
 	<li>https://mindmajix.com/azure-interview-questions</li>
</ul>
