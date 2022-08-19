---
layout: post
title: Table Prefix Vs Schema Vs Database
date: 2018-07-02 21:07
author: tmasabari
comments: true
categories: [Data Model, Design]
---
<ul>
 	<li>naming convention ID Vs Id.</li>
 	<li>According to <a href="http://www.learnersdictionary.com/definition/ID[2]" rel="noreferrer">Merriam-Webster</a>, the abbreviation is "ID". If it were a correct abbreviation, it would have to be "Id." with the period.</li>
 	<li>https://stackoverflow.com/questions/1151338/id-or-id-on-user-interface</li>
</ul>
&nbsp;
<ul>
 	<li>Data that needs to be transactionally and referentially consistent needs to be in the same database. See <a href="http://sqlblog.com/blogs/merrill_aldrich/archive/2011/11/25/one-database-or-ten.aspx" rel="nofollow noreferrer">One Database or Ten?</a></li>
 	<li>Fortunately there are just two mistakes that we can make:
<ul>
 	<li>Separating data that needs to be transactionally consistent into two databases</li>
 	<li>Combining data that has no need to be transactionally consistent into one database</li>
</ul>
</li>
</ul>
<ul>
 	<li>Schemas, introduced in SQL Server 2005, offer a convenient way to separate database users from database object owners. They give DBA’s the ability to protect sensitive objects in the database, and also to group logical entities together.</li>
 	<li>Specifically, it addresses three real-world scenarios:
<ul>
 	<li>Protecting database objects from being altered by users without the knowledge of the database owner</li>
 	<li>Preventing database base objects, independent software vendor (ISV) databases in particular, from ad hoc or incorrect user access leading to poor application performance</li>
 	<li>Bringing related groups of objects (logical entities) together within one physical database to reduce physical database administrative overhead</li>
</ul>
</li>
 	<li>The default schema for a user can be defined by using the DEFAULT_SCHEMA option of the CREATE USER or ALTER USER commands. If no default schema is defined for a user account, SQL Server will assume <strong>dbo</strong> is the default schema.</li>
 	<li>It is important note that if the user is authenticated by SQL Server via the Windows operating system, no default schema will be associated with the user. Therefore if the user creates an object, a new schema will be created and named the same as the user, and the object will be associated with that <em>user schema</em>, though not directly with the user.</li>
 	<li><strong>Managing logical entities in one physical database</strong>: Schemas provide the opportunity to simplify administration of security, backup and restore, and database management by allowing database objects, or entities, to be logically grouped together.</li>
 	<li>This is especially advantageous in situations where those objects are often utilized as a unit by applications. For example, a hotel-management system may be broken down into the following logical entities or modules: Rooms, Bar/Restaurant, and Kitchen Supplies. These entities can be stored as three separate physical databases. Using schemas however, they can be combined as three logical entities in one physical database. This reduces the administrative complexity of managing three separate databases. Schemas help to manage the logical entities separately from one another, but still allow objects to work together where required.</li>
 	<li>Schemas logically group tables, procedures, views together. All employee-related objects in the <code>employee</code> schema, etc.</li>
 	<li>You can also give permissions to just one schema, so that users can only see the schema they have access to and nothing else.</li>
 	<li><i>Unfortunately</i> however, schemas and .NET namespaces don't play very well together from an ORM perspective (<i>namely Entity Framework</i>). Tables in the <code>MyDatabase.MySchema</code> schema don't magically map to entity classes in the <code>MyProject.MyDatabase.MySchema</code> namespace. It's also worth noting that any dot-notation (<code>.</code>) hacks in the table names will end up as underscores (<code>_</code>) in the class names.</li>
 	<li>In a Datawarehouse, with data coming from different sources, you can use a different schema for each source, and then e.g. control access based on the schemas. Also avoids the possible naming collisions between the various source, as another poster replied above.</li>
 	<li>If you keep your schema discrete then you can scale an application by deploying a given schema to a new DB server. (This assumes you have an application or system which is big enough to have distinct functionality).&nbsp;</li>
 	<li>An example, consider a system that performs logging. All logging tables and SPs are in the [logging] schema. Logging is a good example because it is rare (if ever) that other functionality in the system would overlap (that is join to) objects in the logging schema.&nbsp;</li>
 	<li>A hint for using this technique -- have a different connection string for each schema in your application / system. Then you deploy the schema elements to a new server and change your connection string when you need to scale.</li>
 	<li><strong>Implications</strong>The separation of ownership from schemas has important implications:
<ul>
 	<li>Ownership of schemas and schema-owned objects is transferable. This is accomplished using the ALTER AUTHORIZATION command.</li>
 	<li>Objects can be moved between schemas. This is accomplished using the ALTER SCHEMA command.</li>
 	<li>A single schema can contain objects owned by multiple database users.</li>
 	<li>Multiple database users can share a single default schema.</li>
 	<li>Permissions on schemas and schema-contained objects can be managed with greater precision than in earlier releases. This is accomplished using schema GRANT permissions object GRANT permissions.</li>
 	<li>A schema can be owned by any database principal. This includes roles and application roles.</li>
 	<li>A database user can be dropped without dropping objects in a corresponding schema.</li>
 	<li>Code written for earlier releases of SQL Server may return incorrect results, if the code assumes that schemas are equivalent to database users.</li>
 	<li>Catalog views designed for earlier releases of SQL Server may return incorrect results. This includes <strong>sysobjects</strong>.</li>
 	<li>Object access and manipulation are now more complex as well as more secure since they involve an additional layer of security.</li>
</ul>
</li>
</ul>
<h2><a href="https://dba.stackexchange.com/questions/4075/what-are-some-best-practices-for-using-schemas-in-sql-server" target="_blank" rel="nofollow noopener">Best Practices</a></h2>
Useful and practical observations past the white paper mentioned by Marian:
<ul>
 	<li>GRANT on the schema: no more permissions per object. So a new proc in the WebGUI schema automatically has the permissions of the schema</li>
 	<li>Nice groupings in SSMS Object Explorer</li>
 	<li><a href="http://msdn.microsoft.com/en-us/library/bb326599.aspx">OBJECT_SCHEMA_NAME</a></li>
 	<li>You are forced to qualify object names (which is best practice)</li>
</ul>
&nbsp;
<h2>Performance and Common Sense Partitioning</h2>
So, what about the other side of this issue? There are, of course, performance and administrative advantages to partitioning data out where it’s safe to do so. One basic principle of scalability is to avoid global resources (think one huge table) in favor of partitioned resources (several smaller tables). Here are some cases where it can be safe, and advantageous, to separate sets of data into distinct databases:
<ol>
 	<li>True “reference” information that is loosely coupled to the primary database. I have seen this successfully implemented for “lookup data” that may be aggregated together from other areas of an organization, such as other regions or other organizational functions, that is not coupled to an application database in real time. I have also seen it used effectively for small data marts, data warehouses or reporting databases, where reporting information is copied out of a primary database, asynchronously. If such a database is “behind” the main application database, it doesn’t really matter, and whatever interface exists between the two is elastic enough to accommodate that.</li>
 	<li>Audit or application error log information. There are applications where audit or application log data is produced <em>in abundance,</em> i.e. <em>crazy huge tables</em>. It may be safe, if business policies permit, to store this data in its own database with a separate log, enabling different and better administrative and retention policies. Simple example: let’s re-index the transactional database, but maybe let’s <em>not</em> tie up the main application’s database log by re-indexing tens of gigs of log or audit data, where fragmentation of that data isn’t really a concern. Secondarily, perhaps the transaction context for real activity in the main database can be different than the transaction context of audit or error logging so, for example, logging can’t block “real” transactions.</li>
 	<li>Multiple ‘tenants’ using the same application. I have some experience (not a huge amount) with multi-tenant scenarios, and in every case I have seen, it’s been destructive to combine multiple tenants literally into a single database, and much more successful to host the tenants side-by-side, each in their own database. There are some administrative challenges to managing a whole collection of databases, but that can be solved with semi-clever code, tools, and rigor around implementation. The scalability problem of one massive DB is much worse. There are several reasons for this:
<ol>
 	<li>The natural partitioning that results from splitting the DBs out (one tenant cares only about her <em>own</em> transactions) seems always to provide better query performance and scalability than co-mingling data from different audiences into the same tables. There is some penalty in procedure cache, because each different database will have distinct query plans, but having the data partitioned, on balance, tends to make the queries simpler and faster. Table and index scans, when required, are automatically restricted to a small set of data that matches the audience, rather than scanning a huge structure and discarding much of the data because it’s not relevant to the client who is performing a query.</li>
 	<li>Locking and associated concurrency issues can be much simpler, and the damage contained. One tenant locks a table? No problem outside their own world, if they have their own database, and the lock is likely to be much shorter in duration.</li>
 	<li>Tenants frequently want to take data with them when they come and go, and there’s a major advantage in terms of portability and/or archiving if the database for that tenant is physically independent.</li>
 	<li>Scale-out to multiple commodity servers clearly is simpler.</li>
 	<li>Backup and database maintenance across many small databases can be more asynchronous and less impactful than the same for one massive database.</li>
 	<li>The log sequence(s) for each database can be safely and legitimately independent. This makes them smaller, easier to manage, and helps the HA/DR situation.</li>
</ol>
</li>
</ol>
References
<ul>
 	<li><a href="http://sqlblog.com/blogs/merrill_aldrich/archive/2011/11/25/one-database-or-ten.aspx" rel="nofollow noreferrer">One Database or Ten?</a></li>
 	<li>https://www.brentozar.com/archive/2010/05/why-use-schemas/</li>
 	<li>https://stackoverflow.com/questions/529142/what-good-are-sql-server-schemas</li>
 	<li>https://blog.sqlauthority.com/2009/09/07/sql-server-importance-of-database-schemas-in-sql-server/</li>
 	<li>https://www.brentozar.com/archive/2011/06/how-design-multiclient-databases/</li>
</ul>
