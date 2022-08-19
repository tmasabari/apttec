---
layout: post
title: log database
date: 2018-12-20 16:58
author: tmasabari
comments: true
categories: [Architecture, Data Model, Design]
---
<!-- wp:heading -->
<h2>Donot use RDBMS</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Even though many sites use an SQL database for logging, it’s not really the most efficient place to store data from a logging workload. </li><li>Logs don’t require UPDATE/DELETE or rollback, they’re basically an append-only workload. So using a database engine that is designed to support OLTP workload is missing an opportunity to use a more specialized storage solution.</li><li>This one seems ok on the surface and the "I might need to use a complex query on them at some point in the future" argument seems to win people over. Storing your logs in a database isn't a HORRIBLE idea, but storing them in the same database as your other production data is.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Usage</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>The reason I ask that of clients is that often they haven’t thought about it, they fell into the habit of keeping activity and they were going to address how much to keep at another time.</li><li>But even though storage is cheap, when you have a lot of it it adds up. We’ve had teams that got a bad architecture going and started costing serious money in cloud storage.</li><li>Can the logs be converted to summary form? Can they be set up in a time-to-live situation where you keep no more than two months of data (for example)?</li><li>Definitely store it somewhere else no matter the answers to the above. A different database initially, with some thought as to which underlying MySQL storage engine is in use. Then maybe shop around for a more suitable solution.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Design</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A few things:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>If you do a lot of logging - and you want a queryable log - you may want to log to a dedicated logging instance so it doesn’t interfere with the rest of your production data.</li><li>If you have even more logging, you may want to use an external logging mechanism such as MongoDB + app-level logging:&nbsp;<a href="https://docs.mongodb.com/ecosystem/use-cases/storing-log-data/" rel="noreferrer noopener" target="_blank">Storing Log Data</a>. This approach is used by many newer websites (even if they otherwise don’t use MongoDB).</li><li>You can also use the “ELK stack” (<a href="https://en.wikipedia.org/wiki/Elasticsearch" rel="noreferrer noopener" target="_blank">Elasticsearch</a>&nbsp;+ Logstash + Kibana), but as you’re already logging to a db, this may require significant refactoring.</li><li>If you really want your log table in your app database (maybe users can view or search it, etc), you may want to partition the log table by date and delete log entries that are older than a specific time.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>If you want to use the last option, an approach that has worked well for me is to create a “Unix day” field and PARTITION by a HASH on this field, with enough partitions to hold all the days you’re interested in. You then have a script that purges the oldest day every night.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Logic similar to the purge script could dump to a transfer table that is dumped and loaded to a “cold archive” if you need to save the log for data mining,&nbsp;<a href="https://en.wikipedia.org/wiki/Sarbanes%E2%80%93Oxley_Act" rel="noreferrer noopener" target="_blank">SOX</a>reasons, etc - and then purge from the active db.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Characterstics</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>You likely want a database with the following characteristics:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>The ability to do writes without blocking on logging -&nbsp;</strong>you want a write to return as soon as possible.</li><li><strong>Ability to handle flexible schema</strong>&nbsp;- That is, you may add or remove components to a log.</li><li><strong>Ability to query on arbitrary fields</strong></li><li><strong>Ability to index on arbitrary fields&nbsp;</strong>(optional)</li><li><strong>Horizontally scalable</strong>&nbsp;- as you alluded to, your logs are too big to fit on a single node. Also related: ability to handle distributed queries / aggregates</li><li><strong>Capping&nbsp;</strong>(optional) - Maybe you want to limit it to a certain size or a certain age.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Given these choices, I think MongoDB is your best bet.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><a href="https://www.quora.com/What-is-the-best-way-to-use-database-to-log-activities-1">https://www.quora.com/What-is-the-best-way-to-use-database-to-log-activities-1</a></li></ul>
<!-- /wp:list -->
