---
layout: post
title: Distributed Application and coordination
date: 2018-05-04 12:30
author: tmasabari
comments: true
categories: [SOLR, ZooKeeper]
---
<h2>Distributed Application</h2>
<ul>
 	<li>A distributed application can run on multiple systems in a network at a given time (simultaneously) by coordinating among themselves to complete a particular task in a fast and efficient manner.</li>
 	<li>Normally, complex and time-consuming tasks, which will take hours to complete by a non-distributed application (running in a single system) can be done in minutes by a distributed application by using computing capabilities of all the system involved.</li>
 	<li>The time to complete the task can be further reduced by configuring the distributed application to run on more systems. A group of systems in which a distributed application is running is called a <b style="font-size: 1rem;">Cluster</b><span style="font-size: 1rem;"> and each machine running in a cluster is called a </span><b style="font-size: 1rem;">Node</b><span style="font-size: 1rem;">.</span></li>
 	<li>A distributed application has two parts, <b style="font-size: 1rem;">Server</b><span style="font-size: 1rem;"> and </span><b style="font-size: 1rem;">Client</b><span style="font-size: 1rem;"> application. Server applications are actually distributed and have a common interface so that clients can connect to any server in the cluster and get the same result. Client applications are the tools to interact with a distributed application.</span></li>
</ul>
<p id="swphbQQ"><img class="size-full wp-image-1535 aligncenter" src="/wp-content/uploads/2018/05/img_5aec0ff792a60.png" alt="" /></p>

<h3>Benefits of Distributed Applications</h3>
<ul class="list">
 	<li><b>Reliability</b> − Failure of a single or a few systems does not make the whole system to fail.</li>
 	<li><b>Scalability</b> − Performance can be increased as and when needed by adding more machines with minor change in the configuration of the application with no downtime.</li>
 	<li><b>Transparency</b> − Hides the complexity of the system and shows itself as a single entity / application.</li>
</ul>
<h3>Challenges of Distributed Applications</h3>
<ul class="list">
 	<li><b>Race condition</b> − Two or more machines trying to perform a particular task, which actually needs to be done only by a single machine at any given time. For example, shared resources should only be modified by a single machine at any given time.</li>
 	<li><b>Deadlock</b> − Two or more operations waiting for each other to complete indefinitely.</li>
 	<li><b>Inconsistency</b> − Partial failure of data.</li>
</ul>
<h2>What is Apache ZooKeeper Meant For?</h2>
<ul>
 	<li>Apache ZooKeeper is a service <strong>used by a cluster (group of nodes) to coordinate between themselves and maintain shared data with robust synchronization techniques</strong>.</li>
 	<li>ZooKeeper is itself a distributed application providing services for writing a distributed application.</li>
 	<li>ZooKeeper solves this issue with its simple architecture and API. ZooKeeper allows developers to focus on core application logic without worrying about the distributed nature of the application.</li>
 	<li>The ZooKeeper framework was originally built at “Yahoo!” for accessing their applications in an easy and robust manner. Later, Apache ZooKeeper became a standard for organized service used by Hadoop, HBase, and other distributed frameworks. For example, Apache HBase uses ZooKeeper to track the status of distributed data.</li>
 	<li>Race condition and deadlock are handled using <b>fail-safe synchronization approach and </b>inconsistency of data <b>problem </b>is resolved with <b>atomicity</b>.</li>
</ul>
The common services provided by ZooKeeper are as follows −
<ul class="list">
 	<li><b>Naming service</b> − Identifying the nodes in a cluster by name. It is similar to DNS, but for nodes.</li>
 	<li><b>Configuration management</b> − Latest and up-to-date configuration information of the system for a joining node.</li>
 	<li><b>Cluster management</b> − Joining / leaving of a node in a cluster and node status at real time.</li>
 	<li><b>Leader election</b> − Electing a node as leader for coordination purpose.</li>
 	<li><b>Locking and synchronization service</b> − Locking the data while modifying it. This mechanism helps you in automatic fail recovery while connecting other distributed applications like Apache HBase.</li>
 	<li><b>Highly reliable data registry</b> − Availability of data even when one or a few nodes are down.</li>
</ul>
&nbsp;

&nbsp;
<h2>Benefits of ZooKeeper</h2>
<ul class="list">
 	<li><b>Simple distributed coordination process</b></li>
 	<li><b>Ordered Messages</b></li>
 	<li><b>Serialization</b> − Encode the data according to specific rules. Ensure your application runs consistently. This approach can be used in MapReduce to coordinate queue to execute running threads.</li>
 	<li><b>Synchronization</b> − Mutual exclusion and co-operation between server processes.</li>
 	<li><b>Atomicity</b> − Data transfer either succeed or fail completely, but no transaction is partial.</li>
</ul>
<h2>Apache Solr</h2>
Apache Solr is a fast, open source search platform written in Java. It is a blazing fast, faulttolerant distributed search engine. Built on top of <b>Lucene</b>, it is a high-performance, full-featured text search engine.

Solr extensively uses every feature of ZooKeeper such as Configuration management, Leader election, node management, Locking and syncronization of data.

Solr has two distinct parts, <b>indexing</b> and <b>searching</b>. Indexing is a process of storing the data in a proper format so that it can be searched later. Solr uses ZooKeeper for both indexing the data in multiple nodes and searching from multiple nodes. ZooKeeper contributes the following features −
<ul class="list">
 	<li>Add / remove nodes as and when needed</li>
 	<li>Replication of data between nodes and subsequently minimizing data loss</li>
 	<li>Sharing of data between multiple nodes and subsequently searching from multiple nodes for faster search results</li>
</ul>
Some of the use-cases of Apache Solr include e-commerce, job search, etc.
<div class="post-header">
<h1 class="post-title-main">Combining Distribution and Replication</h1>
</div>
<div class="post-content">
<div id="toc" class="toc toc-normal"></div>
<div class="main-content">
<div class="paragraph">

When your index is too large for a single machine and you have a query volume that single shards cannot keep up with, it’s time to replicate each shard in your distributed search setup.

</div>
<div class="paragraph">

The idea is to combine distributed search with replication. As shown in the figure below, a combined distributed-replication configuration features a master server for each shard and then 1-<em>n</em> slaves that are replicated from the master. As in a standard replicated configuration, the master server handles updates and optimizations without adversely affecting query handling performance.

</div>
<div class="paragraph">

Query requests should be load balanced across each of the shard slaves. This gives you both increased query handling capacity and fail-over backup if a server goes down.

<img class="size-full wp-image-1540 aligncenter" src="/wp-content/uploads/2018/05/img_5aec37c5c3f7b.png" alt="" />
<div class="imageblock">
<div class="title">Figure 1. A Solr configuration combining both replication and master-slave distribution.</div>
</div>
<div class="paragraph">

None of the master shards in this configuration know about each other. You index to each master, the index is replicated to each slave, and then searches are distributed across the slaves, using one slave from each master/slave shard.

</div>
<div class="paragraph">

For high availability you can use a load balancer to set up a virtual IP for each shard’s set of slaves. If you are new to load balancing, HAProxy (<a class="bare" href="http://haproxy.1wt.eu/">http://haproxy.1wt.eu/</a>) is a good open source software load-balancer. If a slave server goes down, a good load-balancer will detect the failure using some technique (generally a heartbeat system), and forward all requests to the remaining live slaves that served with the failed slave. A single virtual IP should then be set up so that requests can hit a single IP, and get load balanced to each of the virtual IPs for the search slaves.

</div>
<div class="paragraph">

With this configuration you will have a fully load balanced, search-side fault-tolerant system (Solr does not yet support fault-tolerant indexing). Incoming searches will be handed off to one of the functioning slaves, then the slave will distribute the search request across a slave for each of the shards in your configuration. The slave will issue a request to each of the virtual IPs for each shard, and the load balancer will choose one of the available slaves. Finally, the results will be combined into a single results set and returned. If any of the slaves go down, they will be taken out of rotation and the remaining slaves will be used. If a shard master goes down, searches can still be served from the slaves until you have corrected the problem and put the master back into production.

</div>
&nbsp;

</div>
</div>
</div>
<h2>Architecture of ZooKeeper</h2>
&nbsp;
<p id="OVfplTx"><img class="size-full wp-image-1536 aligncenter" src="/wp-content/uploads/2018/05/img_5aec11ba19a4e.png" alt="" /></p>

<div class="sectionbody">
<div class="sect2">
<div class="ulist">
<table class="table table-bordered">
<tbody>
<tr>
<th>Part</th>
<th>Description</th>
</tr>
<tr>
<td>Client</td>
<td>Clients, one of the nodes in our distributed application cluster, access information from the server. For a particular time interval, every client sends a message to the server to let the sever know that the client is alive.

Similarly, the server sends an acknowledgement when a client connects. If there is no response from the connected server, the client automatically redirects the message to another server.</td>
</tr>
<tr>
<td>Server</td>
<td>Server, one of the nodes in our ZooKeeper ensemble, provides all the services to clients. Gives acknowledgement to client to inform that the server is alive.</td>
</tr>
<tr>
<td>Ensemble</td>
<td>Group of ZooKeeper servers. The minimum number of nodes that is required to form an ensemble is 3.</td>
</tr>
<tr>
<td>Leader</td>
<td>Server node which performs automatic recovery if any of the connected node failed. Leaders are elected on service startup.

The additional duties of a leader are pretty minimal. And the leaders will shift around anyway as you restart servers etc.</td>
</tr>
<tr>
<td>Follower</td>
<td>Server node which follows leader instruction.</td>
</tr>
</tbody>
</table>
<h2 id="HowSolrCloudWorks-KeySolrCloudConcepts" class="clickable-header top-level-header"><a href="https://lucene.apache.org/solr/guide/6_6/how-solrcloud-works.html">Key SolrCloud Concepts</a></h2>
<div class="sectionbody">
<div class="paragraph">

A SolrCloud cluster consists of some "logical" concepts layered on top of some "physical" concepts.

</div>
<div class="sect2">
<h3 id="HowSolrCloudWorks-Logical" class="clickable-header">Logical</h3>
<div class="ulist">
<ul>
 	<li>A Cluster can host multiple Collections of Solr Documents.</li>
 	<li>A collection can be <strong>partitioned into multiple Shards</strong>, which contain a <strong>subset</strong> of the Documents in the Collection.
<ul>
 	<li>It might be that they are going to provide different search interfaces to users (customers in the US and customers in Canada, for example), or</li>
 	<li>they have security concerns (some users cannot have access to some documents), or</li>
 	<li>the documents are really different and just won't mix well in the same index (a shoe database and a dvd database).</li>
</ul>
</li>
 	<li>The <strong>number of Shards that a Collection</strong> has determines:
<div class="ulist">
<ul>
 	<li>The theoretical limit to the number of Documents that Collection can reasonably contain.</li>
 	<li>The <strong>amount of parallelization</strong> that is possible for an individual search request.</li>
</ul>
</div></li>
</ul>
</div>
</div>
<div class="sect2">
<h3 id="HowSolrCloudWorks-Physical" class="clickable-header">Physical</h3>
<div class="ulist">
<ul>
 	<li>A <span style="text-decoration: underline;"><strong>Cluster</strong> </span>is made up of <strong>one or more Solr Nodes</strong>, which are <strong>running instances of the Solr server</strong> process (JVM).</li>
 	<li>Each <strong><span style="text-decoration: underline;">Node </span></strong>can host <strong>multiple Cores</strong>. (one or more)</li>
 	<li>Each <span style="text-decoration: underline;"><strong>Core</strong> </span>in a Cluster is a physical <strong>Replica for a logical Shard</strong>.</li>
 	<li>Every Replica uses the same configuration specified for the Collection that it is a part of.</li>
 	<li>The <strong>number of Replicas</strong> that each Shard has determines:
<div class="ulist">
<ul>
 	<li>The <strong>level of redundancy</strong> built into the Collection and how <strong>fault tolerant</strong> the Cluster can be in the event that some Nodes become unavailable.</li>
 	<li>The theoretical limit in the number concurrent search requests that can be processed under heavy load.</li>
</ul>
</div>
&nbsp;</li>
 	<li>A SolrCloud cluster holds one or more distributed indexes which are called Collections. Each Collection is divided into shards (to increase write capacity) and each shard has one or more replicas (to increase query capacity). One replica from each shard is elected as a leader, who performs the additional task of adding a ‘version’ to each update before streaming it to available replicas. This means that write traffic for a particular shard hits the shard’s leader first and is then synchronously replicated to all available replicas. One Solr node (a JVM instance) may host a few replicas belonging to different shards or even different collections.All nodes in a SolrCloud cluster talk to a Apache ZooKeeper ensemble (an odd number of nodes, typically 3 or more for a production deployment). Among other things, ZooKeeper stores:
<ol>
 	<li>The cluster state of the system (details of collections, shards, replicas and leaders)</li>
 	<li>The set of live nodes at any given time (determined by heartbeat messages sent by Solr nodes to ZooKeeper)</li>
 	<li>The state of each replica (active, recovering or down)</li>
 	<li>Leader election queues (a queue of live replicas for each shard such that the first in the list attempts to become the leader assuming it fulfils certain conditions)</li>
 	<li>Configurations (schema etc) which is shared by each replica in a collection.</li>
</ol>
&nbsp;

Each Solr replica keeps a Lucene index (partly in memory and disk for performance) and a write-ahead transaction log. An update request to SolrCloud is firstly, written to the transaction log, secondly to the lucene index and thirdly, if the replica is a leader, streamed synchronously to all available replicas of the same shard. A commit command flushes the lucene indexes to disk and makes new documents visible to searchers. Therefore, searches are eventually consistent. Real time “gets” of documents can be done at any time using the document’s unique key, returning content from either the Lucene index (for committed docs) or the transaction log for uncommitted docs. Such real time “gets” are always answered by the leader for consistency.

If a leader dies, a new leader is elected from among the ‘live’ replicas as long as the last published state of the replica was <em>active</em>. The selected replica <em>syncs</em> from all other <em>live</em> replicas (in both directions) to make sure that it has the latest updates among all replicas in the cluster before becoming the leader.

If a leader is not able to send an update to a replica then it updates ZooKeeper to publish the replica as <em>inactive</em>and at the same time spawns a background thread to ask the replica to recover. Both of these actions together make sure that a replica which loses an update neither becomes a leader nor receives traffic from other Solr nodes and smart clients before recovering from a leader node.

Solr nodes (and Solrj clients) forward search requests to <em>active</em> replicas. The <em>active</em> replicas will continue to serve search traffic even if they lose connectivity to ZooKeeper. If the entire ZooKeeper cluster becomes unavailable then the cluster state is effectively frozen which means that searches continue to be served by whoever was active at the time of ZooKeeper going down, but replica recovery cannot happen during this time. However replicas which are not <em>active</em> are allowed to return results if, somehow, a non-distributed request reaches them. This is needed for the <em>sync</em> that happens during leader election as well as useful for debugging at times.

In summary, SolrCloud chooses consistency over availability during writes and it prefers consistency for searches but under severe conditions such as ZooKeeper being unavailable, degrades to <em>possibly</em> serving stale data. In the CAP theorem world, this makes Solr a CP system, with some mitigating heuristics to try and keep availability in certain circumstances.</li>
</ul>
</div>
</div>
</div>
</div>
</div>
</div>
<h1 id="title-text" class="with-breadcrumbs"><a href="https://cwiki.apache.org/confluence/display/solr/Nodes%2C+Cores%2C+Clusters+and+Leaders">Leaders</a></h1>
<ol>
 	<li>
<h2 id="Nodes,Cores,ClustersandLeaders-LeadersandReplicas">Leaders and Replicas</h2>
The concept of a <em>leader</em> is similar to that of <em>master</em> when thinking of traditional Solr replication. The leader is responsible for making sure the <em>replicas</em> are up to date with the same information stored in the leader.

However, with SolrCloud, you don't simply have one master and one or more "slaves", instead you likely <strong>have distributed your search and index traffic to multiple machines.</strong></li>
 	<li>Example
<ol>
 	<li>If you have bootstrapped Solr with <code>numShards=2</code>, for example, your indexes are split across both shards.</li>
 	<li>In this case, both cores/shards are considered leaders.</li>
 	<li>If you start more Solr nodes after the initial two, these will be automatically assigned as replicas for the leaders.</li>
 	<li>Replicas are assigned to shards in the order they are started the first time they join the cluster. This is done in a round-robin manner, unless the new node is manually assigned to a shard with the <code>shardId</code> parameter during startup.</li>
</ol>
</li>
</ol>
&nbsp;
<h1>Zookeeper - Workflow</h1>
Once a ZooKeeper ensemble starts, it will wait for the clients to connect. Clients will connect to one of the nodes in the ZooKeeper ensemble. It may be a leader or a follower node. Once a client is connected, the node assigns a session ID to the particular client and sends an acknowledgement to the client. If the client does not get an acknowledgment, it simply tries to connect another node in the ZooKeeper ensemble. Once connected to a node, the client will send heartbeats to the node in a regular interval to make sure that the connection is not lost.
<ul class="list">
 	<li><b>If a client wants to read a particular znode,</b> it sends a <b>read request</b> to the node with the znode path and the node returns the requested znode by getting it from its own database. For this reason, reads are fast in ZooKeeper ensemble.</li>
 	<li><b>If a client wants to store data in the ZooKeeper ensemble</b>, it sends the znode path and the data to the server. The connected server will forward the request to the leader and then the leader will reissue the writing request to all the followers. If only a majority of the nodes respond successfully, then the write request will succeed and a successful return code will be sent to the client. Otherwise, the write request will fail. The strict majority of nodes is called as <b>Quorum</b>.</li>
</ul>
<h2>Sessions</h2>
Sessions are very important for the operation of ZooKeeper. Requests in a session are executed in FIFO order. Once a client connects to a server, the session will be established and a <b>session id</b> is assigned to the client.

The client sends <b>heartbeats</b> at a particular time interval to keep the session valid. If the ZooKeeper ensemble does not receive heartbeats from a client for more than the period (session timeout) specified at the starting of the service, it decides that the client died.

Session timeouts are usually represented in milliseconds. When a session ends for any reason, the ephemeral znodes created during that session also get deleted.
<h2>Watches</h2>
Watches are a simple mechanism for the client to get notifications about the changes in the ZooKeeper ensemble. Clients can set watches while reading a particular znode. Watches send a notification to the registered client for any of the znode (on which client registers) changes.

Znode changes are modification of data associated with the znode or changes in the znode’s children. Watches are triggered only once. If a client wants a notification again, it must be done through another read operation. When a connection session is expired, the client will be disconnected from the server and the associated watches are also removed.
<h2>ZooKeeper Data Model - Hierarchical Namespace</h2>
The following diagram depicts the tree structure of ZooKeeper file system used for memory representation. ZooKeeper node is referred as <b>znode</b>. Every znode is identified by a name and separated by a sequence of path (/).
<ul class="list">
 	<li>In the diagram, first you have a root <b>znode</b> separated by “/”. Under root, you have two logical namespaces <b>config</b> and <b>workers</b>.</li>
 	<li>The <b>config</b> namespace is used for centralized configuration management and the <b>workers</b> namespace is used for naming.</li>
 	<li>Under <b>config</b> namespace, each znode can store upto 1MB of data. This is similar to UNIX file system except that the parent znode can store data as well. The main purpose of this structure is to store synchronized data and describe the metadata of the znode. This structure is called as <b>ZooKeeper Data Model</b>.</li>
 	<li>
<p id="gFbFTXW"><img class="alignnone size-full wp-image-1537 " src="/wp-content/uploads/2018/05/img_5aec158c44949.png" alt="" /></p>
</li>
 	<li>Every znode in the ZooKeeper data model maintains a <b>stat</b> structure. A stat simply provides the <b>metadata</b> of a znode. It consists of <i>Version number, Action control list (ACL), Timestamp, and Data length.</i>
<ul class="list">
 	<li><b>Version number</b> − Every znode has a version number, which means every time the data associated with the znode changes, its corresponding version number would also increased. The use of version number is important when multiple zookeeper clients are trying to perform operations over the same znode.</li>
 	<li><b>Action Control List (ACL)</b> − ACL is basically an authentication mechanism for accessing the znode. It governs all the znode read and write operations.</li>
 	<li><b>Timestamp</b> − Timestamp represents time elapsed from znode creation and modification. It is usually represented in milliseconds. ZooKeeper identifies every change to the znodes from “Transaction ID” (zxid). <b>Zxid</b> is unique and maintains time for each transaction so that you can easily identify the time elapsed from one request to another request.</li>
 	<li><b>Data length</b> − Total amount of the data stored in a znode is the data length. You can store a maximum of 1MB of data.</li>
</ul>
</li>
</ul>
<h3>Types of Znodes</h3>
Znodes are categorized as persistence, sequential, and ephemeral.
<ul class="list">
 	<li><b>Persistence znode</b> − Persistence znode is alive even after the client, which created that particular znode, is disconnected. By default, all znodes are persistent unless otherwise specified.</li>
 	<li><b>Ephemeral znode</b> − Ephemeral znodes are active until the client is alive. When a client gets disconnected from the ZooKeeper ensemble, then the ephemeral znodes get deleted automatically. For this reason, only ephemeral znodes are not allowed to have a children further. If an ephemeral znode is deleted, then the next suitable node will fill its position. Ephemeral znodes play an important role in Leader election.</li>
 	<li><b>Sequential znode</b> − Sequential znodes can be either persistent or ephemeral. When a new znode is created as a sequential znode, then ZooKeeper sets the path of the znode by attaching a 10 digit sequence number to the original name. For example, if a znode with path <b>/myapp</b> is created as a sequential znode, ZooKeeper will change the path to <b>/myapp0000000001</b> and set the next sequence number as 0000000002. If two sequential znodes are created concurrently, then ZooKeeper never uses the same number for each znode. Sequential znodes play an important role in Locking and Synchronization.</li>
</ul>
&nbsp;
<h2>Nodes in a ZooKeeper Ensemble</h2>
Let us analyze the effect of having different number of nodes in the ZooKeeper ensemble.
<ul class="list">
 	<li>If we have <b>a single node</b>, then the ZooKeeper ensemble fails when that node fails. It contributes to “Single Point of Failure” and it is not recommended in a production environment.</li>
 	<li>If we have <b>two nodes</b> and one node fails, we don’t have majority as well, since one out of two is not a majority.</li>
 	<li>If we have <b>three nodes</b> and one node fails, we have majority and so, it is the minimum requirement. It is mandatory for a ZooKeeper ensemble to have at least three nodes in a live production environment.</li>
 	<li>If we have <b>four nodes</b> and two nodes fail, it fails again and it is similar to having three nodes. The extra node does not serve any purpose and so, it is better to add nodes in odd numbers, e.g., 3, 5, 7.</li>
</ul>
We know that a write process is expensive than a read process in ZooKeeper ensemble, since all the nodes need to write the same data in its database. So, it is better to have less number of nodes (3, 5 or 7) than having a large number of nodes for a balanced environment.
<p id="OerZfGN"><img class="size-full wp-image-1538 aligncenter" src="/wp-content/uploads/2018/05/img_5aec1655d9fb1.png" alt="" /></p>

<table class="table table-bordered">
<tbody>
<tr>
<th>Component</th>
<th>Description</th>
</tr>
<tr>
<td>Write</td>
<td>Write process is handled by the leader node. The leader forwards the write request to all the znodes and waits for answers from the znodes. If half of the znodes reply, then the write process is complete.</td>
</tr>
<tr>
<td>Read</td>
<td>Reads are performed internally by a specific connected znode, so there is no need to interact with the cluster.</td>
</tr>
<tr>
<td>Replicated Database</td>
<td>It is used to store data in zookeeper. Each znode has its own database and every znode has the same data at every time with the help of consistency.</td>
</tr>
<tr>
<td>Leader</td>
<td>Leader is the Znode that is responsible for processing write requests.</td>
</tr>
<tr>
<td>Follower</td>
<td>Followers receive write requests from the clients and forward them to the leader znode.</td>
</tr>
<tr>
<td>Request Processor</td>
<td>Present only in leader node. It governs write requests from the follower node.</td>
</tr>
<tr>
<td>Atomic broadcasts</td>
<td>Responsible for broadcasting the changes from the leader node to the follower nodes.</td>
</tr>
</tbody>
</table>
<h3>Exceptional Scenarios</h3>
<ul>
 	<li>One of the questions I tend to get is what happens with SolrCloud cluster when ZooKeeper fails. Of course we are not talking about a single ZooKeeper instance failure, but the whole <em>ensemble</em> not being accessible and so the <em>quorum</em> not present.
<ul>
 	<li>Even when zookeeper is down we can get the results from Solr. Solr responded correctly. This is because Solr already has the clusterstate.json file cached. To search Solr doesn’t need to update that file, so search should and is working as we could see.</li>
 	<li>Indexing with failed ZooKeeperWithout turning on our ZooKeeper instance we try to index files. After a longer period of time Solr responds that it's not able to index data without working ZooKeeper <em>ensemble</em>.</li>
 	<li>Indexing with ZooKeeper restarted but keeping Solr untouched.
So let’s see what will happen when we start our ZooKeeper instance again without restarting Solr nodes. After starting ZooKeeper we try to run the same indexing command, we just did, once again. As we can see the indexing request was successful this time. This allows us to assume that the connection to ZooKeeper was re-established by Solr. We can see that in Solr and ZooKeeper logs.</li>
 	<li>
<h3>Why we can run queries?</h3>
The situation is quite simple – querying is not an operation that needs to alter SolrCloud cluster state. The only thing Solr needs to do is accept the query, run it against known shards/replicas and gather the results. Of course cluster topology is not retrieved with each query, so when there is no active ZooKeeper connection (or ZooKeeper failed) we don’t have a problem with running queries.

There is also one important and not widely know feature of SolrCloud – the ability to return partial results. By adding the <em>shards.tolerant=true</em> parameter to our queries we inform Solr, that we can live with partial results and it should ignore shards that are not available. This means that Solr will return results even if some of the shards from our collection is not available. By default, when this parameter is not present or set to <em>false</em>, Solr will just return error when running a query against collection that doesn’t have all the shards available.</li>
 	<li>
<h3>Why we can’t index data?</h3>
So, we can’t we index data, when ZooKeeper connection is not available or when ZooKeeper doesn’t have a quorum? Because there is potentially not enough <a href="http://solr.pl/en/informations/" rel="nofollow">information</a> about the cluster state to process the indexing operation. Solr just may not have the fresh information about all the shards, replicas, etc. Because of that, indexing operation may be pointed to incorrect shard (like not to the current leader), which can lead to data corruption. And because of that indexing (or cluster change) operation is just not possible.

It is generally worth remembering, that all operations that can lead to cluster state update or collections update won’t be possible when ZooKeeper quorum is not visible by Solr (in our test case, it will be a lack of connectivity of a single ZooKeeper server).</li>
</ul>
</li>
 	<li>A very good test that shows us data consistency related information can be found at <a href="http://lucidworks.com/blog/call-maybe-solrcloud-jepsen-flaky-networks/#referrer=solr.pl" rel="nofollow">http://lucidworks.com/blog/call-maybe-solrcloud-jepsen-flaky-networks/</a>.</li>
</ul>
<h2>References</h2>
<ul>
 	<li>Quick guide https://www.tutorialspoint.com/zookeeper/zookeeper_quick_guide.htm</li>
 	<li>https://lucene.apache.org/solr/guide/6_6/how-solrcloud-works.html</li>
 	<li>https://cwiki.apache.org/confluence/display/solr/Nodes%2C+Cores%2C+Clusters+and+Leaders</li>
 	<li>https://lucene.apache.org/solr/guide/6_6/setting-up-an-external-zookeeper-ensemble.html</li>
 	<li>https://solr.pl/en/2013/12/02/solrcloud-what-happens-when-zookeeper-fails/</li>
 	<li>https://dzone.com/articles/solrcloud-what-happens-when-0</li>
 	<li>https://www.tutorialspoint.com/zookeeper/zookeeper_overview.htm</li>
</ul>
