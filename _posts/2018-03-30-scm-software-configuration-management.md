---
layout: post
title: SCM - Software Configuration Management
date: 2018-03-30 05:12
author: tmasabari
comments: true
categories: [CI CD, Interview Preparation, SCM, Source Control]
---
<strong>Version Control Systems</strong> are just that, software that provides versioning functionality (Git, Subversion, TFS Version Control) all fall into this category.

<strong>Software Configuration Management</strong> is a broader term that encompasses all the processes needed to build, package, and deploy software -- this includes Version Control Systems. It does not refer to software per se.

Caution, <strong><a href="http://en.wikipedia.org/wiki/SCM" rel="noreferrer">SCM</a></strong> can refer to different meanings about Versioning:
<ul>
 	<li><strong><a href="http://en.wikipedia.org/wiki/Software_configuration_management" rel="noreferrer">Software Configuration Management</a></strong> as explained above</li>
 	<li><strong><a href="http://en.wikipedia.org/wiki/Source_Control_Management" rel="noreferrer">Source Control Management</a></strong> is same as <strong>Version Control</strong> and <strong>Source Control</strong> and <strong>VCS</strong></li>
</ul>
Moreover, people may use <strong>SCM</strong> to refer to other naming:
<ul>
 	<li><strong>Source Code Management</strong> as in <strong><a href="http://en.wikipedia.org/wiki/Source_Code_Control_System" rel="noreferrer">Source Code Control System</a></strong></li>
 	<li><strong>Software Code Management</strong> but this is a deformation of <strong>Software Configuration Management</strong></li>
 	<li><strong>Source Configuration Management</strong> same meaning as <strong>Software Configuration Management</strong> but maybe more focused on <em>source code</em> than on the whole software (settings, command line arguments, host parameters...)</li>
</ul>

<hr />

Let's define them:
<ul>
 	<li><strong>Version Control Systems</strong> are the standalone software to manage the versions (Git...)</li>
 	<li><strong>Source Control Management</strong> is the same as <strong>VCS</strong></li>
 	<li><strong>Software Configuration Management</strong> is all processes to manage all the changes of the software: the development (<strong>VCS</strong>), the delivery release (<strong>VCS</strong>), the bug tracking, the software settings, the host/network settings, the version/settings of the other software interacting with...</li>
</ul>

<hr />

Therefore, just using the acronym <strong>SCM</strong> is confusing: some people may understand the same meaning as <strong>VCS</strong>, some others may understand the whole process where <strong>VCS</strong> is just an aspect.

References
<ol>
 	<li>Patterns https://dzone.com/storage/assets/7529578-rc-167-softwareconfigurationmanagementpatterns.pdf</li>
 	<li>SCM</li>
</ol>

<hr />

<strong>Agile / Project management tools</strong>

<a href="https://financesonline.com/list-10-best-project-management-software-tools/">https://financesonline.com/list-10-best-project-management-software-tools/</a>

JIRA, TFS, MS Project

<a href="https://reviews.financesonline.com/p/jira/">JIRA</a> helps you to assign tasks and prioritize your work. This app is recommended for application developers as it covers all aspects from initiation to launch. The cloud version of JIRA is easy to set up and maintain as all updates are automatic. You can also opt for the on-premise solution which offers Windows and Linux installers. Important features include: advanced reporting, robust search and filtering, customizable wallboards and dashboards, seamless issue and source integration, and defect and bugs management.

What are the standout elements of JIRA? You can utilize Scrum and Kanban workflows for project success. With the application’s advanced workflow engine you can easily create a fitting process for your team. The dashboards give you a personalized view.

&nbsp;

<strong>Version control tools</strong>

Git, SourceTree, SVN, Stash (server), TFS

<a title="https://tortoisesvn.net/docs/nightly/TortoiseSVN_en/tsvn-dug-conflicts.html" href="https://tortoisesvn.net/docs/nightly/TortoiseSVN_en/tsvn-dug-conflicts.html">https://tortoisesvn.net/docs/nightly/TortoiseSVN_en/tsvn-dug-conflicts.html</a>
<h5>File Conflicts</h5>
A file conflict occurs when two or more developers have changed the same few lines of a file.You can either launch an external merge tool / conflict editor with TortoiseSVN → Edit Conflicts or you can use any text editor to resolve the conflict manually. You should decide what the code should look like, do the necessary changes and save the file.
<h5>Property Conflicts</h5>
A property conflict occurs when two or more developers have changed the same property. As with file content, resolving the conflict can only be done by the developers.

If one of the changes must override the other then choose the option to Resolve using local property or Resolve using remote property.
<h5>Tree Conflicts</h5>
A tree conflict occurs when a developer moved/renamed/deleted a file or folder, which another developer either also has moved/renamed/deleted or just modified.

Remember that after an update the working BASE will always contain the revision of each item as it was in the repository at the time of update.

For simple file or directory deletions he can choose to keep the item with Developer A's changes and discard the deletion. Or, by marking the conflict as resolved without doing anything he effectively discards Developer A's changes.
<ol>
 	<li>Developer A working on trunk moves <code>Foo.c</code> to <code>Bar.c</code> and commits it to the repository.</li>
 	<li>Developer B working on a branch modifies <code>Foo.c</code> and commits it to the repository.</li>
 	<li>tree conflict:
<ul>
 	<li><code>Bar.c</code> is marked as added.</li>
 	<li><code>Foo.c</code> is marked as modified with a tree conflict.</li>
</ul>
</li>
</ol>
<ul>
 	<li>To merge her local changes with the reshuffle, Developer B must first find out to what filename the conflicted file <code>Foo.c</code> was renamed/moved in the repository. This can be done by using the log dialog for the merge source. The conflict editor only shows the log for the working copy as it does not know which path was used in the merge, so you will have to find that yourself. The changes must then be merged by hand as there is currently no way to automate or even simplify this process. Once the changes have been ported across, the conflicted path is redundant and can be deleted. In this case use the Remove button in the conflict editor dialog to clean up and mark the conflict as resolved.</li>
 	<li>If Developer B decides that A's changes were wrong then she must choose the Keep button in the conflict editor dialog. This marks the conflicted file/folder as resolved, but Developer A's changes need to be removed by hand. Again the log dialog for the merge source helps to track down what was moved</li>
</ul>

<hr />

http://www.theserverside.com/feature/Application-lifecycle-management-Best-practices-for-improving-the-deployment-process

<strong>Deployment procedures</strong>

Document

Documentation is your friend. Make sure there is <a href="http://www.theserverside.com/feature/Project-Documentation-and-Agile-Development">detailed, accurate documentation</a> of the code itself, how all the components fit together, the deployment plan/policies/process/protocols, troubleshooting, maintenance and training/instructions for use.

Rollback plan

you should always be prepared for the worst, which means never deploying without a plan for rolling back the installation if it doesn’t go well. This includes writing <i>and testing</i> uninstall scripts.

As part of a pre-deployment strategy, identify points along the path where you stop and evaluate whether you are really ready to move forward or if you should delay or stop the process.

<strong>Configuration management</strong>

Add a prebuild event (build step after git replication in jenkins) to replace the web.config with appropriate file for the environment.
<ol>
 	<li>Use ASP.NET Web Application Projects (which have MSBuild based project files)</li>
 	<li>Open the VS Configuration Manager and create new "Dev", "QA", "Staging" build configurations for your project and solution</li>
 	<li>Add new "web.config.dev", "web.config.qa", and "web.config.staging" files in your project and customize them to contain the app's mode specific configuration settings</li>
 	<li>Add a new "pre-build event" command to your project file that can automatically copy over the web.config file in your project with the appropriate mode specific version each time you build the project (for example: if your solution was in the "Dev" configuration, it would copy the web.config.dev settings to the main web.config file).</li>
</ol>
The benefit with this approach is that it works well in a source control environment (everyone can sync and build locally without having to make any manual changes on their local machines).  It also works on a build server - including with scenarios where you are doing automated command-line solution builds.

<a title="http://www.hanselman.com/blog/ManagingMultipleConfigurationFileEnvironmentsWithPreBuildEvents.aspx" href="http://www.hanselman.com/blog/ManagingMultipleConfigurationFileEnvironmentsWithPreBuildEvents.aspx">http://www.hanselman.com/blog/ManagingMultipleConfigurationFileEnvironmentsWithPreBuildEvents.aspx</a>

<a title="https://stackoverflow.com/questions/305447/using-different-web-config-in-development-and-production-environment" href="https://stackoverflow.com/questions/305447/using-different-web-config-in-development-and-production-environment">https://stackoverflow.com/questions/305447/using-different-web-config-in-development-and-production-environment</a>

<a title="https://stackoverflow.com/questions/24917435/jenkins-deployment-for-net-application" href="https://stackoverflow.com/questions/24917435/jenkins-deployment-for-net-application">https://stackoverflow.com/questions/24917435/jenkins-deployment-for-net-application</a>
<ul>
 	<li>You will probably deploy using Web Deploy <a href="http://www.iis.net/downloads/microsoft/web-deploy">http://www.iis.net/downloads/microsoft/web-deploy</a></li>
 	<li>If using Web Deploy, you can use either web.config transformations or Web Deploy publish profiles. Both of these are supported by Jenkins.</li>
 	<li>Web.config transformations: <a href="http://msdn.microsoft.com/en-us/library/dd465326.aspx">http://msdn.microsoft.com/en-us/library/dd465326.aspx</a></li>
 	<li>Web Deploy Publish Profiles: <a href="http://msdn.microsoft.com/en-us/library/dd465323(v=vs.110).aspx">http://msdn.microsoft.com/en-us/library/dd465323(v=vs.110).aspx</a>(NOTE each profile has a separate web.config file named web.NAME_OF_PROFILE.config (e.g., web.debug.config))</li>
 	<li>Here is an easy walkthrough of the entire process of creating a profile: <a href="http://www.asp.net/web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12">http://www.asp.net/web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12</a></li>
 	<li>See this question for how to make Web Deploy work with Jenkins: <a href="https://stackoverflow.com/questions/16923126/jenkins-msbuild-and-web-deploy-unable-to-create-web-package">Jenkins, MSBuild and Web Deploy: Unable to create Web Package</a></li>
</ul>
&nbsp;
<h3>Git Flow</h3>
<a title="http://nvie.com/posts/a-successful-git-branching-model/" href="http://nvie.com/posts/a-successful-git-branching-model/">http://nvie.com/posts/a-successful-git-branching-model/</a>
<h4>Decentralized but centralized</h4>
The repository setup that we use and that works well with this branching model, is that with a central “truth” repo. Note that this repo is only <em>considered</em> to be the central one (since Git is a DVCS, there is no such thing as a central repo at a technical level). We will refer to this repo as <code>origin</code>, since this name is familiar to all Git users.

<img src="http://nvie.com/img/centr-decentr@2x.png" alt="" width="487" />

At the core, the development model is greatly inspired by existing models out there. The central repo holds two main branches with an infinite lifetime:
<ul>
 	<li><code>master</code></li>
 	<li><code>develop</code></li>
</ul>
Unlike the main branches, these branches always have a limited life time, since they will be removed eventually.

The different types of branches we may use are:
<ul>
 	<li>Feature branches</li>
 	<li>Release branches</li>
 	<li>Hotfix branches</li>
</ul>
Each of these branches have a specific purpose and are bound to strict rules as to which branches may be their originating branch and which branches must be their merge targets.

<img class="aligncenter" src="http://nvie.com/img/main-branches@2x.png" width="292" height="440" />

<img class="aligncenter" src="http://nvie.com/img/git-model@2x.png" width="554" height="734" />

add three branches – <em>develop</em>, <em>test</em> and <em>production</em>

The <em>develop</em> branch is the common “snapshot” branch that developers merge their completed features or bug fixes into and it can be built on Jenkins. The <em>test</em> and <em>production</em> branches will be used to build your application for the corresponding environments and optionally publishing them automatically. Push all three branches to the remote GitHub repository.

<strong>(Optional)</strong> To prevent developers from merging untested code into test and production you can use the <em>fork/pull request</em> GitHub features. In that scenario, Jenkins will pull code from one GitHub account’s repository to which only certain developers and release managers have push access.

The drawback with this setup is that it requires developers to issue pull requests even when merging into <em>develop</em>. You could also create another repository where all developers has push access and pull <em>develop</em> from that repository.
<h3>CI/CD &amp; Jenkins configuration</h3>
<a title="https://blog.couchbase.com/continuous-deployment-with-jenkins-and-net/" href="https://blog.couchbase.com/continuous-deployment-with-jenkins-and-net/">https://blog.couchbase.com/continuous-deployment-with-jenkins-and-net/</a>

<a title="https://blog.jayway.com/2012/10/17/a-simple-continuous-integration-and-deployment-workflow-with-asp-net-mvc-github-and-jenkins/" href="https://blog.jayway.com/2012/10/17/a-simple-continuous-integration-and-deployment-workflow-with-asp-net-mvc-github-and-jenkins/">https://blog.jayway.com/2012/10/17/a-simple-continuous-integration-and-deployment-workflow-with-asp-net-mvc-github-and-jenkins/</a>

<a title="https://docs.microsoft.com/en-us/aspnet/web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent" href="https://docs.microsoft.com/en-us/aspnet/web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent">https://docs.microsoft.com/en-us/aspnet/web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent</a>

Using Continuous Integration/Continuous Deployment, enables a workflow like this:
<ul>
 	<li>Code, build and test locally on your dev. box (as usual)</li>
 	<li>Check source code in to a development branch in your favourite Source Control Management System.</li>
 	<li>Optional code review by team members.</li>
 	<li>Merge your changes to the main (release) branch.</li>
 	<li>The CI Server will detect the changes to the main branch and download, compile and deploy/install your application on the release server.</li>
</ul>
So let’s take a closer look at my application architecture and components:
<ul>
 	<li><strong>Platform</strong>: .NET 4.5.2</li>
 	<li><strong>IDE</strong>: Visual Studio 2015 (MSBuild files)</li>
 	<li><strong>Application type</strong>: Windows Service</li>
 	<li><strong>NuGet</strong>: Package Manager used for all references.</li>
 	<li><strong>Source Control</strong>: Git (github.com)</li>
</ul>
The build server should be a Windows Server 2008 (or higher) with the following software installed:
<ul>
 	<li>.NET 4 or higher (depending on EF version).</li>
 	<li>Visual Studio Express (or other version, but they require licenses).</li>
 	<li>MSBuild Extensions Pack.</li>
 	<li>Git.</li>
 	<li><a href="https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+as+a+Windows+service">Jenkins as a service</a>.</li>
 	<li>The following Jenkins plugins: <a href="https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin">Git Plugin</a>, <a href="https://wiki.jenkins-ci.org/display/JENKINS/GitHub+Plugin">GitHub Plugin</a>, <a href="https://wiki.jenkins-ci.org/display/JENKINS/MSBuild+Plugin">MSBuild Plugin</a> and <a href="https://wiki.jenkins-ci.org/display/JENKINS/NUnit+Plugin">NUnit Plugin</a>.</li>
</ul>
The CI Server should be able to understand all components mentioned above and (as I’m lazy) it should be really easy to maintain and set up.
<ul>
 	<li style="list-style-type: none;">
<ul>
 	<li>
<h6>Install the Git Plugin for Jenkins:</h6>
</li>
 	<li>
<h6>Install the MSBuild Plugin for Jenkins:</h6>
</li>
 	<li>
<h6>MSBuild configuration</h6>
</li>
 	<li>
<h6>MSBuild installation</h6>
<ul>
 	<li>It’s not always feasible or even possible to install Visual Studio on your build machine. This could be due to license and security issues etc.</li>
 	<li>To accommodate this Microsoft has released a separate package called: “Microsoft Build Tools 2015” that contains all you need for for using MSBuild.</li>
 	<li>Complete the Git configuration by filling in the blanks with a URL to your repository and optionally credentials (if needed).Jenkins can also work with branches. In this set-up I will leave the branch as the default (Master) but you can select whatever fits your needs.</li>
</ul>
</li>
 	<li>Create new job</li>
 	<li>configure git repository  &amp; branch  Next, expand the “Source Code Management” region by selecting “Git”.</li>
 	<li>Save Test Git by Project – &gt; Build</li>
 	<li>Add step to restore nuget packages
<ul>
 	<li>Project –&gt; Configure &gt; Add build step –&gt;Execute Windows
batch command Command nuget restore &lt;path&gt;</li>
 	<li><code>nuget.exe</code> is the executable used to restore the solution’s
NuGet package dependencies. You could argue whether or not it’s good practice to
have binary files in your source control, but in this case it’s a required
dependency for the build system and therefore I have included it.</li>
</ul>
</li>
</ul>
</li>
</ul>
<ul>
 	<li style="list-style-type: none;"></li>
 	<li>Project –&gt; Configure &gt; Add build step –&gt; “Build a Visual Studio project or solution using MSBuild”
<ol>
 	<li>First, select the MSBuild version (we configured this in a previous step).</li>
 	<li>Then give the path to the *.sln or *.proj file for your project.<em>For the pre-cooked repository the path is: <code>srcMyWindowsServiceMyWindowsServiceDeploy-Windows-Service-Via-MSBuild.proj</code></em><strong>Please note</strong>: <em>We are not pointing to the solution file, rather we are pointing to a custom MSBuild file that is in the project. This MSBuild file is handling all steps involved with compiling and deploying the Windows Service.</em></li>
 	<li>The main entry point file is <a href="https://github.com/martinesmann/jenkins-ci-template/blob/master/src/MyWindowsService/MyWindowsService/MyWindowsService.csproj">Deploy-Windows-Service-Via-MSBuild.proj</a> it’s a MSBuild file constructed to, not only, compile the source code; but also: stop, uninstall and start the Windows Service application. This is achieved by calling the three batch files as needed: <a href="https://github.com/martinesmann/jenkins-ci-template/blob/master/src/MyWindowsService/MyWindowsService/safeServiceDelete.bat">safeServiceDelete.bat</a>, <a href="https://github.com/martinesmann/jenkins-ci-template/blob/master/src/MyWindowsService/MyWindowsService/safeServiceStart.bat">safeServiceStart.bat</a> and <a href="https://github.com/martinesmann/jenkins-ci-template/blob/master/src/MyWindowsService/MyWindowsService/safeServiceStop.bat">safeServiceStop.bat</a></li>
</ol>
</li>
 	<li>Use <a href="http://www.iis.net/downloads/microsoft/web-deploy">Web Deploy</a> to push the files from Jenkins straight to IIS</li>
</ul>

<hr />

<strong>ALM &amp; Automate as much as possible</strong>

Take the time to <a href="http://www.theserverside.com/tip/JavaOne-2012-Improving-ALM-workflow-with-automation-in-Oracle-PaaS">source reliable, modular automation tools</a> or scripts to handle as many of the ALM processes as possible, including:
<ul class=" default-list">
 	<li>Load testing and performance testing</li>
 	<li>Identifying dependencies between files and packaging files for distribution</li>
 	<li>Installation to the target environment</li>
 	<li>Configuration and change management</li>
</ul>
Test

<a href="http://www.theserverside.com/feature/Discovering-the-right-metrics-for-scalability-testing">Testing deployment</a> in a sandbox environment that mimics the real production environment as closely as possible is essential for success. Still, many enterprises let their preproduction server and their real-time servers get out of sync as updates and upgrades happen. Make sure the testing servers and the production servers are as close to identical as possible, be it operating system patches or configuration file settings.

Installation

For simple systems, <a title="Installation (computer programs)" href="https://en.wikipedia.org/wiki/Installation_(computer_programs)">installation</a> involves establishing some form of <a title="Command (computing)" href="https://en.wikipedia.org/wiki/Command_(computing)">command</a>, shortcut, script or <a class="mw-redirect" title="Service (computing)" href="https://en.wikipedia.org/wiki/Service_(computing)">service</a> for executing the software (manually or automatically).

In larger software deployments on <a title="Server (computing)" href="https://en.wikipedia.org/wiki/Server_(computing)">servers</a>, the main copy of the software to be used by users - "production" - might be installed on a production server in a production environment. Other versions of the deployed software may be installed in a <a class="mw-redirect" title="Test environment" href="https://en.wikipedia.org/wiki/Test_environment">test environment</a>, <a class="mw-redirect" title="Development environment (software development process)" href="https://en.wikipedia.org/wiki/Development_environment_(software_development_process)">development environment</a> and disaster recovery environment.In complex <a title="Continuous delivery" href="https://en.wikipedia.org/wiki/Continuous_delivery">continuous delivery</a> environments and/or <a title="Software as a service" href="https://en.wikipedia.org/wiki/Software_as_a_service">software as a service</a> systems, differently-configured versions of the system might even exist simultaneously in the production environment for different internal or external customers (this is known as a <i>multi-tenant architecture</i>), or even be gradually rolled out in parallel to different groups of customers, with the possibility of cancelling one or more of the parallel deployments. For example, <a title="Twitter" href="https://en.wikipedia.org/wiki/Twitter">Twitter</a> is known to use the latter approach for <a title="A/B testing" href="https://en.wikipedia.org/wiki/A/B_testing">A/B testing</a> of new features and <a title="User interface" href="https://en.wikipedia.org/wiki/User_interface">user interface</a> changes. A "hidden live" group can also be created within a production environment, consisting of servers that are not yet connected to the production <a class="mw-redirect" title="Load balancer" href="https://en.wikipedia.org/wiki/Load_balancer">load balancer</a>, for the purposes of <a class="new" title="Blue-green deployment (page does not exist)" href="https://en.wikipedia.org/w/index.php?title=Blue-green_deployment&amp;action=edit&amp;redlink=1">blue-green deployment</a>.

Deactivation

Deactivation is the inverse of activation, and refers to shutting down any already-executing components of a system. Deactivation is often required to perform other deployment activities, e.g., a software system may need to be deactivated before an update can be performed. The practice of removing infrequently used or obsolete systems from service is often referred to as <a title="Application retirement" href="https://en.wikipedia.org/wiki/Application_retirement">application retirement</a> or application decommissioning.

<hr />

&nbsp;
