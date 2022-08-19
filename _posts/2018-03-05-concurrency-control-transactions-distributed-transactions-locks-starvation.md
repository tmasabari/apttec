---
layout: post
title: Concurrency Control, Transactions, Distributed Transactions, Locks, Starvation
date: 2018-03-05 17:56
author: tmasabari
comments: true
categories: [Interview Preparation, Services, ServiceTransaction, SOA, Transactions, WCF]
---
<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Background</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The intention of this article is to collect the notes on 'Transactions and concurrency control mechanisms' and include my own experiences as quick refresh guide.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I recently read an article where the recommendation was to delay horizontal data spreading until you reach vertical scaling limits. I can think of few pieces of worse advice for an architect. Splitting data is more complex than splitting applications. But if you don't do it at the beginning, applications will ultimately take short cuts that rely on a monolithic schema. These dependencies will be extremely difficult to break in the future.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1>Transactions</h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A transaction is a unit of work, typically encapsulating a number of operations performed in one or more machines and with one or more type of components.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Consistency is the most defining constraint for our application logic, as it determines the type of consistency to expect from the database system. Thus, we need to consider different consistency models and their impacts on the application. We limit our review to the two important main consistency models, from the perspective of our application, which is the client of the database.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>While the following two models are generally opponents of each other, it is noteworthy that Brewer mentions they in fact form a spectrum. As a result, there are some means for trade-offs in between.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>CAP Theorem</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>http://berb.github.io/diploma-thesis/original/061_challenge.html</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Consistency </strong>The consistency property describes a consistent view of data on all nodes of the distributed system. That is, the system assures that operations have an atomic characteristic and changes are disseminated simultaneously to all nodes, yielding the same results.</li><li><strong>Availability </strong>This property demands the system to eventually answer every request, even in case of failures. This must be true for both read and write operations. In practice, this property is often narrowed down to bounded responses in reasonable time. However, Gilbert and Lynch have confirmed the theorem even for unbounded, eventual responses.</li><li><strong>Partition tolerance </strong>This property describes the fact that the system is resilient to message losses between nodes. A partition is an arbitrary split between nodes of a system, resulting in complete message loss in between. This affects the prior properties. Mechanisms for maintaining consistency must cope with messages losses. And according to the availability property, every node of any potential partition must be able to respond to a request.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Distributed data stores are subject to the CAP Theorem. This theorem states that a distributed system can <strong>implement only two of the three features</strong> (Consistency, Availability, and Partition Tolerance) at any one time. In practice, this means that you can either:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Provide a <strong>consistent view of distributed (<em>partitioned</em>) data at the cost of blocking access</strong> to that data while any inconsistencies are resolved. This may take an indeterminate time, especially in systems that exhibit a high degree of latency or if a network failure causes loss of connectivity to one or more partitions.</li><li>Provide <strong>immediate access to the data at the risk of it being inconsistent across sites</strong>.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3><a href="https://en.wikipedia.org/wiki/Concurrency_control">ACID properties</a></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>RDBMS are the predominant database systems currently in use for most applications, including web applications. Their data model and their internals are strongly connected to transactional behaviour when operating on data. </p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>There are four important ACID properties</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><strong><a href="https://en.wikipedia.org/wiki/Atomicity_(database_systems)">Atomicity</a></strong> - Either the effects of all or none of its operations remain (<strong>"all or nothing"</strong> semantics) when a transaction is completed (<em>committed</em> or <em>aborted</em> respectively).
<ul><li>In other words, to the outside world a committed transaction appears (by its effects on the database) to be indivisible (atomic), and an aborted transaction does not affect the database at all.</li><li>Part of the transaction might fail for various reasons like business rule violation, power failure, system crash, hardware failure, etc.</li></ul>
</li><li><strong><a href="https://en.wikipedia.org/wiki/Consistency_(database_systems)">Consistency</a></strong> - A transaction takes the system from one consistent state to<br/>another consistent state
 
<ul><li>Consistent (correct) state, i.e., maintain the predetermined integrity rules (primary/unique key, check/not null constraint, referential integrity with valid reference, cascading rules ) of the database (constraints upon and among the database's objects).</li><li>However, it is the responsibility of the transaction's programmer to make sure that the transaction itself is correct, i.e., performs correctly what it intends to perform (from the application's point of view) while the predefined integrity rules are enforced by the DBMS</li></ul>
</li><li><strong><a href="https://en.wikipedia.org/wiki/Isolation_(database_systems)">Isolation</a></strong> - Transactions cannot interfere with each other (as an end result of their executions). One a transaction will not affect an other transaction if both work concurrently (i.e., the intermediate effects of a transaction must not be visible to other transactions)
<ul><li>Moreover, usually (depending on concurrency control method) the effects of an incomplete transaction are not even visible to another transaction. Providing isolation is the main goal of concurrency control.</li></ul>
</li><li><strong><a href="https://en.wikipedia.org/wiki/Durability_(database_systems)">Durability</a></strong> - : Once a transaction commits, the results are saved in permanent storage. No failure ( like system failure, database crash, hardware failure, power failure etc.) after a commit can undo the results or cause them to get lost.
<ul><li>Effects of successful (committed) transactions must persist through <a href="https://en.wikipedia.org/wiki/Crash_(computing)">crashes</a> (typically by recording the transaction's effects and its commit event in a <a href="https://en.wikipedia.org/wiki/Non-volatile_memory">non-volatile memory</a>).</li></ul>
</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":4} -->
<h4 id="base">BASE</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>This alternative consistency model is basically the subsumption of properties resulting from a system that provides availability and partition tolerance, but no strong consistency [<a href="http://berb.github.io/diploma-thesis/original/0_bibliography.html#Pritchett2008">Pri08</a>]. While a strong consistency model as provided by ACID implies that all subsequent reads after a write yield the new, updated state for all clients and on all nodes of the system, this is weakened for BASE. Instead, the weak consistency of BASE comes up with an inconsistency window, a period in which the propagation oft the update is not yet guaranteed.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Basically available </strong>The availability of the system even in case of failures represents a strong feature of the BASE model.</li><li><strong>Soft state </strong>No strong consistency is provided and clients must accept stale state under certain circumstances.</li><li><strong>Eventually consistent</strong> Consistency is provided in a "best effort" manner, yielding a consistent state as soon as possible.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>The optimistic behaviour of BASE represents a best effort approach towards consistency, but is also said to be simpler and faster. Availability and scaling capacities are primary objectives at the expense of consistency. This has an impact on the application logic, as the developer must be aware of the possibility of stale data. On the other hand, favoring availability over consistency has also benefits for the application logic in some scenarios. For instance, a partial system failure of an ACID system might reject write operations, forcing the application to handle the data to be written somehow. A BASE system in turn might always accept writes, even in case of network failures, but they might not be visible for other nodes immediately. The applicability of relaxed consistency models depends very much on the application requirements. Strict constraints of balanced accounts for a banking application do not fit eventual consistency naturally. But many web applications built around social objects and user interactions can actually accept slightly stale data. When the inconsistency window is on average smaller than the time between request/response cycles of user interactions, a user might not even realize any kind of inconsistency at all.<br/></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li><a href="http://citeseer.ist.psu.edu/544596.html">White paper on CAP/BASE</a></li><li><a href="http://www.rgoarchitects.com/Files/fallacies.pdf">Fallacies of Distributed Computing</a></li></ol>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Design for Active/Active</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>If you do a good job with the preceding BASE recommendations, then you've most likely created an architecture that can service your customers from all of your locations simultaneously. This architecture will serve your disaster recovery needs well as it is a more efficient and responsive approach than an active/passive pattern where only one location is serving traffic at a time. Utilization of your resources will be higher and by placing services nearer your customers, you are better meeting their needs as well. Additionally, active/active designs handle localized geographic events better as traffic can simply be rebalanced from the impacted data center to your remaining data centers. Business continuity is improved.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Traditional active/passive designs for disaster recovery have a complex testability problem that will often offset the challenges of an active/active design. Determining whether the passive data center is truly ready to take traffic can only be done by sending traffic to it. This is difficult to do in an active/passive design without impacting customers. Active/active has an inherent self-proof of suitability for managing traffic.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Transaction Types</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li><strong>Connection Transaction</strong> - Transaction which is tied directly with a database connection (<code>SqlConnection</code>) is called Connection Transaction. <code>SqlTransaction</code> (<code>IDbTransaction</code>) is an example of a connection transaction. In .NET Framework 1.0/1.1 we use <code>SqlTransaction</code>.
<ul><li><strong>Database Transaction</strong> - a series of data manipulation statements( insert /update /delete) execute as a whole.</li></ul>
</li><li><strong>Ambient Transaction </strong>- A transaction which <strong>automatically identifies a code block</strong> that needs to support a transaction without explicitly mentioning any transaction related things.<br/>An ambient transaction is <strong>not tied just to a database, any transaction aware provider can be used.</strong> <code>TransactionScope</code> implements an ambient transaction. Any one can write a transaction aware provider like the WCF implementation.If you see the use of TransactionScope, you will not find transaction related anything sent to any method or setting any property. A code block is automatically attached with the transaction if that code is in any TransactionScope.</li></ol>
<!-- /wp:list -->

<!-- wp:list {"ordered":true} -->
<ol><li><strong>Local Transaction</strong> - A transaction where a series of data manipulation statements execute as a whole on a <strong>single data source/database</strong>. It is actually a single phase<strong> transaction</strong> handled by a database directly.<br/>To manage local transactions, <code>System.Transactions</code> has a Lightweight Transaction Manager (LTM). It acts like a gateway. All transactions are started by <code>System.Transactions</code> are handled directly by this component. If it finds the transaction nature is distributed based on some predefined rules it has a fallback transaction to the MSDTC distributed transaction.</li><li><strong>Distributed Transaction</strong> -A distributed transaction is a transaction that accesses objects managed by multiple servers. If a transaction fails then the affected data sources will be rolled back.
<ol><li>A distributed transaction is much slower than a local transaction.– All servers involved must agree whether to commit or abort</li><li>Open Group, a vendor consortium, proposed the <a href="https://en.wikipedia.org/wiki/X/Open_XA">X/Open Distributed Transaction Processing (DTP) Model</a> (X/Open XA), which became a de facto standard for behavior of transaction model components.</li><li>For .Net, In <code>System.Transactions</code>, MSDTC (Microsoft Distributed Transaction Coordinator) manages distributed transactions. It implements a two phase<strong> commit protocol</strong>.</li></ol>
</li></ol>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Distributed Transactions Explained</h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li><strong>Example</strong>: A bank keeps account information in an RDBMS and distributes and receives money through automated teller machines (ATMs). It is necessary to ensure that ATM actions are correctly reflected in the accounts, but this cannot be done with the RDBMS alone. A global transaction manager integrates the ATM and database resources to ensure overall consistency of financial transactions.</li><li>Applications that use global transactions involve one or more Resource Managers and a Transaction Manager:

<ul><li>A Resource Manager (RM) provides access to transactional resources. A database server is one kind of resource manager. It must be possible to either commit or roll back transactions managed by the RM.</li></ul>
<ul><li>A Transaction Manager (TM) coordinates the transactions that are part of a global transaction. It communicates with the RMs that handle each of these transactions. The individual transactions within a global transaction are “branches” of the global transaction. Global transactions and their branches are identified by a naming scheme described later.</li><li><strong>Example</strong>: The MySQL implementation of XA enables a <strong>MySQL server to act as a Resource Manager</strong> that handles XA transactions within a global transaction. A <strong>client program</strong> that connects to the MySQL server acts as the <strong>Transaction Manager</strong>.</li></ul>

</li><li>The process for executing a global transaction uses two-phase commit (2PC). This takes place after the actions performed by the branches of the global transaction have been executed.

<ol type="1"><li>In the first phase, all branches are prepared. That is, they are told by the TM to get ready to commit. Typically, this means each RM that manages a branch records the actions for the branch in stable storage. The branches indicate whether they are able to do this, and these results are used for the second phase.</li></ol>


In some cases, a global transaction might use one-phase commit (1PC). For example, when a Transaction Manager finds that a global transaction consists of only one transactional resource (that is, a single branch), that resource can be told to prepare and commit at the same time.
</li><li>A distributed transaction can be structured in two ways:<br/>– In a <strong>flat transaction</strong>, operations are invoked sequentially<br/>– In a <strong>nested transaction</strong>, the top‐level transaction can start sub transactions, and each sub transaction can start further sub transactions down to any depth of nesting</li></ol>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Distributed Transaction System Architecture</h2>
<!-- /wp:heading -->

<!-- wp:image {"align":"left"} -->
<div class="wp-block-image"><figure class="alignleft"><img src="https://www.codeproject.com/KB/dotnet/690136/TransactionArchitecture.png" alt=""/></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>We know that in a distributed transaction, several sites are involved. Each site has two components:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Transaction Manager</li><li>Transaction Coordinator</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>1. <strong>Transaction Manager:</strong> Maintains a log and uses that log if recovery is needed. It controls the whole transaction by initiating and completing, and managing the durability and atomicity of a transaction. It also coordinates transactions across one or more resources. There are two types of transaction managers.</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><strong>Local Transaction Manager: </strong>Coordinates transaction over a single resource only.</li><li><strong>Gloabl Transaction Manager:</strong> Coordinates transaction over multiple resources.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>2. <strong>Transaction Coordinator: </strong>Starting the execution of transactions that originate at the site. Distributes subtransactions at appropriate sites so that they can execute in those sites. Coordinates each transaction of each site. As a result the transaction is committed or rolled back to all sites.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><a href="https://gradeup.co/transactions-and-concurrency-control-i-4c5d9b27-c5a7-11e5-bcc4-bc86a005f7ba">Concurrency Control </a>and <a href="https://msdn.microsoft.com/library/dn589800.aspx">Consistency</a></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>Concurrency Control: </strong>Process of managing simultaneous execution of transactions in a shared database, is known as <strong>concurrency control</strong>. Basically, concurrency control ensures that <strong>correct  (&amp; consistent) results for concurrent operations are generated,</strong> while getting those results as quickly as possible.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Schedule</strong><strong>: </strong>A schedule (or history) is a model to describe execution of transactions running in the system. When multiple transactions are executing concurrently in an interleaved fashion, then the order of execution of operations from the various transactions is known as a schedule or we can say that a schedule is a sequence of read, write, abort and commit operations from a set of transactions.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Need of Concurrency Control:</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Simultaneous execution of transactions over a shared database can create several data integrity and consistency problems.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>
<strong>Dirty Read Problems:</strong> This problem occurs when one transaction reads changes the value while the other reads the value before committing or rolling back by the first transaction.
<ul><li>One transaction reads changed data of another tranasction but that data is still not committed. You may take decision/action based on that data. <strong>A problem will arise when data is rolled-back later.</strong> If rollback happens then your decision/action will be wrong and it produces a bug in your application.</li></ul>
</li><li><strong>Non Repeatable Read:</strong> A transaction reads the same data from same table multiple times. A problem will arise when for each read, data is different.</li><li><strong>Phantom Read:</strong> Suppose a transaction will read a table first and it finds 100 rows. A problem will arise when the same transaction goes for another read and it finds 101 rows. The extra row is called a phantom row.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Lost Update:</strong> This problem occurs when two transactions that access the same database items, have their operations interleaved in a way that makes the value of some database items incorrect.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Inconsistent Retrievals:</strong> This problem occurs when a transaction accesses data before and after another transaction(s) finish working with such data.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4><em>Strong</em> data consistency</h4>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Data consistency implies that all instances of an application are presented with the same set of data values all of the time.</li><li>In the world of relational databases, consistency is often <strong>enforced by transactional models that use locks</strong> to prevent concurrent application instances from modifying the same data at the same time.</li><li>In a strongly consistent system, the locks also<strong> block concurrent requests to query data</strong>,  Many applications that store data in non-relational databases, flat files, or other structures follow a similar strategy, known as <strong>pessimistic locking</strong>.</li><li>Many relational databases enable an application to <strong>relax this rule and provide access to a copy of the data that reflects the state it was in before the update started.</strong></li><li><strong>Optimistic concurrency control</strong> means that locks are not held on data in the data store between the moment the data is queried and the moment the data is updated. Data Access checks for changes in the database before <a href="https://docs.telerik.com/data-access/developers-guide/crud-operations/developer-guide-crud-saving">saving changes</a> to the database. Any conflicts will cause  <strong>Optimistic Verification Exception</strong>. The way you handle concurrency exceptions depends on the business rules required by your application.</li><li><strong>Lock</strong><strong>: </strong>A lock is a variable associated with a data item that describes the status of the item with respect to possible operations that can be applied to it. (e.g., read lock, write lock). Locks are used as means of synchronizing the access by concurrent transactions to the database items. There is one lock per database item.</li><li>In the strong consistency model, all changes are atomic. In the time between a transaction starting and completing, <strong>other concurrent transactions may not be able access any of the data that has been modified</strong>; they will be blocked. If data is being replicated, a transaction that implements strong consistency may not be allowed to complete until every copy of each item that has changed has been successfully updated.</li><li>The cost of implementing this model is the impact it has on the availability, performance, and scalability of the resulting solution.</li><li>In a cloud application, you should implement strong consistency only where it is absolutely necessary. For example, if an application updates multiple items that are located within the same data store, the benefits of strong consistency may outweigh the disadvantages because data is likely to be locked only for a very short period. However, if the items to be updated are dispersed across a network, it may be more appropriate to relax the requirement for strong consistency.</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Methods of concurrency control</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Locking (e.g., <strong><a href="https://en.wikipedia.org/wiki/Two-phase_locking">Two-phase locking</a></strong> - 2PL) - Controlling access to data by <a href="https://en.wikipedia.org/wiki/Lock_(computer_science)">locks</a> assigned to the data. Access of a transaction to a data item (database object) locked by another transaction may be blocked (depending on lock type and access operation type) until lock release.</li><li><strong>Serialization <a href="https://en.wikipedia.org/wiki/Serializability#Testing_conflict_serializability">graph checking</a></strong> (also called Serializability, or Conflict, or Precedence graph checking) - Checking for <a href="https://en.wikipedia.org/wiki/Cycle_(graph_theory)">cycles</a> in the schedule's <a href="https://en.wikipedia.org/wiki/Directed_graph">graph</a> and breaking them by aborts.</li><li><strong><a href="https://en.wikipedia.org/wiki/Timestamp-based_concurrency_control">Timestamp ordering</a></strong> (TO) - Assigning timestamps to transactions, and controlling or checking access to data by timestamp order.</li><li><strong><a href="https://en.wikipedia.org/wiki/Commitment_ordering">Commitment ordering</a></strong> (or Commit ordering; CO) - Controlling or checking transactions' chronological order of commit events to be compatible with their respective <a href="https://en.wikipedia.org/wiki/Serializability#Testing_conflict_serializability">precedence order</a>.</li><li><strong><a href="https://en.wikipedia.org/wiki/Multiversion_concurrency_control">Multiversion concurrency control</a></strong> (MVCC) - Increasing concurrency and performance by generating a new version of a database object each time the object is written, and allowing transactions' read operations of several last relevant versions (of each object) depending on scheduling method.</li><li><strong><a href="https://en.wikipedia.org/wiki/Index_locking">Index concurrency control</a></strong> - Synchronizing access operations to <a href="https://en.wikipedia.org/wiki/Index_(database)">indexes</a>, rather than to user data. Specialized methods provide substantial performance gains.</li><li><strong>Private workspace model</strong> (<strong>Deferred update</strong>) - Each transaction maintains a private workspace for its accessed data, and its changed data become visible outside the transaction only upon its commit (e.g., <a href="https://en.wikipedia.org/wiki/Concurrency_control#Weikum01">Weikum and Vossen 2001</a>). This model provides a different concurrency control behavior with benefits in many cases.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>The most common mechanism type in database systems since their early days in the 1970s has been <em><a href="https://en.wikipedia.org/wiki/Two-phase_locking">Strong strict Two-phase locking</a></em> (SS2PL; also called <em>Rigorous scheduling</em> or <em>Rigorous 2PL</em>) which is a special case (variant) of both <a href="https://en.wikipedia.org/wiki/Two-phase_locking">Two-phase locking</a> (2PL) and <a href="https://en.wikipedia.org/wiki/Commitment_ordering">Commitment ordering</a> (CO). It is pessimistic. The idea of the <strong>SS2PL</strong> mechanism is simple: "Release all locks applied by a transaction only after the transaction has ended."</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Locking and Isolation Levels</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Locking is an operation that secures the permission to read, and permission to write a data item.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Purpose of Concurrency Control with Locking</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>To enforce isolation among conflicting transactions.</li><li>To preserve database consistency.</li><li>To resolve read-write, write-read and write-write conflicts.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Types of Locks: </strong>The two types of Locks are given below</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Binary Locks: </strong>A binary lock has two states: Locked/Unlocked. If a database item X is locked, then X cannot be accessed by any other database operation.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Shared/Exclusive Locks </strong>(Read/Write Locks): There are three states:- Read locked / Writelocked / Unlocked. Several transactions can access the same item X for reading (shared lock), however if any of the transactions want to write the item X, the transaction must acquire an exclusive lock on the item.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":691,"align":"left"} -->
<div class="wp-block-image"><figure class="alignleft"><img src="/wp-content/uploads/2018/03/image1-1-300x118.png" alt="" class="wp-image-691"/></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>A Transaction Management System introduces a locking mechanism. With the help of this mechanism one transaction is isolated from another. The locking policy behaves differently based on the Isolation level set for each transaction.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Important isolation levels in .NET transaction scope.</p>
<!-- /wp:paragraph -->

<!-- wp:table -->
<table class="wp-block-table"><thead><tr><th>Isolation Level</th><th>Suggestion</th></tr></thead><tbody><tr><td>Serializable</td><td>(Default- highest level) A <strong>range lock is placed preventing other users</strong> from<em> updating or inserting</em> rows into the database <strong>until the transaction is complete</strong>. It <strong>locks data exclusively at the time of read/writ</strong>e operations. For that reason, many times it <strong>may create a deadlock</strong>, and as a result you may get a timeout exception. You can use this isolation level for a highly secured transactional application like a financial application.</td></tr><tr><td>Repeatable Read</td><td>Same as Serializable except allows phantom rows (allows insert). This prevents non-repeatable reads, but phantom rows are still possible. May use in a financial application or a heavily transactional application but need to know where phantom row creational scenarios are not there.</td></tr><tr><td>Read Committed</td><td><strong>By </strong>default SQL Server uses the Isolation Level <strong>Read Committed</strong>, which means SQL Server acquires a Shared lock, when you read a record, and and when the record was read, the Shared lock is released.  <strong>Non Repeatable Reads can occur</strong>, because someone else can change the data, when you are reading the data twice in your transaction. Phantom rows can also occur
 
Read committed is implemented with an overly optimistic mechanism that delays writing all changes until the transaction is committed
<strong>Most of the applications you can use it. SQL Server default isolation level is this.</strong>
</td></tr><tr><td>Read Un-Committed</td><td>(lowest level) Every read operation may see pending write operations from any transaction (dirty reads).<br/>Volatile data can be read and modified during the transaction.<br/>Applications with these have no need to support concurrent transactions. <strong>An archive database</strong> that is only updated while offline, or an audit/logging table that is not used within a transaction</td></tr><tr><td>Snapshot</td><td>Volatile data can be read. Before a transaction modifies data, it verifies if another transaction has changed the data after it was initially read. If the data has been updated, an error is raised. This allows a transaction to get to the previously committed value of the data.</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:list -->
<ul><li>99 times out of 100, read committed is the right answer. That ensures that you only see changes that have been committed by the other session (and, thus, results that are consistent, assuming you've designed your transactions correctly). But it doesn't impose the locking overhead (particularly in non-Oracle databases) that repeatable read or serializable impose.</li><li>Very occasionally, you may want to run a report where you are willing to sacrifice accuracy for speed and set a read uncommitted isolation level. That's rarely a good idea, but it is occasionally a reasonably acceptable workaround to lock contention issues.</li><li>Serializable and repeatable read are occasionally used when you have a process that needs to see a consistent set of data over the entire run regardless of what other transactions are doing at the time. It may be appropriate to set a month-end reconciliation process to serializable, for example, if there is a lot of procedureal code, a possibility that users are going to be making changes while the process is running and a requirement that the process needs to ensure that it is always seeing the data as it existed at the time the reconciliation started.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Problems Arising with Locks</strong><strong>: </strong>There are two problems which are possible when using locks to control the concurrency among transactions</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Deadlock</strong><strong>: </strong>Two or more competing transactions are waiting for each other to complete to obtain a missing lock.</li><li><strong>Starvation</strong><strong>: </strong>A transaction is continually denying the access to a given data item.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Guaranteeing Serializability by Two-phase Locking</strong><strong>: </strong>A transaction is said to follow the <strong>two-phase locking protocol, </strong>if all locking operations precede the first unlock operation in the transaction.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Such a transaction can be divided into two phases:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Expanding or Growing Phase </strong>During which new locks on items can be acquired but none can be released.</li><li><strong>Shrinking Phase </strong>During which existing locks can be released but no new locks can be acquired.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Deadlock: </strong>A deadlock is a condition in which two or more transaction are waiting for each other deadlock (T<sub>1</sub> and T<sub>2</sub>). An example is given below</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Deadlock Prevention: </strong>A transaction locks all data items; it refers to before it begins execution. This way of locking prevents deadlock, since a transaction never waits for a data item. The conservative two-phase locking uses this approach.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Deadlock Detection and Resolution: </strong>In this approach, deadlocks are allowed to happen. The scheduler maintains a wait-for-graph for detecting cycle. If a cycle exists, then one transaction involved in the cycle is selected (victim) and rolled back.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Deadlock Avoidance: </strong>There are many variations of two-phase locking algorithm. Some avoid deadlock by not lefting the cycle to complete. This is as soon as the algorithm discovers that blocking a translation is likely to create a cycle, it rolls back the transaction.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Starvation: </strong>Starvation occurs when a particular transaction consistently waits or restarted and never gets a chance to proceed further. In a deadlock resolution scheme, it is possible that the same transaction may consistently be selected as victim and rolled back.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Time-stamp Based Concurrency Control Algorithm</strong><strong>: </strong>This is a different approach that guarantees serializability involves using transaction time-stamps to order transaction execution for an equivalent serial schedule.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Time-stamp: </strong>A time-stamp is a unique identifier created by the DBMS to identify a transaction.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Time-stamp is a monotonically increasing variable (integer) indicating the age of an operation or a transaction.</li><li>A larger time-stamp value indicates a more recent event or operation.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Starvation <em>versus </em>Deadlock</strong></p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":642} -->
<figure class="wp-block-image"><img src="/wp-content/uploads/2018/02/img_5a943b3891e87.png" alt="" class="wp-image-642"/></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3> References</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>https://msdn.microsoft.com/library/dn589800.aspx</li><li>https://msdn.microsoft.com/library/dn271399.aspx</li><li>https://msdn.microsoft.com/en-us/library/system.transactions.isolationlevel(v=vs.110).aspx</li><li>https://en.wikipedia.org/wiki/Isolation_(database_systems)</li><li>https://en.wikipedia.org/wiki/Distributed_transaction</li><li>https://en.wikipedia.org/wiki/Concurrency_control</li><li>https://www.codeproject.com/Articles/690136/All-About-TransactionScope</li><li>http://www.c-sharpcorner.com/article/distributed-transaction-coordinatorcontrol-in-Asp-Net-dtc/</li><li>XA https://dev.mysql.com/doc/refman/5.7/en/xa.html</li><li>https://sqlperformance.com/2014/05/t-sql-queries/read-committed-snapshot-isolation</li></ul>
<!-- /wp:list -->
