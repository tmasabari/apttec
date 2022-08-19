---
layout: post
title: Network basics & network security - ingress egress
date: 2018-01-07 14:37
author: tmasabari
comments: true
categories: [Hardware, Network, Virtualization]
---
<h3><strong><b>Basics</b></strong></h3>
<h4>Ports</h4>
<ul>
 	<li><a href="https://en.wikipedia.org/wiki/Registered_port">Port ranges</a>
<ul>
 	<li><b>Ports 0–1023</b> – system or <a class="mw-redirect" title="Well-known port" href="https://en.wikipedia.org/wiki/Well-known_port">well-known ports</a></li>
 	<li><b>Ports 1024–49151</b> – user or registered ports</li>
 	<li><b>Ports &gt;49151</b> – dynamic / private ports</li>
</ul>
</li>
 	<li>An <a href="https://en.wikipedia.org/wiki/Ephemeral_port"><b>ephemeral port</b></a> is a short-lived transport protocol <a class="mw-redirect" title="Port number" href="https://en.wikipedia.org/wiki/Port_number">port</a> for <a title="Internet Protocol" href="https://en.wikipedia.org/wiki/Internet_Protocol">Internet Protocol</a> (IP) communications. Ephemeral ports are allocated automatically from a predefined range by the <a class="mw-redirect" title="IP stack" href="https://en.wikipedia.org/wiki/IP_stack">IP stack</a> software.</li>
 	<li>The allocations are<strong> temporary and only valid for the duration of the communication session</strong>. After completion (or timeout) of the communication session, the ports become available for reuse.<sup id="cite_ref-1" class="reference"><a href="https://en.wikipedia.org/wiki/Ephemeral_port#cite_note-1">[note 1]</a></sup> Since the ports are used on a per request basis they are also called <b>dynamic ports</b>.</li>
 	<li>The <a title="Internet Assigned Numbers Authority" href="https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority">Internet Assigned Numbers Authority</a> (IANA) suggests the range 49152 to 65535 (2<sup>15</sup>+2<sup>14</sup> to 2<sup>16</sup>−1) for dynamic or private ports.<sup id="cite_ref-2" class="reference"><a href="https://en.wikipedia.org/wiki/Ephemeral_port#cite_note-2">[1]</a></sup></li>
 	<li>Many <a title="Linux kernel" href="https://en.wikipedia.org/wiki/Linux_kernel">Linux kernels</a> use the port range 32768 to 61000. MS OSes through XP use the range 1025–5000 as ephemeral ports by default.<sup id="cite_ref-6" class="reference"><a href="https://en.wikipedia.org/wiki/Ephemeral_port#cite_note-6">[4]</a></sup> <a title="Windows Vista" href="https://en.wikipedia.org/wiki/Windows_Vista">Windows Vista</a>, <a title="Windows 7" href="https://en.wikipedia.org/wiki/Windows_7">Windows 7</a>, and <a class="mw-redirect" title="Server 2008" href="https://en.wikipedia.org/wiki/Server_2008">Server 2008</a> use the IANA range by default.</li>
</ul>
<strong><b>Public (external) IP addresses</b></strong>
<ul>
 	<li>ISP <em><i>(Internet Service Provider) </i></em>provides <strong>unique</strong> public IP to identify resource<strong> in WWW</strong>.</li>
 	<li>IP address that never changes (a <em><i>fixed</i></em>, or <em><i>static</i></em>IP address).</li>
 	<li>an IP address that can change from time to time (a <em><i>dynamic</i></em> IP address).
<ul>
 	<li>For a dynamic IP address, you specify <em><i>DHCP </i></em>in your router's network settings. <strong><em><i>DHCP </i></em>is <em><i>Dynamic Host Control Protocol</i></em></strong>. It tells your router to accept whatever public IP address your ISP issues and gives private ip address to local resources</li>
</ul>
</li>
</ul>
<strong><b>Private (internal) IP addresses</b></strong>
<ul>
 	<li>most of the hosts on the organization's intranet require a specific set of Internet services, such as the World Wide Web access and e-mail, typically access the Internet services through <strong>Application layer gateways such as proxy servers, e-mail servers and routers, firewalls, translators</strong>. (Application layer gateways only need puplic ip)</li>
 	<li> the Internet designers reserved a portion of the IP address space and named this space the <em><i>private address space</i></em>. <u>An IP address in the private address space is never assigned as a public address. </u></li>
 	<li><strong>your router issues private (or <em><i>internal</i></em>) IP addresses to each network device inside your network</strong>.</li>
 	<li>Internet traffic from a host that has a private address must either send its requests to an <strong><b>Application layer gateway (such as a proxy server)</b></strong>, which has a valid public address, or have its private address translated into a valid public address by a <strong><b>network address translator (NAT) </b></strong>before it is sent on the Internet.</li>
 	<li>The private address space specified in RFC 1918 is defined by the following three address blocks:
<ul>
 	<li><strong>10.0.0/8</strong>
The 10.0.0.0/8 private network is a <strong>class A network ID</strong> that allows the following range of valid IP addresses: <strong>10.0.0.1 to 10.255.255.254</strong>. The 10.0.0.0/8 private network has <strong>24 host bits</strong> that can be used for any subnetting scheme within the private organization.</li>
 	<li><strong>16.0.0/12</strong>
The 172.16.0.0/12 private network can be interpreted either as a <strong>block of 16 class B network IDs or as a 20-bit assignable address space (20 host bits)</strong> that can be used for any subnetting scheme within the private organization. The 172.16.0.0/12 private network allows the following range of valid IP addresses: 172.16.0.1 to 172.31.255.254.</li>
 	<li><strong>168.0.0/16</strong>
The 192.168.0.0/16 private network can be interpreted either as a block of 256 class C network IDs or as a 16-bit assignable address space (16 host bits) that can be used for any subnetting scheme within the private organization. The 192.168.0.0/16 private network allows the following range of valid IP addresses: 192.168.0.1 to 192.168.255.254.</li>
</ul>
</li>
</ul>
<ul>
 	<li>Similar to the arrangement with public IP addresses, each device on your network has its network configuration settings on <em><i>DHCP</i></em>, so it can accept the unique private IP address that your router issues it.</li>
 	<li>These <strong>private IP addresses never leave your network</strong>, just as your <strong>public IP address is never used inside your network</strong>. The router controls all the network traffic, both within your home network and outside of it, to the Internet. It is the router's job to make sure that data flows to and from all the correct places.</li>
</ul>
<strong><b>Illegal Addresses</b></strong>
<ul>
 	<li>Private intranets that have no intent on connecting to the Internet can choose any addresses they want, even public addresses that have been assigned by the InterNIC to others.</li>
 	<li>Connectivity from illegal addresses to Internet locations is not possible.</li>
</ul>
<strong>Netmask </strong>IP Calculator <a href="http://jodies.de/ipcalc"><u>http://jodies.de/ipcalc</u></a>

A commonly used netmask is a 24-bit netmask, as seen below.
<table style="margin-left: 30px; width: 521.171px;">
<tbody>
<tr>
<td style="width: 182px;"><strong><b>Netmask:</b></strong></td>
<td style="width: 129px;"><strong><b>255.</b></strong></td>
<td style="width: 129px;"><strong><b>255.</b></strong></td>
<td style="width: 130px;"><strong><b>255.</b></strong></td>
<td style="width: 145.171px;"><strong><b>0</b></strong></td>
</tr>
<tr>
<td style="width: 182px;">Binary:</td>
<td style="width: 129px;">11111111</td>
<td style="width: 129px;">11111111</td>
<td style="width: 130px;">11111111</td>
<td style="width: 145.171px;">00000000</td>
</tr>
<tr>
<td style="width: 182px;">Netmask length</td>
<td style="width: 129px;">8</td>
<td style="width: 129px;">16</td>
<td style="width: 130px;">24</td>
<td style="width: 145.171px;">--</td>
</tr>
</tbody>
</table>
Using a 24-bit netmask, the network would be capable of 2,097,150 networks or 254 different hosts with an IP range of 192.0.1.x to 223.255.254.x, which is usually more than enough addresses for one network.

&nbsp;

A simple formula can be used to determine the capable amount of networks a netmask can support.

2^<sup>(netmask length - # of used segments)</sup> - 2

Below is a breakdown of each of the commonly used network classes.
<table>
<tbody>
<tr>
<td width="77"><strong><b>Class</b></strong></td>
<td width="135"><strong><b>Netmask length</b></strong></td>
<td width="124"><strong><b># of networks</b></strong></td>
<td width="99"><strong><b># of hosts</b></strong></td>
<td width="130"><strong><b>Netmask</b></strong></td>
</tr>
<tr>
<td width="77"><strong><b>Class A</b></strong></td>
<td width="135">8</td>
<td width="124">126</td>
<td width="99">16,777,214</td>
<td width="130">255.0.0.0</td>
</tr>
<tr>
<td width="77"><strong><b>Class B</b></strong></td>
<td width="135">16</td>
<td width="124">16,382</td>
<td width="99">65,534</td>
<td width="130">255.255.0.0</td>
</tr>
<tr>
<td width="77"><strong><b>Class C</b></strong></td>
<td width="135">24</td>
<td width="124">2,097,150</td>
<td width="99">254</td>
<td width="130">255.255.255.0</td>
</tr>
</tbody>
</table>
&nbsp;
<h3><a href="http://akashbhunchal.blogspot.in/2014/07/difference-between-nat-vs-proxy-vs.html">Gateway / Router Vs Proxy Vs NAT</a></h3>
<p id="RgnoXIE"><img class="wp-image-1247 alignright" style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5ab36922848c8.png" alt="" width="296" height="342" /><img class="alignnone wp-image-1248 " src="/wp-content/uploads/2018/03/img_5ab3694c0a007.png" alt="" width="455" height="109" /></p>
<p id="RgnoXIE"><img class="alignnone wp-image-1249 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5ab3695d50e28.png" alt="" width="465" height="199" /><img class="wp-image-1250 alignnone" style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5ab3699ba9d82.png" alt="" width="464" height="112" /></p>
<a href="https://serverfault.com/questions/262071/whats-the-difference-between-a-gateway-and-a-router"><strong><b>Router/Gateway</b></strong></a>
<ul>
 	<li>A router and a gateway are essentially the same. and just <strong><b>acts as a relay for datagram packets.</b></strong> All it knows is where to send the packet. It <strong><b>does not modify the packets and does not require the response to come back through </b></strong>it.   Router <strong>is Network layer (TCP) protocol unaware</strong>.</li>
 	<li><strong>A gateway need not be doing NAT</strong>
<ul>
 	<li>typically a <strong>home network</strong> will have a default gateway that is a router connected to ADSL, that type of device will <strong>do NAT</strong>,</li>
 	<li>whereas the <strong>default gateway on your subnet</strong> at work will just lead to the wider office LAN and will <strong>not do NAT</strong>.</li>
</ul>
</li>
</ul>
<strong>NAT (Network Address Translator)</strong>
<ul>
 	<li><strong><b>NAT is nothing but an intelligent router.</b></strong>What NAT does is hide the machines behind it from the internet. All the machines go through NAT to access the outside world.</li>
 	<li>The <strong>machine A still thinks</strong> that it is talking to machine B <strong>directly</strong> (10.0.0.1:1234 - 11.0.0.1:4567).</li>
 	<li>What the NAT does is replace the Source:Port Header of the packet it received from A with its own IP (w.x.y.z) and its own random port (7897). When the NAT had received the packet from A it had assigned it a random port (7897) and kept that in a table called <strong>NAT table</strong>.</li>
 	<li>When the packet reaches <strong>machine B it thinks it came from the NAT IP</strong>. Since a response is always to the source (NAT), machine B tries to send the response packet back to the NAT at the same port as was overridden in the header(7897).</li>
 	<li>So when the response comes back from Machine B NAT just <strong>does a reverse look up</strong> in the same table and forwards it to the desired recipient (Machine A). This way more than one machines can access the internet through NAT.</li>
 	<li>One important point to note here is that at <strong>each layer of OSI model there is a checksum</strong> to determine if the packet/segment is valid. The same applies here. If the NAT changes the source IP:PORT combination, <strong>it need to recalculate the checksum again both at the Transport as well as Network layer</strong>. This leads to some additional work for the NAT.</li>
</ul>
<strong><b>Proxy / Load balancers:</b></strong>
<ul>
 	<li>A proxy works at the <strong><b>Transport layer and is aware of the protocol</b></strong>. Its <strong>not transparent</strong> in nature. It actually creates two connections one each with source and destination. <strong><b>Machine A does not even know about machine B. For machine A Proxy is the only thing its talking to and does not care how and where the proxy gets its data.</b></strong></li>
 	<li>In the above picture Server A does not even know the IP of Server B. All it knows is the IP and port of the proxy server. The proxy server creates two connections, one with Server A and one with Server B. This happens at the Transport layer. Similarly server B does not even know the IP of server A, for it Proxy is the Source.</li>
 	<li><strong>Examples</strong> of proxy servers are <strong>load balancers</strong> like HAProxy, Nginx, Apache, AWS ELB, F5 BIG-IP. They hide the backend from the outside world and do lot of nifty stuff like load balancing. optimization, etc.</li>
</ul>
Ingress &amp; Egress

<a href="https://paulmoore.livejournal.com/2128.html">Linux</a>
<ul>
 	<li>The new ingress/egress controls are fairly simple: <strong>each packet entering the system must pass an ingress access control</strong> and each packet leaving the system must pass an egress access control. Forwarded packets must also pass an additional forwarding access control</li>
</ul>
<h3><a href="https://en.wikipedia.org/wiki/Egress_filtering">Egress filtering</a></h3>
In <a class="mw-redirect" title="Computer networking" href="https://en.wikipedia.org/wiki/Computer_networking">computer networking</a>, <b>egress filtering</b> is the practice of <strong>monitoring and potentially restricting the flow of information outbound from one network to another.</strong> Typically it is information from a private <a class="mw-redirect" title="TCP/IP" href="https://en.wikipedia.org/wiki/TCP/IP">TCP/IP</a> computer network to the <a title="Internet" href="https://en.wikipedia.org/wiki/Internet">Internet</a> that is controlled.

TCP/IP packets that are being sent out of the internal network are examined via a <a title="Router (computing)" href="https://en.wikipedia.org/wiki/Router_(computing)">router</a>, <a title="Firewall (computing)" href="https://en.wikipedia.org/wiki/Firewall_(computing)">firewall</a>, or similar <a title="Edge device" href="https://en.wikipedia.org/wiki/Edge_device">edge device</a>. Packets that do not meet security policies are not allowed to leave - they are denied "egress".<sup id="cite_ref-1" class="reference"><a href="https://en.wikipedia.org/wiki/Egress_filtering#cite_note-1">[1]</a></sup>

Egress filtering helps ensure that unauthorized or malicious traffic never leaves the internal network.

In a<strong> corporate network,</strong> typical recommendations are that all traffic except that emerging from a select set of <a title="Server (computing)" href="https://en.wikipedia.org/wiki/Server_(computing)">servers</a> would be denied egress.<sup id="cite_ref-2" class="reference"><a href="https://en.wikipedia.org/wiki/Egress_filtering#cite_note-2">[2]</a></sup><sup id="cite_ref-3" class="reference"><a href="https://en.wikipedia.org/wiki/Egress_filtering#cite_note-3">[3]</a></sup><sup id="cite_ref-4" class="reference"><a href="https://en.wikipedia.org/wiki/Egress_filtering#cite_note-4">[4]</a></sup><sup id="cite_ref-5" class="reference"><a href="https://en.wikipedia.org/wiki/Egress_filtering#cite_note-5">[5]</a></sup>Restrictions can further be made such that <strong>only select protocols such as <a class="mw-redirect" title="HTTP" href="https://en.wikipedia.org/wiki/HTTP">HTTP</a>, <a title="Email" href="https://en.wikipedia.org/wiki/Email">email</a>, and <a title="Domain Name System" href="https://en.wikipedia.org/wiki/Domain_Name_System">DNS</a> are allowed.</strong> User <a class="mw-redirect" title="Workstations" href="https://en.wikipedia.org/wiki/Workstations">workstations</a> would then need to be <strong>configured either manually or via <a title="Proxy auto-config" href="https://en.wikipedia.org/wiki/Proxy_auto-config">proxy auto-config</a> to use one of the allowed servers as a <a title="Proxy server" href="https://en.wikipedia.org/wiki/Proxy_server">proxy</a>.</strong>
<h2>VPN</h2>
A virtual private network (VPN) provides a means for securely communicating among remote computers across a public WAN such as the Internet.

<a href="http://searchnetworking.techtarget.com/definition/virtual-private-network">Virtual Private Networks (VPNs)</a> have now become the de facto standard to provide a company’s partners or employees with remote access to corporate resources in a secure manner.

VPN refers to the family of technologies that facilitate remote access to corporate resources. The primary users of this technology are company employees who want to access resources at work from their homes or other public places, and corporate partners/third parties who support various systems within the corporate infrastructure. VPNs typically leverage public long-haul IP networks to transmit data by creating an encrypted channel between the remote site, which could be an employee’s laptop or a third-party system, and the corporate network.

At present, the two most <a href="http://searchsecurity.techtarget.com/buyersguide/The-best-SSL-VPN-products-for-you-A-buyers-guide">popular VPN technologies</a> are the traditional <a href="http://searchmidmarketsecurity.techtarget.com/definition/IPsec">Internet Protocol Security</a> (IPsec)-based VPNs, which function primarily at the <strong>network layer</strong>, and Secure Sockets Layer (SSL) VPNs, which function primarily at the <strong>application layer</strong>.
<h3 id="ipsec-vpn-overview" class="Title">IPsec VPN Overview</h3>
<ul>
 	<li>A VPN connection can link two LANs (<strong>site-to-site VPN</strong>) or a remote dial-up user and a LAN. The traffic that flows between these two points passes through shared resources such as routers, switches, and other network equipment that make up the public WAN.</li>
 	<li>To secure VPN communication while passing through the WAN, the two participants create an IP Security (IPsec) tunnel.</li>
 	<li>IPsec is a suite of related protocols for cryptographically securing communications at the IP Packet Layer.</li>
 	<li>The protocol is designed to work further down the network stack (layer 3) and can be used to transmit any IP-based protocol, irrespective of the application generating the traffic.
<ul>
 	<li>With the advent of the mobile work force, IPsec has been extended to support remote access through the use of a dedicated VPN application (client) installed on the users' mobile assets.</li>
 	<li>Any IP-based protocol could be tunneled through it. This makes IPsec an attractive alternative to an expensive leased line or a dedicated circuit.</li>
 	<li>it provides authentication, authorization and encryption, while basically extending the corporate network to any remote user</li>
</ul>
</li>
 	<li>It could also serve as a backup link in the event that the primary leased line or dedicated circuit connecting the remote site to the central office goes down.</li>
 	<li>IPsec's application-agnostic design is also its weakness, however.
<ul>
 	<li>it does not have the ability to restrict access to resources at a granular level. Once a tunnel is set up, remote users can typically access any corporate resource as if they were plugged directly into the corporate network.</li>
 	<li>there is no guarantee that these devices comply with the level of security that is typically enforced on managed assets.</li>
 	<li>corporations use <strong><a href="http://searchenterprisewan.techtarget.com/definition/Network-Address-Translation">Network Address Translation</a></strong> (NAT)-special configuration is required to ensure IPsec plays nicely with the NAT setup.</li>
</ul>
</li>
 	<li>IPsec should be leveraged in situations where an always-on connection to remote office locations or partners/vendors is required. In these instances, granular access control limitations and missing host-check capabilities should be augmented with a <a href="http://searchnetworking.techtarget.com/definition/network-access-control">Network Access Control</a> (NAC) system, which can ensure only approved remote hosts are allowed to connect to the enterprise.</li>
</ul>
<h3><a href="http://searchsecurity.techtarget.com/definition/SSL-VPN">SSL VPN</a></h3>
<ul>
 	<li><a href="http://searchsecurity.techtarget.com/definition/SSL-VPN">SSL VPNs</a>, on the other hand, were designed with the mobile workforce in mind. The intended goal was to provide a seamless, clientless method for remote access.</li>
 	<li>An SSL VPN can be thought of as an<strong> application proxy</strong>, providing granular access to specific corporate resources that a remote user can access using his or her browser without the need to install a client.
<ul>
 	<li>They do not require any special software to be installed.</li>
 	<li>Specific authentication and authorization schemes for access to an application can be limited to a particular user population.</li>
 	<li>Built-in logging and auditing capabilities address various compliance requirements.</li>
 	<li>SSL VPNs also have the ability to run host compliance checks on the remote assets connecting to the enterprise to validate they are configured with the appropriate security software and have the latest patches installed.</li>
</ul>
</li>
 	<li>Disadvantages
<ul>
 	<li>If a remote site requires an always-on link to the main office, SSL VPN would not be the solution.</li>
 	<li>IPsec, being application agnostic, can support a number of legacy protocols and traditional client/server applications with minimal effort.
<ul>
 	<li>This is not the case with SSL VPNs, which have been built around Web-based applications.</li>
 	<li>Many SSL VPNs get around this weakness by installing a Java or ActiveX-based agent on the remote asset - both ActiveX and Java come with their own security weaknesses that attackers commonly seek to exploit</li>
</ul>
</li>
</ul>
</li>
</ul>
<h2>References</h2>
<ul>
 	<li>http://support.slingbox.com/KB/KB-2000143</li>
 	<li>https://technet.microsoft.com/en-us/library/cc958825.aspx</li>
 	<li>https://www.juniper.net/documentation/en_US/junos/topics/concept/vpn-security-overview.html</li>
 	<li>http://searchsecurity.techtarget.com/tip/IPSec-VPN-vs-SSL-VPN-Comparing-respective-VPN-security-risks</li>
</ul>
