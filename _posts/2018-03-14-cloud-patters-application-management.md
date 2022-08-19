---
layout: post
title: Cloud patterns - Application management
date: 2018-03-14 15:20
author: tmasabari
comments: true
categories: [Architecture, AWS, Azure, Cloud, Design, Design, Patterns]
---
<h2>Background</h2>
<a href="http://www.cloudcomputingpatterns.org/#cloud_application_management">Cloud application management</a> describes how distributed applications can be managed during runtime using additional management components, which rely on functionality provided by the application itself, cloud offerings, and the cloud environment
<h2><a href="http://www.cloudcomputingpatterns.org/provider_adapter/">Provider Adapter</a></h2>
<ul>
 	<li>The integration between the private cloud and public cloud should be easily replaceble and loosely coupled</li>
 	<li>Cloud providers offer many interfaces that can be used in application components of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a>.</li>
 	<li>If a component directly interacts with these interfaces, its implementation becomes strongly interleaved with the specific functions offered and the protocols used.</li>
 	<li>The Provider Adapter encapsulates all provider-specific implementations required for authentication, data formatting etc. in an abstract interface.</li>
 	<li>The Provider Adapter , thus, ensures separation of concerns between application components accessing provider functionality and application components providing application functionality.</li>
 	<li>It may also offer synchronous provider-interfaces to be accessed asynchronously via messages and vice versa.</li>
 	<li>
<p id="DcOuVNs"><img class="alignnone wp-image-944 " src="/wp-content/uploads/2018/03/img_5aa8dd1fe5b28.png" alt="" width="385" height="93" /><img class="alignnone wp-image-943 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5aa8dd0f425b4.png" alt="" width="318" height="191" /></p>
&nbsp;</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/managed_configuration/">Managed Configuration</a></h3>
<ul>
 	<li>Scaled-out application components should use a centrally stored configuration to provide a unified behavior that can be adjusted simultaneously.</li>
 	<li>If configurations are stored with the components, in case of changes
<ul>
 	<li>Each running instance of the application component must be updated separately.</li>
 	<li>Component images stored in <a href="http://www.cloudcomputingpatterns.org/elastic_infrastructure/">Elastic Infrastructures</a> or <a href="http://www.cloudcomputingpatterns.org/elastic_platform/">Elastic Platforms</a> also have to be updated upon configuration change.</li>
</ul>
</li>
 	<li>Configurations are stored in a central <a href="http://www.cloudcomputingpatterns.org/cloud_offerings/#storage_offerings">Storage Offering</a>, commonly, a <a href="http://www.cloudcomputingpatterns.org/relational_database/">Relational Database</a>, <a href="http://www.cloudcomputingpatterns.org/key_value_storage/">Key-Value Storage</a>, or <a href="http://www.cloudcomputingpatterns.org/blob_storage/">Blob Storage</a> from where it is accessed by all running component instances either by accessing the storage periodically or by sending messages to the components.</li>
 	<li>
<p id="DwwUcxw"><img class="alignnone wp-image-945 " src="/wp-content/uploads/2018/03/img_5aa8df445bada.png" alt="" width="425" height="140" /></p>
</li>
</ul>
<h2>ScaleOut and Failure recovery</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/watchdog/">Watchdog</a></h3>
<ul>
 	<li>If a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> is comprised of many application components it is <strong>dependent on the availability of all component instances</strong>.</li>
 	<li>To enable high availability under such conditions, applications have to <strong>rely on redundant application component instances</strong> and the <strong>failure of these instances has to be detected</strong> and coped with automatically.</li>
 	<li>Individual application components rely on external state information by implementing the <a href="http://www.cloudcomputingpatterns.org/stateless_component/">Stateless Component</a> pattern.</li>
 	<li>Components are <strong>scaled out</strong> and multiple instances of them are deployed to redundant resources. The component instances are monitored by a separate Watchdog component and replaced in case of failures.</li>
 	<li>
<p id="rVwivax"><img class="alignnone size-full wp-image-949 " src="/wp-content/uploads/2018/03/img_5aa8e675d3c8e.png" alt="" /></p>
</li>
</ul>
<h2>Scale Out Horizontally</h2>
<ul>
 	<li>Application components of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> shall be scaled out automatically.</li>
 	<li>The instances of applications components, thus, shall be provisioned (scaled up) and decommissioned (scaled down) <strong>automatically</strong> based on the current workload experienced by the application.</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/elasticity_manager/">Elasticity Manager</a></h3>
<ul>
 	<li>The <strong>utilization of IT resources</strong> on which an elastically scaled-out application is hosted, for example, virtual servers is used to determine the number of required application component instances.  This could be, for example, the <strong style="font-size: 1rem;">CPU load</strong><span style="font-size: 1rem;"> of a virtual server. </span></li>
 	<li>
<p id="fXaEkFg"><img class="alignnone size-full wp-image-946 " src="/wp-content/uploads/2018/03/img_5aa8e21627e8f.png" alt="" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/elastic_queue/">Elastic Queue</a></h3>
<ul>
 	<li>The n<strong>umber of asynchronous accesses via messaging</strong> to an elastically scaled-out application is used to adjust the number of required application component instances.</li>
 	<li>Queues that are used to distribute asynchronous requests among multiple application components instances are monitored.</li>
 	<li>
<p id="ihDviMn"><img class="alignnone wp-image-947 " src="/wp-content/uploads/2018/03/img_5aa8e312b7c68.png" alt="" width="348" height="212" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/elastic_load_balancer/">Elastic Load Balancer</a></h3>
<ul>
 	<li>The <strong>number of synchronous accesses (requests to application)</strong> to an elastically scaled-out application is used to determine the <strong>number of required application component instances</strong>.</li>
 	<li>
<p id="jdckSEQ"><img class="alignnone wp-image-948 " src="/wp-content/uploads/2018/03/img_5aa8e3f38c738.png" alt="" width="400" height="244" /></p>
<p id="rVwivax"></p>
</li>
</ul>
<ul>
 	<li>
<p id="TByudJn"></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/elasticity_management_process/">Elasticity Management Process</a></h3>
<ul>
 	<li>Application component instances are added automatically to an application to cope with increasing workload. If the workload decreases application component instances are removed respectively.</li>
 	<li>A <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> uses <a href="http://www.cloudcomputingpatterns.org/elasticity_manager/">Elasticity Managers</a>, <a href="http://www.cloudcomputingpatterns.org/elastic_queue/">Elastic Queues</a>, or <a href="http://www.cloudcomputingpatterns.org/elastic_load_balancer/">Elastic Load Balancers</a> to ensure an elastic scaling of application components.</li>
 	<li>An Elasticity Management Process <strong>analyzes the utilization</strong> of application component instances in <strong>intervals</strong>, when a system manager <strong>requests it</strong>, or if certain conditions are observed by the monitoring component. Based on this information, the current workload of the application is computed and reflected by adjusting used resources.</li>
 	<li>
<p id="zoyAvUp"><img class="alignnone wp-image-953 " src="/wp-content/uploads/2018/03/img_5aa8ee40b3cbc.png" alt="" width="367" height="603" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/standby_pooling_process/">Standby Pooling Process</a></h3>
<ul>
 	<li>Even though application component instances may be provisioned and decommissioned dynamically, it usually <strong>requires some time to actually provision and decommission</strong> them.</li>
 	<li>If a cloud application, however, experiences drastic and quick workload changes, these provisioning times may limit its capability to obtain the required resources quickly enough.</li>
 	<li><strong>Decommissioning</strong> of component instances <strong>immediately</strong> when no longer needed may also be <strong>ineffective</strong>, if cloud resources are charged <strong>for fixed time-slots</strong>.</li>
 	<li>Instead of decommissioning application component instances instantly when they are unused, they are assigned to a standby list They are decommissioned only when the time-slot they have been paid for has been utilized and they are still not needed.</li>
 	<li><strong>The standby list</strong> may always contain a certain number of component instances to <strong>ensure timely provisioning</strong>.</li>
 	<li>
<p id="vTOdKBh"><img class="alignnone wp-image-951 " src="/wp-content/uploads/2018/03/img_5aa8ec144ec63.png" alt="" width="338" height="398" /><img class="alignnone wp-image-952 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5aa8ed18045f9.png" alt="" width="380" height="391" /></p>
</li>
</ul>
<h3>Resiliency Management Process</h3>
<ul>
 	<li>In addition to watchdog, the Resiliency Management Process periodically verifies application component health. If a failure is detected, the faulty application component instance is decommissioned and replaced by a newly provisioned instance.</li>
 	<li>
<p id="TByudJn"><img class="alignnone wp-image-950 " src="/wp-content/uploads/2018/03/img_5aa8eb397d980.png" alt="" width="455" height="603" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/feature_flag_management_process/">Feature Flag Management Process</a></h3>
<ul>
 	<li>If the <strong>workload increases too drastically</strong>, it may take too long to provision new resources. Furthermore, cloud providers often <strong>do not guarantee concrete provisioning times</strong>.</li>
 	<li>Less important application functionality provided by application component instances is disabled or <strong>replaced with a less demanding implementation</strong>, if the cloud provider cannot fulfill current workload demands. When resources can eventually be provisioned again, the application components return to normal operation.</li>
 	<li>
<p id="nhxXOEa"><img class="alignnone wp-image-954 " src="/wp-content/uploads/2018/03/img_5aa8ef4cdbc3a.png" alt="" width="421" height="774" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/update_transition_process/">Update Transition Process</a></h3>
<ul>
 	<li>During the runtime of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a>, new versions of used middleware, operating systems, or application components may become available.</li>
 	<li>A seamless switch from the old to the new version of application components shall be enabled.
<ol>
 	<li>The new component version is created. Additional application component instances of the new version are provisioned.</li>
 	<li>These components are executed simultaneously with the application components of the old version.</li>
 	<li>f necessary, load balancing is then switched to the component instances of the new version. If the application components access a queue, this step is unnecessary.</li>
 	<li>Finally, the old application component instances are decommissioned.</li>
</ol>
</li>
 	<li>
<p id="udVUUQh"><img class="alignnone wp-image-955 " src="/wp-content/uploads/2018/03/img_5aa8f023d27b5.png" alt="" width="440" height="473" /></p>
</li>
</ul>
