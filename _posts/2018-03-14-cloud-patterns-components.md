---
layout: post
title: Cloud Patterns - Components
date: 2018-03-14 10:47
author: tmasabari
comments: true
categories: [Architecture, AWS, Azure, Cloud, Design, Design, Patterns]
---
<h2>State based Component categories</h2>
<ul>
 	<li>The components of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> are deployed among multiple cloud resources to benefit from this distributed runtime environment through scaling out</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/stateful_component/">Stateful Component</a></h3>
<ul>
 	<li>Components maintain an internal state</li>
 	<li><strong>Multiple instances</strong> of <strong>a</strong> scaled-out application component synchronize their internal state to provide a unified behavior.</li>
 	<li>The internal state maintained by application component instances is replicated among all instances.</li>
 	<li>Examples: a configuration file stored centrally or configurations send by clients with every request.</li>
 	<li>ASP.NET IN Process session store with sticky sessions for distributed applications.</li>
 	<li>
<p id="ZaBFkfV"><img class="alignnone wp-image-850 " src="/wp-content/uploads/2018/03/img_5aa77a685df44.png" alt="" width="296" height="90" /></p>
</li>
 	<li>The most significant factor complicating addition and removal of component instances in this scope is the internal state maintained by them. In case of failure, this information may even be lost.</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/stateless_component/">Stateless Component</a></h3>
<ul>
 	<li>State is handled external of application components to ease their scaling-out and to make the application more tolerant to component failures.</li>
 	<li>implemented in a fashion that they do not have an internal state. Instead, their state and configuration is stored externally in <a href="http://www.cloudcomputingpatterns.org/cloud_offerings/#storage_offerings">Storage Offerings</a> or provided to the component with each request.</li>
 	<li>
<p id="ipdUIhG"><img class="alignnone wp-image-851 " src="/wp-content/uploads/2018/03/img_5aa77b7d02fe2.png" alt="" width="287" height="106" /></p>
</li>
 	<li>ASP.NET out of process session store</li>
</ul>
<h2>Layer based Component categories</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/user_interface_component/">User Interface Component</a></h3>
<ol>
 	<li>serves as a bridge between the synchronous access of the human user and the asynchronous communication used with other application components</li>
 	<li>Implemented as <a href="http://www.cloudcomputingpatterns.org/stateless_component/">Stateless Component</a> pattern</li>
 	<li>scaled based on the number of synchronous requests to is as described by the <a href="http://www.cloudcomputingpatterns.org/elastic_load_balancer/">Elastic Load Balancer</a> pattern.
<p id="AFBqpHY"><img class="alignnone wp-image-852 " src="/wp-content/uploads/2018/03/img_5aa77ccde22ca.png" alt="" width="273" height="157" /></p>

<ol>
 	<li>attached to requests, may be held in a part of the user interface that is deployed on the user’s access device, or</li>
 	<li>may be obtained from external storage</li>
</ol>
</li>
</ol>
<h3><a href="http://www.cloudcomputingpatterns.org/processing_component/">Processing Component</a></h3>
<ol>
 	<li>Possibly <strong>long running processing functionality</strong> is handled by separate independent components (<strong>function blocks)</strong> to enable elastic scaling.</li>
 	<li>Processing functionality is further <strong>made configurable</strong> to support different customer requirements.</li>
 	<li><strong>Scaling is handled by an <a href="http://www.cloudcomputingpatterns.org/elastic_queue/">Elastic Queue</a></strong>. Data required for processing is provided with requests or by <a href="http://www.cloudcomputingpatterns.org/cloud_offerings/#storage_offerings">Storage Offerings</a>.</li>
 	<li>
<p id="lGMTpnu"><img class="alignnone wp-image-853 " src="/wp-content/uploads/2018/03/img_5aa77e9141ee5.png" alt="" width="345" height="174" /></p>
</li>
</ol>
<h3><a href="http://www.cloudcomputingpatterns.org/data_access_component/">Data Access Component</a></h3>
<ul>
 	<li>This component coordinates all data manipulation, Isolate complexity of data access, enable additional <strong>data consistency</strong>, and ensure <strong>adjustability of handled data elements</strong> to meet different customer requirements.</li>
 	<li>Handling the complexity of accessing data, i.e., handling of authorization, querying for data, failure handling etc.</li>
 	<li><strong>Different data sources</strong> should be integrated to provide a unified data access to other application components.</li>
 	<li>Also, data may be stored at <strong>different cloud providers</strong> that have to be integrated as well.</li>
 	<li>In case a storage offering shall be replaced or the interface of a storage offering changes, the Data Access Component is the only component that has to be adjusted.</li>
 	<li>
<p id="klqNMtq"><img class="alignnone wp-image-854 " src="/wp-content/uploads/2018/03/img_5aa77fa0e9c70.png" alt="" width="237" height="174" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/batch_processing_component/">Batch Processing Component</a></h3>
<ul>
 	<li>Asynchronous processing requests are <strong>accepted at all times</strong>, but <strong>stored them</strong> until conditions are optimal for their processing.
<ul>
 	<li>Based on the number of stored requests,</li>
 	<li>environmental conditions, and</li>
 	<li>custom rules, components are instantiated to handle the requests</li>
 	<li>only processed under non-optimal conditions if they cannot be delayed any longer</li>
</ul>
</li>
 	<li>
<p id="SXYrfzN"><img class="alignnone wp-image-855 " src="/wp-content/uploads/2018/03/img_5aa7805dc2355.png" alt="" width="260" height="116" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/restricted_data_access_component/">Restricted Data Access Component</a></h3>
<ul>
 	<li>Hosting providers of data storage may vary based up on the assured privacy, security, and trust etc</li>
 	<li>This impacts the data that may be accessible in an environment</li>
 	<li>Data storage <strong>restrictions</strong> and access <strong>privileges</strong> are <strong>defined for each data</strong> element.</li>
 	<li>Access to these data elements is provided by separate Restricted Data Access Components that <strong>interpret the information</strong> associated with data elements. It adjusts data accordingly through <strong>deletion</strong> or <strong>obfuscation</strong> during every access.</li>
 	<li>Example: In traditional application, SPs will be created to access specific set of data and data security will be ensured with in the SP logic.
<p id="yVbAyDi"><img class="alignnone wp-image-856 " src="/wp-content/uploads/2018/03/img_5aa7817a43632.png" alt="" width="316" height="218" /></p>
</li>
</ul>
&nbsp;
<h2>Tenant based component categories</h2>
<ul>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> is offered to multiple tenants. These tenants share IT resources required by applications provided to them.</li>
 	<li>However, the sharing of application components is hindered by three factors.
<ol>
 	<li>First, tenants may have unique requirements and, thus, expect application components to be configurable to their individual needs.</li>
 	<li>Second, tenants may not trust each other.</li>
 	<li>Third, tenants expect an application to behave as if a single tenant was the only one accessing it.</li>
</ol>
</li>
 	<li>A component is accessed by multiple tenants to leverage economies of scale.</li>
 	<li>The provisioning of application component instances shall be optimized by limiting the portion of the application stack and the number of application components deployed exclusively for one tenant.</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/shared_component/">Shared Component</a></h3>
<ul>
 	<li>provides functionality that is equal for all tenants accessing the component. All tenants can be treated as a uniform user group to which a common user experience and service level is guaranteed.</li>
 	<li>
<p id="CSmVoMp"><img class="alignnone wp-image-873 " src="/wp-content/uploads/2018/03/img_5aa7a0564208e.png" alt="" width="282" height="180" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/tenant_isolated_component/">Tenant-isolated Component</a></h3>
<ul>
 	<li>Components on all layers of the application stack are specifically developed to be used by different tenants.</li>
 	<li>Especially, they ensure isolation between tenants by controlling tenant access, processing performance used, and separation of stored data.</li>
 	<li></li>
 	<li><img class="" src="http://www.cloudcomputingpatterns.org/sketches/tenant_isolated_component_sketch.png" alt="Tenant-isolated Component" width="290" height="163" /></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/dedicated_component/">Dedicated Component</a></h3>
<ul>
 	<li>Dedicated application components are provided exclusively for each tenant using the application.</li>
 	<li>
<p id="HrelIPl"><img class="alignnone wp-image-874 " src="/wp-content/uploads/2018/03/img_5aa7a5ec84605.png" alt="" width="315" height="168" /></p>
</li>
</ul>
