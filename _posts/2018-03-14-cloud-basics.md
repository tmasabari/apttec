---
layout: post
title: Cloud Basics
date: 2018-03-14 11:12
author: tmasabari
comments: true
categories: [AWS, Azure, Cloud]
---
<h2>Background</h2>
The intention of this article is to collect the notes on ‘cloud’ and include my own experiences as quick refresh guide.
<ul>
 	<li><a href="http://www.cloudcomputingpatterns.org/#cloud_computing_fundamentals">Cloud computing fundamentals</a> describe cloud service models and cloud deployment types analogous to the <a href="http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf">NIST cloud definition</a></li>
</ul>
<h2>Basics</h2>
Cloud computing is a model for enabling ubiquitous, convenient, <strong>on-demand</strong> network access to a <strong>shared pool of configurable computing resources</strong> (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with <strong>minimal management effort</strong> or service provider interaction. This cloud model is composed of five essential characteristics<strong>,</strong> three service models, and four deployment models.
<h3>Why Cloud ?</h3>
<ul>
 	<li>cloud market grew 28% 110B in 2015</li>
 	<li>18mn cloud computing jobs</li>
 	<li>$90k median salary</li>
 	<li>Salary market
<ul>
 	<li>125K$</li>
 	<li>18million jobs worldwideEconomy of scale - Cost effectiveness</li>
</ul>
</li>
</ul>
<h3><strong>Essential Characteristics: </strong></h3>
<ol>
 	<li><em>On-demand self-service.</em> A consumer can unilaterally provision computing capabilities, such as server time and network storage, as needed automatically without requiring human interaction with each service provider.</li>
 	<li><em>Broad network access.</em> Capabilities are available over the network and accessed through standard mechanisms that promote use by heterogeneous thin or thick client platforms (e.g., mobile phones, tablets, laptops, and workstations).</li>
 	<li><em>Resource pooling.</em> The provider’s computing resources are pooled to serve multiple consumers using a multi-tenant model, with different physical and virtual resources dynamically assigned and reassigned according to consumer demand. There is a sense of location independence in that the customer generally has no control or knowledge over the exact location of the provided resources but may be able to specify location at a higher level of abstraction (e.g., country, state, or datacenter). Examples of resources include storage, processing, memory, and network bandwidth.</li>
 	<li><em>Rapid elasticity.</em> Capabilities can be elastically provisioned and released, in some cases automatically, to scale rapidly outward and inward commensurate with demand. To the consumer, the capabilities available for provisioning often appear to be unlimited and can be appropriated in any quantity at any time.</li>
 	<li><em>Measured service.</em> Cloud systems automatically control and optimize resource use by leveraging a metering capability<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> at some level of abstraction appropriate to the type of service (e.g., storage, processing, bandwidth, and active user accounts). <strong>Resource usage can be monitored, controlled, and reported</strong>, providing transparency for both the provider and consumer of the utilized service.</li>
</ol>
<h3><strong>Service Models:</strong></h3>
Based up on the need of management / flexibility / control
<ol>
 	<li><em>Software as a Service (SaaS).</em> The capability provided to the consumer is to use the provider’s applications running on a cloud infrastructure<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>. The applications are accessible from various client devices through either a thin client interface, such as a web browser (e.g., web-based email), or a program interface. The consumer does not manage or control the underlying cloud infrastructure including network, servers, operating systems, storage, or even individual application capabilities, with the possible exception of limited userspecific application configuration settings.
<ol>
 	<li>end user application</li>
</ol>
</li>
 	<li><em>Platform as a Service (PaaS)</em>. The capability provided to the consumer is to deploy onto the cloud infrastructure consumer-created or acquired applications created using programming languages, libraries, services, and tools supported by the provider.<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a> The consumer does not manage or control the underlying cloud infrastructure including network, servers, operating systems, or storage, but has control over the deployed applications and possibly configuration settings for the application-hosting environment.
<ol>
 	<li>Software maintenance - patch updates</li>
 	<li>capacity planning</li>
 	<li>resource procurement</li>
 	<li>tasks of running an application / application monitoring</li>
</ol>
</li>
 	<li><em>Infrastructure as a Service (IaaS). - hardware as a service</em>
<ol>
 	<li>The capability provided to the consumer is to provision<strong> processing, storage, networks, and other fundamental computing resources</strong> where the consumer is able to deploy and run arbitrary software, which can include operating systems and applications.</li>
 	<li>The consumer does not manage or control the underlying cloud infrastructure but has <strong>control over operating systems, storage, and deployed applications</strong>; and possibly limited control of select networking components (e.g., host firewalls).</li>
</ol>
</li>
</ol>
<h3><strong>Deployment Models: distinct forms</strong></h3>
Based up on the need of  security / monitoring / automation
<ol>
 	<li><em>Private cloud. </em>The cloud infrastructure is provisioned for exclusive use by a single organization comprising multiple consumers (e.g., business units). It may be owned, managed, and operated by the organization, a third party, or some combination of them, and it may exist on or off premises.
<ol>
 	<li>data center on private network for enterprises / projects</li>
</ol>
</li>
 	<li><em>Community cloud.</em> The cloud infrastructure is provisioned for exclusive use by a specific community of consumers from organizations that have shared concerns (e.g., mission, security requirements, policy, and compliance considerations). It may be owned, managed, and operated by one or more of the organizations in the community, a third party, or some combination of them, and it may exist on or off premises.</li>
 	<li><em>Public cloud. </em>The cloud infrastructure is provisioned for open use by the general public. It may be owned, managed, and operated by a business, academic, or government organization, or some combination of them.  It exists on the premises of the cloud provider.
<ol>
 	<li>launch non secured applications - open to www / internet</li>
 	<li>Ex. AWS, Windows Azure, Sun Cloud, IBM's blue cloud</li>
</ol>
</li>
 	<li><em>Hybrid cloud</em>. The cloud infrastructure is a composition of two or more distinct cloud infrastructures (private, community, or public) that remain unique entities, but are bound together by standardized or proprietary technology that enables data and application portability (e.g., cloud bursting for load balancing between clouds).</li>
</ol>
<a href="#_ftnref1" name="_ftn1">[1]</a> Typically this is done on a <strong>pay-per-use or charge-per-use</strong> basis.

<a href="#_ftnref2" name="_ftn2">[2]</a> A cloud infrastructure is the collection of hardware and software that enables the five essential characteristics of cloud computing. The cloud infrastructure can be viewed as containing both a <strong>physical layer and an abstraction layer</strong>. The physical layer consists of the hardware resources that are necessary to support the cloud services being provided, and typically includes server, storage and network components. The abstraction layer consists of the software deployed across the physical layer, which manifests the essential cloud characteristics.  Conceptually the abstraction layer sits above the physical layer.

<a href="#_ftnref3" name="_ftn3">[3]</a> This capability does not necessarily preclude the use of compatible programming languages, libraries, services, and tools from other sources.
