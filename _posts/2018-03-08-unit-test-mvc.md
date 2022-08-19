---
layout: post
title: Unit test & MVC Testing
date: 2018-03-08 14:22
author: tmasabari
comments: true
categories: [Interview Preparation, Unit Test, Unit Test]
---
<h2>Background</h2>
The intention of this article is to collect the notes on ‘Unit testing for MVC’ and include my own experiences as quick refresh guide.
<h2>Basics</h2>
<h3>Unit Testing</h3>
<ul>
 	<li>A unit test focuses on a single “<strong>unit of code</strong>” – usually a <strong>function in an object or module</strong>.</li>
 	<li>By making the test specific to a single function, the test should be simple, quick to write, and quick to run.</li>
 	<li>The basic pieces of a unit test are there: Individual tests, which test one thing, and they are isolated from each other.</li>
 	<li><strong>A unit test should be isolated from dependencies</strong> – for example, <strong>no network access, no storage access and no database access</strong>. There are tools that can replace these dependencies with <strong>fakes</strong> you can control. This makes it <strong>trivial</strong> to test all kinds of scenarios that would otherwise require a <strong>lot of setup</strong>.</li>
</ul>
<h3><strong>What Is Unit Testing?</strong></h3>
<span class="ans"><strong>Answer :</strong></span>

Unit testing is validation and verification methodology where the developers test the individual units of source code. Some key points to be remembered from: -
<ul>
 	<li>A unit is the smallest part in the application which can be tested. So it can be either a method. Function or class.</li>
 	<li>These tests are conducted during development.</li>
 	<li>Unit test belongs to the white box testing category.</li>
</ul>
<h3>Requirements</h3>
In order to implement unit test, the production code should follow below.
<ul>
 	<li><strong>SOLID principles</strong> - software that can be broken down easily into small parts, it becomes easier to test</li>
 	<li><strong>Loose coupling</strong> - allow its independent parts to be tested in isolation.
<ul>
 	<li>Classes needs to be <strong>interact with other classes via interfaces only</strong></li>
</ul>
</li>
 	<li><strong>Dependency injection</strong>
<ul>
 	<li>this in conjunction with interfaces will help you swap parts at will to isolate the modules you want to test.</li>
</ul>
</li>
</ul>
<h3>Benefits</h3>
<ul>
 	<li>Old adage, "Better (Quality / Less bugs), faster(less development time), cheaper(less developers), pick any two."</li>
 	<li>Good unit tests can help <strong>document and define</strong> what something is supposed to do</li>
 	<li>Unit Tests (automated) allows you to make big changes to code quickly.
<ul>
 	<li><strong>regression testing</strong> removes the fear of making changes to code as you can quickly check the modified code against the original requirements. This saves hours.</li>
 	<li><strong><em>merciless</em> refactoring</strong></li>
</ul>
</li>
 	<li>Teammates can look at them to see how to <strong>integrate</strong> other code with the unit</li>
 	<li>Unit tests help with <strong>code re-use</strong>. Migrate both your code and your tests to your new project. Tweak the code till the tests run again.</li>
</ul>
<h2>TDD Vs BDD</h2>
<h3><strong>TDD</strong></h3>
usually broken up into five different stages:
<ol>
 	<li>First the developer writes some tests.</li>
 	<li>The developer then runs those tests and (obviously) they fail because none of those features are actually implemented.</li>
 	<li>Next the developer actually implements those tests in code. Write the minimum amount of code required to make the test pass</li>
 	<li>Run the tests to check the new test passes</li>
 	<li>The developer can then refactor their code, add comments and clean it up, if the new code breaks something, then the tests will be an alert by failing.</li>
 	<li>Repeat from 1</li>
</ol>
<h3><a href="https://codeutopia.net/blog/2015/03/01/unit-testing-tdd-and-bdd/">BDD</a></h3>
<strong>BDD is meant to eliminate issues that TDD might cause.</strong>
<ul>
 	<li>Behavior-driven development borrows the concept of the <i>ubiquitous language</i> from <a href="https://en.wikipedia.org/wiki/Domain_driven_design">domain driven design</a>. A ubiquitous language is a (semi-)formal language that is shared by all members of a software development team — both software developers and non-technical personnel.</li>
 	<li>l BDD is <b>more than TDD</b> because it focuses on collaborating with business people. l BDD was originated by practitioners of <a href="http://c2.com/cgi/wiki?ExtremeProgramming"><u>eXtreme Programming</u></a> (XP) who were looking for a way to involve all perspectives (including BA and QA) in conversations about what to build.</li>
</ul>
<h4>User Story</h4>
Each user story should, in some way, follow the following structure:<a href="#cite_note-BDD_JW-2">[2]</a><a href="#cite_note-WhatStory-12">[12]</a>

<b>Title: The story should have a clear, explicit title.</b><b></b>

<b>Narrative</b><b></b>

A short, introductory section that specifies
<ul>
 	<li>· who: (which business or project role) is the driver or primary stakeholder of the story (the actor who derives business benefit from the story)</li>
 	<li>· what: effect the stakeholder wants the story to have</li>
 	<li>· why: business value the stakeholder will derive from this effect</li>
</ul>
<b>Acceptance criteria or scenarios</b><b></b>
<ul>
 	<li>a description of each specific case of the narrative. Such a scenario has the following structure:</li>
 	<li>· It starts by specifying the initial condition that is assumed to be true at the beginning of the scenario. This may consist of a single clause, or several.</li>
 	<li>· It then states which event triggers the start of the scenario.</li>
 	<li>· Finally, it states the expected outcome, in one or more clauses.</li>
</ul>
<h4>BDD Testing</h4>
<ul>
 	<li>In contrast to TDD, BDD is when we write <em>behavior &amp; specification</em> that then drives our software development. Behavior &amp; specification might seem awfully similar to tests but the difference is very subtle and important.</li>
</ul>
<ol>
 	<li>It is useful in business environments, where work that is done by programmers needs to be mapped to business value.
<ol>
 	<li>Business value is mapped by features, and hopefully features that don't introduce bugs. There are many strategies for mapping features to programming tasks, but one of them is through requirements. In my experience, requirements range from user-level requirements all the way down to small tasks for the user to execute.</li>
 	<li>This is useful because <strong>it's easy for the managers to understand how the work the programmer is doing is impacting their customers/users, and therefore why the programmers are adding value to their business</strong></li>
 	<li>The main difference is just the wording. BDD uses a more verbose style so that it can be read almost like a sentence.</li>
</ol>
</li>
 	<li>The ability to read your tests like a sentence is a cognitive shift in how you will think about your tests. The argument is that if you can read your tests fluidly, you will <em>naturally</em>write better and more comprehensive tests.</li>
</ol>
<h2>Pattern</h2>
in BDD, The essential idea is to break down writing a scenario (or test) into three sections:
<ul>
 	<li>The <b>given</b> part describes the state of the world before you begin the behavior you're specifying in this scenario. You can think of it as the pre-conditions to the test.</li>
 	<li>The <b>when</b> section is that behavior that you're specifying.</li>
 	<li>Finally the <b>then</b> section describes the changes you expect due to the specified behavior</li>
</ul>
<a href="http://www.typemock.com/unit-test-patterns-for-net#aaa">Arrange-Act-Assert (AAA) Pattern</a> Equivalent to GWT (Given-When-Then) of BDD
<ul>
 	<li><strong>Arrange: </strong>
<ul>
 	<li>setup preconditions needed for the running the tested code.</li>
 	<li>This includes any creation of <strong>dependent objects, mocks and data</strong> needed for the test to run.</li>
</ul>
</li>
 	<li><strong>Act: </strong>
<ul>
 	<li>Invoke the code under test.</li>
 	<li>Capture the result</li>
</ul>
</li>
 	<li><strong>Assert:</strong>
<ul>
 	<li>Specify the pass criteria for the test, which fails it if not met.
<ul>
 	<li>Values directly returned from the method</li>
 	<li>Values exposed through the object fields</li>
 	<li>Values exposed through other methods or properties of the object</li>
 	<li>Values that come from outside the object, for example static state or a shared data structure.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3><strong>When Are Unit Tests Written In Development Cycle?</strong></h3>
<span class="ans"><strong>Answer :</strong></span>

Tests are written before the code during development in order to help coders write the best code. Test-driven development is the ideal way to create a bug free code. When all tests pass, you know you are done! Whenever a test fails or a bug is reported, we must  first write the necessary unit test(s) to expose the bug(s), and then fix them. This makes it almost impossible for that particular bug to resurface later.
<h3><strong>What Are The Different Ways By Which You Can Do Unit Testing With .net?</strong></h3>
<span class="ans"><strong>Answer :</strong></span>

There are 2 primary / accepted ways of doing unit testing:-
<ul>
 	<li>NUNIT</li>
 	<li>Visual studio team edition test system</li>
</ul>
<h3><strong>How Can We Do Unit Testing </strong></h3>
In order to create a function which will execute our unit test you need to attribute the function with “[TestMethod]”. If you remember in Nunit it was ‘[Test]’. The assert function does not change.

Once you have done the unit testing coding compile the same, click on test, run and select ‘Tests in the current context”.
<h3><strong>How Can We Do Coverage Testing Using Vsts?</strong></h3>
<span class="ans"><strong>Answer :</strong></span>

Code coverage is a 3 steps process as shown below. The first step is to enable code coverage. So right click on the ‘.testrunconfig’ file in the solution explorer.

The next step is to select the assembly / DLL which we want to monitor for code coverage.

Once you run the test, right click on the test results and select code coverage results. You will be shown a details result.
<h4>The TestCase Attribute</h4>
NUnit provides a feature called <a href="http://nunit.org/index.php?p=parameterizedTests&amp;r=2.5">Parameterized Tests</a>. These provide two mechanisms that allow you to easily run the same test with multiple input data.

The first of these is the <a href="https://github.com/nunit/docs/wiki/TestCase-Attribute">[TestCase]</a> attribute. This replaces the [Test] attribute we used before, and provides input data to pass to the test method via parameters:

<img class="wp-image-1293  alignright" style="font-size: 1rem; font-family: Dosis, sans-serif; font-weight: bold;" src="/wp-content/uploads/2018/03/img_5ab7a7765e4ce.png" alt="" width="370" height="262" />
<div class="line number1 index0 alt2 highlighted"><code class="csharp plain">[TestCase(1, 0)]</code></div>
<div class="line number2 index1 alt1 highlighted"><code class="csharp plain">[TestCase(10, 5)]</code></div>
<div class="line number3 index2 alt2 highlighted"><code class="csharp plain">[TestCase(20, 10)]</code></div>
<div class="line number4 index3 alt1 highlighted"><code class="csharp plain">[TestCase(70, 5)]</code></div>
<div class="line number5 index4 alt2 highlighted"><code class="csharp keyword">public</code> <code class="csharp keyword">void</code> <code class="csharp plain">CalculatePriceTest(</code><code class="csharp keyword">int</code> <code class="csharp plain">age, </code><code class="csharp keyword">decimal</code> <code class="csharp plain">expectedPrice)</code></div>
<div>Assert.AreEqual(expectedPrice, actualPrice);</div>
<div></div>
<div>
<h4>The TestCaseSource Attribute</h4>
<div class="line number1 index0 alt2 highlighted"><code class="csharp plain">[TestCaseSource(</code><code class="csharp string">"TestCases"</code><code class="csharp plain">)]</code></div>
<div class="line number2 index1 alt1"><code class="csharp keyword">public</code> <code class="csharp keyword">decimal</code> <code class="csharp plain">CalculatePriceTest(</code><code class="csharp keyword">int</code> <code class="csharp plain">age)</code></div>
</div>
<h2>Unit testing strategies</h2>
<ul>
 	<li>Testing void methods
<ul>
 	<li>As a guideline, given the option, we’d <strong>prefer state-based tests over interaction-based</strong> tests. Interaction-based tests require knowledge about the internal implementation of the method. Since they increase coupling, they are less robust than state-based tests. In addition, to understand the test failure, the reader needs to know more about the implementation, rather than interface, reducing readability. Most test frameworks don’t support <a id="a5" href="http://www.typemock.com/Best-ever_Introduction_to_Unit_Testing_-_free-webinar">interaction-based tests</a></li>
 	<li><code>public void ReportIfSpam(Message message)
{
if (message.IsSpam)
Administrator.SendEmail(message);
}</code></li>
 	<li><code>[TestMethod]
public void ReportIfSpam_MessageIsSpam_SendEmailToAdministrator()
{
Mailbox mailbox = new Mailbox();
Message spamMessage = new Message();
spamMessage.IsSpam = true; // Set message to be spam
Isolate.Fake.StaticMethods&lt;administrator&gt;(); // Fake sending the emails mailbox.ReportIfSpam(spamMessage); //Assert the call was made with the correct argument
Isolate.Verify.WasCalledWithExactArguments(() =&gt; Administrator.SendEmail(spamMessage));
}</code></li>
</ul>
</li>
 	<li>Testing Exceptions: Testing thrown exceptions depends on your test framework, each uses a different sub-pattern. NUnit and xUnit allow us to use APIs, that combine the Act and Assert parts. For example, in NUnit:</li>
 	<li><code><code>[Test]
public void ReportSpam_MessageIsSpam_ExceptionIsThrown()
{
Mailbox mailbox = new Mailbox();
Message spamMessage = new Message();</code></code>Assert.Throws&lt;spammessageexception&gt;(()=&gt;mailbox.ReportIfSpam());  }  &lt;/spammessageexception&gt;</li>
 	<li>Testing internal/private behaviour
<ul>
 	<li>Legacy code frequently includes code that needs testing, but is not exposed through a public interface. They may benefit from testing the algorithms directly, rather than through the object interface.</li>
 	<li>A classic example is a Balanced Binary Tree. In order to test that the tree is balanced , we will need to access a private interface.</li>
 	<li>Solutions
<ul>
 	<li>Making changes to the tested code</li>
 	<li>Explicitly change private methods to public</li>
 	<li>Exposing internal methods using the InternalVisibleToAttribute.</li>
 	<li>Accessing the internal members from the test</li>
 	<li>Using reflection</li>
 	<li>Using a other tools</li>
</ul>
</li>
</ul>
</li>
 	<li>Testing Code with external dependencies
<ul>
 	<li>When unit testing, often the tested code interacts with external dependencies. These dependencies can be other objects in the system, files, databases, frameworks or 3rd party libraries. In order to speed up our tests, and control the behavior of the dependencies, we would prefer to use mock objects.</li>
 	<li>A mocking framework allows you to create mock objects. Mock objects allow developers to emulate, through interfaces or virtual methods, the behavior of another class during testing and then verify that expected events occurred.</li>
 	<li>The behavior of mock objects (also simply called mocks) is what allows you to replace dependencies in your classes and then test those classes without having the real dependencies in place.</li>
</ul>
</li>
 	<li>There are still many situations in which these patterns are not sufficient and there is a need to change the code to make it testable. These include:
<ul>
 	<li>Singleton classes</li>
 	<li>Calls to static members</li>
 	<li>Objects that do not have an interface (as required for mock-object pattern)</li>
 	<li>Objects that are instantiated in the code being tested</li>
 	<li>Objects that are not passes to the method (as required for mock-object pattern).</li>
</ul>
</li>
</ul>
<h3>Unit Test and MVC Architecture</h3>
<ul>
 	<li>Model View Controller (MVC) pattern is inherently more testable than the Page Controller pattern (Web Froms)
<ul>
 	<li>it encourages <strong>separation</strong> of the application <strong>flow</strong> logic and the <strong>display logic</strong>. The logic that controls the flow of the application resides inside the controller classes</li>
 	<li>Allowing developers to replace or extend controller factories makes it possible to execute logic that can resolve and inject the dependencies of the controllers. Allowing for the dependencies of a controller to be injected at run time is key to creating more loosely coupled and testable applications.</li>
 	<li>The ASP.NET MVC team made the decision to wrap many of the .NET static helper classes (such as HttpContext and HttpRequest) so that they can be replaced during testing with a stub.</li>
 	<li>Testing Web Forms pages requires that you invoke the Web server and run the complete page pipeline. ASP.NET MVC has been architected for testability without dependencies on the IIS server, on a database, or on external classes.</li>
</ul>
</li>
 	<li>A service/Business layer sits on top of an application's domain model and provides a set of operations that can be performed against it. This gives you a place to centralize logic that belongs in your application but might not necessarily belong inside the domain model—logic that would have otherwise likely leaked into the controller's methods.
<ul>
 	<li>Inserting the service layer into the mix greatly reduces the coupling between the controller classes and the repository classes while keeping your controllers lighter because you can push a lot of logic into the services.</li>
 	<li>The design of the controller classes must be changed to reflect the use of services instead of repositories, so instead of injecting repositories into these classes, you inject the services.In turn, you inject the repositories into the services.</li>
 	<li>This might sound complicated, but with dependency injection, you won't even notice—it all gets wired up for you.</li>
</ul>
</li>
 	<li>Repository Layer - Implementations of the Repository pattern provide a view of your persistent storage that appears to be an in-memory repository.
<ul>
 	<li>The Repository pattern is often misinterpreted as a layer that sits between the application and a database, but in fact it is a layer that sits between your application and any sort of persistent storage.</li>
</ul>
</li>
 	<li>View Model
<ul>
 	<li>One good approach is to use the <a href="http://martinfowler.com/eaaDev/PresentationModel.html">presentation model pattern</a>. Presentation models can be <strong>mapped to and from domain objects and can hold view-specific logic and values</strong> that can easily be tested.</li>
 	<li>Fields from multiple domain objects can be placed in single view model.</li>
 	<li>you can add <strong>view-specific behavior to your class</strong> that can easily be unit tested.</li>
 	<li>Second, you can <strong>use the default model binders</strong> built into ASP.NET MVC and place your presentation model on the parameter list of a POST method. The alternative is to define mapping classes that you can use to map entities coming in through action method parameters to entities that you want to save to the database.</li>
</ul>
</li>
</ul>
<h2>MVC Testing strategy</h2>
<ul>
 	<li>ASP.NET MVC unit tests directly call methods of your MVC controllers.</li>
 	<li>When a unit test calls an action method in a controller, you can validate that the correct view is returned (although you do not validate the HTML) and that view data is returned. You can also test whether a method correctly redirects to another controller or view.</li>
 	<li>Controller Layer- Most of your unit testing is around the controller and action method. You write unit test to validate the output against a certain set of input to make sure your controller works fine.</li>
 	<li>Business Layer - If you have business logic in this layer, it makes sense to unit test it along with Controller, they are tied to controller anyway so it will get tested.</li>
 	<li>For unit test, most of the time I <strong>fake out the ORM layer</strong>. I don't think you can truly test them because they perform direct DB transaction.
For me most of the testing for repository layer is integration than unit.</li>
 	<li>Routing
<ul>
 	<li>It is important to ensure that the base route "~/" will forward to the appropriate controller and action, and that other controllers and actions forward correctly as well.</li>
 	<li>It is extremely important to have these tests in place from the beginning so that later, as more routes are added to your application, you are guaranteed that routes that were already defined are not broken.</li>
</ul>
</li>
 	<li>Test Controllers
<ul>
 	<li>The controllers can be instantiated from anywhere(even from tests) without the dependency of context</li>
 	<li><strong>For injections only</strong> Since the controller factory inherits from the default implementation, you just need to override the <strong>GetControllerInstance</strong> method and then request the type from the <strong>Ninject kernel</strong>, which is the class that controls object instantiation in Ninject. All this happens inside the dependency injection container simply by asking for the type.
<ol>
 	<li>When the kernel receives a controller type, Ninject self-binds (tries to construct) the type because it is a concrete type.</li>
 	<li>If the kernel receives a CategoryController type, the constructor will have a parameter of type ICategoryService.</li>
 	<li>Ninject looks to see if it has a binding for this type, and when it finds the type, it performs the same action, looking for a constructor.</li>
 	<li>The Ninject kernel instantiates a CategoryRepository and passes it to the constructor for ControllerService.</li>
 	<li>Then it passes the ControllerService object to the constructor for the CategoryController.</li>
</ol>
</li>
 	<li>The controller factory must be registered for it to work. Registration requires the addition of only a single line to the global.asax</li>
 	<li>
<pre>public void Application_Start() { 
// get the Ninject kernel for resolving dependencies 
kernel = CreateKernel(); // set controller factory for instantiating controller and injecting dependencies ControllerBuilder.Current.SetControllerFactory(new NinjectController Factory(kernel)); }</pre>
</li>
</ul>
</li>
 	<li>Test Views
<ul>
 	<li><strong>Don't format</strong> the code in view. instead have the format logic in view model
<span style="color: #339966;">&lt;%= Html.Encode(String.Format("{0:c}", this.Model.Price)) %&gt;</span></li>
</ul>
</li>
 	<li>Passing Dependencies of Actions as Parameters &amp; Mock HttpContext
<ul>
 	<li>Model binders are classes that implement the IModelBinder interface and provide a way for ASP.NET MVC to instantiate types on action methods.</li>
 	<li>The model binder has access to both the controller's context and a binding context.</li>
 	<li>
<pre>[AcceptVerbs(HttpVerbs.Post)] 
public ActionResult Edit(int id, ViewProduct viewProduct, <span style="color: #ff0000;">HttpServerUtilityBase server</span>, HttpPostedFileBase imageFile) {</pre>
</li>
 	<li>
<pre>public class HttpServerModelBinder: IModelBinder { 
public object BindModel(ControllerContext controllerContext, ModelBindingContext bindingContext) { return controllerContext.HttpContext.Server; } }</pre>
</li>
 	<li>
<pre>public void Application_Start() { 
// assign model binder for passing in the HttpServerUtilityBase to controller actions ModelBinders.Binders.Add(typeof(HttpServerUtilityBase), new HttpServerModelBinder()); }</pre>
</li>
</ul>
</li>
 	<li>Test Results
<ul>
 	<li>Controller results descend from the ActionResult class and represent a task that the action is going to perform. Developer can choose inbuilt or custom ActionResult</li>
 	<li><code>    // Arrange
var controller = new AboutController();
// Act
var result = controller.Index();
// Assert
Assert.<span style="color: #0000ff;">IsInstanceOfType</span>(result, <span style="color: #0000ff;">typeof(ViewResult)</span>);
var viewResult = result as ViewResult;</code>
<code>    Assert.AreEqual(<span style="color: #0000ff;">typeof(AboutViewModel</span>), viewResult);</code></li>
 	<li>
<pre>public ActionResult List() { IEnumerable&lt;Category&gt; categories = categoryService.FindAll(); return View(ViewCategory.MapList(categories)); }</pre>
</li>
 	<li>
<pre>[Fact] public void ListActionReturnsViewResultWithDefaultName() { // Arrange 
var mockService = new Mock&lt;ICategoryService&gt;(); 
var controller = new CategoryController(mockService.Object); // Act var result = controller.List(); 
// Assert var viewResult = Assert.IsType&lt;ViewResult&gt;(result); Assert.Empty(viewResult.ViewName); 
}</pre>
</li>
 	<li>It would be very easy to test the view name against some known string value, or</li>
 	<li>in cases where the return type is something a bit more complex (JSON format, for example), to check the Data property on the result to ensure that it contains the expected information as returned by a call to the action method.</li>
 	<li>ViewBag can be monitored result.ViewBag.&lt;property&gt;</li>
 	<li>The Model passed from controller to the view can be tested by result.Model</li>
</ul>
</li>
 	<li>UrlHelpers
<ul>
 	<li>UrlHelpers are great for cataloging your web application with Urls. We expect a string returned based on parameters passed into the UrlHelper.</li>
</ul>
</li>
 	<li>HtmlHelpers
HtmlHelpers are used for returning properly-formatted HTML snippets of code. The behavior we are expecting back is properly-formatted HTML based on criteria passed into the helper.</li>
</ul>
<ul>
 	<li style="list-style-type: none;"></li>
</ul>
<h3>Tools &amp; Frameworks</h3>
<ul>
 	<li>third-party test frameworks such as NUnit, MbUint, or XUnit, and with third-party mock-object libraries such as Rhino mocks, Type mocks, or NMock</li>
 	<li>xUnit provides a way to run automated unit tests.
<ul>
 	<li>it is simple, easily extended, and has a very clean syntax</li>
</ul>
</li>
 	<li>A testing framework such as MSTest or NUnit can still execute integration tests, but they test multiple layers of the application, including making calls across the network, accessing the disk, persisting data to a database, and so on.
<ul>
 	<li>These sorts of tests are very important and should be present in all applications, but as an application grows, these tests become very slow and can be brittle on different developer machines.</li>
 	<li>Separating unit tests and integration tests allows you to run the unit tests quickly and reliably on developer machines while running your integration tests regularly on your build server.</li>
</ul>
</li>
 	<li>Dependency Injection Framework. <a href="http://ninject.org/">Ninject 2</a> by Nate Kohari. Ninject provides a way to wire up classes in your application.</li>
 	<li>Mocking Framework. <a href="http://code.google.com/p/moq">Moq by Clarius Consulting</a>. Moq provides a framework for mocking interfaces and classes during testing.</li>
 	<li>MSTest
<ul>
 	<li>Test cases are identified using attributes. [TestClass] and [TestMethod]</li>
</ul>
</li>
</ul>
<h2>References</h2>
<ol>
 	<li>https://msdn.microsoft.com/en-us/magazine/dd942838.aspx</li>
 	<li>http://www.typemock.com/unit-test-patterns-for-net</li>
 	<li>https://stackoverflow.com/questions/67299/is-unit-testing-worth-the-effort</li>
 	<li>https://stackoverflow.com/questions/3840125/useful-design-patterns-for-unit-testing-tdd</li>
 	<li>https://stackify.com/unit-testing-basics-best-practices/</li>
 	<li>https://codeutopia.net/blog/2015/03/01/unit-testing-tdd-and-bdd/</li>
 	<li>https://joshldavis.com/2013/05/27/difference-between-tdd-and-bdd/</li>
 	<li>https://xp123.com/articles/3a-arrange-act-assert/</li>
 	<li>https://softwareengineering.stackexchange.com/questions/308160/differences-between-given-when-then-gwt-and-arrange-act-assert-aaa</li>
 	<li>https://martinfowler.com/bliki/GivenWhenThen.html</li>
 	<li><span style="color: #ff0000;">Todo http://aut.tigris.org/</span></li>
 	<li>https://www.danylkoweb.com/Blog/the-ultimate-guide-to-unit-testing-in-aspnet-mvc-E2</li>
 	<li>http://www.typemock.com/unit-test-patterns-for-net</li>
 	<li><a href="https://msdn.microsoft.com/en-us/library/cc514239.aspx#Contents">Common Test Patterns and Reuse of Test Designs</a></li>
 	<li><a href="https://raygun.com/blog/unit-testing-patterns/">common patterns to follow for error free applications</a></li>
 	<li><a href="http://blog.aspiresys.com/testing/design-patterns-in-test-automation-world/">Design Patterns In Test Automation World</a></li>
 	<li>https://app.pluralsight.com/player?author=scott-allen&amp;name=mvc4-building-m9-tests&amp;mode=live&amp;clip=4&amp;course=mvc4-building</li>
</ol>
