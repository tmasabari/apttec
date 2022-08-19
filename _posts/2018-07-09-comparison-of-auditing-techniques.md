---
layout: post
title: Comparison of auditing techniques
date: 2018-07-09 14:49
author: tmasabari
comments: true
categories: [Audit, Data Model, Databases, Design]
---
Audit comparison
<table class=".custom-table-table">
<tbody>
<tr>
<th class="custom-table-th">Technique</th>
<th class="custom-table-th">Advantages</th>
<th class="custom-table-th">Disadvantages</th>
<th class="custom-table-th">Suits best when</th>
</tr>
<tr>
<td>Manual auditing</td>
<td>Flexibility</td>
<td>Coding
Development
Cost
Long implementation</td>
<td>A specific auditing solution is needed and no ready-made tool can be used</td>
</tr>
<tr>
<td>SQL Server Auditing</td>
<td>Flexibility
A large number of action types audited
Easy to set
No additional cost</td>
<td>No deleted, inserted, updated records

Can affect the overall performance

Not available in all SQL Server versions and editions</td>
<td>Enterprise, Developer or Evaluation SQL Server editions, when detailed auditing is not necessary, and no info about the records affected is needed</td>
</tr>
<tr>
<td>Using SQL Server triggers</td>
<td>Easy to set

Can track a specific transaction for only specific tables

Flexible storage</td>
<td>Error-prone when triggers and repository are manually created

Can cause overhead in a high transaction database</td>
<td>Not all tables and DML operations need to be audited; auditing data need to be easily accessed and queried</td>
</tr>
<tr>
<td>Reading transaction logs</td>
<td>No additional data capturing

DML and DDL changes can be audited

Can show records that were affected

No overhead</td>
<td>More storage needed

Difficult without a log reader

Not all actions are audited (security, queries, executes, logins, etc.)</td>
<td>High transaction environments with short downtime, where affected records must be seen, and changes rolled back</td>
</tr>
<tr>
<td>Using SQL Server Profiler and SQL Server traces</td>
<td>Flexible

Already available in SQL Server</td>
<td>Complex and error-prone when used manually</td>
<td>A wide range of SQL Server database actions must be audited. It’s recommended to have a tool designed to read traces, filter results and generate reports</td>
</tr>
</tbody>
</table>
&nbsp;
<table>
<tbody>
<tr>
<td></td>
<td><strong>Change Data Capture</strong></td>
<td><strong>ApexSQL Audit</strong></td>
</tr>
<tr>
<td><strong>Supported SQL Server version</strong></td>
<td>SQL Server 2008+</td>
<td>SQL Server 2005+</td>
</tr>
<tr>
<td><strong>Supported SQL Server edition</strong></td>
<td>Enterprise only, except for SQL Server 2016 and higher</td>
<td>Express, Standard, Developer, Enterprise</td>
</tr>
<tr>
<td><strong>Database transaction log</strong></td>
<td>All recovery models are supported, but truncation of the transaction log file in the simple recovery model can be halted until the CDC is performed</td>
<td>No requirements</td>
</tr>
<tr>
<td><strong>Type of auditing</strong></td>
<td>Asynchronous – latency between the change and auditing</td>
<td>Synchronous – auditing immediately follows the change process</td>
</tr>
<tr>
<td><strong>Auditing mechanisms</strong></td>
<td>Transaction log auditing</td>
<td>Trigger-based auditing (for before after) and SQL Trace (for auditing of other SQL Server events)</td>
</tr>
<tr>
<td><strong>Data repository</strong></td>
<td>Decentralized – separate database tables for each audited database</td>
<td>Centralized – regardless of the number of databases or different SQL Server instances, all audited data is stored in a single repository database</td>
</tr>
<tr>
<td><strong>Tamper-evident repository</strong></td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td><strong>Auditing setup</strong></td>
<td>Query-based. Each table must be manually configured for auditing</td>
<td>GUI based. Configuration of multiple tables in different database over many SQL Server instances at once</td>
</tr>
<tr>
<td><strong>SQL Server Agent required</strong></td>
<td>Yes – must be running so that Change Data Capture can function</td>
<td>No</td>
</tr>
<tr>
<td><strong>Audited data details</strong></td>
<td>The change type, value and historical data information are provided</td>
<td>The change type (insert, update, delete), value and historical data information, who made the change, when and how are provided as well as the DDL and configuration changes</td>
</tr>
<tr>
<td><strong>Audited data types</strong></td>
<td>DML only</td>
<td>Almost 200 SQL Server events, server and database levels, including DDL, DML, Security, Query, Execute, Backup/Restore, Warning and Error events</td>
</tr>
<tr>
<td><strong>Reporting</strong></td>
<td>Only via SQL functions (direct querying is not recommended)</td>
<td>Highly specialized GUI enables use of out-of-the-box reports as well as the creation of fully customized reports</td>
</tr>
<tr>
<td><strong>T-SQL Knowledge required</strong></td>
<td>Intermediate level</td>
<td>Beginner level</td>
</tr>
<tr>
<td><strong>Archiving mechanisms</strong></td>
<td>None</td>
<td>Full archiving as well as configuration mechanisms when working with archives</td>
</tr>
<tr>
<td><strong>Alerting</strong></td>
<td>No</td>
<td>Fully customizable before-after change alerting</td>
</tr>
</tbody>
</table>
&nbsp;
<div>

<a class="LW_CollapsibleArea_TitleAhref" title="" role="heading"><span class="LW_CollapsibleArea_Title">Comparison between change tracking and change data capture</span></a>
<div id="Anchor_1" class="LW_CollapsibleArea_Anchor_Div active"></div>
<div class="LW_CollapsibleArea_HrDiv"></div>
</div>
<div class="sectionblock">
<div class="contentTableWrapper">
<table summary="table">
<thead>
<tr>
<th id="th190DB5000000" scope="col">Feature</th>
<th id="th190DB5000001" scope="col">Change Tracking</th>
<th id="th190DB5000002" scope="col">Change Data Capture
(requires Enterprise edition)</th>
</tr>
</thead>
<tbody>
<tr>
<td headers="th190DB5000000" data-th="Feature">Synchronous</td>
<td headers="th190DB5000001" data-th="Change Tracking">Yes</td>
<td headers="th190DB5000002" data-th="Change Data Capture">No</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Requires SQL Agent</td>
<td headers="th190DB5000001" data-th="Change Tracking">No</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Forces full logging of some bulk operations</td>
<td headers="th190DB5000001" data-th="Change Tracking">No</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Prevents log truncation</td>
<td headers="th190DB5000001" data-th="Change Tracking">No</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes, until log records harvested</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Requires snapshot isolation</td>
<td headers="th190DB5000001" data-th="Change Tracking">Recommended</td>
<td headers="th190DB5000002" data-th="Change Data Capture">No</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Requires separate tables to store tracking data</td>
<td headers="th190DB5000001" data-th="Change Tracking">Yes</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Requires primary key</td>
<td headers="th190DB5000001" data-th="Change Tracking">Yes</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Not by default</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Allows placement of tracking tables</td>
<td headers="th190DB5000001" data-th="Change Tracking">No</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Potential for space consumption issues</td>
<td headers="th190DB5000001" data-th="Change Tracking">Some</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Lots</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Automatic cleanup process</td>
<td headers="th190DB5000001" data-th="Change Tracking">Yes</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Yes</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Restrictions on DDL</td>
<td headers="th190DB5000001" data-th="Change Tracking">Yes</td>
<td headers="th190DB5000002" data-th="Change Data Capture">No</td>
</tr>
<tr>
<td headers="th190DB5000000" data-th="Feature">Permission required to enable</td>
<td headers="th190DB5000001" data-th="Change Tracking">Sysadmin</td>
<td headers="th190DB5000002" data-th="Change Data Capture">Database owner</td>
</tr>
</tbody>
</table>
</div>
</div>
&nbsp;

There are total four solutions found in SQL Server, following is the detail:
<ul>
 	<li>SQL Server Change Tracking [CTC]</li>
 	<li>SQL Server Change Data Capture [CDC]</li>
 	<li>SQL Server Audit Trail with Triggers [Generic - Manual]</li>
 	<li>SQL Server Audit</li>
</ul>
<strong>SQL Server Change Tracking [CTC]</strong>

<strong><em>Pros</em></strong>
<ul>
 	<li>Works on all SQL Server editions</li>
 	<li>DML Triggers and additional tables are not required, as single temp table is created by CTC named CHANGETABLE</li>
 	<li>Minimal disk space costs</li>
 	<li>Packaged functions available to query the data</li>
 	<li>Configurable retention policy and Auto clean-up of CHANGETABLE, Also auto clean-up can be turned off when needed</li>
 	<li>No need to access LDF file of that particular database</li>
 	<li>Purging/truncation is possible when CTC enabled</li>
</ul>
<strong><em>Cons</em></strong>
<ul>
 	<li>Need to enable on both database and each required table</li>
 	<li>Synchronous tracking mechanism</li>
 	<li>Tracking data of all tables is stored in single temp table named CHANGETABLE</li>
 	<li>Cannot get historical data also not give exact detail about previous and new data in tracking columns</li>
 	<li>Composite keys support issue</li>
 	<li>Requires primary key</li>
 	<li>Only maintains current state of the data w.r.t operation I = Insert, U = Update, D = Delete</li>
 	<li>SQL Server user group 'sysadmin' can only enable CTC</li>
</ul>
<strong>SQL Server Change Data Capture [CDC]​</strong>

<strong><em>Pros</em></strong>
<ul>
 	<li>This features provide a table-by-table solution, after enabling on database level.</li>
 	<li>Efficient &amp; fast​, asynchronous tracking mechanism ​</li>
 	<li>Can get historical data, also able to give exact detail about previous and new data in shadow table</li>
 	<li>DML triggers are not required, as new table is created by CDC with prefix 'dbo_' and suffix '_CT' for each table.</li>
 	<li>All CDC related tables &amp; functions will be referred with 'cdc' schema.</li>
 	<li>All CDC related stored procedures will be referred with 'sys' or 'cdc' schema</li>
</ul>
<strong><em>Cons</em></strong>
<ul>
 	<li>Information about the user who made the change isn't captured, for that you may need to create some extra columns existing each table desired to be tracked, the columns are like:CreatedAt datetime default (getdate()), CreatedBy nvarchar(100) default (suser_sname()),​ UpdatedAt datetime default (getdate()),​ UpdatedBy nvarchar(100) default (suser_sname())​</li>
 	<li>SQL Server Agent should be enabled for CDC, also CDC can't work properly, when the Database Engine service or the SQL Server Agent service is running under the NETWORK SERVICE account</li>
 	<li>Need to enable on both database and each required table</li>
 	<li>Works only on Enterprise, Developer and DataCenter editions</li>
 	<li>Need to access LDF file of that particular database</li>
 	<li>SQL Server Agent should be enabled to capture the data</li>
 	<li>Purging/truncation is not possible on main table when CDC enabled, Auto clean-up on shadow table can't be turned off once enabled​</li>
 	<li>Extra space is required for transaction log (LDF file)</li>
 	<li>Db's user group 'db_owner' or server's role 'sysadmin' can only enable CDC</li>
 	<li>There are limitations when tracking changes in columns containing XML, Sparse, Timestamp, CLOB and BLOB data types</li>
 	<li>When the caller does not have permission to view the source data, the function returns error 229</li>
</ul>
<strong>Audit Trail with Triggers​ [Generic Solution]</strong>

<strong><em>Pros</em></strong>
<ul>
 	<li>Can get historical data, also able to give exact detail about previous and new data in shadow table</li>
 	<li>Well controlled w.r.t selection of columns, operations [I=Insert, U=Update, D=Delete]</li>
 	<li>Process can be made automated due to complexity, Audit Trail Process can be govern with some routine or service.</li>
 	<li>Purging/truncation as well as auto clean-up can also be automated</li>
</ul>
<strong><em>Cons</em></strong>
<ul>
 	<li>Exact copy of table with some extra columns is required as Shadow Tables</li>
 	<li>Complex process w.r.t development, data management and purging</li>
 	<li>Performance hit when data becomes huge in shadow tables, Purging is required</li>
 	<li>Takes much time to automate the process considering all the important aspects of reliability, security and performance. Which in native solution, DB Engine provides by default.</li>
</ul>
&nbsp;
<h2><a href="https://stackoverflow.com/questions/2015232/database-design-for-audit-logging?noredirect=1&amp;lq=1">Techniques</a></h2>
<strong>My question is:</strong> A decision tree that I can refer to decide which way should I go based on some input variables, like:
<ul>
 	<li>The maturity of the database schema</li>
 	<li>How the logs will be queried</li>
 	<li>The probability that it will be need to recreate records</li>
 	<li>What's more important: write or read performance</li>
 	<li>Nature of the values that are being logged (string, numbers, blobs)</li>
 	<li>Storage space available</li>
</ul>
The approaches that I know are:

<strong>1. Add columns for created and modified date and user</strong>

Table example:
<ul>
 	<li>id</li>
 	<li>value_1</li>
 	<li>value_2</li>
 	<li>value_3</li>
 	<li>created_date</li>
 	<li>modifed_date</li>
 	<li>created_by</li>
 	<li>modified_by</li>
</ul>
Major cons: We lose the history of the modifications. Can't rollback after commit.

<strong>2. Insert only tables</strong>

<a href="https://stackoverflow.com/questions/1051449/ideas-on-database-design-for-capturing-audit-trails/1051494#1051494">Table example</a>:
<ul>
 	<li>id</li>
 	<li>value_1</li>
 	<li>value_2</li>
 	<li>value_3</li>
 	<li>from</li>
 	<li>to</li>
 	<li>deleted (boolean)</li>
 	<li>user</li>
</ul>
Major cons: How to keep foreign keys up to date? Huge space needed

<strong>3. Create a Separate history table for each table</strong>

History table example:
<ul>
 	<li>id</li>
 	<li>value_1</li>
 	<li>value_2</li>
 	<li>value_3</li>
 	<li>value_4</li>
 	<li>user</li>
 	<li>deleted (boolean)</li>
 	<li>timestamp</li>
</ul>
Major cons: Needs to duplicate all audited tables. If the schema changes it will be needed to the migrate all the logs too.

<strong>4. Create a Consolidated history Table for All Tables</strong>

https://stackoverflow.com/questions/39281/database-design-for-revisions

The <a href="http://database-programmer.blogspot.com/2008/07/history-tables.html" rel="nofollow noreferrer">History Tables</a> article in the <a href="http://database-programmer.blogspot.com/" rel="nofollow noreferrer">Database Programmer</a> blog might be usefu
<pre class="lang-sql prettyprint prettyprinted"><code><span class="pun">[</span><span class="pln">ID</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">int</span><span class="pun">]</span> <span class="kwd">IDENTITY</span><span class="pun">(</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">)</span> <span class="kwd">NOT</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">UserID</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">int</span><span class="pun">]</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">EventDate</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">datetime</span><span class="pun">]</span> <span class="kwd">NOT</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">TableName</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">varchar</span><span class="pun">](</span><span class="lit">50</span><span class="pun">)</span> <span class="kwd">NOT</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">RecordID</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">varchar</span><span class="pun">](</span><span class="lit">20</span><span class="pun">)</span> <span class="kwd">NOT</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">FieldName</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">varchar</span><span class="pun">](</span><span class="lit">50</span><span class="pun">)</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">OldValue</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">varchar</span><span class="pun">](</span><span class="lit">5000</span><span class="pun">)</span> <span class="kwd">NULL</span><span class="pun">,</span>
<span class="pun">[</span><span class="pln">NewValue</span><span class="pun">]</span> <span class="pun">[</span><span class="pln">varchar</span><span class="pun">](</span><span class="lit">5000</span><span class="pun">)</span> <span class="kwd">NULL</span></code></pre>
In the <a href="http://database-programmer.blogspot.com/2008/07/history-tables.html" rel="nofollow noreferrer">History Tables</a> essay, the author (<a href="http://database-programmer.blogspot.co.uk/p/about-author.html" rel="nofollow noreferrer">Kenneth Downs</a>), recommends maintaining a history table of at least seven columns:
<ol>
 	<li>Timestamp of the change,</li>
 	<li>User that made the change,</li>
 	<li>A token to identify the record that was changed (where the history is maintained separately from the current state),</li>
 	<li>Whether the change was an insert, update, or delete,</li>
 	<li>The old value,</li>
 	<li>The new value,</li>
 	<li>The delta (for changes to numerical values).</li>
</ol>
Columns which never change, or whose history is not required, should not be tracked in the history table to avoid bloat. Storing the delta for numerical values can make subsequent queries easier, even though it can be derived from the old and new values.

The history table must be secure, with non-system users prevented from inserting, updating or deleting rows. Only periodic purging should be supported to reduce overall size (and if permitted by the use case).
<ul>
 	<li>You can then add a 'LastUpdatedByUserID' column to all of your tables which should be set every time you do an update / insert on the table.</li>
 	<li>You can then add a trigger to every table to catch any insert / update that happens and creates an entry in this table for each field that's changed. Because the table is also being supplied with the 'LastUpdateByUserID' for each update / insert, you can access this value in the trigger and use it when adding to the audit table.</li>
 	<li>I'm sure this system may have drawbacks - for heavily updated databases the performance may be hit, but for my web-app, we get many more reads than writes and it seems to be performing pretty well. We even wrote a little VB.NET utility to automatically write the triggers based on the table definitions.</li>
 	<li>We use the RecordID field to store the value of the key field of the table being updated. If it's a combined key, we just do a string concatenation with a '~' between the fields.</li>
 	<li>No need to store the NewValue, since it's stored in the audited table?
Strictly speaking, that's true. But - when there are a number of changes to the same field over a period of time, storing the new value makes queries such as 'show me all the changes made by Brian' so much easier as all the information about one update is held in one record.</li>
 	<li>I don't rely on sprocs to fill out their values.
They are declared <b>not null </b>and default to current_date or suser_sname() and maintain the modify values using triggers.</li>
 	<li></li>
</ul>
&nbsp;

History table example:
<ul>
 	<li>table_name</li>
 	<li>field</li>
 	<li>user</li>
 	<li>new_value</li>
 	<li>deleted (boolean)</li>
 	<li>timestamp</li>
</ul>
Major cons: Will I be able to recreate the records (rollback) if needed easily? The new_value column needs to be a huge string so it can support all different column types.

&nbsp;

https://www.quora.com/What-is-the-best-design-for-an-audit-history-table

There are three approaches, but I am not sure which one should be followed,
<ol>
 	<li>A single table with the fields id | table | column | row | old_value | new_value | timestamp | userid. This would track all changes to all tables in a single place and has the benefit of minimizing the number of tables. It does make querying a little difficult, but not impossible.</li>
 	<li>Multiple tables like #1 except without the table column. This would separate the changes from each table into their own history table.</li>
 	<li>Multiple tables that mirror the schema of the original tables to track. This would make the triggers a lot easier to write, would make restoration of the data easier if someone wanted to revert to a specific record, but would come at the expense of storage, as every field, even if it hadn't changed, would be duplicated, possibly multiple times. Also, it would make it difficult to know specifically which fields changed from one version to the next.</li>
</ol>
Option #3 is almost always the best one, at least for traditional structured databases. There are a number of reasons as to why:

- Option #1 and #2 may not duplicate the entire row but they have considerable storage overhead that may exceed just duplicating the row. Remember, you are duplicating row headers, metadata (table, column, etc) for each value that changes in a single updated row. For many data models, you will not save much space this way and storage for things like audit tables is inexpensive because it is rarely accessed except to append.

- If columns in a table have different data types, how are you storing all the values in the same table? You could do something like translating them text but that will be efficient for neither storage nor query.

- Option #1 and #2 are more flexible in terms of schema changes but for #3 many databases will allow schema changes to be applied transactionally to both the main table and the shadow audit table simultaneously. However, you need to decide what should happen to the audit table if, for example, you drop a column in the main table.

- In a number of databases (e.g. PostgreSQL), there are fast, general ways to copy a row to a shadow table with common data models. This is how auditing is often implemented in practice. #3 can be even faster than it appears.

However, the most important reason is what you mention above:

- Option #3 makes it very easy to query or rollback the history because it has the same data model as the original table. You can do simple SQL queries on the union of the live table and the audit table. Queries like "show me all the changes applied to this record over the last month" are simple and efficient to both write and execute. No row reconstruction from individual value changes is necessary. If you ever need to use the audit table, you will appreciate this.

Note that the above assumes a traditional SQL-like database with a well-defined schema. If the database is more document-oriented (e.g. Mongo) then a mechanism like the Option #2 makes more sense.
<h3>"Insert Only Databases" Pattern</h3>
<ul>
 	<li>The basic idea is that you never update or delete data.</li>
 	<li>Each table has 2 datetime columns <strong>from</strong> and <strong>to</strong>.</li>
 	<li>They start with the value null in each (beginning of time to end of time)</li>
 	<li>When you need to "change" the row you add a new row, at the same time you update the <strong>to</strong> in the previous row to Now and the <strong>from</strong> in the row you are adding to Now.</li>
 	<li>You read data out of the table via a view that has a where to = null in it.</li>
 	<li>This method also gives you a picture of the state of your database at any point in time</li>
 	<li>The sequence would be given by the primary key of the table, which would be an autoincrement number.</li>
</ul>
&nbsp;

https://stackoverflow.com/questions/201527/best-design-for-a-changelog-auditing-database-table
<ol>
 	<li>Do not use triggers to audit whole database. They reduce performance significantly and do not store query itself. Triggers may be useful, if audit is required for several small tables.</li>
 	<li>would work only for tables that had surrogate keys. Or add upto 4 key columns (from apexSQL design)</li>
 	<li>Put your audit table in another database. Ideally you want separation from the original data. If you need to restore your database, you don't really want to restore the audit trail.</li>
 	<li>Denormalize as much as reasonably possible. You want the table to have as few dependencies as possible to the original data. The audit table should simple and lightning fast to retrieve data from. No fancy joins or lookups across other tables to get to the data.</li>
 	<li>While you are designing, you should write the code to recover data. When you need to recover, it is usually in a hurry, best to already be prepared.</li>
 	<li>This turned out to be too complex so we ended up reverse engineering trigger based third party tool <a href="http://www.apexsql.com/sql_tools_audit.aspx" rel="noreferrer">ApexSQL Audit</a> to create our own custom solution.Tips:-Include before/after values-Include 3,4 columns for storing primary key (in case it’s a composite key)-Store data outside main database as already suggested by Robert-Spend decent amount of time on preparing reports – especially those you might need for recovery-Plan for storing host/application name – this might come very useful for tracking suspicious activities</li>
</ol>
&nbsp;

https://stackoverflow.com/questions/1798156/how-to-keep-an-audit-history-of-changes-to-the-table

There are two common ways of creating audit trails.
<ol>
 	<li>Code your data access layer.</li>
 	<li>In the database itself using triggers.</li>
</ol>
There are advantages and disadvantages to both. Some people prefer one over the other. It's often down to the type of app and the type of database use you can expect.

If you do it in your DA layer it's pretty much up to you. You just need to add code to every method that saves to the database to also save a log of the changes. This auditing code could be in your DA layer code, or even in your stored procs in your database if you are using stored procs for everything. Essentially the premise is the same, any time you make a change to the database, log that change.

If you want to go down the triggers route, you can write custom triggers for each table, or fashion a more generic trigger that works the same on lots of tables. Check out <a href="http://weblogs.asp.net/jgalloway/archive/2008/01/27/adding-simple-trigger-based-auditing-to-your-sql-server-database.aspx" rel="noreferrer">this article</a> on audit triggers. This works by firing of triggers whenever a change is made, and the triggers log the changes. Remember that if you want to audit SELECT statements, you can't use triggers, you'll have to do that with in code/stored proc auditing. It's also worth remember that depending on your database, triggers may not fire in all circumstances. For example, most databases don't fire triggers during TRUNCATE statements. Check that your triggers get fired in any case that you need auditing.

Alternately, you could also take a look at using the <a href="http://www.sqlteam.com/article/centralized-asynchronous-auditing-with-service-broker" rel="noreferrer">service broker</a> to do async auditing on a dedicated machine. This is more complex and takes a bit of configuring to set up.

Which ever way you do it you need to decide on the format the audit log will take. Normally you would save this log in your database, but you could just save it in a log file or whatever suits your requirements. You could use a single audit table that logs all changes, or you could have an audit table per main table being audited. For large scale implementations you could even consider putting the audit tables in a totally separate database. If your logging into a table, it's common to have a "change type" field which indicates if the audited change was an insert, update or delete style of change, along with the changed data, user who made the change and the date/time the change was made. Don't forget to include the old and new data for update style changes.

&nbsp;

References
<ul>
 	<li>https://solutioncenter.apexsql.com/sql-server-database-auditing-techniques/</li>
 	<li>https://blog.apexsql.com/apexsql-audit-vs-sql-server-change-data-capture-cdc/</li>
 	<li>https://stackoverflow.com/questions/10060408/sql-server-2008-change-data-capture-vs-triggers-in-audit-trail</li>
 	<li>https://technet.microsoft.com/en-us/library/2008.11.sql.aspx</li>
 	<li>https://stackoverflow.com/questions/2015232/database-design-for-audit-logging?noredirect=1&amp;lq=1</li>
 	<li>https://stackoverflow.com/questions/1798156/how-to-keep-an-audit-history-of-changes-to-the-table</li>
 	<li>https://stackoverflow.com/questions/201527/best-design-for-a-changelog-auditing-database-tableDBA Audit</li>
 	<li>https://www.sqlshack.com/creating-successful-auditing-strategy-sql-server-databases/</li>
 	<li><a href="http://www.4guysfromrolla.com/webtech/041807-1.shtml" target="_blank" rel="nofollow noopener">Maintaining a Log of Database Changes - Part 1</a></li>
 	<li><a href="http://www.4guysfromrolla.com/webtech/042507-1.shtml" target="_blank" rel="nofollow noopener">Maintaining a Log of Database Changes - Part 2</a></li>
</ul>
&nbsp;
