---
layout: post
title: GSA Solr ElasticSearch
date: 2018-08-21 15:42
author: tmasabari
comments: true
categories: [Enterprise Search]
---
<a href="https://findwise.com/blog/google-search-appliance-migration-in-4-steps/">https://findwise.com/blog/google-search-appliance-migration-in-4-steps/</a>

<strong>Google Search Appliance features equivalence</strong>
<table>
<tbody>
<tr>
<th>GSA FEATURE</th>
<th>ELASTICSEARCH</th>
<th>APACHE SOLR</th>
</tr>
<tr>
<td>Web crawling</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>Language Bundles</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/language-intro.html">Languages</a></td>
<td><a href="https://cwiki.apache.org/confluence/display/solr/Language+Analysis">Language Analysis</a></td>
</tr>
<tr>
<td>Synonyms</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/using-synonyms.html">Synonyms</a></td>
<td><a href="https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters">Synonyms</a></td>
</tr>
<tr>
<td>Stopwords</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/using-stopwords.html">Stopwords</a></td>
<td><a href="https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters">Stopwords</a></td>
</tr>
<tr>
<td>Result Biasing</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/controlling-relevance.html">Controlling relevance</a></td>
<td><a href="https://cwiki.apache.org/confluence/display/solr/The+Query+Elevation+Component">Query elevation</a></td>
</tr>
<tr>
<td>Suggestions</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-suggesters.html">Search-suggesters</a></td>
<td><a href="https://cwiki.apache.org/confluence/display/solr/Suggester">Suggester</a></td>
</tr>
<tr>
<td>Dynamic navigation</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html">Aggregations</a></td>
<td><a href="https://cwiki.apache.org/confluence/display/solr/Faceting">Faceting</a></td>
</tr>
<tr>
<td>Document preview</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>User result</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>Expert search</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>Keymatch</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>Related Queries</td>
<td>X</td>
<td>X</td>
</tr>
<tr>
<td>Secure search</td>
<td><a href="https://www.elastic.co/products/shield">Shield</a></td>
<td><a href="https://wiki.apache.org/solr/SolrSecurity">Solr Security</a></td>
</tr>
<tr>
<td>Search reports</td>
<td><a href="https://www.elastic.co/products/logstash">Logstash</a>+<a href="https://www.elastic.co/products/kibana">Kibana</a></td>
<td>X</td>
</tr>
<tr>
<td>Mirroring/Distributed</td>
<td><a href="https://www.elastic.co/guide/en/elasticsearch/guide/current/scale.html">Scale Elastic</a></td>
<td><a href="https://cwiki.apache.org/confluence/display/solr/SolrCloud">Solr Cloud</a></td>
</tr>
<tr>
<td>System alert</td>
<td><a href="https://www.elastic.co/products/watcher">Watcher</a></td>
<td>X</td>
</tr>
<tr>
<td>Email update/Alert</td>
<td><a href="https://www.elastic.co/products/watcher">Watcher</a></td>
<td>X</td>
</tr>
</tbody>
</table>
X = not available outside of the box
<h2 class="secthead">Resources</h2>
<ul>
 	<li>My other sites may be of interest if you're new to Lucene, Solr and Elasticsearch:
<ul>
 	<li><a href="http://www.lucenetutorial.com/">Lucene Tutorial</a></li>
 	<li><a href="http://www.elasticsearchtutorial.com/">Elasticsearch Tutorial</a></li>
 	<li><a href="http://www.solrtutorial.com/">Solr Tutorial</a></li>
</ul>
</li>
 	<li>The <a href="http://wiki.apache.org/solr">Solr wiki</a> and the <a href="http://www.elasticsearch.org/guide">Elasticsearch Guide</a> are your friends.</li>
 	<li><a href="https://support.google.com/gsa">https://support.google.com/gsa</a></li>
</ul>
<a href="https://stackoverflow.com/questions/10213009/solr-vs-elasticsearch">https://stackoverflow.com/questions/10213009/solr-vs-elasticsearch</a>

<a href="https://www.slant.co/versus/355/358/~solr_vs_elasticsearch">https://www.slant.co/versus/355/358/~solr_vs_elasticsearch</a>

<a href="http://solr-vs-elasticsearch.com/">http://solr-vs-elasticsearch.com/</a> latest

<a href="https://thishosting.rocks/comparing-elasticsearch-with-solr/">https://thishosting.rocks/comparing-elasticsearch-with-solr/</a>
<h3>Choose Solr if any of the following are true...</h3>
&nbsp;
<ul>
 	<li>If your <strong>data is largely immutable</strong>, and high performance along with accuracy are a priority, Solr may be the better choice for you. In tests, <strong>Solr proved to outdo Elasticsearch</strong> in this area. There is little to no degradation in Solr thanks to the fact that there is no loss of precision.</li>
 	<li>Your team consists mainly of Java programmers</li>
 	<li>You're already using ZooKeeper in your stack</li>
 	<li>You're already using Java in your stack</li>
 	<li>You are building a search application that has specific and nuanced relevancy requirements</li>
 	<li>You are building an ecommerce, job, or product search engine</li>
 	<li>Search is a central part of your product and user experience and there is the <strong>organizational mandate for search</strong> to be a core strength</li>
 	<li>A scalable, reliable, and open source <strong>search platform</strong> that leverages that capabilities of Apache Lucene and other projects and tools from Apache to boost the search performance of highly-trafficked websites and applications across the world.</li>
</ul>
&nbsp;
<h3>Choose Elasticsearch if any of the following are true...</h3>
&nbsp;
<ul>
 	<li>Your team consists mainly of Ruby/PHP/Python/full stack programmers (and your application does not have specific and nuanced relevancy requirements)</li>
 	<li>You live and breathe JSON</li>
 	<li>You already use Kibana/ELK for managing your logs</li>
 	<li>Your application is <strong>analytics-heavy</strong></li>
 	<li>Elasticsearch is a reliable open source <strong>search and analytics engine</strong> that is designed for reliability, easy management, and horizontal scalability.</li>
</ul>
<ul>
 	<li>Elasticsearch is more popular among newer developers due to its ease of use. But if you are already used to working with Solr, stay with it because there is no specific advantage of migrating to Elasticsearch</li>
</ul>
2016 <a href="https://www.hcltech.com/blogs/elasticsearch-vs-solr">https://www.hcltech.com/blogs/elasticsearch-vs-solr</a>

<a href="https://logz.io/blog/solr-vs-elasticsearch/">https://logz.io/blog/solr-vs-elasticsearch/</a>
<p id="CjNroFF"><img class="alignnone size-full wp-image-1716 " src="/wp-content/uploads/2018/08/img_5b7beb09e5e20.png" alt="" /></p>

<h3>Quick Comparison</h3>
Elasticsearch, unlike Solr was built with distribution in mind, to be EC2-friendly, meaning that Elasticsearch runs a search index on multiple servers, in a fail-safe and efficient way, and that’s quite a challenge.

ElasticSearch has been designed with the cloud era in mind. Even though some steps to make Solr cloud-ready have been taken, its initial architecture and design do not include it, so it will take more time to get Solr where Elasticsearch is out-of-the-box. Performance-wise, they are roughly the same. Operationally, Elasticsearch is a bit simpler to work with, it has just a single process. Solr, in its Elasticsearch-like fully distributed deployment mode known as SolrCloud, depends on Apache ZooKeeper. If you love monitoring and metrics, then Elasticsearch is the best choice. Notable users of Elasticsearch include Wikimedia, Facebook, StumbleUpon, Mozilla, Amadeus IT Group, Quora, Foursquare, Etsy, SoundCloud, GitHub, FDA, CERN, Stack Exchange, and Netflix.
<h2>Conclusion</h2>
Solr is search server for creating standard search applications, no massive indexing and no real time updates are required, but on the other hand Elasticsearch takes it to the next level with an architecture aimed at building modern real-time search applications. Percolation is an exciting and innovative feature. Elasticsearch is scalable and speedy, and if distributed indexing is needed then Elasticsearch would be the right choice.

If you’ve already invested a lot of time in Solr, stick with it, unless there are specific use cases that it just doesn’t handle well.

&nbsp;
<ul>
 	<li>Community: Solr has a bigger, more mature user, dev, and contributor community. ES has a smaller, but active community of users and a growing community of contributors</li>
 	<li>Maturity: Solr is more mature, but ES has grown rapidly and I consider it stable</li>
 	<li>Scalability: both can be scaled to very large clusters. ES is easier to scale than pre-Solr 4.0 version of Solr, but with Solr 4.0 that's no longer the case.</li>
 	<li>Performance: ElasticSearch had 13% higher throughput when it came to indexing documents but Solr was ten times faster. When it came to querying for documents, Solr had five times more throughput and was five times faster than ElasticSearch.</li>
 	<li><strong>Solr</strong> may be the weapon of choice when building <strong>standard search applications</strong>, but <strong>Elasticsearch</strong> takes it to the next level with an <strong>architecture for creating modern realtime search applications</strong>. Percolation is an exciting and innovative feature that singlehandedly blows Solr right out of the water. <strong>Elasticsearch is scalable, speedy and a dream to integrate with</strong>.</li>
 	<li>Solr added below features around 2016: 1) SolrCloud is no longer a separate project. Indeed, Solr and Lucene are now part of the same project. 2) Solr supports near real-time search of Apache Lucene. 3) Solr handles multiple collections in a single cluster 4) Solr also has added a replication feature which makes backups easier.</li>
</ul>
2018 https://sematext.com/blog/solr-vs-elasticsearch-differences/
<p class="selectionShareable">Both Solr and Elasticsearch are evolving rapidly so, without further ado, here is up to date information about their top differences.</p>

<table>
<tbody>
<tr>
<td>
<h3><b>Feature</b></h3>
</td>
<td>
<h3><b>Solr/SolrCloud</b></h3>
</td>
<td>
<h3><b>Elasticsearch</b></h3>
</td>
</tr>
<tr>
<td><strong>Community &amp; Developers</strong></td>
<td>Apache Software Foundation and community support</td>
<td>Single commercial entity and its employees</td>
</tr>
<tr>
<td><strong>Node Discovery</strong></td>
<td>Apache Zookeeper, mature and battle-tested in a large number of projects</td>
<td>Zen, built into Elasticsearch itself, requires dedicated master nodes to be split brain proof</td>
</tr>
<tr>
<td><strong>Shard Placement</strong></td>
<td>Static in nature, requires manual work to migrate shards, starting from Solr 7 – Autoscaling API allows for some dynamic actions</td>
<td>Dynamic, shards can be moved on demand depending on the cluster state</td>
</tr>
<tr>
<td><strong>Caches</strong></td>
<td>Global, invalidated with each segment change</td>
<td>Per segment, better for dynamically changing data</td>
</tr>
<tr>
<td><strong>Analytics Engine</strong></td>
<td>Facets and powerful streaming aggregations</td>
<td>Sophisticated and highly flexible aggregations</td>
</tr>
<tr>
<td><strong>Optimized Query Execution</strong></td>
<td>Currently none</td>
<td>Faster range queries depending on the context</td>
</tr>
<tr>
<td><strong>Search Speed</strong></td>
<td>Best for static data, because of caches and uninverted reader</td>
<td>Very good for rapidly changing data, because of per-segment caches</td>
</tr>
<tr>
<td><strong>Analysis Engine Performance</strong></td>
<td>Great for static data with exact calculations</td>
<td>Exactness of the results depends on data placement</td>
</tr>
<tr>
<td><strong>Full Text Search Features</strong></td>
<td>Language analysis based on Lucene, multiple suggesters, spell checkers, rich highlighting support</td>
<td>Language analysis based on Lucene, single suggest API implementation, highlighting rescoring</td>
</tr>
<tr>
<td><strong>DevOps Friendliness</strong></td>
<td>Not fully there yet, but coming</td>
<td>Very good APIs</td>
</tr>
<tr>
<td><strong>Non-flat Data Handling</strong></td>
<td>Nested documents and parent-child support</td>
<td>Natural support with nested and object types allowing for virtually endless nesting and parent-child support</td>
</tr>
<tr>
<td><strong>Query DSL</strong></td>
<td>JSON (limited), XML (limited) or URL parameters</td>
<td>JSON</td>
</tr>
<tr>
<td><strong>Index/Collection Leader Control</strong></td>
<td>Leader placement control and leader rebalancing possibility to even the load on the nodes</td>
<td>Not possible</td>
</tr>
<tr>
<td><strong>Machine Learning</strong></td>
<td>Built-in – on top of streaming aggregations focused on logistic regression and learning to rank contrib module</td>
<td>Commercial feature, focused on anomalies and outliers and time-series data</td>
</tr>
<tr>
<td><strong>Ecosystem</strong></td>
<td>Modest – Banana, Zeppelin with community support</td>
<td>Rich – Kibana, Grafana, with large entities support and big user base</td>
</tr>
</tbody>
</table>
<a href="http://manmustbecool.github.io/MyWiki/papers/Enterprise%20search%20with%20development%20for%20network%20management%20system.pdf">http://manmustbecool.github.io/MyWiki/papers/Enterprise%20search%20with%20development%20for%20network%20management%20system.pdf</a>
<ul>
 	<li>Enterprise search vs RDBMS paper</li>
 	<li>Solr full stack explanation</li>
</ul>
2016 update <a href="https://stackoverflow.com/questions/10213009/solr-vs-elasticsearch">https://stackoverflow.com/questions/10213009/solr-vs-elasticsearch</a>

&nbsp;
<p id="EtzkCnG"><img class="alignnone size-full wp-image-1711 " src="/wp-content/uploads/2018/08/img_5b7be2335ae1c.png" alt="" /></p>
Solr ecosystem

&nbsp;
<p id="bHlhiah"><img class="alignnone wp-image-1712 " src="/wp-content/uploads/2018/08/img_5b7be2df25dc2.png" alt="" width="421" height="245" /></p>
<a href="https://comparisons.financesonline.com/apache-solr-vs-elasticsearch">https://comparisons.financesonline.com/apache-solr-vs-elasticsearch</a>
<table class="compare-table main-compare-table">
<tbody>
<tr id="compare-features" class="compare-row-grey">
<td class="compare-title compare-title-left" valign="top" data-td-id="1">
<div class="compare-td-wrap">
<div class="compare-td-wrap-cell">
<h2 class="normalize">Features</h2>
</div>
</div></td>
<td class="compare-td" data-td-id="2">
<div class="compare-td-wrap">
<div class="compare-td-wrap-cell">
<div class="compare-limit-box inactive">
<h4><a href="https://reviews.financesonline.com/p/apache-solr/">Apache Solr FEATURES</a></h4>
<ul class="tick-list">
 	<li>Schema when you want, schemaless when you don’t</li>
 	<li>Dynamic Fields</li>
 	<li>Field Types</li>
 	<li>Copy Field Capabilities</li>
 	<li>Advanced Configurable Text Analysis</li>
 	<li>Powerful Relevance Tuning Capabilities</li>
 	<li>Multiple Approaches to Query Parsing</li>
 	<li>Near Real-Time Indexing</li>
 	<li>Pivot Faceting</li>
 	<li>Range Faceting</li>
 	<li>Multi-Select Facet Parameters</li>
 	<li>Content Discovery</li>
 	<li>Dynamic Search Results Clustering</li>
 	<li>Typeahead,</li>
 	<li>Autocomplete,</li>
 	<li>Auto-suggest</li>
 	<li>Spelling Suggestions</li>
 	<li>Hint Highlighting</li>
 	<li>Location-Aware Search</li>
 	<li>Spatial Integration</li>
 	<li>Rich Content</li>
 	<li>Manage a Variety of Data Types</li>
 	<li>Apache Tika Integration</li>
 	<li>Flexible and Extensible Input and Output Formats</li>
 	<li>Single-Node and Distributed Capabilities</li>
 	<li>Smart Caching</li>
 	<li>Performance Tuning</li>
 	<li>Scaling</li>
 	<li>Advanced Transaction log, Replication and Failover</li>
 	<li>Shard Splitting</li>
 	<li>Admin Interface</li>
 	<li>Open Source and Open Development</li>
 	<li>Plugins and Extensions</li>
</ul>
</div>
<button class="btn btn-default btn-sm pull-right limit-box-button" type="button" data-max-height="150px">Show Less</button>

</div>
</div></td>
<td class="compare-td" data-td-id="3">
<div class="compare-td-wrap">
<div class="compare-td-wrap-cell">
<div class="compare-limit-box inactive">
<h4><a href="https://reviews.financesonline.com/p/elasticsearch/">Elasticsearch FEATURES</a></h4>
<ul class="tick-list">
 	<li>Query</li>
 	<li>Analyze</li>
 	<li>Monitoring</li>
 	<li>Management</li>
 	<li>Security</li>
 	<li>Reporting</li>
 	<li>Machine learning</li>
 	<li>Alerting</li>
 	<li>Scalability</li>
 	<li>Client libraries</li>
</ul>
</div>
</div>
</div></td>
</tr>
</tbody>
</table>
