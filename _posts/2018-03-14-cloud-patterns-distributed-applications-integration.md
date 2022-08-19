---
layout: post
title: Cloud Patterns - Distributed applications and integration
date: 2018-03-14 10:42
author: tmasabari
comments: true
categories: [Architecture, Design, Design, Patterns]
---
<h2>Background</h2>
<a href="http://www.cloudcomputingpatterns.org/#cloud_application_architectures">Cloud application architectures</a> describe the general structure of the cloud application and specific application components for user interfaces, processing, and data handling.
<h2>Design Patterns</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/loose_coupling/">Loose Coupling</a></h3>
Application components can be <strong>treated individually</strong> and the <strong>dependencies among them are kept to a minimum, </strong>separates application functionality from concerns of communication partners regarding their
<ol>
 	<li>location,</li>
 	<li>implementation platform,</li>
 	<li>the time of communication, and</li>
 	<li>the used data format.</li>
 	<li>as well as associated management tasks, such as
<ol>
 	<li>scaling,</li>
 	<li>failure handling, or</li>
 	<li>update management</li>
</ol>
</li>
</ol>
Communicating components and multiple integrated applications are decoupled from each other by interacting <strong>through a broker</strong>.
<p id="tRxShYY"><img class="alignnone wp-image-846 " src="/wp-content/uploads/2018/03/img_5aa76fd644f1e.png" alt="" width="396" height="119" /></p>
&nbsp;
<h3><a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a></h3>
<ul>
 	<li>Divides provided functionality among multiple application components that can be scaled out independently</li>
 	<li>respect the distribution and the scaling-out support of cloud environments in their architecture. –  especially provider assures <a href="http://www.cloudcomputingpatterns.org/environment_based_availability/">Environment-based Availability</a>  for complete environment and not of single IT resources hosted in it</li>
 	<li>Types
<ul>
 	<li><strong>Tiers</strong> - logical components are subsumed to multiple tiers to denote that they shall be deployed together physically, i.e., on one server (cluster)
<ul>
 	<li>
<p id="IMNeusl"><img class="alignnone size-full wp-image-849 " src="/wp-content/uploads/2018/03/img_5aa77943c8722.png" alt="" /></p>
</li>
</ul>
</li>
 	<li><strong>Layer-based</strong> decomposition - separate logical layers - Components are restricted to access components of the same layer or one layer below</li>
 	<li><strong>Process-based</strong> decomposition (micro services) - focuses on the business processes supported by the application. These processes are comprised out of activities that are executed in a specific order
<ul>
 	<li>
<p id="OrHYucG"><img class="alignnone size-full wp-image-848 " src="/wp-content/uploads/2018/03/img_5aa7792a380f4.png" alt="" /></p>
</li>
</ul>
</li>
 	<li><strong>Pipes-and-filters-based</strong> decomposition (data services ?) - focues on for data-centric processing
<ul>
 	<li>Each filter provides a certain function that is performed on input data and produces output data after processing.</li>
 	<li>Multiple filters are interconnected with <strong>pipes</strong>, i.e, through <strong>messaging</strong></li>
 	<li>
<p id="mTMaZyd"><img class="alignnone size-full wp-image-847 " src="/wp-content/uploads/2018/03/img_5aa77903baa88.png" alt="" /></p>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3>Multi-tier architecture</h3>
<h4><a href="http://www.cloudcomputingpatterns.org/two_tier_cloud_application/">2 Tier</a></h4>
<ul>
 	<li><a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> functionality is decomposed into
<ol>
 	<li>data handling functionality, provided by one or several <a href="http://www.cloudcomputingpatterns.org/cloud_offerings/#storage_offerings">Storage Offerings</a>, and</li>
 	<li>application components handling presentation and business logic.</li>
</ol>
</li>
 	<li>This separation enables the two tiers to elastically scale independently with their workloads. <img class="alignnone wp-image-844 " src="/wp-content/uploads/2018/03/img_5aa76ca77515a.png" alt="" width="452" height="228" /></li>
</ul>
<h4><a href="http://www.cloudcomputingpatterns.org/three_tier_cloud_application/">3 Tier</a></h4>
<ul>
 	<li>if <strong><a href="http://www.cloudcomputingpatterns.org/processing_components/">Processing Components</a></strong> are more <strong>computation intensive</strong> or are used <strong>less frequent</strong>ly than <a href="http://www.cloudcomputingpatterns.org/user_interface_components/">User Interface Components</a>, aligning the elastic scaling of these two components by summarizing their implementation in one tier can be inefficient.
<ol>
 	<li>The presentation tier is comprised of a load balancer and an application component that implements the <a href="http://www.cloudcomputingpatterns.org/stateless_component/">Stateless Component</a> pattern and <a href="http://www.cloudcomputingpatterns.org/user_interface_component/">User Interface Component</a> pattern.</li>
 	<li>The business logic tier is comprised of an application component implementing the <a href="http://www.cloudcomputingpatterns.org/stateless_component/">Stateless Component</a> pattern in addition to the <a href="http://www.cloudcomputingpatterns.org/processing_component/">Processing Component</a>pattern.</li>
</ol>
</li>
 	<li>each tier is elastically scaled independently</li>
 	<li><img class="alignnone wp-image-845 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5aa76e6214fe9.png" alt="" width="572" height="234" /></li>
</ul>
<h3><a href="https://en.wikipedia.org/wiki/Middleware"><b>Middleware</b> </a></h3>
<ol>
 	<li>"The software layer that lies <strong>between the <a title="Operating system" href="https://en.wikipedia.org/wiki/Operating_system">operating system</a> and applications</strong> on each side of a <strong>distributed</strong> computing system in a network."</li>
 	<li>dash ("-") in <i><a class="mw-redirect" title="Client-server" href="https://en.wikipedia.org/wiki/Client-server">client-server</a></i>, or the <i>-to-</i> in <i><a title="Peer-to-peer" href="https://en.wikipedia.org/wiki/Peer-to-peer">peer-to-peer</a></i>. Services that can be regarded as middleware include <a title="Enterprise application integration" href="https://en.wikipedia.org/wiki/Enterprise_application_integration">enterprise application integration</a>, <a title="Data integration" href="https://en.wikipedia.org/wiki/Data_integration">data integration</a>, <a class="mw-redirect" title="Message oriented middleware" href="https://en.wikipedia.org/wiki/Message_oriented_middleware">message oriented middleware</a> (MOM), <a title="Object request broker" href="https://en.wikipedia.org/wiki/Object_request_broker">object request brokers</a>(ORBs), and the <a title="Enterprise service bus" href="https://en.wikipedia.org/wiki/Enterprise_service_bus">enterprise service bus</a> (ESB).</li>
 	<li>Examples of database-oriented middleware include <a class="mw-redirect" title="ODBC" href="https://en.wikipedia.org/wiki/ODBC">ODBC</a>, <a class="mw-redirect" title="JDBC" href="https://en.wikipedia.org/wiki/JDBC">JDBC</a> and <a title="Transaction processing" href="https://en.wikipedia.org/wiki/Transaction_processing">transaction processing</a> monitors.</li>
</ol>
<h2>Replication for distributed applications</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/compliant_data_replication/">Compliant Data Replication</a></h3>
<ul>
 	<li>If application <strong>components</strong> accessing the data are <strong>globally distributed</strong>, data access performance may be reduced drastically if data is only stored in one <strong>geographic location</strong>. Therefore, data may have to be replicated.</li>
 	<li>Due to<strong> laws and corporate regulations</strong>, some of these locations may only <strong>handle a subset of the available data</strong> <span style="text-decoration: underline;"><em>or</em></span> data has to be <strong>obfuscated</strong>.</li>
 	<li>Data is replicated among multiple environments asynchronously using messaging that may handle different data subsets.</li>
 	<li><strong>Message filters</strong> are used to delete and obfuscate certain data elements in these messages as they leave the trusted environment.</li>
 	<li>Information about the data <strong>manipulations</strong> stored in a <strong>storage offering</strong>.</li>
 	<li>If data is then altered in the less secure environment, the corresponding update <strong>message is enriched by a message enricher</strong> as it enters the secure environment.</li>
 	<li><img class="" src="http://www.cloudcomputingpatterns.org/sketches/compliant_data_replication_sketch.png" alt="Compliant Data Replication" width="390" height="284" /></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/content_distribution_network/">Content Distribution Network</a></h3>
<ul>
 	<li>If time critical content is located too far from the user accessing it, the communication delay of the distribution network may hinder the timely access to data. Therefore, storing content in only one centralized location, i.e., one cloud or data center is unfeasible.</li>
 	<li>Applications component instances and Content replicas are established in <strong>different physical locations of one or multiple clouds</strong>.</li>
 	<li>During this distribution of replicas, the topology of distribution networks is considered to ensure locality for all users.</li>
 	<li>Replicas are <strong>updated from a central</strong> location.</li>
 	<li><img class="" src="http://www.cloudcomputingpatterns.org/sketches/content_distribution_network_sketch.png" alt="Content Distribution Network" width="422" height="171" /></li>
</ul>
&nbsp;
<h2>Consistency for distributed applications</h2>
<h3><a href="http://www.cloudcomputingpatterns.org/strict_consistency/">Strict Consistency</a></h3>
<ul>
 	<li>Same set of data is stored at different locations (replicas)
<ul>
 	<li>to improve response time and</li>
 	<li>to avoid data loss in case of failures</li>
</ul>
</li>
 	<li>while consistency of replicas is ensured at all times.</li>
 	<li>A subset of data replicas is accessed by read and write operations.</li>
 	<li>The ratio of the number of replicas accessed during read (r) and write (w) operations guarantees consistency: n &lt; r + w</li>
 	<li><img class="alignnone wp-image-860 " src="/wp-content/uploads/2018/03/img_5aa78e4cea08d.png" alt="" width="147" height="115" /></li>
 	<li>Keeping all these replicas in a consistent state, however, requires a significant <strong>overhead</strong> as <strong>multiple or all data replicas have to be accessed during read and write operations</strong></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/eventual_consistency/">Eventual Consistency</a></h3>
<ul>
 	<li><strong>Performance (response time) and the availability(avoid data loss) of data </strong>in case of network partitioning <strong>[</strong>stored at different locations (replicas)<strong>]</strong></li>
 	<li>are enabled by <em>ensuring data consistency eventually</em> and not at all times</li>
 	<li>The consistency of data is relaxed. Data alterations are <em><strong>eventually</strong> </em>transferred to all replicas by propagating them <em><strong>asynchronously</strong> </em>over the connection network.</li>
 	<li>
<p id="InfLoff"><img class="alignnone wp-image-861 " src="/wp-content/uploads/2018/03/img_5aa78fbaa11f0.png" alt="" width="195" height="149" /></p>
</li>
 	<li>Issues: application components can possibly read obsolete information that has already been processed. Still, the component may choose to process the data again as changes cannot be seen.</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/data_abstractor/">Data Abstractor</a></h3>
<ul>
 	<li>The <strong>data</strong> provided <strong>to users or other application components is abstracted</strong> to inherently support eventually consistent data storage through the use of <strong><em>abstractions and approximations</em></strong>.</li>
 	<li>The style of data representation is adjusted to allow retrieved data to be eventually consistent.</li>
 	<li>The data representation always reflects that the <strong>consistent state is unknown</strong> by approximating values or abstracting them into more general ones, such as progress bars, traffic lights, or change tendencies (increase / decrease).</li>
 	<li>
<p id="XNXROjx"><img class="alignnone size-full wp-image-875 " src="/wp-content/uploads/2018/03/img_5aa7a80801ffe.png" alt="" /></p>
</li>
</ul>
&nbsp;
<h2><a href="http://www.cloudcomputingpatterns.org/message_oriented_middleware/">Message-oriented Middleware</a></h2>
<ul>
 	<li><strong>Communication partners (</strong>components of distributed application) exchange information <em><strong>asynchronously</strong> </em><strong>using messages</strong>.</li>
 	<li>Application components of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> are deployed in different Cloud Environments that form a <a href="http://www.cloudcomputingpatterns.org/hybrid_cloud/">Hybrid Cloud</a>.</li>
 	<li>When companies collaborate or one company has to integrate applications of different <strong>regional offices</strong>, different <strong>applications</strong> or the <strong>components</strong> of a <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Application</a> are distributed among different <strong>hosting environments</strong>.</li>
 	<li>Communication between these environments may be restricted and enabling communication may be hindered by corporate regulations.</li>
 	<li>Often, the integration with other cloud applications and non-cloud applications is also required</li>
 	<li>These environments often have different privacy, security, and trust properties.</li>
 	<li>The communication between environments is often restricted through the use of firewalls.</li>
 	<li>The message-oriented middleware handles the complexity of <strong>addressing</strong>, <strong>routing, availability</strong> of communication partners and <strong>message format</strong> transformation o make interaction robust and flexible</li>
 	<li>
<p id="eTaBqHT"><img class="alignnone wp-image-863 " src="/wp-content/uploads/2018/03/img_5aa7925ebe4ab.png" alt="" width="352" height="201" /></p>
</li>
</ul>
<h1><a href="http://www.cloudcomputingpatterns.org/integration_provider/">Integration Provider</a></h1>
<ul>
 	<li>Integration functionality such as messaging and shared data is hosted by a separate provider to enable integrate of otherwise separated hosting environments.</li>
 	<li>The Distributed Applications or their components communicate using integration components offered by a third party provider.</li>
 	<li><img class="" src="http://www.cloudcomputingpatterns.org/sketches/integration_provider_sketch.png" alt="Integration Provider" width="464" height="371" /></li>
</ul>
<h1>Message Mover</h1>
<ul>
 	<li>Messages are moved automatically between different cloud providers to provide unified access to application components using messaging.</li>
 	<li>If used message queues reside in different cloud environments that form a <a href="http://www.cloudcomputingpatterns.org/hybrid_cloud/">Hybrid Cloud</a> accessibility to <strong>queues of one environment may be restricted</strong> for application components that are deployed in another environment.</li>
 	<li>A Message Mover is used to integrate message queues hosted in different environments by receiving messages from one queue and transferring it to a queue in other environments.</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/message_mover_sketch.png" alt="Message Mover" /></li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/application_component_proxy/">Application Component Proxy</a></h3>
<ul>
 	<li>However, application components hosted in unrestricted environments may have to access application components hosted in a restricted environment.</li>
 	<li>The interface of a restricted application component is duplicated to form a proxy component.</li>
 	<li>Synchronous and asynchronous communication with this proxy component is initiated and maintained from the restricted environment that may access the unrestricted environment directly.</li>
 	<li><img src="http://www.cloudcomputingpatterns.org/sketches/application_component_proxy_sketch.png" alt="Application Component Proxy" /></li>
</ul>
&nbsp;
<h2>Reliability for distributed applications</h2>
Message duplicity is a very critical design issue for <a href="http://www.cloudcomputingpatterns.org/distributed_application/">Distributed Applications</a> and or application components that exchange messages via a <a href="http://www.cloudcomputingpatterns.org/message_oriented_middleware/">Message-oriented Middleware</a>.

Below definitions are quoted from <a href="http://doc.akka.io/docs/akka/current/scala/general/message-delivery-reliability.html" rel="nofollow noreferrer">Akka</a> Documentation
<ul>
 	<li><strong>at-most-once</strong> delivery means that for each message handed to the mechanism, that message is <strong>delivered zero or one</strong> times; in more casual terms it means that messages <strong>may be lost </strong>but <strong>not duplicated</strong>.
<ul>
 	<li>The first one is the <strong>cheapest</strong>—<strong>highest performance</strong>, <strong>least implementation</strong> overhead—because it can be done in a <strong>fire-and-forget fashion</strong> <strong>without keeping state</strong> at the sending end or in the transport mechanism.</li>
</ul>
</li>
 	<li><strong>at-least-once</strong> delivery means that for each message handed to the mechanism potentially <strong>multiple attempts</strong> are made at delivering it, such that at least one succeeds; again, in more casual terms this means that <strong>messages may be duplicated</strong> but <strong>not lost</strong>.
<ul>
 	<li>The second one requires retries to counter transport losses, which means <strong>keeping state at the sending end</strong> and having an <strong>acknowledgement mechanism</strong> at the receiving end.</li>
</ul>
</li>
 	<li><strong>exactly-once</strong> delivery means that for each message handed to the mechanism exactly one delivery is made to the recipient; the message can <strong>neither be lost nor duplicated</strong>.
<ul>
 	<li>The third is <strong>most expensive</strong>—and has consequently <strong>worst performance</strong>—because in addition to the second it <strong>requires state to be kept at the receiving end</strong> in order to <strong>filter out duplicate deliveries</strong>.</li>
</ul>
</li>
</ul>
&nbsp;
<h3><a href="http://www.cloudcomputingpatterns.org/exactly_once_delivery/">Exactly-once Delivery</a> and <a href="http://www.cloudcomputingpatterns.org/idempotent_processor/">Idempotent Processor</a></h3>
<ul>
 	<li>For many critical systems <em>duplicate messages are inacceptable</em>. The messaging system ensures that each <strong>message is delivered exactly once</strong> by filtering possible message duplicates <strong>automatically</strong>.</li>
 	<li>Upon creation, each message is associated with a unique message identifier. This identifier is used to filter message duplicates during their traversal from sender to receiver.</li>
 	<li>
<p id="hEzgzzx"><img class="alignnone size-full wp-image-862 " src="/wp-content/uploads/2018/03/img_5aa791167767d.png" alt="" /></p>
</li>
 	<li>The Idempotent Processor ensures that duplicate messages and inconsistent data do not affect application functionality
<ul>
 	<li>either through inconsistency detection identifying message duplicates and data inconsistencies
<ul>
 	<li>With non-idempotent operations, the algorithm may have to keep track of whether the operation was already performed or not</li>
 	<li>In REST The PUT and DELETE methods are defined to be idempotent.</li>
</ul>
</li>
 	<li>or through idempotent semantics of application functions enabling them to be erroneously executed multiple times with the same outcome.
<ul>
 	<li>idempotent is used more comprehensively to describe an operation that will produce the same results if executed once or multiple times</li>
 	<li>GET, HEAD, OPTIONS and TRACE methods are defined as safe</li>
</ul>
</li>
</ul>
</li>
 	<li id="kziAjxx"><img class="alignnone wp-image-869 " src="/wp-content/uploads/2018/03/img_5aa7993d56243.png" alt="" width="417" height="159" /></li>
</ul>
&nbsp;
<h3><a href="http://www.cloudcomputingpatterns.org/at_least_once_delivery/">At-least-once Delivery</a></h3>
<ul>
 	<li>In case of <strong>failures</strong> that lead to <strong>message loss</strong> or take <strong>too long to recover</strong> from, messages are retransmitted to assure they are delivered at least once.</li>
 	<li>For each message retrieved by a receiver an acknowledgement is sent back to the message sender. In case this <strong>acknowledgement is not received after a certain time frame, the message is resend</strong>.</li>
 	<li>Sometimes, message duplicity can be coped with by the application using a <a href="http://www.cloudcomputingpatterns.org/message_oriented_middleware/">Message-oriented Middleware</a>.</li>
 	<li>For scenarios where message duplicates are uncritical, it shall still be ensured that messages are received.</li>
 	<li>
<p id="eTqzxFs"><img class="alignnone size-full wp-image-864 " src="/wp-content/uploads/2018/03/img_5aa79342962b7.png" alt="" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/timeout_based_delivery/">Timeout-based Delivery</a> and <a href="http://www.cloudcomputingpatterns.org/timeout_based_message_processor/">Timeout-based Message Processor</a></h3>
<ul>
 	<li>ensure that messages are received successfully <strong><em>by at least one client</em></strong></li>
 	<li>Additionally, it shall be assured by the application that a message has also been properly processed after its reception.</li>
 	<li>Clients acknowledge message receptions to ensure that messages are received properly.</li>
 	<li>To assure that a message is properly received, it is not deleted immediately after it has been read by a client, but is only marked as being invisible. In this state a message may not be read by another client.</li>
 	<li>After a client has successfully read a message, it sends an acknowledgement to the message queue upon which reception the message is deleted.</li>
 	<li>
<p id="mvNzVrc"><img class="alignnone size-full wp-image-865 " src="/wp-content/uploads/2018/03/img_5aa794cd36e90.png" alt="" /></p>
</li>
 	<li>Instead of sending an acknowledgement right after receiving a message, a timeout-based message processor sends this acknowledgement after it has successfully processed the message.</li>
 	<li>If a message is not acknowledged after a certain timeout, it is processed by a different client.</li>
 	<li>
<p id="cbSCFDy"><img class="alignnone size-full wp-image-870 " src="/wp-content/uploads/2018/03/img_5aa79d5b6e218.png" alt="" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/transaction_based_delivery/">Transaction-based Delivery</a> and <a href="http://www.cloudcomputingpatterns.org/transaction_based_processor/">Transaction based processor</a></h3>
<ul>
 	<li>Clients retrieve messages under a transactional context to ensure that messages are received by a handling component.</li>
 	<li>The <a href="http://www.cloudcomputingpatterns.org/message_oriented_middleware/">Message-oriented Middleware</a> and the client reading a message from a queue participate in a transaction. All operations involved in the reception of a message are, therefore, performed under one transactional context guaranteeing ACID behavior.
<img class="alignnone size-full wp-image-866 " style="font-size: 1rem;" src="/wp-content/uploads/2018/03/img_5aa79539a3d81.png" alt="" /></li>
 	<li>However, using  <a href="http://www.cloudcomputingpatterns.org/transaction_based_delivery/">Transaction-based Delivery</a> approach no assurances can be made regarding the processing of that received message.</li>
 	<li>Transaction-based Processor: Components receive messages or read data and process the obtained information <strong>under a transactional context</strong> to ensure that all received messages are processes and all altered data is consistent after processing, respectively.</li>
 	<li>Transaction-based Delivery subsumes reading the message from a queue and deleting it from a queue in one transaction. The Transaction-based Processor extends the transactional context to the processing of the message in the receiver.</li>
 	<li>Analogous, if interacting with a storage offering, the Transaction-based Processor reads, processes and writes data in one transactional context.</li>
 	<li>
<p id="vytLTPS"><img class="alignnone size-full wp-image-871 " src="/wp-content/uploads/2018/03/img_5aa79f004be94.png" alt="" /></p>
</li>
</ul>
&nbsp;
