---
layout: post
title: DMZ & N Tier Architecture Security
date: 2018-04-16 09:36
author: tmasabari
comments: true
categories: [Architecture, Hardware, Network, Security]
---
<h2 id="page-title" class="title"><a href="https://securitycommunity.tcs.com/infosecsoapbox/articles/2017/12/05/dmz-your-internet-facing-application-protect-cyber-security-threats">DMZ </a>/ Landing Zone / Perimeter network</h2>
<ul>
 	<li>
<p class="rtejustify">In computer networks, a DMZ (demilitarized zone) is a physical or logical sub-network that separates an internal local area network (LAN) from other untrusted networks, usually the Internet. A DMZ is a <a href="https://searchsecurity.techtarget.com/definition/DMZ">protected middle ground network</a> where you can deploy servers that offer services to the public.</p>

<ul>
 	<li><a href="https://securitycommunity.tcs.com/infosecsoapbox/articles/2017/12/05/dmz-your-internet-facing-application-protect-cyber-security-threats"><img class="alignnone  wp-image-1476 " src="/wp-content/uploads/2018/04/img_5ad39e6e4840c.png" alt="" width="531" height="228" /></a></li>
</ul>
</li>
 	<li>The term DMZ comes from the geographic buffer zone that was set up between North Korea and South Korea at the end of the Korean War. A DMZ is now often referred to as a <a href="https://searchnetworking.techtarget.com/definition/network-perimeter">perimeter network</a>.</li>
 	<li>
<p class="rtejustify">External-facing servers, resources and services are located in the DMZ so they are accessible from the Internet but the rest of the internal <a href="https://searchnetworking.techtarget.com/definition/local-area-network-LAN">LAN</a> remains unreachable.</p>
</li>
 	<li>
<p class="rtejustify">This provides an additional layer of security to the LAN as it restricts the ability of hackers to directly access internal servers and data via the Internet.</p>
</li>
 	<li>We create DMZ to separate outside world (internet) facing services from internal network, so when (<strong>because it really is WHEN, not IF</strong>) they got compromised, attacker can't move easily to exploit local network.</li>
 	<li>A general use case is that the application server has a public face, it can be remotely rooted. If that happens, and a malicious party gains access to your server, he should be isolated in the DMZ network and not have direct access to the private hosts</li>
 	<li>The systems running these services in the DMZ are reachable by <a href="https://searchsecurity.techtarget.com/definition/hacker">hackers</a>and cybercriminals around the world and need to be hardened to withstand constant attack.</li>
 	<li>Any service that is being provided to users on the external network can be placed in the DMZ. The most common of these services are:
<ul>
 	<li><a class="mw-redirect" title="Web servers" href="https://en.wikipedia.org/wiki/Web_servers">Web servers</a></li>
 	<li><a class="mw-redirect" title="Mail servers" href="https://en.wikipedia.org/wiki/Mail_servers">Mail servers</a></li>
 	<li><a class="mw-redirect" title="FTP servers" href="https://en.wikipedia.org/wiki/FTP_servers">FTP servers</a></li>
 	<li><a class="mw-redirect" title="VoIP" href="https://en.wikipedia.org/wiki/VoIP">VoIP</a> servers</li>
</ul>
</li>
 	<li>There are various ways to design a network with a DMZ. The two most common methods are with a single or dual <a href="https://searchsecurity.techtarget.com/definition/firewall">firewalls</a>.</li>
 	<li>A more secure approach is to use two firewalls to create a DMZ. The first firewall also called the perimeter firewall is configured to allow traffic destined to the DMZ only. The second or internal firewall only allows traffic from the DMZ to the internal network.</li>
 	<li>This is considered more secure since two devices would need to be compromised before an attacker could access the internal LAN. As a DMZ segments a network, security controls can be tuned specifically for each segment.</li>
 	<li>For example a <a href="https://searchsecurity.techtarget.com/tutorial/Intrusion-detection-and-prevention-learning-guide">network intrusion detection and prevention system</a> located in a DMZ that only contains as Web server can block all traffic except HTTP and HTTPS requests on ports 80 and 443.</li>
 	<li>Setting up a DMZ is very easy. If you have multiple computers, you can choose to simply place one of the computers between the Internet connection and the firewall. Most of the software firewalls available will allow you to designate a directory on the gateway computer as a DMZ.</li>
 	<li>Application proxy servers which accept traffic initiated from the Internet and heading inbound are usually placed in a DMZ. The assumption is that a connection initiated by an attacker could somehow breach the software on the proxy - a buffer overflow, for example - and that once that happens the attacker can use the proxy as a hopping-off point. Such a proxy is kept in the DMZ to limit the damage a successful breach of that first layer can cause.</li>
 	<li>A function that is often combined with a firewall is a <b>proxy server</b>. The proxy server is used to access <a href="https://computer.howstuffworks.com/web-page.htm">Web pages</a> by the other computers. When another computer requests a Web page, it is retrieved by the proxy server and then sent to the requesting computer. The net effect of this action is that the remote computer hosting the Web page never comes into direct contact with anything on your home network, other than the proxy server.

Proxy servers can also make your Internet access work more efficiently. If you access a page on a Web site, it is <b>cached</b> (stored) on the proxy server. This means that the next time you go back to that page, it normally doesn't have to load again from the Web site. Instead it loads instantaneously from the proxy server.
<div class="row recirc-panel">

There are times that you may want remote users to have access to items on your network. Some examples are:
<div class="str-body-list">
<ul>
 	<li>Web site</li>
 	<li>Online business</li>
 	<li>FTP download and upload area</li>
</ul>
</div>
</div>
&nbsp;</li>
 	<li>The F5 <a href="https://f5.com/products/big-ip">BIG-IP system</a> is a full proxy that can be deployed to provide basic and advanced application network services, including <a href="https://f5.com/products/application-delivery">load balancing</a>, <a href="https://f5.com/solutions/enterprise/reference-architectures/acceleration">web performance optimization</a>, <a href="https://f5.com/products/security">application delivery firewall</a> and <a href="https://f5.com/products/security">secure remote access</a>.
<p id="csyAYTX"><img class="wp-image-1554  aligncenter" src="/wp-content/uploads/2018/06/img_5b1f6b85dd614.png" alt="" width="542" height="220" /></p>
</li>
 	<li><a href="https://security.stackexchange.com/questions/153958/proxy-between-web-server-in-dmz-and-soap-service-in-internal-network">Every configuration where you allow connections from DMZ to internal network is bad and should be avoided.</a> You can create second, restricted DMZ for SOAP-service and configure port forwarding only for traffic comming from your web service in DMZ and internal network. This way SOAP-service is protected in the same way as when it's in internal network, but in addition, when compromised, you don't open internal network to attacker.</li>
 	<li class="rtejustify">The DMZ must be separated from the rest of the network both in terms of IP routing and security policy.</li>
 	<li class="rtejustify">Identify your network areas. Internal: critical systems; DMZ: systems you can afford to be "exposed", systems you want to host services to the outside world, e.g. your SSH hosts; External: the rest of the world.</li>
 	<li class="rtejustify">Set up these separate areas on your network architecture.</li>
 	<li class="rtejustify">Firewalls/routers are then configured to allow direct connections from the outside world only to the DMZ. Correspondingly, your internal systems should be able to connect only to the DMZ and access the outside world via HTTP, application proxies, mail relays etc. there. Your firewall rules should reflect these decisions by blocking the corresponding traffic directions/IPs/ports: e.g. inward allow only ports for services operating in the DMZ etc.</li>
 	<li class="rtejustify">Ideally any services exchanging information between network areas (internal, DMZ, external) must be configured to be initiated FROM the most secure network segment TO the less secure areas, e.g. If you need to transfer files to "inside" hosts have the inside systems initiate the transfer (have the client role, rather than the server role).</li>
 	<li class="rtejustify">Internet services should be placed in the DMZ. The most common of these services are: <span style="background-color: #ff9900;">Web, Mail, DNS, FTP, and VoIP</span>. The systems running these services in the DMZ are reachable by hackers and cybercriminals around the world and need to be hardened to withstand constant attack.</li>
 	<li class="rtejustify">SSL termination &amp; handshaking must be configured at DMZ. DMZ must contain systems to detect &amp; isolate attacks e.g. Web Application Firewalls.</li>
 	<li>There are various ways to design a network with a DMZ. The two most common methods are with a<strong> single or dual firewalls</strong>.
<ul>
 	<li>A more secure approach is to use<strong> two firewalls</strong> to create a DMZ. The first firewall also called the perimeter firewall is configured to allow traffic destined to the DMZ only. The second or internal firewall only allows traffic from the DMZ to the internal network. This is considered more secure since two devices would need to be compromised before an attacker could access the internal LAN. As a DMZ segments a network, security controls can be tuned specifically for each segment. For example a network intrusion detection and prevention system located in a DMZ that only contains as Web server can block all traffic except HTTP and HTTPS requests on ports 80 and 443.</li>
</ul>
</li>
</ul>
<h2>Inputs</h2>
<ul>
 	<li>The factory shop floor (assembly line) – did the parts arrive or not</li>
 	<li>3<sup>rd</sup> party parts supplier companies – were the parts produced</li>
 	<li>Logistics warehouses – did the parts leave/arrive at the warehouse</li>
 	<li>Trucks on the road – where are they, carrying which parts</li>
 	<li>Logistics “control room” – where is everyone and everything</li>
 	<li>Factory production forward planning area – which parts do we need, by when, to achieve optimized production cycles</li>
</ul>
<h3>Business Logic Tier</h3>
<ul>
 	<li>The business logic tier would be constituted by several tiers of application server clusters</li>
 	<li>distributed by multiple data centers in separate geographies</li>
 	<li>with a production layer running on one server and</li>
 	<li>a quality/tests layer running on another server in each data center.</li>
</ul>
<h3>Data Tier</h3>
<ul>
 	<li>The data tier would consist of an active database server cluster with multiple nodes (servers)<span style="background-color: #ff9900;"> - High Availability</span></li>
 	<li>each running its layer distributed by two data centers in separate geographies<span style="background-color: #ff9900;"> - Distritbuted</span></li>
 	<li>plus a historic data/ quick recovery tier at yet another distinct geographic location.<span style="background-color: #ff9900;"> - Disaster recovery</span></li>
</ul>
&nbsp;
<p id="zQuMWgi"><img class="alignnone size-full wp-image-1475 " src="/wp-content/uploads/2018/04/img_5ad39884b3595.png" alt="" /></p>
&nbsp;
<h1>References</h1>
<ul>
 	<li>
<p class="rtejustify">https://en.wikipedia.org/wiki/DMZ_(computing)</p>
</li>
 	<li><a href="https://searchsecurity.techtarget.com/definition/DMZ">https://searchsecurity.techtarget.com/definition/DMZ</a></li>
 	<li><a href="https://computer.howstuffworks.com/firewall4.htm">https://computer.howstuffworks.com/firewall4.htm</a></li>
 	<li><a href="https://security.stackexchange.com/questions/3667/what-is-the-real-function-and-use-of-a-dmz-on-a-network">https://security.stackexchange.com/questions/3667/what-is-the-real-function-and-use-of-a-dmz-on-a-network</a></li>
 	<li><a href="https://securitycommunity.tcs.com/infosecsoapbox/articles/2017/12/05/dmz-your-internet-facing-application-protect-cyber-security-threats">https://securitycommunity.tcs.com/infosecsoapbox/articles/2017/12/05/dmz-your-internet-facing-application-protect-cyber-security-threats</a></li>
 	<li><a href="https://stackoverflow.com/questions/224664/difference-between-proxy-server-and-reverse-proxy-server">https://stackoverflow.com/questions/224664/difference-between-proxy-server-and-reverse-proxy-server</a></li>
 	<li><a href="http://smallbusiness.chron.com/difference-between-dmz-server-reverse-proxy-71583.html">http://smallbusiness.chron.com/difference-between-dmz-server-reverse-proxy-71583.html</a></li>
 	<li><a href="https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/">https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer/</a></li>
 	<li><a href="https://support.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-4-0/21.html">https://support.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-4-0/21.html</a></li>
 	<li><a href="https://f5.com/glossary/reverse-proxy">https://f5.com/glossary/reverse-proxy</a></li>
</ul>
