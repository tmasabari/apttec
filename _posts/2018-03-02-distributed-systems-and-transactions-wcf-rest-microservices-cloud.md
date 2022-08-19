---
layout: post
title: Distributed systems and Transactions - WCF, REST, MicroServices, Cloud
date: 2018-03-02 17:16
author: tmasabari
comments: true
categories: [Interview Preparation, Services, ServiceTransaction, Transactions, WCF]
---
<h2>Background</h2>
The intention of this article is to collect the notes on 'implementing different level of  transaction consistencies' and include my own experiences as quick refresh guide.
<ul>
 	<li>Data consistency in distributed- systems / databases / services</li>
 	<li>Handling failures in distributed systems</li>
</ul>
Distributed transactions are used very often in Service Oriented environments.
<ul>
 	<li>ACID transactions are simply not appropriate is when the work to be done cannot be performed in a very short period of time. This condition is pervasive in modern Service-Oriented Architecture (SOA) applications where the unit of work to be performed can span multiple service endpoints.</li>
 	<li>Another common scenario is a business process that might take seconds, minutes or even days or weeks to complete.</li>
</ul>
<ul>
 	<li>If you've a composite service calling multiple services, the underlying service calls should be handled as a single transaction. If the underlying resources allow for it, you can use 2-phase commits, but in many cases it is impossible.</li>
 	<li>Business processes should allow for a roll-back of their steps. In these cases compensating actions should be done on the services/resources invoked before the failed step.</li>
</ul>
<h2>Distributed Systems / Databases / Services</h2>
In a modern cloud application, there is a possibility of data stored on different cloud systems, different heterogeneous DBMS databases (RDBMS, NO SQL, Cube, Document Stores, Graphs) and different geographical regions. Reasons:
<ul>
 	<li>to improve <strong>scalability</strong> by balancing the load across multiple computers,</li>
 	<li>to improve response time by <strong>co-locating data</strong> close to the users and services that access it,</li>
 	<li>or to <strong>improve availability by replicating</strong> data across different sites.</li>
 	<li><strong>Polyglot Programming</strong>: applications should be written in a mix of languages to take advantage of different languages are suitable for tackling different problems</li>
 	<li><strong>Polyglot persistence</strong>: any decent sized enterprise will have a variety of different data storage technologies for different kinds of data
<ul>
 	<li>A new strategic enterprise application should no longer be built assuming a relational persistence support. The relational option might be the right one - but you should seriously look at other alternatives</li>
</ul>
</li>
</ul>
<h3>CAP Theorem</h3>
Distributed data stores are subject to the CAP Theorem. This theorem states that a distributed system can <strong>implement only two of the three features</strong> (Consistency, Availability, and Partition Tolerance) at any one time. In practice, this means that you can either:
<ul>
 	<li>Provide a <strong>consistent view of distributed (<em>partitioned</em>) data at the cost of blocking access</strong> to that data while any inconsistencies are resolved. This may take an indeterminate time, especially in systems that exhibit a high degree of latency or if a network failure causes loss of connectivity to one or more partitions.</li>
 	<li>Provide <strong>immediate access to the data at the risk of it being inconsistent across sites</strong>.</li>
</ul>
<h2>Transaction management for Distributed Systems</h2>
<ul style="list-style-type: circle;">
 	<li>WCF supports TransactionScope(<strong>Two-phase commit)</strong> for ACID Transactions.</li>
 	<li><strong>SOAP services with <a href="http://docs.oasis-open.org/ws-tx/wstx-wsat-1.2-spec.html">WS-AT</a></strong>. It's a solution with several moving parts, not much used in industry.</li>
 	<li>"X/Open CAE document <em class="citetitle">Distributed Transaction Processing: The XA Specification</em>" is published by The Open Group and available at <a class="ulink" href="http://www.opengroup.org/public/pubs/catalog/c193.htm" target="_top">http://www.opengroup.org/public/pubs/catalog/c193.htm</a>. XA supports distributed transactions, that is, the ability to permit multiple separate transactional resources to participate in a global transaction. Transactional resources often are RDBMSs but may be other kinds of resources. In essence, this extends ACID properties <span class="quote">“up a level”</span> so that multiple ACID transactions can be executed in concert as components of a global operation that also has ACID properties.</li>
 	<li><strong>Disadvantages of Two phase commit</strong>
<ul>
 	<li>ACID transaction are used to maintain database consistency by coordinating multiple database updates within a single request so that if an error occurs during processing, all database updates are rolled back for that request.</li>
 	<li>The issue is that strategies such as <strong>serialization and locking only work well if all application instances share the same data store</strong>, and the application is designed to ensure that the locks are very short-lived.</li>
 	<li>However, if data is partitioned or replicated across different data stores, locking and serializing data access to maintain consistency can become an expensive overhead that <strong>impacts the throughput, response time, and scalability of a system</strong>.</li>
 	<li>With service-based architectures it is extremely difficult to propagate and maintain a <strong>ACID </strong><strong>transaction context across multiple remote services.</strong></li>
 	<li>So Classic protocols are not an option (Ex: Two-phase commit) <span style="color: #ff0000;">Voting phase, Commit phase = Scalability issues
</span><img class="alignnone wp-image-689" src="/wp-content/uploads/2018/03/image1-300x76.png" alt="" width="343" height="87" /></li>
 	<li>2PC is not fail proof. There are situations the transaction simply can't complete. Then you need to identify and fix database inconsistencies manually. It may happen once in a million transactions if you're lucky, but it may happen once in every 100 transactions depending on your platform and scenario.</li>
 	<li><strong>Distributed transactions with REST services</strong>. REST services by definition are stateless, so they should not be participants in a transactional boundary that spans more than one service.</li>
</ul>
</li>
 	<li>Therefore, traditional DBMS/monoliths focus on providing strong consistency, whereas most modern distributed applications do not lock the data that they modify, and they take a rather more relaxed approach to consistency, known as <em>eventual</em> consistency.</li>
 	<li><em>Eventual consistency is <strong>unlikely</strong> to be specified as an explicit requirement</em> of a distributed system. Instead it is often a result of implementing a system that must exhibit scalability and high availability, which precludes most common strategies for providing strong consistency.</li>
</ul>
<h3>Alternatives to ACID</h3>
Not all data in an application has to be treated in the same way with respect to consistency. An application may <strong>implement different strategies for handling consistency across different data sets</strong>. The decision over which strategy and consistency model to use for any given dataset should be based on the business requirements of the application.
<ul>
 	<li><strong>BASE (Basic Availability, Soft-state, Eventual consistency)</strong>
<ul>
 	<li>When you deposit cash into your account through an ATM machine, it may take anywhere from several minutes to several hours for your money to appear in your account.</li>
 	<li>In other words, there is a soft transition state where <strong>the money has left your hands but has not reached your bank account</strong>. We are tolerant of this time lag and rely on soft state and eventual consistency, <strong>knowing and trusting</strong> that the money will reach our account at some point soon.</li>
 	<li>You can also leverage event-driven techniques to push notifications to consumers when the state of a request has become consistent. This technique adds a significant amount of complexity to an application, but helps in managing transactional state when using BASE transactions.</li>
 	<li><strong>Eventual consistency</strong>. Neither ACID-like distributed transactions nor compensating transactions are fail proof, and both may lead to inconsistencies. Eventual consistency is often better than occasional inconsistency, so you may create a more robust solution using asynchronous communication.</li>
 	<li>Async increases performance so prefer being async, send notifications by email at each major step whenever possible.</li>
</ul>
</li>
 	<li><strong>Refactor the services</strong> In situations where you simply cannot rely on eventual consistency and soft state and require transactional consistency, you can make your services more coarse-grained to encapsulate the business logic into a single service, allowing the use of ACID transactions to achieve consistency at the transaction-level.</li>
</ul>
<h2>Eventual Consistency</h2>
<ul>
 	<li>It is worth bearing in mind that an application may not actually require data to be consistent all of the time.</li>
 	<li><strong>For example</strong>, in a typical <strong>ecommerce web application</strong> that enables a user to browse and purchase goods, any stock levels presented to a user are likely to be static values determined when the details for a stock item are queried. If another concurrent user purchases the same item, the stock level in the system will decrease but this change will probably not need to be reflected in the data displayed to the first user. If the stock level drops to zero and the first user attempts to purchase the item, the system could <strong>either alert the user that the item is now out of stock, or place the item on back order and inform the user that the delivery time may be extended.</strong><img class="alignnone wp-image-707" src="/wp-content/uploads/2018/03/temp-300x256.png" alt="" width="428" height="366" /></li>
 	<li>Although these operations comprise a logical transaction, attempting to implement strong transactional consistency in this scenario is likely to be impractical.</li>
 	<li>Instead, implementing the order process as an eventually consistent<em> </em>series of steps, where each step in the process is essentially an autonomous operation, is a much more scalable solution.</li>
 	<li><strong>While these steps are progressing, the state of the overall system is inconsistent</strong>. For example, after the stock level has been updated but before the details of the order have been recorded the system has temporarily <em>lost</em> some stock. However, when all the steps have been completed, the system returns to a consistent state and all stock items can be accounted for.</li>
 	<li>
<h3 class="subheading">Problem 1: Failures in between the steps, Solution: Retrying Failing Steps</h3>
In a distributed environment, the inability to complete an operation is often due to <strong>some type of temporary error (communication failure is always a possibility.)</strong> If such a failure occurs, an application might assume that the situation is transient and simply attempt to repeat the step that failed. <strong>Less transient exceptions, such as database or virtual machine failure</strong>, may also occur and the remedy might be similar—wait for the system to be recovered and then try the failing operation again.</li>
 	<li>This approach could result in the same step actually being run twice, possibly resulting in multiple updates. It is very difficult to design a solution to prevent this repetition from occurring, but the application should attempt to render such repetition harmless.</li>
 	<li>A common technique is to associate the message sent to the service with a unique identifier. The service can store the identifier for each message it receives locally, and only process a message if the identifier does not match that of a message it received earlier. This technique is known as <em>de-duping</em> (the removal of duplicate messages). This strategy, exemplified by the <a href="http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.html">Idempotent Receiver</a> pattern, depends on the service being able to store message identifiers successfully.</li>
 	<li>
<h3 class="subheading">Problem 2: Concurrent Transactions tries to modify same data, Solution <a href="https://msdn.microsoft.com/en-gb/library/dn589792.aspx">Event Sourcing pattern</a></h3>
</li>
 	<li>You should try and partition your system to ensure that concurrent instances of an application attempting to perform the same operations simultaneously do not conflict with each other.</li>
 	<li>Rather than thinking in terms of simple CRUD (create, retrieve, update, and delete) operations, you can structure your system around atomic commands that perform business tasks in an idempotent style.</li>
 	<li>Event sourcing performs operations on data by driving tasks from a sequence of events, each of which is recorded in an append-only store.</li>
 	<li>
<h3 class="subheading">Problem 3: Handling transaction failure, Solution: Compensating Transaction pattern</h3>
</li>
 	<li>
<p class="subheading">There may ultimately be situations where the logic in the application determines that an operation cannot or should not be allowed to complete (this could be for a variety of business-specific reasons). In these cases you can implement compensating logic that undoes the work performed by the operation, as described by the <a href="https://msdn.microsoft.com/en-gb/library/dn589804.aspx">Compensating Transaction pattern</a>.
<img class="" src="/wp-content/uploads/2018/03/502.png" width="486" height="282" /></p>
</li>
 	<li> Compensating transactions can be <strong>complicated</strong> to implement and <strong>expensive</strong> to perform. You should <strong>only use</strong> them where they are <strong>absolutely necessary</strong>.</li>
 	<li>In Domain Driven Design (<strong class="markup--strong markup--p-strong">DDD</strong>) the pattern is well known as you need to apply it as soon as you have use cases involving multiple bounded contexts to collaborate. In the <strong class="markup--strong markup--p-strong">microservice </strong>community it is less known but necessary whenever an overall flow involves multiple services.</li>
 	<li>A common approach is to use a workflow to implement an eventually consistent operation that requires compensation. As the original operation proceeds, the system records information about each step and how the work performed by that step can be undone. If the operation fails at any point, the workflow rewinds back through the steps it's completed and performs the work that reverses each step.This approach is similar to the Sagas strategy discussed in <a href="http://vasters.com/clemensv/2012/09/01/Sagas.aspx" data-linktype="external">Clemens Vasters’ blog</a>.</li>
 	<li>This technique may be complicated by the fact that undoing a step may not be as simple as performing the exact opposite of the original step, and there may be additional business rules that the application must apply.</li>
 	<li>For example, undoing the step that records the details of an order in the document database may not be as straightforward as removing the document. For auditing purposes, it may be necessary to leave the original order document in place but change the status of the order in this document to “cancelled.”</li>
 	<li>A compensating transaction is also an eventually consistent operation and it could also fail. The system should be able to resume the compensating transaction at the point of failure and continue. It might be necessary to repeat a step that's failed, so the steps in a compensating transaction should be defined as idempotent commands.</li>
 	<li>In some cases it might not be possible to recover from a step that has failed except through manual intervention. In these situations the system should raise an alert and provide as much information as possible about the reason for the failure.</li>
 	<li>For SOAP services, if you have a BPEL engine you can benefit from this alternative, which is a better alternative for long-running transactions. There are other frameworks/platforms that support compensation, but BPEL is probably the most common one. But compensation is not fail proof either. You may still end up with inconsistencies (= headache).</li>
</ul>
<h2>BPEL, orchestration and choreography</h2>
<ul>
 	<li>The <b>Web Services Business Process Execution Language</b> (<b>WS-BPEL</b>), commonly known as <b>BPEL</b> (<b>Business Process Execution Language</b>), is an <a title="OASIS (organization)" href="https://en.wikipedia.org/wiki/OASIS_(organization)">OASIS</a><sup id="cite_ref-1" class="reference"><a href="https://en.wikipedia.org/wiki/Business_Process_Execution_Language#cite_note-1"> </a></sup>standard executable language for specifying actions within <a title="Business process" href="https://en.wikipedia.org/wiki/Business_process">business processes</a> with <a title="Web service" href="https://en.wikipedia.org/wiki/Web_service">web services</a>. Processes in BPEL export and import information by using web service interfaces exclusively.</li>
 	<li>BPEL is an <a class="mw-redirect" title="Orchestration (computers)" href="https://en.wikipedia.org/wiki/Orchestration_(computers)">orchestration</a> language, and not a <a class="mw-redirect" title="Web Service Choreography" href="https://en.wikipedia.org/wiki/Web_Service_Choreography">choreography</a> language.</li>
 	<li>The primary difference between orchestration and choreography is executability and control.</li>
 	<li>An orchestration specifies an executable process that involves message exchanges with other systems, such that the message exchange sequences are c<strong>ontrolled by the orchestration designer</strong>.</li>
 	<li>A choreography specifies a protocol for <strong>peer-to-peer interactions</strong>, defining, e.g., the legal sequences of messages exchanged with the purpose of guaranteeing interoperability. Such a protocol is not directly executable, as it allows many different realizations (processes that comply with it).</li>
 	<li>A choreography can be realized by writing an orchestration (e.g., in the form of a BPEL process) for each peer involved in it.</li>
 	<li>The orchestration and the choreography distinctions are based on analogies: orchestration refers to the central control (by the conductor) of the behavior of a distributed system (the orchestra consisting of many players), while choreography refers to a distributed system (the dancing team) which operates according to rules (the choreography) but without centralized control.</li>
 	<li>This usage of <i>orchestration</i> is often discussed in the context of <a title="Service-oriented architecture" href="https://en.wikipedia.org/wiki/Service-oriented_architecture">service-oriented architecture</a>, <a class="mw-redirect" title="Platform virtualization" href="https://en.wikipedia.org/wiki/Platform_virtualization">virtualization</a>, <a title="Provisioning" href="https://en.wikipedia.org/wiki/Provisioning">provisioning</a>, <a class="mw-redirect" title="Converged Infrastructure" href="https://en.wikipedia.org/wiki/Converged_Infrastructure">converged infrastructure</a> and <b>dynamic datacenter</b> topics. Orchestration in this sense is about aligning the business request with the applications, data, and infrastructure.<sup id="cite_ref-2" class="reference"><a href="https://en.wikipedia.org/wiki/Orchestration_(computing)#cite_note-2">[2]</a></sup></li>
 	<li>It defines the policies and service levels through automated workflows, provisioning, and change management. This creates an application-aligned infrastructure that can be scaled up or down based on the needs of each application.</li>
 	<li>Orchestration also provides centralized management of the resource pool, including billing, metering, and chargeback for consumption. For example, orchestration reduces the time and effort for deploying multiple instances of a single application. And as the requirement for more resources or a new application is triggered, automated tools now can perform tasks that previously could only be done by multiple administrators operating on their individual pieces of the physical stack.<sup id="cite_ref-3" class="reference"><a href="https://en.wikipedia.org/wiki/Orchestration_(computing)#cite_note-3">[3]</a></sup></li>
</ul>
&nbsp;
<h3>X/Open Distributed Transaction Processing (DTP) standard</h3>
&nbsp;
<p style="font-weight: 400;">This is a popular distributed transaction standard. The architecture diagram (from Kosaraju, javaworld.com):</p>
<p id="WaxUNJc"><img class=" wp-image-1067  aligncenter" src="/wp-content/uploads/2018/03/img_5aaf1dddf349e.png" alt="" width="386" height="333" /></p>
<p style="font-weight: 400;">The <strong>Transaction Manager</strong> manages the transaction: manage transaction context, maintain associations with participating resources, conduct 2PC and recovery protocol. You can use open source transaction manager such as Atomikos. Transaction manager is also included in enterprise platforms such as Weblogic.</p>
<p style="font-weight: 400;">The<strong> Resource manager</strong> is a wrapper over a resource (e.g. database, JMS message broker) that implements XA interface for participating in transactions with a transaction manager. The transaction manager keeps track which resources that are participating in the transaction using resource enlistment process. For example in the case of Oracle database you get the resource manager by using an XA capable Oracle JDBC database driver.</p>
<p style="font-weight: 400;"><strong>TX interface</strong> is the interface between your application and the transaction manager. The important methods in this interface are such as for transaction demarcation  (e.g. begin, rollback, commit).</p>
<p style="font-weight: 400;"><strong>XA interface</strong> is the interface between resource managers and the transaction manager. The important methods in this interface are such as start, end, prepare (the first phase of 2PC), and commit  (the second phase of 2PC),.</p>
<p style="font-weight: 400;">For more details please read the article by Allamaraju (see the references below.)</p>

<h2 class="heading">Related Patterns and Guidance</h2>
The following patterns and guidance may also be relevant when managing consistency in a cloud application:
<ul>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589804.aspx">Compensating Transaction Pattern</a>. This pattern describes how to undo the work performed by a series of steps, which together define an eventually consistent operation, if one or more of the operations fail.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn568103.aspx">Command and Query Responsibility Segregation Pattern</a>. This pattern describes how you can segregate the operations that read data from the operations that update data. This pattern can use different models of the same data, and it is necessary to ensure that the information in these models can become consistent.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589792.aspx">Event Sourcing Pattern</a>. This pattern is frequently used with the Command and Query Responsibility Segregation pattern. It can simplify tasks in complex domains; improve performance, scalability, and responsiveness; provide consistency for transactional data; and maintain full audit trails and history that may enable compensating actions.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589795.aspx">Data Partitioning Guidance</a>. In many large-scale applications, data is divided into separate partitions that can be managed and accessed separately. It may be necessary to ensure that the data is consistent across partitions.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589787.aspx">Data Replication and Synchronization Guidance</a>. Data replication and synchronization can help to maximize availability and performance, ensure consistency, and minimize data transfer costs between locations.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589802.aspx">Caching Guidance</a>. Data in application caches can become inconsistent across instances and with the data store that acts as the original source of the data. This guidance describes how caches may support expiration policies that can help to reduce the period during which cached data is inconsistent.</li>
 	<li><a href="https://msdn.microsoft.com/en-gb/library/dn589799.aspx">Cache-Aside Pattern</a>. This pattern describes how to fetch data into a cache on demand, as the data is required by an application. It can be used to good effect to reduce the overhead associated with repeatedly accessing the same data.</li>
</ul>
<h2>References</h2>
<ul>
 	<li>https://en.wikipedia.org/wiki/Business_Process_Execution_Language</li>
 	<li>https://nofluffjuststuff.com/magazine/2015/10/the_challenges_of_service_based_architecture</li>
 	<li>https://stackoverflow.com/questions/30213456/transactions-across-rest-microservices</li>
 	<li>Orchestration pattern http://arnon.me/soa-patterns/Orchestration/</li>
 	<li>https://blog.bernd-ruecker.com/saga-how-to-implement-complex-business-transactions-without-two-phase-commit-e00aa41a1b1b</li>
 	<li>Saga pattern http://www.rgoarchitects.com/Files/SOAPatterns/Saga.pdf</li>
 	<li>http://vargas-solar.com/cloud-data-management/wp-content/uploads/sites/11/2013/04/IIa-PolyGlot-persistence1.pdf</li>
 	<li>The guide <a href="https://msdn.microsoft.com/library/dn271399.aspx">Data Access for Highly-Scalable Solutions: Using SQL, NoSQL, and Polyglot Persistence</a> on MSDN.</li>
 	<li>The <a href="http://www.enterpriseintegrationpatterns.com/IdempotentReceiver.html">Idempotent Receiver</a> pattern by Gregor Hohpe and Bobby Woolf on the Enterprise Integration Patterns website.</li>
 	<li>The article <a href="http://blog.jonathanoliver.com/2010/04/idempotency-patterns/">Idempotency Patterns</a> on Jonathan Oliver’s blog.</li>
 	<li><a href="https://msdn.microsoft.com/library/jj591577.aspx">Reference 4: A CQRS and ES Deep Dive</a> on MSDN.</li>
 	<li>The article <a href="http://queue.acm.org/detail.cfm?id=1466448">Eventually Consistent</a> on the ACM website.</li>
 	<li><a href="http://en.wikipedia.org/wiki/CAP_theorem">CAP Theorem</a> on Wikipedia.</li>
 	<li><a href="https://www.microsoft.com/en-us/download/details.aspx?id=34774">Book Download: Exploring CQRS and Event Sourcing</a></li>
 	<li>Orchestration https://blog.sandro-pereira.com/2009/08/15/what-are-the-different-types-of-transactions-available-for-orchestration/</li>
 	<li>Nuts and Bolts of Transaction Processing by Allamaraju
<a href="http://www.subbu.org/articles/transactions/NutsAndBoltsOfTP.html">http://www.subbu.org/articles/transactions/NutsAndBoltsOfTP.html</a>
<a href="http://www.subbu.org/articles/jts/JTS.html">http://www.subbu.org/articles/jts/JTS.html</a></li>
</ul>
