---
layout: post
title: No SQL and DynamoDB
date: 2018-03-22 18:07
author: tmasabari
comments: true
categories: [AWS, Databases, DynamoDB, No SQL]
---
<h2>No SQL "Not only SQL."</h2>
<ul>
 	<li>Unstructured data from the web can include <strong>sensor data, social sharing, personal settings, photos, location-based information, online activity, usage metrics</strong>, and more. Trying to store, process, and analyze all of this unstructured data led to the development of <strong>schema-less alternatives to SQL</strong>. Taken together, these alternatives are referred to as <strong>NoSQL, meaning “Not only SQL.” </strong></li>
 	<li>The NoSQL databases enable storing <strong>unstructured and heterogeneous data</strong>.</li>
 	<li>NoSQL databases are <strong>document-oriented</strong>.</li>
 	<li>Storing data in bulk like this requires extra processing effort and more storage than highly organized SQL data. That’s why <a href="https://www.upwork.com/hiring/data/a-guide-to-hadoop/"><strong>Hadoop</strong>, an open-source computing and data analysis platform</a> <strong>capable of processing huge amounts of data</strong> in the cloud, is so popular in conjunction with NoSQL database stacks.</li>
 	<li>The <strong>enhanced scalability</strong> have helped grow their popularity to a greater extent in the current market. <strong style="font-size: 1rem;">Horizontal scaling</strong><span style="font-size: 1rem;"> means the organization doesn't have to worry about the underlying infrastructure. </span></li>
 	<li><span style="font-size: 1rem;">Conceptually, data is stored in JSON files. </span></li>
 	<li>NoSQL databases are often able to sidestep this problem through APIs, which allow developers to execute queries without having to learn SQL or understand the underlying architecture of their database system.</li>
 	<li><span style="font-size: 1rem;">The ability for data to scale out naturally takes advantage of NoSQL's <strong>characteristics</strong>.</span>
<ul>
 	<li>Non-relational.</li>
 	<li>Open source.</li>
 	<li>Cluster-friendly.</li>
 	<li>Schema-Independent.</li>
 	<li>No Join.</li>
 	<li>Heterogeneous.</li>
 	<li>Humongous Volume of data.</li>
 	<li>Easy Development.</li>
 	<li>Easy Administration.</li>
</ul>
</li>
 	<li>Other factors
<ul>
 	<li>license cost,
<ul>
 	<li> lower expense and maintenance overhead</li>
</ul>
</li>
 	<li>business process, and</li>
 	<li>organization decisions</li>
</ul>
</li>
 	<li>Consistency
<ul>
 	<li>With NoSQL, and thus without ACID-compliance, it's very difficult to write reliable software even though it follows the CAP theorem.</li>
 	<li>The problem is that when you have a tremendous amount of data scattered across multiple systems, it’s nearly impossible to maintain transaction consistency that satisfies all the ACID properties.</li>
</ul>
</li>
</ul>
<h3><a href="https://dzone.com/articles/sql-vs-nosql">Vs SQL</a></h3>
<ul>
 	<li>The choice of the database between SQL and NoSQL <strong>cannot be concluded on the differences</strong> between them but the project requirements.</li>
 	<li>If your application has a <strong>fixed structure and doesn’t need frequent modifications,</strong> SQL is a preferable database.</li>
 	<li>Conversely, if you have applications where d<strong>ata is changing frequently and growing rapidly</strong>, like in Big Data analytics, NoSQL is the best option for you.</li>
 	<li>And remember, SQL is not deceased and can never be superseded by NoSQL, or any other database technology.</li>
 	<li>NoSQL existed before SQL’s usage exploded in the 1990s. NoSQL is as old as the 1960s; however, they have gained traction lately with the eruption of several options like MongoDB, Cassandra, and HBase.</li>
</ul>
<p id="GNnlKys"><img class=" wp-image-1266 aligncenter" src="/wp-content/uploads/2018/03/img_5ab3cb1fe5ae7.png" alt="" width="656" height="236" /></p>
http://www.zdnet.com/article/rdbms-vs-nosql-how-do-you-pick/
<table>
<tbody>
<tr>
<td></td>
<td>SQL</td>
<td>NoSQL</td>
</tr>
<tr>
<td>Engines</td>
<td>MSSQL, Oracle, MySQL,Maria, IBM DB2, Sybase, Microsoft Azure, and Postgres</td>
<td>MongoDB, BigTable, Redis, RavenDb, Cassandra, Hbase, Neo4j, Oracle NoSQL, and CouchDB.</td>
</tr>
<tr>
<td> <strong>Nature of data</strong></td>
<td> If the data has a simple tabular structure, like an accounting spreadsheet, then the relational model could be adequate.</td>
<td>  Multi-level nesting and hierarchies are very easily represented in the JavaScript Object Notation (JSON) format used by some NoSQL products. Data not fit into that two-dimensional row-column structure naturally.<strong>
</strong> Data such as geo-spatial, engineering parts, or molecular modeling, on the other hand, tends to be very complex. It may have multiple levels of nesting and the complete data model can be complicated.</td>
</tr>
<tr>
<td>volatility of the data model?</td>
<td>"get it right first" approach: cautioning users to design the schema right the first time, as revisions made later slowed or stopped the database from operating</td>
<td>not be suitable for the new world of dynamic schema, where changes need to be made daily, if not hourly, to fit the ever changing data model.  It is no wonder that many NoSQL users are Web-centric businesses which require a greater amount of flexibility.</td>
</tr>
<tr>
<td><strong>Application development (high coding velocity &amp; agility)</strong></td>
<td>delineated the database administrator (DBA) from the application developer.</td>
<td>very little dependency on dedicated DBAs.

The learning curve on JSON, for example, is quite fast and programmers can build a prototype in days and weeks. Since many NoSQL offerings include an open system,

MongoDB, even offer free courses online</td>
</tr>
<tr>
<td><strong>Operational issues (scale, performance, )</strong></td>
<td><strong>Vertical scaling</strong> is usually recommended at <strong>high cost.</strong> As processors are added, <strong>linear</strong> scaling occurs, up to a point where other <strong>bottlenecks</strong> can appear.

Many commercial RDBMS products offer <strong>horizontal scaling (clustering)</strong> as well, but these are <strong>bolted-on</strong> solutions and can be <strong>very expensive</strong> and <strong>complex</strong>.</td>
<td>address these scale (horizontal scaling or scale-out using commodity servers) and performance issues. Just like Google’s HDFS horizontal scaling architecture for distributed systems in batch processing,

Redundancy (in triplicate) is implemented here for high availability.

&nbsp;</td>
</tr>
<tr>
<td><strong>Consistency and high availability</strong></td>
<td>one should consider an RDBMS if one has multi-row transactions and complex joins.</td>
<td>NoSQL offers choices of strict to relaxed consistency that need to be looked at on a case-by-case basis. Tthey forfeit consistency in favor of high availability.

a document (aka complex object) can be the equivalent of rows joined across multiple tables, and consistency is guaranteed within that object.</td>
</tr>
<tr>
<td><strong>Data warehousing &amp; analytics</strong></td>
<td>RDBMS is a good choice if the query and reporting needs are very critical.

Even in today’s world, Hadoop data is sometimes loaded back to an RDBMS for reporting purposes.</td>
<td>Real time analytics for operational data is better suited to a NoSQL setting. Further, in cases where data is brought together from many upstream systems to build an application (not just reporting), NoSQL is a must. Today, BI tool-support for NoSQL is new, but growing rapidly.</td>
</tr>
<tr>
<td></td>
<td>
<ul>
 	<li>store related data in tables</li>
 	<li>require a schema which defines tables prior to use</li>
 	<li>encourage normalization to reduce data redundancy</li>
 	<li>support table JOINs to retrieve related data from multiple tables in a single command</li>
 	<li>implement data integrity rules</li>
 	<li>provide transactions to guarantee two or more updates succeed or fail as an atomic unit</li>
 	<li>can be scaled (with some effort)</li>
 	<li>use a powerful declarative language for querying</li>
 	<li>offer plenty of support, expertise and tools.</li>
</ul>
</td>
<td>
<ul>
 	<li>store related data in JSON-like, name-value documents</li>
 	<li>can store data without specifying a schema</li>
 	<li>must usually be denormalized so information about an item is contained in a single document</li>
 	<li>should not require JOINs (presuming denormalized documents are used)</li>
 	<li>permit any data to be saved anywhere at anytime without verification</li>
 	<li>guarantee updates to a single document — but not multiple documents</li>
 	<li>provide excellent performance and scalability</li>
 	<li>use JSON data objects for querying
<ul>
 	<li>are a newer, exciting technology.</li>
</ul>
</li>
</ul>
</td>
</tr>
<tr>
<td></td>
<td>
<ul>
 	<li><strong>SQL is digital.</strong> It works best for clearly defined, discrete items with exact specifications. Typical use cases are online stores and banking systems.</li>
</ul>
</td>
<td>
<ul>
 	<li><strong>NoSQL is analog.</strong> It works best for organic data with fluid requirements. Typical use cases are social networks, customer management and web analytics systems.</li>
</ul>
</td>
</tr>
</tbody>
</table>
<h3 align="justify"><strong>Co-existence of RDBMS and NoSQL databases</strong></h3>
<ul>
 	<li>IBM just announced the implementation of the MongoDB API, data representation, query language and wire protocol, thus establishing a way for mobile and other next-generation applications to connect with enterprise database systems such as IBM’s DB2 relational database and its WebSphere eXtreme Scale data grid.</li>
 	<li><span style="font-size: 1rem;">Oracle introduced its NoSQL product 2012.</span></li>
 	<li><span style="font-size: 1rem;">In fact, SQL 2016 has a feature to support JSON queries, just like support for XML.</span></li>
</ul>
<h3 align="justify">Types of NoSQL Databases</h3>
todo comparisons https://kkovacs.eu/cassandra-vs-mongodb-vs-couchdb-vs-redis
<p id="CmCWcmf"><img class="alignnone size-full wp-image-1267 " src="/wp-content/uploads/2018/03/img_5ab3d4017b612.png" alt="" /></p>

<h4>Key-Value Model</h4>
The <strong>least complex</strong> NoSQL option, which stores data in a<strong> schema-less</strong> way that consists of <strong>indexed keys and values</strong>. Examples: Cassandra, Azure, LevelDB, and Riak.
<h4>Column Store — or Wide-Column Store</h4>
It stores data tables as columns rather than rows. It’s more than <strong>just an inverted table</strong> — sectioning out columns allows for excellent scalability and high performance. Examples: <strong>HBase, BigTable, and HyperTable</strong>.
<h4>Document Database</h4>
Taking the <strong>key-value concept and adding</strong> more complexity, <strong>each document</strong> in this type of database has its <strong>own data and its own unique key</strong>, which is used to retrieve it. It’s a great option for storing, retrieving, and managing data that’s document-oriented but still somewhat structured. Examples: <strong>MongoDB and CouchDB</strong>.
<h4 align="justify"><strong>Graph Database</strong></h4>
<p align="justify">Here, the <strong>data is interconnected and best represented as a graph</strong>. This method is capable of lots of complexity. Examples: <strong>Polyglot and Neo4J</strong>.</p>

<h3>REASONS TO USE A NOSQL DATABASE</h3>
<ol>
 	<li><strong>Storing large volumes of data that often have little to no structure.</strong> A NoSQL database sets <strong>no limits on the types of data</strong> you can store together, and allows you to <strong>add different new types</strong> as your needs change. With <strong>document-based</strong> databases, you can store data in one place <strong>without</strong> having to <strong>define what “types” of data</strong> those are in advance.</li>
 	<li><strong>Making the most of cloud computing and storage.</strong> Cloud-based storage is an excellent cost-saving solution, but <strong>requires data to be easily spread across multiple servers</strong> to scale up. Using commodity (affordable, smaller) hardware on-site or in the cloud saves you the hassle of additional software, and NoSQL databases like Cassandra are designed to be scaled across multiple data centers out of the box without a lot of headaches.</li>
 	<li><strong>Rapid development.</strong> If you’re developing within two-week Agile sprints, cranking out quick iterations, or needing to <strong>make frequent updates to the data structure without a lot of downtime between versions</strong>, a relational database will slow you down. NoSQL data doesn’t need to be prepped ahead of time.</li>
</ol>
<h3><a href="https://www.networkworld.com/article/2999856/big-data-business-intelligence/10-use-cases-where-nosql-will-outperform-sql.html">Use cases</a></h3>
todo https://www.sitepoint.com/sql-vs-nosql-choose/
<ul>
 	<li>Once only used by the likes of Google, Amazon and Facebook, many industries are now adopting NoSQL database technology for crucial business applications, replacing their relational database deployments to gain flexibility and scalability.</li>
 	<li><strong>* Personalization. </strong>A personalized experience requires data, and lots of it – demographic, contextual, behavioral and more. The more data available, the more personalized the experience.
<ul>
 	<li>However, relational databases are overwhelmed by the volume of data required for personalization. In contrast, a distributed NoSQL database can scale elastically to meet the most demanding workloads and build and update visitor profiles on the fly, delivering the low latency required for real-time engagement with your customers.</li>
</ul>
</li>
 	<li><strong>* Profile Management. </strong>User profile management is core to Web and mobile applications to enable online transactions, user <strong>preferences</strong>, user <strong>authentication</strong> and more. Today, Web and mobile applications<strong> support millions – or even hundreds of millions – of users.</strong>
<ul>
 	<li>While <strong>relational</strong> databases can struggle to serve this amount of user profile data as they are <strong>limited to a single server</strong>, distributed databases can scale out across multiple servers.</li>
 	<li>With NoSQL, capacity is increased simply by adding commodity servers, making it far easier and less expensive to scale.</li>
</ul>
</li>
 	<li><strong>* Real-Time Big Data. </strong>The ability to extract information from <strong>operational data in real-time</strong> is critical for an agile enterprise. It increases <strong>operational efficiency, reduces costs, and increases revenue</strong> by enabling you to <strong>act immediately</strong> on current data.
<ul>
 	<li>In the past, operational databases and analytical databases were maintained as different environments. The operational database powered applications while the <strong>analytical database was part of the business intelligence and reporting</strong> environment.</li>
 	<li>Today, NoSQL is used <strong>as both the front-end</strong> – to store and manage operational data from any source, and to <strong>feed data to Hadoop</strong> – as well as the<strong> back-end</strong> to receive, store and serve analytic results from Hadoop.</li>
</ul>
</li>
 	<li><strong>* Content Management. </strong>The key to effective content is the ability to select a variety of content, aggregate it and present it to the customer at the moment of <span class="skimlinks-unlinked">interaction. <strong>NoSQL</strong></span><strong> document databases</strong>, with their flexible data model, are perfect for storing any type of content – <strong>structured, semi-structured or unstructured</strong> – because NoSQL document databases don’t require the data model to be defined first. Not only does it enable enterprises to easily create and produce new types of content, it also enables them to<strong> incorporate user-generated content, such as comments, images, or videos posted on social media</strong>, with the same ease and agility.</li>
 	<li><strong>* Catalog. </strong>Catalogs are not only referenced by <strong>Web and mobile</strong> applications, they also enable <strong>point-of-sale terminals, self-service kiosks</strong> and more. As enterprises offer more products and services, and collect more reference data, <strong>catalogs become fragmented by application and business unit or brand</strong>.
<ul>
 	<li>Because relational databases rely on fixed data models, it’s not uncommon for multiple applications to access multiple databases, which introduces complexity and data management challenges.</li>
 	<li>By contrast, a NoSQL document database, with its flexible data model, enables enterprises to more easily aggregate catalog data within a single database.</li>
</ul>
</li>
 	<li><strong>* Customer 360° View. </strong>Customers expect a consistent experience regardless of channel, while the enterprise wants to <strong>capitalize on upsell/cross-sell opportunities</strong> and to provide the highest level of customer service.
<ul>
 	<li>However, as the number of products and services, channels, brands and business units increases, the fixed data model of relational databases <strong>forces enterprises to fragment customer data</strong> because different applications work with different customer data.</li>
 	<li>NoSQL document databases use a flexible data model that enables multiple applications to access the <strong>same customer data as well as add new attributes</strong> without affecting other applications.</li>
</ul>
</li>
 	<li><strong>* Mobile Applications</strong>. With nearly two billion smartphone users, mobile applications face scalability challenges in terms of growth and volume. For instance, it is <strong>not uncommon for mobile games to reach tens of millions of users in a matter of </strong><span class="skimlinks-unlinked"><strong>months</strong>.</span>
<ul>
 	<li><span class="skimlinks-unlinked">With</span> a <strong>distributed, scale-out database</strong>, mobile applications can start with a small deployment and expand as the user base grows, <strong>rather than deploying an expensive, large</strong> relational database server from the beginning.</li>
</ul>
</li>
 	<li><strong>* Internet of Things. </strong>Today, some 20 billion devices are connected to the Internet – everything from smartphones and tablets to home appliances and systems installed in cars, hospitals and warehouses. The volume, velocity, and variety of machine-generated data are increasing with the proliferation of digital telemetry, which is semi-structured and continuous.
<ul>
 	<li>Relational databases struggle with the three well-known challenges from big data IoT applications:<strong> scalability, throughput, and data variety</strong>.</li>
 	<li>By contrast, NoSQL allows enterprises to scale concurrent data access to millions of connected devices and systems, store large volumes of data, and meet the performance requirements of mission-critical infrastructure and operations.</li>
</ul>
</li>
 	<li><strong>* Digital Communications. </strong>In an enterprise environment, digital communication may take the form of online interaction via <strong>direct messaging to help visitors find a product or complete the checkout process</strong>. And as with <strong>mobile text messaging</strong>, the application may need to support millions of website visitors.
<ul>
 	<li>Relational databases are limited in responsiveness and scalability while NoSQL databases, thanks to their distributed architecture, deliver the sub-millisecond responsiveness and elastic scalability that digital communication applications require.</li>
</ul>
</li>
 	<li><strong>* Fraud Detection. </strong>For financial service organizations, fraud detection is <strong>essential to reducing profit loss, minimizing financial exposure and complying with regulations</strong>. When <strong>customers pay with a credit or debit card, they expect immediate confirmation</strong>. The process impacts both the enterprise and its customers. Fraud Detection <strong>relies on data – detection algorithm rules, customer information, transaction information, location, time of day and more</strong> – applied at scale and in less than a <strong>millisecond</strong>.
<ul>
 	<li>While relational databases struggle to meet this low latency requirement, elastically scalable NoSQL databases can reliably deliver the required performance..</li>
</ul>
</li>
</ul>
&nbsp;

&nbsp;
<ol>
 	<li>No SQL
<ol>
 	<li>Flexible</li>
 	<li>scalable</li>
 	<li>high performance</li>
</ol>
</li>
 	<li>employ different data modeling techniques</li>
 	<li>key value pairs</li>
 	<li>managed service - regular advantages</li>
 	<li>table data stored in SSD</li>
 	<li>copied over serveral AZs in region</li>
 	<li>spread particular data over adquate number of servers</li>
 	<li>Key concepts
<ol>
 	<li>Table - data arranged in rows and columns</li>
 	<li>Items and attributes
<ol>
 	<li>item - row
<ol>
 	<li>can't be more than 400 KB (including all attributes and values)</li>
</ol>
</li>
 	<li>attribute is fundamendal data model where you can't break any further
<ol>
 	<li>attribute - columns - fields</li>
 	<li>key value pair</li>
 	<li>can contain set of values, json document or a single value (scalar)</li>
 	<li>attributes and datatypes need not to specified in advance except primary key</li>
</ol>
</li>
</ol>
</li>
 	<li>data types - 3 categories
<ol>
 	<li>Scalar
<ol>
 	<li>Number
<ol>
 	<li>limit of precisoin up to 38 digits</li>
 	<li>trailing and leading zeros are trimmed</li>
 	<li>all numbers are sent as string to dynamo db</li>
 	<li></li>
</ol>
</li>
 	<li>String
<ol>
 	<li>Unicode - independent of platform or language or software</li>
 	<li>U-T-F-8 binary encoding  - Unicode transformation format</li>
 	<li>each unicode character has unique decimal number or coe point</li>
 	<li>binary encoding determines how to transform in to binary numbers for storage purpose</li>
 	<li>As name, U-T-F-8 uses 4 blocks each 8 bits long to represent character into its binary state</li>
 	<li>no maixmum limit for the size of value when assigning to an attribute (except primary key)</li>
</ol>
</li>
 	<li>Binary
<ol>
 	<li>any binary such as image or compressed data</li>
 	<li>while comparing each byte is considered as unsigned</li>
 	<li>for processing and easy transmission of data, binary is converted to base 64 format (ASCII text)</li>
 	<li>no maixmum limit for the size of value when assigning to an attribute (except primary key)</li>
</ol>
</li>
 	<li>Boolean true/fase</li>
 	<li>Null - unknown or undefined - can't be primary key</li>
</ol>
</li>
 	<li>Document - json format, list/map can be nested
<ol>
 	<li>List - unordered set of values</li>
 	<li>Maps - ordered set of vaues</li>
</ol>
</li>
 	<li>Set - multi value columns, values must be unique, need not be in order, can be empty
<ol>
 	<li>String set - ex 2 or more authors</li>
 	<li>Number Set-</li>
 	<li>Binary Set</li>
</ol>
</li>
</ol>
</li>
 	<li><span style="background-color: #ff6600;">Primary key</span>
<ol>
 	<li>during CUD specify the primarykey
<p id="NwuPnWY"><img class="alignnone size-full wp-image-1261 " src="/wp-content/uploads/2018/03/img_5ab3982b2d0be.png" alt="" /></p>
</li>
</ol>
</li>
 	<li><span style="background-color: #ff6600;">secondary indexes</span></li>
 	<li>item distribution
<ol>
 	<li>date stored in partitions</li>
 	<li>partition
<ol>
 	<li>storage space allocated for a table</li>
 	<li>once the maximum capacity is reached, new partition is created and data is distributed</li>
 	<li>never combine the allocated partitions</li>
 	<li>never deallocates the allocated</li>
 	<li>if you delete some or all items the partition will remain</li>
</ol>
</li>
 	<li>if table contains simple primary key, fetch by the primary key</li>
 	<li>if composite key used
<ol>
 	<li>hash value is calculated to identify the partition</li>
 	<li>values are stored in the order of sort key values</li>
</ol>
</li>
</ol>
</li>
</ol>
</li>
</ol>
9 Features
<ol>
 	<li>Document data model support - json format , CRUD with GUI tool</li>
 	<li>Key Value data model support</li>
 	<li>schema less
<ol>
 	<li>items can have different no of attributes and different type of attributes</li>
</ol>
</li>
 	<li>seamless scaling
<ol>
 	<li>no maximum limit for storage</li>
 	<li>no max limit for read or write throughput</li>
</ol>
</li>
 	<li>local development but global scaling
<ol>
 	<li>develop from EC2 instances once ready scale quickly</li>
</ol>
</li>
 	<li>strong consistency, atomic counters
<ol>
 	<li>strong consistency on read / read only the latest values</li>
 	<li> Atomic counters
<ol>
 	<li>increase/decrease numeric attributes in an atomic manner though A-P-I call.</li>
 	<li>commit all changes or rollback everything</li>
</ol>
</li>
</ol>
</li>
 	<li>integrated monitoring - cloud watch
<ol>
 	<li>request throughput</li>
 	<li>latency of table</li>
</ol>
</li>
 	<li>security  - - authentication &amp; authorizatoin
<ol>
 	<li>IAM</li>
</ol>
</li>
 	<li>integration with aws data pipeline
<ol>
 	<li>automatically move / transform data</li>
 	<li>scheduled job without programming</li>
</ol>
</li>
</ol>
Five new features
<ol>
 	<li>Streams
<ol>
 	<li>timed sequence of changes in item level (logging)</li>
 	<li>track recent changes / updates in last 24 hours</li>
 	<li>take backups analyze trends innovative application for replication</li>
</ol>
</li>
 	<li>Cross region replication
<ol>
 	<li>globally distributed application</li>
 	<li>quicker data migration</li>
 	<li>better traffic management</li>
 	<li>lower latency access</li>
 	<li>effortless disaster recovery</li>
</ol>
</li>
 	<li>Triggers
<ol>
 	<li>integrate with Lambdas to provide triggers</li>
 	<li>execute user defined function/task when a change occurs at item level in desired table</li>
</ol>
</li>
 	<li>Free text search
<ol>
 	<li>search its contents - keywords, tags, locations</li>
</ol>
</li>
 	<li>Integration with Titan graph database
<ol>
 	<li>storage and navigation through graph - small or big with billion of edges / vertices</li>
 	<li>optimized for quick navigation</li>
</ol>
</li>
</ol>
<h2>References</h2>
<ul>
 	<li>the best scalability benchmark today is the <a href="http://labs.yahoo.com/news/yahoo-cloud-serving-benchmark/">Yahoo Cloud Serving Benchmark</a>.</li>
 	<li><a href="http://www.odbms.org/blog/2011/05/measuring-the-scalability-of-sql-and-nosql-systems/">YCSB Interview</a></li>
 	<li><a href="http://www.odbms.org/downloads.aspx#nosql">ODBMS.org</a> has various papers and links on NoSQL systems as well as other object stores.</li>
 	<li><a href="http://nosql.mypopescu.com/">NoSQL.mypopescu.com</a> is frequently updated with posts, videos, and articles on NoSQL topics and systems.</li>
 	<li><a href="http://nosql-database.org/">NoSQL-Database.org</a> has lots of good articles, upcoming events, and a complete list of all the systems.</li>
 	<li><a href="http://www.nosqldatabases.com/">NoSQLDatabases.com</a> has regular postings, jobs, upcoming events, and links.</li>
 	<li><a href="http://highscalability.com/">HighScalability.com</a> has good articles on scalability of databases and applications.</li>
 	<li><a href="http://www.linkedin.com/news?viewArticle=&amp;articleID=323780843&amp;gid=2085042&amp;type=news&amp;item=323780843&amp;articleURL=http://www.nosqldatabases.com/main/2011/1/11/nosql-tapes-now-available.html&amp;urlhash=O4Xp">Tim Anglade's NoSQL Tapes</a> include great interviews of leading NoSQL players.</li>
 	<li><a href="http://nosqlweekly.com/">NoSQLWeekly.com</a> offers weekly newsletters on NoSQL systems from Rahul Chaudhary.</li>
 	<li><a href="http://doubleclix.wordpress.com/2010/05/29/nosql-bookmarks/">Krishna Sankar's blog</a> had lots of good NoSQL and cloud computing posts, along with web references.</li>
 	<li><a href="http://www.rackspacecloud.com/blog/2009/11/09/nosql-ecosystem/">Jonathan Ellis</a> has broad knowledge in NoSQL systems and has good posts on his blog.  There are some interesting discussions in the responses as well.</li>
</ul>
