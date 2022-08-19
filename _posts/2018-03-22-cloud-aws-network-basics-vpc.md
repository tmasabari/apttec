---
layout: post
title: Network & Security - Cloud, AWS & VPC
date: 2018-03-22 15:31
author: tmasabari
comments: true
categories: [AWS, Cloud, Hardware, Network, Virtualization]
---
<h3><a href="http://www.cloudcomputingpatterns.org/virtual_networking/">Cloud Virtual Networking</a></h3>
<ul>
 	<li>Application components deployed on <a href="http://www.cloudcomputingpatterns.org/elastic_infrastructure/">Elastic Infrastructures</a> and <a href="http://www.cloudcomputingpatterns.org/elastic_platform/">Elastic Platforms</a> rely on physical network hardware to communicate with each other and the outside world. On this networking layer, <strong>different customers shall be isolated from each</strong>.</li>
 	<li>Physical networking resources, such as networking interface cards, switches, routers etc. are abstracted to virtualized ones. These Virtual Networking resources may share the same physical networking resources.</li>
 	<li>Configuration is handled by customers through self-service interfaces.</li>
 	<li>
<p id="ALXKoiZ"><img class="alignnone wp-image-932 " src="/wp-content/uploads/2018/03/img_5aa8c2c3e1f56.png" alt="" width="227" height="156" /></p>
</li>
</ul>
<h2><a href="https://stackoverflow.com/questions/38690012/aws-vpc-internet-gateway-vs-nat">AWS - Networking</a></h2>
<a href="https://aws.amazon.com/vpc/faqs/?sc_channel=PS&amp;sc_campaign=acquisition_IN&amp;sc_publisher=google&amp;sc_medium=vpc_b&amp;sc_content=sitelink&amp;sc_detail=aws%20vpc&amp;sc_category=vpc&amp;sc_segment=vpc_faqs&amp;sc_matchtype=e&amp;sc_country=IN&amp;s_kwcid=AL!4422!3!208384572667!e!!g!!aws%20vpc&amp;ef_id=WgMqYgAAAH6AP3CP:20180322064613:s"><b>What are the components of Amazon VPC?</b></a>

<img class="wp-image-1049 alignright" src="/wp-content/uploads/2018/03/img_5aad2823b51ef.png" alt="" width="435" height="125" />
<ul>
 	<li><b>A Virtual Private Cloud: </b>A <strong>logically isolated virtual network</strong> in the AWS cloud. You define a <strong>VPC’s IP address space</strong> from ranges you select.</li>
 	<li>
<p id="LNJueGX"><img class=" wp-image-1444 alignright" src="/wp-content/uploads/2018/04/img_5ac6b4a77b465.png" alt="" width="223" height="317" /></p>
VPC is equivalent to country.
<ul>
 	<li>it has a name</li>
 	<li>it's <strong>associated with a region.</strong> A VPC s<strong>pans all the Availa</strong><strong>bility Zones</strong> in the region. Every region has default VPC created.</li>
 	<li>all the resources can interact with each other freely. resources outside of the VPC need special permissions to access resources</li>
</ul>
</li>
 	<li>Subnet are equivalent to state
<ul>
 	<li><b>Subnet:</b> A <strong>segment of a VPC’s IP address range</strong> where you can place groups of isolated resources.</li>
 	<li>subnet range maximum - 16, minimum - 28 (4 bits)</li>
 	<li>use different set of rules (taxes, driving licenses, language etc) for communication (firewall, security group, ACL, route table rules and flow logs)</li>
 	<li>associated with a <strong>particular availability zone.</strong> <strong>Cannot  span across AZs</strong>.</li>
 	<li>In a 3 tier architecture, web servers are in public network, application subnets</li>
</ul>
</li>
 	<li>If you <strong>attach a Internet gateway to private subnet, it becomes a public subnet</strong>. A <strong>private subnet</strong> will not have IGW hence they <strong>use Bastion and NAT</strong> to connect to internet.</li>
 	<li>If a subnet <strong>doesn't</strong> have a route to the <strong>internet gateway</strong>, but has its traffic <strong>routed to a virtual private gateway</strong> for a VPN connection, the subnet is known as a <strong><em>VPN-only subnet</em></strong>.</li>
 	<li>When you create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a <strong>Classless Inter-Domain Routing (CIDR) block</strong>; for example, <code class="code">10.0.0.0/16</code>. This is the primary CIDR block for your VPC.</li>
 	<li>After creating a VPC, you can add one or more subnets in each Availability Zone. When you create a subnet, you specify the <strong>CIDR block for the subnet, which is a subset of the VPC CIDR block</strong>. Each subnet must reside entirely within one Availability Zone and cannot span zones.
<ul>
 	<li>We assign a unique ID to each subnet.</li>
</ul>
</li>
</ul>
<table>
<tbody>
<tr style="height: 27px;">
<td style="height: 27px; width: 395px;">Private</td>
<td style="height: 27px; width: 337px;">Public</td>
</tr>
<tr style="height: 5px;">
<td style="height: 5px; width: 395px;">means the instances are not publicly accessible from the internet.</td>
<td style="height: 5px; width: 337px;"> means a subnet that has internet traffic routed through AWS's Internet Gateway</td>
</tr>
<tr style="height: 7px;">
<td style="height: 7px; width: 395px;">Do NOT have a public IP address</td>
<td style="height: 7px; width: 337px;"> They must have a public IPv4 address or an Elastic IP address (IPv4) to connect with internet</td>
</tr>
<tr style="height: 82px;">
<td style="height: 82px; width: 395px;">External applications cannot access them directly via internet. Use bastion host / Jump servers to acccess the private subnet resources. Remote Desktop Gateway (Windows instances) or SSH-agent forwarding(linux instances) are to be configured</td>
<td style="height: 82px; width: 337px;">External applications can access them via internet.</td>
</tr>
<tr style="height: 189px;">
<td style="height: 189px; width: 395px;">Instances on private subnets may still access the internet by using a NAT Gateway for software updates and OS patches

A NAT will allow private instances (without a public IP) to access the Internet, but not the other way around.</td>
<td style="height: 189px; width: 337px;"> Instances can access the internet directly</td>
</tr>
</tbody>
</table>
<ul>
 	<li><b>Internet Gateway:</b> The Amazon VPC side of a connection to the public Internet.</li>
 	<li><b>NAT Gateway:</b> A highly available, managed Network Address Translation (NAT) service for your resources in a private subnet to access the other resources publicly accessible (AWS services / Internet / other subnets etc)</li>
 	<li><b>Egress-only Internet Gateway:</b> A stateful gateway to provide egress only access for IPv6 traffic from the VPC to the Internet.
<ul>
 	<li><a href="https://www.reddit.com/r/aws/comments/6qxtbs/vpc_architecture_nat_gateway_vs_egressonly/">VS NAT</a>: egress-only gateways are <strong>only for IPv6</strong> since all those addresses are internet routable.</li>
 	<li>In a true autoscale environment, your source IPs in a IGW-only situation would potentially change all the time.Often vendors will require whitelisting of IPs to gain access to a service.NAT solves  that. <strong>With a NAT gateway, all egress traffic appears from a single IP</strong> (or at least one per AZ).</li>
</ul>
</li>
 	<li><b>Hardware VPN Connection:</b> A hardware-based VPN connection between your Amazon VPC and your datacenter, home network, or co-location facility.
<ul>
 	<li><b>Virtual Private Gateway: </b>The Amazon VPC side of a VPN connection.</li>
 	<li><b>Customer Gateway:</b> Your side of a VPN connection.</li>
</ul>
</li>
 	<li><b><strong>VPC Peering / </strong>Peering Connection:</b> A peering connection enables you to route traffic via private IP addresses between two peered VPCs.
<ul>
 	<li>VPC peering can be used to create secure connectivity and resource sharing between two VPCs.</li>
 	<li>You can also create a VPC peering connection between your VPCs, or with a VPC in another AWS account.</li>
 	<li>A VPC peering connection enables you to <strong>route traffic between the VPCs using private IP addresses</strong>; however, you <strong>cannot</strong> create a VPC peering connection between VPCs that have <strong>overlapping CIDR blocks</strong>.</li>
</ul>
</li>
 	<li><b>VPC Endpoints: </b>Enables private connectivity to services hosted in AWS, from within your VPC without using an an Internet Gateway, VPN, Network Address Translation (NAT) devices, or firewall proxies.</li>
 	<li><b>Router:</b> Routers interconnect subnets and direct traffic between Internet gateways, virtual private gateways, NAT gateways, and subnets.</li>
 	<li>
<p id="SubnetRouting"><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Route_Tables.html"><strong>Route Table Basics</strong></a></p>

<ul>
 	<li>A <em>route table</em> contains a <strong>set of rules, called <em>routes</em></strong>, that are used to determine where network traffic is directed.</li>
 	<li>Your VPC has an implicit router.</li>
 	<li>Your VPC automatically comes with a main route table that you can modify. You can <strong>create additional custom route tables</strong> for your VPC.</li>
 	<li>Each subnet in your VPC must be associated with a route table; the table controls the routing for the subnet.<strong> A subnet can only be</strong> <strong>associated with one route table at a time</strong>, but you can associate multiple subnets with the same route table.</li>
 	<li>If you don't explicitly associate a subnet with a particular route table, Every subnet that you create is <strong>automatically associated with the main route table for the VPC</strong>.</li>
</ul>
</li>
</ul>
<h3><strong><b>AWS IP Addresses</b></strong></h3>
The<strong> first four IP addresses and the last IP address in <span style="text-decoration: underline;">each subnet</span> CIDR block</strong> are not available for you to use, and cannot be assigned to an instance. For example, in a subnet with CIDR block <code class="code">10.0.0.0/24</code>, the following five IP addresses are reserved:
<ul>
 	<li class="listitem"><code class="code">10.0.0.0</code>: Network address.</li>
 	<li class="listitem"><code class="code">10.0.0.1</code>: Reserved by AWS for the VPC router.</li>
 	<li class="listitem"><code class="code">10.0.0.2</code>: Reserved by AWS. The IP address of the DNS server is always the base of the VPC network range plus two; however, we also reserve the base of each subnet range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR. For more information, see <a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS">Amazon DNS Server</a>.</li>
 	<li class="listitem"><code class="code">10.0.0.3</code>: Reserved by AWS for future use.</li>
 	<li class="listitem"><code class="code">10.0.0.255</code>: Network broadcast address. We do not support broadcast in a VPC, therefore we reserve this address.</li>
</ul>
<h3>Elastic IP</h3>
<strong>Static Public ip</strong> <strong>associated with account</strong> and can be associated with any instance. An <strong>Elastic IP (EIP)</strong> is an IP address that you can reserve from AWS for your account. Once you reserve an Elastic IP, nobody else can use that IP address.
<ul>
 	<li>Elastic IPs are unique because they are <strong>dynamically remappable IP addresses</strong> that make it easier to manage servers and make global changes in the cloud.</li>
 	<li>Once you've created an Elastic IP, you can <strong>assign it to any instance of your choice.</strong></li>
 	<li>Elastic IPs are also an essential component for creating failover deployments on EC2.</li>
 	<li>EIPs can be reassigned to different instances when necessary as you launch and terminate servers. Typically, you will associate EIPs to your frontend servers. You can assign an EIP to a running instance or associate an EIP when an instance is launched.</li>
 	<li>Be careful, you can also <strong>steal </strong><strong>an EIP</strong> from one of your instances.
<ul>
 	<li>As a best practice, you should age any new EIP before you assign it to one of your public facing servers because that IP address <strong>may still be temporarily cached and mapped to its previous instance.</strong> You do not want to accidentally inherit unintended traffic from its predecessor.</li>
 	<li>As a preventative measure, Amazon gives users the ability to reserve a public IP address for your use only from their pool of IP addresses.</li>
</ul>
</li>
 	<li>By default, Amazon will let you reserve up to 5 EIPs per account. If you would like to reserve more than 5 EIPs, you can submit a request to Amazon.</li>
 	<li><strong>Elastic IPs are totally free</strong>, as long as they are being used by an instance. However, Amazon <strong>will charge you $0.01/hr for each EIP that you reserve and do not use</strong>. (to avoid the wastage of resources)</li>
 	<li>You<strong> will be charged</strong> if you ever <strong>remap an EIP more than 100 times</strong> in a month.</li>
</ul>
Once you delete an Elastic IP from your account, it gets returned to Amazon's pool of IP addresses.

Follow the steps below to make sure that you take the necessary steps before deleting an Elastic IP.
<ol>
 	<li>Remove the Elastic IP from all DNS entries.</li>
 	<li>Wait a minimum of 24 hrs.</li>
 	<li>While your Elastic IP remains idle in your account, perform some tests to make sure that your new DNS changes have gone through and that your deployment is running as expected without any errors related to the DNS records.</li>
 	<li>Delete your unused Elastic IP. (Clouds &gt; AWS -&gt; Elastic IPs). Click the <strong>Delete</strong>
NOTE: It may take about 5 minutes for the EIP to disappear from your screen after you've deleted it.</li>
</ol>
<ul>
 	<li>You cannot migrate an Elastic IP address to another region.</li>
</ul>
<h3><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html">DNS HostNames</a></h3>
<ul>
 	<li>When you launch an instance into a <strong>default</strong> VPC, we provide the instance <strong>with public and private DNS hostnames</strong> that correspond to the public IPv4 and private IPv4 addresses for the instance.</li>
 	<li>When you launch an instance into a<strong> nondefault VPC,</strong> we provide the instance with a private DNS hostname and we might provide a <strong>public DNS hostname</strong>, depending on the <a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-dns-support">DNS attributes</a> you specify for the VPC and if your instance has a public IPv4 address.</li>
 	<li>
<h4 id="vpc-dns-support">DNS Support in Your VPC</h4>
Your VPC has attributes that determine whether your instance receives public DNS hostnames, and whether DNS resolution through the Amazon DNS server is supported.
<div class="table">
<div class="table-contents">
<table id="w87aac19c19c13b4">
<tbody>
<tr>
<th>Attribute</th>
<th>Description</th>
</tr>
<tr>
<td><code class="code">enableDnsHostnames</code></td>
<td>Indicates whether the instances launched in the VPC get public DNS hostnames.

If this attribute is <code class="code">true</code>, instances in the VPC get public DNS hostnames, but only if the <code class="code">enableDnsSupport</code> attribute is also set to <code class="code">true</code>.</td>
</tr>
<tr>
<td><code class="code">enableDnsSupport</code></td>
<td>Indicates whether the DNS resolution is supported for the VPC.

If this attribute is <code class="code">false</code>, the Amazon-provided DNS server in the VPC that resolves public DNS hostnames to IP addresses is not enabled.

If this attribute is <code class="code">true</code>, queries to the Amazon provided DNS server at the 169.254.169.253 IP address, or the reserved IP address at the base of the VPC IPv4 network range plus two will succeed.</td>
</tr>
</tbody>
</table>
</div>
</div></li>
</ul>
<h3>Charges / cost</h3>
<ul>
 	<li>EC2 instances charged per configuration</li>
 	<li>VPC, subnets, route tables, ACLs are not charged</li>
 	<li>VPN connections are charged per hour</li>
 	<li>Internet gateway - no charge</li>
 	<li>NAT gateway - NAT Gateway - hour</li>
 	<li>Load balancer - charged</li>
 	<li>Elastic IPs - charged only in case not allocated to any instance</li>
</ul>
<h3><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Security.html">VPC Security</a></h3>
<p id="gycrZAe"><img class=" wp-image-1368 alignright" src="/wp-content/uploads/2018/03/img_5abaf79ed5f67.png" alt="" width="355" height="381" /></p>
Amazon VPC provides features that you can use to increase and monitor the security for your VPC:
<div class="itemizedlist">
<ul>
 	<li><strong>Security groups</strong> — Act as a <strong>firewall</strong> for associated Amazon <strong>EC2 instances</strong>, controlling both inbound and outbound traffic at the instance level</li>
 	<li><strong>Network access control lists (ACLs)</strong> — Act as a <strong>firewall for associated subnets,</strong> controlling both inbound and outbound traffic at the subnet level</li>
 	<li><strong>Flow logs</strong> — Capture information about the IP traffic going to and from network interfaces in your VPC
<ul>
 	<li>You can monitor the accepted and rejected IP traffic going to and from your instances by creating a flow log for a VPC, subnet, or individual network interface. Flow log data is published to CloudWatch Logs, and can help you diagnose overly restrictive or overly permissive security group and network ACL rules.</li>
</ul>
</li>
</ul>
<h4 id="VPC_Security_Comparison">Comparison of Security Groups and Network ACLs</h4>
<div>
<table id="w87aac17c17b4" style="width: 741px;">
<tbody>
<tr>
<th style="width: 357px;">Security Group</th>
<th style="width: 362px;">Network ACL</th>
</tr>
<tr>
<td style="width: 357px;">Operates at the instance level (first layer of defense)</td>
<td style="width: 362px;">Operates at the subnet level (second layer of defense)</td>
</tr>
<tr>
<td style="width: 357px;">whitelisting ports

Supports<strong> allow rules only / no deny.</strong> (by default all traffic are denied).</td>
<td style="width: 362px;">Blacklisting ports and protocols

Supports allow rules and deny rules.
Each network ACL includes a default rule whose rule number is an asterisk. This rule ensures that if a packet doesn't match any of the other rules, it's denied. You can't modify or remove this rule. <strong>(by default all traffic are denied</strong>)</td>
</tr>
<tr>
<td style="width: 357px;">Is <strong>stateful</strong>:<strong> Return traffic is automatically allowed,</strong> regardless of any rulesExample: port 22 is for incoming SSH connections from external world. But response is not from 22 but from higher dynamic port range. Security group tracks the request by maintaining state with response and allows the responses automatically.</td>
<td style="width: 362px;">Is <strong>stateless</strong>: Return traffic must be explicitly allowed by rules.

Has to configure both inbound and outbound ports</td>
</tr>
<tr>
<td style="width: 357px;">We <strong>evaluate all rules</strong> before deciding whether to allow traffic</td>
<td style="width: 362px;">We process rules in number <strong>order</strong> (<strong>starting with lowes</strong>t) when deciding whether to allow traffic</td>
</tr>
<tr>
<td style="width: 357px;">Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance later on</td>
<td style="width: 362px;">Automatically applies to all instances in the subnets it's associated with (backup layer of defense, so you don't have to rely on someone specifying the security group)</td>
</tr>
</tbody>
</table>
</div>
</div>
<p id="EptbbiP"><img class="wp-image-1252 aligncenter" src="/wp-content/uploads/2018/03/img_5ab379a17d2e7.png" alt="" width="463" height="548" /></p>

<h3><strong><b>Internet Gateway</b></strong></h3>
<ul>
 	<li>An Internet Gateway is a <strong><b>logical connection between an Amazon VPC and the Internet</b></strong>. It is <em><i>not </i></em>a physical device.</li>
 	<li>In order <strong>to connect with internet, VPC needs a gateway</strong>. If a VPC does not have an Internet Gateway, then the resources in the VPC cannot be accessed from the Internet (unless the traffic flows via a corporate network and VPN/Direct Connect).</li>
 	<li>You use an Internet Gateway with a route table to tell the VPC how internet traffic gets to the internet.</li>
 	<li><strong>Only one gateway can be associated with each VPC</strong>. It does <em><i>not</i></em> limit the bandwidth of Internet connectivity.</li>
 	<li>Amazon manages the gateway and there's nothing user can do.</li>
</ul>
<h3><strong><b>NAT Instance</b></strong></h3>
<ul>
 	<li>A <strong>NAT Instance</strong> is an Amazon EC2 instance configured to <strong>forward traffic to the Internet</strong>.</li>
 	<li>Your NAT-instance must be launched within your public subnet and it must have a public IP address. The route table of your public subnet where your NAT resides must have a route to the internet via <strong>your Internet Gateway</strong>.</li>
 	<li>Instances in a private subnet that want to access the Internet can have their Internet-bound <strong>traffic forwarded to the NAT Instance via a Route Table configuration</strong>. The NAT Instance will then make the request to the Internet (since it is in a Public Subnet) and the response will be forwarded back to the private instance.</li>
 	<li>Traffic sent to a NAT Instance will typically be sent to an IP address that is not associated with the NAT Instance itself (it will be destined for a server on the Internet). Therefore, it is important to turn off the <strong style="font-size: 1rem;"><b>Source/Destination Check</b></strong><span style="font-size: 1rem;"> option on the NAT Instance otherwise the traffic will be blocked.</span></li>
 	<li>AWS provides some <strong>Amazon Machine Images (AMIs)</strong> that are already pre-configured as NAT instances—I recommend that you consider using one. NAT AMIs have names that include the string ‘amzn-ami-vpc-nat’.</li>
</ul>
<strong><b>NAT Gateway</b></strong>
<ul>
 	<li>AWS introduced a <strong><b>NAT Gateway Service</b></strong> (around 2017) that can <strong>take the place of a NAT Instance.</strong> The benefits of using a NAT Gateway service are:
<ul>
 	<li>It is a <strong>fully-managed service</strong> -- just create it and it works automatically, including <strong>fail-over / highly available</strong></li>
 	<li>It can<strong> burst up to 10 Gbps (</strong>a NAT Instance is limited to the bandwidth associated with the EC2 instance type)</li>
</ul>
</li>
 	<li>However:
<ul>
 	<li><strong>Security Groups <b>cannot </b></strong>be associated with a NAT Gateway</li>
 	<li>You'll need one in each AZ since they <strong>only operate in a single AZ</strong></li>
</ul>
</li>
 	<li>Need to be created in public subnet with public ip address</li>
</ul>
As far as <strong>NAT gateway vs. NAT instance</strong>, either will work. A <strong>NAT instance can be a little cheaper, but the NAT gateway is fully managed by AWS</strong>, so it has the advantage of not needing to maintain an EC2 instance just for NATing.
<h3>What is a bastion host / jump server ?</h3>
<ul>
 	<li class="selectionShareable">Bastion hosts are instances that sit within your public subnet and are typically accessed using</li>
 	<li class="selectionShareable">SSH or RDP.</li>
 	<li class="selectionShareable">Once remote connectivity has been established with the bastion host, it then acts as a ‘jump’ server, allowing you to use SSH or RDP to log in to other instances (within private subnets) deeper within your VPC.</li>
 	<li class="selectionShareable">When properly configured through the use of security groups and Network ACLs (NACLs), the <strong>bastion essentially acts as a bridge</strong> to your private instances via the internet.
<p id="GzuCWMe"><img class="alignnone wp-image-1251 " src="/wp-content/uploads/2018/03/img_5ab370b676194.png" alt="" width="461" height="180" /></p>
</li>
 	<li>However, once you have connected to your bastion host, logging in to your private instances from the bastion would require <strong>having their private keys on the bastion.</strong> As you will probably already know (and if not, then take careful note now), storing private keys on remote instances is <strong>not a good security practice</strong>.</li>
 	<li>As a result, AWS suggests that you implement either <strong>Remote Desktop Gateway</strong> (for connecting to Windows instances) or <strong>SSH-agent forwarding</strong> (for Linux instances). Both of these solutions eliminate the need for storing private keys on the bastion host.</li>
</ul>
&nbsp;
<h2 style="text-align: center;">Amazon VPC</h2>
<ul>
 	<li>Free to create VPCs</li>
 	<li>works as network layer for instances</li>
 	<li>creates virtual network - logically isolated area</li>
 	<li> to build a virtual network in the AWS cloud - no VPNs, hardware, or physical datacenters required.</li>
 	<li>connectivity options
<ul>
 	<li>VPC to VPC</li>
 	<li>VPC to VPN (data centers)</li>
 	<li>VPC to Internet</li>
</ul>
</li>
 	<li>can be created in minutes
<ul>
 	<li>during creation automatically assigns</li>
 	<li>secuirty groups</li>
 	<li>ip range</li>
 	<li>subnet</li>
 	<li>routing tables</li>
</ul>
</li>
 	<li>Advanced secuirty
<ul>
 	<li>control inboud . outbound
<ul>
 	<li>subnet level</li>
 	<li>instance level</li>
 	<li>Hardware level</li>
 	<li>or user level</li>
</ul>
</li>
 	<li>Leverage security layers
<ul>
 	<li>ACL - Access Control Lists</li>
 	<li>Security groups</li>
</ul>
</li>
</ul>
</li>
 	<li>Create
<ul>
 	<li>range of IP address</li>
 	<li>Subnets</li>
 	<li>network gateways</li>
 	<li>routing tables</li>
</ul>
</li>
 	<li>Limits</li>
 	<li>
<p id="KiaodnX"><img class="alignnone size-full wp-image-1454 " src="/wp-content/uploads/2018/04/img_5ac8098a5d8f8.png" alt="" /></p>
</li>
 	<li>connect to VPN connection from on premises data center. so cloud will act as an extension of the data center</li>
 	<li>
<p id="ItPvRnu"><img class="alignnone wp-image-1238 " src="/wp-content/uploads/2018/03/img_5ab34d5397cb3.png" alt="" width="567" height="99" /></p>
</li>
 	<li>Scalability,  reliability, pay as you go and other aws features</li>
</ul>
Benefits of launching instances within a VPC
<ul>
 	<li>
<p id="SZiRzlU"><img class="alignnone size-full wp-image-1239 " src="/wp-content/uploads/2018/03/img_5ab34f64b1694.png" alt="" /></p>
</li>
 	<li>allocate static ip addresses to instances</li>
 	<li>split the range of ip addresses of VPC</li>
 	<li>allocate multiple ip addresses to instances</li>
 	<li><span style="background-color: #999999;">run instances on the hardware used by single entity. ( in case of auto scaling ?)</span></li>
 	<li>Define network interfaces</li>
 	<li>change the membership of security group of instances</li>
 	<li>Default VPC is created for each account
<ul>
 	<li>defalt VPC contains a subnet in each AZ - default subnets</li>
 	<li>all others are not default subnets</li>
</ul>
</li>
</ul>
<a href="https://aws.amazon.com/vpc/?sc_channel=PS&amp;sc_campaign=Acquisition_IN&amp;sc_publisher=google&amp;sc_medium=vpc_b&amp;sc_content=aws_vpc_e&amp;sc_detail=aws%20vpc&amp;sc_category=vpc&amp;sc_segment=208384572667&amp;sc_matchtype=e&amp;sc_Country=IN&amp;s_kwcid=AL!4422!3!208384572667!e!!g!!aws%20vpc&amp;ef_id=WgMqYgAAAH6AP3CP:20180322064617:s">5 use cases of VPC Wizard</a>

<img class="wp-image-1240 alignright" src="/wp-content/uploads/2018/03/img_5ab356e89bb56.png" alt="" width="122" height="187" />

&nbsp;
<ol>
 	<li>
<p id="Host_a_simple.2C_public-facing_website" class="lb-txt-uppercase lb-h3 lb-title">VPC with a Single Public Subnet Only</p>

<ol>
 	<li>HOST A SIMPLE (SINGLE TIER), PUBLIC-FACING WEBSITE- blog or simple website</li>
 	<li>You can help secure the website by creating security group rules which allow the webserver to respond to inbound HTTP and SSL requests from the Internet while simultaneously <strong>prohibiting the webserver from initiating outbound connections</strong> to the Internet.</li>
</ol>
</li>
 	<li>VPC with Public and Private Subnets
<p id="KbmXXoc"><img class="wp-image-1241 alignright" src="/wp-content/uploads/2018/03/img_5ab3575156a44.png" alt="" width="246" height="231" /></p>

<ol>
 	<li>HOST MULTI-TIER WEB APPLICATIONS -</li>
 	<li>strictly enforce access and security restrictions between your webservers, application servers, and databases</li>
 	<li>You can launch <strong>webservers in a publicly accessible subnet</strong> and</li>
 	<li>application servers and databases in <strong>non-publically accessible subnets</strong>. The application servers and databases can’t be directly accessed from the Internet,</li>
 	<li>but <strong>they can still access the Internet via a <span style="text-decoration: underline;">NAT gateway</span></strong> to download patches, for example.</li>
 	<li>You can control access between the servers and subnets using inbound and outbound packet filtering provided by network access control lists and security groups.</li>
</ol>
</li>
 	<li>VPC with Public and Private Subnets and Hardware <strong>VPN Access </strong>
<p id="VRqMLpp"><img class="alignnone wp-image-1242 alignleft" src="/wp-content/uploads/2018/03/img_5ab3585635fc4.png" alt="" width="212" height="244" /><img class="wp-image-1243 alignnone" src="/wp-content/uploads/2018/03/img_5ab358bd11ee8.png" alt="" width="332" height="127" /></p>

<ol>
 	<li>VPC where instances in one subnet, such as web servers, communicate with the Internet</li>
 	<li>while instances in another subnet, such as <strong>application servers, communicate</strong> with <strong>databases on your corporate network</strong></li>
 	<li>An IPsec VPN connection between your VPC and your corporate network helps secure all communication between the application servers in the cloud and databases in your data center.</li>
 	<li>Web servers and application servers in your VPC can leverage Amazon EC2 elasticity and <strong>Auto Scaling features</strong> to grow and shrink as needed.</li>
</ol>
</li>
 	<li>VPC with a <strong>Private Subnet Only</strong> and Hardware <strong>VPN Access </strong>
<p id="qvPCjvF"><img class="wp-image-1244 alignright" src="/wp-content/uploads/2018/03/img_5ab3590d8dee9.png" alt="" width="111" height="196" /></p>

<ol>
 	<li>VPC can be <strong>hosted behind your corporate firewall</strong>, you can seamlessly <strong>move your IT resources into the cloud</strong> without changing how your users access these applications.</li>
 	<li>launch additional web servers, or add <strong>more compute capacity to your network</strong> by connecting your VPC to your corporate network.</li>
</ol>
</li>
 	<li>DISASTER RECOVERY
<ol>
 	<li>periodically backup your mission critical data from your datacenter to a small number of Amazon EC2 instances with Amazon Elastic Block Store (EBS) volumes, or import your virtual machine images to Amazon EC2.</li>
 	<li>In the event of a disaster in your own datacenter, you can quickly launch replacement compute capacity in AWS to ensure business continuity.</li>
 	<li>When the disaster is over, you can send your mission critical data back to your datacenter and terminate the Amazon EC2 instances that you no longer need.</li>
 	<li>By using Amazon VPC for disaster recovery, you can have all the benefits of a disaster recovery site at a fraction of the normal cost.</li>
</ol>
</li>
</ol>
<h3><a href="https://www.quora.com/How-should-I-migrate-an-existing-set-of-EC2-instances-into-a-VPC">Setup and Move existing instances to VPC</a></h3>
<ul>
 	<li>You <strong>can't directly move the existing EC2 instance in default VPN to newly created VPN</strong></li>
</ul>
<ol>
 	<li>Setup VPC
<ol>
 	<li>Create an initial VPC, and give it a nice big CIDR, like 10.8.X.X/16. That will let you assign the third octet to each availability zone you want to include within your VPC, and your fourth octet to individual addresses within each AZ. A common mistake is to create the CIDR too small, so that you can't spread out across multiple AZ's.</li>
 	<li>Add subnets to your VPC, at least two of them. Here's where you can add 10.8.1.X in US-East-1a, 10.8.2.X in US-East-1b, and so on.</li>
 	<li>Make sure your routing rules are in line, so that each subnet can see and talk to the others. Also create an Internet gateway and direct traffic bound for 0.0.0.0/0 to that gateway.</li>
 	<li>Create the appropriate security groups for your servers to live in. This will lock down what ports can be made available to the world, or to other resources within the VPC. (For instance it would be a best practice to have a database server in its own group, accessible over a specific port by members of your web server security group, and so on.)</li>
</ol>
</li>
 	<li> move some EC2 instances into your new VPC
<ol>
 	<li>Stop your instance</li>
 	<li>Create a private AMI of the instance</li>
 	<li>Detach all secondary EBS volumes from the instance</li>
 	<li>Create a new instance within your VPC based upon the AMI you created above. Create it in the same AZ as the original instance, within the corresponding VPC subnet of that AZ. You can assign it a specific IP within that subnet if you like, like 10.8.1.5, or let one be automatically assigned to it.</li>
 	<li>Attach the secondary EBS volumes you disconnected to your new instance.</li>
 	<li>Create a new elastic IP, related to your VPC, and connect it to your instance.</li>
 	<li>If everything works okay -- you can connect to your instance, it's working well, etc. -- then you can delete the original instance and perhaps even the AMI you created earlier, though the latter might be nice to have on hand.</li>
</ol>
</li>
</ol>
<h4><a href="https://forums.aws.amazon.com/thread.jspa?threadID=234959">Ec2 instance as NAT gateway</a></h4>
<ul>
 	<li>Problem: In order for my Lambda functions to call external services, I am forced to use a NAT Gateway on the VPC that my Lambda function sits on. There is <strong>no free tier</strong> (or any tiering for that matter) and its difficult to justify a 35USD additional spend on a development account that under normal circumstances would rack up a bill of between 10USD and 20USD. In addition to that... <strong>I cant even disable it when it is not in use. Its either created or deleted.</strong></li>
 	<li>Solution: I would like to suggest that you <strong>remove the NAT Gateway and try implementing a t2.micro as a <a class="jive-link-external" href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_NAT_Instance.html">NAT instance</a> instead</strong>. If run for an entire month, a <strong>t2.micro will cost less than $10 USD in the US-East-1 region</strong>, and <strong>you are able to stop it whenever it is not in use</strong>. Additionally, t2.micro instances are <strong>within the free-tier.</strong> You can configure an instance as a NAT instance yourself, or you can use one of our provided NAT AMIs you can access from the instance launch wizard.</li>
</ul>
<h3><a href="https://aws.amazon.com/premiumsupport/knowledge-center/create-attach-igw-vpc/">Steps to use internet gateway</a></h3>
In order for the resources in a VPC to send and receive traffic from the internet via gateway, the following must be true:
<ol>
 	<li>An <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IGW_Attach_Gateway" target="_blank" rel="noopener">internet gateway must be attached</a> to the VPC.</li>
 	<li>The <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Route_Tables.html" target="_blank" rel="noopener">route tables associated with your public subnet</a> (including <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IGW_Routing" target="_blank" rel="noopener">custom route tables</a>) must have a route to the internet gateway.</li>
 	<li>The <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IG_Security_Groups" target="_blank" rel="noopener">security groups</a> associated with your VPC must allow traffic to flow to and from the Internet.</li>
 	<li>Any instances in the VPC must either have a <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#Add_IG_EIPs" target="_blank" rel="noopener">public IP address or an attached Elastic IP address</a>.</li>
</ol>
<p style="padding-left: 30px;">You can find instructions for each of these steps at <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Internet_Gateway.html#d0e22943" target="_blank" rel="noopener">Creating a VPC with an Internet Gateway</a>.</p>
<a href="https://aws.amazon.com/vpc/pricing/">VPC Pricing &amp; Endpoints to route traffic instead of NAT gateways</a>
<ul>
 	<li><b>Note:</b> To avoid the NAT Gateway Data Processing charge in this example, you could setup a Gateway Type VPC endpoint and route the traffic to/from S3 through the VPC endpoint instead of going through the NAT Gateway. There is no data processing or hourly charges for using Gateway Type VPC endpoints. For details on how to use VPC endpoints, please visit <a href="http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-endpoints.html" target="_blank" rel="noopener">VPC Endpoints Documentation</a>.</li>
</ul>
<h3><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-endpoints.html">VPC Endpoints</a></h3>
<ul>
 	<li>A VPC endpoint enables you to <strong>privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink</strong> without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.</li>
 	<li>Instances in your VPC <strong>do not require public IP addresses</strong> to communicate with resources in the service.</li>
 	<li>Traffic between your VPC and the other service <strong>does not leave the Amazon network.</strong></li>
 	<li>Endpoints are <strong>virtual devices.</strong> They are <strong>horizontally scaled, redundant, and highly available</strong> VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.</li>
 	<li>By default, IAM users do not have permission to work with endpoints. You can create an IAM user policy that grants users the permissions to create, modify, describe, and delete endpoints.</li>
 	<li><img class="wp-image-1343 alignleft" style="font-family: Dosis, sans-serif; font-weight: bold;" src="/wp-content/uploads/2018/03/img_5ab8d2cd1ae87.png" alt="" width="439" height="260" />current rules and limitations:
<div class="itemizedlist"></div>
<ul>
 	<li>You cannot tag an endpoint service.</li>
 	<li>An endpoint service supports IPv4 traffic over TCP only.</li>
 	<li>Service consumers must use the endpoint-specific DNS hostnames to access the endpoint service. Private DNS is not supported. For more information, see <a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpce-interface.html#access-service-though-endpoint">Accessing a Service Through an Interface Endpoint</a>.</li>
 	<li>Endpoint services are only available in the AWS Region in which they are created.</li>
 	<li>If an endpoint service is associated with multiple Network Load Balancers, then for a specific Availability Zone, an interface endpoint will establish a connection with one load balancer only.</li>
</ul>
</li>
 	<li>
<table id="w87aac19c25b7" style="width: 700px;">
<tbody>
<tr>
<th style="width: 97px;">Endpoint type</th>
<th style="width: 194.442px;">Description</th>
<th style="width: 378.558px;">Supported services</th>
</tr>
<tr>
<td style="width: 97px;">Interface (powered by AWS PrivateLink)</td>
<td style="width: 194.442px;">An elastic network interface with a private IP address that serves as an entry point for traffic destined to a supported service.</td>
<td style="width: 378.558px;">
<ul class="itemizedlist" type="disc">
 	<li class="listitem">Amazon EC2 API</li>
 	<li class="listitem"><a href="http://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-setting-up-vpc.html" target="_blank" rel="noopener">AWS Systems Manager</a></li>
 	<li class="listitem"><a href="http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/cloudwatch-logs-and-interface-VPC.html" target="_blank" rel="noopener">Amazon CloudWatch Logs</a></li>
 	<li class="listitem">Elastic Load Balancing API</li>
 	<li class="listitem"><a href="http://docs.aws.amazon.com/streams/latest/dev/vpc.html" target="_blank" rel="noopener">Amazon Kinesis Data Streams</a></li>
 	<li class="listitem"><a href="http://docs.aws.amazon.com/kms/latest/developerguide/kms-vpc-endpoint.html" target="_blank" rel="noopener">AWS KMS</a></li>
 	<li class="listitem">AWS Service Catalog</li>
 	<li class="listitem"><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/endpoint-service.html">Endpoint services</a>hosted by other AWS accounts</li>
 	<li class="listitem">Supported AWS Marketplace partner services</li>
</ul>
</td>
</tr>
<tr>
<td style="width: 97px;">Gateway</td>
<td style="width: 194.442px;">A gateway that is a target for a specified route in your route table, used for traffic destined to a supported AWS service.</td>
<td style="width: 378.558px;">
<div class="itemizedlist">
<ul class="itemizedlist" type="disc">
 	<li class="listitem">Amazon S3</li>
 	<li class="listitem">DynamoDB</li>
</ul>
</div></td>
</tr>
</tbody>
</table>
</li>
</ul>
&nbsp;

&nbsp;
<h2>LAB</h2>
<ul>
 	<li>VPC collection of ip addresses - CIDR block - range of ip addresses</li>
 	<li>Default VPC
<ul>
 	<li>Default VPC has internet gateway attached by default</li>
 	<li>once deleted, you can't created default VPC. You have to contact AWS support, to create default VPC</li>
 	<li></li>
</ul>
</li>
 	<li class="awsc-header ico-networking">Networking &amp; Content Delivery - VPC - create vpc
<ul>
 	<li>name</li>
 	<li class="awsc-header ico-networking">IPv4 CIDR block*</li>
 	<li>IPv6 CIDR block*</li>
 	<li>Tenancy
<ul>
 	<li>default - An instance launched into the VPC runs on shared hardware by default, unless you explicitly specify a different tenancy during instance launch.</li>
 	<li>dedicated - A <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html"><em>Dedicated Host</em></a> is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.</li>
</ul>
</li>
 	<li>Whenever you create VPC default security group is created. Allows all traffic with in the subnet</li>
</ul>
</li>
 	<li>Delete VPC - Deleting the VPC will also delete objects associated with this VPC in this region.
<ul>
 	<li>
<table class="GFBBVFQGNG">
<tbody>
<tr>
<td>
<ul>
 	<li>Subnets</li>
 	<li>Security Groups</li>
 	<li>Network ACLs</li>
 	<li>VPN Attachments</li>
</ul>
</td>
<td>
<ul>
 	<li>Internet Gateways</li>
 	<li>Route Tables</li>
 	<li>Network Interfaces</li>
 	<li>VPC Peering Connections</li>
</ul>
</td>
</tr>
</tbody>
</table>
</li>
 	<li>
<p id="czWPUdn"><img class="alignnone wp-image-1450 " src="/wp-content/uploads/2018/04/img_5ac78899e1d1f.png" alt="" width="433" height="229" /></p>
</li>
</ul>
</li>
 	<li>Create subnet
<ul>
 	<li>the subnet created <strong>by default private</strong></li>
 	<li>provide name, vpc, choose CIDR block subset of VPC, Availability Zone (choose different zones for each subnet for high availability)</li>
 	<li>Create a EC2 instance</li>
 	<li><strong>Public IPs</strong>
<ul>
 	<li>Enable auto-assign public IPv4 or IPv6 addresses to automatically request an IP address for instances launched into this subnet.</li>
 	<li>by default disabled</li>
 	<li>You <strong>can override the auto-assign IP settings for each individual instance</strong> at launch time for IPv4 or IPv6. Regardless of how you've configured the auto-assign public IP feature, you can assign a public IP address to an instance that has a single, new network interface with a device index of eth0.</li>
</ul>
</li>
</ul>
</li>
 	<li>
<p class="title"><a href="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html"><b>To describe and update DNS support for a VPC using the console</b></a></p>

<ol>
 	<li>Open the Amazon VPC console at <a href="https://console.aws.amazon.com/vpc/" target="_blank" rel="noopener">https://console.aws.amazon.com/vpc/</a>.</li>
 	<li>In the navigation pane, choose <b>Your VPCs</b>.</li>
 	<li>Select the VPC from the list.</li>
 	<li>Review the information in the <b>Summary</b> tab. In this example, both settings are enabled.
<div class="mediaobject"><img src="https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/images/dns-settings-gwt.png" alt=" The DNS Settings tab " /></div></li>
 	<li>To update these settings, choose <b>Actions</b> and either <b>Edit DNS Resolution</b> or <b>Edit DNS Hostnames</b>. In the dialog box that opens, choose <b>Yes</b> or <b>No</b>, and <b>Save</b>.</li>
</ol>
</li>
 	<li>VPC Dashboard - Security - Security groups
<ul>
 	<li>outbound. by default all outgoing traffic is allowed
<ul>
 	<li>
<table id="gwt-debug-tabContent2" class="GFBBVFQID"><colgroup> <col /></colgroup>
<tbody>
<tr class="GFBBVFQGE">
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Type</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Protocol</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Port Range</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Destination</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Description</div></td>
</tr>
<tr class="GFBBVFQJE">
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL Traffic</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">0.0.0.0/0</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left"></td>
</tr>
</tbody>
</table>
</li>
</ul>
</li>
 	<li>In bound. <strong>by default all traffic within the VPC is allowed.</strong> other end points available S3 and dynamodb of the region.
<ul>
 	<li>
<table id="gwt-debug-tabContent1" class="GFBBVFQID"><colgroup> <col /></colgroup>
<tbody>
<tr class="GFBBVFQGE">
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Type</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Protocol</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Port Range</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Source</div></td>
<td class="GFBBVFQFE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Description</div></td>
</tr>
<tr class="GFBBVFQJE">
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL Traffic</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">ALL</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">(VPC name)</div></td>
<td class="GFBBVFQIE" colspan="1" rowspan="1" align="left"></td>
</tr>
</tbody>
</table>
</li>
</ul>
</li>
</ul>
</li>
 	<li>By default no internet connection is provided. In order to connect with internet create internet gateway
<ul>
 	<li>Virtual Private Cloud - internet gateways - Create internet gateway - name</li>
 	<li>By default its detached. attach with VPC
<ul>
 	<li>Actions - Attach to VPC</li>
</ul>
</li>
 	<li>Gateway <strong>needs to be associated with necessary specific subnets</strong> to enable access to resources <strong>using routing rules</strong></li>
</ul>
</li>
 	<li>Route table
<ul>
 	<li>subnet is not aware of presence of gateway. so it can't connect with internet.</li>
 	<li>route table connect internet gateway with subnets</li>
 	<li>Route table route/forward packets to preconfigured gateway/intermediate node</li>
 	<li>Whenever a VPC is created default main route table is created. default route table is implicitly connected with all subnets</li>
 	<li>create public subnet route using Virtual Private Cloud -route tables - create route table
<ul>
 	<li>name -&gt; public route</li>
 	<li>select VPC</li>
</ul>
</li>
 	<li>connect route table with subnets
<ul>
 	<li>In bottom side bar - subnet associations - edit - select subnet(s) - save</li>
 	<li>
<table id="gwt-debug-tabContent1" class="GFBBVFQID" style="width: 414px;">
<tbody>
<tr>
<td class="GFBBVFQBE" style="width: 95px;" colspan="1" rowspan="1" align="left">
<div class="gwt-HTML">View: Default</div></td>
<td class="GFBBVFQKE" style="width: 72px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">All rules</div></td>
</tr>
<tr class="GFBBVFQGE">
<td class="GFBBVFQFE" style="width: 95px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Destination</div></td>
<td class="GFBBVFQFE" style="width: 72px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Target</div></td>
<td class="GFBBVFQFE" style="width: 27px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Status</div></td>
<td class="GFBBVFQFE" style="width: 84px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Propagated</div></td>
<td class="GFBBVFQDE" style="width: 74px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">Remove</div></td>
</tr>
<tr class="GFBBVFQJE">
<td class="GFBBVFQIE" style="width: 95px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">10.5.0.0/24</div></td>
<td class="GFBBVFQIE" style="width: 72px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">local</div></td>
<td class="GFBBVFQIE" style="width: 27px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label GFBBVFQCDC">Active</div></td>
<td class="GFBBVFQIE" style="width: 84px;" colspan="1" rowspan="1" align="left">
<div class="gwt-Label">No</div></td>
</tr>
</tbody>
</table>
</li>
</ul>
</li>
 	<li>
<p id="qsZHuWp">connect route table with gateway<img class="alignnone wp-image-1443 " src="/wp-content/uploads/2018/04/img_5ac6b36f42f67.png" alt="" width="506" height="125" /></p>

<ul>
 	<li>Routes - Edit - Add route - Destination 0.0.0.0/0 all - target - gateway -&gt; save</li>
</ul>
</li>
</ul>
</li>
 	<li>NAT Gateway
<ul>
 	<li>provide outgoing internet connection to private instances to get the patches</li>
 	<li>NAT gateway needs to be in public subnet</li>
 	<li>create route table and connect with instances with nat gateway and nat gateway to internet gateway</li>
 	<li>NAT Gateways &gt; Create NAT Gateway -&gt; Select public subnet -&gt; Allocate elastic ip (EIP - create a new EIP)</li>
 	<li>You<strong> can't detach an internet gateway</strong> if there is an instance with public ip</li>
 	<li>
<p id="FHeojaQ"><img class="alignnone wp-image-1448 " src="/wp-content/uploads/2018/04/img_5ac755c6f3ce8.png" alt="" width="397" height="254" /></p>
</li>
</ul>
</li>
 	<li>
<p id="fdKsMvR"><img class=" wp-image-1446 alignright" src="/wp-content/uploads/2018/04/img_5ac6e9b3174e9.png" alt="" width="205" height="164" /><span style="font-size: 1rem;">VPC peering - connection between 2 peers</span></p>

<ul>
 	<li>2 VPCS should be in same region</li>
 	<li>IP addresses range should not overlap</li>
 	<li>it's peer to peer connection</li>
 	<li>peer hoping is not allowed</li>
</ul>
</li>
 	<li>Elastic IP
<ul>
 	<li>EC 2 Dashboard -&gt; NETWORK &amp; SECURITY -&gt; Elastic IPs &gt; Allocate New Address -&gt; allocate button (no config)</li>
 	<li>Select ip -&gt; Action -&gt; Associate the address -&gt; select Instance</li>
</ul>
</li>
</ul>
<h2>References</h2>
<ul>
 	<li style="list-style-type: none;">
<ul>
 	<li>https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html</li>
 	<li>Bastion host, NAT, Gateways <a href="https://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/"><u>https://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/</u></a></li>
 	<li>Elastic IP https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-eips.html</li>
 	<li><a href="https://docs.rightscale.com/cm/dashboard/clouds/aws/ec2_elastic_ips.html">EC2 Elastic IPs</a></li>
</ul>
</li>
</ul>
