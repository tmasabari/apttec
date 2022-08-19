---
layout: post
title: Writing Testable Code:Design -From Google testing blog
date: 2018-10-31 17:37
author: tmasabari
comments: true
categories: [Architecture, Design, Unit Test]
---
<!-- wp:heading -->
<p><a href="https://testing.googleblog.com/">https://testing.googleblog.com/</a></p>
<ul>
<li><a href="http://misko.hevery.com/2008/08/25/root-cause-of-singletons/">Global state is bad</a> and how it makes your application <a href="http://misko.hevery.com/2008/08/17/singletons-are-pathological-liars/">hard to understand</a>.</li>
<li><a href="http://misko.hevery.com/2008/07/08/how-to-think-about-the-new-operator/">how to think about the new operator</a>, and <a href="http://misko.hevery.com/code-reviewers-guide/flaw-constructor-does-real-work/">class does real work</a> </li>
<li><a class="foreign" href="http://stackoverflow.com/questions/137975/what-is-so-bad-about-singletons">What is so bad about singletons?</a></li>
</ul>
<h2>Testable code summary <a href="http://misko.hevery.com/attachments/Guide-Writing%20Testable%20Code.pdf">PDF Book</a></h2>
<p><a href="http://misko.hevery.com/code-reviewers-guide/flaw-constructor-does-real-work/">Flaw #1: Constructor does Real Work</a></p>
<p align="left"><strong>Warning Signs</strong></p>
<ul>
<li>new keyword in a constructor or at field declaration</li>
<li>Static method calls in a constructor or at field declaration</li>
<li>Anything more than field assignment in constructors</li>
<li>Object not fully initialized after the constructor finishes (watch out for initialize methods)</li>
<li>Control flow (conditional or looping logic) in a constructor</li>
<li>Code does complex object graph construction inside a constructor rather than using a factory or builder</li>
<li>Adding or using an initialization block</li>
</ul>
<p align="left"><a href="http://misko.hevery.com/code-reviewers-guide/flaw-digging-into-collaborators/">Flaw #2: Digging into Collaborators</a></p>
<p align="left"><strong>Warning Signs</strong></p>
<ul>
<li>Objects are passed in but never used directly (only used to get access to other objects)</li>
<li>Law of Demeter violation: method call chain walks an object graph with more than one dot (.)</li>
<li>Suspicious names: context, environment, principal, container, or manager</li>
</ul>
<p align="left"><a href="http://misko.hevery.com/code-reviewers-guide/flaw-brittle-global-state-singletons/">Flaw #3: Brittle Global State &amp; Singletons</a></p>
<p align="left"><strong>Warning Signs</strong></p>
<ul>
<li>Adding or using singletons</li>
<li>Adding or using static fields or static methods</li>
<li>Adding or using static initialization blocks</li>
<li>Adding or using registries</li>
<li>Adding or using service locators</li>
</ul>
<p align="left"><a href="http://misko.hevery.com/code-reviewers-guide/flaw-class-does-too-much/">Flaw #4: Class Does Too Much</a></p>
<p align="left"><strong>Warning Signs</strong></p>
<ul>
<li>Summing up what the class does includes the word “and”</li>
<li>Class would be challenging for new team members to read and quickly “get it”</li>
<li>Class has fields that are only used in some methods</li>
<li>Class has static methods that only operate on parameters</li>
</ul>
<p>&nbsp;</p>
<h2>You can not use new keyword in your core / business logic</h2>
<ul>
<li>Unit Testing as the name implies asks you to test a Class (Unit) in isolation.</li>
<li>If your code mixes Object Construction with Logic you will never be able to achieve isolation.</li>
<li>In order to unit-test you need to separate object graph construction from the application logic into two different classes</li>
<li>The end goal is to have either: classes with logic OR classes with “new” operators.</li>
</ul>
<p>&nbsp;</p>
<h2>private static methods - Allowed recommended</h2>
<ul>
<li>A <code>private static</code> method by itself does not violate OOP per se, but when you have a lot of these methods on a class that don't need (and cannot*) access instance fields, you are not programming in an OO way, because "object" implies state + operations on that state defined together.</li>
<li>As mentioned above, private static methods are often useful for organizing re-used logic and reducing/eliminating repeated code.</li>
<li>Performance of static methods are high compare to instance methods.</li>
</ul>
<p>&nbsp;</p>
<p><a href="https://stackoverflow.com/questions/685522/using-private-static-methods">https://stackoverflow.com/questions/685522/using-private-static-methods</a></p>
<h2>Prefer sub classes and extension methods over static classes</h2>
<p>&nbsp;</p>
<h2>Static Helper Classes</h2>
<p><a href="https://blogs.msdn.microsoft.com/nickmalik/2005/09/06/are-helper-classes-evil/">https://blogs.msdn.microsoft.com/nickmalik/2005/09/06/are-helper-classes-evil/</a></p>
<p><a href="https://stackoverflow.com/questions/3339929/if-a-utilities-class-is-evil-where-do-i-put-my-generic-code">https://stackoverflow.com/questions/3339929/if-a-utilities-class-is-evil-where-do-i-put-my-generic-code</a></p>
<p><a href="http://www.ralin.net/blog/oop-anti-patterns-utility-or-helper-classes.html">http://www.ralin.net/blog/oop-anti-patterns-utility-or-helper-classes.html</a></p>
<p><a href="https://stackoverflow.com/questions/241339/when-to-use-static-classes-in-c-sharp">https://stackoverflow.com/questions/241339/when-to-use-static-classes-in-c-sharp</a></p>
<p><a href="https://stackoverflow.com/questions/205689/class-with-single-method-best-approach">https://stackoverflow.com/questions/205689/class-with-single-method-best-approach</a></p>
<ul>
<li>Based on this set of OOP criteria, it is fairly clear that helper classes fail to work well with two out of the five fundamental principles that we are trying to achieve with Object Oriented Programming. </li>
<li>Generally, <code>Utils</code> and <code>Helper</code> type classes should be avoided. More often than not, you will find that what you may <em>think</em> is a utility method, is actually a rather specific method that probably belongs in a class of its own (just like you say). However, there will be domain specific cases where <code>Util</code>-like classes (classes which group related useful methods) are valid entities.</li>
</ul>
<p>A static helper class is a collection of related static methods. (They ought to be related, anyway.) For example, I have a <strong>DatabaseHelper </strong>class in my library of test utilities with methods like <strong>CreateDatabase</strong>, <strong>DropDatabase</strong>, and <strong>ExecuteScalar</strong>. Each one is just a convenience method that wraps up a few lines of code, saving me from having to repeat it.</p>
<p>Static helper classes are a very humble design element. They hide no data, do not inherit anything, and do not implement an interface. They are just there to help. <em>There is nothing wrong with that</em>, provided they are organized and cohesive.</p>
<h2>Extension Methods</h2>
<p>In effect, extension methods let you add methods to a class even if you don't have the source for that class. But they do more than that: you can <strong>add methods to an interface, to a built-in type, even to an enum.</strong></p>
<h2>Guidelines for Extension Methods</h2>
<p>Cwalina and Abrams' book, <a title="Amazon.com: Framework Design Guidelines" href="http://www.amazon.com/Framework-Design-Guidelines-Conventions-Libraries/dp/0321545613/ref=sr_1_1?ie=UTF8&amp;qid=1340741058&amp;sr=8-1&amp;keywords=framework+design+guidelines" target="_blank" rel="noopener">Framework Design Guidelines</a>, offers these rules for extension methods.</p>
<ul>
<li>Allow you to avoid polluting the core API of a class,</li>
<li>if the extended type later adds an instance method of the same name which is applicable with the same parameters, <strong>your calling code will transparently start calling that instance method next time you recompile</strong>. For example, <code>Stream</code> gained <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.copyto.aspx" rel="noreferrer"><code>CopyTo</code></a> in .NET 4... I'd previously written a <code>CopyTo</code> extension method, which then wouldn't be called. There's no warning that this is occurring, so you have to be on your guard.</li>
<li>Extension methods simply shouldn't be considered an alternative for class methods; but rather as a way to give otherwise syntactically ugle <strong>static</strong> methods a "class methody" look and feel.</li>
<li>Extension methods allow for a method chaining coding style; which has become more popular lately, as opposed to the more vanilla method wrapping syntax. Similar syntactical preferences can be seen in LINQ's method syntax.</li>
<li>Not only allow method-chaining style, but allow it to more flexibly handle <code>null</code> values since an extension method called from a <code>null</code> value simply receives the <code>null</code> as its first argument,</li>
<li>Prevent you from accidentally accessing/modifying private/protected state in a method that shouldn't have access to it</li>
<li>Extension methods have one more benefit: they can still be used as a static method, and can be <strong>passed directly as a value to a higher order function</strong>. So if <code>MyMethod</code> is an extension method, instead of say, <code>myList.Select(x =&gt; x.MyMethod())</code>, you could simply use <code>myList.Select(MyMethod)</code>. I find that nicer.</li>
<li>Avoid frivolously defining extension methods, especially <strong>on types you don't own</strong>.</li>
<li>Consider extension methods to <strong>provide functionality to every implementation of an interface</strong>. LINQ's extensions on <strong>IEnumerable&lt;T&gt;</strong> are an example.</li>
<li>Consider extension methods to avoid dependencies you don't want.
<ul>
<li>You don't want the <strong>String</strong> class to depend on<strong> System.Uri</strong>, but you could extend<strong> String</strong> with a <strong>ToUri </strong>method that converts the string to a <strong>Uri</strong>.</li>
</ul>
</li>
</ul>
<p><a href="https://softwareengineering.stackexchange.com/questions/371868/when-to-write-extension-methods-for-your-own-classes">https://softwareengineering.stackexchange.com/questions/371868/when-to-write-extension-methods-for-your-own-classes</a></p>
<p><a href="http://www.fascinatedwithsoftware.com/blog/post/2012/06/26/Extension-Methods-and-Helper-Classes-as-Design-Elements.aspx">http://www.fascinatedwithsoftware.com/blog/post/2012/06/26/Extension-Methods-and-Helper-Classes-as-Design-Elements.aspx</a></p>
<p><a href="https://stackoverflow.com/questions/4646328/extension-methods-vs-static-utility-class?noredirect=1&amp;lq=1">https://stackoverflow.com/questions/4646328/extension-methods-vs-static-utility-class?noredirect=1&amp;lq=1</a></p>
<h2>Static classes</h2>
<ul>
<li>“So leaf methods are ok to be static but other methods should not be?” I like to go a step further and <strong>simply say, static methods are not OK</strong>.</li>
<li>The issue is that a methods starts off being a leaf and over time more and more code is added to them and t<strong>hey lose their positions as a leafs</strong>. It is way to easy to turn a leaf method into none-leaf method, the other way around is not so easy.</li>
<li>Therefore a static leaf method is a slippery slope which is waiting to grow and become a problem.</li>
<li><strong>Static methods are procedural!</strong> I<strong>n OO language stick to OO</strong>. And as far as Math.abs(-5) goes, I think Java got it wrong. I really want to write -5.abs(). Ruby got that one right.</li>
</ul>
<p>&nbsp;</p>
<h2>Singleton</h2>
<ol>
<li>
<p>They are generally used as a global instance, why is that so bad? Because you hide the dependencies of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a <a href="https://en.wikipedia.org/wiki/Code_smell" rel="noreferrer">code smell</a>.</p>
</li>
<li>
<p>They violate the <a href="https://en.wikipedia.org/wiki/Single_responsibility_principle" rel="noreferrer">single responsibility principle</a>: by virtue of the fact that they control their own creation and lifecycle.</p>
</li>
<li>
<p>They inherently cause code to be tightly <a href="https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29" rel="noreferrer">coupled</a>. This makes faking them out under test rather difficult in many cases.</p>
</li>
<li>
<p>They carry state around for the lifetime of the application. Another hit to testing since you can end up with a situation where tests need to be ordered which is a big no no for unit tests. Why? Because each unit test should be independent from the other.</p>
</li>
<li>Difficult to parallelize in the case of mutable state (requires extensive locking);</li>
</ol>
<p>&nbsp;</p>
<ol>
<li>
<p>Singletons solve one (and only one) problem: <strong>Resource Contention. </strong>If you have some resource that: (<strong>1</strong>) can only have a single instance, and (<strong>2</strong>) you need to manage that single instance, you need a <strong>singleton</strong>. But it will create below problems</p>
</li>
<li>By-principle singletons are very rare (and a <strong>printer queue certainly isn't one, and neither is a log file</strong> - see log4j). More often than not, hardware is a singleton by coincidence rather than by principle. All hardware connected to a PC is at best a coincidental singleton (think multiple monitors, mice, printers, sound cards). thus: no singleton. In telecommunications, neither phone number nor the physical phone are singletons (think ISDN, call center).</li>
<li>There's no reason that a single serial port on a development board should be modeled as a Singleton. Indeed, modeling it so will only make it harder to port to the new board that has two ports!</li>
</ol>
<h2>Static classes</h2>
<p>There is nothing wrong with static classes that are truly <em>static</em>. That is to say, there is no internal state to speak of that would cause the output of the methods to change.</p>
<ul>
<li>A pure function is one which is deterministic, which is to say, for a given input, you will get one and exactly one output. You want static methods to be pure functions.</li>
<li>static methods should be deterministic; they should have no side effects.</li>
<li>There is nothing wrong with static classes that are truly <em>static</em>. That is to say, there is no internal state to speak of that would cause the output of the methods to change.</li>
<li>A singleton is a class containing static methods about as opposite of "pure function" as you can be. A <strong>single static private member is kept</strong> internally to the class which is used to ensure there is exactly one instance.</li>
</ul>
<!-- /wp:heading -->

<!-- wp:heading -->
<h2>Advantages of Singleton over static class</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>The only OO feature that static classes lack compared to Singletons is polymorphism.<br />
<ul>
<li>First, a singleton can extend classes and implement interfaces, while a static class cannot (it can extend classes, but it does not inherit their instance members).Singletons are easier to work with <strong>when unit testing a class</strong>.</li>
<li>Wherever you pass singletons as a <strong>parameter</strong> (constructors, setters or methods) you can instead substitute a mocked or stubbed version of the singleton.</li>
<li>you can pass around the object for delegates and callbacks</li>
</ul>
</li>
<li>Object creation
<ul>
<li>with a singleton you can use a factory pattern to build up your instance</li>
<li>Singleton can be <strong>initialized lazily or asynchronously</strong> while a static class is generally initialized when it is first loaded, leading to <strong>potential class loader issues</strong>.</li>
</ul>
</li>
<li>However the most important advantage, though, is that singletons can be handled polymorphically <strong>without forcing their users to assume that there is only one instance</strong>.</li>
<li>Another advantage of a singleton is that it can easily be serialized, which may be necessary if you need to save its state to disc, or send it somewhere remotely.</li>
</ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Static Class:-</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol>
<li>You cannot create the instance of static class.</li>
<li>Loaded automatically by the .NET Framework common language runtime (CLR) when the program or namespace containing the class is loaded.</li>
<li>We cannot pass the static class to method.</li>
<li>We cannot inherit Static class to another Static class in C#.</li>
<li>A class having all static methods.</li>
<li>Better performance (static methods are bonded on compile time)</li>
</ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Singleton:-</strong></p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol>
<li>You can create one instance of the object and reuse it.</li>
<li>Singleton instance is created for the first time when the user requested.</li>
<li>Singleton class can have constructor.</li>
<li>You can create the object of singleton class and pass it to method.</li>
<li>Singleton class does not say any restriction of Inheritance.</li>
<li>We can dispose the objects of a singleton class but not of static class.</li>
<li>Methods can be overridden.</li>
<li>Can be lazy loaded when need (static classes are always loaded).</li>
<li>We can implement interface(static class can not implement interface).</li>
</ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>A static class allows only static methods.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
<li>The big difference between a singleton and a bunch of static methods is that singletons can implement interfaces (or derive from useful base classes, although that's less common, in my experience), so you can pass around the singleton as if it were "just another" implementation.</li>
<li>Imagine the singleton implements an interface <code>Foo</code>, and you have a method taking a <code>Foo</code> as a parameter. With that setup, callers can choose to use the singleton as the implementation - or they could use a different implementation. The method is decoupled from the singleton. Compare that with the situation where the class just has static methods - every piece of code which wants to call those methods is tightly coupled to the class, because it needs to specify which class contains the static methods.</li>
<li> </li>
</ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<h2>References</h2>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
<li><a href="http://misko.hevery.com/code-reviewers-guide/">http://misko.hevery.com/code-reviewers-guide/</a></li>
<li><a href="https://stackoverflow.com/questions/137975/what-is-so-bad-about-singletons">https://stackoverflow.com/questions/137975/what-is-so-bad-about-singletons</a></li>
<li><a href="https://softwareengineering.stackexchange.com/questions/40373/so-singletons-are-bad-then-what">https://softwareengineering.stackexchange.com/questions/40373/so-singletons-are-bad-then-what</a></li>
<li><a href="http://misko.hevery.com/2008/12/15/static-methods-are-death-to-testability/">http://misko.hevery.com/2008/12/15/static-methods-are-death-to-testability/</a></li>
<li><a href="https://stackoverflow.com/questions/519520/difference-between-static-class-and-singleton-pattern">https://stackoverflow.com/questions/519520/difference-between-static-class-and-singleton-pattern</a></li>
<li><a href="https://stackoverflow.com/questions/14097656/singleton-class-vs-class-with-static-member">https://stackoverflow.com/questions/14097656/singleton-class-vs-class-with-static-member</a></li>
</ul>
<!-- /wp:list -->
