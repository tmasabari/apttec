---
layout: post
title: Cloud patterns - Offerings
date: 2018-03-14 10:33
author: tmasabari
comments: true
categories: [Architecture, AWS, Azure, Cloud, Design, Design, Patterns]
---
<h2>Background</h2>
<a href="http://www.cloudcomputingpatterns.org/#cloud_offerings">Cloud offerings</a> describe the functionality offered by cloud providers to be used by an application for processing of workload, communication, and data storage. Again, these patterns cover the conditions under which an offering should be selected, as well as the implications on the application.
<h2>Optimization</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/multi_component_image/">Multi-Component Image</a></h3>
<ul>
 	<li>Underutilization: The individual application components may, however, not fully utilize the <a href="http://www.cloudcomputingpatterns.org/elastic_infrastructure/">Elastic Infrastructure</a> servers (IaaS) if only one component is hosted per server.</li>
 	<li>Multiple application components (possibly including middleware) are hosted on a single virtual server to ensure that running virtual servers may be used for different purposes <strong>without making provisioning or decommissioning</strong> operations necessary.</li>
 	<li><img class="" src="http://www.cloudcomputingpatterns.org/sketches/multi_component_image_sketch.png" alt="Multi-Component Image" width="299" height="228" /></li>
</ul>
<h2>Availability</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/environment_based_availability/">Environment-based Availability</a></h3>
<ul>
 	<li>A cloud provider guarantees the <strong>availability of the environment</strong> hosting individual nodes, such as virtual servers or hosted application components.</li>
 	<li>for example, the availability for at-least-once provisioned component or virtual server and the availability to provision replacements in case of failures is assured</li>
 	<li>
<p id="HBNVvfv"><img class="alignnone size-full wp-image-933 " src="/wp-content/uploads/2018/03/img_5aa8c3e4d26d6.png" alt="" /></p>
</li>
</ul>
<h1>Node-based Availability</h1>
<ul>
 	<li>The provider assures availability for <strong>each hosted application component</strong>, which is defined to be available if it is reachable and performs its function as advertised, i.e., it provides correct results.</li>
 	<li>This timeframe is often expressed as a percentage. An availability of 99.95%, thus, means that a hosted component will be available during 99.95% of the time it is hosted at the provider.</li>
 	<li>
<p id="MvzIHbo"><img class="alignnone size-full wp-image-934 " src="/wp-content/uploads/2018/03/img_5aa8c4542a83b.png" alt="" /></p>
</li>
</ul>
<h2>Elastic Infrastructure vs Elastic Platform</h2>
[table id=10 /]
<p id="NjQLPHL"><img class=" alignleft wp-image-841" src="/wp-content/uploads/2018/03/img_5aa768edb6558.png" alt="" width="320" height="282" /></p>
<img class="alignnone wp-image-842 " src="/wp-content/uploads/2018/03/img_5aa76a49aed9e.png" alt="" width="331" height="270" />

&nbsp;
<h2>Storage Offerings</h2>
[table id=11 /]
<h2>References</h2>
<ul>
 	<li>http://www.cloudcomputingpatterns.org/</li>
</ul>
