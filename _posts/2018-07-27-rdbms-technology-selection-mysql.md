---
layout: post
title: RDBMS - Technology selection MySQL
date: 2018-07-27 20:14
author: tmasabari
comments: true
categories: [Uncategorized]
---
<h1>DB-Engines Ranking</h1>
The DB-Engines Ranking ranks database management systems according to their popularity. The ranking is updated monthly.

Read more about the <a href="https://db-engines.com/en/ranking_definition">method</a> of calculating the scores.
<table class="dbi">
<tbody>
<tr>
<td class="dbi_header" colspan="3">Rank</td>
<th class="dbi_header pad-l" rowspan="2">DBMS</th>
<th class="dbi_header pad-r" rowspan="2">Database Model</th>
<td class="dbi_header" colspan="3">Score</td>
</tr>
<tr>
<td class="dbi_header small">Jul
2018</td>
<td class="dbi_header small">Jun
2018</td>
<td class="dbi_header small pad-r">Jul
2017</td>
<td class="dbi_header small pad-l">Jul
2018</td>
<td class="dbi_header small">Jun
2018</td>
<td class="dbi_header small">Jul
2017</td>
</tr>
<tr>
<td>1.</td>
<td class="small">1.</td>
<td class="small pad-r">1.</td>
<th class="pad-l"><a href="https://db-engines.com/en/system/Oracle">Oracle <span class="info"><img src="https://db-engines.com/moreattributes.png" alt="detailed information" /></span></a></th>
<th class="small pad-r"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a></th>
<td class="pad-l">1277.79</td>
<td class="small minus">-33.47</td>
<td class="small minus">-97.09</td>
</tr>
<tr>
<td>2.</td>
<td class="small">2.</td>
<td class="small pad-r">2.</td>
<th class="pad-l"><a href="https://db-engines.com/en/system/MySQL">MySQL <span class="info"><img src="https://db-engines.com/moreattributes.png" alt="detailed information" /></span></a></th>
<th class="small pad-r"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a></th>
<td class="pad-l">1196.07</td>
<td class="small minus">-37.62</td>
<td class="small minus">-153.04</td>
</tr>
<tr>
<td>3.</td>
<td class="small">3.</td>
<td class="small pad-r">3.</td>
<th class="pad-l"><a href="https://db-engines.com/en/system/Microsoft+SQL+Server">Microsoft SQL Server <span class="info"><img src="https://db-engines.com/moreattributes.png" alt="detailed information" /></span></a></th>
<th class="small pad-r"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a></th>
<td class="pad-l">1053.41</td>
<td class="small minus">-34.32</td>
<td class="small minus">-172.59

&nbsp;</td>
</tr>
</tbody>
</table>
<h3>Features</h3>
<p dir="ltr">Oracle and SQL Server are considered tools that favor users with large enterprise systems, while MySQL is considered a tool that appeals most often to individuals interested in managing databases associated with their websites.</p>
<p dir="ltr">MySQL</p>
<p dir="ltr">The original version was developed in the mid 1990s. The most notable changes to MySQL was in 2010, the time of the last acquisition in 2010. The enhancements to this release (GA release 5.5) included semisynchronous replication, custom partitioning, improved support for SMP and updates to the InnoDB I/O subsystem. If you are just learning about MySQL, you may be interested in learning more details about it.</p>
https://medium.com/@mindfiresolutions.usa/a-comparison-between-mysql-vs-ms-sql-server-58b537e474be
<p id="9208" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Platform and Programming Languages</strong></p>
The enterprises can run MySQL smoothly on several popular operating systems including Windows, Linux and Mac OS X.

Microsoft recently announced its decision to make the RDBMS available on both Linux, and Mac OS X (via Docker).But they will lack the option to avail certain features while running SQL Server on Linux or Mac OS X

Both RDBMS support Java, PHP, C++, Python, Ruby, Visual Basic, Delphi, Go and R. But MySQL additionally supports programming languages like Perl, Scheme, Tcl, Haskel and Eiffel. The support for many programming languages makes MySQL popular among varying developer communities.
<p class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Editions</strong></p>
<p id="e1eb" class="graf graf--p graf-after--p">The users can choose from two distinct versions of MySQL. They can use either MySQL Community Sever or MySQL Enterprise Server. The community edition of MySQL is open source and free, whereas the enterprise edition comes with a number of proprietary extensions. On the other hand, MS SQL Server is available in several mainstream and specialized editions.</p>
<p id="8a73" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Security</strong></p>
<p id="3bf7" class="graf graf--p graf-after--p">Both enterprise database systems are designed as binary collections. MySQL enables developers to manipulate database files through binaries while running. It even allows the database files to be accessed and manipulated by other processes at runtime. But SQL Server does not allow any process to access or manipulate its database files or binaries. It requires users to perform specific functions or manipulate files by running an instance. Hence, the hackers lack the option to access or manipulate data directly. The design rule makes MS SQL Server more secure than MySQL.</p>
<p id="036f" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Backup</strong></p>
<p id="a18c" class="graf graf--p graf-after--p">While using MySQL, developers have to backup data by extracting all data as SQL statements. The tool provided by the RDBMS further blocks the database while backing up data. The feature reduces chances of data corruption while switching from one version or edition of MySQL to another. But the feature makes the data restoration process time-consuming due to execution of multiple SQL statements. Unlike MySQL, SQL Server does not block the database while backing up data. The feature enables users to backup and restore huge amount of data without putting extra time and effort.</p>
<p id="cc8a" class="graf graf--p graf-after--p"><strong class="markup--strong markup--p-strong">Option to Stop Query Execution</strong></p>
<p id="26b6" class="graf graf--p graf-after--p">MySQL does not allow users to kill or cancel a query when it is running. The users have to kill the entire process to stop SQL query execution. But <a class="markup--anchor markup--p-anchor" href="http://www.mindfiresolutions.com/sql-server-development.htm" target="_blank" rel="nofollow noopener" data-href="http://www.mindfiresolutions.com/sql-server-development.htm">SQL Server programmers</a> can truncate a database query during execution without killing the entire process. Also, it uses a transactional engine to keep the state consistent. The feature makes SQL Server score over MySQL.</p>
&nbsp;

<strong>Performance</strong>

<strong>Case study - 1
</strong>

Vzweb, is mission-critical, 24x7 employee portal of Verizon. https://blogs.oracle.com/mysql/verizon-wireless-supports-its-mission-critical-employee-portal-with-mysql

“MySQL is the key component of Verizon Wireless’ mission-critical employee portal application,” said Shivinder Singh, senior DBA at Verizon Wireless. “We achieved 1400% performance improvement by moving from the MyISAM storage engine to InnoDB, upgrading to the latest GA release MySQL 5.5,
and using the MySQL Thread Pool to support high concurrent user connections.
MySQL has become part of our IT infrastructure, on which potentially more future applications will be built.”

<strong>Case study - 2
</strong>

'BBC News Live Stats' https://www.mysql.com/why-mysql/case-studies/bbc-news-website-uses-mysql-to-monitor-reader-interest/

Number of tables in MySQL database:24, excluding merge tables
Number of records in Largest Table:up to 4 million
Size of database: around 8 million rows
Number of transactions:around 30,000 inserts/minute, 4000 selects/hour

&nbsp;

Cost

comparison <a href="https://www.mysql.com/tcosavings/customize/?hash=&amp;controller_url=%2Ftcosavings&amp;server_count=1&amp;cpu_count=1&amp;core_count=8&amp;editions%5B1%5D=3&amp;editions%5B2%5D=18&amp;editions%5B3%5D=9&amp;years=5" target="_blank" rel="nofollow noopener">link</a>

Core-based licensing
Under the Per Core licensing model, each server running SQL Server 2017 software or any of its components (such as Reporting Services or Integration Services) must be assigned an appropriate number of SQL Server 2017 core licenses. The number of core licenses needed, depends on whether customers are licensing the physical server or individual virtual operating system environments (OSEs).

Unlike the Server+CAL licensing model, the Per Core model allows access for an unlimited number of users or devices to connect from either inside or outside an organization’s firewall. With the Per Core model, customers do not need to purchase additional client access licenses (CALs) to access the SQL Server software.

<a href="http://msdn.microsoft.com/en-us/library/ms143760%28v=sql.105%29.aspx">http://msdn.microsoft.com/en-us/library/ms143760(v=sql.105).aspx</a>

&nbsp;

&nbsp;
<table class="tools">
<tbody>
<tr>
<td class="headline" colspan="99">Editorial information provided by DB-Engines</td>
</tr>
<tr>
<td class="attribute">Name</td>
<td class="header">Microsoft SQL Server  <span class="exclude"><a href="https://db-engines.com/en/system/MySQL%3BOracle">X</a></span></td>
<td class="header">MySQL  <span class="exclude"><a href="https://db-engines.com/en/system/Microsoft+SQL+Server%3BOracle">X</a></span></td>
<td class="header">Oracle  <span class="exclude"><a href="https://db-engines.com/en/system/Microsoft+SQL+Server%3BMySQL">X</a></span></td>
</tr>
<tr>
<td class="attribute">Description</td>
<td class="value">Microsofts relational DBMS</td>
<td class="value">Widely used open source <a href="https://db-engines.com/en/article/RDBMS">RDBMS</a></td>
<td class="value">Widely used <a href="https://db-engines.com/en/article/RDBMS">RDBMS</a></td>
</tr>
<tr>
<td class="attribute">Primary database model</td>
<td class="value"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a></td>
<td class="value"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a> <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value"><a href="https://db-engines.com/en/article/RDBMS">Relational DBMS</a></td>
</tr>
<tr>
<td class="attribute">Secondary database models</td>
<td class="value"><a href="https://db-engines.com/en/article/Document+Stores">Document store</a>
<a href="https://db-engines.com/en/article/Graph+DBMS">Graph DBMS</a>
<a href="https://db-engines.com/en/article/Key-value+Stores">Key-value store</a></td>
<td class="value"><a href="https://db-engines.com/en/article/Document+Stores">Document store</a>
<a href="https://db-engines.com/en/article/Key-value+Stores">Key-value store</a></td>
<td class="value"><a href="https://db-engines.com/en/article/Document+Stores">Document store</a>
<a href="https://db-engines.com/en/article/Graph+DBMS">Graph DBMS</a> <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span>
<a href="https://db-engines.com/en/article/Key-value+Stores">Key-value store</a>
<a href="https://db-engines.com/en/article/RDF+Stores">RDF store</a> <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">
<table>
<tbody>
<tr>
<td><a href="https://db-engines.com/en/ranking">DB-Engines Ranking</a> <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td rowspan="2"><a href="https://db-engines.com/en/ranking_trend/system/Microsoft+SQL+Server%3BMySQL%3BOracle"><img src="https://db-engines.com/ranking_trend_s.png" alt="ranking trend" /></a></td>
</tr>
<tr>
<td><a href="https://db-engines.com/en/ranking_trend/system/Microsoft+SQL+Server%3BMySQL%3BOracle">Trend Chart</a></td>
</tr>
</tbody>
</table>
</td>
<td class="value">
<table class="dbi_mini">
<tbody>
<tr>
<th class="dbi_mini">Score</th>
<td class="dbi_mini" colspan="2">1053.41</td>
</tr>
<tr>
<th class="dbi_mini">Rank</th>
<td class="dbi_mini">#3</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking">Overall</a></th>
</tr>
<tr>
<th class="dbi_mini"></th>
<td class="dbi_mini">#3</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking/relational+dbms">Relational DBMS</a></th>
</tr>
</tbody>
</table>
</td>
<td class="value">
<table class="dbi_mini">
<tbody>
<tr>
<th class="dbi_mini">Score</th>
<td class="dbi_mini" colspan="2">1196.07</td>
</tr>
<tr>
<th class="dbi_mini">Rank</th>
<td class="dbi_mini">#2</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking">Overall</a></th>
</tr>
<tr>
<th class="dbi_mini"></th>
<td class="dbi_mini">#2</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking/relational+dbms">Relational DBMS</a></th>
</tr>
</tbody>
</table>
</td>
<td class="value">
<table class="dbi_mini">
<tbody>
<tr>
<th class="dbi_mini">Score</th>
<td class="dbi_mini" colspan="2">1277.79</td>
</tr>
<tr>
<th class="dbi_mini">Rank</th>
<td class="dbi_mini">#1</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking">Overall</a></th>
</tr>
<tr>
<th class="dbi_mini"></th>
<td class="dbi_mini">#1</td>
<th class="dbi_mini">  <a href="https://db-engines.com/en/ranking/relational+dbms">Relational DBMS</a></th>
</tr>
</tbody>
</table>
</td>
</tr>
<tr>
<td class="attribute">Website</td>
<td class="value"><a href="https://www.microsoft.com/en-us/sql-server/" rel="nofollow">www.microsoft.com/­en-us/­sql-server</a></td>
<td class="value"><a href="https://www.mysql.com/" rel="nofollow">www.mysql.com</a></td>
<td class="value"><a href="https://www.oracle.com/database/index.html" rel="nofollow">www.oracle.com/­database/­index.html</a></td>
</tr>
<tr>
<td class="attribute">Technical documentation</td>
<td class="value"><a href="https://docs.microsoft.com/en-ie/sql/sql-server/sql-server-technical-documentation" rel="nofollow">docs.microsoft.com/­en-ie/­sql/­sql-server/­sql-server-technical-documentation</a></td>
<td class="value"><a href="https://dev.mysql.com/doc/" rel="nofollow">dev.mysql.com/­doc</a></td>
<td class="value"><a href="https://docs.oracle.com/en/database/" rel="nofollow">docs.oracle.com/­en/­database</a></td>
</tr>
<tr>
<td class="attribute">Developer</td>
<td class="value">Microsoft</td>
<td class="value">Oracle <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">Oracle</td>
</tr>
<tr>
<td class="attribute">Initial release</td>
<td class="value">1989</td>
<td class="value">1995</td>
<td class="value">1980</td>
</tr>
<tr>
<td class="attribute">Current release</td>
<td class="value">SQL Server 2017, October 2017</td>
<td class="value">8.0.11, April 2018</td>
<td class="value">18 (18.1), February 2018</td>
</tr>
<tr>
<td class="attribute">License <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">commercial <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">Open Source <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">commercial <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Cloud-based <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">no</td>
<td class="value">no</td>
<td class="value">no</td>
</tr>
<tr>
<td class="attribute">DBaaS offerings <span>(sponsored links)</span> <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value"></td>
<td class="value"><a href="https://cloud.google.com/sql/" rel="nofollow">Google Cloud SQL</a>: A fully-managed database service for the Google Cloud Platform</td>
<td class="value"></td>
</tr>
<tr>
<td class="attribute">Implementation language</td>
<td class="value">C++</td>
<td class="value">C and C++</td>
<td class="value">C and C++</td>
</tr>
<tr>
<td class="attribute">Server operating systems</td>
<td class="value">Linux
Windows</td>
<td class="value">FreeBSD
Linux
OS X
Solaris
Windows</td>
<td class="value">AIX
HP-UX
Linux
OS X
Solaris
Windows
z/OS</td>
</tr>
<tr>
<td class="attribute">Data scheme</td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Typing <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">XML support <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">Secondary indexes</td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">SQL <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">APIs and other access methods</td>
<td class="value">OLE DB
Tabular Data Stream (TDS)
ADO.NET
JDBC
ODBC</td>
<td class="value">Proprietary native API
ADO.NET
JDBC
ODBC</td>
<td class="value">ODP.NET
Oracle Call Interface (OCI)
JDBC
ODBC</td>
</tr>
<tr>
<td class="attribute">Supported programming languages</td>
<td class="value">C#
C++
Delphi
Go
Java
JavaScript (Node.js)
PHP
Python
R
Ruby
Visual Basic</td>
<td class="value">Ada
C
C#
C++
D
Delphi
Eiffel
Erlang
Haskell
Java
JavaScript (Node.js)
Objective-C
OCaml
Perl
PHP
Python
Ruby
Scheme
Tcl</td>
<td class="value">C
C#
C++
Clojure
Cobol
Delphi
Eiffel
Erlang
Fortran
Groovy
Haskell
Java
JavaScript
Lisp
Objective C
OCaml
Perl
PHP
Python
R
Ruby
Scala
Tcl
Visual Basic</td>
</tr>
<tr>
<td class="attribute">Server-side scripts <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">Transact SQL and .NET languages</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">PL/SQL <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Triggers</td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">Partitioning methods <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">tables can be distributed across several files (horizontal partitioning); sharding through federation</td>
<td class="value">horizontal partitioning, sharding with MySQL Cluster or MySQL Fabric</td>
<td class="value">horizontal partitioning <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Replication methods <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes, but depending on the SQL-Server Edition</td>
<td class="value">Master-master replication
Master-slave replication</td>
<td class="value">Master-master replication
Master-slave replication</td>
</tr>
<tr>
<td class="attribute">MapReduce <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">no</td>
<td class="value">no</td>
<td class="value">no <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Consistency concepts <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">Immediate Consistency</td>
<td class="value">Immediate Consistency</td>
<td class="value">Immediate Consistency</td>
</tr>
<tr>
<td class="attribute">Foreign keys <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">Transaction concepts <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">ACID</td>
<td class="value">ACID <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">ACID <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">Concurrency <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">Durability <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes</td>
</tr>
<tr>
<td class="attribute">In-memory capabilities <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">yes</td>
<td class="value">yes</td>
<td class="value">yes <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
</tr>
<tr>
<td class="attribute">User concepts <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">fine grained access rights according to SQL-standard</td>
<td class="value">Users with fine-grained authorization concept <span class="info"><img src="https://db-engines.com/info.png" alt="info" /></span></td>
<td class="value">fine grained access rights according to SQL-standard</td>
</tr>
<tr>
<td class="headline" colspan="99">More information provided by the system vendor</td>
</tr>
<tr>
<td></td>
<td class="header">Microsoft SQL Server</td>
<td class="header">MySQL</td>
<td class="header">Oracle</td>
</tr>
<tr>
<td class="attribute external_att">Specific characteristics</td>
<td class="value external_val"></td>
<td class="value external_val"></td>
<td class="value external_val">Oracle Database (commonly referred to as Oracle RDBMS or simply as Oracle) is a multi-model...
<a href="https://db-engines.com/en/system/Oracle#a32">» more</a></td>
</tr>
<tr>
<td class="attribute external_att">Licensing and pricing models</td>
<td class="value external_val"></td>
<td class="value external_val"></td>
<td class="value external_val">Oracle Database Cloud Services Customers can choose from a wide range of database...
<a href="https://db-engines.com/en/system/Oracle#a37">» more</a></td>
</tr>
<tr>
<td class="hint" colspan="99">We invite representatives of system vendors to <a href="https://db-engines.com/en/services">contact us</a> for updating and extending the system information,
and for displaying vendor-provided information such as key customers, competitive advantages and market metrics.</td>
</tr>
</tbody>
</table>
<ul>
 	<li>Performance  comparison- https://www.ijarcce.com/upload/2015/march-15/IJARCCE%2039.pdf</li>
 	<li>https://db-engines.com/en/system/Microsoft+SQL+Server%3BMySQL%3BOracle</li>
</ul>
&nbsp;
