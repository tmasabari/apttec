---
layout: post
title: Visual Studio with Report generator and SonarQube
date: 2018-04-18 19:57
author: tmasabari
comments: true
categories: [Code Review, SonarQube, Testing]
---
Only Visual Studio 2015 Enterprise has code coverage built-in. See <a href="https://www.visualstudio.com/en-us/compare-visual-studio-2015-products-vs.aspx" rel="noreferrer">the feature matrix</a> for details.

Report generator <a href="http://www.allenconway.net/2015/06/using-opencover-and-reportgenerator-to.html">http://www.allenconway.net/2015/06/using-opencover-and-reportgenerator-to.html</a>

You can use the <a href="https://visualstudiogallery.msdn.microsoft.com/6950a046-8919-4935-8542-c6f37956f688" rel="noreferrer">OpenCover.UI extension</a> for code coverage check inside Visual Studio. It supports MSTest, nUnit, and xUnit. <span style="font-size: 1rem;">opencover.UI (that is integrated with VS) has very messy report (results window) that is simply impossible to use. go to opencover directly</span>

<a href="https://stackoverflow.com/questions/32369664/does-visual-studio-have-code-coverage-for-unit-tests/42433925">https://stackoverflow.com/questions/32369664/does-visual-studio-have-code-coverage-for-unit-tests/42433925</a>
<h2>Introduction</h2>
<strong>Software quality measurement</strong> is a quantitative process summing up weighted attribute values, which in part describe specific software <em>characteristics</em>. For each <em>characteristic</em>, a set of such measurable attributes is defined.

What are <strong>software characteristics</strong>?
<ol>
 	<li>Whether  the coding has been done following a specific convention</li>
 	<li>Whether well-known/established good practices have been followed and well-known/established bad practices have been avoided</li>
 	<li>Are there any potential bugs and performance issues, security vulnerabilities</li>
 	<li>Is there any duplicate code</li>
 	<li>Is the code logic very complex</li>
 	<li>Whether the public API has good documentation and comments</li>
 	<li>Whether the code has unit tests</li>
 	<li>Whether the code follows good design and architecture principles</li>
</ol>
How do we define the corresponding attributes?
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="192"><strong>Attribute</strong></td>
<td valign="top" width="192"><strong>Weighted Value</strong></td>
</tr>
<tr>
<td valign="top" width="192">Blocker</td>
<td valign="top" width="192">5</td>
</tr>
<tr>
<td valign="top" width="192">Critical</td>
<td valign="top" width="192">4</td>
</tr>
<tr>
<td valign="top" width="192">Major</td>
<td valign="top" width="192">3</td>
</tr>
<tr>
<td valign="top" width="192">Minor</td>
<td valign="top" width="192">2</td>
</tr>
<tr>
<td valign="top" width="192">Info</td>
<td valign="top" width="192">1</td>
</tr>
</tbody>
</table>
<h1>Static Code Analysis</h1>
<strong> </strong>Static code analysis is a collection of algorithms and techniques used to analyze source code in order to automatically find potential errors or poor coding practices. The idea is similar in spirit to compiler warnings (which can be useful for finding coding errors), but to take that idea a step further and find bugs that are traditionally found using run-time debugging techniques such as testing.

Static code analysis, also commonly called "white-box" testing, looks at applications in non-runtime environments. It is the only proven method to cover the entire code base and identify all the vulnerable patterns. Static code analysis is also considered as a way to automate code review process.

The tasks solved by static code analysis software can be divided into 3 categories:
<ul>
 	<li>Detecting errors in programs</li>
 	<li>Recommendations on code formatting. Some static analyzers allow you to check if the source code corresponds to the code formatting standard accepted in your company</li>
 	<li>Metrics computation. Software metrics are a measure that lets you get a numerical value of some property of software or its specifications</li>
</ul>
<h1>SonarQube</h1>
<ul>
 	<li><strong> </strong>SonarQube collects and analyzes source code, measuring quality and providing reports for your projects.</li>
 	<li>It combines static and dynamic analysis tools and enables <strong>quality to be measured continuously over time.</strong></li>
 	<li>Everything that affects our code base, from minor styling details to critical design errors, is inspected and evaluated by SonarQube, thereby enabling developers to access and track code analysis data ranging from styling errors, potential bugs, and code defects to design inefficiencies, code duplication, lack of test coverage, and excess complexity.</li>
 	<li>The Sonar platform analyzes source code from different aspects and hence it drills down to your code layer by layer, moving from the module level down to the class level.</li>
 	<li>At each level, SonarQube <strong>produces metric values and statistics, revealing problematic areas</strong> in the source that require inspection or improvement.</li>
</ul>
<h3>Why SonarQube</h3>
You may wonder if SonarQube uses existing, proven, tools then why use it at all? You can just configure these tools as a plugin in the CI server and bang we will be done. Well not necessarily, well there are lots of caveats.
<ul>
 	<li>As of now, CI tools does not have a plugin which would make all these play together</li>
 	<li>As of now, CI tools does not have pugins to provide nice drill-down features as SonarQube does</li>
 	<li>CI plugins does not talk about overall compliance value</li>
 	<li>CI plugins does not provide managerial perspective</li>
 	<li>As of now there is no CI plugin for Design/Architecture issues</li>
 	<li>It does not provide a dashboard for overall projects quality</li>
</ul>
<h3>Features:</h3>
<ul>
 	<li>SonarQube doesn't just show you what's wrong. It also offers quality-management tools to actively help you put it right</li>
 	<li>SonarQube's commercial competitors seem to focus their definition of quality mainly on bugs and complexity, whereas SonarQube's offerings span what its creators call the Seven Axes of Quality</li>
 	<li>SonarQube addresses not just bugs but also coding rules, test coverage, duplications, API documentation, complexity, and architecture, providing all these details in a dashboard</li>
 	<li>It gives you a moment-in-time snapshot of your code quality today, as well as trends of lagging (what's already gone wrong) and leading (what's likely to go wrong in the future) quality indicators</li>
 	<li>It provides you with metrics to help you take right decision. In nearly every industry, serious leaders track metrics. Whether it's manufacturing defects and waste, sales and revenue, or baseball hits and RBIs, there are metrics that tell you how you're doing: if you're doing well overall, or whether you're getting better or worse.</li>
</ul>
What makes SonarQube really stand out is that it not only provides metrics and statistics about your code, but translates these non-descript values to real business values such as risk and technical debt. SonarQube not only addresses core developers and programmers but, project managers and even higher managerial levels due to the management aspect it offers. This concept is further strengthened by SonarQube's enhanced reporting capabilities and multiple views addressing source code from different perspectives.

From a managerial perspective, transparent and continuous access on historical data enables the manager to ask the right questions.

<strong>Note:</strong> SonarQube is in <strong>no way competing</strong> with any of the above static analysis tools, but rather it <strong>complements</strong> and works very well with these tools. In fact, it ceases to work if these static analysis tools (Checkstyle, PMD, and FindBugs) do not exist. Further, we can integrate Fortify with SonarQube using <a href="http://www.sonarsource.com/products/plugins/integration/fortify/" target="_blank" rel="nofollow noopener">this plugin</a>.
<h2>2 Minute installation</h2>
<h3 id="GetStartedinTwoMinutes-GetStartedinTwoMinutes">Get Started in Two Minutes</h3>
<ol>
 	<li>Go to <a title="_blank" href="http://www.sonarsource.com/products/editions/community-edition/" target="_blank" rel="nofollow noopener">Sonar community edition page</a> and download.</li>
 	<li>Unzip the downloaded file</li>
 	<li>Go to &lt;install_directory&gt;/bin folder. You would find different folders related with OS platforms. As I have 64 bit Win system, I further went inside “windows-x86-64″ folder.</li>
 	<li>Copy the path of this folder which may look like &lt;install_director&gt;/bin/Windows-x86-64 (in case of my laptop), and append it to “Path” environment variable.</li>
 	<li>Run below commands to start Sonarqube web server</li>
</ol>
<div class="code panel pdl conf-macro output-block" data-hasbody="true" data-macro-name="code">
<div class="codeContent panelContent pdl">
<div>
<div id="highlighter_790487" class="syntaxhighlighter sh-confluence nogutter plain">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td class="code">
<div class="container" title="Hint: double-click to select code">
<div class="line number1 index0 alt2"><code class="plain plain"># On Windows, execute:</code></div>
<div class="line number2 index1 alt1"><code class="plain plain">C:\sonarqube\bin\windows-x86-xx\StartSonar.bat</code></div>
<div class="line number3 index2 alt2"></div>
<div class="line number4 index3 alt1"><code class="plain plain"># On other operating system, execute:</code></div>
<div class="line number5 index4 alt2"><code class="plain plain">/etc/sonarqube/bin/[OS]/sonar.sh console</code></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
<ol>
 	<li>Log in to <a class="external-link" href="http://localhost:9000/" rel="nofollow">http://localhost:9000</a> with System Administrator credentials (admin/admin) and follow the tutorial to analyze your first project.</li>
 	<li>Sonar comes with an embedded H2 database, by default. For quick setup and testing purpose, you may live with embedded database.</li>
 	<li>However, for production and real usage, one may want to use production-read databases such as MySQL, Oracle etc. For configuration instructions, edit install_directory&gt;/conf/sonar.properties to configure the database settings. Templates are available for every supported database. Just uncomment and configure the template you need and comment out the lines dedicated to H2 database.</li>
</ol>
<h3 id="InstalltheSonarScannerforMSBuild-Installation">MSBuild integration</h3>
<ol>
 	<li><a href="https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild">Download SonarScanner for MSBuild</a>.</li>
 	<li>Unzip the downloaded file into a directory, for example <code>c:\sonarscanner-msbuild</code> on <strong>Windows</strong> or <code>~/sonarscanner-msbuild</code> on <strong>Linux/OSX</strong>. On <strong>Windows</strong>, you might need to unblock the ZIP file first (Right click on file -&gt; Properties -&gt; Unblock).</li>
 	<li>Set default analysis properties in <code>SonarQube.Analysis.xml</code> that is located in the folder where you unzipped the archive. Usually those would be:
<ol>
 	<li><code>sonar.host.url</code> - URL to SonarCloud / your SonarQube server</li>
 	<li><code>sonar.login</code> - <a href="https://docs.sonarqube.org/display/SONAR/User+Token" rel="nofollow">Analysis token</a> of an user with <a href="https://docs.sonarqube.org/display/SONARQUBE54/Authorization#Authorization-GlobalPermissions" rel="nofollow">Execute Analysis</a> permissions. Required only if Anonymous does not have them</li>
</ol>
</li>
 	<li>If you have added authentication properties into <code>SonarQube.Analysis.xml</code> we would advise to restrict the access to it by setting the appropriate file system permissions.</li>
 	<li>Add <code>c:\sonarscanner-msbuild</code> (or <code>~/sonarscanner-msbuild</code>) path to the system PATH environment variable.</li>
 	<li>On <strong>Linux/OSX</strong> you may need to set <code>execute permissions</code> on the files in <code>~/sonarscanner-msbuild/sonar-scanner-(version)/bin</code>.</li>
</ol>
&nbsp;
<h3 id="AnalyzingwithSonarQubeScannerforMSBuild-BeginStep">Begin Step</h3>
The begin step is executed when you add the `begin` command line argument. It <strong>hooks into the MSBuild pipeline, downloads SonarQube quality profiles, settings and prepares your project for the analysis.</strong>

The "begin" step will modify your build like this:
<ul>
 	<li>all existing code analyzers that are referenced by your projects will be disabled and only analyzers from SonarQube plugins will be executed</li>
 	<li>the active CodeAnalysisRuleSet will be updated to match the SonarQube quality profile</li>
 	<li>WarningsAsErrors will be turned off</li>
</ul>
<h2>SonarQube integration with MSBuild and Team Build</h2>
<ul>
 	<li>Technical debt is the set of problems in a development effort that make forward progress on customer value inefficient. Technical debt saps productivity by making code hard to understand, fragile, difficult to validate, and creates unplanned work that blocks progress. Technical debt is insidious. It starts small and grows over time through rushed changes, lack of context and lack of discipline. Organizations often find that more than 50% of their capacity is sapped by technical debt.</li>
 	<li><a href="http://www.sonarqube.org/">SonarQube</a> is an open source platform that is the de facto solution for understanding and managing technical debt.</li>
 	<li>Customers have been telling us and <a href="http://www.sonarsource.com/">SonarSource</a>, the company behind SonarQube, that the SonarQube analysis of .Net apps and integration with Microsoft build technologies needs to be considerably improved.</li>
 	<li>Over the past few months we have been collaborating with our friends from SonarSource and are pleased to make available a set of <a href="http://docs.sonarqube.org/display/SONAR/C%23+Plugin">integration components</a> that allow you to configure a Team Foundation Server (TFS) Build to connect to a SonarQube server and send the following data, which is gathered during a build under the governance of quality profiles and gates defined on the SonarQube server.
<ul>
 	<li>results of .Net and JavaScript code analysis</li>
 	<li>code clone analysis</li>
 	<li>code coverage data from tests</li>
 	<li>metrics for .Net and JavaScript</li>
</ul>
</li>
 	<li>In addition, SonarSource have produced a set of .Net rules, written using the new Roslyn-based code analysis framework, and published them in two forms: a <a href="http://www.nuget.org/packages?q=SonarLint">nuget package</a> and a <a href="https://visualstudiogallery.msdn.microsoft.com/47d1049d-bb27-454e-aab8-24566c85e548?SRC=Home">VSIX</a>. With this set of rules, the analysis that is done as part of build can also be done live inside Visual Studio 2015, exploiting the new Visual Studio 2015 code analysis experience</li>
 	<li>The source code for the above has been made available at <a href="https://github.com/SonarSource">https://github.com/SonarSource</a>, specifically:
<ul>
 	<li><a href="https://github.com/SonarSource/sonar-msbuild-runner">sonar-msbuild-runner</a></li>
 	<li><a href="https://github.com/SonarSource/sonarlint-vs">sonarlint-vs</a></li>
</ul>
</li>
 	<li>We are also grateful to our ever-supportive ALM Rangers who have, in parallel, written a <a href="http://aka.ms/vsartdsq">SonarQube Installation Guide</a>, which explains how to set up a production ready SonarQube installation to be used in conjunction with Team Foundation Server 2013 to analyse .Net apps. This includes reference to the new integration components mentioned above.</li>
</ul>
<h2>Architecture</h2>
&nbsp;
<p id="JvtXUne"><img class="alignnone size-full wp-image-1511 " src="/wp-content/uploads/2018/04/img_5ad75603a9fb3.png" alt="" /></p>

<ol>
 	<li>One <strong>SonarQube Server</strong> starting 3 main processes:
<ol>
 	<li>a <strong>Web Server</strong> for developers, managers to browse quality snapshots and configure the SonarQube instance</li>
 	<li>a <strong>Search Server </strong>based on Elasticsearch to back searches from the UI</li>
 	<li>a <strong>Compute Engine Server</strong> in charge of processing code analysis reports and saving them in the SonarQube Database</li>
</ol>
</li>
 	<li>One <strong>SonarQube </strong><span class="confluence-link"><strong>Database</strong></span><strong> </strong>to store:
<ul>
 	<li>the configuration of the SonarQube instance (security, plugins settings, etc.)</li>
 	<li>the quality snapshots of projects, views, etc.</li>
</ul>
</li>
 	<li>Multiple <strong>SonarQube Plugins</strong> installed on the server, possibly including language, SCM, integration, authentication, and governance plugins</li>
 	<li>One or more<strong> <span class="confluence-link">SonarQube Scanners</span></strong> running on your Build / Continuous Integration Servers to analyze projects</li>
</ol>
<h3 id="ArchitectureandIntegration-AboutMachinesandLocations">About Machines and Locations</h3>
<div>
<ul>
 	<li>The SonarQube Platform cannot have more than one SonarQube Server and one SonarQube Database.</li>
 	<li>For optimal performance, each component (server, database, scanners) should be installed on a separate machine, and the server machine should be dedicated.</li>
 	<li>SonarQube Scanners scale by adding machines.</li>
 	<li>All machines must be time synchronized.</li>
 	<li>The SonarQube Server and the SonarQube Database must be located in the same network</li>
 	<li>SonarQube Scanners don't need to be on the same network as the SonarQube Server.</li>
 	<li>There is <strong>no communication </strong>between<strong> SonarQube Scanners </strong>and the<strong> SonarQube Database</strong>.</li>
</ul>
</div>
<p id="jNNAJaT"><img class="alignnone size-full wp-image-1512 " src="/wp-content/uploads/2018/04/img_5ad7560e70318.png" alt="" /></p>

<h2>References</h2>
<ol>
 	<li>https://dzone.com/articles/why-sonarqube-1</li>
 	<li>https://docs.sonarqube.org/display/SONAR/Get+Started+in+Two+Minutes</li>
 	<li><a href="http://www.sonarqube.org/what-makes-checkstyle-pmd-findbugs-and-macker-complementary/" target="_blank" rel="nofollow noopener">Sonar Blog on CheckStyle, PMD, Findbug</a></li>
 	<li><a href="http://www8.hp.com/us/en/software-solutions/software.html?compURI=1338812#.UnuwSnWAU14" target="_blank" rel="nofollow noopener">HP Fortify Website</a></li>
 	<li>Sonar Code Quality Testing Essentials</li>
 	<li><a href="http://www.manning.com/papapetrou/" rel="nofollow">SonarQube in Action</a></li>
 	<li>https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild</li>
 	<li>https://docs.sonarqube.org/display/SONAR/Architecture+and+Integration</li>
 	<li>https://dzone.com/articles/how-quickly-get-started-sonar</li>
 	<li>https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild</li>
 	<li>https://docs.sonarqube.org/display/SCAN/Install+the+SonarScanner+for+MSBuild</li>
 	<li>Plugin library https://docs.sonarqube.org/display/PLUG</li>
 	<li>Visual studio plugin SonarLint https://www.sonarlint.org/visualstudio/index.html</li>
</ol>
