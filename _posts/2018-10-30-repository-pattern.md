---
layout: post
title: Repository pattern, EF and DI
date: 2018-10-30 08:42
author: tmasabari
comments: true
categories: [Uncategorized]
---
<!-- wp:heading -->
<h2>Concepts</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>DB Context follows unit of work pattern. So if "save changes" method is called entire operation on the repository will be saved.  </li><li>DB Context will be injected by DI framework to the controller. So all the operations in the containers is wrapped in UoW.</li><li>EF's <code>DbContext</code>used to not implement an interface, so it made mocking it difficult for testing purposes. However, that was corrected in EF 6<br></li><li>EF Core is completely testable end-to-end and has an in-memory database provider as well now, which means you don't even need to mock it, though you very much can if you want.</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>What is Repository pattern and why should you use it?</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>I think the main reason to implement the repository pattern is to separate your storage framework (i.e. EntityFramework) from the rest of your application.</li><li>With the Repository pattern, we create an abstraction layer between the data access and the business logic layer of an application. </li><li>By using it, we are promoting a more loosely coupled approach to access our data from the database. </li><li>Also, the code is cleaner and easier to maintain and reuse. </li><li>Data access logic is in a separate class, or sets of classes called a repository, with the responsibility of persisting the application’s business model.</li><li>Business class will depend up on exact repository instead of depending up on entire context.</li><li>In case if EF needs to be replaced in future, it can be easily done.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Inject repository classes as services to the DI. (make sure generic repository is not abstract)</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Just use the non-generic registration overloads (The ones where you need to pass the 2 <code>Type</code>objects.) Then provide the <a href="https://stackoverflow.com/questions/2173107/what-exactly-is-an-open-generic-type-in-net">open generic types</a> of both your interface and the implementation:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>services.AddScoped(typeof(IGenericRepository&lt;>), typeof(GenericRepository&lt;>));</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>In your controller add a dependency for a repository of a specific type (a closed generic type)</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>public HomeController(IGenericRepository&lt;Lookup1> repository){    ...}</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>now you can resolve it in the following way:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>serviceProvider.GetService(typeof(IRepository&lt;A,B>));
// or: with extensionmethod
serviceProvider.GetService&lt;IRepository&lt;A,B>>();</code></pre>
<!-- /wp:code -->

<!-- wp:list -->
<ul><li>Mocking EF.Core</li><li>You got InMemory Provider for testing, it InMemory DB isn't a relational DB, so it doesn't enforce indexes and uniques, FK/PK relationships etc. </li><li>If you want something closer to relational database you have to use Sqlite in-memory mode for tests. This is as official recommendation as the <a href="https://docs.microsoft.com/en-us/ef/core/miscellaneous/testing/in-memory">official docs go for</a></li><li>An integration test should actually, you know, test the integration of the components your app is using, such as a SQL Server database, which the in memory provider is not one of. <br>Likewise, SQLite would not be a replacement for integration testing, unless you're actually using it in production.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>References</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://code-maze.com/net-core-web-development-part4/">https://code-maze.com/net-core-web-development-part4/</a></li><li><a href="https://code-maze.com/async-generic-repository-pattern/">https://code-maze.com/async-generic-repository-pattern/</a></li><li><a href="https://stackoverflow.com/questions/33566075/generic-repository-in-asp-net-core-without-having-a-separate-addscoped-line-per">https://stackoverflow.com/questions/33566075/generic-repository-in-asp-net-core-without-having-a-separate-addscoped-line-per</a></li><li><a href="https://stackoverflow.com/questions/48874591/the-use-of-repository-and-unit-of-work-patterns-revisited-in-ef-core-with">https://stackoverflow.com/questions/48874591/the-use-of-repository-and-unit-of-work-patterns-revisited-in-ef-core-with</a></li><li><a href="https://stackoverflow.com/questions/43087821/how-to-add-a-generic-dependency-injection/43094684#43094684">https://stackoverflow.com/questions/43087821/how-to-add-a-generic-dependency-injection/43094684#43094684</a></li><li><a href="https://www.c-sharpcorner.com/article/generic-repository-pattern-in-asp-net-core/">https://www.c-sharpcorner.com/article/generic-repository-pattern-in-asp-net-core/</a></li><li><a href="https://medium.com/bynder-tech/c-why-you-should-use-configureawait-false-in-your-library-code-d7837dce3d7f">https://medium.com/bynder-tech/c-why-you-should-use-configureawait-false-in-your-library-code-d7837dce3d7f</a></li></ul>
<!-- /wp:list -->
