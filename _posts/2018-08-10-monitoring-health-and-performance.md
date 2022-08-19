---
layout: post
title: Monitoring - Health and Performance
date: 2018-08-10 13:14
author: tmasabari
comments: true
categories: [Monitoring &amp; logging, NFR, Performance]
---
<img class="alignnone size-full wp-image-1695 " src="/wp-content/uploads/2018/08/img_5b6daa1ce5dc3.png" alt="" />

The good place for an overview on the available open source tools and how they can be integrated together can be checked on the <span class="qlink_container"><a class="external_link" href="http://openapm.io/" target="_blank" rel="noopener nofollow" data-qt-tooltip="openapm.io" data-tooltip="attached">OpenAPM</a></span> website. The website also provides the information about which tools to use based on tech stack or depending on what kind of APM related aspects you are interested in. As a result you can create a custom landscape of the open source APM tools as the one presented in the image below:

&nbsp;
<p id="IqLLZmI"><img class="wp-image-1697 aligncenter" src="/wp-content/uploads/2018/08/img_5b6daa74aa8e8.png" alt="" width="406" height="236" /></p>
<strong>My Selection</strong>
<p id="cXQblkT"><img class="alignnone size-full wp-image-1699 " src="/wp-content/uploads/2018/08/img_5b6dad3eebe19.png" alt="" /></p>
<a href="https://www.app-metrics.io/">App Metrics</a> is an open-source and cross-platform .NET library used to record metrics within an application. App Metrics can run on .NET Core or on the full .NET framework also supporting .NET 4.5.2.

With <a href="https://www.app-metrics.io/">App Metrics</a> you can:
<ul>
 	<li>Capture application metrics within any type of .NET application e.g. Windows Service, MVC Site, Web API etc</li>
 	<li>Automatically measure the performance and error of each endpoint in an MVC or Web API project</li>
 	<li>When securing an API with OAuth2, automatically measure the request rate and error rate per client</li>
 	<li>Choose where to persist captured metrics and the dashboard you wish to use to visualize these metrics</li>
</ul>
<em>Kamon</em> is a monitoring toolkit for applications running on the JVM.

<a href="http://micrometer.io/">Micrometer</a> provides a simple facade over the instrumentation clients for the most popular monitoring systems, allowing you to instrument your JVM-based application code without vendor lock-in. Think SLF4J, but for metrics.

<a href="https://github.com/stagemonitor/stagemonitor">Stagemonitor</a> is a Java monitoring agent that tightly integrates with time series databases
<h2>Health monitoring / Infrastructure Monitoring</h2>
Infrastructure monitoring lets you visualize events and get alerts in real time.

<strong>Tools #1, #2, #3, #4, #5 &amp; #6: Nagios, Zabbix, Sensu, Prometheus, SysDig and New Relic Infrastructure</strong>
<ul>
 	<li dir="ltr">Both <a href="http://www.nagios.org/" target="_blank" rel="noopener noreferrer">Nagios</a> &amp; <a href="http://www.zabbix.com/" target="_blank" rel="noopener noreferrer">Zabbix</a> are ‘traditional’ tools - widely used, downloadable and open source.</li>
 	<li>But these tools aren’t well-equipped to handle DevOps’ rapidly changing environment. If you’ve decided to stick with them, you’ve probably developed internal capabilities built on their APIs to extend their offerings, like supporting automatic adaptation to resource capacity and configuration changes.</li>
 	<li dir="ltr"><a href="http://sensuapp.org/" target="_blank" rel="noopener noreferrer">Sensu</a>, <a href="https://prometheus.io/" target="_blank" rel="noopener noreferrer">Prometheus</a><a href="http://www.sysdig.org/" target="_blank" rel="noopener noreferrer"> by SoundCloud</a>, <a href="http://www.sysdig.org/" target="_blank" rel="noopener noreferrer">SysDig</a> and <a href="https://newrelic.com/infrastructure" target="_blank" rel="noopener noreferrer">New Relic Infrastructure</a> are more modern, trending open source tools. All of them monitor compute resources, storage, and network, and measure inventory usage, and health of an infrastructure's resources.</li>
 	<li dir="ltr">Prometheus and SysDig are also adapted for containers, which is a very important ability in the changing world of infrastructure monitoring.</li>
 	<li><a href="https://blog.ipswitch.com/were-providing-free-microsoft-apm-tools-for-it-teams">IPSwitch</a>: The four free <a href="https://www.ipswitch.com/solutions/application-performance" target="_blank" rel="noopener">application performance monitoring (APM)</a> tools will pinpoint problems stemming from Microsoft IIS, Active Directory, SQL and Exchange.  Sysadmins can use these tools to help solve the problem they are currently having with these popular applications.</li>
 	<li>Ipswitch Free Tools that monitor availability and performance in Microsoft environments include:
<ul>
 	<li><a href="https://www.ipswitch.com/resources/free-tools/whatsup-active-directory-monitor">WhatsUp Active Directory Monitor</a>
<ul>
 	<li>Track Microsoft Active Directory availability and performance</li>
</ul>
</li>
 	<li><a href="https://www.ipswitch.com/resources/free-tools/whatsup-iis-monitor">WhatsUp IIS Monitor</a>
<ul>
 	<li>Monitor Microsoft Internet Information Services (IIS) and identify performance issues</li>
</ul>
</li>
 	<li><a href="https://www.ipswitch.com/resources/free-tools/whatsup-exchange-monitor">WhatsUp Exchange Monitor</a>
<ul>
 	<li>Ensure application availability in a Microsoft Exchange environment</li>
</ul>
</li>
 	<li><a href="https://www.ipswitch.com/resources/free-tools/whatsup-sql-server-monitor">WhatsUp SQL Server Monitor</a>
<ul>
 	<li>Monitor and keep Microsoft SQL Server running smoothly</li>
</ul>
</li>
</ul>
</li>
</ul>
I found an famous open source  tool ‘<a href="https://kjanshair.github.io/2018/02/20/prometheus-monitoring/">Prometheus</a>‘ for monitoring, recording and visualizing the server and application statuses.

It can even alert via email in case of threshold conditions on the resources like high CPU, memory usage.

Below hardware and software can be monitored
<ul>
 	<li>Windows – <a href="https://github.com/martinlindhe/wmi_exporter">WMI Exporter</a></li>
 	<li><a href="http://leapfrogonline.io/articles/2018-05-11-exporting-windows-and-sql-server-metrics-to-prometheus-with-sonar/">SQL Server</a></li>
 	<li><a href="https://groups.google.com/forum/#!topic/prometheus-developers/BsoIriE31i4">IIS</a> (web sites and services)</li>
 	<li>JVM (<a href="https://lucene.apache.org/solr/guide/7_3/monitoring-solr-with-prometheus-and-grafana.html">Solr</a>)</li>
</ul>
<h3>Cons: Administrative overhead</h3>
<ul>
 	<li>It’s not ready made tool. Operation team need to configure it with necessary plugins for visualization, alerts etc.</li>
 	<li>Each and every server needs to be configured with the exporters.</li>
 	<li>Each and every service needs to be configured with plugins(exporters)</li>
</ul>
<h3>References</h3>
<ul>
 	<li><a href="https://events.static.linuxfound.org/sites/events/files/slides/(OSF_Mr.%20Brian%20Brazil)prometheus-japan-161115062158.pdf">https://events.static.linuxfound.org/sites/events/files/slides/(OSF_Mr.%20Brian%20Brazil)prometheus-japan-161115062158.pdf</a></li>
 	<li><a href="https://prometheus.io/docs/introduction/faq/">https://prometheus.io/docs/introduction/faq/</a></li>
 	<li><a href="https://prometheus.io/docs/instrumenting/exporters/">https://prometheus.io/docs/instrumenting/exporters/</a></li>
 	<li><a href="https://dzone.com/articles/monitoring-with-prometheus">https://dzone.com/articles/monitoring-with-prometheus</a></li>
</ul>
&nbsp;
<h2>APM - Application Performance Monitoring</h2>
Visual Studio is really a profiler/debugger for development and test environments, it was never designed for production usage.

<strong>Tools #9, #10, #11 &amp;12: New Relic, AppDynamics, Compuware APM &amp; Boundary</strong>
<div></div>
<ul>
 	<li>APM tools allow you to target bottlenecks with your application's framework.</li>
 	<li><a href="http://newrelic.com/" target="_blank" rel="noopener noreferrer">New Relic</a> is the reigning market leader – and for good reason. It lets you pinpoints precisely where and when bottlenecks are occurring.</li>
 	<li> <a href="http://www.appdynamics.com/" target="_blank" rel="noopener noreferrer">AppDynamics</a> is also a great tool, enabling you to monitor Java, .NET, PHP, and Node.js applications.</li>
 	<li><a href="http://www.compuware.com/" target="_blank" rel="noopener noreferrer">Compuware APM</a> &amp; <a href="http://www.boundary.com/" target="_blank" rel="noopener noreferrer">Boundary</a> are enterprise-geared APM tools which give you a clear view of the user experience, offering metrics like data transactions performance and user requests.</li>
 	<li dir="ltr"><span class="qlink_container"><a class="external_link" href="https://github.com/Icinga" target="_blank" rel="noopener" data-qt-tooltip="github.com" data-tooltip="attached">Icinga</a></span> - Distributed, high availability monitoring. Most likely the most mature open source APM tool at the moment.</li>
</ul>
<strong>Introducing AppDynamics Lite for .NET</strong>
<ul>
 	<li><a href="http://www.appdynamics.com/products-free-download.php">AppDynamics Lite for .NET</a> – the first completely free .NET application monitoring solution for production. This, in addition to our commercial solution <a href="http://www.appdynamics.com/solutions-dot-net-monitoring.php">AppDynamics Pro for .NET</a>, which has already experienced significant success since its launch in July 2011.</li>
 	<li>All these features are c<strong>ompletely free and will run all day in production 24/7</strong>! AppDynamics <strong>Lite is limited to a single IIS web server</strong>, with AppDynamics Pro becoming the choice for applications that are distributed across multiple IIS web servers and services.</li>
 	<li>Because we wanted to prove that monitoring .NET application performance in production can be simple, thru software that was designed to auto-discover, configure and monitor whats relevant in your .NET application, without you lifting a finger. Our mission at AppDynamics is to deliver maximum monitoring visibility thru minimal effort.</li>
</ul>
<strong>Application Mapping, Business Transaction Monitoring and Diagnostics for Free!</strong>
<ul>
 	<li>Instead of looking at Server metrics, Events and SQL profiles, AppDynamics Lite will automatically discover and visualize your .NET application.</li>
 	<li>Showing all IIS web server interactions (e.g. Web services, databases, LDAP and message queus), business transactions (user requests) and associated performance metrics.</li>
 	<li>End users experience business transactions, with AppDynamics Lite you now have complete business transaction context to monitor and troubleshoot what your end users experience.</li>
 	<li>After drilling down we now see a view showing all bad requests (known as snapshots) that were captured by AppDynamics Lite. Snapshots represent an individual execution of a business transaction that relates to a user. You can see the response time of snapshots shown in the above screenshot differ. This means some user requests were OK, some threw exceptions (red icons) and others stalled (exclamation icons).From the above snapshots view its possible to drill-down on any snapshot to understand its code execution and latency, as well as identifying the actual root cause behind slow performance:
<img src="http://46zwyrvli634e39iq2l9mv8g-wpengine.netdna-ssl.com/wp-content/uploads/2012/05/42.png" /></li>
 	<li>In the above screenshot, AppDynamics Lite provides a view showing the code execution latency (call graph) of application classes and methods that were invoked by the slow snapshot (business transaction). Its worth stating that this visibility is available in production with minimal impact to the application running. Notice that the majority of total response time spent in this “Update Order” business transaction was spent on two ADO.NET calls which took ~3.5 seconds each.</li>
 	<li>From the above view we can see the associated SQL calls by either clicking on the ADO.NET link (next to each call) or by clicking the “SQL Calls” tab to the left of the call graph. Here we see the two SQL statements responsible for the 7.5 second response time. We can now confirm that the root cause of “Update Orders” business transaction taking 7.5 seconds was data access and two offending SQL queries.
<p id="dJyiscj"><img class="alignnone size-full wp-image-1690 " src="/wp-content/uploads/2018/08/img_5b6d46aa5fb7c.png" alt="" /></p>
&nbsp;</li>
 	<li><strong>Pro-Active Alerting for Free!</strong>AppDynamics Lite also has pro-active dashboard and alerting capabilities. This means you can continuously monitor the performance of your application and business transactions in real-time, and be alerted via email when performance deviates from its normal baseline or threshold. For example, below is a screenshot showing a simple dashboard which has been created with four alerts (Overall App Response Time, Overall App Errors/min, Get Product Response Time and Login Response Time). You can see that the Overall App Response Time is breaching its 1 second threshold, in this scenario an alert would be fired to development or operations so they can begin troubleshooting.<img class="alignnone size-full wp-image-1692 " src="/wp-content/uploads/2018/08/img_5b6d46de226a5.png" alt="" /></li>
</ul>
&nbsp;
<h3>References</h3>
<ul>
 	<li>https://www.quora.com/Application-Performance-Management-Is-there-an-open-source-competitor-to-AppDynamics#</li>
 	<li>https://openapm.io/landscape</li>
 	<li>https://www.blazemeter.com/blog/top-ten-monitoring-tools-every-devops-needs</li>
 	<li><a href="https://blog.appdynamics.com/engineering/monitoring-net-applications-just-got-way-better/">https://blog.appdynamics.com/engineering/monitoring-net-applications-just-got-way-better/</a></li>
 	<li><a href="https://opensource.com/article/17/3/inspectit">https://opensource.com/article/17/3/inspectit</a></li>
 	<li>50 tools https://haydenjames.io/50-top-server-monitoring-application-performance-monitoring-apm-solutions/</li>
 	<li>https://dzone.com/articles/monitoring-using-spring-boot-20-prometheus-and-gra</li>
</ul>
