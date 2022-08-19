---
layout: post
title: .NET Core - EF Core
date: 2018-07-26 20:02
author: tmasabari
comments: true
categories: [Architecture, Databases, Design]
---
<ul>
 	<li>EF Core keeps the developer experience from EF6, and most of the top-level APIs remain the same too, so EF Core will feel very familiar to folks who have used EF6. At the same time, EF Core is built over a completely new set of core components.</li>
 	<li>This means EF Core doesn't automatically inherit all the features from EF6. While some of these features will show up in future releases, other less commonly used features will not be implemented in EF Core.</li>
 	<li>The new, extensible, and lightweight core has also allowed us to add some features to EF Core that will not be implemented in EF6 (such as alternate keys, batch updates, and mixed client/database evaluation in LINQ queries).</li>
 	<li>https://docs.microsoft.com/en-in/ef/efcore-and-ef6/</li>
</ul>
&nbsp;
<ul>
 	<li>https://docs.microsoft.com/en-in/ef/efcore-and-ef6/features</li>
 	<li>https://docs.microsoft.com/en-in/ef/efcore-and-ef6/choosing</li>
</ul>
EF6 requires .NET Framework 4.0 (or a later version) and is only supported on Windows (that is, EF6 does not currently run on .NET Core and is not supported in other operating systems), but it is still a viable choice for new applications as long those constraints are acceptable and the application does not require new features in EF Core that are not available to EF6.
<ul>
 	<li>Review <a href="https://docs.microsoft.com/en-in/ef/efcore-and-ef6/features" data-linktype="relative-path">Feature Comparison</a>to see if EF Core may be a suitable choice for your application.</li>
 	<li><strong class="">You should view the move from EF6 to EF Core as a port rather than an upgrade.</strong> See <a class="" href="https://docs.microsoft.com/en-in/ef/efcore-and-ef6/porting/index" data-linktype="relative-path">Porting from EF6 to EF Core</a> for more information.</li>
</ul>
<p class="">The EF Core column contains the number of the product version in which the feature first appeared.</p>

<div class="table-scroll-wrapper">
<table>
<thead>
<tr>
<th class=""><strong>Creating a Model</strong></th>
<th><strong>EF 6</strong></th>
<th><strong>EF Core</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Basic class mapping</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Constructors with parameters</td>
<td></td>
<td>2.1</td>
</tr>
<tr>
<td>Property value conversions</td>
<td></td>
<td>2.1</td>
</tr>
<tr>
<td>Mapped types with no keys (query types)</td>
<td></td>
<td>2.1</td>
</tr>
<tr>
<td>Conventions</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Custom conventions</td>
<td>Yes</td>
<td>1.0 (partial)</td>
</tr>
<tr>
<td>Data annotations</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Fluent API</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Inheritance: Table per hierarchy (TPH)</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Inheritance: Table per type (TPT)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Inheritance: Table per concrete class (TPC)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Shadow state properties</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Alternate keys</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Many-to-many without join entity</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Key generation: Database</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Key generation: Client</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Complex/owned types</td>
<td>Yes</td>
<td>2.0</td>
</tr>
<tr>
<td>Spatial data</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Graphical visualization of model</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Graphical model editor</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Model format: Code</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Model format: EDMX (XML)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Create model from database: Command line</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Create model from database: VS wizard</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Update model from database</td>
<td>Partial</td>
<td></td>
</tr>
<tr>
<td>Global query filters</td>
<td></td>
<td>2.0</td>
</tr>
<tr>
<td>Table splitting</td>
<td>Yes</td>
<td>2.0</td>
</tr>
<tr>
<td>Entity splitting</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Database scalar function mapping</td>
<td>Poor</td>
<td>2.0</td>
</tr>
<tr>
<td>Field mapping</td>
<td></td>
<td>1.1</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Querying Data</strong></td>
<td><strong>EF6</strong></td>
<td><strong>EF Core</strong></td>
</tr>
<tr>
<td>LINQ queries</td>
<td>Yes</td>
<td>1.0 (in-progress for complex queries)</td>
</tr>
<tr>
<td>Readable generated SQL</td>
<td>Poor</td>
<td>1.0</td>
</tr>
<tr>
<td>Mixed client/server evaluation</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>GroupBy translation</td>
<td>Yes</td>
<td>2.1</td>
</tr>
<tr>
<td>Loading related data: Eager</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Loading related data: Eager loading for derived types</td>
<td></td>
<td>2.1</td>
</tr>
<tr>
<td>Loading related data: Lazy</td>
<td>Yes</td>
<td>2.1</td>
</tr>
<tr>
<td>Loading related data: Explicit</td>
<td>Yes</td>
<td>1.1</td>
</tr>
<tr>
<td>Raw SQL queries: Entity types</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Raw SQL queries: Non-entity types (query types)</td>
<td>Yes</td>
<td>2.1</td>
</tr>
<tr>
<td>Raw SQL queries: Composing with LINQ</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Explicitly compiled queries</td>
<td>Poor</td>
<td>2.0</td>
</tr>
<tr>
<td>Text-based query language (Entity SQL)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Saving Data</strong></td>
<td><strong>EF6</strong></td>
<td><strong>EF Core</strong></td>
</tr>
<tr>
<td>Change tracking: Snapshot</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Change tracking: Notification</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Change tracking: Proxies</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Accessing tracked state</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Optimistic concurrency</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Transactions</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Batching of statements</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Stored procedure mapping</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Disconnected graph low-level APIs</td>
<td>Poor</td>
<td>1.0</td>
</tr>
<tr>
<td>Disconnected graph End-to-end</td>
<td></td>
<td>1.0 (partial)</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Other Features</strong></td>
<td><strong>EF6</strong></td>
<td><strong>EF Core</strong></td>
</tr>
<tr>
<td>Migrations</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Database creation/deletion APIs</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Seed data</td>
<td>Yes</td>
<td>2.1</td>
</tr>
<tr>
<td>Connection resiliency</td>
<td>Yes</td>
<td>1.1</td>
</tr>
<tr>
<td>Lifecycle hooks (events, interception)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>Simple Logging (Database.Log)</td>
<td>Yes</td>
<td></td>
</tr>
<tr>
<td>DbContext pooling</td>
<td></td>
<td>2.0</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Database Providers</strong></td>
<td><strong>EF6</strong></td>
<td><strong>EF Core</strong></td>
</tr>
<tr>
<td>SQL Server</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>MySQL</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>PostgreSQL</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Oracle</td>
<td>Yes</td>
<td>1.0 <sup>(1)</sup></td>
</tr>
<tr>
<td>SQLite</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>SQL Server Compact</td>
<td>Yes</td>
<td>1.0 <sup>(2)</sup></td>
</tr>
<tr>
<td>DB2</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>Firebird</td>
<td>Yes</td>
<td>2.0</td>
</tr>
<tr>
<td>Jet (Microsoft Access)</td>
<td></td>
<td>2.0 <sup>(2)</sup></td>
</tr>
<tr>
<td>In-memory (for testing)</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Platforms</strong></td>
<td><strong>EF6</strong></td>
<td><strong>EF Core</strong></td>
</tr>
<tr>
<td>.NET Framework (Console, WinForms, WPF, ASP.NET)</td>
<td>Yes</td>
<td>1.0</td>
</tr>
<tr>
<td>.NET Core (Console, ASP.NET Core)</td>
<td></td>
<td>1.0</td>
</tr>
<tr>
<td>Mono &amp; Xamarin</td>
<td></td>
<td>1.0 (in-progress)</td>
</tr>
<tr>
<td>UWP</td>
<td></td>
<td class="">1.0 (in-progress)</td>
</tr>
</tbody>
</table>
</div>
&nbsp;

Steps
<ul>
 	<li>Create class library</li>
 	<li>To add identity db support install Microsoft.AspNetCore.Identity.EntityFrameworkCore. This will install all necessary dependencies
<ul>
 	<li>Microsoft.AspNetCore.Identity.Core</li>
 	<li>Microsoft.EntityFrameworkCore, etc</li>
</ul>
</li>
 	<li>To add EF Core support to a project, install the database provider that you want to target. This tutorial uses SQL Server, and the provider package is <a href="https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/" data-linktype="external">Microsoft.EntityFrameworkCore.SqlServer</a>. This package is included in the <a class="xref" href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/metapackage?view=aspnetcore-2.0" data-linktype="relative-path">Microsoft.AspNetCore.All</a> metapackage, so you don't have to install it.
<ul>
 	<li>This package and its dependencies (<code>Microsoft.EntityFrameworkCore</code> and <code>Microsoft.EntityFrameworkCore.Relational</code>) provide runtime support for EF. You'll add a tooling package later, in the <a href="https://docs.microsoft.com/en-us/aspnet/core/data/ef-mvc/migrations?view=aspnetcore-2.1" data-linktype="relative-path">Migrations</a> tutorial.</li>
</ul>
</li>
 	<li>Create model classes
<ul>
 	<li>Create classes to represent role, user and database context by inheriting from framework classes IdentityRole, IdentityUser and IdentityDbContext,
<code><code>public class AppIdentityRole : IdentityRole
{ }</code></code>public class AppIdentityUser : IdentityUser
{
public int Age { get; set; }
}<code><code></code></code>public class AppIdentityDbContext
: IdentityDbContext&lt;AppIdentityUser, AppIdentityRole, string&gt;
{
public AppIdentityDbContext(DbContextOptions options)
: base(options)
{ }
}</li>
</ul>
</li>
 	<li>The advantage of inheriting from framework classes is that you can add your own custom properties (e.g. Age in my case) to user entity. Also by inheriting database context you could modify the database schema, if required.</li>
 	<li>Configure services for Identity in Startup class, including configuration of cookie middleware,</li>
</ul>
&nbsp;

EF Tools

https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/index
<p class="">The <a class="" href="https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/powershell" data-linktype="relative-path">EF Core Package Manager Console (PMC) Tools</a> provide a superior experience inside Visual Studio. Run them using NuGet's <a href="https://docs.microsoft.com/nuget/tools/package-manager-console" data-linktype="external">Package Manager Console</a>. These tools work with both .NET Framework and .NET Core projects.</p>
The <a href="https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/dotnet" data-linktype="relative-path">EF Core .NET Command-line Tools</a> are an extension to the <a href="https://docs.microsoft.com/dotnet/core/tools/" data-linktype="external">.NET Core command-line interface (CLI) tools</a> that are cross-platform and can run outside of Visual Studio. These tools require a .NET Core SDK project (one with <code>Sdk="Microsoft.NET.Sdk"</code> or similar in the project file).

The tools support projects targeting .NET Framework or .NET Core.
<h2 id="startup-and-target-projects" class="heading-with-anchor">Startup and Target Projects</h2>
Whenever you invoke a command, there are two projects involved: the target project and the startup project.

The target project is where any files are added (or in some cases removed).

The startup project is the one emulated by the tools when executing your project's code.
<p class="">Both the target project and the startup project can be the same.</p>
&nbsp;

Install and commands https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/powershell
<p class="">You can install it by executing the following command inside <a href="https://docs.microsoft.com/nuget/tools/package-manager-console" data-linktype="external">Package Manager Console</a>.</p>

<div class="codeHeader" data-bi-name="code-header"><span class="language">PowerShell</span><button class="action" data-bi-name="copy">Copy</button></div>
<pre class=""><code class="lang-powershell"><span class="hljs-pscommand">Install-Package</span> Microsoft.EntityFrameworkCore.Tools
</code></pre>
If everything worked correctly, you should be able to run this command:
<div class="codeHeader" data-bi-name="code-header"><span class="language">PowerShell</span><button class="action" data-bi-name="copy">Copy</button></div>
<pre><code class="lang-powershell"><span class="hljs-pscommand">Get-Help</span> about_EntityFrameworkCore</code></pre>
<h2>EF steps to generate tables (migrations)</h2>
<code>context.Database.EnsureCreated()</code> only ensures that the database is created, it doesn't check whether all the tables are present or not.

To add the OpenIddict entities in an existing app, use the EF Core migrations.

To regenerate the tables
<ul>
 	<li>Delete all the tables in a context</li>
 	<li>Select the project which has EF context as the Default project in "Package Manager Console"</li>
 	<li>Delete all the files in migrations folder
<ul>
 	<li>Add-Migration &lt;migration name =V2IdentityCustomized&gt; -o &lt;relative folder path = \Migrations&gt;
<ul>
 	<li>This step will compile the project</li>
</ul>
</li>
 	<li>Update-Database - to generate the data definition scripts</li>
</ul>
</li>
 	<li>Dotnet SDK
<ul>
 	<li>
<pre><code class="language-text" data-lang="text">dotnet ef migrations add CreateOpenIddictModels</code> <code class="language-text" data-lang="text">dotnet ef database update</code></pre>
</li>
</ul>
</li>
</ul>
&nbsp;
