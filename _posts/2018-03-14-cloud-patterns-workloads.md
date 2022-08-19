---
layout: post
title: Cloud Patterns - Workloads
date: 2018-03-14 10:48
author: tmasabari
comments: true
categories: [Architecture, AWS, Azure, Cloud, Design, Design, Patterns]
---
<h2>Background</h2>
<a href="http://www.cloudcomputingpatterns.org/#composite_cloud_applications">Composite cloud applications</a> cover frequent combinations of patterns from all other categories in various use cases.
<h2>Scale Out</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/map_reduce/">Map Reduce</a></h3>
<ul>
 	<li>Cloud applications often have to handle very large amounts of data, which have to be processed efficiently. As <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Applications</a> are designed to scale out,
<ol>
 	<li>data processing should be <strong>distributed (mapped)</strong> among multiple application component instances in a similar means.</li>
 	<li>Data Processing Components simultaneously execute the query to be performed on the assigned data chunks.</li>
 	<li>Afterwards, results of these distributed components have to be <strong>consolidated (reduced)</strong>.</li>
</ol>
</li>
 	<li>During the distribution or reduction, additional functions, such calculations of sums, average values etc. may be used.</li>
 	<li>
<p id="kOerIUJ"><img class="alignnone size-full wp-image-937 " src="/wp-content/uploads/2018/03/img_5aa8cee060585.png" alt="" /></p>
</li>
</ul>
&nbsp;
<h2>Hybrid components</h2>
<ul>
 	<li><a href="http://www.cloudcomputingpatterns.org/#composite_cloud_applications">Composite cloud applications</a> cover frequent combinations of patterns from all other categories in various use cases</li>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> provides processing functionality that experience different workload behavior.</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_multimedia_web_application/">Hybrid Multimedia Web Application</a></h3>
<ul>
 	<li>Website content is largely provided from a static environment.</li>
 	<li>Multimedia files that cannot be cached efficiently are provided from a large distributed elastic environment for high-performance access, where it is accessed from the application’s <a style="font-size: 1rem;" href="http://www.cloudcomputingpatterns.org/user_interface_component/">User Interface Component</a><span style="font-size: 1rem;">.</span></li>
 	<li>The static content is provided to users’ client software and in this static content, the multimedia content is referenced.</li>
 	<li>Retrieval of this streaming content is often handled directly by the users’ browser software.</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/hybrid_multimedia_web_application_sketch.png" alt="Hybrid_Multimedia_Web_Application" /></li>
</ul>
&nbsp;
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_user_interface/">Hybrid User Interface</a></h3>
<ul>
 	<li>Context
<ul>
 	<li>One user group generates <a href="http://www.cloudcomputingpatterns.org/static_workload/">Static Workload</a>,</li>
 	<li>while another user group generates <a href="http://www.cloudcomputingpatterns.org/periodic_workload/">Periodic Workload</a>, <a href="http://www.cloudcomputingpatterns.org/once_in_a_lifetime_workload/">Once-in-a-lifetime Workload</a>, <a href="http://www.cloudcomputingpatterns.org/unpredictable_workload/">Unpredictable Workload</a>, or <a href="http://www.cloudcomputingpatterns.org/continuously_changing_workload/">Continuously Changing Workload</a>.</li>
 	<li>Since the predictability of the user group size and workload behavior differs, it shall be ensured that unexpected peak workloads do not affect the performance of the application while each user group is handled by the most suitable cloud environment.</li>
</ul>
</li>
 	<li>Solution
<ul>
 	<li>The <a href="http://www.cloudcomputingpatterns.org/user_interface_component/">User Interface Component</a> serving users generating varying workload is hosted in an elastic cloud environment.</li>
 	<li>Other application components that are hosted in a static environment.</li>
 	<li>The user interface deployed in the elastic cloud is integrated with the remainder of the application in a decoupled fashion using messaging to ensure <a href="http://www.cloudcomputingpatterns.org/loose_coupling/">Loose Coupling</a>.</li>
</ul>
</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/hybrid_user_interface_sketch.png" alt="Hybrid User Interface" /></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_processing/">Hybrid Processing</a></h3>
<ul>
 	<li>The user group (all users) accesses the functions provided by the application differently.</li>
 	<li>While most of the functions are used equally over time and, therefore, experience <a href="http://www.cloudcomputingpatterns.org/static_worklaod/">Static Workload</a>, some <a href="http://www.cloudcomputingpatterns.org/processing_component/">Processing Components</a> experience <a href="http://www.cloudcomputingpatterns.org/periodic_worklaod/">Periodic Workload</a>, <a href="http://www.cloudcomputingpatterns.org/unpredictable_workload/">Unpredictable Workload</a>, or <a href="http://www.cloudcomputingpatterns.org/continuously_changing_workload/">Continuously Changing Workload</a>.</li>
 	<li>The <a href="http://www.cloudcomputingpatterns.org/processing_component/">Processing Components</a> experiencing varying workloads are provisioned in an elastic cloud. <a href="http://www.cloudcomputingpatterns.org/loose_coupling/">Loose Coupling</a> is ensured by exchanging information between the hosting environments asynchronously via messages.</li>
 	<li>
<p id="JQSGCtn"><img class="alignnone size-full wp-image-876 " src="/wp-content/uploads/2018/03/img_5aa7b7602b031.png" alt="" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_data/">Hybrid Data</a></h3>
<ul>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> handles data whose size varies drastically over time. Large amounts of data may, thus, be generated periodically and are then deleted again, may <strong>increase and decrease randomly</strong>, or may <strong>display a general increase or decrease over time</strong>.</li>
 	<li>Data whose varying size makes it unsuitable for hosting in a static environment is handled by Storage Offerings in an elastic cloud.</li>
 	<li>At this location data is either accessed by <a href="http://www.cloudcomputingpatterns.org/data_access_component/">Data Access Components</a> that are hosted in the static environment or by Data Access Components hosted in the elastic environment.</li>
 	<li>
<p id="jSSsoIY"><img class="alignnone size-full wp-image-877 " src="/wp-content/uploads/2018/03/img_5aa7b80f60d15.png" alt="" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_backend/">Hybrid Backend</a> (Processing and Data)</h3>
<ul>
 	<li>Context
<ol>
 	<li>Mainly, <a href="http://www.cloudcomputingpatterns.org/static_workload/">Static Workload</a> has to be handled, but some Processing Components experience <a href="http://www.cloudcomputingpatterns.org/periodic_workload/">Periodic Workload</a>, <a href="http://www.cloudcomputingpatterns.org/unpredictable_workload/">Unpredictable Workload</a>, or <a href="http://www.cloudcomputingpatterns.org/continuously_changing_workload/">Continuously Changing Workload</a>.</li>
 	<li>However, these components have to access large amounts of data during their execution making them highly dependent on the availability and the timely access to such data</li>
</ol>
</li>
 	<li>Solution
<ul>
 	<li>The Processing Components experiencing varying workloads are hosted in an elastic cloud together with the data accessed during their operation.</li>
 	<li>Processing Components in the elastic cloud are triggered from the static environment through asynchronous messages exchanged via message queues provided by a <a href="http://www.cloudcomputingpatterns.org/message_oriented_middleware/">Message-oriented Middleware</a>.</li>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/data_access_component/">Data Access Component</a> in the static environment ensures that data required by elastic Processing Components is stored in Storage Offerings</li>
 	<li>Data that is not required by the backend functionality may still be stored in <a href="http://www.cloudcomputingpatterns.org/stateful_component/">Stateful Components</a> hosted in the static data center.</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/hybrid_backend_sketch.png" alt="Hybrid Backend" /></li>
</ul>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_application_functions/">Hybrid Application Functions</a></h3>
<ul>
 	<li>Application components comprising a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> experience varying workloads on all layers of the application stack</li>
 	<li>In addition to the workload requirements other issues, such as legal and corporate regulations or requirements on security, privacy, and trust may limit the environments to which an application component may be provisioned.</li>
 	<li>solution
<ul>
 	<li>Application components are grouped regarding similar requirements and are deployed into best fitting environments.</li>
 	<li>Inter-dependencies between the components are reduced by exchanging data using asynchronous messaging to ensure <a href="http://www.cloudcomputingpatterns.org/loose_coupling/">Loose Coupling</a>.</li>
 	<li>Depending on the accessed function, a <strong>load balancer</strong> redirects user accesses to the different environments seamlessly.</li>
</ul>
</li>
 	<li>
<p id="zJxYmQt"><img class="alignnone wp-image-878 " src="/wp-content/uploads/2018/03/img_5aa7bd57a48a1.png" alt="" width="378" height="278" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_backup/">Hybrid Backup</a></h3>
<ul>
 	<li>Especially, requirements regarding business resiliency – the ability to recover from an error – and business continuity – the ability to operate during an error – are challenging.</li>
 	<li>Furthermore, there are laws and regulations making businesses liable to <strong>archive data</strong> and keep it <strong>accessible for audits</strong>, often over <strong>very long periods of time</strong>.</li>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> is hosted in a local static environment of the company. Data handled by <a href="http://www.cloudcomputingpatterns.org/stateful_component/">Stateful Components</a> is periodically extracted and replicated to a cloud storage offering.</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/hybrid_backup_sketch.png" alt="Hybrid Backup" /></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/hybrid_development_environment/">Hybrid Development Environment</a></h3>
<ul>
 	<li>Applications have different requirements on the runtime environment during their development, test, and production phase.</li>
 	<li>During development, hardware requirements are often uncertain, so hardware resources should be flexible to extend resources if necessary.</li>
 	<li>During the test phase, diverse test systems may be needed to verify the proper functioning of the application
<ol>
 	<li>on different operating systems or</li>
 	<li>when being accessed using different client software, i.e., different browsers.</li>
 	<li>Large numbers of resources may also be required to perform load tests.</li>
 	<li>During the productive use other factors, such as security and availability may be of greater importance than resource flexibility.</li>
</ol>
</li>
 	<li>The production environment of the application is simulated in the development and test environment through the use of equivalent addressing, similar mocking data, and equivalent functionality provided by the environment.</li>
 	<li>Migration of developed applications is ensured through transformation of application components or compatibility of runtimes.</li>
 	<li>Some testing resources are provided exclusively in the development environment to verify the application behavior under different circumstances.</li>
 	<li>
<p id="PMBOEXL"><img class="alignnone size-full wp-image-879 " src="/wp-content/uploads/2018/03/img_5aa7c512788c1.png" alt="" /></p>
</li>
</ul>
&nbsp;
<ul>
 	<li>http://www.restapitutorial.com/lessons/idempotency.html</li>
 	<li>https://en.wikipedia.org/wiki/Idempotence#Examples</li>
</ul>
