---
layout: post
title: Microservices
date: 2018-03-30 10:31
author: tmasabari
comments: true
categories: [Architecture, Indexes, MicroServices, Prepare, QuickRefresh, Todo]
---
<h2>Must read</h2>
<ul>
 	<li><a href="Free%20eBook/Guide on ‘.NET Microservices – Architecture for Containerized .NET Applications’">Microsoft Free ebook - .NET Microservices. Architecture for Containerized .NET Applications</a></li>
 	<li><a href="http://microservices.io/index.html">http://microservices.io/index.html</a></li>
 	<li><a href="https://github.com/ThreeMammals/Ocelot">Ocelot is a .NET Api Gateway.</a></li>
 	<li></li>
 	<li><a href="https://www.slideshare.net/rbanks54/architecting-microservices-in-net">https://www.slideshare.net/rbanks54/architecting-microservices-in-net</a></li>
 	<li>In practice <a href="file:///C:/ArthanariS/OneDrive%20-%20Virtusa/architecture%20diagrams/netmeetforit-microservices-160310091120.pdf">file:///C:/ArthanariS/OneDrive%20-%20Virtusa/architecture%20diagrams/netmeetforit-microservices-160310091120.pdf</a></li>
 	<li><a href="https://www.slideshare.net/spnewman/principles-of-microservices-xp-days-ukraine">Principles</a></li>
 	<li><a href="https://www.microsoft.com/net/learn/architecture">Microsoft</a></li>
</ul>
References
<ul>
 	<li><a href="https://www.javacodegeeks.com/2014/06/microservice-architecture-a-quick-guide.html">https://www.javacodegeeks.com/2014/06/microservice-architecture-a-quick-guide.html</a></li>
</ul>
<h2>1. What is Architecture (Software)?</h2>
Architecture is the fundamental organization of a system embodied in its components (i.e. Web Server, Application Server, Databases,Storage, Communication layer, etc…), their relationships to each other, and to the environment (i.e. deployment environment shared server, dedicated server, cloud deployment, etc..), and the principles guiding its design and evolution.
<h2>2. What is microservice architecture ?</h2>
Microservice means developing a <strong>single, small, meaningful functional feature as single service</strong>, each service has it’s own process and communicate with lightweight mechanism, deployed in single or multiple servers.
<h2>3. Advantages of microservice architecture ?</h2>
<ul>
 	<li>Each micro service is small and focused on a <strong>specific feature / business requirement</strong>.
<ul>
 	<li>Microservice has code for business logic only, No mixup with HTML,CSS or other UI component.</li>
 	<li>Every microservice has it’s own storage capability but it depends on the project’s requirement, you can have common database like MySQL or Oracle for all services.</li>
 	<li>Microservice can deploy on commodity hardware or low / medium configuration servers</li>
</ul>
</li>
 	<li>Microservice can be <strong>developed independently by small team</strong> of developers (normally 2 to 5 developers).
<ul>
 	<li>The productivity of a new team member will be quick enough.</li>
</ul>
</li>
 	<li>Microservice is <strong>loosely coupled</strong>, means services are independent, in terms of development and deployment both.
<ul>
 	<li>Microservice is easy to understand, modify and maintain for a developer because separation of code,small team and focused work.</li>
 	<li>Microservice is easy to scale based on demand.</li>
</ul>
</li>
 	<li>Microservice can be developed using <strong>different programming language</strong> (Personally I don’t suggest to do it).
<ul>
 	<li>Microservice allows you to take advantage of emerging and latest technologies (framework, programming language , programming practice, etc.).</li>
 	<li>Easy to integrate 3rd party service.</li>
</ul>
</li>
 	<li>Microservice allows easy and flexible way to <strong>integrate automatic deployment</strong> with Continuous Integration tools (for e.g: <a href="http://jenkins-ci.org/" target="_blank" rel="nofollow noopener">Jenkins</a>, <a href="http://hudson-ci.org/" target="_blank" rel="nofollow noopener">Hudson</a>, <a href="https://www.atlassian.com/software/bamboo" target="_blank" rel="nofollow noopener">bamboo</a> etc..).</li>
</ul>
<h2>4. Disadvantages of microservice architecture ?</h2>
<ul>
 	<li>Microservice architecture brings a lot of operations overhead.</li>
 	<li>DevOps Skill required (<a href="http://en.wikipedia.org/wiki/DevOps" target="_blank" rel="nofollow noopener">http://en.wikipedia.org/wiki/DevOps</a>).</li>
 	<li>Duplication of Effort.</li>
 	<li>Distributed System is complicated to manage .</li>
 	<li>Default to trace problem because of distributed deployment.</li>
 	<li>Complicated to manage whole products when number of services increases.</li>
</ul>
<h2>5. In which case / requirement microservice architecture best fit ?</h2>
When you need to support Desktop, web , <strong>mobile, Smart TVs, Wearable, etc</strong>… or <strong>you don’t know in future</strong> which kind of devices you need to support.
<h2>6. Which products / companies are using Microservie architecture?</h2>
Most large scale web sites including Twitter, Netflix, Amazon and eBay have evolved from a monolithic architecture to a microservices architecture.
<h2>7. How independent micro services communicate with each other?</h2>
It’s depend upon requirement, normally developers use HTTP/<a href="http://en.wikipedia.org/wiki/Representational_state_transfer" target="_blank" rel="nofollow noopener">REST</a> with <a href="http://en.wikipedia.org/wiki/JSON" target="_blank" rel="nofollow noopener">JSON</a> or <a href="http://en.wikipedia.org/wiki/Protocol_Buffers" target="_blank" rel="nofollow noopener">Protobuf</a>(Binary protocol) but are free to use any communication protocol.
<h2>8. Why is it that everyone are talking about microservices now?</h2>
It’s been nearly 15 years since the concept of SOA really took hold. With the improvement of <strong>RESTful web service and JSON</strong> as a data interchange format has made it easier than ever to <strong>build easily interconnectable services simply and quickly</strong>.

&nbsp;
<h2>When to use?</h2>
One of the fundamental concepts to remember is that microservices architecture is a share-as-little-as-possible architecture pattern that places a heavy emphasis on the concept of a bounded context, whereas SOA is a share-as-much-as-possible architecture pattern that places heavy emphasis on abstraction and business functionality reuse.

&nbsp;
<h3>API Gateways</h3>
<a href="https://dzone.com/articles/microservices-communication-zuul-api-gateway-1">Why</a>

<a href="https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/architect-microservice-container-applications/direct-client-to-microservice-communication-versus-the-api-gateway-pattern">Microsoft Link</a>
<p id="YVNlxsV"><img class="wp-image-1387  alignright" src="/wp-content/uploads/2018/03/img_5abdab11d1414.png" alt="" width="335" height="196" /></p>

<ul>
 	<li>The crux of the microservices pattern is to create an independent service which can be scaled and deployed independently.</li>
 	<li>A direct client-to-microservice communication architecture could be good enough for a small microservice-based application, especially if the client app is a server-side web application like an ASP.NET MVC app.</li>
 	<li>But in a complex business domain, more than <strong>50-100 microservices</strong> is very common.</li>
 	<li><em>How can client apps minimize the number of requests to the backend and reduce chatty communication to multiple microservices?</em>
<ul>
 	<li>Interacting with multiple microservices to build a single UI screen increases the <strong>number of roundtrips</strong> across the Internet. This <strong>increases latency and complexity</strong> on the UI side.</li>
 	<li><strong>encapsulation</strong>: So the UI client has to know the details of all REST API and URL patterns/ports to call them. It is kind of a breach of encapsulation</li>
</ul>
</li>
 	<li class=""><em>How can you handle cross-cutting concerns such as CORS, <strong>authentication, security, monitoring, </strong><strong>authorization, data transformations, and dynamic request dispatching</strong>?</em>
<ul>
 	<li>Traditionally each microservice team has to <strong>develop all these aspects into its own service,</strong> so the same code has been replicated over fifty microservices. Changes in the requirements or policy will ripple over all services.<strong> It is against the DRY principle,</strong> so this type of design is very error-prone and rigid.</li>
 	<li> A <strong><em>man-in-the-middle </em>approach can help</strong> in this situation. We have only one entry point where all common aspects code is written and the client communicates with that common service</li>
</ul>
</li>
 	<li><em class="">How can you shape a <strong>façade</strong> especially made for <strong>mobile apps</strong>?</em>
<ul>
 	<li>The needs of a mobile app might be different than the needs of a web app.</li>
 	<li>For mobile apps, you might need to<strong> optimize even further</strong> so that data responses can be more efficient. You might do this by a<strong>ggregating data from multiple microservices and returning a single set of data</strong>, and</li>
 	<li>sometimes <strong>eliminating any data</strong> in the response that is not needed by the mobile app.</li>
 	<li>And, of course, you might <strong>compress that data</strong>.</li>
 	<li>Again, a façade or API in between the mobile app and the microservices can be convenient for this scenario.</li>
</ul>
</li>
</ul>
<a href="https://medium.com/@anil789/api-gateway-and-its-nuances-766b7beecb19">What</a>
<p id="hGrLxKX"><img class="wp-image-1386  aligncenter" src="/wp-content/uploads/2018/03/img_5abdaaeed79cb.png" alt="" width="486" height="268" /></p>

<ul>
 	<li>It is similar to the<strong> <a href="https://en.wikipedia.org/wiki/Facade_pattern" data-linktype="external">Facade pattern</a> </strong>from object‑oriented design, but in this case, it is part of a distributed system.</li>
 	<li>An API gateway or Edge service is an <strong>abstraction layer</strong> which <strong>receives all the requests coming from the UI</strong> and then <strong>delegates the requests to internal microservices</strong>. So, we have to create a brand new microservice sits on top of all other microservices.</li>
 	<li>As the Edge service itself is a microservice, it can be independently scalable and deployable, so we can perform some load testing, also.</li>
</ul>
<p id="89d7" class="graf graf--p graf-after--p"><a href="https://medium.com/@anil789/api-gateway-and-its-nuances-766b7beecb19">Functionalities</a>:</p>

<ol class="postList">
 	<li id="4b96" class="graf graf--li graf-after--p"><strong>Mapping external requests’ UR</strong>L: It maps external URLs to internal URLs <strong>using a table, service discovery service, DNS</strong> etc.
<ol>
 	<li><strong class="markup--strong markup--li-strong">Long term service discovery needs</strong>: API gateway should be able to <strong>discover services using different mechanism</strong>. Some services may be external with well known URLs and ip-addresses, others may be dynamic in nature. In a <strong>multi-cloud environment,</strong> service discovery needs may vary.</li>
</ol>
</li>
 	<li id="631c" class="graf graf--li graf-after--li"><strong>Security</strong>: It enforces security such as<strong> CSRF, XSS, access control, authorization, IP whitelist / blacklist enforcement, detection of anomalies v/s historical usage patterns</strong>.</li>
 	<li id="38fc" class="graf graf--li graf-after--li">Building logs of<strong> interactions with client for audit</strong> and troubleshooting.</li>
 	<li id="8660" class="graf graf--li graf-after--li">API metering: Meters API requests,<strong> permit or deny request based on threshold limits</strong>.</li>
 	<li id="f54c" class="graf graf--li graf-after--li">Analytics: Creates a logs of timing, rate, failure etc. for analytics purpose.</li>
 	<li id="3ae5" class="graf graf--li graf-after--li"><strong>Documentation</strong>: API Gateway can also serve documentation and examples of API.</li>
 	<li><strong class="markup--strong markup--li-strong">API Trace</strong>: Since API Gateway is the first point of interaction with the client, it can tag each request with a <strong>unique tracking id</strong>. If down-stream services use this tag in log messages and also <strong>propagate it while calling other services</strong>, it can be used to <strong>trace the API call end-to-end</strong>.
<ol>
 	<li>This is very useful for debugging, troubleshooting, audit and analytics.</li>
 	<li>You can also build analytics / monitoring tool / search based on tracking id.</li>
 	<li>By adding time, user session info (which user) you can make it very useful trouble shooting / debugging tool.</li>
</ol>
</li>
 	<li><strong class="markup--strong markup--li-strong">API Orchestrator</strong>: API Gateway should be generic.<strong> Any custom code should be avoided</strong> in it. But <strong>there are use-cases when it is needed</strong> that the server abstracts a number of API calls into one. Such abstraction may be needed for simplicity, performance etc. reasons. Such a functionality should be provided by a special service called <strong>API Orchestrator</strong>.</li>
</ol>
Drawbacks
<ol>
 	<li>Consider API Gateway as separate tier
<ol>
 	<li>you are coupling that tier with the internal microservices.</li>
 	<li>consider multiple instances for availability and avoid single point of failure.</li>
 	<li>If not scaled out properly, the API Gateway can become a bottleneck.</li>
 	<li>An API Gateway can introduce increased response time due to the additional network call. However, this extra call usually has less impact than having a client interface that is too chatty directly calling the internal microservices.</li>
 	<li>Developers must update the API Gateway in order to expose each microservice’s endpoints.</li>
 	<li>If you have custom logic
<ol>
 	<li>requires additional development cost and future maintenance if it includes custom logic and data aggregation.</li>
 	<li>Moreover, implementation changes in the internal microservices might cause code changes at the API Gateway level.</li>
</ol>
</li>
</ol>
</li>
</ol>
<h3></h3>
<h3>Application scope</h3>
Application scope refers to the overall size of the application that an architecture pattern can support.
<ul>
 	<li>SOA is well-suited for<strong> large, complex, enterprise-wide systems</strong> that require integration with many <strong>heterogeneous applications</strong> and services. It is also well-suited for applications that have many shared components, particularly components that are shared across the enterprise. As such, SOA tends to be a good fit for large insurance companies due to the heterogeneous systems environment and the sharing of common services—customer, claim, policy, etc.—across multiple applications and systems.</li>
 	<li>The microservices pattern is better suited for<strong> smaller, well partitioned web-based systems</strong> rather than large-scale enterprise  wide systems. The lack of a mediator (messaging middleware) is one of the factors that makes it ill-suited for large-scale complex business application environments. Other examples of applications that are well-suited for the microservices architecture pattern are ones that have few shared components and ones that can be broken down into very small discrete operations.</li>
 	<li>However, workflow-based applications that have a well-defined processing flow and not many shared components (such as securities trading) are difficult to implement using the SOA architecture pat‐ tern.</li>
 	<li>Small web-based applications are also not a good fit for SOA because they don’t need an extensive service taxonomy, abstraction layers, and messaging middleware components.</li>
</ul>
<h3>Heterogeneous Interoperability</h3>
Heterogeneous interoperability refers to the ability to integrate with systems implemented in different programming languages and plat‐ forms.  The ability to integrate with multiple heterogeneous systems and services is one of the few areas where microservices architecture takes a back seat to SOA.
<ul>
 	<li>Many banking and insurance systems still have a majority of the backend core processing in COBOL mainframe applications that must be accessed by modern web-based platforms.</li>
 	<li>For example, you might have a situation in which a single complex business request requires the coordination of a Java-based application, a .NET application, and a Customer Information Con‐ trol System (CICS) COBOL program to process the single request.</li>
 	<li>Other examples include a trading application implemented in the .NET platform that needs to access an AS400 to perform compli‐ ance checks on a stock trade, and a Java-based retail shop that needs to integrate with a large third-party .NET warehousing system. These examples are found everywhere in most large companies.</li>
 	<li>The microservices architecture style <strong>supports protocol-aware heterogeneous interoperability.</strong> With protocol-aware heterogeneous interoperability, the architecture can support multiple types of remote access protocols, but the communication between a particular ser‐ vice consumer and the corresponding service that it’s invoking must be the same (e.g., REST).</li>
 	<li>With REST, for example, the service consumer could easily be implemented in C# with .NET, whereas the service could be implemented in Java. However, with microservices, the protocol between the service consumer and ser‐ vice must be the same because there is no central middleware com‐ ponent to transform the protocol.</li>
 	<li>With protocol-agnostic het‐ erogeneous interoperability, the service consumer is ignorant not only of the implementation of the service, but also of the protocol the service is listening on.Being able to translate the consumer protocol to the service protocol known as protocol transformation is supported through the use of a messaging middleware component.
<a href="/wp-content/uploads/2017/12/image-3.png"><img style="display: inline; background-image: none;" title="image" src="/wp-content/uploads/2017/12/image_thumb-3.png" alt="image" width="260" height="241" border="0" /></a></li>
</ul>
&nbsp;
<h3>Contract Decoupling</h3>
<ul>
 	<li>Contract decoupling is a very powerful capability that provides the highest degree of decoupling between service consumers and serv‐ ices. This capability allows services and service consumers to evolve independently from each other while still maintaining a contract between them. It also helps give your service consumers the ability to drive contract changes using consumer-driven contracts, thereby creating a more collaborative relationship between the service and the service consumer.</li>
 	<li>abstracting the interfaces and contracts through contract decoupling allows the IT department to make technology changes with no impact on the business applications across the enterprise.</li>
 	<li>There are two primary forms of contract decoupling: message trans‐ formation and message enhancement. Message transformation is concerned only about the format of the message, not the actual request data. For example, a service might require XML as its input format, but a service consumer decides to send JSON payload instead. This is a straightforward transformation task that is handled very nicely by most of the open source integration hubs, including Apache Camel, Mule, and Spring Integration.</li>
 	<li>Things tend to get a bit more complicated when the data sent by a service consumer differs from the data expected by the correspond‐ ing service. This impedance mismatch in the actual contract data is addressed through message enhancement capability. Whereas mes‐ sage transformation is concerned about the format of the request, message enhancement is concerned about the request data. This capability allows a component (usually a middleware component) to add or change request data so that the data sent by the service con</li>
 	<li>Fortunately, lookup capabilities and basic transformations (such as date, time, and number fields) can usually fix most contract variances between service consumers and services.</li>
 	<li>Microservices architecture does not support contract decoupling, whereas contract decoupling is one of the primary capabilities offered within a SOA.</li>
</ul>
&nbsp;

The microservices pattern does not support the concept of messag‐ ing middleware (e.g., integration hub or enterprise service bus). Rather, it supports the notion of an API layer in front of the services that acts as a service-access facade. Placing an API layer between your service consumers and the services is generally a good idea because it forms an abstraction layer so that service consumers don’t need to know the actual location of the service endpoints. It also allows you to change the granularity level of your services without impacting the service consumers. Abstracting service granularity does require a bit of intelligence and some level of orchestration within the API layer, but this can be refactored over time, allowing services to evolve without constant changes to the corresponding service consumers.

Notice in the diagram the use of a service registry or service-discovery com‐ ponent, as well as the use of service orchestration. Both microservi‐ ces and SOA share this capability, particularly with regard to a ser‐ vice registry or service-discovery component. However, with micro‐ services service orchestration is typically minimized or not used at all, whereas with SOA it is frequently used.

<a href="/wp-content/uploads/2017/12/image-1.png"><img style="display: inline; background-image: none;" title="image" src="/wp-content/uploads/2017/12/image_thumb-1.png" alt="image" width="439" height="241" border="0" /></a>

Message enhancement describes the capability of the architecture to modify, remove, or augment the data portion of a request before it reaches the service.

The microservices pattern does not support this capability, primarily because it doesn’t include a middleware component to implement this functionality. SOA fully supports this capability through its messaging middleware.

One of the fundamental differences between microservices and SOA with regard to remote access is that <strong>microservices architectures tend to rely on REST</strong> as their primary remote-access protocol, whereas <strong>SOA has no such restrictions.</strong> As a matter of fact, having the ability to handle dozens of different kinds of remote-access protocols is one of the main things that sets SOA apart from microservices

the messaging middleware component of the architecture that provides support for any number of remote access protocols, allowing for transformation from one protocol to another. That being said, most SOA architectures typically rely on messaging (e.g., JMS, AMQP, MSMQ) and SOAP as the primary service remote-access protocols.
<h2>Service-based architectures</h2>
Both microservices architecture and SOA are considered service based architectures, meaning that they are architecture patterns that place a heavy emphasis on services as the primary architecture component used to implement and perform business and nonbusiness functionality.
<h2>Distributed architectures (similarities of SOA &amp; Microservices)</h2>
They are generally <strong>distributed architectures</strong>, meaning that service <strong>components are accessed remotely</strong> through some sort of remote access
protocol—for example,
<ul>
 	<li>Representational State Transfer (REST),</li>
 	<li>Simple Object Access Protocol (SOAP),</li>
 	<li>Advanced Message Queuing Protocol (AMQP),</li>
 	<li>Java Message Service (JMS),</li>
 	<li>Microsoft Message Queuing (MSMQ),</li>
 	<li>Remote Method Invocation (RMI), or</li>
 	<li>.NET Remoting.</li>
</ul>
<strong>Modularity</strong>
<ul>
 	<li>In the context of service-based architecture, modularity is the practice of encapsulating portions of your application into self-contained services that can be individually designed, developed, tested, and deployed with little or no dependency on other components or services in the application.</li>
 	<li>Modular architectures also support the notion of favoring rewrite over maintenance, allowing architectures to be refactored or replaced in smaller pieces over time as the business grows—as opposed to replacing or refactoring an entire application using a big-bang approach</li>
</ul>
<h3>Advantages</h3>
Distributed architectures offer significant advantages over monolithic and layered-based architectures, including
<ul>
 	<li>Distributed architectures also lend themselves to more loosely coupled and modular applications. So provides better control over development, testing, and deployment.</li>
 	<li>Components within a distributed architecture tend to be more self-contained, allowing for better change control and easier maintenance, which in turn leads to
applications that are more robust and more responsive.</li>
</ul>
<h2>Some Complex Issues</h2>
<h3>Service Contracts</h3>
<ul>
 	<li>A service contract is an agreement between a (usually remote) service and a service consumer (client) that specifies the inbound and outbound data along with the contract format (XML, JavaScript Object Notation [JSON], Java object, etc.).</li>
 	<li>two basic types of service contract models: service-based contracts and consumer-driven contracts.</li>
 	<li>Open source tools such as <a href="https://github.com/realestate-com-au/pact">Pact</a> and <a href="http://thoughtworks.github.io/pacto">Pacto</a> can help with maintaining and testing consumer-driven contracts.</li>
</ul>
<h4>Contract versioning</h4>
<ul>
 	<li>Another critical topic within the context of service contracts is contract versioning. Let’s face it—at some point the contracts binding your services and service consumers <strong>are bound to change.</strong> Plan for contract versioning from the very start of your development effort.</li>
 	<li>Contract versioning allows you to roll out new service features that involve contract changes and at the same time provide backward compatibility for service consumers that are still using prior contracts.</li>
 	<li>You can use two basic techniques to implement your own custom contract-versioning strategy: homogeneous versioning and heterogeneous versioning.</li>
</ul>
<h5>Homogeneous versioning</h5>
the contract used by service consumer A and service consumer B are both the same circle shape (signifying the same contract) but contain different version numbers.
<p id="AvKQqrm"><img class="alignnone wp-image-515 " src="/wp-content/uploads/2017/12/img_5a38af4b2ce10.png" alt="" width="273" height="97" /></p>
Heterogeneous versioning involves supporting multiple types of contracts. With this technique, as new features are introduced, new contracts are introduced as
well that support that new functionality.
<p id="TqyNYVo"><img class="alignnone wp-image-516 " src="/wp-content/uploads/2017/12/img_5a38b0d3c9da9.png" alt="" width="348" height="141" /></p>
Providing backward compatibility is the real goal of contract versioning. Maintaining a mindset that services must support multiple versions of a contract (or multiple contracts) will allow your development teams to quickly deploy new features and other changes without fear of breaking the existing contracts with other service consumers. Keep in mind that it is also possible to combine these two techniques by supporting multiple version numbers for different contract types.

be sure to have a solid service consumer communication strategy in place from the start so that service consumers know when a contract changes or a particular version or contract type is no longer supported. In many circumstances this may not be feasible because the number of internal and/or external service consumers is large. In this situation an integration hub (i.e., messaging middleware) can help by providing an abstraction layer to transform service contracts between services and service consumers.
<h3>Security</h3>
<ul>
 	<li>Security was a major issue with early SOA implementations. Functionality that used to be located in a secure silo-based application was <strong>suddenly available globally</strong> to the entire enterprise.</li>
 	<li>With microservices, security becomes a challenge primarily because no middleware component handles security-based functionality.
Instead, each service must handle security on its own, or in some cases the API layer can be made more intelligent to handle the security aspects of the application.</li>
 	<li>One security design I have seen implemented in microservices that works well is to delegate authentication to a separate service and place the responsibility for authorization in the service itself.</li>
 	<li>Although this design could be modified to delegate both authentication and authorization to a separate security service, I prefer encapsulating the authorization in the service itself to avoid chattiness with a remote security service and to create a stronger bounded context with fewer external dependencies.</li>
</ul>
<h3>Transaction management</h3>
<ul>
 	<li>Transaction management is a big challenge in service-based architectures because, unlike in microservices architecture, multiple services are typically used to
perform a single business request.</li>
 	<li>Most of the time when we talk about transactions we are referring to the <strong>ACID</strong> (atomicity, consistency, isolation, and durability) transactions found in most business applications.</li>
 	<li>ACID transaction are used to maintain database consistency by coordinating multiple database updates within a single request so that if an error
occurs during processing, all database updates are rolled back for that request.</li>
 	<li>Rather than use ACID transactions, service-based architectures rely on BASE transactions. BASE is a family of styles that include basic availability, soft state, and eventual consistency. Distributed applications relying on BASE transactions strive for eventual consistency in the database rather than consistency at every transaction.</li>
 	<li>A classic example of <strong>BASE</strong> transactions is making a deposit into an ATM.
When you deposit cash into your account through an ATM, it can take from several minutes to several hours for the deposit to appear in your account. In other words, there is a soft transition state in which the money has left your hands but has not reached your bank account. We are tolerant of this time lag and rely on soft state and eventual consistency, knowing and trusting that the money will reach our account at some point soon.</li>
 	<li>Batch jobs also sometimes rely on eventual consistency when seen from a holistic system view</li>
 	<li>In situations in which you simply cannot rely on eventual consistency and soft state and require transactional consistency, you can make your services more coarse-grained to encapsulate the business logic into a single service, allowing the use of ACID transactions to achieve consistency at the transaction level.</li>
 	<li>You can also leverage event driven techniques to push notifications to consumers when the state of a request has become consistent. This technique adds a significant amount of complexity to an application but helps in managing transactional state when BASE transactions are used.</li>
</ul>
<h3><span style="font-weight: bold;"><u>MicroServices VS SOA</u></span></h3>
Microservices have at times been billed as “SOA done right,” but is that really the case?
<table>
<tbody>
<tr>
<td>Features</td>
<td>SOA</td>
<td>MicroService</td>
</tr>
<tr>
<td>Populerd</td>
<td>2000's</td>
<td></td>
</tr>
<tr>
<td></td>
<td>Reuse

Better communication

big, bloated monolithic, expensive,

the complicated architecture style

took too long to
design and implement</td>
<td></td>
</tr>
</tbody>
</table>
The power of microservices comes from their non-prescriptive
nature. There is no formal, slow-moving, industry-driven specifica‐
tion; rather, the microservices approach has emerged as a pattern of
development that has been practiced and refined by pioneers. Born
in the modern Web, microservices are interconnected using a thin
layer of simple APIs and the lingua franca of HTTP.

&nbsp;

The modules in microservice interact with other modules
Modules can be evolved separately.
Polyglot multiple technologies

Integrating large volume of data
<ul>
 	<li><a href="http://microservices.io/patterns/data/database-per-service.html">http://microservices.io/patterns/data/database-per-service.html</a></li>
 	<li><a href="https://stackoverflow.com/questions/29761872/microservices-and-database-joins">https://stackoverflow.com/questions/29761872/microservices-and-database-joins</a></li>
 	<li><a href="https://auth0.com/blog/introduction-to-microservices-part-4-dependencies/">https://auth0.com/blog/introduction-to-microservices-part-4-dependencies/</a></li>
 	<li><a href="https://softwareengineering.stackexchange.com/questions/279409/how-does-polyglot-persistence-handle-relational-data">https://softwareengineering.stackexchange.com/questions/279409/how-does-polyglot-persistence-handle-relational-data</a></li>
</ul>
<a href="http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/">http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/</a>
<h1>Open-Source Service Discovery</h1>
Service discovery is a key component of most distributed systems and service oriented architectures. The problem seems simple at first: <em>How do clients determine the IP and port for a service that exist on multiple hosts? </em>

With a live system, service locations can change quite frequently due to auto or manual scaling, new deployments of services, as well as hosts failing or being replaced.

Dynamic service registration and discovery becomes much more important in these scenarios in order to avoid service interruption.

There are two sides to the problem of locating services. <em>Service Registration</em> and <em>Service Discovery</em>.

<a href="https://stackshare.io/service-discovery">https://stackshare.io/service-discovery</a>

Service discovery open source software - ‎eureka <a href="https://stackshare.io/consul">Consul </a>
<h6>What is Eureka?</h6>
<a href="https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance">https://github.com/Netflix/eureka/wiki/Eureka-at-a-glance</a>

Eureka is a REST (Representational State Transfer) based service that is primarily used in the AWS cloud for locating services for the purpose of load balancing and failover of middle-tier servers. We call this service, the <strong>Eureka Server</strong>. Eureka also comes with a Java-based client component,the <strong>Eureka Client</strong>, which makes interactions with the service much easier.

&nbsp;
<h3>Kubernetes Vs. Docker</h3>
<a href="https://dzone.com/articles/docker-vs-kubernetes-prons-and-cons">https://dzone.com/articles/docker-vs-kubernetes-prons-and-cons</a>
<ol>
 	<li dir="ltr">Overall, Docker wins hands-down when it comes to setup and installation.</li>
 	<li dir="ltr">For Kubernetes, there is more than one way to monitor and log the clusters. You can use any of the following ways to do so:</li>
</ol>
<ul>
 	<li dir="ltr">
<p dir="ltr"><strong>Logging: </strong><a href="https://www.elastic.co/products/kibana" target="_blank" rel="nofollow noopener">Kibana</a> (ELK) or <a href="https://www.elastic.co/" target="_blank" rel="nofollow noopener">Elasticsearch</a></p>
</li>
 	<li dir="ltr">
<p dir="ltr"><strong>Monitoring: </strong><a href="https://grafana.com/" target="_blank" rel="nofollow noopener">Grafana</a>, <a href="https://github.com/kubernetes/heapster" target="_blank" rel="nofollow noopener">Heapster</a>, or <a href="http://www.influx.co.in/" target="_blank" rel="nofollow noopener">Influx</a></p>
</li>
</ul>
<p dir="ltr">For Docker, there is no in-built library or process for monitoring or logging. However, developers can use third-party applications for monitoring and logging purposes. Some of the good examples of 3rd party monitoring tools are <a href="https://twitter.com/SumoLogic" target="_blank" rel="nofollow noopener">Sumo Logic</a>, <a href="https://stackify.com/retrace/" target="_blank" rel="nofollow noopener">Retrace</a>, <a href="https://blog.docker.com/2016/03/realtime-cluster-monitoring-docker-swarm-riemann/" target="_blank" rel="nofollow noopener">Reimann</a><strong>, </strong>and <a href="https://www.datadoghq.com/" target="_blank" rel="nofollow noopener">DataDog</a>.</p>

<ul>
 	<li>Both the systems roughly support 1000 node clusters. The 1000 node clusters can support up to 30,000 containers.</li>
 	<li dir="ltr">Performance wise, Kubernetes holds a good ground against Docker. However, the r<a href="https://blog.docker.com/2016/03/swarmweek-docker-swarm-exceeds-kubernetes-scale/" target="_blank" rel="nofollow noopener">esearch done by an independent body</a> revealed that Docker could spin containers five times faster than Kubernetes.</li>
</ul>
<table>
<tbody>
<tr>
<td>
<p dir="ltr">Kubernetes</p>
</td>
<td>
<p dir="ltr">Docker</p>
</td>
</tr>
<tr>
<td>
<p dir="ltr">Most mature solution in the market.</p>
</td>
<td>
<p dir="ltr">Docker offers good features, but limited by its API.</p>
</td>
</tr>
<tr>
<td>
<p dir="ltr">Kubernetes is also the most popular solution in the market.</p>
</td>
<td>
<p dir="ltr">Docker’s market is relatively weaker compared to Kubernetes.</p>
</td>
</tr>
<tr>
<td>
<p dir="ltr">Kubernetes is hard to setup and configure.</p>
</td>
<td>
<p dir="ltr">Docker’s setup and installation is easy.</p>
</td>
</tr>
<tr>
<td>
<p dir="ltr">Kubernetes offers inbuilt logging and monitoring tools.</p>
</td>
<td>
<p dir="ltr">Docker only supports 3rd party monitoring and logging tools.</p>
</td>
</tr>
<tr>
<td>
<p dir="ltr">CPU utilization is a big factor in autoscaling.</p>
</td>
<td>
<p dir="ltr">It is possible to scale services manually.</p>
</td>
</tr>
</tbody>
</table>
<h3>Conclusion</h3>
<p dir="ltr">Kubernetes is widely accepted by the community of developers, despite the hard installation process. The sole reason behind its popularity is the flexibility it offers and also the fact that it is backed by Google, one of the leading tech giants.</p>

<ul>
 	<li>In micro service if there is an issue search in all logs? Use analysis tool</li>
 	<li>Use correlation ids to track transaction which it executed on multiple servers</li>
 	<li>Selective scalability</li>
 	<li>Cross-cutting concerns will be a separate service</li>
 	<li>API gateway to write common code for all services</li>
 	<li><strong>Drawbacks</strong>
<ul>
 	<li>Distributed
Consistency
Transaction
Request travelling
Integration tests
Require a eco system
More complex than monolithic</li>
</ul>
</li>
</ul>
Similar to OAuth, SSO the authentication can also be moved to separate service.
<p id="oCBWXmG"><img class="alignnone wp-image-384 " src="/wp-content/uploads/2017/12/img_5a24e80ad31cf.png" alt="" width="565" height="417" /></p>
&nbsp;

If we are splitting the monolith to micro services architecture, performance has to increase

if the latency between the services is high (separate data centers, geographical locations) the performance will be poor

&nbsp;

If overall transaction time for the microservices is high, it's not recommended to use micro services.
<p id="WqZlOOS"><img class="alignnone wp-image-385 " src="/wp-content/uploads/2017/12/img_5a24e8ea27dcd.png" alt="" width="504" height="370" /></p>
REST - Stateless service.

&nbsp;

Group funcitonality together

in monolith few people have overall visibility of the different modules

many modules are installed in hundreds of installations. So the automated continuous integration is mandatory.

Containers, instantiations and deployments need to be managed.

&nbsp;

Some applications will load millions of rows in to cache before getting ready to serve the content.

So the start time in monolithic is higher than micro services
<p id="yHYnCyv"><img class="alignnone size-full wp-image-387 " src="/wp-content/uploads/2017/12/img_5a24ed0bcdc26.png" alt="" /></p>
&nbsp;

&nbsp;
<p id="fwAyoUo"><img class="alignnone size-full wp-image-389 " src="/wp-content/uploads/2017/12/img_5a24eddb8e2cd.png" alt="" /></p>
&nbsp;
<p id="lcYsNet"><img class="alignnone size-full wp-image-388 " src="/wp-content/uploads/2017/12/img_5a24ed9842e36.png" alt="" /></p>
&nbsp;
<p id="KIumAmk"><img class="alignnone size-full wp-image-390 " src="/wp-content/uploads/2017/12/img_5a24ee1ea8ec9.png" alt="" /></p>
&nbsp;
<p id="gTTcrvw"><img class="alignnone size-full wp-image-391 " src="/wp-content/uploads/2017/12/img_5a24ef0eed7d4.png" alt="" /></p>
&nbsp;

&nbsp;
<p id="kmkNlOB"><img class="alignnone size-full wp-image-392 " src="/wp-content/uploads/2017/12/img_5a24ef32d1eb3.png" alt="" /></p>
&nbsp;

&nbsp;

&nbsp;
<p id="urBSAxr"><img class="alignnone size-full wp-image-393 " src="/wp-content/uploads/2017/12/img_5a24ef916e5e0.png" alt="" /></p>
&nbsp;
<p id="CgZuDlA"><img class="alignnone size-full wp-image-394 " src="/wp-content/uploads/2017/12/img_5a24efab469c5.png" alt="" /></p>
&nbsp;

&nbsp;
<p id="ZAVPfUH"><img class="alignnone size-full wp-image-395 " src="/wp-content/uploads/2017/12/img_5a24eff5b9ab4.png" alt="" /></p>
&nbsp;

&nbsp;

Even a unused module can't be shut down in monolithic

&nbsp;
<p id="ndDQBZR"><img class="alignnone size-full wp-image-396 " src="/wp-content/uploads/2017/12/img_5a24f0d12dadf.png" alt="" /></p>
&nbsp;
<p id="lXRJMCy"><img class="alignnone size-full wp-image-397 " src="/wp-content/uploads/2017/12/img_5a24f0facc529.png" alt="" /></p>
client like angularjs
<p id="qrkYtHv"><img class="alignnone size-full wp-image-398 " src="/wp-content/uploads/2017/12/img_5a24f12bea352.png" alt="" /></p>
&nbsp;
<p id="HjuQRpS"><img class="alignnone size-full wp-image-399 " src="/wp-content/uploads/2017/12/img_5a24f1473f6c3.png" alt="" /></p>
&nbsp;
<p id="gCLpnJq"><img class="alignnone size-full wp-image-400 " src="/wp-content/uploads/2017/12/img_5a24f2872981d.png" alt="" /></p>
