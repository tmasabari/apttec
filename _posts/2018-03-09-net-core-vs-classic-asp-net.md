---
layout: post
title: .NET core vs Classic ASP.NET
date: 2018-03-09 13:11
author: tmasabari
comments: true
categories: [Interview Preparation, Uncategorized]
---
.NET core
<ul>
 	<li>Free and open source</li>
 	<li>Cross platform compatible</li>
 	<li>Ease of access</li>
 	<li>Thin, fast, modular and extensible</li>
</ul>
Componenets
<ul>
 	<li><a title="Entity Framework" href="https://en.wikipedia.org/wiki/Entity_Framework">Entity Framework (EF) Core</a></li>
 	<li>Identity Core</li>
 	<li><a title="ASP.NET MVC" href="https://en.wikipedia.org/wiki/ASP.NET_MVC">MVC</a> Core</li>
 	<li><a title="ASP.NET Razor" href="https://en.wikipedia.org/wiki/ASP.NET_Razor">Razor</a> Core</li>
</ul>
Features
<ul>
 	<li>No-compile developer experience (i.e. compilation is continuous, so that the developer does not have to invoke the compilation command)</li>
 	<li>Modular framework distributed as <a title="NuGet" href="https://en.wikipedia.org/wiki/NuGet">NuGet</a> packages</li>
 	<li>Cloud-optimized runtime (optimised for the internet)</li>
 	<li>Host-agnostic via <a title="Open Web Interface for .NET" href="https://en.wikipedia.org/wiki/Open_Web_Interface_for_.NET">Open Web Interface for .NET</a> (OWIN) support<sup id="cite_ref-3" class="reference"><a href="https://en.wikipedia.org/wiki/ASP.NET_Core#cite_note-3">[3]</a></sup><sup id="cite_ref-4" class="reference"><a href="https://en.wikipedia.org/wiki/ASP.NET_Core#cite_note-4">[4]</a></sup> - runs in <a title="Internet Information Services" href="https://en.wikipedia.org/wiki/Internet_Information_Services">IIS</a> or standalone</li>
 	<li>A unified story for building web UI and web APIs (i.e. both the same)</li>
 	<li>A cloud-ready environment-based configuration system</li>
 	<li>A light-weight and modular HTTP request pipeline</li>
 	<li>Build and run cross-platform ASP.NET Core apps on Windows, Mac, and Linux</li>
 	<li>Open-source and community-focused</li>
</ul>
Originally deemed <b>ASP.NET vNext</b>, the framework was going to be called <b>ASP.NET 5</b> when ready. However, in order to avoid implying it is an update to the existing ASP.NET framework, Microsoft later changed the name to <b>ASP.NET Core</b> at the 1.0 release.<sup id="cite_ref-2" class="reference"><a href="https://en.wikipedia.org/wiki/ASP.NET_Core#cite_note-2">[2</a></sup>
<ul>
 	<li>https://dusted.codes/understanding-aspnet-core-10-aka-aspnet-5-and-why-it-will-replace-classic-aspnet</li>
 	<li>https://www.hanselman.com/blog/ASPNET5IsDeadIntroducingASPNETCore10AndNETCore10.aspx</li>
</ul>
<h4 id="linux-cost-savings"><a href="http://docs.servicestack.net/netcore">Linux Cost Savings</a></h4>
<ol>
 	<li>In addition to the thriving ecosystem and superior automation, another benefit of hosting .NET Core Apps on Linux is the considerable cost savings of hosting on a Linux infrastructure.</li>
 	<li>Docker instances enable isolation with considerably more efficiency than VM’s allowing you to pack them with greater density.</li>
 	<li>For .NET Core Live Demos the single <a href="https://aws.amazon.com/ec2/instance-types/">T2 medium instance</a> (<strong>$25 /month</strong>) is hosting <strong>15 Docker Images</strong> whilst running at <strong>~50% Memory Utilization</strong> and <strong>&lt;1% CPU Utilization</strong> in its current idle state.</li>
</ol>
<table style="width: 435.178px; margin-left: 90px;" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr style="height: 56.8959px;">
<td style="height: 56.8959px; width: 70.9838px;">Model</td>
<td style="height: 56.8959px; width: 34.6875px;">vCPU</td>
<td style="height: 56.8959px; width: 112.465px;">CPU Credits / hour</td>
<td style="height: 56.8959px; width: 86.5394px;">Mem (GiB)</td>
<td style="height: 56.8959px; width: 68.7616px;"> Storage</td>
</tr>
<tr>
<td style="width: 70.9838px;" height="15">t2.medium</td>
<td style="width: 34.6875px;">2</td>
<td style="width: 112.465px;">24</td>
<td style="width: 86.5394px;">4</td>
<td style="width: 68.7616px;">EBS-Only</td>
</tr>
</tbody>
</table>
&nbsp;

&nbsp;

<strong>Death of Microsoft development tools</strong>

https://dusted.codes/understanding-aspnet-core-10-aka-aspnet-5-and-why-it-will-replace-classic-aspnet
<ul>
 	<li>Windows Desktop application development is slowly dying. There is no denial to that.</li>
 	<li>Left is the mobile market and the web. Windows phones and tablets are still <a href="http://www.winbeta.org/news/windows-phone-market-share-drops-1-7-percent">a drop on a hot stone</a> in comparison to the market shares of iOS and Android. This leaves the web as a last resort.</li>
 	<li>After Silverlight's death ASP.NET is the only Microsoft product which competes with other web technologies such as Node, Ruby, Python, Java and more. This is a though battle for ASP.NET, because up until now you had to be a Windows user to be able to develop web applications with ASP.NET.</li>
</ul>
The biggest problem is that the .NET framework and ASP.NET are not cross platform compatible.
<ul>
 	<li>As a web developer you are writing applications which can be understood by any browser, any OS and any device which is connected to the web. There are no limitations, but with ASP.NET you can only develop from a Windows machine.</li>
 	<li>Many of today's biggest internet businesses were born out of small startups. They use free open source technologies such as PHP, Ruby, Python, Java or Node.js.</li>
 	<li>ASP.NET 4.6 developers are missing out on big innovations which are not immediately available on the Windows platform. Over the last years Microsoft was chasing after many innovations by providing its own version to the .NET community, but not always with success (Silverlight, AppFabric Cache, DocumentDb, Windows Phone, etc.). This is not a sustainable model.</li>
 	<li>ASP.NET developers miss out on big innovations such as containers and Docker and don't even realize it, because they know very little to nothing about it. This is a dangerous place to be.</li>
</ul>
ASP.NET 4.6 will be soon remembered as Classic ASP.NET. It will not entirely disappear, just like Classic ASP has never fully disappeared, but new development will likely happen in ASP.NET Core going forward. ASP.NET 4.6 is a dead horse in the long run
