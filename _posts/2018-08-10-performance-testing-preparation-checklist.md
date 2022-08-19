---
layout: post
title: Performance Testing - Preparation & Checklist
date: 2018-08-10 13:25
author: tmasabari
comments: true
categories: [NFR, Performance, Testing]
---
Metrics and Environment
<table width="0">
<tbody>
<tr>
<td style="width: 383.583px;">Identify Performance metrics for different type of operations

Response time Vs Number of concurrent users for each category of operations
<ol>
 	<li>OLTP</li>
 	<li>Batch operations &amp; ETL opertions</li>
 	<li>Report generations - SSRS, PDF etc</li>
 	<li>Text file generations</li>
 	<li>External dependencies - AD, Email etc</li>
</ol>
</td>
<td style="width: 266.417px;">Architect</td>
</tr>
<tr>
<td style="width: 383.583px;">Identify the suitable hardware for the performance testing. If possible, have environment similar to the Production. Provide deployment architecture to performance test team.</td>
<td style="width: 266.417px;">Architect</td>
</tr>
<tr>
<td style="width: 383.583px;">Check latency between the servers where the VSTS scripts are run and the server where the application.</td>
<td style="width: 266.417px;">Operations team</td>
</tr>
<tr>
<td style="width: 383.583px;">No of errors and error percentage to be included in the VSTS performance Report</td>
<td style="width: 266.417px;">Srini</td>
</tr>
<tr>
<td style="width: 383.583px;">Before running the test script in Sac Test environment, drop an email to us. We will let respective team know to refrain from doing any activities</td>
<td style="width: 266.417px;">Test Team</td>
</tr>
<tr>
<td style="width: 383.583px;">Once a server is found in AFRM domain, set up a call for Thursday - have a live working session to track app dynamics results</td>
<td style="width: 266.417px;">Test Team</td>
</tr>
</tbody>
</table>
&nbsp;

Development checklist
<table>
<tbody>
<tr>
<td width="34">S. No</td>
<td width="99">Issue</td>
<td width="338">Checklist / Action items</td>
</tr>
<tr>
<td width="34">1</td>
<td width="99">Slow DB Operations</td>
<td width="338">Rebuild indexes before each performance test</td>
</tr>
<tr>
<td width="34">2</td>
<td width="99">&nbsp;</td>
<td width="338">Update SQL Server statistics before each performance test</td>
</tr>
<tr>
<td width="34">3</td>
<td width="99">&nbsp;</td>
<td width="338">Check all the necessary indexes are in place for the frequently used operations like Staff search. (Staff search stored procedure takes 10 seconds on average to execute)</td>
</tr>
<tr>
<td width="34">4</td>
<td width="99">Performance hit even on the landing page (enter url)</td>
<td width="338">All the static files need to be cached in the browser until there’s a change in server.

They should not be loaded for each and every operation</td>
</tr>
<tr>
<td width="34">5</td>
<td width="99">&nbsp;</td>
<td width="338">All the dynamic pages need to be cached on the server for a very short period (say few seconds based up on functionality). SharePoint pages, SP Documents and  web parts etc.

·       <a href="https://www.c-sharpcorner.com/UploadFile/Roji.Joy/how-to-configuring-page-output-caching-in-sharepoint-2013/">https://www.c-sharpcorner.com/UploadFile/Roji.Joy/how-to-configuring-page-output-caching-in-sharepoint-2013/</a>

·       <a href="https://docs.microsoft.com/en-us/sharepoint/administration/cache-settings-operations">https://docs.microsoft.com/en-us/sharepoint/administration/cache-settings-operations</a></td>
</tr>
<tr>
<td width="34">6</td>
<td width="99">&nbsp;</td>
<td width="338">The caching can be enabled at the user control level using very by param etc.

<a href="https://msdn.microsoft.com/en-us/library/53a3xxk8.aspx">https://msdn.microsoft.com/en-us/library/53a3xxk8.aspx</a></td>
</tr>
</tbody>
</table>
&nbsp;

Sample volume and SLAs

The office records approximately 3,000 to 4,000 real and personal property documents every day and approximately one million per year.  Around 50% are recorded electronically, and 50% over the counter/mail. The County typically scans 1500-2000 documents a day, with each document averaging 5 pages for a total page scan of 10,000 pages/day.

&nbsp;

Around 50 million documents and images for real property currently reside on 20/20 (the legacy system).  Vitals are not in scope of the project.

[In the table below, the AFRM Response column states that AFRM satisfies the metric; if it does not satisfy the metric, it explains what action needs to be taken.]

Volume and Capacity Table
<table width="0">
<tbody>
<tr>
<td colspan="3" width="630"><strong>Response Time Online and Daily Volume</strong>

The response time to User commands must not exceed the response times defined below. The system should continue to stay within the expected response times accounting for future growth. Response times must be achievable during all other System activities (e.g., report generation, System backup, etc.).

&nbsp;</td>
</tr>
<tr>
<td width="192"><strong>Activity</strong></td>
<td width="156"><strong>Metric</strong></td>
<td width="282"><strong>AFRM Response</strong></td>
</tr>
<tr>
<td width="192">Transactions that require validation

&nbsp;</td>
<td width="156">2 sec

&nbsp;</td>
<td width="282">Proposed solution will meet this SLA with the required hardware as outlined in this document.</td>
</tr>
<tr>
<td width="192">Bulk retrieval database queries

&nbsp;</td>
<td width="156">5 seconds</td>
<td width="282">Proposed solution will meet this SLA with the required hardware as outlined in this document.</td>
</tr>
<tr>
<td width="192">Cashiering documents</td>
<td width="156">2,500—8000/daily</td>
<td width="282">Proposed solution is able to process the average of between 2500-8000 daily cashiering transactions, based on current usage. It is expected that Cook County will provide the necessary upgrades if the number of daily transactions unexpectedly spike or exceed this expected usage.</td>
</tr>
<tr>
<td width="192">e-commerce (web) purchases\receipts</td>
<td width="156">1,400/daily

(see end of table for volume summary for 3+ months)</td>
<td width="282">Proposed solution is able to process  1,400/daily web transactions, based on current usage. It is expected that Cook County will provide the necessary upgrades if the web capacity unexpected spike or  exceeds this expected usage.</td>
</tr>
<tr>
<td width="192">Indexing documents</td>
<td width="156">2,400+/daily</td>
<td width="282">Proposed solution is able to p rocess 2,400/daily documents indexed, based on current usage. It is expected that Cook County will provide the necessary upgrades if the number of documents to index has unexpected spikes or exceeds this expected usage.</td>
</tr>
<tr>
<td width="192">Lookups and searches (web)</td>
<td width="156">50,000--100,000+ hits/daily</td>
<td width="282">Proposed solution is able to process the average of 50,000 – 100,000 daily web hits, based on current usage. It is expected that Cook County will provide the necessary upgrades if the number of daily web hits unexpectedly spike or exceeds this expected usage.</td>
</tr>
<tr>
<td width="192">Network wise, server wise.</td>
<td width="156">1,500 to 3,000 a day</td>
<td width="282">System specifications are able to manage between 1,500 – 3,000 transactions by internal users, based on current usage. It is expected that Cook County will provide the necessary upgrades if the number of transactions increases.</td>
</tr>
<tr>
<td width="192">Running 4 morning processing threads</td>
<td width="156">1.1. to 1.3 gigs per thread.</td>
<td width="282">Proposed solution is able to maintain a processing threads with 1.1 – 1.3 gigs per thread, based on current usage. It is expected that Cook County will provide the necessary upgrades the volume increases such that additional threads are necessary to maintain this expected load.</td>
</tr>
<tr>
<td width="192">Minimal latency when returning search results: for either online or local search.</td>
<td width="156">1 to 3 seconds</td>
<td width="282">Proposed solution is able to maintain minimal latency of 1-3 seconds, based on current usage. It is expected that Cook County will provide the necessary upgrades if the latency for search results increases based on deficiencies outside control of AgileFlow Records Management.</td>
</tr>
<tr>
<td colspan="2" width="348">&nbsp;</td>
<td width="282">&nbsp;</td>
</tr>
<tr>
<td colspan="3" width="630"><strong>System Uptime </strong>

SYSTEM uptime shall be 99.9% availability for all key functions of the SYSTEM applications on a 24 hour per day, 7 days a week basis.  The COUNTY in consultation with CONTRACTOR has authority to make the final determination of whether the components of the System meet specifications and performance standards listed in this section. <strong>Note: </strong>This does not apply to standard maintenance windows or preplanned downtime.<strong> (From </strong><strong>APPENDIX A)</strong>

&nbsp;</td>
</tr>
<tr>
<td width="192">Activity</td>
<td width="156">Metric</td>
<td width="282">AFRM response</td>
</tr>
<tr>
<td width="192">The system must return a complete, recorded image of the document (as recorded) to the submitter

&nbsp;</td>
<td width="156">3-5 seconds from recording</td>
<td width="282"><strong>Does solution meet these metrics?</strong></td>
</tr>
<tr>
<td colspan="2" width="348">&nbsp;</td>
<td width="282">&nbsp;</td>
</tr>
<tr>
<td colspan="3" width="630"><strong>Bandwidth Consumption </strong>

The proposed solution must effectively use bandwidth between system architecture tiers as Internet, Intranet and Extranet users/partners may have limited connectivity. Our slowest connection is at our service center which is connected via 3 T1s. The solution must effectively utilize bandwidth.

<strong>(From </strong><strong>APPENDIX A)</strong>

&nbsp;</td>
</tr>
<tr>
<td width="192">Activity</td>
<td width="156">Metric</td>
<td width="282">AFRM response</td>
</tr>
<tr>
<td width="192">Queries must typically be executed against tables referencing millions of documents</td>
<td width="156">Product:

·       minimizes bandwidth,

·       uses small packets of data wherever possible,

·       gets data only when the user actually navigates to that information</td>
<td width="282"><strong>Does solution meet these metrics?</strong></td>
</tr>
</tbody>
</table>
&nbsp;
