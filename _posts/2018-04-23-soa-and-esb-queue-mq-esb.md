---
layout: post
title: SOA and ESB Queue, MQ, ESB
date: 2018-04-23 12:49
author: tmasabari
comments: true
categories: [Architecture, EnterpriseIntegration, MessageBroker, ServiceBus]
---
<ul style="text-align: justify;">
 	<li><strong>SOA is an architectural pattern</strong> where you expose 'services'
<ul>
 	<li>in a coarse (SOAP) grained or</li>
 	<li>fine (RESTFul) grained manner.</li>
</ul>
</li>
 	<li>It does <strong>not prescribe any implementation</strong> details.</li>
 	<li>It is a <strong>lightweight interaction between systems</strong> that speak HTTP (the most common SOA use case).</li>
 	<li>A service bus is an <strong>actual implementation</strong> – one that relies on a ‘bus’ construct. The ‘bus’ encompasses SOA as potential endpoints</li>
 	<li>Typically, you would need a point-point connection between the client and the SOAP service – and another one between the client and the RESTFul service. This can quickly become a maintenance nightmare, as each service would require it’s own error handling, audit logs etc.</li>
</ul>
<ul style="text-align: justify;">
 	<li>The quick rundown
<ul>
 	<li>Message Queues for asynchronous communication in your system</li>
 	<li>Message Brokers for loosely coupled components</li>
 	<li>Integration frameworks if you need to make them understand each other first</li>
 	<li>ESBs if you’re facing a zoo of services and tricky requirements (e.g. governance)</li>
 	<li>Integration suites if you need BPM or MDM in the picture</li>
</ul>
</li>
</ul>
<ul style="text-align: justify;">
 	<li>Message transports / Queues
<ul>
 	<li>transports - Dumb -  just pushing data around from A to B. Examples are Thrift, ICE, CORBA or ZeroMQ (0mq being a bit special, as it has some features of the next higher layer).</li>
 	<li>Queues are dumb too. You push stuff in and take stuff out eventually. That’s it. Examples are Pipes, ring-buffers, stacks or even DBs (e.g. Redis) can be used for this.</li>
 	<li>primitive building blocks</li>
 	<li>Queues are great for asynchronous operations, where the time between pushing and removing doesn’t matter so much, but messages should never be lost (as queues can be implemented as persistent storage), while message transport are great when the delay should be minimal or you want to fan out to a large audience - guarantees for delivery may be available, too - to a certain extent.</li>
</ul>
</li>
 	<li>Message queues -few features on top of the queue implementation
<ul>
 	<li>Durability (resilience)</li>
 	<li>Policies (e.g. message TTL, terms of delivery, batching, etc)</li>
 	<li><strong>Security</strong> (access control)</li>
 	<li><strong>Routing</strong> (pub/sub, point-to-point, etc.)</li>
</ul>
</li>
 	<li>Message brokers
<ul>
 	<li>provide loose coupling between components without necessarily being asynchronous or queue-based at all.</li>
 	<li>Message brokers aim primarily for decoupling and help <strong>integrating different components</strong>, without having to know too much about your communication partners. For this to work, they provide the transformation functionality to make sure the peers can understand each other.</li>
 	<li>few additional services on top of their lower layer:
<ul>
 	<li>Routing, Durability (resilience), Security, Policies</li>
 	<li>Multiplexing / De-multiplexing (i.e. aggregation and decomposition of messages from/into multiple messages to different receipients)</li>
 	<li>Transformation (translation of messages between formats)</li>
</ul>
</li>
 	<li>Here things usually get blurry - many solutions are both (message queue and message broker) - for example <strong>RabbitMQ or QDB.</strong></li>
 	<li>Samples for message queues are <strong>Gearman, IronMQ, JMS, SQS or MSMQ.</strong></li>
 	<li>Message broker examples are <strong><strong>Qpid, Open AMQ or ActiveMQ.</strong></strong></li>
</ul>
</li>
 	<li>Integration frameworks
<ul>
 	<li>Integration frameworks are basically <strong>specialized message brokers</strong> for integrating different pieces of software with each other.</li>
 	<li>They usually ship with a selection of connectors (e.g. <strong>FTP, HTTP, AMQP, SMTP and what not</strong>). They may also support some enterprise application integration patterns (<a href="https://t.umblr.com/redirect?z=http%3A%2F%2Fwww.eaipatterns.com%2F&amp;t=YzJjMWI1NjA2OWY2MzIyMmI1MWM4ODhlODcyNTUyYjM0ZjFhYWU1YSw2WjZseDZXcQ%3D%3D&amp;b=t%3AlieMaBJ-gXaoraD17KneAg&amp;p=http%3A%2F%2Fox86.tumblr.com%2Fpost%2F76315629526%2Fdo-you-know-the-difference-between-queue-mq-esb&amp;m=1">EAI patterns</a>).</li>
 	<li>Examples for those beasts are <strong>Spring Integration Framework or Apache Camel</strong>.</li>
 	<li>These are great if you’re going to make different systems talk to and understand each other. If you’re building something that speaks the same language anyway, you may be better off with a message queue or message broker, I guess.</li>
</ul>
</li>
 	<li>Enterprise Service Buses -widely-used buzzword.
<ul>
 	<li>In addition to the integration framework it provides:
<ul>
 	<li>Monitoring of the services and the messages passed between them</li>
 	<li>Deployment and service version controlling</li>
 	<li>Scheduling, mapping, QoS management, error handling and more</li>
 	<li>load balancing between services of the same type and concurrency control</li>
</ul>
</li>
 	<li>Samples for ESBs are <strong>Apache ServiceMix or Synapse, BizTalk, JBoss ESB, Open ESB or Mule</strong>.</li>
</ul>
</li>
 	<li>Integration Suites
<ul>
 	<li>integration suites are basically ESBs with business process logic on top.
<ul>
 	<li>BPM integration</li>
 	<li><a href="https://t.umblr.com/redirect?z=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FMaster_data_management&amp;t=ZmY3YzUxOWZkZTMyMWMzODk2YjJlZDNiZjM0OWE3MGYxYTZlNTBiMiw2WjZseDZXcQ%3D%3D&amp;b=t%3AlieMaBJ-gXaoraD17KneAg&amp;p=http%3A%2F%2Fox86.tumblr.com%2Fpost%2F76315629526%2Fdo-you-know-the-difference-between-queue-mq-esb&amp;m=1">MDM</a> services</li>
</ul>
</li>
</ul>
</li>
</ul>
<p style="text-align: justify;">References</p>

<ul style="text-align: justify;">
 	<li>http://ox86.tumblr.com/post/76315629526/do-you-know-the-difference-between-queue-mq-esb</li>
</ul>
<p style="text-align: justify;">Quotes</p>
<p style="text-align: justify;">“There are 2 hard problems in computer science: caching, naming, and off-by-1 errors”</p>
<p style="text-align: justify;">– Phil Karlton</p>
