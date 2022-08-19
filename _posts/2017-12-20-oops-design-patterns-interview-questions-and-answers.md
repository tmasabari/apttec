---
layout: post
title: OOPs Design Patterns and Dependency Injection
date: 2017-12-20 03:51
author: tmasabari
comments: true
categories: [Architecture, Design, Interview Preparation, Prepare, QuickRefresh, Software]
---
<!-- wp:heading -->
<h2>Background</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The intention of this article is to collect the quick notes on important design principles across multiple websites and include my own experience as quick refresh guide.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Design Patterns</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A design pattern in software is used to solve similar problems that occur in different scenarios.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>What is design patterns? Have you used any design pattern in your code ?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Design patterns are tried and tested way to solve particular design issues by various programmers in the world. Design patterns are extension of code reuse.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Read more: <a href="http://javarevisited.blogspot.com/2012/06/20-design-pattern-and-software-design.html#ixzz52HXCxjjh">http://javarevisited.blogspot.com/2012/06/20-design-pattern-and-software-design.html#ixzz52HXCxjjh</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3><strong>Most used patterns</strong></h3>
<!-- /wp:heading -->

<!-- wp:embed {"url":"http://www.dofactory.com/topic/1035/most-frequently-used-design-patterns.aspx"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.dofactory.com/topic/1035/most-frequently-used-design-patterns.aspx
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"https://www.quora.com/Which-are-top-5-common-mostly-used-design-patterns-for-C"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://www.quora.com/Which-are-top-5-common-mostly-used-design-patterns-for-C
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"http://www.developerfusion.com/article/8307/aspnet-patterns-every-developer-should-know/"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.developerfusion.com/article/8307/aspnet-patterns-every-developer-should-know/
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p>The following list shows some of the most common design patterns within these groups:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>· Presentation Pattern
<ul><li>· Model-View-Controller (MVC)</li><li>MVVM – Angular – Dual binding</li><li>Page Controller Pattern - Web forms</li><li>· Use Case Controller</li><li>· Model-View-Presenter (MVP)</li></ul>
</li><li>· Persistence Pattern
<ul><li>· Repository</li><li>Unit of Work</li></ul>
</li><li>· Creational
<ul><li>· Factory</li><li>Prototype – Serialization</li><li>Builder - Separate representation and object construction- UWP, WPF and WinForm</li><li>Injection</li><li>· Singleton -The Timer class in UWP, WPF, and WinForms all utilize this.</li></ul>

</li><li>Structural
<ul><li>· Service Agent / Proxy / Broker</li><li>· Provider</li><li>Adapter- You can look at many of the built in classes that have interfaces<br/>that are matched with different interfaces.</li></ul>
</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>· Host or Behavioral
<ul><li>· Command</li><li>· Publish-Subscribe / Observer- .NET Event</li><li>· Plug-in / Module / Intercepting Filter – MVC filtering</li><li>Strategy Pattern - List, Array, Dictionary, Char all have a sort method and that sort method chooses the best algorithm for sorting based on the data. Encapsulate algorithms within a class and make them interchangeable</li></ul>
</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Personally, my answer would go something like this:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Layers (n-Tier architecture - all my projects are layered)</li><li>Facade (Service Layer)</li><li>Iterator (LINQ really)</li><li>Active Record (we use this as our business object and data access<br/>pattern)</li><li>Singleton (every app has use for several singletons)</li><li>Proxy WCF</li><li>Factory (great useful pattern for creating families of objects)</li><li>Adapter</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Presentation Patterns</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><a href="https://stackoverflow.com/questions/2056/what-are-mvp-and-mvc-and-what-is-the-difference?rq=1">MVC Vs MVP</a> - They separate the dependencies between a Model (think Domain objects), your screen/web page (the View), and how your UI is supposed to behave (Presenter/Controller)</li><li>In MVC,controller has one to many relationship with View(s). in MVP view has one to one relationship with a controller</li><li>In <strong>MVP</strong>, the Presenter contains the UI business logic for the View. All invocations from the View delegate directly to Presenter. The Presenter is also decoupled directly from the View and talks to it through an interface. This is to allow mocking of the View in a unit test. One common attribute of MVP is that there has to be a lot of two-way dispatching.</li><li>In MVC,
<ul><li>Controller are based on behaviors and can be shared across views</li><li>Can be responsible for determining which view to display</li></ul>
</li><li><a href="https://stackoverflow.com/questions/667781/what-is-the-difference-between-mvc-and-mvvm?rq=1">MVC vs MVVM</a> For ASP.Net, MVVM is used to <em>two-way bind</em> data within views
<ol><li>MVVM. Don't be fooled by the letters, by the omission of the C. Controllers are still there.</li><li>We just add one thing: statefulness, data cached on the client (and along with it intelligence to handle that data). That data, essentially a cache on the client, now gets called »ViewModel«. It's what allows rich interactivity. And that's it.
<ol><li>MVC = model, controller, view = essentially one-way communication = poor interactivity</li><li>MVVM = model, controller, cache, view = two-way communication = rich interactivity</li></ol>
</li><li>Views <em>display a certain shape of data</em>. They have no idea where the data comes from.</li><li>ViewModels <em>hold a certain shape of data and commands</em>, they do not know where the data, or code, comes from or how it is displayed (what view is displaying it).<br/>The VM then becomes a dumb container that requires little, if any, testing.</li><li>Models <em>hold the actual data</em> (various context, store or other methods)</li><li>Controllers listen for, and publish, events. Controllers provide the logic that controls what data is seen and where. Controllers provide the command code to the ViewModel so that the ViewModel is actually reusable.</li></ol>
</li></ol>
<!-- /wp:list -->

<!-- wp:image {"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2017/12/image-8.png"><img src="/wp-content/uploads/2017/12/image_thumb-8.png" alt="image"/></a></figure>
<!-- /wp:image -->

<!-- wp:image {"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2017/12/image-9.png"><img src="/wp-content/uploads/2017/12/image_thumb-9.png" alt="image"/></a></figure>
<!-- /wp:image -->

<!-- wp:heading {"level":3} -->
<h3><a href="http://deviq.com/repository-pattern/">The Repository Pattern</a></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The Repository pattern virtualizes storage of entities in a persistent medium, such as a database or as XML. . It effectively hides the storage implementation from the application code, and allows the use of a common set of methods in the application without requiring knowledge of the storage mechanism or format.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Repository Pattern has gained quite a bit of popularity since it was first introduced as a part of <a href="http://bit.ly/PS-DDD">Domain-Driven Design</a> in 2004. Essentially, it provides an abstraction of data, so that your application can work with a simple abstraction that has an interface approximating that of a collection. Adding, removing, updating, and selecting items from this collection is done through a series of straightforward methods, without the need to deal with database concerns like connections, commands, cursors, or readers. Using this pattern can help achieve loose coupling and can keep domain objects <a href="http://deviq.com/persistence-ignorance/">persistence ignorant</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2017/12/wps5E41.tmp_-1.jpg"><img src="/wp-content/uploads/2017/12/wps5E41.tmp_thumb-1.jpg" alt="wps5E41.tmp"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><strong>Specification</strong><br/>Repositories that follow the advice of not exposing IQueryable can often become bloated with many custom query methods. The solution to this is to separate queries into their own types, using the <a href="http://deviq.com/specification-pattern/">Specification Design Pattern</a>. The Specification can include the expression used to filter the query, any parameters associated with this expression, as well as how much data the query should return (i.e. “.Include()” in EF/EF Core). Combining the Repository and Specification patterns can be a great way to ensure you follow the <a href="http://deviq.com/single-responsibility-principle/">Single Responsibility Principle</a> in your data access code. See <a href="http://deviq.com/specification-pattern/">an example of how to implement a generic repository along with a generic specification in C#</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Repository Per Entity or Business Object</li><li>Generic Repository Interface</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":4} -->
<h4><strong>Scenarios</strong></h4>
<!-- /wp:heading -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td>Singleton</td><td>The Singleton Design Pattern is used to restrict the number of times a specific object can be created to a single time by providing access to a share instance of itself</td></tr><tr><td>Factory pattern</td><td>If you are using large chunk of if/else or switch statement in your code to create instances of similar classes.
 
Every time when you introduce a new class, you will have to add more conditions to the statement.
Factory pattern provides a simple interface for external codes to acquire an instance of a class. It makes code much easier to maintain and test.
</td></tr><tr><td>Observer pattern</td><td>The main class which will notify its listener class (Observer) upon its changes of state is called Observerable class.
 
A change of state can be from a simple property update to business logic.
Observerable class does not care about what its Observers do; it does not even know their existence.
This way, two objects are loosely coupled. It became very easy to add additional functions without alerting main code.
</td></tr><tr><td><a href="https://stackoverflow.com/questions/757743/what-is-the-difference-between-builder-design-pattern-and-factory-design-pattern?rq=1">Builder pattern</a></td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3>Gang of Four (GoF) patterns</h3>
<!-- /wp:heading -->

<!-- wp:embed {"url":"https://msdn.microsoft.com/en-us/magazine/cc188707.aspx"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://msdn.microsoft.com/en-us/magazine/cc188707.aspx
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"http://dotnetacademy.blogspot.in/2011/10/design-patterns-which-are-used-in-net.html#sthash.LZaSea83.dpuf"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://dotnetacademy.blogspot.in/2011/10/design-patterns-which-are-used-in-net.html#sthash.LZaSea83.dpuf
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"http://www.ehartwell.com/InfoDabble/Design_patterns_and_the_.NET_framework"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.ehartwell.com/InfoDabble/Design_patterns_and_the_.NET_framework
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"http://stackoverflow.com/questions/1316743/are-there-any-design-patterns-used-in-the-net-framework"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://stackoverflow.com/questions/1316743/are-there-any-design-patterns-used-in-the-net-framework
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p><strong>Acronyms - </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ABFPS (Abraham Became First President of States)</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>ABCDFFP, MMIICCSS OTV</strong></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Creational Pattern</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Factory Methods are usually called within Template Methods.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components get built.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Abstract Factory, Builder, and Prototype can use Singleton in their implementations.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The Abstract Factory Pattern can be implemented using the Factory Method Pattern, Prototype Pattern or the Singleton Pattern.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Abstract Factory classes are often implemented with Factory Methods, but they can also be implemented using Prototype</li><li>The ConcreteFactory object can be implemented as a Singleton as only one instance of the ConcreteFactory object is needed.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><a href="http://www.careerride.com/NET-Architecture-factory-abstract-factory-patterns.aspx">What is the difference between Factory and Abstract Factory Patterns?</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Factory vs Abstract Factory</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><strong>What is main benefit of using factory pattern ? Where do you use it?</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Factory pattern’s main benefit is increased level of encapsulation while creating objects. If you use Factory to create object you can later replace original implementation of Products or classes with more advanced and high performance implementation without any change on client layer.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The main difference between a "factory method" and an "abstract factory" is that the factory method is a single method, and an abstract factory is an object.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In Factory pattern, we create object without exposing the creation logic. In this pattern, an interface is used for creating an object, but let subclass decide which class to instantiate. The creation of object is done when it is required.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Factory Method pattern is a simplified version of Abstract Factory pattern. Factory Method pattern is responsible of creating products that belong to one family, while Abstract Factory pattern deals with multiple families of products.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://www.go4expert.com/articles/design-pattern-simple-examples-t5127/#factory">Factory</a> method takes care of one product where as the abstract factory Pattern provides a way to encapsulate a family of products.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In Factory pattern, we create object without exposing the creation logic. In this pattern, an interface is used for creating an object, but let subclass decide which class to instantiate. The creation of object is done when it is required. The Factory method allows a class later instantiation to subclasses.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Abstract Factory patterns acts a super-factory which creates other factories. This pattern is also called as Factory of factories. In Abstract Factory pattern an interface is responsible for creating a set of related objects, or dependent objects without specifying their concrete classes.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2017/12/image-10.png"><img src="/wp-content/uploads/2017/12/image_thumb-10.png" alt="image"/></a></figure>
<!-- /wp:image -->

<!-- wp:image {"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="/wp-content/uploads/2017/12/image-7.png"><img src="/wp-content/uploads/2017/12/image_thumb-7.png" alt="image"/></a></figure>
<!-- /wp:image -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong>Factory patterns</strong></td><td><strong>Abstract patterns</strong></td></tr><tr><td>The objects are created through inheritance.</td><td>The objects are created through composition.</td></tr><tr><td>It is used in which the subclass is responsible for object instantiation.</td><td>It is used to delegate object instantiation by a class to some object.</td></tr><tr><td>This pattern creates products.</td><td>This pattern creates factory.</td></tr><tr><td>Each subclass knows what other classes to use or objects to create.</td><td>Swapping FactoryMethod classes with object composition.</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td>Name</td><td>Description</td><td>.NET</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Creational_pattern">Creational patterns</a>
 
 
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Abstract_factory_pattern">Abstract factory</a></td><td>Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
 
Any place where you need a run-time value to construct a particular dependency, <strong>Abstract Factory </strong>is the solution.
Having Initialize methods on the interfaces smells of a <strong>Leaky Abstraction</strong>.
the approach becomes very powerful when we want to dynamically create instances based on parameters. For example, creating instances at runtime based on User Inputs. This is also very centric to Dependency Injection (DI). Activator.CreateInstance is not centric to Abstract Factory Pattern. It just allows us to create instances in a convenient way based on the type parameter.
</td><td><strong>Abstract Factory</strong>: System.Data.Common.DbProviderFactory. Every member function of this class is a factory method.
 
 
Example multi-tenant application. The set of interfaces are going to be the same for multiple factories(tenants). For example customer/account interfaces are going to be same. But based up on factories (Citibank / JPMorgon) the implementations will be different.
<a href="https://www.codeproject.com/Articles/328373/Understanding-and-Implementing-Abstract-Factory-Pa"> Phone example with smart &amp; dump phones with Samsung, HTC, Nokia companies </a>
https://www.codeproject.com/Articles/328373/Understanding-and-Implementing-Abstract-Factory-Pa
 
<a href="http://stackoverflow.com/questions/1943576/is-there-a-pattern-for-initializing-objects-created-via-a-di-container/1945023#1945023">http://stackoverflow.com/questions/1943576/is-there-a-pattern-for-initializing-objects-created-via-a-di-container/1945023#1945023</a>
 
 
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Factory_method_pattern">Factory method</a></td><td>Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
 
This strategy for creating new object instances is known as a Factory pattern. Rather than invoking the object's constructor, you can ask the object factory to create the instance for you. That way, the factory class can hide the complexity of object creation (like how to parse a Double out of a string). If you wanted to change the details of creating the object, you'd only have to change the factory itself; you would not have to change every single place in the code where the constructor is called.
</td><td><strong>Factory Method</strong>:
 
System.Data.IDbConnection.BeginTransaction(). The type of transaction created depends on the underlying IDbConnection implementation.
WebRequest.Create() returns a concrete type that depends on the URL scheme
System.Convert class contains a host of static methods that work like factory design pattern
System.Net.WebRequest: This class is used to request and receive a response from a resource on the Internet.FTP, HTTP, and file system requests are supported by default. To create a request, call the Create method and pass in a URI. The Create method itself determines the appropriate protocol for the request and returns the appropriate subclass of WebRequest: <strong>HttpWebRequest, FtpWebRequest, or FileWebRequest</strong>. The caller doesn't need to know the specifics of each protocol, only how to invoke the factory and work with the WebRequest that gets returned. If the URI changes from an HTTP address to an FTP address, the code won't have to change at all.
 
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Builder_pattern">Builder</a></td><td>Separate the construction of a complex object from its representation so that the same construction process can create different representations.</td><td><strong>Builder</strong>: The WCF channel construction infrastructure.
 

If separate parts of a complex class needs to be constructed with multiple methods
If class needs to be constructed in multiple steps. Each step different set of adjectives/specifications will be passed.

a less well-known derivate of Builder pattern - <a href="http://www.svlada.com/step-builder-pattern/">Step Builder pattern. / Wizard pattern</a>
The Builder is only needed when an object cannot be produced in one step.
The builder design pattern describes an object that knows how to craft another object of a specific type over several steps. It holds the needed state for the target item at each intermediate step.
Think what StringBuilder goes through to produce a final string.
Wizard
One great an example of this would be in the de-serialization process for a complex object. Often times the parameters for the complex object must be retrieved one by one.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Prototype_pattern">Prototype</a></td><td>Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.</td><td><strong>Prototype</strong> - used in framework for cloning and serialization
 
In .Net, cloning can be achieved my making use of the ICloneable of the system namespace. Using the clone method, we can create clones or copies of instances with the same value of the existing instance. Shallow copy is used here which simply creates a reference of the original. Deep copy can be used when a duplicate instance needs to be created. <a href="http://www.careerride.com/NET-Architecture-implement-prototype-pattern.aspx">http://www.careerride.com/NET-Architecture-implement-prototype-pattern.aspx</a> 
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Singleton_pattern">Singleton</a></td><td>Ensure a class only has one instance, and provide a global point of access to it.</td><td><strong>Singleton</strong> - used as an activation method in WCF, i.e. a web service may be treated as a singleton by the WCF infrastructure. Ditto for .NET Remoting
 
<a href="http://www.careerride.com/NET-Architecture-singleton-pattern.aspx">Singleton pattern</a> is commonly used in print spoolers.
- A class with static members needs to be created.
- A private constructor to the class above should be defined.<br/>- A static method can be used to access the singleton object.
<a href="https://stackoverflow.com/questions/519520/difference-between-static-class-and-singleton-pattern?rq=1">Static Class vs Singleton</a>
Singletons can be handled polymorphically without forcing their users to assume that there is only one instance.
First, a singleton can extend classes and implement interfaces, while a static class cannot (it can extend classes, but it does not inherit their instance members)
A singleton instance (or rather, a reference to that instance) can be passed as a parameter to other methods, and treated as a normal object. A static class allows only static methods.
A singleton can be initialized lazily or asynchronously while a static class is generally initialized when it is first loaded, leading to potential class loader issues. So state management is not properly handled
If there are bunch of functions should be kept together, then <code>static</code> is the choice. Anything else which needs single access to some resources, could be implemented <code>singleton</code>.

What makes you say that either a singleton or a static method isn't<br/>thread-safe? Usually both <em>should</em> be implemented to be thread-safe.

</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Structural_pattern">Structural patterns</a></td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Adapter_pattern">Adapter</a></td><td>The Provider and Adapter patterns allows otherwise incompatible classes to work together by converting the interface of one class into an interface expected by the other. In more practical terms, these patterns provide separation between components that allows behavioral changes to occur without prior knowledge of requirements.
 
The Adapter Design Pattern, also known as the Wrapper, allows two classes to work together that otherwise would have incompatible interfaces.
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
</td><td><a href="/wp-content/uploads/2017/12/image-2.png"></a>
 
The ADO.NET providers, eg System.Data.SqlClient.SqlConnection, System.Data.OleDb.OleDbConnection etc. Each provider is an adapter for its specific database.
DataAdapter; Encoding; TypeLibConverter; delegate
By allowing managed classes and COM components to interact despite their interface differences, RCWs are an example of the Adapter pattern. The Adapter pattern lets you adapt one interface to another. COM doesn't understand the System.String class, so the RCW adapts it to something that it can understand. Even though you can't change how a legacy component works, you can still interact with it. Adapters are frequently used like this.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Bridge_pattern">Bridge</a></td><td>Decouple an abstraction from its implementation so that the two can vary independently.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Composite_pattern">Composite</a></td><td>Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.</td><td><strong>Composite</strong>: many examples
 
System.Windows.Forms.Control and its derived classes.
System.Web.UI.Control and its derived classes.
System.Xml.XmlNode and its derived classes.
ASP.NET has lots of controls. A control may be a simple single item like a Literal, or it could be composed of a complex collection of child controls, like a DataGrid is. Regardless, calling the Render method on either of these controls should still perform the same intuitive function.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Decorator_pattern">Decorator</a></td><td>Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.</td><td>System.Windows.Controls.Decorator (in WPF).
 
<a href="/wp-content/uploads/2017/12/wpsC706.tmp_.jpg"></a>
System.IO.Stream :Any useful executable program involves either reading input, writing output, or both. Regardless of the source of the data being read or written, it can be treated abstractly as a sequence of bytes. .NET uses the System.IO.Stream class to represent this abstraction. <strong>CryptoStream</strong> :System.Security.Cryptography.CryptoStream to encrypt and decrypt Streams on the fly, without the rest of the application needing to know anything more than the fact that it is a Stream.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Facade_pattern">Facade</a></td><td>Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.</td><td><strong>Facade</strong>: System.Xml.Serialization.XmlSerializer. XmlSerializer hides a complex task (that includes generating assemblies on the fly!) behind a very easy-to-use class.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Flyweight_pattern">Flyweight</a></td><td>Use sharing to support large numbers of fine-grained objects efficiently.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Proxy_pattern">Proxy</a></td><td>Provide a surrogate or placeholder for another object to control access to it.
 
 
<strong>Various patterns exist that remove dependencies between a client and a service by using intermediate brokers</strong>The aim of all these patterns is to allow remote connection to, and use of, a service without the client having to know how the service works.
</td><td><strong>Proxy</strong>: The web service proxies generated by svcutil.exe and deriving from System.ServiceModel.ClientBase&lt;TChannel>
 
The service exposes a Contract that defines its interface, such as the <strong>Web Service Description Language (WSDL)</strong> document for a Web Service. A client-side proxy or gateway interface uses the Contract to create a suitably formatted request, and passes this to the service interface. The service sends the formatted response back through its gateway interface to the client proxy, which exposes it to the client. In effect, the client just calls the service methods on the client proxy, which returns the results just as if the service itself was a local component.
<a href="/wp-content/uploads/2017/12/wps2A6E.tmp_-1.jpg"></a>
 
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Behavioral_pattern">Behavioral patterns</a></td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Chain_of_responsibility_pattern">Chain of responsibility</a></td><td>Gives more than one object an opportunity to handle a<br/>request by linking receiving objects togetherA request not being handled is an acceptable potential outcomeAvoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request.Chain the receiving objects and pass the request along the chain until an object handles it.</td><td>Exception handling in some languages implements<br/>this pattern.System.Web.UI.Control.OnBubbleEvent() and System.Web.UI.Control.RaiseBubbleEvent()</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Command_pattern">Command</a></td><td>Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
 
encapsulates a operation call in an object thus making it transferable over a wire or persist-able
</td><td>System.Windows.Input.ICommand (in WPF)
 
Job queues are widely used to facilitate the asynchronous processing of algorithms.
<strong>Implement the wizard using a command object</strong>. The command object is created when the wizard is first displayed. Each wizard page stores its GUI changes in the command object, so the object is populated as the user progresses. "Finish" simply triggers a call to execute(). This way, the command class will work.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Interpreter_pattern">Interpreter</a></td><td>Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Iterator_pattern">Iterator</a></td><td>Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.</td><td>foreach; <strong>IEnumerator</strong>; generic List&lt;>
 
System.Collections.IEnumerable,System.Collections.Generic.IEnumerable&lt;T>. System.Data.IDataReader
foreach statements make use of the iterator for the array behind the scenes. All you need to know is that you are guaranteed to have the loop run exactly once for each item in the array.
To make those statements work, the object referenced in the In expression must implement IEnumerable.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Mediator_pattern">Mediator</a></td><td>Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Memento_pattern">Memento</a></td><td>Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.</td><td>The .NET <em>Serializable</em> pattern is a variation on the <em>Memento</em> pattern</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Observer_pattern">Observer</a> / EventListner</td><td>Define a <strong>one-to-many dependency between objects</strong> so that when one object changes state, all its dependents are notified and updated automatically.
 
<strong>callback</strong> - notifies a single caller that some operation finished with some result
<strong>observer</strong> - notifies zero to n interested parties that some event (for example a finished operation) happened
</td><td>The .NET <strong>event mechanism</strong>
 
delegates and events
<a href="https://stackoverflow.com/questions/8951276/callback-command-vs-eventlistener-observer-pattern">https://stackoverflow.com/questions/8951276/callback-command-vs-eventlistener-observer-pattern</a>
 
then <code>Observer</code> pattern is a natural choice for you.
Use the <strong>callback</strong> pattern to trigger operations and <strong>notify the caller</strong> asynchronously that the triggered operation finished.
Use the <strong>event/observer</strong> pattern to give some other components (that <strong>did <em>not</em> trigger the operation</strong>) the chance to be notified when an operation finishes
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Intercom_pattern">Intercom</a></td><td>Define a many-to-many as well as one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/State_pattern">State</a></td><td>Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Strategy_pattern">Strategy</a></td><td>The Strategy Design Pattern allows an object to <strong>have some or all of its behavior</strong> defined <strong>in terms of another object which follows a particular interface</strong>.
 
A particular instance of this interface is provided to the client when it is instantiated or invoked, providing the concrete behavior to be used.
Define a family of algorithms, encapsulate each one, and make them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.
</td><td>Sort method in ArrayList
 
<a href="/wp-content/uploads/2017/12/wpsC726.tmp_.jpg"></a>
Both Array and ArrayList provide the capability to sort the objects contained in the collection via the Sort method. Strategy Design Pattern is used with Array and Arraylist to sort them using different strategy without changing any client code using IComparable interface
One of the new generic collections in version 2.0 of the .NET Framework, List&lt;T>, also makes heavy use of the Strategy pattern, shown in <strong>Figure </strong>. In addition to the updated Sort method, the find-related methods, BinarySearch, and others all take parameters that allow parts of the respective algorithms to vary based on the needs of the caller.
The Strategy design pattern is used extensively to achieve the <a href="http://deviq.com/single-responsibility-principle">Single Responsibility Principle</a>, the <a href="http://deviq.com/explicit-dependencies-principle">Explicit Dependencies Principle</a>, and the <a href="http://deviq.com/dependency-inversion-principle">Dependency Inversion Principle</a>, and is a key to <a href="http://deviq.com/dependency-injection">Dependency Injection</a> and the use of Inversion of Control Containers.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Template_method_pattern">Template method</a></td><td>Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.</td><td>Render method for custom controls. Regardless of which style of custom control you choose, you don't have to write any code to handle the functionality that's common to all controls, like loading and saving ViewState at the right time, allowing PostBack events to be handled, and making sure the control lifecycle events are raised in the correct order. The main algorithm for how a control should be loaded, rendered, and unloaded is contained in the control base class.
 
Strategy is used to allow callers to vary an entire algorithm, like how to compare two objects, while Template Method is used to vary steps in an algorithm. Because of this, Strategy is more coarsely grained. There can be vast differences between different client implementations, while with Template Method the algorithm remains fundamentally the same.
Strategy uses delegation while Template Method uses inheritance. In the sorting example of Strategy, the comparison algorithm is delegated to the IComparer parameter, but with custom controls you subclass the base and override methods to make changes. Both, however, let you easily alter processes to fit your specific needs.
</td></tr><tr><td><a href="http://en.wikipedia.org/wiki/Visitor_pattern">Visitor</a></td><td>Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.</td><td>System.Linq.Expressions.ExpressionVisitor (<a href="http://en.wikipedia.org/wiki/Language_Integrated_Query">used internally by [LINQ]</a>)</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:heading {"level":3} -->
<h3>What is the difference between Static class and Singleton instance?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>– In c# a static class cannot implement an interface. When a single instance class needs to implement an interface for some business reason or IoC purposes, you can use the Singleton pattern without a static class.<br/>– You can clone the object of Singleton but, you can not clone the static class object<br/>– Singleton object stores in Heap but, static object stores in stack<br/>– A singleton can be initialized lazily or asynchronously while a static class is generally initialized when it is first loaded</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>How to implement singleton design pattern in C#?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>There are several ways for implementing Singleton in C#.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Standard Implementation</li><li>Double checked locking</li><li>Early Instance Creation</li><li>Fully Lazy Instantiation</li><li>Using Generics</li><li>using Lazy&lt;T> type</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>You can read each way of Singleton Implementation <a href="http://www.csharpstar.com/singleton-design-pattern-csharp/" target="_blank" rel="noreferrer noopener">here</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3><a href="http://www.csharpstar.com/csharp-interview-questions-part-7/">How to avoid Singleton instance creation by cloning</a> ?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We can create a copy of an object using clone() method.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To avoid creating a clone of our singleton class, we can do the following :<br/>– Implement MethodwiseClone()<br/>– Override the clone() method and throw CloneNotSupportedException from it.</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:heading {"level":1} -->
<h1><em>What is the Dependency injection?</em></h1>
<!-- /wp:heading -->

<!-- wp:heading -->
<h2 id="what-is-dependency-injection"><a href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection">What is dependency injection?</a></h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Dependency injection (DI) is a technique for achieving loose coupling between objects and their collaborators, or dependencies. Rather than directly instantiating collaborators, or using static references, the objects a class needs in order to perform its actions are provided to the class in some fashion. Most often, classes will declare their dependencies via their constructor, allowing them to follow the <a href="http://deviq.com/explicit-dependencies-principle/">Explicit Dependencies Principle</a>. This approach is known as "constructor injection".</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>When classes are designed with DI in mind, they're more loosely coupled because they don't have direct, hard-coded dependencies on their collaborators. This follows the <a href="http://deviq.com/dependency-inversion-principle/">Dependency Inversion Principle</a>, which states that <em>"high level modules shouldn't depend on low level modules; both should depend on abstractions."</em></li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Instead of referencing specific implementations, classes request abstractions (typically <code>interfaces</code>) which are provided to them when the class is constructed. Extracting dependencies into interfaces and providing implementations of these interfaces as parameters is also an example of the <a href="http://deviq.com/strategy-design-pattern/">Strategy design pattern</a>.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>When a system is designed to use DI, with many classes requesting their dependencies via their constructor (or properties), it's helpful to have a class dedicated to creating these classes with their associated dependencies. These classes are referred to as <em>containers</em>, or more specifically, <a href="http://deviq.com/inversion-of-control/">Inversion of Control (IoC)</a> containers or Dependency Injection (DI) containers.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>A container is essentially a factory that's responsible for providing instances of types that are requested from it. If a given type has declared that it has dependencies, and the container has been configured to provide the dependency types, it will create the dependencies as part of creating the requested instance. In this way, complex dependency graphs can be provided to classes without the need for any hard-coded object construction. In addition to creating objects with their dependencies, containers typically manage object lifetimes within the application.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Martin Fowler has written an extensive article on <a class="" href="https://www.martinfowler.com/articles/injection.html">Inversion of Control Containers and the Dependency Injection Pattern</a>. Microsoft Patterns and Practices also has a great description of <a href="https://msdn.microsoft.com/library/hh323705.aspx">Dependency Injection</a>.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Entity Framework contexts should be added to the services container using the <code class="">Scoped</code> lifetime.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>The main danger to be wary of is resolving a <code>Scoped</code> service from a singleton. It's likely in such a case that the service will have incorrect state when processing subsequent requests.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>Service lifetimes and registration options<ul><li><strong>Transient </strong>Transient lifetime services are created each time they're requested. This lifetime works best for lightweight, stateless services. <em>Transient</em> objects are always different; a new instance is provided to every controller and every service.</li></ul> <ul><li><strong>Scoped </strong>Scoped lifetime services are created once per request. <em class="">Scoped</em> objects are the same within a request, but different across different requests  </li></ul> <ul><li><strong>Singleton </strong>Singleton lifetime services are created the first time they're requested (or when <code>ConfigureServices</code> is run if you specify an instance there) and then every subsequent request will use the same instance.</li></ul> <ul><li><em class="">Singleton</em> objects are the same for every object and every request (regardless of whether an instance is provided in <code>ConfigureServices</code>)</li></ul> <ul><li>If your application requires singleton behavior, allowing the services container to manage the service's lifetime is recommended instead of implementing the singleton design pattern and managing your object's lifetime in the class yourself.</li></ul></li><li>Best practices <a href="https://medium.com/volosoft/asp-net-core-dependency-injection-best-practices-tips-tricks-c6e9c67f9d96">https://medium.com/volosoft/asp-net-core-dependency-injection-best-practices-tips-tricks-c6e9c67f9d96</a></li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Dependency injection &amp; Factory</h2>
<!-- /wp:heading -->

<!-- wp:embed {"url":"https://stackoverflow.com/questions/557742/dependency-injection-vs-factory-pattern"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://stackoverflow.com/questions/557742/dependency-injection-vs-factory-pattern
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"http://www.c-sharpcorner.com/UploadFile/97fc7a/factory-pattern-in-net-with-an-example/"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.c-sharpcorner.com/UploadFile/97fc7a/factory-pattern-in-net-with-an-example/
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p>Dependency Injection is more of a architectural pattern for loosely coupling software components. Factory pattern is just one way to separate the responsibility of creating objects of other classes to another entity. Factory pattern can be called as a tool to implement DI. Dependency injection can be implemented in many ways like DI using constructors, using mapping xml files etc.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Factory pattern offers higher-level abstraction than DI. A factory can offer configuration options just as DI does, but it can also <strong>choose to hide all those configuration details, so that the factory can decide to switch to a completely different implementation</strong> without the client knowing. DI on its own does not allow this. DI requires the client to specify the changes he want</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Life cycle management is one of the responsibilities dependency containers assume in addition to instantiation and injection. The fact that the container sometimes<strong> keep a reference to the components</strong> after instantiation is the rea<strong>son it is called a "</strong>container",<strong> and not a factory. </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Dependency injection containers usually <strong>only keep a reference to objects it needs to manage life cycles for,</strong> or that are reused for future injections, like singletons or flyweights. When configured to create new instances of some components for each call to the container, the container usually just forgets about the created object.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>One disadvantage of DI is that <strong>it can not initialize objects with logic.</strong> For example, when I need to create a character that has random name and age, DI is not the choice over factory pattern. With factories, we can easily encapsulate the random algorithm from object creation, which supports one of the design patterns called "Encapsulate what varies".</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Inversion of Control Container</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>An Inversion of Control Container uses the principle stated above to (in a nutshell) manage classes. That is, their creation, destruction, lifetime, configuration, and dependencies. This way classes do not need to obtain and configure the classes they depend on. This dramatically reduces coupling in a system and, as a consequence, simplifies reuse and testability.</p>
<!-- /wp:paragraph -->

<!-- wp:embed {"url":"http://ayende.com/blog/2887/dependency-injection-doesnt-cut-it-anymore"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://ayende.com/blog/2887/dependency-injection-doesnt-cut-it-anymore
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p>the core things that an IoC container should provide.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>· Dependency Injection</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>· No required dependency on the container from the services</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>· Life style management</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>· Aspect Oriented Programming</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>.NET Core</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>Services Registration</h4>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Services can be registered with the container in several ways. We have already seen how to register a service implementation with a given type by specifying the concrete type to use.</li><li>In addition, a factory can be specified, which will then be used to create the instance on demand.</li><li>The third approach is to directly specify the instance of the type to use, in which case the container will never attempt to create an instance (nor will it dispose of the instance).</li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 id="thread-safety">Thread safety</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Singleton services need to be thread safe. If a singleton service has a dependency on a transient service, the transient service may also need to be thread safe depending how it's used by the singleton.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 id="recommendations">Recommendations</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>When working with dependency injection, keep the following recommendations in mind:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>DI is for objects that have complex dependencies. Controllers, services, adapters, and repositories are all examples of objects that might be added to DI.</li><li>Avoid storing data and configuration directly in DI. For example, a user's shopping cart shouldn't typically be added to the services container. Configuration should use the <a href="https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options">options pattern</a>. Similarly, avoid "data holder" objects that only exist to allow access to some other object. It's better to request the actual item needed via DI, if possible.</li><li>Avoid static access to services.</li><li>Avoid service location in your application code.</li><li>
Avoid static access to <code>HttpContext</code>.
</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>NInject</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In Package Manager Console enter Command: <em>Install-Package Ninject.MVC4</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>After Installing Ninject Framework you should be able to see one class, NinjectWebCommon class, in the Application start folder [App_Start].</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":446} -->
<figure class="wp-block-image"><img src="/wp-content/uploads/2017/12/img_5a2a03fdbc8f0.png" alt="" class="wp-image-446"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>A NinjectResolver will inherit System.Web.Mvc.IDependencyResolver,</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>using Ninject;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>using System;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>using System.Collections.Generic;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>using System.Linq;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>using System.Web;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>namespace MvcNInject.App_Start</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public class NinjectResolver: System.Web.Mvc.IDependencyResolver</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>private readonly IKernel _kernel;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public NinjectResolver()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_kernel = new StandardKernel();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>AddBindings();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public object GetService(Type serviceType)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>return _kernel.TryGet(serviceType);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public IEnumerable&lt;object> GetServices(Type serviceType)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>return _kernel.GetAll(serviceType);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>private void AddBindings()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>// _kernel.Bind&lt;To, From>(); // Registering Types  </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>this._kernel.Bind&lt;IEvent>().To&lt;EventConcrete>(); // Registering Types </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In Application_Start() method we are going to call our NinjectResolver class.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>protected void Application_Start()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>AreaRegistration.RegisterAllAreas();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>DependencyResolver.SetResolver(new NinjectResolver());// Calling  NinjectResolver Class  </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>WebApiConfig.Register(GlobalConfiguration.Configuration);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>After completing with calling class in Global.asax now we are going to move forward to EventController and in this controller we are going to implement Constructor Injection.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public class EventController : Controller</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>private readonly IEvent _IEvent;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public EventController(IEvent IEvent)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_IEvent = IEvent;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Property Injection</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Here I have created Property with name [_Event];  to inject in property we need to Use [Inject] attribute on top of the Property where you want it.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>See below example.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>[Inject]</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>public </strong>IEvent _Event { set; get; }</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>If you have looked closely then you can see I have commented Constructor; and still we are able to inject using Property injection.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Method Injection</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Here I have created Method Injection. To use this just create a Method with any unique name, I have named it DemoMethod and this method should take the Interface as Parameter, after that, on that method, just add [Inject] Attribute.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>[Inject]  </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public void DemoMethod(IEvent IEvent)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_IEvent = IEvent;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Dependency injection <a href="http://www.ninject.org/">http://www.ninject.org</a></p>
<!-- /wp:paragraph -->

<!-- wp:embed {"url":"https://www.hanselman.com/blog/ListOfNETDependencyInjectionContainersIOC.aspx"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://www.hanselman.com/blog/ListOfNETDependencyInjectionContainersIOC.aspx
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p>Write your code so it's flexible...</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted">public class Samurai {
    public IWeapon Weapon { get; private set; }
    public Samurai(IWeapon weapon) 
    {
        this.Weapon = weapon;
    }
}</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>...and let Ninject glue it together for you.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>public class WarriorModule : NinjectModule {  public override void Load()  {  this.Bind&lt;IWeapon>().To&lt;Sword>();  } }</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li><a href="https://www.developerfusion.com/article/8307/aspnet-patterns-every-developer-should-know/">https://www.developerfusion.com/article/8307/aspnet-patterns-every-developer-should-know/</a></li><li><a href="http://www.rmfusion.com/design_patterns/design_patterns_menu.htm">http://www.rmfusion.com/design_patterns/design_patterns_menu.htm</a></li><li><a href="https://dzone.com/storage/assets/6848282-rc0008-designpatterns-online.pdf">https://dzone.com/storage/assets/6848282-rc0008-designpatterns-online.pdf</a></li></ul>
<!-- /wp:list -->
