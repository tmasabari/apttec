---
layout: post
title: Principles - Architecture and Object Oriented Design
date: 2018-02-28 17:53
author: tmasabari
comments: true
categories: [Interview Preparation, Prepare, QuickRefresh, Uncategorized]
---
<h2>Background</h2>
The intention of this article is to collect the quick notes on important design principles across multiple websites and include my own experience as quick refresh guide.
<h2>Design</h2>
<a href="http://en.wikipedia.org/wiki/High-level_design"><strong>High-level_design</strong></a> (HLD) is the overall system design - covering the system architecture and database design. It describes the relation between various modules and functions of the system. data flow, flow charts and data structures are covered under HLD. Examples use cases, state diagrams, activity diagrams, conceptual data model, logical data model

<b>Low Level Design</b> (LLD) is like detailing the HLD. It defines the actual logic for each and every component of the system. Class diagrams with all the methods and relation between classes come under LLD. Programs specs are covered under LLD. Examples class diagrams, sequence diagrams, physical data models
<h2>Architectural principles</h2>
<a href="https://ardalis.com/when-should-you-upgrade-to-asp-net-core">When to upgrade to .NET Core and Microsoft architecture book</a>
<h3>Separation of Concerns</h3>
<ul>
 	<li>software should be separated based on the kinds of work it performs.</li>
 	<li>Layers - Ideally, business rules and logic should reside in
a separate project, which should not depend on other projects in the application</li>
</ul>
<h3>Encapsulation</h3>
<ul>
 	<li>Application components and layers should be able to adjust their internal implementation without breaking their collaborators as long as external contracts are not violated.</li>
 	<li>OOPs - If an outside actor wants to manipulate the state of the object, it should do so through a well-defined function (or property setter), rather than having direct access to the private state of the object.</li>
 	<li>This frees the application’s internal design to evolve over time without worrying that doing so will break collaborators, so long as the public contracts are maintained.</li>
</ul>
<h3>Dependency Inversion</h3>
<ul>
 	<li>Most applications are written such that <span style="background-color: #ffff00;"><span style="background-color: #ffff00;">compile-time dependency flows in the direction of runtime execution
</span></span>
<p id="GYxMOeG"><img class="alignnone size-full wp-image-1645 " src="/wp-content/uploads/2018/08/img_5b615d72151d6.png" alt="" /></p>
</li>
 	<li>Inverting the typical compile-time dependency.(B to depend on an interface controlled by A at compile time)</li>
 	<li>At runtime, the flow of program execution remains unchanged, but the introduction of interfaces means that different implementations of these interfaces can easily be plugged
<p id="CWRpWPE"><img class="alignnone size-full wp-image-1646 " src="/wp-content/uploads/2018/08/img_5b615e0fb087b.png" alt="" /></p>
</li>
</ul>
<h4>Explicit Dependencies</h4>
<ul>
 	<li>Methods and classes should explicitly require any collaborating objects they need in order to function correctly</li>
 	<li>Class constructors provide an opportunity for classes to identify the things they need in order to be in a valid state and to function properly.</li>
 	<li>This makes your code more self-documenting and your coding contracts more user-friendly, since users will come to trust that as long as they provide what’s required in the form of method or constructor parameters, the objects they’re working with will behave correctly at run time.</li>
 	<li>Don't create objects for the classes in external assembles with in the classes or methods instead inject them</li>
</ul>
<h3>Single Responsibility</h3>
<ul>
 	<li>applies to object-oriented design but can also be considered as an
architectural principle similar to separation of concerns.</li>
 	<li>When this principle is applied to application architecture, and taken to its logical endpoint, you get microservices.</li>
 	<li>A given microservice should have a single responsibility. If you need to extend the behavior of a system, it’s usually better to do it by adding additional microservices, rather than by adding responsibility to an existing one.</li>
</ul>
<h3>Don’t Repeat Yourself (DRY)</h3>
<ul>
 	<li>“Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.” The application should avoid specifying behavior related to a particular concept in multiple places as this is a frequent source of errors.</li>
 	<li>At some point, a change in requirements will require changing this behavior and the likelihood that at least one instance of the behavior will fail to be updated will result in inconsistent behavior of the system.</li>
 	<li><strong>Note: Avoid binding together behavior that is only coincidentally repetitive.</strong> For example, just because two different constants both have the same value, that doesn’t mean you should have only one constant, if conceptually they’re referring to different things.</li>
 	<li>They apply it quite broadly to include “<a href="http://en.wikipedia.org/wiki/Database_schema"><u>database schemas</u></a>, <a href="http://en.wikipedia.org/wiki/Test_plan"><u>test plans</u></a>, the <a href="http://en.wikipedia.org/wiki/Software_build"><u>build</u></a> system, even <a href="http://en.wikipedia.org/wiki/Software_documentation"><u>documentation</u></a>.”<a href="#cite_note-HuntThomasBroadInfo-1"><u><sup>[1]</sup></u></a> When the DRY principle is applied successfully, a modification of any single element of a system does not require a change in other logically unrelated elements.</li>
</ul>
<h3>Persistence Ignorance</h3>
<ul>
 	<li>Persistence ignorance is valuable because it allows the same business model to be persisted in multiple ways, offering additional flexibility to the application.</li>
 	<li>Persistence choices might change over time, from one database technology to another, or additional forms of persistence might be required in addition to whatever the application started with (for example, using a Redis cache or Azure Cosmos DB in addition to a relational database).</li>
 	<li>Persistence ignorance (PI) refers to types that need to be persisted, but whose code is unaffected by the choice of persistence technology. Such types in .NET are sometimes referred to as Plain Old CLR Objects (POCOs), because they do not need to inherit from a particular base class or implement a particular interface.</li>
 	<li>Some examples of violations of this principle include:
• A required base class
• A required interface implementation
• Classes responsible for saving themselves (such as the Active Record pattern)
• Required default constructor
• Properties requiring virtual keyword
• Properties forced to use certain types (for example, collection properties must expose ICollection, not just IEnumerable)
• Persistence-specific required attributes</li>
</ul>
<h3>Bounded Contexts</h3>
<ul>
 	<li>Bounded contexts are a central pattern in Domain-Driven Design.</li>
 	<li>They provide a way of tackling complexity in <strong>large applications or organizations by breaking it up into separate</strong> conceptual modules.</li>
 	<li>Each conceptual module then represents a context which is separated from other contexts (hence, bounded), and can evolve independently.</li>
 	<li>Each bounded context should ideally be free to choose its own names for concepts within it and should have exclusive access to its own persistence store.</li>
 	<li>At a minimum, individual web applications should strive to be their own bounded context, with their own persistence store for their business model, rather than sharing a database with other applications.</li>
 	<li>Communication between bounded contexts occurs through programmatic interfaces, rather than through a shared database, which allows for business logic and events to take place in response to
changes that take place.</li>
 	<li>Bounded contexts map closely to microservices, which also are ideally
implemented as their own individual bounded contexts.</li>
</ul>
<h2>Important Design principles</h2>
<ol>
 	<li>SOLID</li>
 	<li><b>"Good enough" principle</b></li>
 	<li><b>Don't repeat yourself (DRY)</b></li>
 	<li>Keep it Simple and Sweet / Stupid. ( KISS)</li>
 	<li>YAGNI (You aren’t going to need it. So don’t implement it).</li>
 	<li>Hollywood Principle. ( Don’t call use, we will call you )</li>
 	<li>Least Knowledge Principle. (Only talk to your immediate friends. Classes that they inherit from, objects that they contain, objects passed by argument)</li>
 	<li>Depend on Abstractions, Not Concrete classes.</li>
 	<li>Program to Interface Not Implementation.</li>
 	<li>Minimize Coupling</li>
 	<li>Maximize Cohesion</li>
</ol>
<h4><b>KISS </b><b></b></h4>
KISS is an acronym for "Keep it simple, stupid" : most systems work best if they are kept simple rather than made complicated;

<i>“Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.”</i> -Brian Kernighan
<h4><span style="font-weight: bold;">"Good enough" principle</span></h4>
The <b>principle of good enough</b> or <b>"good enough" principle</b> is a rule for <u>software</u> and <a href="http://en.wikipedia.org/wiki/Systems_design"><u>systems design</u></a>. It indicates that consumers will use products that are good enough for their requirements, despite the availability of more advanced technology.

<b>YAGNI - "You aren't gonna need it" </b><b></b>

a principle of <a href="http://en.wikipedia.org/wiki/Extreme_programming"><u>extreme programming</u></a> (XP) that states a <a href="http://en.wikipedia.org/wiki/Programmer"><u>programmer</u></a> should not add functionality until deemed necessary. <u></u>

<i>“Decide as late as possible: Delaying decisions as much as possible </i><b><i>until they can be made based on facts</i></b><i> and not on uncertain assumptions and predictions.</i><i></i>

<i>“Always implement things when you actually need them, never when you just foresee that you need them.”</i> – Ron Jeffries

<hr />

<h1>OOPS</h1>
<strong>Identifying Classes from requirements</strong>
<ul>
 	<li>Prepare requirements document as set of rules</li>
 	<li>While analysing the requirements,
<ol>
 	<li>Nouns in rules represent objects.</li>
 	<li>Adjectives of the noun represent attributes (or properties).</li>
 	<li>Verb represents methods (or functions).</li>
</ol>
</li>
</ul>
<ul>
 	<li>A class is a blueprint for creating an object.</li>
 	<li>An object is an implementation of the class</li>
</ul>
<h2><b>Fundamental principles of OOP</b>:</h2>
<ul>
 	<li><b>Encapsulation</b>
<ul>
 	<li>The combining together of<strong> attributes (data) and methods (behaviour/processes)</strong> into a <strong>single abstract data type with a public interface and a private implementation.</strong> This allows the implementation to be altered without affecting the interface.</li>
 	<li>Use : <strong>Consumer needs not to know the implementation</strong> in order to use it.</li>
</ul>
</li>
 	<li><b>Abstraction</b>
<ul>
 	<li>Abstraction means <b>working with something we know how to use without knowing how it works internally</b>.</li>
 	<li>to deal with objects considering their important characteristics and ignore all other details.</li>
 	<li>How to Achieve A design in which the names of classes, methods, and other elements convey both the original developer’s purpose in creating them and their value to a client developer. If a developer must consider the implementation of a component in order to use it, the value of encapsulation is lost.</li>
</ul>
</li>
 	<li><b>Inheritance</b>
<ul>
 	<li>The derivation of one class from another so that the attributes and methods of one class are part of the definition of another class. The first class is often referred to the base or parent class.</li>
</ul>
</li>
 	<li><b>Polymorphism</b>
<ul>
 	<li>Polymorphic <strong>methods</strong> are used which have <strong>one name but different implementations</strong> for different classes.</li>
 	<li><b>Polymorphism Types</b>
<ol>
 	<li>Method overloading - <strong>Static</strong> Polymorphism / Static Binding / <strong>Early binding</strong> /.(in same class) - is the polymorphism exhibited at compile time.</li>
 	<li>Method overriding – <strong>Dynamic</strong> Polymorphism / Dynamic binding / <strong>Runtime</strong> binding/.(in different classes.) - is the polymorphism exhibited at run time.</li>
</ol>
</li>
</ul>
</li>
 	<li>Some OOP theorists also put the concept of <b>exception handling</b> as additional <b>fifth fundamental principle of OOP</b>.</li>
</ul>
<strong>SOLID</strong>

<a href="http://zeroturnaround.com/rebellabs/object-oriented-design-principles-and-the-5-ways-of-creating-solid-applications/"><u>http://zeroturnaround.com/rebellabs/object-oriented-design-principles-and-the-5-ways-of-creating-solid-applications/</u></a>
<table style="height: 3152px; width: 794px;" border="1">
<tbody>
<tr style="height: 13px;">
<td style="height: 13px; width: 792px;" colspan="3" valign="middle"><a href="http://deviq.com/single-responsibility-principle/">The Single Responsibility Principle</a> (SRP)</td>
</tr>
<tr style="height: 39.0811px;">
<td style="height: 39.0811px; width: 10px;" valign="middle"></td>
<td style="height: 39.0811px; width: 369.801px;" valign="middle">· An entity (an object, a class) should have only a single responsibility

· A responsibility is, in fact, a reason to change

· A class should have one, and only one reason to change.

If a class has poor cohesion, some part of it may change that only certain depending classes utilize, while the rest of it may remain unchanged. Nonetheless, classes that depend on the class must all be retested as a result of the change, increasing the total surface area of the application that is affected by the change.</td>
<td style="height: 39.0811px; width: 412.199px;" valign="top">This means that every class, or similar structure, in your code should have only one job to do.

Example: The clear separation between Customer and Savings Account. A customer may have multiple accounts.

Tip: If you have (1. Regions inside your methods, 2.longer methods) you are NOT adhering to the Single Responsibility Principle!

If you grok only one of the SOLID principles, make it Single Responsibility Principle. Everything else flows from that.

Few people realize that the single responsibility principle and the open/closed principle are the same.</td>
</tr>
<tr style="height: 29px;">
<td style="height: 29px; width: 792px;" colspan="3" valign="middle"><a href="http://deviq.com/open-closed-principle/">The Open Closed Principle</a> (OCP)</td>
</tr>
<tr style="height: 433px;">
<td style="height: 433px; width: 10px;" valign="middle"></td>
<td style="height: 433px; width: 369.801px;" valign="middle">Software entities (classes, modules, methods, etc.) should be Open for extension, closed for modification

You should be able to change the behaviour of a method by extending a class (or behaviour passed as a parameter), without modifying it.

Abstractions through inheritance - changed behaviour through polymorphism Open for extension: behaviour of classes can be extended to satisfy changing requirements

Closed for modification: classes themselves are not allowed to change</td>
<td style="height: 433px; width: 412.199px;" valign="top">Once you have developed a class you should never modify it, except to correct bugs.

If you need a additional modified behaviour of a class just change that class. This is however wrong. The answer here is the abstraction. In OO it is possible to create abstractions with fixed design but limitless behaviours

Example Web API. In case of changes required in the interface new version of interface will be created, instead of changing existing

The Open-Closed Principle can also be achieved in many other ways, including through the use of inheritance or through compositional design patterns like the <a href="http://deviq.com/most-popular-patterns/strategy-design-pattern">Strategy pattern</a>.

The strategy pattern is the backbone of the Open/Closed Principle.</td>
</tr>
<tr style="height: 24px;">
<td style="height: 24px; width: 792px;" colspan="3" valign="middle"><a href="http://deviq.com/liskov-substitution-principle/">The Liskov Substitution Principle</a> (LSP) / Design by contract / Preconditions, Postconditions &amp; Invariants</td>
</tr>
<tr style="height: 134px;">
<td style="height: 134px; width: 10px;" valign="middle"></td>
<td style="height: 134px; width: 369.801px;" valign="middle">Definition: (LSP) states that subtypes must be substitutable for their base types without the client knowing about the change

· Rule: It is allowed to weaken preconditions and strengthen postconditions in overridden methods, but not vice versa

· If you can not satisfy this rule then you need to refactor the class hierarchy. Typically, those two types should be in the same level of the hierarchy. There is a superclass for both of these classes</td>
<td style="height: 134px; width: 412.199px;" valign="top">Examples
<ol>
 	<li>DBConnection is substitutable with SQLconnection or Oracleconnection</li>
 	<li>Joint account can be derived from Saving account which will have extra parameters for the multiple accounts.</li>
 	<li>square is not the subtype of the rectangle as rectangle length need not be equal to the width. (rectangle can't be subtype of square as well)</li>
</ol>
A very common violation of this principle is the partial implementation of interfaces or base class functionality, leaving unimplemented methods or properties to throw an exception (e.g. NotImplementedException).</td>
</tr>
<tr style="height: 36px;">
<td style="height: 36px; width: 792px;" colspan="3" valign="middle"><a href="http://deviq.com/interface-segregation-principle/">The Interface Segregation Principle</a> (ISP)</td>
</tr>
<tr style="height: 34px;">
<td style="height: 34px; width: 10px;" valign="middle"></td>
<td style="height: 34px; width: 369.801px;" valign="middle">Clients should not be forced to depend on methods that they do not use.

Make fine grained interfaces that are client specific.

ISP guides us to create multiple, smaller, cohesive interfaces.

Interfaces should belong to clients, not to libraries or hierarchies.</td>
<td style="height: 34px; width: 412.199px;" valign="top">Examples
<ol>
 	<li>Separate interfaces have to be created for the Savings Account and OD Account. There will be a common interface for Account. Separate interfaces for Savings account (interest calculation) and OverDraft Account (Mortages)</li>
 	<li>Having an IRepository interface composed of an IReadOnlyRepository and an IWriteRepository would allow base implementations that go against a data store and separate implementations that employ caching and queuing, as well.</li>
</ol>
</td>
</tr>
<tr style="height: 26px;">
<td style="height: 26px; width: 792px;" colspan="3" valign="middle"><a href="http://deviq.com/dependency-inversion-principle/">The Dependency Inversion Principle</a> (DIP)</td>
</tr>
<tr style="height: 270px;">
<td style="height: 270px; width: 10px;" valign="middle"></td>
<td style="height: 270px; width: 369.801px;" valign="middle">Depend on abstractions, not on concretions.

high-level modules should not depend upon low-level modules; they should depend on abstractions.

abstractions should not depend upon details; details should depend upon abstractions.

The implementation of the interface is provided when the form is created, through a process known as <a href="http://deviq.com/dependency-injection">Dependency Injection</a>.</td>
<td style="height: 270px; width: 412.199px;" valign="top">Example
<ol style="list-style-type: lower-alpha;">
 	<li>Let’s say, once credit score reaches the certain limit, OD account is provided.</li>
 	<li>The implementation can’t happen on the CreditScore class directly.</li>
 	<li>The CreditScore might have used for LoanAgainstGold as well.</li>
 	<li>Create a separate ICreditScore interface as parent of CreditScore class. ODAccount can depend upon the ICreditScore.</li>
 	<li>Further Adapter pattern could be used to convert the event to the necessary format for the ODAccount.</li>
</ol>
</td>
</tr>
</tbody>
</table>

<hr />

<a href="http://deviq.com/Pain-Driven-Development/"><strong>Pain Driven Development (PDD)</strong></a>

It’s a variation of <a href="http://deviq.com/yagni/">YAGNI</a> that ensures you are <strong>not blindly gold-plating the codebase</strong> without adding value to the customer. It means waiting to apply <a href="http://deviq.com/category/principles/">principles</a>, <a href="http://deviq.com/category/patterns/">patterns</a>, and <a href="http://deviq.com/category/practices/">practices</a> to your code until there is some pain the current approach is causing that must be addressed.

<strong>Example:</strong> No software can be open to extension, but closed to modification in every possible way. If it were, it would be too abstract to be useful – like shipping an IDE to your customer so they can build whatever they want, instead of shipping them the actual software they’ve asked for.
<figure id="attachment_612" class="wp-caption aligncenter"><figcaption class="wp-caption-text">Rate your code pain from low to stepping on a Lego…</figcaption></figure>
Some kinds of pain may make sense to avoid altogether. This includes pain that will be very difficult to alleviate in the future. <strong>Example:</strong> If you know that you are going to want to be able to decouple your UI layer from your Data layer, for instance, because you’ve experienced the pain of tight coupling enough times in the past, better implement the same.

&nbsp;
<h2>References</h2>
Separation of Concerns
https://deviq.com/separation-of-concerns/
Encapsulation
https://deviq.com/encapsulation/
Dependency Inversion Principle
https://deviq.com/dependency-inversion-principle/
Explicit Dependencies Principle
https://deviq.com/explicit-dependencies-principle/
Don’t Repeat Yourself
https://deviq.com/don-t-repeat-yourself/
Persistence Ignorance
https://deviq.com/persistence-ignorance/
Bounded Context
https://martinfowler.com/bliki/BoundedContext.html
Domain-Driven Design Fundamentals
http://bit.ly/ddd-fundamentals
SOLID Principles of Obj
