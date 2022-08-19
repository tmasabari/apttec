---
layout: post
title: Architect questions - scenarios, NFR - Performance
date: 2018-03-21 08:28
author: tmasabari
comments: true
categories: [Architecture, Interview Preparation, NFR, Performance, Todo]
---
<ol>
 	<li>how do you create fire and forget services in wcf and rest</li>
 	<li>how do you create aync methods in wcf and rest</li>
 	<li><a href="https://stackoverflow.com/questions/12803012/fire-and-forget-with-async-vs-old-async-delegate">fire and forget</a></li>
 	<li><a href="https://www.hanselman.com/blog/HowToRunBackgroundTasksInASPNET.aspx">Schedulers</a>, <a href="https://www.mikesdotnetting.com/article/254/scheduled-tasks-in-asp-net-with-quartz-net">Quartz</a></li>
 	<li>Singleton in web farm</li>
 	<li>how do you create manual database connection pool</li>
 	<li>if we call methods with base class reference with subclass object <a href="https://www.akadia.com/services/dotnet_polymorphism.html">how override and new differs</a></li>
 	<li>javascript patterns - <a href="https://addyosmani.com/resources/essentialjsdesignpatterns/book/">https://addyosmani.com/resources/essentialjsdesignpatterns/book/</a>
<ol>
 	<li><a href="https://stackoverflow.com/questions/592396/what-is-the-purpose-of-a-self-executing-function-in-javascript">How will you create self executing function in javascript ? </a>
<ul>
 	<li>Now we come to auto-execution functions (or self-executing, self-running, whatever). ((){})();</li>
</ul>
</li>
 	<li><a href="https://medium.freecodecamp.org/javascript-modules-a-beginner-s-guide-783f7d7a5fcc">What's module in javascript ?</a></li>
</ol>
</li>
 	<li>Can you create multiple action filters for the same method? What's the use of action filters ?</li>
 	<li>In OAuth who is generating the token ? Explain OAuth flow (Covered)</li>
 	<li>in order to achieve 27/7 or 99.9 % availability how will you architect your application
<ol>
 	<li>use redundancy on each tier - load balancers, queues with multiple application server, database clusters</li>
</ol>
</li>
 	<li>In case of peak load on certain time of the day, how will give cost optimized performance benefits
<ol>
 	<li>use cloud on demand instances</li>
 	<li>use other server (such as reporting or batch servers) to act as application servers</li>
 	<li>use queuing mechanism</li>
</ol>
</li>
 	<li>delete millions of rows from a table
<ol>
 	<li>https://ask.sqlservercentral.com/questions/28252/deleting-10-million-records-from-a-database-table.html</li>
</ol>
</li>
 	<li>load huge data from multiple sources to a DB</li>
 	<li>unique values for 2 sets which not exist on others from millions of Ilist strings</li>
 	<li><a class="question-hyperlink" href="https://stackoverflow.com/questions/1645215/how-do-i-add-a-column-to-large-sql-server-table">How do I add a column to large sql server table</a>
<ol>
 	<li>
<pre class="lang-sql prettyprint prettyprinted"><code><span class="kwd">ALTER</span> <span class="kwd">TABLE</span><span class="pln"> table1 </span><span class="kwd">ADD</span><span class="pln">
  newcolumn int </span><span class="kwd">NULL</span><span class="pln">
GO</span></code></pre>
should not take that long... What takes a long time is to insert columns in the middle of other columns... b/c then the engine needs to create a new table and copy the data to the new table.</li>
</ol>
</li>
 	<li><a class="question-hyperlink" href="https://stackoverflow.com/questions/9280957/sql-server-drop-column-from-vlt-very-large-table">Sql Server - Drop column from VLT (Very Large Table )</a></li>
 	<li>Delete data in batches from large SQL database tables
<ol>
 	<li>https://support.solarwinds.com/Success_Center/Network_Performance_Monitor_(NPM)/Delete_data_in_batches_from_large_SQL_database_tables</li>
 	<li>Note: Removing table rows in batches instead of a single transaction is time consuming, but a more reliable process.</li>
</ol>
</li>
</ol>
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">
<div id="slide_body">

<a href="https://www.nginx.com/blog/10-tips-for-10x-application-performance/">https://www.nginx.com/blog/10-tips-for-10x-application-performance/</a>

</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
</div>
https://www.infragistics.com/community/blogs/b/brijmishra/posts/leveraging-http-2-with-asp-net-4-6-and-iis10

https://stackoverflow.com/questions/2246251/how-do-i-improve-asp-net-mvc-application-performance
<h2 id="slide_title">How do you diagnose performance issues?</h2>
<strong>What are the tools used for performance monitoring on the server side</strong>
<div id="slide_body">

A: The candidate's answer should include a discussion about latencies, as well as the capacities/bottlenecks of CPU, memory, disk, and network. Solutions architects are often confronted with the most difficult problems, and an understanding of isolating bottlenecks and resolving them is vital.

</div>
<h2 id="tip1">Tip 1 – Accelerate and Secure Applications with a Reverse Proxy Server / Load BALANCER</h2>
Problem: The application server may be thrashing – running out of memory, swapping chunks of memory out to disk, and making many requests wait on a single task such as disk I/O.

Idea: A <a href="https://www.nginx.com/resources/glossary/reverse-proxy-server">reverse proxy server</a> sits in front of the machine running the application and handles Internet traffic. Only the reverse proxy server is connected directly to the Internet; communication with the application servers is over a fast internal network.

Evidence: Using a reverse proxy server frees the application server from having to wait for users to interact with the web app and lets it concentrate on building pages for the reverse proxy server to send across the Internet.
<ul>
 	<li><strong>Load balancing</strong> (see <a href="https://www.nginx.com/blog/10-tips-for-10x-application-performance/#tip2">Tip 2</a>) – A load balancer runs on a reverse proxy server to share traffic evenly across a number of application servers. With a load balancer in place, you can add application servers without changing your application at all.</li>
 	<li><strong>Caching static files</strong> (see <a href="https://www.nginx.com/blog/10-tips-for-10x-application-performance/#tip3">Tip 3</a>) – Files that are requested directly, such as image files or code files, can be stored on the reverse proxy server and sent directly to the client, which serves assets more quickly and offloads the application server, allowing the application to run faster.</li>
 	<li><strong>Securing your site</strong> – The reverse proxy server can be configured for high security and monitored for fast recognition and response to attacks, keeping the application servers protected.</li>
 	<li>A load balancer is, first, a reverse proxy server (see <a href="https://www.nginx.com/blog/10-tips-for-10x-application-performance/#tip1">Tip 1</a>) – it receives Internet traffic and forwards requests to another server.</li>
 	<li>The trick is that the load balancer supports two or more application servers, using <a href="https://www.nginx.com/resources/admin-guide/load-balancer/">a choice of algorithms</a> to <strong>split requests between servers</strong>. The simplest load balancing approach is round robin, with each new request sent to the next server on the list. Other methods include sending requests to the server with the fewest active connections Protocols that can be load balanced include HTTP, HTTPS, SPDY, HTTP/2, WebSocket, <a href="https://www.digitalocean.com/community/tutorials/understanding-and-implementing-fastcgi-proxying-in-nginx" target="_blank" rel="noopener">FastCGI</a>, SCGI, uwsgi, memcached, and several other application types, including TCP‑based applications and other Layer 4 protocols. Analyze your web applications to determine which you use and where performance is lagging.</li>
 	<li>The same server or servers used for load balancing can also handle several other tasks, such as SSL termination, support for HTTP/1.<em>x</em> and HTTP/2 use by clients, and caching for static files.</li>
</ul>
<h2 id="tip3">Tip 2 – Cache Static and Dynamic Content</h2>
Caching improves web application performance by delivering content to clients faster. Caching can involve several strategies: preprocessing content for fast delivery when needed, storing content on faster devices, storing content closer to the client, or a combination.

There are two different types of caching to consider:
<ul>
 	<li><strong>Caching of static content</strong> – Infrequently changing files, such as image files (JPEG, PNG) and code files (CSS, JavaScript), can be stored on an edge server for fast retrieval from memory or disk.</li>
 	<li><strong>Caching of dynamic content</strong> – Many Web applications generate fresh HTML for each page request. By briefly caching one copy of the generated HTML for a brief period of time, you can dramatically reduce the total number of pages that have to be generated while still delivering content that’s fresh enough to meet your requirements. If a page gets 10 views per second, for instance, and you cache it for 1 second, 90% of requests for the page will come from the cache.</li>
</ul>
<h2>Tip 3 – Compress Data- Bundling and minification</h2>
The smaller you make the images, the faster the web page renders.

Sprites are images inside a larger image. The browser makes a request for that one large image file and you use CSS to grab the images and display them on the webpage.

&nbsp;

Compression is a huge potential performance accelerator. There are carefully engineered and highly effective compression standards for photos (JPEG and PNG), videos (MPEG‑4), and music (MP3), among others. Each of these standards reduces file size by an order of magnitude or more.

Smart content compression can reduce the bandwidth requirements of HTML, Javascript, CSS and other text‑based content, typically by 30% or more, with a corresponding reduction in load time.

If you use SSL, compression reduces the amount of data that has to be SSL‑encoded, which offsets some of the CPU time it takes to compress the data. As another example of text compression you can <a href="https://www.nginx.com/resources/admin-guide/compression-and-decompression/">turn on GZIP</a> compression
<h2>Tip 4 – Optimize SSL/TLS</h2>
The Secure Sockets Layer (<a href="https://www.digicert.com/ssl.htm" target="_blank" rel="noopener">SSL</a>) protocol and its successor, the Transport Layer Security (TLS) protocol, are being used on more and more websites. SSL/TLS encrypts the data transported from origin servers to users to help improve site security.

SSL/TLS slows website performance for two reasons:
<ol>
 	<li>The initial handshake required to establish encryption keys whenever a new connection is opened. The way that browsers using HTTP/1.<em>x</em> establish multiple connections per server multiplies that hit.</li>
 	<li>Ongoing overhead from encrypting data on the server and decrypting it on the client.</li>
</ol>
To encourage the use of SSL/TLS, the authors of HTTP/2 and SPDY (described in the <a href="https://www.nginx.com/blog/10-tips-for-10x-application-performance/#tip6">next Tip</a>) designed these protocols so that browsers need just one connection per browser session. This greatly reduces one of the two major sources of SSL overhead. However, even more can be done today to improve the performance of applications delivered over SSL/TLS.
<ul>
 	<li><strong>Session caching</strong> – Uses the <a href="http://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_session_cache"><code>ssl_session_cache</code></a> directive to cache the parameters used when securing each new connection with SSL/TLS.</li>
 	<li><strong>Session tickets or IDs</strong> – These store information about specific SSL/TLS sessions in a ticket or ID so a connection can be reused smoothly, without new handshaking.</li>
 	<li><strong>OCSP stapling</strong> – Cuts handshaking time by caching SSL/TLS certificate information.</li>
</ul>
<h2 id="tip6">Tip 5 – Implement HTTP/2 or SPDY</h2>
<ul>
 	<li>Google introduced SPDY in 2012 as a way to achieve faster performance on top of HTTP/1.<em>x</em>. HTTP/2 is the recently approved IETF standard based on SPDY. SPDY is broadly supported, but is soon to be deprecated, replaced by HTTP/2.</li>
 	<li>The key feature of SPDY and HTTP/2 :  HTTP/2 is based on the SPDY protocol which opens one TCP connection and uses multiplexing, which allows many requests to be sent in parallel without waiting for the response.  Apart from that, it also compresses the HTTP Headers and enables the server push</li>
 	<li>By getting the most out of one connection, these protocols avoid the overhead of setting up and managing multiple connections, as required by the way browsers implement HTTP/1.<em>x</em>. The use of a single connection is especially helpful with SSL, because it minimizes the time‑consuming handshaking that SSL/TLS needs to set up a secure connection.</li>
 	<li>When you implement SPDY or HTTP/2, you no longer need typical HTTP performance optimizations such as domain sharding, resource merging, and image spriting. These changes make your code and deployments simpler and easier to manage.
<p id="MADbdHH"><img class="alignnone wp-image-459 " style="margin-right: auto; margin-left: auto; float: none; display: block;" src="/wp-content/uploads/2017/12/img_5a2a6e1c875b8.png" alt="" width="435" height="240" /></p>
</li>
</ul>
<h2 id="tip6">Tip 6 – Optimize iis &amp; Site config</h2>
&nbsp;
<h2 id="tip6">Tip 7 USE AJAX WHEN YOU CAN</h2>
AJAX has been around for a while and for good reason. It blurs the distinction between a desktop and web application. This gives the user the perspective that the web site is fast and gives them time to focus on things that have changed on the dashboard while the widgets are updating.

<strong>Client Side Validation</strong>

Validation takes important part because it validates the user data that it is valid or not. But suppose after validating the single data, your site is going to load that means user should wait every time to load your site again and again. So, always prefer to make the validation on Client Side.
<p class="label"><strong>Design Guidelines  to improve Performance </strong></p>

<div class="tablediv">
<div class="contentTableWrapper">
<table border="1" summary="table" cellspacing="0" cellpadding="2">
<tbody>
<tr>
<th scope="col">Performance profile category</th>
<th scope="col">Guidelines</th>
</tr>
<tr>
<td data-th="Performance profile category">Coupling and Cohesion</td>
<td data-th="Guidelines">
<ul>
 	<li><strong>Design</strong> for loose coupling.Design for high cohesion.</li>
 	<li>Partition application functionality into <strong>logical layers</strong>.</li>
 	<li>Use early binding where possible.</li>
 	<li>Evaluate resource affinity.</li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">Communication</td>
<td data-th="Guidelines">
<ul>
 	<li>Choose the appropriate <strong>remote communication</strong> mechanism.Design chunky interfaces.</li>
 	<li>Consider how to pass data between layers.</li>
 	<li>Minimize the amount of data sent across the wire.</li>
 	<li>Batch work to reduce calls over the network.</li>
 	<li>Reduce transitions across boundaries.</li>
 	<li>Consider <strong>asynchronous communication</strong>.</li>
 	<li>Consider message queuing.</li>
 	<li>Consider a <strong>"fire and forget"</strong> invocation model.</li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">Concurrency</td>
<td data-th="Guidelines">
<ul>
 	<li>Use <a href="http://msdn.microsoft.com/en-in/library/ee728598(v=vs.98).aspx" rel="noreferrer">Asynchronous Controllers</a> to implement actions that depend on external resources processing.</li>
 	<li><strong>Reduce contention by minimizing lock times</strong>.Balance between coarse-grained and fine-grained locks.</li>
 	<li>Choose an appropriate transaction isolation level.</li>
 	<li>Avoid long-running atomic transactions.</li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">Resource Management</td>
<td data-th="Guidelines">
<ul>
 	<li>Treat threads as a shared resource.Pool shared or scarce resources.</li>
 	<li>Acquire late, release early.</li>
 	<li>Consider efficient object creation and destruction.</li>
 	<li>Consider resource throttling.</li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">Caching</td>
<td data-th="Guidelines">
<ul>
 	<li>Decide where to cache data.Decide what data to cache.</li>
 	<li>Decide the expiration policy and scavenging mechanism.</li>
 	<li>Decide how to load the cache data.</li>
 	<li>Avoid distributed coherent caches.</li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">State Management</td>
<td data-th="Guidelines">
<ul>
 	<li>Evaluate stateful versus stateless design.Consider your state store options.</li>
 	<li><strong>Minimize session data.</strong></li>
 	<li>Free session resources as soon as possible.</li>
 	<li><strong>Avoid accessing session variables from business logic.</strong></li>
</ul>
</td>
</tr>
<tr>
<td data-th="Performance profile category">Data Structures/Algorithms</td>
<td data-th="Guidelines">
<ul>
 	<li>Choose an appropriate data structure.Pre-assign size for large dynamic growth data types.</li>
 	<li>Use value and reference types appropriately.</li>
</ul>
</td>
</tr>
</tbody>
</table>
</div>
</div>
<h2 id="slide_title">Q7: How do you address cache coherency?</h2>
<div id="slide_body">

A: A candidate's answer will vary, but should at least mention the use of multi-server, in-memory caches, and caches that may be quasi-memory, such as a SQL server database. They should understand that a SQL server database is where the data gets maintained in memory by the SQL server predictive caching. The candidate should be aware of problems with cached objects not being in-sync across multiple servers, and the need to clear cached objects when cache coherency is critical.
<h2 id="slide_title">Q8: How do you address scalability?</h2>
<div id="slide_body">

A: Scalability can be addressed vertically (increasing the resources on the same server) or horizontally (across multiple servers). <strong>Scalability is limited by single-threaded operations</strong>, so a candidate should know to give them special consideration when considering how to scale an application.
<h2 id="slide_title">Q9: How do you address fault tolerance?</h2>
<div id="slide_body">

A: The candidate should recognize the need to eliminate <strong>single points of failure</strong> as much as is possible. It's also important for candidates to be aware of the ability to ensure that sessions can be switched to a new server at any point—even if there's a performance impact to this switch. Modeling failures—and testing with simulated failures—are important for any solutions architect.
<h2 id="slide_title">How do you protect against injection attacks?</h2>
<div id="slide_body">

A: There are multiple different ways of approaching this question, but a candidate should include discussions of SQL injection and cross site scripting (XSS). Any mentioned approaches should include cleaning and screening the input. SQL injection conversations should include a conversation about parameterized queries and stored procedures.
<h2 id="slide_title"></h2>
</div>
</div>
</div>
</div>
