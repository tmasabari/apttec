---
layout: post
title: Database design
date: 2018-07-31 14:03
author: tmasabari
comments: true
categories: [Data Model, Databases, Design, Design]
---
<ol>
 	<li>Internationalization: varchar vs nvarchar
<ol>
 	<li>Cook county implementation assumed the product stores English/latin characters only. So they selected varchar  for all the text fields.</li>
 	<li>Please note Oakland and Macomb uses Google translation to provide public search UI in multiple languages.</li>
 	<li>In any case, business expects to store data in any other language, nvarchar type needs to be used.</li>
 	<li>Cost of storing a character using nvarchar (2 bytes per character) is double over varchar (1 byte).</li>
</ol>
</li>
 	<li>Selecting the size of surrogate keys (auto increment numbers)
<ol>
 	<li>If any table is expected to grow more than 2 billion rows. They should have bigint surrogate keys. Otherwise int keys can be used.</li>
 	<li>Bigint (8 Bytes)  -1 to 2^63-1 (9,223,372,036,854,775,807). Negative numbers are not applicable
<ol>
 	<li>Consider ATT: assuming 100 million customers, 1 text per day for 30 days, that's 3 billion records that need an id field for just one month of use.</li>
 	<li>Imagine you have a table with - say - 10 million rows (orders for your company). Let's say, you have an Orders table, and that OrderID which you made a BIGINT is referenced by 5 other tables, and used in 5 non-clustered indices on your Orders table - not overdone, I think, right?10 million rows, by 5 tables plus 5 non-clustered indices, that's 100 million instances where you are using 8 bytes each instead of 4 bytes - 400 million bytes = 400 MB. A total waste</li>
</ol>
</li>
 	<li>Int (4 Bytes)       -1 to 2^31-1 (2,147,483,647). Negative numbers are not applicable</li>
</ol>
</li>
 	<li>DateTime fields name convention
<ol>
 	<li>Though certain fields will hold both DateTime, generally their name just have ApprovalDate etc. But if we want to be more precise in our naming conventions, we can add DateTime suffix to the columns like ApprovalDateTime</li>
 	<li>If fields are going to have only date portion we can have date type columns</li>
</ol>
</li>
 	<li>Selecting the length of the text fields
<ol>
 	<li>The length of the text fields affect the performance of the queries. So correct field sizes needs to be considered.</li>
 	<li>Normally the length of the fields are decided as part of the user stories prepared by the BA.</li>
 	<li>As per my understanding, there are currently no guidelines/standards available for the US government for the length address and names. However there is an old document from the UK government <a href="http://webarchive.nationalarchives.gov.uk/+/http:/www.cabinetoffice.gov.uk/media/254290/GDS%20Catalogue%20Vol%202.pdf">UK Government Data Standards Catalogue</a>. Generally,
<ol>
 	<li>If we have first name and last name separately each will have 50 characters</li>
 	<li>Length of organization names are 90 characters</li>
</ol>
</li>
</ol>
</li>
</ol>
<ul>
 	<li>Email address length is 70 characters</li>
</ul>
<ol>
 	<li>Whenever the length of the field may grow beyond 8000 characters, varchar(max) should be used. It supports up to 2 GB.  But it will have performance issues.</li>
 	<li>Reference: <a href="https://stackoverflow.com/questions/20958/list-of-standard-lengths-for-database-fields">https://stackoverflow.com/questions/20958/list-of-standard-lengths-for-database-fields</a></li>
</ol>
Selecting integer data type
<table>
<tbody>
<tr class="ztXv9">
<th>Data type</th>
<th>Range</th>
<th>Storage</th>
</tr>
<tr>
<td>bigint</td>
<td>-2^63 (-9,223,372,036,854,775,808) to 2^<b>63-1</b>(9,223,372,036,854,775,807)</td>
<td><b>8 Bytes</b></td>
</tr>
<tr>
<td>int</td>
<td>-2^31 (-2,147,483,648) to 2^<b>31-1</b> (2,147,483,647)</td>
<td><b>4 Bytes</b></td>
</tr>
<tr>
<td>smallint</td>
<td>-2^15 (-32,768) to 2^15-1 (32,767)</td>
<td><b>2 Bytes</b></td>
</tr>
<tr>
<td>tinyint</td>
<td>0 to 255</td>
<td><b>1 Byte</b></td>
</tr>
</tbody>
</table>
&nbsp;

&nbsp;

8 byte encoding - varchar

Most popular encoding in SQL Server is SQL_Latin1_General_CP1_CI_AS.

The default encoding for CHAR is <code>iso_1</code>, which is actually <code>ISO 8859-1</code>

varchar can hold the latin alphabet (which English and the western European languages use) and some special characters which can be used for any number of characters.

ISO 8859-1 encodes what it refers to as "Latin alphabet no. 1," consisting of 191 <a title="Character (computing)" href="https://en.wikipedia.org/wiki/Character_(computing)">characters</a>from the <a title="Latin script" href="https://en.wikipedia.org/wiki/Latin_script">Latin script</a>. This character-encoding scheme is used throughout the <a title="Americas" href="https://en.wikipedia.org/wiki/Americas">Americas</a>, <a title="Western Europe" href="https://en.wikipedia.org/wiki/Western_Europe">Western Europe</a>, <a title="Oceania" href="https://en.wikipedia.org/wiki/Oceania">Oceania</a>, and much of <a title="Africa" href="https://en.wikipedia.org/wiki/Africa">Africa</a>. It is also commonly used in most standard romanizations of East-Asian languages. It is the basis for most popular 8-bit character sets and the first block of characters in <a title="Unicode" href="https://en.wikipedia.org/wiki/Unicode">Unicode</a>.

The <a title="Windows-1252" href="https://en.wikipedia.org/wiki/Windows-1252">Windows-1252</a> code page coincides with ISO-8859-1 for all codes except the range 128 to 159 (<a title="Hexadecimal" href="https://en.wikipedia.org/wiki/Hexadecimal">hex</a> 80 to 9F), where the little-used C1 controls are replaced with additional <a title="Character (computing)" href="https://en.wikipedia.org/wiki/Character_(computing)">characters</a> including all the missing characters provided by <a class="mw-redirect" title="ISO-8859-15" href="https://en.wikipedia.org/wiki/ISO-8859-15">ISO-8859-15</a>.

&nbsp;

http://rusanu.com/2010/03/22/performance-comparison-of-varcharmax-vs-varcharn/

The non-max types can internally be represented as an ordinary pointer-and-length structure. But the max types cannot be stored internally as a contiguous memory area, since they can possibly grow up to 2Gb. So they have to be represented by a streaming interface, similar to COM's <a href="http://msdn.microsoft.com/en-us/library/aa380034%28VS.85%29.aspx" target="_blank" rel="noopener">IStream</a>. This carries over to every operation that involves the max types, including simple assignment and comparison, since these operations are more complicated over a streaming interface. The biggest impact is visible in the code that allocates and assign max-type variables (my first test), but the impact is visible on every operation.

The impact is reasonable on most operations with the max type operations being about 10% slower.

Actually, in a recent project of mine I had to change a column type from varchar(max) to varchar(5000) to alleviate the impact of max-types performance. The code happened to be on a very very performance critical path and testing clearly showed the impact was not only measurable, was quite actually quite serious. The processing throughput increased by about 25% just from this minor change in my case.

&nbsp;

https://dba.stackexchange.com/questions/162113/would-using-varchar5000-be-bad-compared-to-varchar255#162117

Here's a demo from <a href="https://groupby.org/2016/11/t-sql-bad-habits-and-best-practices/">my recent GroupBy presentation on bad habits</a> that makes it easy to prove for yourself (requires SQL Server 2016 for some of the <code>sys.dm_exec_query_stats</code> output columns, but should still be provable with <code>SET STATISTICS TIME ON</code> or other tools on earlier versions); it shows larger memory and longer runtimes for <em>the same query</em> against <em>the same data</em> - the only difference is the declared size of the columns:

<img src="https://i.stack.imgur.com/m5MVf.png" />
<p id="wqhowwD"><img class="alignnone size-full wp-image-1628 " src="/wp-content/uploads/2018/07/img_5b60490870b8d.png" alt="" /></p>
