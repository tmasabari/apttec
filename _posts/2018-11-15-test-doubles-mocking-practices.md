---
layout: post
title: Test doubles/Mocking practices
date: 2018-11-15 17:27
author: tmasabari
comments: true
categories: [Mock, Test Doubles, Testing, Unit Test]
---
<!-- wp:heading {"level":3} -->
<h3>Test doubles</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Test Double is a generic term for any case where you replace a production object for testing purposes. There are various kinds of double are:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><strong>Dummy</strong>&nbsp;objects are passed around but never actually used. Usually they are just used to fill parameter lists.</li><li><strong>Fake</strong>&nbsp;objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an&nbsp;<a href="https://martinfowler.com/bliki/InMemoryTestDatabase.html">InMemoryTestDatabase</a>&nbsp;is a good example).</li><li><strong>Stubs</strong>&nbsp;provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test.</li><li><strong>Spies</strong>&nbsp;are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.</li><li><strong>Mocks</strong>&nbsp;are pre-programmed with expectations which form a <strong>specification of the calls they are expected to receive</strong>.
<ul><li>They can throw an exception if they receive a call they don't expect and are checked during verification to ensure they got all the calls they were expecting.</li><li>
Mocks interact with the code being tested by means of interfaces. This means that in order to use mocks for testing, you <strong>must write code that is fully interface-compliant.</strong>
</li><li>
A mock stands in for the object which it represents. From the point of view of the unit being tested, there should be no difference between a mock and the actual object.
</li><li>
A mock, however, does not need to duplicate the internal operations of the object that it represents. Instead, it <strong>can return hard-coded responses</strong> (always sending back "True" or "Smith, J.Q.," for example), or
</li><li>
it can contain logic designed to test the unit in more sophisticated ways (by using assertions, or by emulating complex behavior on the part of a client, for instance).
</li></ul>
</li></ul>
<!-- /wp:list -->

<h2>Mock VS Fake/Shim</h2>
<ol>
<li>
<p>Your architecture should make proper use of stubs, mocks and dependency injection, rather than relying on the crutch of Fakes and mocks.</p>
</li>
<li>Shims are slower (because the fake assemblies need to be generated), and it takes more coding effort to match the functionality that you get with mocking framework. </li>
<li>
<p>Fakes and mocks are useful for testing code you shouldn't or can't change, such as:</p>
<ul>
<li>Legacy code that does not make use (or efficient use) of stubs</li>
<li>class that I don't have access to implement an interface
<ul>
<li>3rd party APIs</li>
<li>Resources for which you have no source code</li>
</ul>
</li>
<li>shared/static method</li>
<li>Performance of the piece of code is critical and memory availability is very less like IoT, where DI or additional code can't be applied</li>
</ul>
</li>
</ol>
<p> </p>
<h3>Mock, Stub Vs Shims</h3>
<ul>
<li>A stub is also interface-based and is in many other ways similar to a mock.</li>
<li>If the target resource is <strong>not fully interface-compliant,</strong> you must use a shim rather than a mock or stub. A shim functions much like a stub, returning set values and testing against assertions.</li>
<li>Shims are used mainly to test the untestable code. You find more of these code third party components that contains lots of statics, privates etc. Often this implies there is some <em>code smell</em>. It is recommended to use Stubs, because the virtual types are extendable, replaceable and easily testable. The other aspect is that if you see the code that is hard to test, and you have no confidence of changing code, you can use Shims to write integration type tests and refactor the code incrementally to make the code testable.</li>
<li>
<p>Fakes come in two flavors:</p>
</li>
<li>
<p>A <a href="https://docs.microsoft.com/en-us/visualstudio/test/isolating-code-under-test-with-microsoft-fakes?view=vs-2017#get-started-with-stubs" data-linktype="self-bookmark">stub</a> replaces a class with a small substitute that implements the same interface. To use stubs,<strong> you have to design your application so that each component depends only on interfaces</strong>, and not on other components. (By "component" we mean a class or group of classes that are designed and updated together and typically contained in an assembly.)</p>
</li>
<li>
<p class="">A <a href="https://docs.microsoft.com/en-us/visualstudio/test/isolating-code-under-test-with-microsoft-fakes?view=vs-2017#get-started-with-shims" data-linktype="self-bookmark">shim</a> modifies the compiled code of your application at run time so that instead of making a specified method call, it runs the shim code that your test provides. Shims can be used to replace calls to assemblies that you cannot modify, such as .NET assemblies.</p>
</li>
<li>
<p id="JSzwzrl"><img class="alignnone size-full wp-image-1770 " src="/wp-content/uploads/2018/10/img_5bd312997a159.png" alt="" /></p>
</li>
</ul>
<p><!-- /wp:paragraph --><!-- wp:heading --><!-- /wp:list --><!-- wp:heading --></p>

<!-- wp:paragraph -->
<p><a href="http://www.typemock.com/unit-test-patterns-part-ii/"><strong>Isolation Technology: How does it work?</strong></a><br>Typemock Isolator uses uses&nbsp;the&nbsp;<strong>.NET Framework profiler API</strong>&nbsp;to intercept and monitor an application’s execution. When a method is loaded by the CLR for the test process, Typemock Isolator retrieves the IL and weaves in instrumented IL code.&nbsp;Typemock Isolator does not change the original IL code – it simply inserts new code that checks if the method should be faked, and with which behavior. With this technology, Typemock Isolator can do powerful stuff:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Fake any .Net code, including framework objects like SharePoint and ASP.Net.</li><li>Can return fake values, ignore, throw an exception or even run custom code when a method is called.</li><li>Return Recursive Fakes that fake full object trees in a single line.</li><li>Tests require short setup, and are more readable</li><li>Tests are robust, and don’t break easily because of production code changes.</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Code weaving</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>The main difference between code weaving and the open-source library's is that code weaving uses the Profiler API provided by Microsoft instead of a&nbsp;<a href="http://www.castleproject.org/dynamicproxy/index.html">dynamic proxy</a>. This allows TypeMock to mock concrete classes and static methods.</li><li>In case you aren't sure what the profiler is, it is the same API that is used by tools like JetBrain's dotTrace and RedGate's Ants .Net profilers. TypeMock just uses the API in a different way to fake(mock) what you tell it to.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>There are three frameworks to my knowledge that allow you to mock non virtual methods and sealed classes like Fakes' Shims. There are</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Microsofts' Fakes
<ul><li>All the developers needs to have VS Enterprise edition. <br>References <a href="https://visualstudio.uservoice.com/forums/330519-azure-devops-formerly-visual-studio-team-services/suggestions/3619488-provide-microsoft-fakes-with-all-visual-studio-edi">1</a>, <a href="https://social.msdn.microsoft.com/Forums/vstudio/en-US/5972a514-3c75-4a09-a48b-43d48b023a9d/fakesdll-can-be-referenced-in-vs-professional-and-updated-?forum=vsunittest">2</a></li></ul>
</li><li>Teleriks&nbsp;<a href="http://www.telerik.com/justmock%22JustMock%22">JustMock</a></li><li><a href="http://www.typemock.com/%22TypeMocks%22">TypeMocks</a></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Freeware</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://github.com/urasandesu/Prig">Prig</a></li><li><a href="https://www.microsoft.com/en-us/research/project/moles-isolation-framework-for-net/">Moles</a>&nbsp;&amp; <a href="https://www.microsoft.com/en-us/research/project/pex-and-moles-isolation-and-white-box-unit-testing-for-net/">Pex</a>&nbsp;(deprecated and cannot be used)</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Code weaving libraries can address below <a href="https://www.telerik.com/justmock/free-mocking">scenarios</a></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>MsCorlib Mocking</li><li>Elevated Silverlight Mocking</li><li>SharePoint Mocking</li><li>OpenAccess Mocking</li><li>Entity Framework Mocking</li><li>Final Mocking</li><li>Sealed Mocking</li><li>Static Mocking</li><li>Partial Mocking</li><li>Mocking Non-public Members and Types</li><li>Mocking LINQ Queries</li><li>Threadpool Mocking</li><li>Extension Methods Mocking</li><li>Private Accessor</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><a href="https://martinfowler.com/bliki/TestDouble.html">https://martinfowler.com/bliki/TestDouble.html</a></li><li><a href="https://github.com/powermock/powermock/wiki/Motivation">https://github.com/powermock/powermock/wiki/Motivation</a></li><li><a href="https://dzone.com/articles/mock-frameworks-vs-microsoft-fakes">https://dzone.com/articles/mock-frameworks-vs-microsoft-fakes</a></li><li><a href="https://stackoverflow.com/questions/9677445/mock-framework-vs-ms-fakes-frameworks">https://stackoverflow.com/questions/9677445/mock-framework-vs-ms-fakes-frameworks</a></li></ul>
<!-- /wp:list -->
