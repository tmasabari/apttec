---
layout: post
title: Soft delete vs Hard delete Vs Business Scenarios
date: 2018-06-28 18:09
author: tmasabari
comments: true
categories: [Data Model, Design]
---
<h4>Hard delete as a valid option</h4>
<ul>
 	<li>Of course there is the need to delete things physically. Temporary data, old data, erroneous data.</li>
 	<li>There are cases that hard “delete” is a valid business operation. Let’s say I uploaded a photo of my mom instead of a scan of the contract. We might want to allow the user to delete within a certain context. Or maybe not. It’s a business decision. But to be clear, “delete” as a business operation should be understood to wipe something out with no auditing trail left behind.</li>
 	<li>Sometimes this can be enforced by law; i.e. the UK Data Protection Act enforces some fairly strict procedures of the data that a company keeps about its customers and sometimes the easiest way to comply is to simply not hold that data anymore.</li>
 	<li>One scenario that is more difficult though is the one where someone makes a mistake and puts something into the system they shouldn’t have. In those cases you need to cascade the delete since erroneously adding the item will cause problems downstream as other systems take action in response.
<ul>
 	<li>When someone creates an entity the first time, give it a status, say ‘<strong>tentative</strong>’, which requires some kind of authorization to make it visible to everyone else. We might only allow the ‘delete’ task to be performed on entities in the ‘tentative’ status.</li>
 	<li> When entities in that state are “published” or “authorized” is when we check for uniqueness and “reserve” that necessary name/code/resource.</li>
 	<li>Mistakes can happen in entity creation, but those are of relatively minor concern. The bigger concern is mistakenly deleting an entity. In this model, since you don’t delete, you can more easily revert back to a previous status (un-canceling an order).</li>
</ul>
</li>
</ul>
&nbsp;
<h4><strong>Model business rules VS Soft delete</strong></h4>
If you (as suggested) chose to replace physical deletes with modelling the business rules underlying this operation, you will still be faced with the two main problems associated with soft deletes.

1. bypass the referential integrity of the RDMS. (delete is replaced with status)? <strong>we don’t bypass RI – we actually model the business life cycle of important entities</strong>.
2. You end up with more complicated and error-prone queries? correspondingly, we show users what they need to see – <strong>adding a single where clause might make it a *tiny* bit more complex</strong>, but I’d hardly go so far as to say “error-prone”
<ul>
 	<li><strong>As long as the business people are making the tradeoffs</strong> between complexity/cost and value in the statuses, then we as developers have done our job.</li>
 	<li>It’s when we assume that deleting (whether soft or not) is a good enough technical solution – without vetting that with the business, that we overstep our responsibility.</li>
 	<li><strong>Flexibility equates to complexity.</strong> Hard deletes are easier to implement but can have far more profound effects. Soft deletes are more flexible, but require a lot more work to implement properly.
<ul>
 	<li>The SQL etc. might be rather trivial to fix, but the biggest problem is to locate all the places that need fixing – and *that* is error prone.</li>
 	<li>Neither is a big test suite going to help you: all your test will run fine since none of them are aware of the new status. Adding new tests helps of course, but figuring out which to add is also a problem.</li>
 	<li>As someone mentioned, <strong>every report and every screen has to account for the state of the record</strong>. In <strong>some cases, they have to allow for ignoring</strong> the state (i.e., don’t filter on anything). Thus, it is not just a matter of gleaning from the user what they are really trying to accomplish, it is a matter of presenting a <strong>cost/benefit proposal of development time vs flexibility</strong>.</li>
</ul>
</li>
</ul>
I think there's perfectly reasonable scenarios for both soft and hard deletes, with and without audit trails.
<table border="1">
<tbody>
<tr>
<td>Deletion Method</td>
<td>Use case</td>
</tr>
<tr>
<td>Soft delete</td>
<td>A user signs off of your service, but application need to keep (anonymized) stats data consistent for the customers - here application cannot remove the entire user, It just blank his/her personal data (name, email, phone, ...) and keep the anonymized statistical data (country, birth year, profession).</td>
</tr>
<tr>
<td>Soft (or super-soft) delete with audit trail</td>
<td>Any financial transaction data, even if entered by error, may only be corrected by adding a correction entry, not by deleting the erroneous entry. So either application flag it as deleted (soft delete) or application correct it by adding another entry ("super-soft delete").</td>
</tr>
<tr>
<td>Hard delete with audit trail</td>
<td>A user unsubscribes from the application. No need to keep the info "he once was subscribed to it" in the live database, but need to keep the info somewhere accessible in case he/she sues the product for spamming and business can prove "but back in August when you got the mail, you were still subscribed".</td>
</tr>
<tr>
<td>Hard delete with no audit trail</td>
<td>Personal data as in #1 if product's local data protection laws require. (This means <em>no</em> more storing, <em>anywhere</em>, technically speaking not even in last month's backup)</td>
</tr>
</tbody>
</table>
<h4>Regulated environment scenarios</h4>
<ul>
 	<li>When you live and work in a regulated environment, you do not have a choice - the data must live on. If it is added to the database, it shall remain in the database - no exceptions.</li>
 	<li>Plus, a secondary rule often comes into play - thou shall not read from the audit trail for anything other than audit reports. Therefore, you live with soft deletes and status tables</li>
</ul>
<h2 id="soft-delete">Soft Delete</h2>
<ul>
 	<li>Involves setting a column like deleted_flag when the row has to be ‘deleted’.</li>
 	<li>All queries involving the active flow of the application will ignore such entries with the condition ‘deleted_flag = 0’</li>
</ul>
<h2 id="hard-delete">Hard Delete</h2>
<ul>
 	<li>Involves directly deleting the data row from the table.</li>
 	<li>Many a times, the data (or action) is copyed onto an audit table to assist in possible debugging in the future.</li>
</ul>
<a href="http://abstraction.blog/2015/06/28/soft-vs-hard-delete" target="_blank" rel="nofollow noopener">Differences</a>
<table style="height: 732px;" border="1">
<tbody>
<tr style="height: 28px;">
<td style="height: 28px;">Description</td>
<td style="height: 28px;">Soft</td>
<td style="height: 28px;">Hard</td>
</tr>
<tr style="height: 28px;">
<td style="height: 28px;">Complexity to implement</td>
<td style="height: 28px;">Easy</td>
<td style="height: 28px;">Hard</td>
</tr>
<tr style="height: 28px;">
<td style="height: 28px;">Query active data (change in other parts of application)</td>
<td style="height: 28px;">Hard</td>
<td style="height: 28px;">Easy</td>
</tr>
<tr style="height: 240px;">
<td style="height: 240px;">
<ul>
 	<li>Unique index ensures data integrity by preventing multiple occurrences of a row at the database level.</li>
 	<li>Having soft delete prevents usage of Unique index.</li>
</ul>
for example, a User table that has a unique index on username; A deleted record would still block the deleted users username for new records. Working around this you could tack on a GUID to the deleted username column, but it's a very hacky workaround that I wouldn't recommend. Probably in that circumstance it would be better to just have a rule that once a username is used, it can never be replaced.</td>
<td style="height: 240px;">Yes</td>
<td style="height: 240px;">No</td>
</tr>
<tr style="height: 72px;">
<td style="height: 72px;">
<ul>
 	<li>For soft delete, we cannot make use of ‘ON DELETE’ cascading.</li>
 	<li>The alternative is to create an ‘UPDATE’ trigger which keeps track of deleted_flag.</li>
</ul>
</td>
<td style="height: 72px;"></td>
<td style="height: 72px;"></td>
</tr>
<tr style="height: 84px;">
<td style="height: 84px;">While this was good from the standpoint of<strong> auditing, troubleshooting, and reporting</strong> (This was an e-commerce / tools site for B2B transactions, and if someone used a tool, we wanted to record it even if their account was later turned off), it did have several downsides.</td>
<td style="height: 84px;">Yes</td>
<td style="height: 84px;">No</td>
</tr>
<tr style="height: 56px;">
<td style="height: 56px;">Performance Implications of keeping all that data, We to develop various archiving strategies. For example one area of the application was getting close to generating around 1Gb of data a week.</td>
<td style="height: 56px;"></td>
<td style="height: 56px;"></td>
</tr>
<tr style="height: 84px;">
<td style="height: 84px;">Cost of keeping the data does grow over time, while disk space is cheap, the ammount of infrastructure to keep and manage terrabytes of data both online and off line is a lot. It takes a lot of disk for redundancy, and people's time to ensure backups are moving swiftly etc.</td>
<td style="height: 84px;"></td>
<td style="height: 84px;"></td>
</tr>
<tr style="height: 112px;">
<td style="height: 112px;">Finally, a soft delete will work on a table with artificial keys, but potentially won't work on a table with a natural primary key (e.g. you "delete" someone from a table keyed by Social Security Number - what do you do when you need to add him back? Please don't say "include IsDeleted in a compound primary key".).</td>
<td style="height: 112px;"></td>
<td style="height: 112px;"></td>
</tr>
</tbody>
</table>
<h4>How to implement</h4>
<ul>
 	<li>This copying can be done with one of the following options :</li>
 	<li>– Listener code in the application (observer pattern)</li>
 	<li>– Database Trigger – Combine the copy + delete operations in a stored procedure.</li>
</ul>
When you write UPDATE statement to the isDeleted column, write INSERT INTO another table and DELETE it from original table. If the situation is of rollback, write another INSERT INTO and DELETE in reverse order. If you are worried about a failed transaction, wrap this code in TRANSACTION.

<a href="http://blog.sqlauthority.com/2010/09/03/sql-server-soft-delete-isdelete-column-your-opinion/" target="_blank" rel="nofollow noopener">What are the advantages of the smaller table verses larger table in above described situations?</a>
<ul>
 	<li>A smaller table is easy to maintain</li>
 	<li>Index Rebuild operations are much faster</li>
 	<li>Moving the archive data to another filegroup will reduce the load of primary filegroup (considering that all filegroups are on different system) – this will also speed up the backup as well.</li>
 	<li>Statistics will be frequently updated due to smaller size and this will be less resource intensive.</li>
 	<li>Size of the index will be smaller</li>
 	<li>Performance of the table will improve with a smaller table size</li>
</ul>
<h4>Soft delete is not an option</h4>
<ul>
 	<li>One of the annoyances that we have to deal when building enterprise applications is the requirement that no data shall be lost.</li>
 	<li>The usual response to that is to introduce a WasDeleted or an IsActive column in the database and implement deletes as an update that would set that flag.</li>
 	<li>Simple, easy to understand, quick to implement and explain. It is also, quite often, wrong.</li>
</ul>
Consider soft-delete as an anti-pattern. For exactly the reason Rafal says - it makes your database very fragile with FKs to deleted items, and adds a mandatory additional layer of complexity to queries and joins (where deleted = 0) that is not ORM-friendly and can cause serious problems if you forget.
<ul>
 	<li>We've been slowly replacing soft deletes with AFTER DELETE/UPDATE triggers that copy it to an xyz_log table.</li>
 	<li>It's already accepted not to mix reporting concerns with your transactional database. I think you shouldn't mix audit logging in the live tables either.</li>
</ul>
<h1>References</h1>
<ul>
 	<li><a href="https://ayende.com/blog/4157/avoid-soft-deletes" target="_blank" rel="nofollow noopener">https://ayende.com/blog/4157/avoid-soft-deletes</a></li>
 	<li>http://richarddingwall.name/2009/11/20/the-trouble-with-soft-delete/</li>
</ul>
