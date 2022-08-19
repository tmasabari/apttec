---
layout: post
title: Data Model
date: 2018-06-27 14:31
author: tmasabari
comments: true
categories: [Data Model, Design]
---
<h1 style="text-align: justify;">Different types of data</h1>
<table class="chart" style="height: 396px; width: 880px;" cellspacing="0" cellpadding="0">
<thead>
<tr style="height: 84px;">
<th style="width: 127px; height: 84px;">Pattern Name</th>
<th style="width: 69px; height: 84px;">Relative Column Count</th>
<th style="width: 85px; height: 84px;">Relative Row Count</th>
<th style="width: 84px; height: 84px;">Type</th>
<th style="width: 515px; height: 84px;">Notes</th>
</tr>
</thead>
<tbody>
<tr style="height: 28px;">
<td style="width: 127px; height: 28px;"><a href="http://database-programmer.blogspot.com/2008/01/database-skills-sane-approach-to.html#rule1">Lookup</a></td>
<td style="width: 69px; height: 28px;">Small</td>
<td style="width: 85px; height: 28px;">Small</td>
<td style="width: 84px; height: 28px;">Permanent</td>
<td style="width: 515px; height: 28px;">
<ul>
 	<li>Factory settings tables</li>
 	<li>Should not have relationship with any other tables</li>
</ul>
</td>
</tr>
<tr style="height: 28px;">
<td style="width: 127px; height: 28px;"><a href="http://database-programmer.blogspot.com/2008/01/database-skills-sane-approach-to.html#rule1">Reference</a></td>
<td style="width: 69px; height: 28px;">Small</td>
<td style="width: 85px; height: 28px;">Small</td>
<td style="width: 84px; height: 28px;">Permanent</td>
<td style="width: 515px; height: 28px;">
<ul>
 	<li><em>Relating data in a database to information beyond the boundaries of the enterprise. </em></li>
 	<li>Should be inline with standards like ISO for ex. Timezone, countries, states, Zipcode etc.</li>
</ul>
</td>
</tr>
<tr style="height: 28px;">
<td style="width: 127px; height: 28px;"><a href="http://database-programmer.blogspot.com/2008/01/database-skills-sane-approach-to.html#rule3">Master Data (MDM)</a></td>
<td style="width: 69px; height: 28px;">Large</td>
<td style="width: 85px; height: 28px;">Large</td>
<td style="width: 84px; height: 28px;">Permanent</td>
<td style="width: 515px; height: 28px;">
<ul>
 	<li>Many database programmers use the term "master table" to mean any table that lists the properties of things that have some permanence, like customers, teachers, students, school subjects, countries, timezones, items (skus), and anything else that can be listed once and used many times in other places. Generally a master table has more columns than a simple reference table.</li>
 	<li>Compared to the list of students, which is much larger and changes every year, the table of teachers at most schools (except for huge state universities) will have only a few changes each year.</li>
</ul>
</td>
</tr>
<tr style="height: 84px;">
<td style="width: 127px; height: 84px;"><a href="http://database-programmer.blogspot.com/2008/01/database-skills-sane-approach-to.html#rule4">Transactions</a></td>
<td style="width: 69px; height: 84px;">n/a</td>
<td style="width: 85px; height: 84px;">n/a</td>
<td style="width: 84px; height: 84px;">Transient</td>
<td style="width: 515px; height: 84px;">Describes interactions between things, like a customer purchase of an item. Use integer auto-assigned primary key</td>
</tr>
<tr style="height: 144px;">
<td style="width: 127px; height: 144px;"><a href="http://database-programmer.blogspot.com/2008/01/database-skills-sane-approach-to.html#rule5">Cross Reference</a></td>
<td style="width: 69px; height: 144px;">n/a</td>
<td style="width: 85px; height: 144px;">n/a</td>
<td style="width: 84px; height: 144px;">Permanent</td>
<td style="width: 515px; height: 144px;">Describes relationships between master entries, such as an item's price group.

A cross-reference table is any table that lists various facts about how master tables relate to each other. These tables are extremely useful for validating transactions.

Normally Many to Many relationship tables.</td>
</tr>
<tr>
<td style="width: 127px;">Read Only Import Master Table</td>
<td style="width: 69px;">Large</td>
<td style="width: 85px;">Large</td>
<td style="width: 84px;">Periodic refresh</td>
<td style="width: 515px;">
<ul>
 	<li>Many systems today that we create will interact with systems that already exist.</li>
 	<li>For some of these tables, your own system will absolutely never make new rows.</li>
 	<li>A very common example is a table of items on an eCommerce site that is loaded up from some other computer system.</li>
</ul>
</td>
</tr>
<tr>
<td style="width: 127px;">Import &amp; Export Master</td>
<td style="width: 69px;">Large</td>
<td style="width: 85px;">Large</td>
<td style="width: 84px;">Periodic refresh</td>
<td style="width: 515px;">
<ul>
 	<li>Sometimes you may have a table whose original values come from another system, but unlike the previous case your own system is generating new rows for the table, and you may have to send these rows back to the original system.</li>
 	<li>One classic example of this is a list of customers. I created a website a few years ago where the list of customers is updated from a different system from time-to-time. However, new customers can also sign up online. Both systems are handing the customer list back and forth from time to time to keep them reconciled.</li>
 	<li>The most important concept here is that you must not try to combine your key and the key from the original table. Keep the key from the original table in its own column, index on it, and use it for updates, but do not try to enforce it as a unique column. The other system must take care of its own key, and your system must take care of yours.</li>
</ul>
</td>
</tr>
</tbody>
</table>
<ul style="text-align: justify;">
 	<li style="list-style-type: none;"></li>
</ul>
<h4 style="text-align: justify;">Absolute Rule 1: Only Atomic Values</h4>
<p style="text-align: justify;">This is not merely a "rule of thumb" but a rule that I follow absolutely. It is actually part of First Normal Form, which is that column values must be atomic, or indivisible. Another way to say it is that the column must not have "subvalues" buried in it. <strong>Don't use comma separated values.</strong></p>

<h4 style="text-align: justify;">Absolute Rule 2: No Magic Values</h4>
<ul style="text-align: justify;">
 	<li>Another rule that I follow is to absolutely never have magic values. <strong>A magic value is a value in a column that causes some non-obvious result. Use flag columns instead.
</strong></li>
 	<li>Most programmers who break this rule do so by hard-coding special actions to occur based on values of keys in reference tables and master tables.</li>
 	<li>Magic values are bad because the code is harder to debug. It may not be obvious to a programmer that some special value of the TEACHER column would cause special actions to occur. But if you have a column called FLAG_SUBSTITUTE then any programmer who must maintain code written by somebody else will have a much easier time of it.</li>
 	<li>Magic numbers also confuse end-users. It may seem obvious to us that the value "SUBSTITUTE" in the teacher column means substitute, but if this value causes other things to occur, and we are in the regular habit of having these values in lots of tables, then the compound effect can be lots and lots of phone calls from confused users, and big trouble for the software developer's bottom line.</li>
 	<li>Finally, magic numbers limit you. If you use the value "SUBSTITUTE" as a single teacher in the teachers file, then how do you keep track of the dozen-odd substitutes the school may hire in a year? The end-user is stuck here, they must use pen and paper. It is much better to allow them to enter the substitute as a regular faculty member with a FLAG_SUBSTITUE column to check off.</li>
</ul>
<h1 style="text-align: justify;">Logical model vs Physical model</h1>
<ul style="text-align: justify;">
 	<li style="text-align: justify;">There is an assumption in database design that all design can be represented in data models. I have not actually heard this assumption stated, but I have not heard it challenged either.</li>
 	<li style="text-align: justify;">It is true that data modelers will question whether a denormalized data model intended for direct implementation as a database truly represents the enterprise’s view of its data. This is often a reason for disagreement between those responsible for logical data models and those responsible for instantiating physical databases.</li>
 	<li style="text-align: justify;">However, ardent purists never act in a way that questions whether a sound logical data model can capture everything that is needed to understand a database design.</li>
 	<li>In fact, within every physically implemented database, there is a layer of design that is absent from any possible data model, which cannot even be represented in a data model and yet which must be understood to actually use the database.</li>
 	<li>This additional layer of design only exists when data values are populated in a physical database, and it is specified in reference data tables.</li>
</ul>
<table style="border-collapse: collapse; width: 100%;" border="1">
<tbody>
<tr>
<td style="width: 50%;">
<p id="jvElKID"><img class="alignnone size-full wp-image-1565 " src="/wp-content/uploads/2018/06/img_5b32418dd974f.png" alt="" /></p>
Figure shows a <strong>Party</strong> entity, representing legal entities that maybe involved in the sale of a business, and a <strong>Business Sale Transaction</strong> entity, representing an actual sale of a business.

Within the <strong>Business Sale Transaction </strong>entity the <strong>different roles which a party can play are represented by the attributes</strong> <em>Business for Sale ID, Broker ID, Buying Institution ID, Selling Institution ID, Buyer’s Legal Representative ID</em>, and <em>Seller’s Legal Representative ID</em>. All these attributes are role names of the attribute Party ID in the Party entity.</td>
<td style="width: 50%;">
<p id="hygmhST"><img class="alignnone size-full wp-image-1566 " src="/wp-content/uploads/2018/06/img_5b324195c16b2.png" alt="" /></p>
Many data modelers will be tempted to look at Figure 1 and ask themselves if there are so many known roles for institution today, might there not be more in the future? If this question is answered
in the affirmative, the data modeler will likely implement a design like that shown in Figure</td>
</tr>
</tbody>
</table>
<ul style="text-align: justify;">
 	<li>What we see here is how individual attributes at the logical level in one data model can be replaced by records in a physically implemented database table in an equivalent data model. The data modelers have chased design structure out of the logical level into physical reference data tables.</li>
 	<li>The definitions of the institution roles can only be found in the records in the physical database itself.</li>
 	<li>In practice, there is usually no place to store such definitions in reference data tables, so this information is nearly always lost. It is lost from the data model, that is. Users still have to know about it to use the database.</li>
 	<li>No data modeler would add attributes to a data model without specifying definitions, but this is essentially what happens when records are added to the typical reference data table.</li>
</ul>
<h2 style="text-align: justify;">Self-Limited Data Administration</h2>
<ul style="text-align: justify;">
 	<li>More importantly, it needs to be understood that any data model with reference data tables means that a layer of database design is going to exist in the physical database itself and that the facts of this design cannot be found in the data model itself.</li>
 	<li>Data models with many reference data entities always look generalized. We can pretend that we understand the design of the databases such models represent, but we do not and we cannot.</li>
 	<li>Database designs that are deliberately intended to be generalized always have many reference data tables. These include a lot of so-called <strong>COTS (commercial off-the-shelf) software</strong>.</li>
 	<li>Although a customer may think they are getting a standard product, the reality is that this software often needs “configuring.” This is done, in part, by adding values to and selecting values from reference data tables.</li>
 	<li>The result is a design that is very specific to an individual customer, even though the same data model applies to all customers.</li>
 	<li>None of this would be a problem if we acknowledged that we are simply pushing complexity from one level (the logical) to another (the physical), and captured all the metadata involved for reuse.</li>
 	<li>However, data modelers, and traditional data administrators, usually see themselves as concerned only with the logical level. They have the attitude that any data populated into a physically implemented database is solely the responsibility of the business. Hence, the design constructs that the data modelers themselves have chased out of the logical level simply fall onto the unwitting heads of the business users. It should, therefore, come as no surprise that enterprises have a hard time understanding and managing their data.</li>
 	<li>It may be thought that this is too harsh a judgment. After all, many data administration units try to do “codes management.”</li>
 	<li>The problem is that they are still thinking in the paradigm of IT owning the logical design and the business owning the physical data.</li>
 	<li>Also, they tend to think that all data is just data, not that reference data is a special class of data (among others) that has its own special needs – particularly semantic management.</li>
 	<li>This artificial divide between the logical and physical allows data modelers and data administrators to escape from their true responsibilities, and will always limit the capacity of an enterprise to manage its data assets.</li>
</ul>
<h1 style="text-align: justify;">Reference Data</h1>
<ul style="text-align: justify;">
 	<li style="text-align: justify;"><em>Reference data is any kind of data that is used solely to categorize/structure other data found in a database, or solely for relating data in a database to information beyond the boundaries of the enterprise. </em></li>
 	<li><span style="color: white; font-family: Verdana; font-size: small;"><span style="color: #000000;"> It can often be recognised by the appearance of words like 'code' and 'type'. Typical examples include Country Codes, Currency Codes and Payment Methods. </span></span></li>
 	<li><span style="color: white; font-family: Verdana; font-size: small;"><span style="color: #000000;">Within any enterprise it should be defined, recorded and distributed in a standard manner. </span></span></li>
 	<li><span style="color: white; font-family: Verdana; font-size: small;"><span style="color: #000000;">Techniques to do this can range from Spreadsheets and Microsoft Access Databases, a centralized Database to a full-blown Commercial Product, combined with a Publish/Subscribe mechanism. </span></span></li>
 	<li><span style="color: white; font-family: Verdana; font-size: small;"><span style="color: #000000;">Standards should be compliant with any appropriate National and International Standards, for example, Country Codes and Currency Codes are published by <a style="color: #000000;" href="http://www.iso.org/" target="_NEW"><span style="font-size: small;">the International Standards Organization</span></a><span style="font-size: small;">, (ISO).</span></span></span></li>
</ul>
<h1 style="text-align: justify;"><a href="https://www.red-gate.com/simple-talk/sql/database-delivery/master-data-management-mdm-using-sql-server/" target="_blank" rel="nofollow noopener">MDM</a></h1>
<p style="text-align: justify;">All organizations of any size will have a complex set of disparate systems and technologies, including</p>

<ol style="text-align: justify;">
 	<li>Enterprise Resource Planning (ERP),</li>
 	<li>Human Resource Management (HRM),</li>
 	<li>Customer Relationship Management (CRM),</li>
 	<li>Supply Chain Management (SCM), and</li>
 	<li>Financial system.</li>
</ol>
<p style="text-align: justify;">Successful enterprises can grow organically or through acquisition. Either way, this will increase the volume and complexity of the data flowing through enterprise applications.</p>
<p style="text-align: justify;">These systems create a tendency toward data silos.</p>
<p style="text-align: justify;">Disconnected and separate systems bring various issues such as data inconsistency, fragmented data, data inaccuracy, and an increasing difficulty and effort within IT departments in reacting to changing business needs.</p>
<p style="text-align: justify;">It is this increasing task of disentangling the complex data issues that makes the case to have a centralized system that can define, integrate, cleanse, manage, and finally distribute data to various systems.</p>
<p style="text-align: justify;">Master Data Management (MDM) defines a process of collecting enterprise data from various sources, applying standard rules and business processes, building a single view of the data, and finally distributing this ‘golden’ version of data to various systems in the enterprise, thereby making it accessible to all consumers.</p>

<h2 style="text-align: justify;">2 Architectural approaches of MDM</h2>
<p id="MUXofrh" style="text-align: justify;"><img class="alignnone size-full wp-image-1567 " src="/wp-content/uploads/2018/06/img_5b3251cf0c61a.png" alt="" /></p>
<p id="VTuzSEG" style="text-align: justify;"><img class="alignnone size-full wp-image-1568 " src="/wp-content/uploads/2018/06/img_5b325236d2c75.png" alt="" /></p>
<p id="UyslIaV" style="text-align: justify;"><img class="alignnone size-full wp-image-1569 " src="/wp-content/uploads/2018/06/img_5b3252b49530d.png" alt="" /></p>

<h2 style="text-align: justify;">What is Master Data Management</h2>
<p style="text-align: justify;">Master data management (MDM),</p>

<ul style="text-align: justify;">
 	<li style="text-align: justify;">defines a process of collecting enterprise data from various sources,</li>
 	<li style="text-align: justify;">applying standard rules and business processes,</li>
 	<li style="text-align: justify;">building a single view of the data, and</li>
 	<li style="text-align: justify;">finally distributing this ‘golden’ version of data to various systems in the enterprise, thereby making it accessible to all consumers.</li>
</ul>
<p style="text-align: justify;">This is different from existing data warehousing systems. The purpose of data warehousing is to make it easier to perform analytics and business intelligence on historical data from transactional systems as well as from an MDM system. Master Data Management (MDM) <strong>reconciles data from various systems to create a single view of the master data, more usually for operational purposes.</strong></p>
<p style="text-align: justify;">MDM stores data about entities: in other words</p>

<ul style="text-align: justify;">
 	<li>People (Customers, Vendors, Employees, Patients, etc.)</li>
 	<li>Things (Products, Business Units, Parts, Equipment, etc.)</li>
 	<li>Places (Locations, Stores, Geo Areas, etc.)</li>
 	<li>Abstractions (Accounts, Contracts, Time, etc.) which is less frequently changed.</li>
</ul>
<table style="border-collapse: collapse; width: 100%;" border="1">
<tbody>
<tr style="height: 116px;">
<td style="width: 48.7414%; height: 116px;"><img class="alignnone wp-image-1563 " src="/wp-content/uploads/2018/06/img_5b3234f682a8c.png" alt="" width="433" height="246" /></td>
<td style="width: 61.8915%; height: 116px;">
<p id="jvygVAJ"><img class="alignnone wp-image-1562 " src="/wp-content/uploads/2018/06/img_5b3234d3961ae.png" alt="" width="417" height="237" /></p>
</td>
</tr>
</tbody>
</table>
<p style="text-align: justify;"><strong>Data Flow</strong></p>

<ol style="text-align: justify;">
 	<li>MDM provides a way to import data from various sources using different formats into staging tables:</li>
 	<li>It then can map this staged data to domain attributes for standardization and normalization, cleanse data, apply business rules, enrich data, and finally mark it as a ‘named’ version.</li>
 	<li>This named version of data is ready for transferring to downstream systems, usually via web service endpoints, and provide a mechanism for publishing data to subscribed consumers.</li>
</ol>
<p style="text-align: justify;">MDM creates a new version of data every time changes are made, along with information about who is making the change. You can trace it back and look for differences (delta) between various versions, when it was made and who did it. By having this level of auditing history, your organization is helped to achieve complete regulatory compliance and also to provide an overall enterprise information management program.</p>

<ul style="text-align: justify;">
 	<li><strong>Business Rules</strong>
Repository attributes are defined as being of a particular type and with a certain length, but business rules are used for more complex constraints such as where number values should be in range of 5 and 250 or where medicine storage temperature should be between -20F and 80F.</li>
 	<li><strong>Permissions – Authentication and authorization</strong>
Because MDM comes with industry-standard access controls, only authenticated and authorized users can see and make changes to data. Apart from credential-based authentication, most MDM solutions come with role-based security where you can create as many roles as you want based on business domains. Typical roles will be Data steward, approvers, requesters, etc. for data management and Administrator, domain owner, repository owner, deployment, etc. for administration purpose.</li>
 	<li><strong>Web Services</strong>
Master data is not very useful if you do not make it accessible and web services are one of the better ways to access master data and administrative functions.</li>
 	<li><strong>Data Publish</strong>
This is another way, other than Web Services, of making data available for consumption by various current and future consumers in bulk. The difference is that, compared to a pull-based web service approach, this is a push mechanism where MDM systems can publish modified data and interested parties can subscribe to channels.</li>
 	<li><strong>Data Quality</strong>
Data Quality is a tool to profile, cleanse and masks data, while monitoring data quality over time regardless of format or size. By using data de-duplication, validation, standardization, and enrichment you create clean data for access.</li>
</ul>
<h3 style="text-align: justify;">MDS Architecture</h3>
<p style="text-align: justify;">Master Data Services has a three-tier architecture consisting of the database layer, service layer, and UI/Add-in layer. This is illustrated in an architecture diagram below that shows MDS integrated with Data Quality Services and SQL Server Integrations Services. In order to understand MDS the area better, I have put blue rectangular box around the MDS components.</p>
<p id="tEyLQiP" style="text-align: justify;"><img class=" wp-image-1564 aligncenter" src="/wp-content/uploads/2018/06/img_5b3238a0c9106.png" alt="" width="446" height="296" /></p>

<h2 style="text-align: justify;">Data Quality Services (DQS)</h2>
<p style="text-align: justify;">Due to an exponential increase in data sources, it’s highly likely that the data from them is incomplete, inaccurate, duplicate, and possibly missing important business attributes as well. The reasons could be anything from user entry error, by way of corruption in transmission or storage to the use of different data standard by different sources.</p>
<p style="text-align: justify;">Data Quality Services (DQS) provides a way to build a knowledge-base using various data points over time and then it can be used for data correction, enrichment, standardization, and de-duplication of data coming from various data sources. DQS maintains a knowledge base in various domains and each domain is specific for data fields. DQS also supports cloud-based reference data services to cleanse enterprise data using this external knowledge bases.</p>
<p style="text-align: justify;">SQL Server Data Quality Service (DQS) provides following features:</p>

<ul style="text-align: justify;">
 	<li>Knowledge base creation</li>
 	<li>Data Cleansing</li>
 	<li>Data Matching</li>
 	<li>Data De-duplication</li>
 	<li>Data Profiling</li>
</ul>
<p style="text-align: justify;">Data Quality System (DQS) is totally separate from MDM systems and can be used with and without MDM.</p>
&nbsp;
<h2><a href="https://www.brentozar.com/archive/2011/06/how-design-multiclient-databases/" target="_blank" rel="nofollow noopener">Single tenant VS Multi tenant DB</a></h2>
<table style="border-collapse: collapse; width: 100%;" border="1">
<tbody>
<tr>
<td style="width: 40.7595%;">Company A excels at <strong>hardware performance tuning</strong>.

They’re really, really good at wringing the very last bit of performance out of hardware, and they don’t mind replacing their SQL Server hardware on a 12-18 month cycle.  (They refresh web servers every 4-6 months!)

Their Achilles’ heel is extreme compliance and security requirements.

They have incredible auditing needs, and it’s just <strong>easier for them to implement bulletproof controls on a single server</strong>, single database than it is to manage those requirements across thousands of databases on dozens of servers.

They chose one database, one server, many clients.

&nbsp;

<strong>Easier to build an external API.</strong> If we need to grant access to our entire database for outsiders to build products, we can do that easier if all of the data is in a single database.  If the API has to deal with grouping data from multiple databases on multiple servers, it adds development and testing time.  (On the other hand, that “multiple servers” thing starts to hint at a restriction for the one-database-to-rule-them-all scenario: one database usually means all our load impacts just one database server.)

<strong>Easier high availability &amp; disaster recovery.</strong> It’s really, really simple to manage database mirroring, log shipping, replication, and clustering if all we have to worry about is just one database.  We can build a heck of an infrastructure quickly.

<strong>Easier schema management.</strong> When developers deploy a new version of the application, they only have to make schema changes in one database.  There’s no worries about different customers being out of sync or on the wrong version.</td>
<td style="width: 59.2405%;">Company 2 excels at development practices.

Managing schema changes and code deployments across thousands of databases just isn’t an issue for them.

They have <strong>clients around the world</strong>, and they’re processing<strong> secure (credit card)</strong> transactions for those clients around the clock.

They need the ability to spread load geographically, and they don’t want to replace servers around the world every 12-18 months.

They chose one database for each client, and it’s paying off as they start to put SQL Servers in Asia and Europe for their offshore clients

<strong>Easier single-client restores.</strong> Clients  have all kinds of “oops” moments where they want to retrieve all of their data back to a point in time, and that’s a huge pain in the rear if their data is intermingled with other client data in the same tables.  Restores in a single-client-database scenario are brain-dead easy: just restore the client’s database.  No one else is affected.

<strong>Easier data exports.</strong> Clients love getting their hands on their data.  They want the security of knowing they can get their data out anytime they want, avoiding the dreaded vendor lock-in scenario, and they want to do their own reporting.  With each client’s data isolated into their own database, we can simply give them a copy of their own database backup.  We don’t have to build data export APIs.

<strong>Easier per-client performance tuning.</strong> If some clients use different features or reports, we can build a specialized set of indexes or indexed views just for those clients without growing everyone’s data size.

<strong>Easier security management.</strong> As long as we’ve properly locked down security with one user per database, we don’t have to worry about Client X accessing Client Y’s data.  However, if we just use a single login for everyone, then we haven’t really addressed this concern.

<strong>Easier maintenance windows</strong>.  In a global environment where customers are scattered around the globe, it’s easier to take customers offline for maintenance if we can do it in groups or zones.</td>
</tr>
</tbody>
</table>
<h1 style="text-align: justify;">References</h1>
<ul>
 	<li style="text-align: justify;"><a href="http://tdan.com/why-data-models-do-not-work-the-role-of-reference-data/5017" target="_blank" rel="nofollow noopener">http://tdan.com/why-data-models-do-not-work-the-role-of-reference-data/5017</a></li>
 	<li style="text-align: justify;"><a href="http://www.databaseanswers.org/ref_data_overview.htm" target="_blank" rel="nofollow noopener">http://www.databaseanswers.org/ref_data_overview.htm</a></li>
 	<li style="text-align: justify;"><a href="https://www.slideshare.net/Dataversity/lessons-in-data-modeling-data-modeling-mdm" target="_blank" rel="nofollow noopener">https://www.slideshare.net/Dataversity/lessons-in-data-modeling-data-modeling-mdm</a></li>
 	<li style="text-align: justify;"><a href="https://www.red-gate.com/simple-talk/sql/database-delivery/master-data-management-mdm-using-sql-server/" target="_blank" rel="nofollow noopener">https://www.red-gate.com/simple-talk/sql/database-delivery/master-data-management-mdm-using-sql-server/</a></li>
 	<li style="text-align: justify;"><a href="https://www.red-gate.com/simple-talk/sql/database-delivery/master-data-services-basics/" target="_blank" rel="nofollow noopener">https://www.red-gate.com/simple-talk/sql/database-delivery/master-data-services-basics/</a></li>
</ul>
