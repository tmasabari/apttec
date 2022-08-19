---
layout: post
title: Sql Server Version control & Tools
date: 2018-06-28 15:57
author: tmasabari
comments: true
categories: [Data Model, Design]
---
<h2 class="grid--cell fs-headline1 fl1"><a class="question-hyperlink" href="https://stackoverflow.com/questions/173/versioning-sql-server-database">Versioning SQL Server database</a></h2>
The database is a critical part of your application. If you deploy version 2.0 of your application against version 1.0 of your database, what do you get? A broken application. And that's why <b>your database should always be under source control right next to your application code</b>. You deploy the app, and you deploy the database. Like peanut butter and chocolate, they are two great tastes that taste great together.
<h2>Agile / Evolutionary DB design</h2>
https://martinfowler.com/articles/evodb.html
<h3>Database Upgrade Scripts</h3>
A sequence database upgrade scripts that contain the DDL necessary to move the schema from version N to N+1. (These go in your version control system.)
<h3>Developer Sandbox Synchronization</h3>
<ol>
 	<li>A script to backup, sanitize, and shrink a production database. Run this after each upgrade to the production DB.</li>
 	<li>A script to restore (and tweak, if necessary) the backup on a developer's workstation. Each developer runs this script after each upgrade to the production DB.</li>
</ol>
&nbsp;
<p id="XTqFILA"><img class="alignnone size-full wp-image-1594 " src="/wp-content/uploads/2018/07/img_5b39cd745b53b.png" alt="" /></p>
<p id="hmHllMb"><img class="alignnone size-full wp-image-1592 " src="/wp-content/uploads/2018/07/img_5b39cd1d39d9b.png" alt="" /></p>
&nbsp;
<h3>A database consists of schema and data</h3>
When we talk about a database here, we mean not just the schema of the database and database code, but also a fair amount of data. This data consists of common standing data for the application, such as the inevitable list of all the states, countries, currencies, address types and various application specific data. We may also include some sample test data such as a few sample customers, orders etc. This sample data would not make it to production, unless specifically needed for sanity testing or semantic monitoring.

This data is there for a number of reasons. The main reason is to enable testing. We are great believers in using a large body of automated tests to help stabilize the development of an application. Such a body of tests is a common approach in agile methods. For these tests to work efficiently, it makes sense to work on a database that is seeded with some sample test data, which all tests can assume is in place before they run.

This sample data needs to be version controlled, so we know where to look for it when we need to populate a new database, and so we have a record of changes that's synchronized with the tests and application code.

&nbsp;
<h2>Tools</h2>
Microsoft's new <a href="http://msdn2.microsoft.com/en-us/teamsystem/aa718807.aspx">Team Edition for Database Professionals</a>. <a href="https://stackoverflow.com/questions/14701635/is-there-a-recent-version-of-visual-studio-team-edition-for-database-professiona" target="_blank" rel="nofollow noopener">In Visual Studio 2012</a>, <a href="http://msdn.microsoft.com/en-US/data/hh297027" rel="noreferrer">SQL Server Data Tools</a> replaced and provided conversion capability for existing Visual Studio database projects.

It goes far beyond mere reverse engineering of the database into files. You get an industrial-strength database project that you can add to your solution, along with a few other goodies:
<ul>
 	<li><b>Create test data.</b> A blank database schema isn't particularly useful to develop against. Now you can distribute your database schema along with one-click synthetic data generation plans. With flexible synthetic data generators, you can avoid dumping production data to developers, or, God forbid, letting developers fend for themselves by creating their own test data. And you can generate 1,000 rows or 100,000 rows. I wish I had a dollar every time an application I've worked on began to have performance problems because none of the developers had the foresight to test the app with more than a few rows of crappy, manually entered test data. Data generation is a <i>huge</i> increase in development quality.</li>
 	<li><b>Schema comparison</b>. If we can compare two files in source control, why can't we compare two tables? A robust schema comparison tool is essential. Not sure why staging is different than production? Run a quick schema compare on 'em. Did I mention it also creates a real-time update script every time you do a comparison.. which it can execute with one additional click?</li>
 	<li><b>Data comparison</b>. If your testers are complaining because they entered test data that causes your application to crash, run the data compare tool to determine exactly how their data differs from yours.</li>
 	<li><b>Database unit testing</b>. If you make a change to the database schema, how do you know if you've broken any applications that rely on that database? You know because you've written unit tests that validate the database. Right? <i>Right?</i></li>
 	<li><b>Refactoring</b>. You can rename entities in the database (columns, tables, procs, etc) and have the rename automatically cascade throughout the database.</li>
 	<li><b>Integrated T-SQL editor</b>. T-SQL is now a first class language construct in the IDE, just like C# and VB.NET. Run queries and view execution plans and stats, all without leaving the cozy confines of good old Visual Studio.</li>
</ul>
&nbsp;

<a href="https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017" target="_blank" rel="nofollow noopener"><strong>SQL Server Data Tools</strong></a> is a modern development tool for building SQL Server relational databases, Azure SQL databases, Analysis Services (AS) data models, Integration Services (IS) packages, and Reporting Services (RS) reports. With SSDT, you can design and deploy any SQL Server content type with the same ease as you would develop an application in Visual Studio.
<p class=""><em>For most users, SQL Server Data Tools (SSDT) is installed during Visual Studio installation. Installing SSDT using the Visual Studio installer adds the base SSDT functionality, so you still need to run the <a href="https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017#ssdt-for-vs-2017-standalone-installer" data-linktype="self-bookmark">SSDT standalone installer</a> to get AS, IS, and RS tools.</em></p>
Supported versions

SQL Server 2005* - SQL Server 2017
(use SSDT 17.x or SSDT for Visual Studio 2017 to connect to <a href="https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview?view=sql-server-2017" data-linktype="relative-path">SQL Server on Linux</a>)

Azure SQL Database

Azure SQL Data Warehouse (supports queries only; database projects are not yet supported)

* SQL Server 2005 support is deprecated
<h2>OpenDBDiff</h2>
Open DBDiff can synchronize
<ul>
 	<li>Tables (including Table Options like vardecimal, text in row, etc.)</li>
 	<li>Columns (including Computed Columns, XML options, Identities, etc.)</li>
 	<li>Constraints</li>
 	<li>Indexes (and XML Indexes)</li>
 	<li>XML Schemas</li>
 	<li>Table Types</li>
 	<li>User Data Types (UDT)</li>
 	<li>CLR Objects (Assemblies, CLR-UDT, CLR-Store Procedure, CLR-Triggers)</li>
 	<li>Triggers (including DDL Triggers)</li>
 	<li>Synonyms</li>
 	<li>Schemas</li>
 	<li>File groups</li>
 	<li>Views</li>
 	<li>Functions</li>
 	<li>Store Procedures</li>
 	<li>Partition Functions/Schemes</li>
 	<li>Users</li>
 	<li>Roles</li>
</ul>
References and Links
<ul>
 	<li><a href="https://github.com/OpenDBDiff/OpenDBDiff" target="_blank" rel="nofollow noopener">OpenDBDiff</a></li>
 	<li><a href="https://www.mssqltips.com/sqlservertip/1069/sql-server-comparison-tools/" target="_blank" rel="nofollow noopener">Other Tools</a></li>
</ul>
&nbsp;
