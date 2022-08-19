---
layout: post
title: DB Patterns
date: 2018-07-02 21:48
author: tmasabari
comments: true
categories: [Data Model, Design]
---
Design patterns are reusable, by definition. They're patterns <em>you</em> detect in other good solutions.

A pattern is not trivially reusable. You can implement your down design following the pattern however.

Relational design patters include things like:
<ol>
 	<li>One-to-Many relationships (master-detail, parent-child) relationships using a foreign key.</li>
 	<li>Many-to-Many relationships with a bridge table.</li>
 	<li>Optional one-to-one relationships managed with NULLs in the FK column.</li>
 	<li>Star-Schema: Dimension and Fact, OLAP design.</li>
 	<li>Fully normalized OLTP design.</li>
 	<li>Multiple indexed search columns in a dimension.</li>
 	<li>"Lookup table" that contains PK, description and code value(s) used by one or more applications. Why have code? I don't know, but when they have to be used, this is a way to manage the codes.</li>
 	<li>Uni-table. [Some call this an anti-pattern; it's a pattern, sometimes it's bad, sometimes it's good.] This is a table with lots of pre-joined stuff that violates second and third normal form.</li>
 	<li>Array table. This is a table that violates first normal form by having an array or sequence of values in the columns.</li>
 	<li>Mixed-use database. This is a database normalized for transaction processing but with lots of extra indexes for reporting and analysis. It's an anti-pattern -- don't do this. People do it anyway, so it's still a pattern.</li>
</ol>
&nbsp;
<h2>References</h2>
<ul>
 	<li>There's a book in Martin Fowler's Signature Series called <a href="http://www.ambysoft.com/books/refactoringDatabases.html" rel="noreferrer">Refactoring Databases</a>. That provides a list of techniques for refactoring databases. I can't say I've heard a list of database patterns so much.

&nbsp;</li>
 	<li>I would also highly recommend David C. Hay's <a href="https://www.amazon.com/dp/0120887983" rel="noreferrer">Data Model Patterns</a> and the follow up <a href="https://www.amazon.com/dp/0120887983" rel="noreferrer">A Metadata Map</a> which builds on the first and is far more ambitious and intriguing. The Preface alone is enlightening.

&nbsp;</li>
 	<li>Also a great place to look for some pre-canned database models is Len Silverston's Data Model Resource Book Series <a href="https://www.amazon.com/dp/0471380237" rel="noreferrer">Volume 1</a> contains universally applicable data models (employees, accounts, shipping, purchases, etc), <a href="https://www.amazon.com/dp/0471353485" rel="noreferrer">Volume 2</a> contains industry specific data models (accounting, healthcare, etc), <a href="https://www.amazon.com/dp/0470178450" rel="noreferrer">Volume 3</a> provides data model patterns.

&nbsp;</li>
 	<li>Finally, while this book is ostensibly about UML and Object Modelling, Peter Coad's <a href="https://www.amazon.com/dp/013011510X" rel="noreferrer">Modeling in Color With UML</a> provides an "archetype" driven process of entity modeling starting from the premise that there are 4 core archetypes of any object/data model</li>
 	<li>https://stackoverflow.com/questions/145689/relational-database-design-patterns</li>
 	<li>http://www.databaseanswers.org/data_models/</li>
 	<li><a href="http://database-programmer.blogspot.com/" rel="noreferrer">The Database Programmer</a>.</li>
 	<li>Here is a link to a gentleman who has developed several hundred free database schemas.

<a href="http://www.databaseanswers.org/data_models/" rel="noreferrer">http://www.databaseanswers.org/data_models/</a></li>
 	<li><a href="http://www.amazon.co.uk/Data-Model-Resource-Book-Enterprises/dp/0471380237/ref=pd_sim_b_2" rel="nofollow noreferrer">The Data Model Resource Book: A Library of Universal Data Models for All Enterprises: Vol 1</a>

&nbsp;</li>
 	<li><a href="http://www.amazon.co.uk/Data-Model-Resource-Book-Universal/dp/0471353485/ref=pd_sim_b_3" rel="nofollow noreferrer">The Data Model Resource Book: A Library of Universal Data Models by Industry Types: Vol 2</a>

&nbsp;</li>
 	<li><a href="http://www.amazon.co.uk/Data-Model-Resource-Book-Universal/dp/0470178450/ref=cm_cr_pr_product_top" rel="nofollow noreferrer">The Data Model Resource Book: Universal Patterns for Data Modeling Vol 3</a></li>
 	<li>I recommend <a href="http://www.intelligententerprise.com/030320/605celko1_1.jhtml" rel="noreferrer">this articly by Joe Celko</a> for more on keys.

More general notes:

Suggestions for schema designs/data models for different businesses: David C. Hay: Data Model Patterns: Conventions of Thought Rather old, but there is a reason why it's still in print
<a href="http://www.dorsethouse.com/books/dmp.html" rel="noreferrer">http://www.dorsethouse.com/books/dmp.html</a>

Maybe not very pattern-like, but still very good: Stephane Faroult, Peter Robson: The Art of SQL<a href="http://oreilly.com/catalog/9780596008949/" rel="noreferrer">http://oreilly.com/catalog/9780596008949/</a>

Another one which I can recommend: Vadim Tropashko: SQL Design Patterns - The Expert Guide to SQL Programming <a href="http://www.rampant-books.com/book_2006_1_sql_coding_styles.htm" rel="noreferrer">http://www.rampant-books.com/book_2006_1_sql_coding_styles.htm</a>

Systematic text-book about data modelling: Graeme Simsion &amp; Graham Witt, "Data Modeling Essentials" <a href="http://www.elsevierdirect.com/product.jsp?isbn=9780126445510" rel="noreferrer">http://www.elsevierdirect.com/product.jsp?isbn=9780126445510</a>

Maybe you are actually looking for a "style guide"?. I that case: Joe Celko: SQL Programming Style<a href="http://www.elsevierdirect.com/product.jsp?isbn=9780120887972" rel="noreferrer">http://www.elsevierdirect.com/product.jsp?isbn=9780120887972</a></li>
</ul>
