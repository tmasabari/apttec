---
layout: post
title: SQL DB
date: 2018-02-26 22:22
author: tmasabari
comments: true
categories: [Interview Preparation, Prepare, QuickRefresh, Uncategorized]
---
<ol>
 	<li><em>why we should use procedures and what is the usage (parameterised procedure).</em></li>
 	<li><em>Diff between functions and store procedures</em></li>
 	<li><em>why we should use transaction.
</em></li>
 	<li><em>Triggers.
</em></li>
 	<li><em>Table variable and temp table – diff</em></li>
 	<li><em>clustered and non clustered indexing.
</em></li>
 	<li><em>Normalisation and forms.</em></li>
 	<li><em>sql injection</em></li>
</ol>
&nbsp;

<a href="https://www.codeproject.com/Articles/4451/SQL-Server-Transactions-and-Error-Handling">https://www.codeproject.com/Articles/4451/SQL-Server-Transactions-and-Error-Handling</a>
Transactions group a set of tasks into a single execution unit. Each transaction begins with a specific task and ends when all the tasks in the group successfully complete. If any of the tasks fails, the transaction fails. Therefore, a transaction has only two results: success or failure. Incomplete steps result in the failure of the transaction.
Users can group two or more Transact-SQL statements into a single transaction using the following statements:
<ul>
 	<li>Begin Transaction</li>
 	<li>Rollback Transaction</li>
 	<li>Commit Transaction</li>
</ul>
Before the real processing starts, the <code>BEGIN TRAN </code>statement notifies SQL Server to treat all of the following actions as a single transaction. It is followed by two <code>UPDATE </code>statements. If no errors occur during the updates, all changes are committed to the database when SQL Server processes the <code>COMMIT TRAN </code>statement, and finally the stored procedure finishes.
SQL Server allows you to nest transactions. Basically, this feature means that a new transaction can start even though the previous one is not complete. Transact-SQL allows you to nest transaction operations by issuing nested <code>BEGIN TRAN </code>commands. The <code>@@TRANCOUNT </code>automatic variable can be queried to determine the level of nesting - 0 indicates no nesting , 1 indicates nesting one level deep, and so fourth.
Savepoints offer a mechanism to roll back portions of transactions. A user can set a savepoint, or marker, within a transaction. The savepoint defines a location to which a transaction can return if part of the transaction is conditionally canceled.
SQL Server allows you to use savepoints via the <code>SAVE TRAN </code>statement
<pre class="notranslate" lang="sql"><span class="code-keyword">SAVE</span> <span class="code-keyword">TRAN</span> sales <span class="code-comment">--</span><span class="code-comment"> Mark a save point	 	 
</span></pre>
<pre id="pre387459" class="notranslate" lang="sql"><span class="code-keyword">ROLLBACK</span> <span class="code-keyword">TRAN</span> sales</pre>
&nbsp;
<h2><a href="https://www.seguetech.com/advantages-and-drawbacks-of-using-stored-procedures-for-processing-data/">SPs </a></h2>
<strong>Security</strong>
<ul>
 	<li>Limit direct access to tables via defined roles in the database</li>
 	<li>Provide an “interface” to the underlying data structure so that all implementation and even the data itself is shielded.</li>
 	<li>Securing just the data and the code that accesses it is easier than applying that security within the application code itself</li>
</ul>
<strong>Utilization of Set-based Processing</strong>
<ul>
 	<li>The power of SQL is its ability to quickly and efficiently perform set-based processing on large amounts of data; the coding equivalent is usually iterative looping, which is generally much slower</li>
</ul>
<strong>Speed / Optimization</strong>
<ul>
 	<li>Stored procedures are cached on the server</li>
 	<li>Execution plans for the process are easily reviewable without having to run the application</li>
</ul>
<strong>Testing</strong>
<ul>
 	<li>Can be tested independent of the application. Easy to identify the issue in data access.</li>
</ul>
<ul>
 	<li><strong>Disadvantages</strong></li>
 	<li><strong>Limited Coding Functionality</strong>
<ul>
 	<li>Stored procedure code is not as robust as app code, particularly in the area of looping (not to mention that iterative constructs, like cursors, are slow and processor intensive)</li>
</ul>
</li>
 	<li><strong>Portability</strong>
<ul>
 	<li>Complex Stored Procedures that utilize complex, core functionality of the RDBMS used for their creation will not always port to upgraded versions of the same database. This is especially true if moving from one database type (Oracle) to another (MS SQL Server).</li>
</ul>
</li>
 	<li><strong>Testing</strong>
<ul>
 	<li>Any data errors in handling Stored Procedures are not generated until runtime</li>
</ul>
</li>
 	<li><strong>Location of Business Rules</strong>
<ul>
 	<li>Since SP’s are not as easily grouped/encapsulated together in single files, this also means that business rules are spread throughout different Stored Procedures. App code architecture helps to ensure that business rules are encapsulated in single objects.</li>
 	<li>There is a general opinion that business rules / logic should not be housed in the data tier</li>
</ul>
</li>
 	<li><strong>Utilization of Set-based Processing</strong>
<ul>
 	<li>Too much overhead is incurred from maintaining Stored Procedures that are not <em>complex </em>enough. As a result, the general consensus is that simple SELECT statements should <em>not </em>be bound to Stored Procedures and instead implemented as inline SQL.</li>
</ul>
</li>
</ul>
Alternatives
<ul>
 	<li><strong>In-line or Parameterized Queries</strong>
<ul>
 	<li>These are written within the application code itself</li>
</ul>
</li>
 	<li><strong>Object Relational Mapping (ORM)</strong>
<ul>
 	<li>Provides an abstraction to the database without having to manually write data access classes.</li>
</ul>
</li>
</ul>
<h2>SP Vs Function</h2>
<a href="http://www.mytecbits.com/microsoft/sql-server/function-vs-stored-procedure">http://www.mytecbits.com/microsoft/sql-server/function-vs-stored-procedure</a>
<table style="width: 763px;">
<thead>
<tr>
<td style="width: 32px;"><strong>Sl.#
</strong></td>
<td style="width: 304px;"><strong>User Defined Function (UDF)
</strong></td>
<td style="width: 385px;"><strong>Stored Procedure</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td style="width: 32px;">1</td>
<td style="width: 304px;">Function should return a value, either a scalar value or a table.</td>
<td style="width: 385px;">Stored procedure may or may not return value. It can even return multiple scalar values or tables</td>
</tr>
<tr>
<td style="width: 32px;">2</td>
<td style="width: 304px;">Function should have only input parameters.</td>
<td style="width: 385px;">Stored procedure can have both input and out parameters.</td>
</tr>
<tr>
<td style="width: 32px;">3</td>
<td style="width: 304px;">Functions should have at least one input parameter.</td>
<td style="width: 385px;">In stored procedures input parameters are optional.</td>
</tr>
<tr>
<td style="width: 32px;">4</td>
<td style="width: 304px;">A maximum of 1024 input parameters can be used in a function.</td>
<td style="width: 385px;">A maximum of 2100 parameters can be used in a stored procedure.</td>
</tr>
<tr>
<td style="width: 32px;">5</td>
<td style="width: 304px;">A function can be called from inside a stored procedure.</td>
<td style="width: 385px;">A stored procedure cannot be called from inside a function.</td>
</tr>
<tr>
<td style="width: 32px;">6</td>
<td style="width: 304px;">Functions cannot perform any permanent environmental change to the database.</td>
<td style="width: 385px;">Stored procedures can perform any permanent environmental change to the database.</td>
</tr>
<tr>
<td style="width: 32px;">7</td>
<td style="width: 304px;"><strong>Functions cannot use DML statements like INSERT, UPDATE or DELETE against any tables,</strong> temp tables or views. These statements can be used only against local table variables.</td>
<td style="width: 385px;">Stored procedures and use DML statements against permanent tables, temp tables or views.</td>
</tr>
<tr>
<td style="width: 32px;">8</td>
<td style="width: 304px;"><strong>Transaction management: Begin / Commit / Rollback Transactions cannot be used in functions.</strong></td>
<td style="width: 385px;">Transactions can be used in stored procedure.</td>
</tr>
<tr>
<td style="width: 32px;">9</td>
<td style="width: 304px;"><strong>Exception or error handling using try/catch cannot be used in a function.</strong></td>
<td style="width: 385px;">Exception or error handling is allowed to be used in stored procedure.</td>
</tr>
<tr>
<td style="width: 32px;">10</td>
<td style="width: 304px;">Function can be called from inside SELECT statement and WHERE or HAVING classes.</td>
<td style="width: 385px;">Stored procedure cannot be called from inside SELECT statement and WHERE or HAVING classes.</td>
</tr>
<tr>
<td style="width: 32px;">11</td>
<td style="width: 304px;"><strong>Table-Valued Function</strong> can be used in JOIN clause just like a table.</td>
<td style="width: 385px;">Stored procedures cannot be used in JOINs.</td>
</tr>
<tr>
<td style="width: 32px;">12</td>
<td style="width: 304px;"> On using as function in SELECT, WHERE or HAVING clause, you can pass the column as a parameter.</td>
<td style="width: 385px;"> Column cannot be passed as parameter in stored procedure.</td>
</tr>
<tr>
<td style="width: 32px;">13</td>
<td style="width: 304px;"> Functions are normally used for computing small logic and return the result.</td>
<td style="width: 385px;"> Stored procedures are normally used for highly complex business logic and either return the result or update the values in tables.</td>
</tr>
<tr>
<td style="width: 32px;">14</td>
<td style="width: 304px;"> You cannot use temporary tables in functions. Instead they can use table variables.</td>
<td style="width: 385px;"> In stored procedures you can use temp tables as well as table variables.</td>
</tr>
<tr>
<td style="width: 32px;">15</td>
<td style="width: 304px;"> Non-deterministic built-in functions like NEWID,NEWSEQUENTIALID,RAND and TEXTPTR cannot be used in user defined function.</td>
<td style="width: 385px;"> No such condition.</td>
</tr>
<tr>
<td style="width: 32px;">16</td>
<td style="width: 304px;"> Function cannot be executed using EXECUTE or EXEC command.</td>
<td style="width: 385px;"> Stored procedures can be executed using EXECUTE or EXEC command.</td>
</tr>
</tbody>
</table>
<h2>Temp Tables vs Table variables vs CTE</h2>
<a href="http://www.mytecbits.com/microsoft/sql-server/temp-table-vs-table-variable-vs-cte">http://www.mytecbits.com/microsoft/sql-server/temp-table-vs-table-variable-vs-cte</a>
<h3>1. Local Temp Table</h3>
The local temp table’s name is prefixed with single number sign (#) (Example: #TableName). These local temp tables are available only in the current session. I.e. if you create a hash table in a stored procedure, then the table will be available only for that stored procedure or any other nested stored procedures called from inside that stored procedure. <strong>Once the stored procedure finishes execution, the hash table drops automatically from the TempDB</strong>. So only SQL user/connection which created the temp table alone can use it.
<h3>2. Global Temp Table</h3>
The global temp table’s name is prefixed with double number sign (##) (Example: ##TableName). The global temp tables are available for all the sessions or the SQL Server connections. I.e. Multiple SQL Server users can use the same temp table. The table exists till the creates session and all the other sessions or connections using the global temp table closes. Once all the sessions and connections stops using the global temp table, it will automatically drops from the TempDB.

When to use ?
<ul>
 	<li>If the size of the temporary data is huge, say <strong>more than 100 rows</strong>.</li>
 	<li>If you want to use <strong>explicit transactions</strong> against the temporary data.</li>
 	<li>When you may need to <strong>create indexes.</strong></li>
 	<li>If you may need to apply <strong>read lock.</strong></li>
 	<li>You <strong>CANNOT</strong> use temp tables in User Defined Functions (UDF).</li>
</ul>
<h3>Table Variable</h3>
It has most of the features of a normal variable along with the capability of storing a result set. This stored result set can be used within a batch. This is also <strong>created in the </strong>Tempdb<strong> database but <span style="text-decoration: underline;">not</span> the memory</strong>. This also allows you to create primary key, identity at the time of Table variable declaration but not non-clustered index.

The table variable needs to be declared just like a variable. While declaring, we have to specify the column details.
<ul>
 	<li>To store temporary data in user defined<strong> functions (UDF),</strong> stored procedures and query batches. In fact it is the means of returning result set in table-valued user defined functions.</li>
 	<li>If the volume of data is less, say l<strong>ess than 100 rows</strong>. the optimizer in some cases may ignore the number of records in table variable while generating the query plan.</li>
 	<li>If you<strong> don’t want to have transactions</strong> against the temporary data.</li>
 	<li>When you <strong>don’t need to alter the table</strong> structure after creating it.</li>
</ul>
&nbsp;
<h3>CTE</h3>
CTE stands for Common Table expressions. It was introduced with SQL Server 2005. It is a temporary result set and typically it may be a result of complex sub-query. Unlike temporary table its life is limited to the current query. It is defined by using WITH statement. CTE improves readability and ease in maintenance of complex queries and sub-queries. Always begin CTE with semicolon.
<h3>1. Non-Recursive CTE</h3>
Non-recursive common table expression is the generic form of CTE. It does not have any reference to itself in the CTE definition.
<div class="ad-cnt"></div>
<h3>2. Recursive CTE</h3>
When a CTE has reference in itself, then it’s called recursive CTE.
<h2>Temp Table Vs Table Variable Vs CTE</h2>
<table>
<thead>
<tr>
<td><strong>Sl.#</strong></td>
<td><strong>Temp Table</strong></td>
<td><strong>Table Variable</strong></td>
<td><strong>CTE</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>Scope wise the local temp table is available only in the current session.The global temp tables are available for all the sessions or the SQL Server connections.</td>
<td>The scope of the table variable is just within the batch or a view or a stored procedure.</td>
<td>The scope of the CTE is limited to the statement which follows it.</td>
</tr>
<tr>
<td>2</td>
<td>Temp tables are stored in TempDB.</td>
<td>Table variables are also stored in TempDB.</td>
<td>The result set from CTE is not stored anywhere as that are like disposable views.</td>
</tr>
<tr>
<td>3</td>
<td>The name of the temp table can have only up to 116 characters.</td>
<td>The name of the table variable can have up to 128 characters.</td>
<td>Not Applicable</td>
</tr>
<tr>
<td>4</td>
<td>Considering the performance, it is recommenced to use temp table for storing huge data, say more than 100 rows.</td>
<td>Table variable is recommended for storing below 100 rows.</td>
<td>No such performance consideration. CTE normally used as a replacement for complex sub queries.</td>
</tr>
<tr>
<td>5</td>
<td>The structure of temp table can be altered after creating it.</td>
<td>The structure of table variable cannot be altered.</td>
<td>The definition of CTE cannot be changed during run time.</td>
</tr>
<tr>
<td>6</td>
<td>Can explicitly drop temp tables using DROP statement.</td>
<td>Cannot drop table variable explicitly.</td>
<td>Cannot be dropped.</td>
</tr>
<tr>
<td>7</td>
<td>Cannot be used in User Defined Function (UDF).</td>
<td>Can be used in UDF.</td>
<td>Can be used in UDF.</td>
</tr>
<tr>
<td>8</td>
<td>Temp tables take part in transactions.</td>
<td>Table variables wont take part in transactions.</td>
<td>Not Applicable</td>
</tr>
<tr>
<td>9</td>
<td>Index can be created on temp tables.</td>
<td>Index is not possible on table variables.</td>
<td>CTE cannot be indexed.</td>
</tr>
<tr>
<td>10</td>
<td>Can apply read lock on temp tables.</td>
<td>Locking is not possible in table variables.</td>
<td>Locking is not possible in CTE as well.</td>
</tr>
<tr>
<td>11</td>
<td>Constraints can be created on temp tables except FOREIGN KEY.</td>
<td>PRIMARY KEY, UNIQUE KEY and NULL are the only constraints allowed in table variable.</td>
<td>CTE cannot have constraints.</td>
</tr>
</tbody>
</table>
&nbsp;

&nbsp;

Triggers

<a href="https://www.codeproject.com/Articles/25600/Triggers-SQL-Server">https://www.codeproject.com/Articles/25600/Triggers-SQL-Server</a>

&nbsp;

There are two types of Triggers:
<ol>
 	<li>DDL Trigger</li>
 	<li>DML trigger</li>
</ol>
<strong>DDl Triggers</strong>

They fire in response to DDL (Data Definition Language) command events that start with Create, Alter and Drop. Like Create_table, Create_view, drop_table, Drop_view and Alter_table.
<ol class="dp-sql" start="1">
 	<li class="alt"><span class="keyword">create</span> <span class="keyword">trigger</span> saftey</li>
 	<li class=""><span class="keyword">on</span> <span class="keyword">database</span></li>
 	<li class="alt"><span class="keyword">for</span></li>
 	<li class="">create_table,alter_table,drop_table</li>
 	<li class="alt"><span class="keyword">as</span></li>
 	<li class="">print<span class="string">'you can not create ,drop and alter table in this database'</span></li>
 	<li class="alt"><span class="keyword">rollback</span>;</li>
</ol>
&nbsp;

Basically, triggers are classified into two main types:
<ol type="i">
 	<li>After Triggers (For Triggers)</li>
 	<li>Instead Of Triggers</li>
</ol>
<ol>
 	<li>After Triggers (For Triggers)</li>
</ol>
The <code>CREATE TRIGGER</code> statement is used to create the trigger. <code>THE ON</code> clause specifies the table name on which the trigger is to be attached. The <code>FOR INSERT</code> specifies that this is an <code>AFTER INSERT</code> trigger. In place of <code>FOR INSERT</code>, <code>AFTER INSERT</code> can be used. Both of them mean the same.

In the trigger body, table named <strong>inserted </strong>has been used. This table is a logical table and contains the row that has been inserted. I

In this trigger, the deleted record’s data is picked from the <strong>logical deleted table</strong> and inserted into the audit table.
<ol>
 	<li>Instead Of Triggers</li>
</ol>
These can be used as an interceptor for anything that anyone tried to do on our table or view. If you define an <em>Instead Of trigger</em> on a table for the Delete operation, they try to delete rows, and they will not actually get deleted (unless you issue another delete instruction from within the trigger)

INSTEAD OF TRIGGERS can be classified further into three types as:
<ol type="a">
 	<li>INSTEAD OF INSERT Trigger.</li>
 	<li>INSTEAD OF UPDATE Trigger.</li>
 	<li>INSTEAD OF DELETE Trigger.</li>
</ol>
&nbsp;

&nbsp;

Indexes

<a href="https://technet.microsoft.com/en-us/library/ms190457(v=sql.110).aspx">https://technet.microsoft.com/en-us/library/ms190457(v=sql.110).aspx</a>

A table or view can contain the following types of indexes:
<ul>
 	<li>Clustered
<ul>
 	<li>Clustered indexes sort and store the data rows in the table or view based on their key values. These are the columns included in the index definition. There can be only one clustered index per table, because the data rows themselves can be sorted in only one order.</li>
 	<li>The only time the data rows in a table are stored in sorted order is when the table contains a clustered index. When a table has a clustered index, the table is called a clustered table. If a table has no clustered index, its data rows are stored in an unordered structure called a heap.</li>
</ul>
</li>
 	<li>Nonclustered
<ul>
 	<li>Nonclustered indexes have a structure separate from the data rows. A nonclustered index contains the nonclustered index key values and each key value entry has a pointer to the data row that contains the key value.</li>
 	<li>The pointer from an index row in a nonclustered index to a data row is called a row locator. The structure of the row locator depends on whether the data pages are stored in a heap or a clustered table. For a heap, a row locator is a pointer to the row. For a clustered table, the row locator is the clustered index key.</li>
 	<li>You can add nonkey columns to the leaf level of the nonclustered index to by-pass existing index key limits, 900 bytes and 16 key columns, and execute fully covered, indexed, queries. For more information, see <a href="https://technet.microsoft.com/en-us/library/ms190806(v=sql.110).aspx">Create Indexes with Included Columns</a>.</li>
</ul>
</li>
</ul>
&nbsp;

When performing a table scan, the query optimizer reads all the rows in the table, and extracts the rows that meet the criteria of the query. A table scan generates many disk I/O operations and can be resource intensive. However, a table scan could be the most efficient method if, for example, the result set of the query is a high percentage of rows from the table.

When the query optimizer uses an index, it searches the index key columns, finds the storage location of the rows needed by the query and extracts the matching rows from that location. Generally, searching the index is much faster than searching the table because unlike a table, an index frequently contains very few columns per row and the rows are in sorted order.

The query optimizer typically selects the most efficient method when executing queries. However, if no indexes are available, the query optimizer must use a table scan.

<a href="https://msdn.microsoft.com/en-us/library/cc505842.aspx">https://msdn.microsoft.com/en-us/library/cc505842.aspx</a>

<a href="https://www.guru99.com/database-normalization.html">https://www.guru99.com/database-normalization.html</a>
<h2>What is Normalization?</h2>
Normalization is a database design technique which organizes tables in a manner that reduces redundancy and dependency of data.

There are three main reasons to normalize a database.  The first is to minimize duplicate data, the second is to minimize or avoid data modification issues, and the third is to simplify queries.

It divides larger tables to smaller tables and links them using relationships.

Theory of Data Normalization in SQL is still being developed further. For example, there are discussions even on 6<sup>th</sup> Normal Form. <strong>However, in most practical applications, normalization achieves its best in 3<sup>rd</sup> Normal Form</strong>. The evolution of Normalization theories is illustrated below-
<p id="lTmIEzI"><img class="alignnone size-full wp-image-436 " src="/wp-content/uploads/2017/12/img_5a293783d99ce.png" alt="" /></p>

<ul>
 	<li><a title="Get Ready to Learn SQL: 9. Database First Normal Form Explained in Simple English" href="http://www.essentialsql.com/get-ready-to-learn-sql-8-database-first-normal-form-explained-in-simple-english/"><strong>First Normal Form</strong></a> – The information is stored in a relational table and each column contains atomic values, and there are not repeating groups of columns.</li>
 	<li><a title="Get Ready to Learn SQL: 10. Database Second Normal Form Explained in Simple English" href="http://www.essentialsql.com/get-ready-to-learn-sql-10-database-second-normal-form-explained-in-simple-english/"><strong>Second Normal Form</strong></a> – The table is in first normal form and all the columns depend on the table’s primary key.</li>
 	<li><a title="Get Ready to Learn SQL: 11. Database Third Normal Form Explained in Simple English" href="http://www.essentialsql.com/get-ready-to-learn-sql-11-database-third-normal-form-explained-in-simple-english/"><strong>Third Normal Form</strong></a> – the table is in second normal form and all of its columns are not transitively dependent on the primary key</li>
</ul>
<h2><strong>1NF (First Normal Form) Rules</strong></h2>
<ul>
 	<li><strong>Values are atomic. </strong>The columns in a relational table are not a repeating group or arrays.</li>
 	<li><strong>Columns are of the same kind. </strong>All values in a column come from the same domain.</li>
 	<li><strong>Rows are unique. </strong>There is at least one column or set of columns, the values of which uniquely identify each row in the table.</li>
 	<li><strong>The order of columns is insignificant. </strong>You can share the same table without worrying about table organization.</li>
 	<li><strong>The sequence of rows is insignificant. </strong>A relational table can be retrieved in a different order and sequence.</li>
 	<li><strong>Each column must have a unique name. </strong>This is required because the order of columns is not significant.</li>
</ul>
<h2>What is a KEY?</h2>
A KEY is a value used to identify a record in a table uniquely. A KEY could be a single column or combination of multiple columns

Note: Columns in a table that are NOT used to identify a record uniquely are called non-key columns.
<h2>What is Composite Key?</h2>
A composite key is a primary key composed of multiple columns used to identify a record uniquely
<h2>Foreign Key</h2>
Foreign Key references the primary key of another Table! It helps connect your Tables
<ul>
 	<li>A foreign key can have a different name from its primary key</li>
 	<li>It ensures rows in one table have corresponding rows in another</li>
 	<li>Unlike the Primary key, they do not have to be unique. Most often they aren't</li>
 	<li>Foreign keys can be null even though primary keys can not</li>
</ul>
<h2>2NF (Second Normal Form) Rules</h2>
<ul>
 	<li>Rule 1- Be in 1NF</li>
 	<li>every non-key column must be fully functionally dependent on the entire primary key. This means that no column can depend on part of the primary key only.</li>
</ul>
After decomposing to multiple tables, you must have some common value that enables you to join the tables in queries; otherwise, you would lose some information. The decomposition has to be lossless. Of course, you need relationships between tables. A relationship is an association between two or more tables. Relationships are expressed in the data values of the primary and foreign keys. A primary key is a column or columns in a table whose values uniquely identify each row in the table. A foreign key is a column or columns whose values are the same as the primary key of another table—in other words, a copy of the primary key from another relational table. The relationship is made between two relational tables by matching the values of the foreign key with the values of the primary key.
<h2>What are transitive functional dependencies?</h2>
A transitive functional dependency is when changing a non-key column, might cause any of the other non-key columns to change
<h2>3NF (Third Normal Form) Rules</h2>
<ul>
 	<li>Rule 1- Be in 2NF</li>
 	<li>Rule 2- Has no transitive functional dependencies</li>
</ul>
