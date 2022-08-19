---
layout: post
title: Availability & Performance - Regions, AZ, Edge locations
date: 2018-03-26 09:35
author: tmasabari
comments: true
categories: [Uncategorized]
---
<h3>Availability</h3>
<h4>Region</h4>
<ol>
 	<li>Each Amazon EC2 region is designed to be completely isolated from each other</li>
 	<li>we don't replicate resources across regions automatically</li>
 	<li>Note that there is a charge for data transfer between regions.</li>
 	<li>at least have 2 AZ / data center</li>
 	<li>physically separated from each other</li>
 	<li>connected by high speed/low latency connection</li>
 	<li>price of services/usage vary based up on region</li>
 	<li class="listitem">An AWS GovCloud (US) account provides access to the AWS GovCloud (US) region only. For more information, see <a href="https://aws.amazon.com/govcloud-us/" target="_blank" rel="noopener">AWS GovCloud (US) Region</a>.</li>
 	<li class="listitem">An Amazon AWS (China) account provides access to the China (Beijing) region only.</li>
</ol>
<h4>Availability zone</h4>
<ul>
 	<li>isolated location with single or multiple advanced data centers
<ul>
 	<li>distribute their computing resources among several tier 1 internet service and power providers</li>
</ul>
</li>
 	<li> If you distribute your instances across multiple Availability Zones and one instance fails, you can design your application so that an instance in another Availability Zone can handle requests.</li>
 	<li>An Availability Zone is represented by a region code followed by a letter identifier; for example, <code class="code">us-east-1a</code>.</li>
 	<li>at least sets up more than one data center in a city</li>
 	<li>There can be a charge to move data between Azones.</li>
</ul>
<h4><a href="https://aws.amazon.com/cloudfront/details/">Edge location</a></h4>
<ul>
 	<li>located in major cities distribute content to end users</li>
 	<li>reduce latency</li>
 	<li>CDN of amazon</li>
 	<li>support static</li>
 	<li>support dynamic content as well
<ul>
 	<li>data cache</li>
 	<li>url output cache</li>
</ul>
</li>
 	<li>edge Servers - caching servers</li>
 	<li>edge city</li>
</ul>
<h5>Amazon CloudFront</h5>
<ul>
 	<li>economical dynamic CDN. delivers both static, streaming and dynamic</li>
 	<li>Not cached data
<ul>
 	<li>amazon continuously connected with servers and makes sure contents delivered immediately</li>
</ul>
</li>
 	<li>ability to scale according to requirements
<ul>
 	<li>start small and grow as the traffic increases</li>
 	<li>automatically manages the load without user intervention</li>
</ul>
</li>
 	<li>flexible cost model
<ul>
 	<li>no fixed term monthly commitment or fixed contract</li>
 	<li>pay for the delivered content</li>
</ul>
</li>
 	<li>114 Points of Presence (103 Edge Locations and 11 Regional Edge Caches) in 56 cities across 24 countries</li>
 	<li><b>Dynamic and Customized Content</b>
<ul>
 	<li>With CloudFront, you can configure <strong>multiple origin servers and multiple cache behaviors</strong> based on <strong>URL path patterns</strong> on your website. You can also configure a minimum expiration period (also known as <strong>“time-to-live” or TTL</strong>) to as short as 0 seconds, detect user requests based on the <strong>device used</strong> and the <strong>country</strong> where the end user is accessing your content from (<strong>geo targeting</strong>), and specify which <strong>query string parameters, cookies, or standard HTTP request headers</strong> you want to forward to your custom (non-S3) origin server.</li>
 	<li>In addition, the integration with <a href="https://aws.amazon.com/lambda/edge/">Lambda@Edge</a> allows you to customize or personalize content for your end users close to where they’re located by writing <a href="https://aws.amazon.com/lambda/details/">AWS Lambda</a> functions deployed to the global CloudFront network and execute these functions in response to CloudFront events.</li>
</ul>
</li>
 	<li><b>Streaming Features</b>
<ul>
 	<li>supports multiple protocols for media (audio and video – both on-demand and live) streaming</li>
 	<li>deliver live media using Adobe Media Server, Window Media Services, or Wowza Media Server</li>
 	<li> <a href="https://aws.amazon.com/elastictranscoder/details/">Amazon Elastic Transcoder</a>, a service that allows you to convert your mezzanine (or master) media files stored in <a href="https://aws.amazon.com/s3/">Amazon S3</a> to various formats depending on the devices your viewers will be using to play it</li>
</ul>
</li>
 	<li><b>Reporting and Analytics</b>
<ul>
 	<li>monitoring your CloudFront usage in near real-time with <a href="https://aws.amazon.com/cloudwatch/">Amazon CloudWatch</a>,</li>
 	<li>tracking your most popular objects,</li>
 	<li>setting alarms on operational metrics, or</li>
 	<li>learning more about your end users and which domains referred them to your website.</li>
 	<li>You can also choose to receive information about traffic delivered by your CloudFront distribution by enabling CloudFront access logs for <strong>no additional cost</strong>.</li>
</ul>
</li>
 	<li><b>Security Features</b>
<ul>
 	<li>enforce end-to-end HTTPS connections from your viewer to your origin</li>
 	<li>The integration between CloudFront and <strong><a href="https://aws.amazon.com/certificate-manager/">AWS Certificate Manager</a> allows you to create free custom SSL certificates</strong> or <strong>bring your own</strong> and deploy them in minutes.</li>
 	<li>CloudFront also integrates with <a href="https://aws.amazon.com/waf/">AWS WAF</a>, a web application firewall that helps protect web applications from common web exploits, and</li>
 	<li><a href="https://aws.amazon.com/shield/">AWS Shield</a>, a managed DDoS protection service that safeguards web applications running on AWS.</li>
 	<li>All CloudFront customers benefit from the <strong>automatic protections of AWS Shield Standard, at no additional charge</strong>.</li>
 	<li>CloudFront is a PCI DSS compliant and <a href="https://aws.amazon.com/compliance/hipaa-compliance/">HIPAA eligible service</a> and allows you to log configuration changes to your distributions through <a href="https://aws.amazon.com/cloudtrail/">AWS CloudTrail</a> for auditing purposes.</li>
</ul>
</li>
</ul>
