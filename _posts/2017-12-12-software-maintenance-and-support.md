---
layout: post
title: Software Maintenance and Support
date: 2017-12-12 12:11
author: tmasabari
comments: true
categories: [Architecture, Estimation, Estimation, Maintenance, Maintenance, Software, Software]
---
<h2>Introduction</h2>
This article is a collection of notes and references from other web sites for the self study of Single Page Applications and Angular. The list of source web sites referred are mentioned in the “References” section of this article.
<h2>Background</h2>
<span style="font-family: georgia, palatino, serif;"><em>“Begin with the end in mind”</em></span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">Maintenance and support will continue for the life of your software system. A significant portion of the system’s life-cycle budget will be consumed by these tasks. In fact, experts estimate that Maintenance can eventually account for 40 to 80% of the total project cost. </span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Software does not <strong>“wear out” but it will become less useful</strong> as it gets older, plus there WILL always be issues within the software itself.</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Software maintenance cost is derived from the changes made to software after it has been delivered to the end user.</span></li>
</ul>
&nbsp;
<div class="av-special-heading av-special-heading-h3 avia-builder-el-6 el_before_av_textblock avia-builder-el-first">
<h3 class="av-special-heading-tag"><span style="font-family: georgia, palatino, serif;">What is Maintenance?</span></h3>
<div class="special-heading-border">
<div class="special-heading-inner-border">

&nbsp;

</div>
</div>
</div>
<section class="av_textblock_section">
<div class="avia_textblock">

<span style="font-family: georgia, palatino, serif;">This phase of the software lifecycle consists of the tasks required to keep your system operational after it is delivered into Production.</span>

&nbsp;

<span style="font-family: georgia, palatino, serif;">The different types of maintenance tasks are described as:</span>
<ol>
 	<li><span style="font-family: georgia, palatino, serif;">Corrective – Updates that are required to <strong>correct or fix problems</strong>. (generally 20% of software maintenance costs)</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Perfective – Modifications that enhance or improve the <strong>functionality or performance</strong> of the software. This <strong>includes new user requirements.</strong> – costs due to <strong>improving or enhancing a software</strong> solution to improve overall performance (generally 5% of software maintenance costs)</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Adaptive – Software modifications that are required due to <strong>environmental changes</strong> (eg. upgrade to operating system) – costs due to <strong>modifying a software solution</strong> to allow it to <strong>remain effective</strong> in a changing business environment (25% of software maintenance costs)</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Preventative – This corrects potential flaws or problems in the software before they become effective.</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Enhancements – costs due to <strong>continuing innovations</strong> (generally 50% or more of software maintenance costs) Same as Perfective ?</span></li>
</ol>
</div>
</section><span style="color: #333333; font-family: georgia, palatino, serif; font-size: 20px; font-weight: bold; letter-spacing: 2px; text-transform: uppercase;">What is Support?</span>

<section class="av_textblock_section">
<div class="avia_textblock">

<span style="font-family: georgia, palatino, serif;">Support refers to the assistance given to users to address their problems and queries after system implementation.</span>

<span style="color: #333333; font-family: georgia, palatino, serif; font-size: 20px; font-weight: bold; letter-spacing: 2px; text-transform: uppercase;">Effort Estimation</span>

</div>
</section><section class="av_textblock_section">
<div class="avia_textblock">

<span style="font-family: georgia, palatino, serif;">Key parameters considered while estimating the efforts required are as below</span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">The industry and application type</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Size of the application</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Platform Types.</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Programming language used</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Effort spent on different maintenance activities</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Effort spent on different support activities</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">The number and types of defects found during the maintenance period</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Average time is taken to repair defects</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Calls to Help Desk</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Team size</span></li>
</ul>
</div>
<span style="color: #333333; font-family: georgia, palatino, serif; font-size: 20px; font-weight: bold; letter-spacing: 2px; text-transform: uppercase;">Approaches to take over projects in production</span>
<h4><a style="font-family: georgia, palatino, serif;" href="https://en.wikipedia.org/wiki/Requirements_elicitation">Requirement Elicitation</a></h4>
<div class="avia_textblock">
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">The term elicitation is used in books and research to raise the fact that good requirements cannot just be collected from the customer, as would be indicated by the name requirements gathering. Requirements elicitation is non-trivial because you can never be sure you get all requirements from the user and customer by just asking them what the system should do OR NOT do (for Safety and Reliability). Requirements elicitation practices include interviews, questionnaires, user observation, workshops, <a title="Brainstorming" href="https://en.wikipedia.org/wiki/Brainstorming">brainstorming</a>, <a class="mw-redirect" title="Use cases" href="https://en.wikipedia.org/wiki/Use_cases">use cases</a>, role playing and <a title="Software prototyping" href="https://en.wikipedia.org/wiki/Software_prototyping">prototyping</a></span></li>
</ul>
<h4><span style="font-family: georgia, palatino, serif;"><b>Detect patterns and the general structure of an application at a high level</b></span></h4>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;"><strong>Reverse analysis the source code</strong></span>

<span style="font-family: georgia, palatino, serif;">The architecture tools and Static Code Analysis in Visual Studio Ultimate help us to visualize the organization, relationships, design patterns and behavior of existing applications</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Generate sequence diagrams from the existing code and get required interfaces for each component</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Sequence diagrams help to asses the impact of changes</span></li>
</ul>
<h4><span style="font-family: georgia, palatino, serif;"><b>Improve productivity and quality through Automation</b></span></h4>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">Automated Live Unit Testing with VS</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Automatically runs the impacted unit tests in the background as you type and provides real-time feedback</span></li>
</ul>
<span style="font-family: georgia, palatino, serif;"><strong>Use Agile or Iterative Waterfall SDLC</strong></span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">Produces working software early during the lifecycle</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">The focus is on delivering a sprint of work</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">Deliver series of valuable/shippable features/projects</span></li>
 	<li><span style="font-family: georgia, palatino, serif;"><b>Low</b><b>risk </b></span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">Low risks factors as the risks can be identified and resolved during each iteration.</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">if one project goes wrong, it would not impact another project</span></li>
</ul>
</li>
 	<li><b style="font-family: georgia, palatino, serif;">Flexible</b>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">More flexible as scope and requirement changes can be implemented at low cost</span></li>
</ul>
</li>
</ul>
</div>
</section><section class="av_textblock_section"><span style="font-family: georgia, palatino, serif;"><strong>Questions / Metrics to be clarified</strong></span>
<ol>
 	<li><span style="font-family: georgia, palatino, serif;">Size of each application or module</span></li>
</ol>
<table width="955">
<tbody>
<tr style="height: 15.1042px;">
<td style="height: 15.1042px;">Application</td>
<td style="height: 15.1042px;">Number of Modules</td>
<td style="height: 15.1042px;">Number of

Screens

&nbsp;</td>
<td style="height: 15.1042px;" width="107">Number of  Scheduled Batches</td>
<td style="height: 15.1042px;" width="144">Number of  Integrations to External applications</td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">The number and types of defects found in a year</span>
<table style="width: 447.333px;">
<tbody>
<tr>
<td style="width: 100px;"><span style="font-family: georgia, palatino, serif;">Classification</span></td>
<td style="width: 170px;"><span style="font-family: georgia, palatino, serif;">Priority</span></td>
<td style="width: 158.333px;"><span style="font-family: georgia, palatino, serif;"><strong>No of issues found</strong></span></td>
</tr>
<tr>
<td style="width: 100px;" rowspan="4"><span style="font-family: georgia, palatino, serif;">Standard</span></td>
<td style="width: 170px;"><span style="font-family: georgia, palatino, serif;"><strong>Critical (P1)</strong></span></td>
</tr>
<tr>
<td style="width: 170px;"><span style="font-family: georgia, palatino, serif;"><strong>High (P2)</strong></span></td>
</tr>
<tr>
<td style="width: 170px;"><span style="font-family: georgia, palatino, serif;"><strong>Medium (P3) </strong></span></td>
</tr>
<tr>
<td style="width: 170px;"><span style="font-family: georgia, palatino, serif;"><strong>Low (P4) </strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">List of different .NET languages, Databases used with the applications.</span>
<table>
<tbody>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Technology / Languages</strong></span></td>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Number of applications</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>C#</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>VB. NET</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>SQL Server</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Oracle</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>MySQL</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>NoSQL</strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">List of different .NET frameworks used with the applications.</span>
<table>
<tbody>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Technology / Languages</strong></span></td>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Number of applications</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>ASP.NET – Web Forms</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>ASP.NET – MVC</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>WinForms</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>WPF</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>WebAPI</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>WCF</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>SingalR</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Entity Framework</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>NHibernate</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Angular</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Any other technologies</strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">Third-party applications or packages integrated with the applications</span>
<table>
<tbody>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Third Party integrations</strong></span></td>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Number of applications</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>CRM (Siebel, Vantive, Remedy, SharePoint, Documentum etc.) </strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>BI / OLAP / DW Tools</strong></span>

<span style="font-family: georgia, palatino, serif;"><strong>(ETL, Data Stage, Sagent, Informatica, </strong></span>

<span style="font-family: georgia, palatino, serif;"><strong>SAS, Ab Initio)</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>ERP Skills (Peoplesoft, SAP,</strong></span>

<span style="font-family: georgia, palatino, serif;"><strong>Oracle Applications etc.)</strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">Software development life cycle models used</span>
<table>
<tbody>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>SDLC</strong></span></td>
<td width="178"><span style="font-family: georgia, palatino, serif;"><strong>Number of applications</strong></span></td>
<td width="178"><span style="font-family: georgia, palatino, serif;"><strong>Number of releases in a year</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Waterfall</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Iterative Waterfall</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Agile</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Any other SDLC methods</strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">Type of Integration and deployment methods used (to estimate the efforts to deliver the build to different environments</span>
<table>
<tbody>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Integration and Deployment</strong></span></td>
<td width="178"><span style="font-family: georgia, palatino, serif;"><strong>Number of applications</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>CI/CD </strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Automated deployments only</strong></span></td>
</tr>
<tr>
<td width="319"><span style="font-family: georgia, palatino, serif;"><strong>Manual Integration and deployment</strong></span></td>
</tr>
</tbody>
</table>
<span style="font-family: georgia, palatino, serif;">Availability of the documents in English </span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">Architecture documents, HLD, LLD, User guides, deployment documents etc</span></li>
</ul>
</section>
<h3><span style="font-family: georgia, palatino, serif;">References</span></h3>
<section class="av_textblock_section">
<div class="avia_textblock">
<ol>
 	<li><span style="font-family: georgia, palatino, serif;">https://files.ifi.uzh.ch/rerg/arvo/courses/seminar_ws02/reports/Seminar_9.pdf</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">https://gupea.ub.gu.se/bitstream/2077/10553/1/gupea_2077_10553_1.pdf</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">https://www.slideshare.net/anandsubramaniam/project-metrics-measures</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">http://isbsg.org/maintenance-support/</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">SDLC Models</span>
<ul>
 	<li><span style="font-family: georgia, palatino, serif;">https://www.itproportal.com/2010/07/04/comparison-various-software-development-life-cycle/</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=32B2FE647EC4C6DF095FC1D671C4A24A?doi=10.1.1.667.9896&amp;rep=rep1&amp;type=pdf</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">http://www.agilistapm.com/differences-between-waterfall-iterative-waterfall-scrum-and-lean-software-development-in-pictures/</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">https://www.mountaingoatsoftware.com/blog/an-iterative-waterfall-isnt-agile</span></li>
</ul>
</li>
 	<li><span style="font-family: georgia, palatino, serif;">Visual Studio Architecture Tooling Guide Scenarios </span>
<ol>
 	<li><span style="font-family: georgia, palatino, serif;">https://blogs.msdn.microsoft.com/visualstudioalmrangers/2015/04/22/library-of-tooling-and-guidance-solutions-aka-msvsarsolutions/</span></li>
 	<li><span style="font-family: georgia, palatino, serif;">https://vsardata.blob.core.windows.net/projects/Visual%20Studio%20Architecture%20Tooling%20Guide%20-%20Scenarios.pdf </span></li>
</ol>
</li>
</ol>
</div>
</section>
