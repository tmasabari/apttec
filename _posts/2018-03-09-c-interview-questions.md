---
layout: post
title: c# interview questions
date: 2018-03-09 13:11
author: tmasabari
comments: true
categories: [Interview Preparation, Prepare, QuickRefresh, Uncategorized]
---
<ol>
 	<li>Managed/Unmanaged resources</li>
 	<li>Value/Reference types. Where reference for reference type is stored? Is Stack the only place where value type can be stored?</li>
 	<li>Stack/Heap. What is the purpose of Stack? What is stack as an abstract data type?</li>
 	<li>Generics</li>
 	<li>Linq, IQueriable&lt;&gt;</li>
 	<li>Dynamic</li>
 	<li>Reflection
<ol>
 	<li>Aspect Oriented Programming (AOP)</li>
</ol>
</li>
 	<li>CodeGeneration
<ol>
 	<li>Expression Trees</li>
 	<li>CodeDom</li>
 	<li>Emit</li>
</ol>
</li>
</ol>
<em>what happens while using the "using keyword".
abstract class and interface - when and how to use</em>

<em>What is the use of abstract
difference between const and readonly.</em>

<em>difference between var and dynamic keyword.</em>

<em>What is garbage collection and its usage</em>

<em>What is the generic, what is the usage</em>

<em>Extension method, how it has to be created</em>

<em>What is the ref key word and what is the out parameter</em>

<em>Partial class, usage</em>

<em>Construct – how many types, usage, </em><em>What is the copy construct</em>

<em>What is the CSRF? How will u implement?</em>

Post Sharp

advanced http://cybarlab.com/advance-c-sharp-interview-questions-and-answers

basics http://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/

http://www.iminfo.in/post/advanced-c-sharp-dot-net-interview-questions-for-experienced–developers

<hr />

<strong>What is attribute in C#?</strong>
An attributes is a declarative tag that is used to convey information about the behaviors of various elements (classes, methods, assemblies, structures, enumerators, etc). it is access at compile time or run-time.

The Microsoft .Net Framework allows creating custom attributes that can be used to store declarative information and can be retrieved at run-time.

<hr />

<h2>Managed/Unmanaged resources</h2>
<ul>
 	<li>The code, which is developed in .NET framework is known as managed code. This code is directly executed by CLR with the help of managed code execution. Any language that is written in .NET Framework is managed code</li>
 	<li>Applications that do not run under the control of the CLR are said to be unmanaged, and certain languages such as C++ can be used to write such applications, which, for example, access low - level functions of the operating system. Background compatibility with the code of VB, ASP and COM are examples of unmanaged code. Unmanaged code can be unmanaged source code and unmanaged compile code. Unmanaged code is executed with the help of wrapper classes.
Wrapper classes are of two types:
<ul>
 	<li>CCW (COM Callable Wrapper).</li>
 	<li>RCW (Runtime Callable Wrapper).</li>
</ul>
</li>
</ul>
&nbsp;

<a href="https://stackoverflow.com/questions/3607213/what-is-meant-by-managed-vs-unmanaged-resources-in-net">https://stackoverflow.com/questions/3607213/what-is-meant-by-managed-vs-unmanaged-resources-in-net</a>

The term "unmanaged resource" is usually used to describe something <em>not directly under the </em><em>control of the garbage collector</em>.
<ul>
 	<li><span class="comment-copy">Adding a bit more clarification: SqlConnection (or FileStream, etc) are managed resources which internally use unmanaged resources which GC is unaware of.</span>  File handles, pinned memory, COM objects, database connections etc. These wrapper classes (File, DbConnection etc.) are managed, but they inside use unmanaged resources the same way like you, if you don't use the wrappers and do the "dirty work" by yourself. And therefore these wrappers DO implement Dispose/Finalize patterns.</li>
 	<li>For those, which implement dispose/finalise (you recognize them, that they implement IDisposable), implement also your dispose/finalise pattern and Dispose even these wrappers or give them signal to release their unmanaged resources. If you don't, the resources will be after some indefinite time released, but it is clean to release it immediately (close the file immediately and not leaving it open and blocked for random several minutes/hours). So in your class's Dispose method you call Dispose methods of all your used wrappers.</li>
</ul>
<pre class="default prettyprint prettyprinted"><code><span class="kwd">using</span> <span class="pun">(</span><span class="kwd">var</span><span class="pln"> connection </span><span class="pun">=</span> <span class="kwd">new</span> <span class="typ">SqlConnection</span><span class="pun">(</span><span class="str">"connection_string_here"</span><span class="pun">)) {}</span></code></pre>

<hr />

<h3>Garbage Collection</h3>
<a href="https://stackoverflow.com/questions/2257563/what-are-the-generations-in-garbage-collection">https://stackoverflow.com/questions/2257563/what-are-the-generations-in-garbage-collection</a>

<a href="https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals">https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals</a>
<p class="lf-text-block lf-block" data-lf-anchor-id="9dd0aced1f196e53231dec4366125351:0">In the common language runtime (CLR), the garbage collector serves as an automatic memory manager. It provides the following benefits:<span class="lf-thread-btn"><a class="fycon-action-view" tabindex="0" aria-label="Write a Sidenote" data-lf-anchor-id="9dd0aced1f196e53231dec4366125351:0">+</a></span></p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="0dc5ee657796dc9369e9559771016751:0">
 	<li>Enables you to develop your application without having to free memory.
<ul>
 	<li>Allocates objects on the managed heap efficiently.</li>
 	<li>Reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. Managed objects automatically get clean content to start with, so their constructors do not have to initialize every data field.</li>
</ul>
</li>
 	<li>
<p class="">Provides memory safety by making sure that an object cannot use the content of another object.</p>
</li>
</ul>
The heap is organized into generations so it can handle long-lived and short-lived objects.

Generation 0 – Short-lived Objects
Generation 1- As a buffer between short lived and long lived objects
Generation 2 – Long lived objects
<ol>
 	<li>Generation 0 identifies a newly created object that has never been marked for collection. When an object is first created, it is put into generation 0.</li>
 	<li>Generation 1 identifies an object that has survived a GC (marked for collection but not removed because there was sufficient heap space). If the creation of an object causes the generation 0 to surpass it’s budget, garbage colllection is started. <span style="text-decoration: underline;">The objects which are not collected in Generation 0 are moved to Generation 1 and Generation 0 is emptied.</span></li>
 	<li>Generation 2 identifies an object that has survived more than one sweep of the GC. Over the several generation 0 collection, <span style="text-decoration: underline;">generation 1 may surpass </span>it’s<span style="text-decoration: underline;"> budget limit</span> which cause GC to collect the Garbage from both generations. In this case, <span style="text-decoration: underline;">generation 1 survivors are promoted to generation 2, generation 0 survivors are promoted to generation 1, and generation 0 is empty.</span></li>
</ol>
Because objects in generations 0 and 1 are short-lived, these generations are known as the ephemeral generations.
<p class="lf-text-block lf-block" data-lf-anchor-id="ef954dcf5fb9c6bb38cf88454f376b45:0">The size of the ephemeral segment varies depending on whether a system is 32- or 64-bit, and on the type of garbage collector it is running. Default values are shown in the following table.</p>

<table border="1">
<thead>
<tr>
<th></th>
<th>32-bit</th>
<th>64-bit</th>
</tr>
</thead>
<tbody>
<tr>
<td>Workstation GC</td>
<td>16 MB</td>
<td>256 MB</td>
</tr>
<tr>
<td>Server GC</td>
<td>64 MB</td>
<td>4 GB</td>
</tr>
<tr>
<td>Server GC with &gt; 4 logical CPUs</td>
<td>32 MB</td>
<td>2 GB</td>
</tr>
<tr>
<td>Server GC with &gt; 8 logical CPUs</td>
<td>16 MB</td>
<td>1 GB</td>
</tr>
</tbody>
</table>
&nbsp;
<p id="mdNzrLm"><a href="http://www.csharpstar.com/csharp-interview-questions-part-2/"><img class="alignnone  wp-image-1035 " src="/wp-content/uploads/2018/03/img_5aacbe5982a61.png" alt="" width="553" height="459" /></a></p>


<hr />

<h3>catch multiple exceptions at once in C#</h3>
In C#6.0,
<div id="crayon-5a0e873dc2e3d502665664" class="crayon-syntax crayon-theme-vs2012-black crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums " data-settings="show">
<div class="crayon-nums-content">
<div class="crayon-num" data-line="crayon-5a0e873dc2e3d502665664-1">1</div>
<div class="crayon-num crayon-striped-num" data-line="crayon-5a0e873dc2e3d502665664-2">2</div>
<div class="crayon-num" data-line="crayon-5a0e873dc2e3d502665664-3">3</div>
<div class="crayon-num crayon-striped-num" data-line="crayon-5a0e873dc2e3d502665664-4">4</div>
<div class="crayon-num" data-line="crayon-5a0e873dc2e3d502665664-5">5</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-5a0e873dc2e3d502665664-1" class="crayon-line"><span class="crayon-st">catch</span> <span class="crayon-sy">(</span><span class="crayon-e">Exception </span><span class="crayon-v">ex</span><span class="crayon-sy">)</span> <span class="crayon-e">when</span> <span class="crayon-sy">(</span><span class="crayon-e">ex </span><span class="crayon-st">is</span> <span class="crayon-v">FormatException</span> <span class="crayon-o">||</span> <span class="crayon-e">ex </span><span class="crayon-st">is</span> <span class="crayon-v">OverflowException</span><span class="crayon-sy">)</span><span class="crayon-h">           </span></div>
<div id="crayon-5a0e873dc2e3d502665664-2" class="crayon-line crayon-striped-line"><span class="crayon-sy">{</span><span class="crayon-h">                </span></div>
<div id="crayon-5a0e873dc2e3d502665664-3" class="crayon-line"><span class="crayon-h">   </span><span class="crayon-v">testid</span> <span class="crayon-o">=</span> <span class="crayon-s">""</span><span class="crayon-sy">;</span></div>
<div id="crayon-5a0e873dc2e3d502665664-4" class="crayon-line crayon-striped-line"><span class="crayon-h">   </span><span class="crayon-st">return</span><span class="crayon-sy">;</span></div>
<div id="crayon-5a0e873dc2e3d502665664-5" class="crayon-line"><span class="crayon-sy">}</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
&nbsp;

<span style="font-weight: bold;"><u>Value  Type Vs Reference Type Vs Pointers</u></span>
<ol>
 	<li><a href="https://blogs.msdn.microsoft.com/ericlippert/2009/02/17/references-are-not-addresses/">https://blogs.msdn.microsoft.com/ericlippert/2009/02/17/references-are-not-addresses/</a></li>
 	<li><a href="https://blogs.msdn.microsoft.com/ericlippert/2009/04/27/the-stack-is-an-implementation-detail-part-one/">https://blogs.msdn.microsoft.com/ericlippert/2009/04/27/the-stack-is-an-implementation-detail-part-one/</a></li>
 	<li><a href="https://blogs.msdn.microsoft.com/ericlippert/2010/09/30/the-truth-about-value-types/">https://blogs.msdn.microsoft.com/ericlippert/2010/09/30/the-truth-about-value-types/</a></li>
 	<li>https://www.codeproject.com/Articles/76153/Six-important-NET-concepts-Stack-heap-value-types</li>
</ol>
<ul>
 	<li>When we assign the <code>int</code> value to the other <code>int</code> value, it creates a completely different copy. In other words, if you change either of them, the other does not change. These kinds of data types are called as ‘Value types’.</li>
 	<li>When we create an object and when we assign an object to another object, they both point to the same memory location. In other words if we change one of them, the other object is also affected; this is termed as ‘Reference types’.</li>
 	<li>When the data moves from value types to reference types, it is termed ‘Boxing’ and the reverse is termed ‘UnBoxing’.</li>
 	<li>I dearly wish that all those articles explaining what “the stack” is would instead spend time explaining what exactly “copied by value” means and how misunderstanding or misusing “copy by value” can cause bugs.</li>
 	<li>Versions of C# provided by other vendors may choose other allocation strategies for their temporary variables; there is no language requirement that a data structure called "the stack" be used to store locals of value type. The jitter <strong>could choose to put every local “on the heap”</strong> and live with the performance cost of doing so, as long as the value type semantics were maintained.</li>
 	<li>"<em>a variable of reference type <strong>stores the</strong> <b>reference </b>of the object</em>".</li>
 	<li>Pointers are strictly "more powerful" than references; <strong>anything you can do with references you can do with pointers</strong>, but not vice versa.</li>
 	<li>Pointers are typically <em>implemented</em> as <strong>addresses</strong>. An address is a number which is an offset into the "array of bytes" that is the entire virtual address space of the process.  Since addresses are just numbers you can easily perform pointer arithmetic with them</li>
 	<li>The spec just says that a variable of reference type "stores a reference" to an object, and leaves it completely vague as to how that might be implemented. Similarly, a pointer variable stores "the address" of an object, which again, is left pretty vague.</li>
 	<li>You cannot do anything with a reference except dereference it, and compare it with another reference for equality.</li>
 	<li>We see that references and instances of value types are essentially the same thing as far as their storage is concerned; they go on either the stack, in registers, or the heap depending on whether the storage of the value needs to be short-lived or long-lived.</li>
 	<li>It is frequently the case that array elements, fields of reference types, locals in an iterator block and closed-over locals of a lambda or anonymous method must live longer than the activation period of the method that first required the use of their storage. And even in the rare cases where their lifetimes are shorter than that of the activation of the method, it is difficult or impossible to write a compiler that knows that. Therefore we must be conservative: all of these storage locations go on the heap.</li>
 	<li>It is frequently the case that local variables and temporary values can be shown via compile-time analysis to be unused after the activation period ends, and therefore can be treated short-lived, and therefore can go onto the stack or put into registers.</li>
 	<li>There are three kinds of values: (1) instances of value types, (2) instances of reference types, and (3) references. (Code in C# cannot manipulate instances of reference types directly; it always does so via a <em>reference</em>. In unsafe code, pointer types are treated like value types for the purposes of determining the storage requirements of their values.)</li>
 	<li>Value types are allocated on the stack <em>sometimes</em>. For example, the memory for an integer field in a class type is part of the <strong>class instance’s memory, which is allocated on the heap</strong>. A local variable is hoisted to be implemented as a field of a hidden class if the <strong>local is an outer variable used by an anonymous method(</strong>*) so again, the storage associated with that local variable will be on the <strong>heap</strong> if it is of value type.</li>
 	<li></li>
</ul>

<hr />

https://dzone.com/articles/event-vs-delegate

<strong>Event and Delegate both follow the Observer pattern</strong>.
<ul>
 	<li><a href="https://dzone.com/articles/event-vs-delegate">Delegate in C# is</a> a reference type, which holds a reference to the function and invokes the function when called with an Invoke method. In a class, delegate object <strong>needs to be accessible by client</strong> to add event handler if used directly. <strong>No safety.</strong></li>
 	<li>Event in C# is a type of Delegate, which means that if one wants to use Event, then one must define delegate first. Events can have multiple event-handler functions, which have a signature like Delegate, and get called when an Event is raised by some other Event in an application.</li>
 	<li>
<pre><span class="cm-variable">eventTest</span>.<span class="cm-variable">PrintEvent</span> <span class="cm-operator">=</span> <span class="cm-keyword">new</span> <span class="cm-variable">PrintEvent</span>()<strong><span class="cm-comment">//Not allowed in C#</span></strong></pre>
</li>
</ul>
The difference between both is that <strong>Event wraps Delegate</strong> type, and makes Delegate<strong> not modifiable</strong> in terms of changing references, i.e. assigning a new object is not possible.

Both Event and Delegate do the same task, which is to hold event handlers and call them when delegate or event are invoked.
<div>
<pre><span class="cm-keyword">public</span> <span class="cm-variable">delegate</span> <span class="cm-variable">void</span> <span class="cm-variable">Print</span>(<span class="cm-keyword">string</span> <span class="cm-variable">val</span>);     
<span class="cm-keyword">public</span> <span class="cm-variable">event</span> <span class="cm-variable">Print</span> <span class="cm-variable">PrintEvent</span>;
public virtual void OnPrintEvent() { 
 if (PrintEvent != null) 
 PrintEvent("Test"); 
 }

</pre>
<ol>
 	<li>Event is very helpful to create <strong>Notification systems</strong>. The same is not possible with Delegate because <strong>Delegate cannot be exposed as public</strong>.</li>
 	<li><strong>Delegate</strong> is very helpful to <strong>create call back functions</strong>, i.e pass delegate as function argument, which is <strong>not possible with Event</strong>.</li>
</ol>
</div>

<hr />

<h3><span style="font-weight: bold;">Generics</span></h3>
<ul>
 	<li>Generics provide type safety without the overhead of multiple implementations.</li>
 	<li>Generics eliminates boxing and unboxing.</li>
 	<li>There is no need to write code to test for the correct data type because it is enforced at compile time. The need for type casting and the possibility of run-time errors are reduced.</li>
 	<li>By providing strong typing, a class built from a generic lets visual studio provide IntelliSense.</li>
 	<li>Generic collection types generally perform better for storing and manipulating value types because there is no need to box the value types</li>
 	<li>Generic delegates enable type-safe callbacks without the need to create multiple delegate classes.</li>
</ul>
<strong>What is Collections in C#?</strong>

Collections are two types. One is standard collections, which is found under System.Collections namespace and another one is generic collections, which is found under System.Collections.Generic namespace.
<ul>
 	<li>Array List, Stack and Queues provide collections which are not type safe. This leads 2 problems first it's not type safe and second it leads to boxing and unboxing.</li>
 	<li>By using generics we can have type safety and also we can avoid boxing and unboxing.</li>
 	<li>Avoids redunancy of code by implementing common class</li>
</ul>
Example Common Repository class to perform common operations like top in all tables.

&nbsp;
<h3><a href="http://www.dotnettricks.com/learn/linq/difference-between-deferred-execution-and-immediate-execution">Deferred VS Immediate</a> "In process" vs out-of-process</h3>
<ul>
 	<li>In case of differed execution, a query is not executed at the point of its declaration. It is executed when the Query variable is iterated by using loop like as for, foreach.</li>
 	<li>In case of immediate execution, a query is executed at the point of its declaration. The query which returns a singleton value (a single value or a set of values) like Average, Sum, Count, List etc. caused Immediate Execution.</li>
</ul>
Query execution:
<ul>
 	<li>Where the execution of a query is going to be performed <strong>"in process"</strong>, typically all that's required is the code (as code) to execute each part of the query.</li>
 	<li>Where the execution will be performed <strong>out-of-process</strong>, the logic of the query has to be represented in data such that the LINQ provider can convert it into the appropriate form for the out-of-memory execution - whether that's an LDAP query, SQL or whatever.</li>
</ul>
You can force a query to execute immediately of by calling ToList, ToArray methods.

http://naweenblogs.blogspot.in/2014/03/extension-methods.html

<a class="question-hyperlink" href="https://stackoverflow.com/questions/252785/what-is-the-difference-between-iqueryablet-and-ienumerablet"><span style="font-weight: bold;">IQueryable&lt;T&gt; and IEnumerable&lt;T&gt;?</span></a>

First of all, <a title="MSDN reference" href="http://msdn.microsoft.com/en-us/library/bb351562.aspx" rel="noreferrer"><code>IQueryable&lt;T&gt;</code></a> <em>extends</em> the <code>IEnumerable&lt;T&gt;</code> interface, so anything you can do with a "plain" <code>IEnumerable&lt;T&gt;</code>, you can also do with an <code>IQueryable&lt;T&gt;</code>.

Yes, both will give you <a href="https://msdn.microsoft.com/en-us/library/bb738633(v=vs.110).aspx#Anchor_0" rel="noreferrer">deferred execution</a>.
<ul>
 	<li>The difference is that <a href="https://msdn.microsoft.com/en-us/library/bb351562.aspx" rel="noreferrer"><code>IQueryable&lt;T&gt;</code></a> is the interface that allows LINQ-to-SQL (LINQ.-to-anything really) to work. So if you further refine your query on an <a href="https://msdn.microsoft.com/en-us/library/bb351562.aspx" rel="noreferrer"><code>IQueryable&lt;T&gt;</code></a>, that query will be executed in the database, if possible.</li>
 	<li>For the <a href="https://msdn.microsoft.com/en-us/library/9eekhta0.aspx" rel="noreferrer"><code>IEnumerable&lt;T&gt;</code></a> case, it will be LINQ-to-object, meaning that all objects matching the original query will have to be loaded into memory from the database.</li>
 	<li><code>IQueryable</code> is only useful if the underlying data provider can do something with it.
<table>
<tbody class="js-comments-list" data-addlink-disabled="true" data-comments-unavailable="false" data-cansee="true" data-canpost="false" data-remaining-comments-count="12">
<tr id="comment-32483130" class="comment js-comment ">
<td class="comment-text js-comment-text-and-form">
<div class="comment-body"><span class="comment-copy">Another reason to prefer <code>IEnumerable</code> to <code>IQueryable</code> is that not <strong>all LINQ operations are supported by all LINQ providers</strong>. So as long as you know what you're doing, you can use <strong><code>IQueryable</code> to push as much of the query</strong> to the LINQ provider (LINQ2SQL, EF, NHibernate, MongoDB etc.). But if you let other code do whatever it wants with your <code>IQueryable</code> you'll eventually end up in trouble because some client code somewhere used an unsupported operation. I agree with the recommendation to not release <code>IQueryable</code>s "into the wild" past the repository or equivalent layer</span></div></td>
</tr>
</tbody>
</table>
<code></code></li>
</ul>
The primary difference is that the LINQ operators for <strong><code>IQueryable&lt;T&gt;</code></strong> take <strong><code>Expression</code></strong> objects<strong> instead of delegates</strong>, meaning the custom query logic it receives, e.g., a predicate or value selector, is in the form of an <strong>expression tree</strong> instead of a delegate to a method.
<ul>
 	<li>The <code>IEnumerable</code> version signature is: <code>Where(Func&lt;Customer, bool&gt; predicate)</code></li>
 	<li>The <code>IQueryable</code> version signature is: <code>Where(Expression&lt;Func&lt;Customer, bool&gt;&gt; predicate)</code></li>
</ul>
<ul>
 	<li><code>IEnumerable&lt;T&gt;</code> is great for working with sequences that are iterated in-memory, but</li>
 	<li><code>IQueryable&lt;T&gt;</code> allows for out-of memory things like a remote data source, such as a database or web service.</li>
 	<li>So the difference between <code>IQueryable</code> and <code>IEnumerable</code> is about where the filter logic is executed. One executes on the client side and the other executes on the database.So if you working with only in-memory data collection <code>IEnumerable</code> is a good choice but if you want to query data collection which is connected with database `IQueryable is a better choice as it reduces network traffic and uses the power of SQL language.</li>
</ul>
The expression can simply be a constant expression of the object itself or a more complex tree of a composed set of query operators and operands. The query provider's <code>IQueryProvider.Execute()</code>or <code>IQueryProvider.CreateQuery()</code> methods are called with an <em>Expression</em> passed to it, and then either a query result or another <code>IQueryable</code> is returned, respectively

&nbsp;

<hr />

<h3>What are extension methods?</h3>
Extension methods enable you to add methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type.

An extension method is a special kind of static method, but they are called as if they were instance methods on the extended type.
<h3><b>How to use extension methods?</b></h3>
An extension method is a <strong>static method of a static class, where the "this" modifier is applied to the first parameter</strong>. The type of the first parameter will be the type that is extended.

Extension methods are only in scope when you explicitly import the namespace into your source code with a using directive.
<h3>Partial Classes</h3>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-9/">http://www.csharpstar.com/csharp-interview-questions-part-9/</a>

– By Using Partial Classes, multiple developer can work on the same class easily.
– Partial classes are mainly used by code generator to <strong>keep different concerns separate</strong>. Example <strong>auto generation code</strong> vs custom code in ORM frameworks.
– you can also define <strong>Partial methods</strong> as well where a developer can simply define the method and the other developer can implement that.

<hr />

<strong>What is the difference between Object pooling and Connection pooling in C#?</strong>

Object Pooling is something that tries to keep a pool of objects in memory to be re-used later and hence it will reduce the load of object creation to a great extent. Object Pool is nothing but a container of objects that are ready for use. Whenever there is a request for a new object, the pool manager will take the request and it will be served by allocating an object from the pool.

object pool needs to be implemented by custom code

The object pool implementation will increase the size of the pool up to the specified maximum. When the maximum is reached,instead of throwing an exception, it makes the client wait until an object is returned to the pool, and then gives the newly returned object to the waiting client.

<a href="https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql-server-connection-pooling">The connection pooler</a> satisfies requests for connections by reallocating connections as they are released back into the pool. If the maximum pool size has been reached and no usable connection is available, the request is queued.

[check: The connection pool implementation does not have a maximum size parameter – it will keep creating new connections to meet demand (eventually it will hit some system limit and the request will fail in some way that isn’t specified.]

<hr />

<span class="term"><u><span style="font-weight: bold;">Reflection and dynamic</span></u></span>

<a href="https://www.codeproject.com/Articles/593881/What-is-the-difference-between">https://www.codeproject.com/Articles/593881/What-is-the-difference-between</a>

<strong>What is Reflection?</strong>
Reflection is a process by which a computer program can monitor and modify its own structure and behavior. It is a way to explore the structure of assemblies at run time (classes, resources, methods). Reflection is the capability to find out the information about objects, metadata, and application details (assemblies) at run-time. We need to include <em>System.Reflection</em> namespace
<ul>
 	<li>– Load assemblies at runtime
– it allows you to learn what assembly defines a particular item such as a class or enumeration
– List a class’s field,properties, constructors, event and methods
– Get information about a property such as type and if it is read only
– Get and Set property’s value
– Get information about item’s attribute etc..To view attribute information at run time
- It allows dynamic/late binding to methods and properties</li>
 	<li>In serialization, it is used to serialize and de-serialize objects</li>
 	<li>In web service, it is used to create and consume SOAP messages and also to generate WSDL</li>
 	<li>Debugging tools can use reflection to examine the state of an object</li>
</ul>
Reflection is needed when you want to <strong>determine / inspect contents of an assembly</strong>. All code can use reflection to perform the following tasks:<a>+</a>
<ul>
 	<li>dynamically load a class, create object and invoke methods at runtime</li>
 	<li>Enumerate types and members, and examine their metadata.</li>
 	<li>Enumerate and examine assemblies and modules.</li>
</ul>
<a href="https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/security-considerations-for-reflection#accessingNormallyInaccessible">https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/security-considerations-for-reflection#accessingNormallyInaccessible</a>
<ul>
 	<li>One of the biggest practical uses of the <code>dynamic</code> keyword is when we operate on MS Office components via interop.</li>
 	<li>If you are creating an application like a Visual Studio editor where you want to show the internals of an object by using intellisense.</li>
 	<li>If you are creating a unit testing framework. In unit testing frameworks we need to invoke methods and properties dynamically for testing purpose.</li>
 	<li>Sometimes we would like to dump properties, methods, and assembly references to a file or show it on screen.</li>
</ul>
<h4>What is the difference between Reflection and dynamic?</h4>
<ul>
 	<li style="list-style-type: none;">
<ul>
 	<li>Both Reflection and <code>dynamic</code> are used when we want to operate on an object during runtime.</li>
 	<li>Reflection is used to inspect the meta-data of an object. It also has the ability to invoke members of an object at runtime.</li>
 	<li><code>dynamic</code> is a keyword which was introduced in .NET 4.0. It evaluates object calls during runtime. So until the method calls are made the compiler is least bothered if those methods / properties exist or not.</li>
 	<li><code>dynamic</code> uses Reflection internally. It caches the method calls made thus improving performance to a certain extent.</li>
 	<li>Reflection can invoke both public and private members of an object while <code>dynamic</code> can only invoke public members.</li>
 	<li><code>dynamic</code> is instance specific: you don't have access to static members; you have to use Reflection in those scenarios.</li>
</ul>
Below is the detailed comparison table which shows in which scenario they are suited:
<table border="1">
<tbody>
<tr>
<td width="163"></td>
<td width="68"><strong>Reflection</strong></td>
<td><strong>Dynamic</strong></td>
</tr>
<tr>
<td width="163"><strong>Inspect (meta-data) </strong></td>
<td width="68">Yes</td>
<td>No</td>
</tr>
<tr>
<td width="163"><strong>Invoke public members</strong></td>
<td width="68">Yes</td>
<td>Yes</td>
</tr>
<tr>
<td width="163"><strong>Invoke private members</strong></td>
<td width="68">Yes</td>
<td>No</td>
</tr>
<tr>
<td width="163"><span style="color: #ff00ff;"><strong>Caching</strong></span></td>
<td width="68"><span style="color: #ff00ff;">No</span></td>
<td><span style="color: #ff00ff;">Yes</span></td>
</tr>
<tr>
<td width="163"><span style="color: #ff00ff;"><strong>Static class </strong></span></td>
<td width="68"><span style="color: #ff00ff;">Yes</span></td>
<td><span style="color: #ff00ff;">No</span></td>
</tr>
</tbody>
</table>
</li>
</ul>

<hr />

<strong>What is serialization?</strong>
When we want to transport an object through network then we need to convert the object into a stream of bytes. Serialization is a process to convert a complex objects into stream of bytes for storage (database, file, cache, etc) or transfer. Its main purpose is to save the state of an object.
De-serialization is the reverse process of creating an object from a stream of bytes to their original form.

Serialization is used in the following purposes:
<ul>
 	<li>To pass an object from on application to another</li>
 	<li>In SOAP based web services</li>
 	<li>To transfer data through cross platforms, cross devices</li>
</ul>
<strong>What are the types of serialization?</strong>
The types of Serializations are given bellow:
<ul>
 	<li><em>Binary Serialization</em>
In this process all the public, private, read only members are serialized and convert into stream of bytes. This is used when we want a complete conversion of our objects.</li>
 	<li><em>SOAP Serialization</em>
In this process only public members are converted into SOAP format. This is used in web services.</li>
 	<li><em>XML Serialization</em>
In this process only public members are converted into XML. This is a custom serialization. Required namespaces: System.Xml, System.Xml.Serialization.</li>
</ul>
&nbsp;
<h3><u><span class="term"><span style="font-weight: bold;">Aspect-oriented programming</span></span><span style="font-weight: bold;"> (AOP)</span></u></h3>
The attributes that implement the standard and thread safety patterns are called <span class="term">aspects</span>. This term comes from the paradigm of <span class="term">aspect-oriented programming</span> (AOP). An <span class="term">aspect</span> is a class that encapsulates behaviors that are injected into another class, method, field, property or event. The process of injecting an aspect into another piece of code is called <span class="term">weaving</span>.

<strong>PostSharp weaves aspects at build time;</strong> it is also named a <span class="term">build-time aspect weaver</span>.
<ol>
 	<li>Separation of cross cutting concerns to separate modules using attributes</li>
 	<li>Exception handling</li>
 	<li>Auditing</li>
 	<li>Logging</li>
</ol>

<hr />

<strong>What is Code Document Object Model (CodeDom) ?</strong>

<strong><a href="https://www.codeproject.com/Articles/18676/Dynamic-Code-Generation-using-CodeDOM">https://www.codeproject.com/Articles/18676/Dynamic-Code-Generation-using-CodeDOM</a> </strong>

<strong><a href="https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation">https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation</a></strong>

CodeDom (Code Document Object Model) is a <strong>language independent Object-model</strong> which is used to develop language independent source code for developing automatic source code generators. Two important usage of CodeDom are -

1) Templated Code Generation and 2) Dynamic code compilation

Code Document Object Model are used  to minimize repetitive coding tasks, and to minimize the number of human-generated source code lines. CodeDOM (or Code Document Object Model) is a mechanism provided by the .NET Framework which lets us generate source code in multiple languages using a single model.

To represent source code, CodeDOM elements are linked to each other to form a data structure known as a CodeDOM graph, which models the structure of some source code.

The <code>System.CodeDom</code> namespace defines types that can represent the logical structure of source code, independent of a specific programming language. The <code>System.CodeDom.Compiler</code> namespace defines types for generating source code from CodeDOM graphs and managing the compilation of source code in supported languages. Compiler vendors or developers can extend the set of supported languages.
<pre><em><strong>using System.CodeDom;
using System.CodeDom.Compiler;</strong></em></pre>
<pre><strong><em>using Microsoft.CSharp;</em></strong>
</pre>
<pre><a title="https://stackoverflow.com/questions/7852926/microsoft-roslyn-vs-codedom" href="https://stackoverflow.com/questions/7852926/microsoft-roslyn-vs-codedom">https://stackoverflow.com/questions/7852926/microsoft-roslyn-vs-codedom</a></pre>
<pre><span style="font-family: Calibri;"><code>CodeDom</code> and <code>CodeDom.Compiler</code> provide the necessary API to build the code graph and build it. </span></pre>
<pre><span style="font-family: Calibri;"><code>Microsoft.CSharp</code>provides the generator which uses the code graph to generate code in C#.</span></pre>
<pre><span style="font-family: Calibri;">CodeDom is a precursor to Roslyn, but is only marginally related. Essentially, CodeDom is a simple and (somewhat) language agnostic way </span></pre>
<pre><span style="font-family: Calibri;">to generate code that was added in .NET 1.0 to support designers (a la WinForms). </span></pre>
<pre><span style="font-family: Calibri;">Because CodeDom was an attempt at providing a unified model that can generate code in C#, VB, and other languages, </span></pre>
<pre><span style="font-family: Calibri;">it lacks high fidelity with any of the languages that it supports (that's why you can't create a switch statement with CodeDom). </span></pre>
<pre><span style="font-family: Calibri;">CSharpCodeProvider.CompileAssemblyFromSource is simply a wrapper around executing csc.exe</span></pre>
<pre><span style="font-family: Calibri;"> </span></pre>
<pre><span style="font-family: Calibri;">Roslyn can be used as a sophisticated C# and VB source code generator, but that's where the similarity to CodeDom ends. </span></pre>
<pre><span style="font-family: Calibri;">The Roslyn Compiler APIs can be used to parse code, perform semantic analysis, compile and evaluate code dynamically, etc.</span></pre>
Roslyn is a completely different animal. It is a rewrite of both the C# and VB compilers from the ground up using managed code -- C# in C# and VB in VB (the versions of csc.exe and vbc.exe that ship today are written in native code). The advantage of building them in managed code is that users can reference the real compilers as libraries from .NET applications (no wrappers needed).

While building each component of the compiler pipeline, we've exposed public APIs on top:
<ul>
 	<li>Parser -&gt; Syntax Tree API</li>
 	<li>Symbol Table/Metadata Import -&gt; Symbol API</li>
 	<li>Binder -&gt; Binding and Flow Analysis APIs</li>
 	<li>IL Emitter -&gt; Emit API</li>
</ul>
<pre><span style="font-family: Calibri;"> </span></pre>
<pre><span style="font-family: Calibri;"> </span></pre>
<strong>What is Native Image Generator (Ngen.exe) ?</strong>

Ngen.exe creates compiled processor-specific machine code called native images which are files and installs them into the native image cache on the local computer. The runtime will use native images from the cache rather than using the JIT compiler to compile the original assembly.

<strong> </strong>

<strong>What is unsafe code?</strong>

In the CLR, unsafe code is referred to as unverifiable code. In C#, the unsafe code is not necessarily dangerous. The CLR does not verify its safety. The CLR will only execute the unsafe code if it is within a fully trusted assembly. If we use unsafe code, it is our own responsibility to ensure that the code does not introduce security risks or pointer errors.

Some properties of unsafe codes are given bellow:
<ul>
 	<li>We can define Methods, types, and code blocks as unsafe</li>
 	<li>In some cases, unsafe code may increase the application’s performance by removing array bounds checks</li>
 	<li>Unsafe code is required in order to call native functions that require pointers</li>
 	<li>Using unsafe code brings security and stability risks</li>
 	<li>In order to compile unsafe code, the application must be compiled with /unsafe</li>
</ul>
Pointer is a variable that stores the memory address of another variable. Pointers in C# have the same capabilities as in C or C++.
<ul>
 	<li>To deal with existing structures on disk</li>
 	<li>Some advanced COM or Platform Invoke scenarios that involve pointer</li>
 	<li>To performance critical codes</li>
</ul>
<table border="1px">
<tbody>
<tr>
<td>Dispose</td>
<td>Finalize</td>
</tr>
<tr>
<td>It is used to free unmanaged resources at any time.</td>
<td>It can be used to free unmanaged resources held by an object before that object is destroyed.</td>
</tr>
<tr>
<td>It is called by user code and the class which is implementing dispose method, must has to implement IDisposable interface.</td>
<td>It is called by Garbage Collector and cannot be called by user code.</td>
</tr>
<tr>
<td>It is implemented by implementing IDisposable interface Dispose() method.</td>
<td>It is implemented with the help of Destructors</td>
</tr>
<tr>
<td>There is no performance costs associated with Dispose method.</td>
<td>There is performance costs associated with Finalize method since it doesn’t clean the memory immediately and called by GC automatically.</td>
</tr>
</tbody>
</table>
&nbsp;
<p id="IDRwVep"><img class="alignnone size-full wp-image-1036 " src="/wp-content/uploads/2018/03/img_5aacbf5594412.png" alt="" /></p>
<strong>When to use “==” operator and when to use “.Equals()” method?</strong>

For value comparison, with Value Type use “==” operator and use “Equals()” method while performing value comparison with Reference Type.
<h3>What are weakreferences in C#?</h3>
You can use weak references for objects that consume a lot of memory. In using weak references for such objects, you enable those objects to be garbage collected while at the same time allowing those objects to be recreated later if need be. So, if you have a large object in your application that you would use less frequently, you can use weak reference to such objects provided recreating such objects isn't that expensive.
<h3>How is it different than StrongReferences</h3>
Creating a weak reference to an object doesn't increase the life time of the object. It enables the garbage collector to reclaim the memory occupied by the object when no strong references to that object exist. The difference between a weak and a strong reference to an object is that while the former still allows the garbage collector to reclaim the memory occupied by that object, a strong reference to an object doesn't allow the garbage collector to reclaim the memory occupied by that object if the object is reachable.

The following code snippet shows how you can create a weak reference to an object.

<code>Rectangle rectangle = new Rectangle(15, 10);</code>

<code>var weakReference = new WeakReference(rectangle);</code>

<aside id="" class="nativo-promo nativo-promo-1 tablet desktop"></aside>You can use the IsAlive property to check if the weak reference to the object is still alive. Here's a code listing that illustrates this.

In essence, you should use short weak references when you would like to use an object that is in a usable state. On the contrary, a long weak reference is a good choice when you would like to use the object irrespective of its state.

var weakReference = new WeakReference(rectangle, true);
<h3>What is the difference between an EXE and a DLL?</h3>
EXE:
– Executable file, can run independently
– It runs in a separate process
– It can’t be reused in application
– it has a main function
DLL:
– Dynamic link library is used as part of EXE or other DLL’s
– It runs in application process memory,
– It can be reused in application
– It does not have a main function
<h3>How do you mark a method as Obsolete/Deprecated?</h3>
You can use Obsolete attribute to mark a method as Obsolete or Deprecated.
<div id="crayon-5a0e778a4bd65854141170" class="crayon-syntax crayon-theme-vs2012-black crayon-font-courier-new crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-plain-wrap"></div>
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums " data-settings="show">
<div class="crayon-nums-content">
<div class="crayon-num" data-line="crayon-5a0e778a4bd65854141170-1">1</div>
<div class="crayon-num crayon-striped-num" data-line="crayon-5a0e778a4bd65854141170-2">2</div>
<div class="crayon-num" data-line="crayon-5a0e778a4bd65854141170-3">3</div>
<div class="crayon-num crayon-striped-num" data-line="crayon-5a0e778a4bd65854141170-4">4</div>
<div class="crayon-num" data-line="crayon-5a0e778a4bd65854141170-5">5</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-5a0e778a4bd65854141170-1" class="crayon-line"><span class="crayon-sy">[</span><span class="crayon-v">Obsolete</span><span class="crayon-sy">]</span></div>
<div id="crayon-5a0e778a4bd65854141170-2" class="crayon-line crayon-striped-line"><span class="crayon-c">//You can add an explanation:</span></div>
<div id="crayon-5a0e778a4bd65854141170-3" class="crayon-line"><span class="crayon-sy">[</span><span class="crayon-e">Obsolete</span><span class="crayon-sy">(</span><span class="crayon-s">"Method1 is deprecated, please use Method2 instead."</span><span class="crayon-sy">)</span><span class="crayon-sy">]</span></div>
<div id="crayon-5a0e778a4bd65854141170-4" class="crayon-line crayon-striped-line"><span class="crayon-c">//You can also cause the compilation to fail if the method is called from somewhere in code like this:</span></div>
<div id="crayon-5a0e778a4bd65854141170-5" class="crayon-line"><span class="crayon-sy">[</span><span class="crayon-e">Obsolete</span><span class="crayon-sy">(</span><span class="crayon-s">"Method1 is deprecated, please use Method2 instead."</span><span class="crayon-sy">,</span> <span class="crayon-t">true</span><span class="crayon-sy">)</span><span class="crayon-sy">]</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
<h3> return multiple values from a function in C#</h3>
&nbsp;
<p id="LJRUWeI"><img class="alignnone  wp-image-1037 " src="/wp-content/uploads/2018/03/img_5aacc3a9de80c.png" alt="" width="335" height="138" /></p>
&nbsp;
<h3>differences between Rectangular and Jagged Array in C#</h3>
It is more efficient to use jagged arrays of one-dimensional arrays—which can be optimized—than rectangular arrays.On the other hand, the programming complexity can be significantly less for a rectangular array because it can be treated as a single unit, rather than an array of arrays.

&nbsp;
<p id="kJWApUL"><img class="alignnone  wp-image-1038 " src="/wp-content/uploads/2018/03/img_5aacc3e2055ec.png" alt="" width="462" height="195" /></p>
&nbsp;
<p id="QMzGuwr"><img class="wp-image-1040  aligncenter" src="/wp-content/uploads/2018/03/img_5aacc6792cdc1.png" alt="" width="367" height="284" /></p>
&nbsp;

&nbsp;

<hr />

<span style="font-family: 'Segoe UI'; font-size: small;"><b>Constructors can be divided into 5 types:
</b></span><span style="font-family: 'Segoe UI'; font-size: small;">Once we provide a constructor that is either private or public or any, the compiler will not add the </span><span style="font-size: small;">parameter-less</span><span style="font-family: 'Segoe UI'; font-size: small;"> public constructor to the class.</span>
<ol>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Default Constructor - A constructor without any parameters,  every instance of the class will be initialized to the same values</span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;"><span style="font-size: small;">Parametrized</span> Constructor - A constructor with at least one parameter</span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Copy Constructor - The constructor which creates an object by copying variables from another object is called a copy constructor. </span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Static Constructor - When a constructor is created as static, it will be invoked only once for all of instances of the class and it is <strong>invoked during the creation of the first instance of the class or the first reference to a static member</strong> in the class. A static constructor is used to initialize static fields of the class and to write the code that needs to be <strong>executed only once.</strong></span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;"><span style="font-family: 'Segoe UI'; font-size: small;">Private Constructor -singleton pattern - </span></span>
<pre><span style="font-family: 'Segoe UI'; font-size: small;">When a constructor is created with a private specifier, it is not possible for other classes to derive from this class,  </span>neither is it possible to create an instance of this class.</pre>
</li>
</ol>
Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated. CSRF attacks specifically target state-changing requests, not theft of data, since the attacker has no way to see the response to the forged request. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker's choosing. If the victim is a normal user, a successful CSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, CSRF can compromise the entire web application.
<ol>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Default Constructor - A constructor without any parameters,  every instance of the class will be initialized to the same values</span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;"><span style="font-size: small;">Parametrized</span> Constructor - A constructor with at least one parameter</span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Copy Constructor - The constructor which creates an object by copying variables from another object is called a copy constructor. </span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;">Static Constructor - When a constructor is created as static, it will be invoked only once for all of instances of the class and it is <strong>invoked during the creation of the first instance of the class or the first reference to a static member</strong> in the class. A static constructor is used to initialize static fields of the class and to write the code that needs to be <strong>executed only once.</strong></span></li>
 	<li><span style="font-family: 'Segoe UI'; font-size: small;"><span style="font-family: 'Segoe UI'; font-size: small;">Private Constructor -singleton pattern - </span></span>
<pre><span style="font-family: 'Segoe UI'; font-size: small;">When a constructor is created with a private specifier, it is not possible for other classes to derive from this class,  </span>neither is it possible to create an instance of this class.</pre>
</li>
</ol>
&nbsp;

References
<ul>
 	<li><a href="http://www.csharpstar.com/csharp-interview-questions-part-1/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 1)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-2/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 2)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-3/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 3)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-4/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 4)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-5/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 5)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-6/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 6)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-7/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 7)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-8/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 8)</a>
<a href="http://www.csharpstar.com/csharp-interview-questions-part-9/" target="_blank" rel="noopener">C# Interview Questions for Experienced professionals (Part – 9)</a></li>
</ul>
