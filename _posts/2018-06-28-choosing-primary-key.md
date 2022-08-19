---
layout: post
title: Choosing Primary key
date: 2018-06-28 17:51
author: tmasabari
comments: true
categories: [Data Model, Design]
---
<strong>Summary</strong>
<ol>
 	<li>For reference Tables - Use natural key</li>
 	<li>For lookup tables, master tables, transaction tables - use surrogate keys</li>
</ol>
&nbsp;
<h2><a href="http://www.itprotoday.com/business-intelligence/what-makes-good-primary-key">What Makes a Good Primary Key</a></h2>
When you evaluate candidates for a table's primary key, follow these rules:
<ol class="articlelist">
 	<li> The primary key should consist of one column whenever possible.</li>
 	<li> The name should mean the same 5 years from now as it does today.</li>
 	<li> The data value should be <strong>non-null</strong> and <strong>remain constant over time</strong>. (The primary key you choose must have a constant and unchanging set of values)
<ol>
 	<li>When you assign a primary key value to a record, the value must not change for the life of that record and</li>
 	<li>you can't reuse the value—even after the record is deleted from the table.</li>
</ol>
</li>
 	<li> The data type should be either an <strong>integer or a short, fixed-width character</strong>.</li>
 	<li> If you're using a character data type, the primary key should <strong>exclude differential capitalization, spaces, and special characters</strong>, which might be difficult to remember.</li>
</ol>
<ul>
 	<li>The primary key's purpose is to be used internally for distinguishing one row from another. You can use the primary key as a search key, but using a natural key for searching is usually easier. For example, a Customer table's primary key might be called CustID, which is a 16-digit surrogate key. Although CustID uniquely identifies each row in the Customer table, you don't expect customers to be able to identify themselves by their customer ID. Instead, customers give you their name, phone number, and perhaps a residence or mailing address. This combination of attributes is a search key.</li>
</ul>
Questions that point to a primary key's four criteria:
<ul>
 	<li> Is the primary key unique?</li>
 	<li> Does it apply to all rows?</li>
 	<li> Is it minimal?</li>
 	<li> Is it stable over time? (should not change)</li>
</ul>
Question <em>"Should I inject an artificial key or not?"</em> always <strong>depends</strong> on natural key structure:
<ul>
 	<li>If it contains a large string, then it is slower and will add data overhead if migrating as foreign to another entity.</li>
 	<li>If it consists of multiple columns, then it is slower and will add data overhead if migrating as foreign to another entity.</li>
</ul>
<h3>RID</h3>
<ul>
 	<li>Although SQL Server assigns a row identifier (RID) to each record in a file, users and user programs can't use an RID as a uniqueidentifier, because you can't guarantee that an RID will remain constant over time.</li>
 	<li>Therefore, an RID doesn't meet the criterion that a primary key's value must never change.</li>
 	<li>An RID is composed of a file number, a page number, and a page's row number. As the position of each record shifts in the file, the record's associated RID changes.</li>
 	<li>In addition to these logical reasons for not using an RID as a primary key, you can't access it through any supported programming interface.</li>
</ul>
&nbsp;
<h1><a href="https://www.mssqltips.com/sqlservertip/5431/surrogate-key-vs-natural-key-differences-and-when-to-use-in-sql-server/" target="_blank" rel="nofollow noopener">Surrogate key Vs Natural Key</a></h1>
References: <a href="https://dba.stackexchange.com/questions/50708/do-natural-keys-provide-higher-or-lower-performance-in-sql-server-than-surrogate" target="_blank" rel="nofollow noopener">2</a>
<h2>Surrogate Key Overview</h2>
A surrogate key is a system generated (could be GUID, sequence, etc.) value with no business meaning that is used to uniquely identify a record in a table.  The key itself could be made up of one or multiple columns.
<ul>
 	<li>GUID</li>
 	<li>Identity column</li>
</ul>
<h2>Natural Key Overview</h2>
A natural key is a column or set of columns that already exist in the table (e.g. they are attributes of the entity within the data model) and uniquely identify a record in the table.  Since these columns are attributes of the entity they obviously have business meaning.
<h2>Natural Key Pros</h2>
<ul>
 	<li>Key values have <strong>business meaning</strong> and can be used as a search key when querying the table</li>
 	<li>Column(s) and primary key index already exist so <strong>no disk extra space</strong> is required for the extra column/index that would be used by a surrogate key column</li>
 	<li><strong>Fewer table joins since join columns have meaning</strong>.  For example, this can reduce disk IO by not having to perform extra reads on a lookup table</li>
</ul>
<h2>Natural Key Cons</h2>
<ul>
 	<li>May need to <strong>change/rework key if business requirements change</strong>.  For example, if you used SSN for your employee as in the example above and your company expands outside of the United States not all employees would have a SSN so you would have to come up with a new key.</li>
 	<li>More difficult to maintain<strong> if key requires multiple columns</strong>.  It's much easier from the application side dealing with a key column that is constructed with just a single column.
<ul>
 	<li>Poorer performance since key value is usually larger and/or is made up of multiple columns.  Larger keys will require more IO both when inserting/updating data as well as when you query.</li>
</ul>
</li>
 	<li>Can't enter record until key value is known.  It's sometimes beneficial for an application to load a <strong>placeholder record</strong> in one table then load other tables and then come back and update the main table.You do not need to bother about their creation and handling (in most cases) as this feature handled by database engine. They are unique by default and doesn't take a lot of space. Custom operations like <code>ON UPDATE CASCADE</code> might be ommited, because key values not changing.</li>
 	<li>Can sometimes be <strong>difficult to pick a good key</strong>.  There might be multiple candidate keys each with their own trade-offs when it comes to design and/or performance.</li>
</ul>
<h2>Surrogate Key Pros</h2>
<ul>
 	<li>You <strong>do not need to bother about their creation and handling</strong> (in most cases) as this feature handled by database engine. They are unique by default and doesn't take a lot of space. Custom operations like <code><strong>ON UPDATE CASCADE</strong></code><strong> might be ommited</strong>, because key values not changing.</li>
 	<li>No business logic in key so no changes based on business requirements.  For example, if the Employee table above used a integer surrogate key you could simply add a separate column for SIN if you added an office in Canada (to be used in place of SSN)</li>
 	<li>Less code if maintaining same key strategy across all entities.  For example, application code can be reused when referencing primary keys if they are all implemented as a sequential integer.</li>
 	<li>Better performance since key value is smaller and simple type.  Less disk IO is required on when accessing <strong>single column indexes</strong>.</li>
 	<li>Surrogate key is guaranteed to be unique.  For example, when moving data between test systems you don't have to worry about duplicate keys since new key will be generated as data is inserted.</li>
 	<li>If a sequence used then there is little index maintenance required since the value is ever increasing which leads to less index fragmentation.</li>
</ul>
<h2>Surrogate Key Cons</h2>
<ul>
 	<li><strong>For an association entities</strong>, which keys are not migrate anywhere, it might become a pure data overhead, as it usefulness is lost. Complex natural primary key (if there are no string columns there) will be more useful.
<ul>
 	<li>Extra column(s)/index for surrogate key will require extra disk space</li>
 	<li>Extra column(s)/index for surrogate key will require extra IO when insert/update data</li>
</ul>
</li>
 	<li>Requires more table joins to child tables since data has no meaning on its own.</li>
 	<li>Can have duplicate values of natural key in table if there is no other unique constraint defined on the natural key</li>
 	<li>Difficult to differentiate between test and production data.  For example, since surrogate key values are just auto-generated values with no business meaning it's hard to tell if someone took production data and loaded it into a test environment.</li>
 	<li>Key value has no relation to data so technically design breaks 3NF</li>
 	<li>The surrogate key value can't be used as a search key</li>
 	<li>Different implementations are required based on database platform.   For example, SQL Server identity columns are implemented a little bit different than they are in Postgres or DB2.</li>
 	<li>We can now see the surprising fact that the <strong>integer keys</strong> will slow us down in many situations. Not only do they have no performance advantage, but they actually hurt performance. The reason is because they <i><b>require joins on almost every query</b></i>.</li>
 	<li>A 3-table query with two joins will always be much slower than a 1-table query with no joins. If you are using an ORM system that does not do JOIN's, but instead does separate fetches, then you have <i>3 round trips to the server instead of 1</i>, and heaven forbid you have queries in a nested loop, the performance will simply crash and burn.</li>
</ul>
<h4>Surrogate Keys for ORM tools</h4>
<ul>
 	<li>Your programs can be made simpler in many cases if you add an "Object ID" to every single table in addition to the primary key. An object id is useful specifically for user interface code. If you use an object id, then it is easier to write UPDATE and DELETE statements, and it is easier to write framework or <strong>ORM code that does these things for you</strong>.</li>
 	<li>If you are following these rules of thumb closely in your project then it is important not to use the object id as a primary key, and therefore you may never use it as a foreign key either. If you use an object id as the primary key then you lose a lot of the benefits of the character keys listed above.</li>
 	<li>Also if you follow these rules in your projects it means that your transaction tables have both an auto-generated primary key like CART_ID and an auto-generated object id. Some programmers are bothered by this because we don't like the idea that two columns appear to be doing the same thing, and we try to save a column. But personally this does not bother me because it helps me write robust applications, and this is not 1985 where a 10MB hard drive cost hundreds of dollars.</li>
</ul>
<h4>GUID As Keys</h4>
<ul>
 	<li>Sometimes it makes sense to use random keys. GUID (Globally Unique Identifier) is basically a 128 bit integer that's randomly generated using a certain algorithm. The idea actually precedes windows and the standard is implemented on other platforms.</li>
 	<li>While having a 128 bit integer as an index column causes some performance concern, it has one advantage over sequential keys; You can easily merge data from different databases. Just dump the data from one database and insert it into the next one.
<ul>
 	<li>1) 128 bits is wide, that means fewer rows per page, more pages taking up more buffer cache. This impacts every part of query processing from more data to pull from disk to more cpu time &amp; cache misses when computing joins, etc.</li>
 	<li>2) Fragmentation and data packing-- guid keys necessarily cause more splits, which results in much less compaction, resulting in poor space utlization (i.e. more pages, etc.)</li>
 	<li>3) cache locality-- there is often (not always) some "temporal" locality when inserting adjacent records. I.e. inserting checks for a bank deposit: if there were four checks then you might insert all four into the "checks" table at the same time. With "random" keys, these checks will end up in different locations in the index. When you later must retrieve the checks in the transaction, you will be pulling from four different locations instead of from one location (in the case of sequential keys). The point is that you break the spacial locality which often benefits the intrinsic temporal locality present in a lot of tables/relationships.</li>
</ul>
</li>
</ul>
<h2><a href="https://dba.stackexchange.com/questions/50708/do-natural-keys-provide-higher-or-lower-performance-in-sql-server-than-surrogate" target="_blank" rel="nofollow noopener">Indexes and Keys</a></h2>
<ul>
 	<li>In general, SQL Server uses <a href="http://en.wikipedia.org/wiki/B+_tree" rel="nofollow noreferrer">B+Trees</a> for indexes. The expense of an index seek is directly related to the length of the key in this storage format. Hence, a surrogate key usually outperforms a natural key on index seeks.</li>
 	<li>SQL Server clusters a table on the primary key by default. The clustered index key is used to identify rows, so it gets added as included column to every other index. The wider that key, the larger every secondary index.</li>
 	<li>Even worse, if the secondary indexes are not explicitly defined as <code>UNIQUE</code> the clustered index key automatically becomes part of the key of each of those. That usually applies to most indexes, as usually indexes are declared as unique only when the requirement is to enforce uniqueness.</li>
 	<li><strong>So if the question is, natural versus surrogate clustered index, the surrogate will almost always win.</strong></li>
 	<li>On the other hand, you are adding that surrogate column to the table making the table in itself bigger. That will cause clustered index scans to get more expensive. So, if you have only very few secondary indexes and your workload requires to look at all (or most of the) rows often, you actually might be better of with a natural key saving those few extra bytes.</li>
</ul>
References
<ul>
 	<li>http://www.itprotoday.com/business-intelligence/surrogate-key-vs-natural-key</li>
</ul>
