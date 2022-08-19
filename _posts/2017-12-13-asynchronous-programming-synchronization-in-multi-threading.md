---
layout: post
title: Asynchronous programming and Synchronization in Multi-Threading
date: 2017-12-13 09:59
author: tmasabari
comments: true
categories: [C#, Interview Preparation, Parallel Programming, Prepare, QuickRefresh, Task, Threading, Uncategorized]
---
<!-- wp:embed {"url":"https://docs.microsoft.com/en-us/dotnet/csharp/async"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://docs.microsoft.com/en-us/dotnet/csharp/async
</div></figure>
<!-- /wp:embed -->

<!-- wp:embed {"url":"https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap
</div></figure>
<!-- /wp:embed -->

<!-- wp:core-embed/wordpress {"url":"http://www.csharpstar.com/csharp-interview-questions-part-5/","type":"wp-embed","providerNameSlug":"csharp-star","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed-wordpress wp-block-embed is-type-wp-embed is-provider-csharp-star wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
http://www.csharpstar.com/csharp-interview-questions-part-5/
</div></figure>
<!-- /wp:core-embed/wordpress -->

<!-- wp:heading {"level":3} -->
<h3>What is the difference between a process and a thread?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Process:<br>– An executing instance of a program is called a process.<br>– Some operating systems use the term ‘task‘ to refer to a program that is being executed.<br>– A process is always stored in the main memory also termed as the primary memory or random access memory.<br>– Therefore, a process is termed as an active entity. It disappears if the machine is rebooted.<br>– Several process may be associated with a same program.<br>– On a multiprocessor system, multiple processes can be executed in parallel.<br>– On a uni-processor system, though true parallelism is not achieved, a process scheduling algorithm is applied and the processor is scheduled to execute each process one at a time yielding an illusion of concurrency.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Thread:<br>– A thread is a subset of the process.<br>– It is termed as a ‘lightweight process’, since it is similar to a real process but executes within the context of a process and shares the same resources allotted to the process by the kernel.<br>– Usually, a process has only one thread of control – one set of machine instructions executing at a time.<br>– A process may also be made up of multiple threads of execution that execute instructions concurrently.<br>– Multiple threads of control can exploit the true parallelism possible on multiprocessor systems.<br>– On a uni-processor system, a thread scheduling algorithm is applied and the processor is scheduled to run each thread one at a time.<br>– All the threads running within a process share the same address space, file descriptors, stack and other process related attributes.<br>– Since the threads of a process share the same memory, synchronizing the access to the shared data withing the process gains unprecedented importance.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>– Source: Knowledge Quest</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In Synchronus mode, every task executes in sequence, so it’s easier to program. That’s the way we’ve been doing it for years.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>With asynchronous execution, you have few challenges:<br>– You must synchronize tasks. for e.g. you run a task that must be executed after the other three have finished. You will have to create a mechanism to wait for all tasks to finish before launching the new task.<br>– You must address concurrency issues. If you have a shared resource, like a list that is written in one task and read in another, make sure that it’s kept in a known state.<br>– There is no logical sequence anymore. The tasks can end at any time, and you don’t have control of which one finishes first.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>But in synchronous programming we have below disadvantages:<br>– It takes longer to finish.<br>– It may stop the user interface (UI) thread. Typically, these programs have only one UI thread, and when you use it as a blocking operation, you get the spinning wheel (and “not responding” in the caption title) in your program—not the best experience for your users.<br>It doesn’t use the multicore architecture of the new processors. Regardless of whether your program is running on a 1-core or a 64-core processor, – it will run as quickly (or slowly) on both.<br>Asynchronous programming eliminates these disadvantages: it won’t hang the UI thread (because it can run as a background task), and it can use all the cores in your machine and make better use of machine resources. So, do you choose easier programming or better use of resources? Fortunately, you don’t have to make this decision. Microsoft has created several ways to minimize the difficulties of programming for asynchronous execution.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Static methods and Multi-threading</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Any public static (Shared in Visual Basic) members of this type are thread safe.</li><li>When MS designs a static method,   they don't access any variable/member/ state which is outside the scope of that method. They rely completely on method scoped local variables only for implementing that method's logic. </li><li>Any instance members are not guaranteed to be thread safe.</li><li>Static data on the other hand could cause a problem because attempts to access the same data from different threads needs to be controlled to ensure that only one thread at a time is reading or writing the data.</li><li>If each thread has it's own separate instance of the class with it's own set of data, there is no risk of data being mixed up. If the data is static, there is only one set of data, and all threads share the same data, so there is no way to not mix it up.</li><li></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Variables declared inside methods (with the possible exception of "<em>captured</em>" variables) are isolated, so you won't get any inherent problems; however, if your static method accesses any shared state, all bets are off.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Examples of shared-state would be:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>static fields</li><li>objects accessed from a common cache (non-serialized)</li><li>data obtained via the input parameters (and state on those objects), if it is possible that multiple threads are touching the same object(s)</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>If you have shared state, you must either:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>take care not to mutate the state once it can be shared (better: use immutable objects to represent state, and take a snapshot of the state into a local variable - i.e. rather than reference&nbsp;<code>whatever.SomeData</code>&nbsp;repeatedly, you read&nbsp;<code>whatever.SomeData</code>&nbsp;<strong>once</strong>&nbsp;into a local variable, and then just use the variable - note that this only helps for immutable state!)</li><li>synchronize access to the data (all threads must synchronize) - either mutually exclusive or (more granular) reader/writer</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Should a return statement be inside or outside a lock statement?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>It is recommended to put the return inside the lock. Otherwise you risk another thread entering the lock and modifying your variable before the return statement, therefore making the original caller receive a different value than expected.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>What is the use of volatile keyword?</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>The volatile keyword indicates that a field might be modified by multiple threads that are executing at the same time. Fields that are declared volatile are not subject to compiler optimizations that assume access by a single thread. This ensures that the most up-to-date value is present in the field at all times.<br>The volatile modifier is usually used for a field that is accessed by multiple threads without using the lock statement to serialize access.<br>The volatile keyword can be applied to fields of these types:<br>– Reference types.<br>– Pointer types (in an unsafe context). Note that although the pointer itself can be volatile, the object that it points to cannot. In other words, you cannot declare a “pointer to volatile.”<br>– Integral types such as sbyte, byte, short, ushort, int, uint, char, float, and bool.<br>– An enum type with an integral base type.<br>– Generic type parameters known to be reference types.<br>– IntPtr and UIntPtr.</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:heading -->
<h2>Task-based Asynchronous Pattern (TAP)</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Reasons for a quick return include the following:</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Asynchronous methods may be invoked from user interface (UI) threads, and any long-running synchronous work could harm the responsiveness of the application.</li><li>Multiple asynchronous methods may be launched concurrently. Therefore, any long-running work in the synchronous portion of an asynchronous method could delay the initiation of other asynchronous operations, thereby decreasing the benefits of concurrency.</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Will your code be "waiting" for something, such as data from a database Extracting Data from a Network? If your answer is "yes", then your work is <strong>I/O-bound</strong>.</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Will your code be performing a very expensive computation? If you answered "yes", then your work is <strong>CPU-bound</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>For I/O-bound code, you await an operation which returns a Task or Task&lt;T&gt; inside of an async method.</li><li>For CPU-bound code, you await an operation which is started on a background thread with the Task.Run method.</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>I/O-Bound Example: Downloading data from a web service</h3>
<!-- /wp:heading -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>private readonly HttpClient _httpClient = new HttpClient(); </p><p>downloadButton.Clicked += async (o, e) =&gt; { // This line will yield control to the UI as the request</p><p>// from the web service is happening.</p><p>// // The UI thread is now free to perform other work.</p><p>var stringData = await _httpClient.GetStringAsync(URL); DoSomethingWithData(stringData);</p><p>};</p></blockquote>
<!-- /wp:quote -->

<!-- wp:heading {"level":3} -->
<h3>CPU-bound Example: Performing a Calculation for a Game</h3>
<!-- /wp:heading -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>private DamageResult CalculateDamageDone() { </p><p>// Code omitted: // // Does an expensive calculation and returns // the result of that calculation.</p><p>}</p><p>calculateButton.Clicked += async (o, e) =&gt; {</p><p> // This line will yield control to the UI while CalculateDamageDone()</p><p>// performs its work. The UI thread is free to perform other work.</p><p>var damageResult = await Task.Run(() =&gt; CalculateDamageDone()); DisplayDamage(damageResult);</p><p>};</p></blockquote>
<!-- /wp:quote -->

<!-- wp:list -->
<ul><li>async <strong>methods need to have an</strong> await <strong>keyword in their body or they will never yield!</strong></li><li><strong>You should add "Async" as the suffix of every async method name you write.</strong></li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li>async void <strong>should only be used for event handlers.</strong></li><li>Exceptions thrown in an async void method can’t be caught outside of that method.</li><li>async void methods are very difficult to test.</li><li>async void methods can cause bad side effects if the caller isn’t expecting them to be async.</li></ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul><li><strong>Tread carefully when using async lambdas in LINQ expressions</strong></li><li><strong>Write code that awaits Tasks in a non-blocking manner The Task API contains two Methods,&nbsp; Task.WhenAll and Task.WhenAnywhich allow you to write asynchronous code which performs a non-blocking wait on multiple background jobs.</strong></li></ul>
<!-- /wp:list -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td>Use this...</td><td>Instead of this...</td><td>When wishing to do this</td></tr><tr><td>await</td><td>Task.Wait or Task.Result</td><td>Retrieving the result of a background task</td></tr><tr><td>await Task.WhenAny</td><td>Task.WaitAny</td><td>Waiting for any task to complete</td></tr><tr><td>await Task.WhenAll</td><td>Task.WaitAll</td><td>Waiting for all tasks to complete</td></tr><tr><td>await Task.Delay</td><td>Thread.Sleep</td><td>Waiting for a period of time</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:list -->
<ul><li><strong>Write less stateful code</strong></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Don’t depend on the state of global objects or the execution of certain methods. Instead, depend only on the return values of methods. Why?</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Code will be easier to reason about.</li><li>Code will be easier to test.</li><li>Mixing async and synchronous code is far simpler.</li><li>Race conditions can typically be avoided altogether.</li><li>Depending on return values makes coordinating async code simple.</li><li>(Bonus) it works really well with dependency injection.</li></ul>
<!-- /wp:list -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:embed {"url":"http://www.albahari.com/threading/part2.aspx"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.albahari.com/threading/part2.aspx
</div></figure>
<!-- /wp:embed -->

<!-- wp:heading -->
<h2><strong>Immutable Objects</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>An immutable object is one whose state cannot be altered — externally or internally. The fields in an immutable object are typically declared read-only and are fully initialized during construction.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Immutability is a hallmark of functional programming — where instead of <em>mutating</em> an object, you create a new object with different properties. LINQ follows this paradigm. Immutability is also valuable in multithreading in that it avoids the problem of shared writable state — by eliminating (or minimizing) the writable.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>One pattern is to use immutable objects to encapsulate a group of related fields, to minimize lock durations.</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>class ProgressStatus&nbsp;&nbsp;&nbsp; <em>// Represents progress of some activity</em>{</p><p>public readonly int PercentComplete;</p><p>public readonly string StatusMessage;</p><p>&nbsp;</p><p><em>// This class might have many more fields...</em></p><p>&nbsp;</p><p>public ProgressStatus (int percentComplete, string statusMessage)</p><p>{</p><p>PercentComplete = percentComplete;</p><p>StatusMessage = statusMessage;</p><p>}}</p></blockquote>
<!-- /wp:quote -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:embed {"url":"http://www.albahari.com/threading/part4.aspx"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
http://www.albahari.com/threading/part4.aspx
</div></figure>
<!-- /wp:embed -->

<!-- wp:heading {"level":1} -->
<h1><strong>Nonblocking Synchronization</strong></h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Writing nonblocking or lock-free multithreaded code properly is tricky! Memory barriers, in particular, are easy to get wrong (the <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_The_volatile_keyword"><strong>volatile keyword</strong></a> is even easier to get wrong). Think carefully whether you really need the performance benefits before dismissing ordinary locks.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>Memory Barriers and Volatility</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Consider the following example:</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>class Foo{</p><p>int _answer;</p><p>bool _complete;</p><p>&nbsp;</p><p>void A()</p><p>{</p><p>_answer = 123;</p><p>_complete = true;</p><p>}</p><p>&nbsp;</p><p>void B()</p><p>{</p><p>if (_complete) Console.WriteLine (_answer);</p><p>}}</p>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>If methods <strong>A</strong> and <strong>B</strong> ran concurrently on different threads, might it be possible for <strong>B</strong> to write “0”? The answer is yes — for the following reasons:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>The compiler, CLR, or CPU may reorderyour program's instructions to improve efficiency.</li><li>The compiler, CLR, or CPU may introduce caching optimizations such that assignments to variables won't be visible to other threads right away.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>C# and the runtime are very careful to ensure that such optimizations don’t break ordinary single-threaded code — or multithreaded code that makes proper use of locks. Outside of these scenarios, you must explicitly defeat these optimizations by creating <em>memory barriers</em> (also called <em>memory fences</em>) to limit the effects of instruction reordering and read/write caching.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static void Main(){</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>bool complete = false;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>var t = new Thread (() =&gt;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>bool toggle = false;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>while (!complete) toggle = !toggle;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>});</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>t.Start();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Thread.Sleep (1000);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>complete = true;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>t.Join();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Blocks indefinitely</em>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This program never terminates because the <strong>complete</strong> variable is cached in a CPU register. Inserting a call to <strong>Thread.MemoryBarrier</strong> inside the <strong>while</strong> loop (or <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_Locking">locking</a> around reading <strong>complete</strong>) fixes the error.</p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:paragraph -->
<p>The volatile keyword</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Another (more advanced) way to solve this problem is to apply the <strong>volatile</strong> keyword to the <strong>_complete</strong> field:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>volatile bool _complete;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The <strong>volatile</strong> keyword instructs the compiler to generate an <em>acquire-fence</em> on every read from that field, and a <em>release-fence</em> on every write to that field. An acquire-fence prevents other reads/writes from being moved before the fence; a release-fence prevents other reads/writes from being moved after the fence. These “half-fences” are faster than full fences because they give the runtime and hardware more scope for optimization.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>As it happens, Intel’s X86 and X64 processors always apply acquire-fences to reads and release-fences to writes — whether or not you use the <strong>volatile</strong> keyword — so this keyword has no effect on the hardware if you’re using these processors. However, <strong>volatile</strong> does have an effect on optimizations performed by the compiler and the CLR — as well as on 64-bit AMD and (to a greater extent) Itanium processors. This means that you cannot be more relaxed by virtue of your clients running a particular type of CPU.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>he effect of applying <strong>volatile</strong> to fields can be summarized as follows:</p>
<!-- /wp:paragraph -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong>First instruction</strong></td><td><strong>Second instruction</strong></td><td><strong>Can they be swapped?</strong></td></tr><tr><td>Read</td><td>Read</td><td>No</td></tr><tr><td>Read</td><td>Write</td><td>No</td></tr><tr><td>Write</td><td>Write</td><td>No (The CLR ensures that write-write operations are never swapped, even without the <strong>volatile</strong> keyword)</td></tr><tr><td>Write</td><td>Read</td><td><strong>Yes!</strong></td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:paragraph -->
<p>Notice that applying <strong>volatile</strong> doesn’t prevent a write followed by a read from being swapped, and this can create brainteasers.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This presents a strong case for avoiding <strong>volatile</strong></p>
<!-- /wp:paragraph -->

<!-- wp:separator -->
<hr class="wp-block-separator"/>
<!-- /wp:separator -->

<!-- wp:paragraph -->
<p>Interlocked</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Use of <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_Memory_Barriers_and_Volatility">memory barriers</a> is not always enough when reading or writing fields in lock-free code. Operations on 64-bit fields, increments, and decrements require the heavier approach of using the <strong>Interlocked</strong> helper class. <strong>Interlocked</strong> also provides the <strong>Exchange</strong> and <strong>CompareExchange</strong> methods, the latter enabling lock-free read-modify-write operations, with a little additional coding.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A statement is intrinsically <em>atomic</em> if it executes as a single indivisible instruction on the underlying processor. Strict atomicity precludes any possibility of preemption. A simple read or write on a field of 32 bits or less is always atomic. Operations on 64-bit fields are guaranteed to be atomic only in a 64-bit runtime environment, and statements that combine more than one read/write operation are never atomic</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>class Atomicity{</p><p>static int _x, _y;</p><p>static long _z;</p><p>&nbsp;</p><p>static void Test()</p><p>{</p><p>long myLocal;</p><p>_x = 3;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Atomic</em></p><p>_z = 3;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Nonatomic on 32-bit environs (_z is 64 bits)</em></p><p>myLocal = _z;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Nonatomic on 32-bit environs (_z is 64 bits)</em></p><p>_y += _x;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Nonatomic (read AND write operation)</em></p><p>_x++;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Nonatomic (read AND write operation)</em></p><p>}}</p><p>class Program{</p><p>static long _sum;</p><p>&nbsp;</p><p>static void Main()</p><p>{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// _sum</em></p><p><em>// Simple increment/decrement operations:</em></p><p>Interlocked.Increment (ref _sum);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 1</em></p><p>Interlocked.Decrement (ref _sum);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 0</em></p><p>&nbsp;</p><p><em>// Add/subtract a value:</em></p><p>Interlocked.Add (ref _sum, 3);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 3</em></p><p>&nbsp;</p><p><em>// Read a 64-bit field:</em></p><p>Console.WriteLine (Interlocked.Read (ref _sum));&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 3</em></p><p>&nbsp;</p><p><em>// Write a 64-bit field while reading previous value:</em></p><p><em>// (This prints "3" while updating _sum to 10)</em></p><p>Console.WriteLine (Interlocked.Exchange (ref _sum, 10));&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 10</em></p><p>&nbsp;</p><p><em>// Update a field only if it matches a certain value (10):</em></p><p>Console.WriteLine (Interlocked.CompareExchange (ref _sum,</p><p>123, 10);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// 123</em></p><p>}</p>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p><strong>Interlocked</strong>’s mathematical operations are restricted to <strong>Increment</strong>, <strong>Decrement</strong>, and <strong>Add</strong>. If you want to multiply — or perform any other calculation — you can do so in lock-free style by using the <strong>CompareExchange</strong>method (typically in conjunction with spin-waiting). We give an example in <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_SpinLock_and_SpinWait">the parallel programming section</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Interlocked</strong> works by making its need for atomicity known to the operating system and virtual machine.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Interlocked</strong>’s methods have a typical overhead of 10 ns — half that of an uncontended <strong>lock</strong>. Further, they can never suffer the additional cost of context switching due to <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_Blocking">blocking</a>. The flip side is that using <strong>Interlocked</strong> within a loop with many iterations can be less efficient than obtaining a single lock around the loop (although <strong>Interlocked</strong> enables greater concurrency).</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>When to Lock</strong></h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>In .NET Framework, nearly all of its nonprimitive types are not thread-safe (for anything more than read-only access) when instantiated, and yet they can be used in multithreaded code if all access to any given object is protected via a <a href="file:///C:/Users/tmasabari/AppData/Local/Temp/OpenLiveWriter758310246/6DE7A4ABA32D/index.htm#_Locking">lock</a>.</li><li>Wrapping access to an object around a custom lock <strong>works only if all concurrent threads are aware of — and use — the lock</strong>. This may not be the case if the object is widely scoped. <strong>The worst case is with static members in a public type.</strong></li><li>Thread safety in static methods is something that you must explicitly code: it doesn’t happen automatically by virtue of the method being static!</li><li>Making types thread-safe for <strong>concurrent read-only access (where possible) is advantageous</strong> because it means that consumers can avoid excessive locking. Many of the .NET Framework types follow this principle: collections, for instance, are thread-safe for concurrent readers.</li></ul>
<!-- /wp:list -->

<!-- wp:image {"id":466} -->
<figure class="wp-block-image"><img src="/wp-content/uploads/2017/12/img_5a2f547f234b5.png" alt="" class="wp-image-466"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>Exclusive locking is used to ensure that only one thread can enter particular sections of code at a time. The two main exclusive locking constructs are <strong>lock</strong> and <strong>Mutex</strong>. Of the two, the <strong>lock</strong> construct is faster and more convenient. <strong>Mutex</strong>, though, has a niche in that its lock can span applications in different processes on the computer.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>A Comparison of Locking Constructs</strong></p>
<!-- /wp:paragraph -->

<!-- wp:table -->
<table class="wp-block-table"><tbody><tr><td><strong>Construct</strong></td><td><strong>Purpose</strong></td><td><strong>Cross-process?</strong></td><td><strong>Overhead*</strong></td></tr><tr><td><a href="#_Locking">lock</a> (<strong>Monitor.Enter</strong> / <strong>Monitor.Exit</strong>)</td><td>Ensures just one thread can access a resource, or section of code at a time</td><td>-</td><td>20ns</td></tr><tr><td><a href="#_Mutex">Mutex</a></td><td>Yes</td><td>1000ns</td></tr><tr><td><a href="#_Semaphore">SemaphoreSlim</a> (introduced in Framework 4.0)</td><td>Ensures not more than a specified number of concurrent threads can access a resource, or section of code</td><td>-</td><td>200ns</td></tr><tr><td><a href="#_Semaphore">Semaphore</a></td><td>Yes</td><td>1000ns</td></tr><tr><td><a href="#_Reader_Writer_Locks">ReaderWriterLockSlim</a>(introduced in Framework 3.5)</td><td>Allows multiple readers to coexist with a single writer</td><td>-</td><td>40ns</td></tr><tr><td><a href="#_Reader_Writer_Locks">ReaderWriterLock</a>(effectively deprecated)</td><td>-</td><td>100ns</td></tr></tbody></table>
<!-- /wp:table -->

<!-- wp:paragraph -->
<p>*Time taken to lock and unlock the construct once on the same thread (assuming no blocking), as measured on an I<strong>ntel Core i7 860.</strong></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Locking</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As a basic rule, you need to lock around accessing any writable shared field. Even in the simplest case — an assignment operation on a single field — you must consider synchronization.</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>class ThreadSafe{</p><p>&nbsp;</p><p>static readonly object _locker = new object();</p><p>&nbsp;</p><p>static int _x;</p><p>&nbsp;</p><p>&nbsp;</p><p>static void Increment() { lock (_locker) _x++; }</p><p>&nbsp;</p><p>static void Assign()&nbsp;&nbsp;&nbsp; { lock (_locker) _x = 123; }}</p><p>&nbsp;</p><p>In <a href="#_Nonblocking_Synchronization">Nonblocking Synchronization</a>, we explain how this need arises, and how the memory barriers and the <a href="#_Interlocked"><strong>Interlocked</strong></a> class can provide alternatives to locking in these situations.</p><p>&nbsp;</p><p>&nbsp;</p><p>A thread can repeatedly lock the same object in a nested (<em>reentrant</em>) fashion:</p><p>&nbsp;</p><p>lock (locker)</p><p>&nbsp;</p><p>lock (locker)</p><p>&nbsp;</p><p>lock (locker)</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p><em>// Do something...</em></p><p>&nbsp;</p><p>}</p>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>In these scenarios, the object is unlocked only when the outermost <strong>lock</strong> statement has exited — or a matching number of <strong>Monitor.Exit</strong> statements have executed.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Nested locking is useful when one method calls another within a lock</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>Deadlocks</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A deadlock happens when two threads each wait for a resource held by the other, so neither can proceed. The easiest way to illustrate this is with two locks:</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>object locker1 = new object();object locker2 = new object();</p><p>&nbsp;</p><p>new Thread (() =&gt; {</p><p>&nbsp;</p><p>lock (locker1)</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p>Thread.Sleep (1000);</p><p>&nbsp;</p><p>lock (locker2);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Deadlock</em></p><p>&nbsp;</p><p>}</p><p>&nbsp;</p><p>}).Start();lock (locker2){</p><p>&nbsp;</p><p>Thread.Sleep (1000);</p><p>&nbsp;</p><p>lock (locker1);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </p><p><em>// Deadlock</em></p><p>}</p>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>The popular advice, “lock objects in a consistent order to avoid deadlocks,” although helpful in our initial example, is hard to apply to the scenario just described. A better strategy is to be wary of locking around calling methods in objects that may have references back to your own object. Also, consider whether you really need to lock around calling methods in other classes (often you do — <a href="#_Locking">as we’ll see later</a> — but sometimes there are other options). Relying more on <a href="#_PLINQ">declarative</a> and <a href="#_The_Parallel_Class">data parallelism</a>, <a href="#_Immutable_Objects">immutable types</a>, and <a href="#_Nonblocking_Synchronization">nonblocking synchronization constructs</a>, can lessen the need for locking.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Here is an alternative way to perceive the problem: when you call out to other code while holding a lock, the encapsulation of that lock subtly leaks. This is not a fault in the CLR or .NET Framework, but a fundamental limitation of locking in general. The problems of locking are being addressed in various research projects, including <em>Software Transactional Memory</em>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>Mutex</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A <strong>Mutex</strong> is like a C# <strong>lock</strong>, but it can work across multiple processes. In other words, <strong>Mutex</strong> can be computer-wide as well as application-wide.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Acquiring and releasing an uncontended <strong>Mutex</strong> takes a few microseconds — about 50 times slower than a <strong>lock</strong>.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>With a <strong>Mutex</strong> class, you call the <strong>WaitOne</strong> method to lock and <strong>ReleaseMutex</strong> to unlock. Closing or disposing a <strong>Mutex</strong> automatically releases it. Just as with the <strong>lock</strong> statement, a <strong>Mutex</strong> can be released only from the same thread that obtained it.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A common use for a cross-process <strong>Mutex</strong> is to ensure that only one instance of a program can run at a time. Here’s how it’s done:</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>class OneAtATimePlease{</p><p>&nbsp;</p><p>static void Main()</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p><em>// Naming a Mutex makes it available computer-wide. Use a name that's</em></p><p>&nbsp;</p><p><em>// unique to your company and application (e.g., include your URL).</em></p><p>&nbsp;</p><p>&nbsp;</p><p>using (var mutex = new Mutex (false, "oreilly.com OneAtATimeDemo"))</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p><em>// Wait a few seconds if contended, in case another instance</em></p><p>&nbsp;</p><p><em>// of the program is still in the process of shutting down.</em></p><p>&nbsp;</p><p>&nbsp;</p><p>if (!mutex.WaitOne (TimeSpan.FromSeconds (3), false))</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p>Console.WriteLine ("Another app instance is running. Bye!");</p><p>&nbsp;</p><p>return;</p><p>&nbsp;</p><p>}</p><p>&nbsp;</p><p>RunProgram();</p><p>&nbsp;</p><p>}</p><p>&nbsp;</p><p>}</p><p>&nbsp;</p><p>&nbsp;</p><p>static void RunProgram()</p><p>&nbsp;</p><p>{</p><p>&nbsp;</p><p>Console.WriteLine ("Running. Press Enter to exit");</p><p>&nbsp;</p><p>Console.ReadLine();</p><p>&nbsp;</p><p>}}</p>
<!-- /wp:html -->

<!-- wp:paragraph -->
<p>If running under Terminal Services, a computer-wide <strong>Mutex</strong> is ordinarily visible only to applications in the same terminal server session. To make it visible to all terminal server sessions, prefix its name with Global\.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>Semaphore</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>A semaphore with a capacity of one is similar to a <strong>Mutex</strong> or <strong>lock</strong>, except that the semaphore has no “owner” — it’s <em>thread-agnostic</em>. Any thread can call <strong>Release</strong> on a <strong>Semaphore</strong>, whereas with <strong>Mutex</strong> and <strong>lock</strong>, only the thread that obtained the lock can release it.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>There are two functionally similar versions of this class: <strong>Semaphore</strong> and <strong>SemaphoreSlim</strong>. The latter was introduced in Framework 4.0 and has been optimized to meet the low-latency demands of <a href="#_Parallel_Programming">parallel programming</a>. It’s also useful in traditional multithreading because it lets you specify a <a href="#_Cancellation_Tokens">cancellation token</a> when waiting. It cannot, however, be used for interprocess signaling.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>While performing intensive disk I/O, the <strong>Semaphore</strong> would improve overall performance by limiting excessive concurrent hard-drive activity.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Semaphores can be useful in limiting concurrency — preventing too many threads from executing a particular piece of code at once. In the following example, five threads try to enter a nightclub that allows only three threads in at once:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>class TheClub&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// No door lists!</em>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static SemaphoreSlim _sem = new SemaphoreSlim (3);&nbsp;&nbsp;&nbsp; <em>// Capacity of 3</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static void Main()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>for (int i = 1; i &lt;= 5; i++) new Thread (Enter).Start (i);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static void Enter (object id)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Console.WriteLine (id + " wants to enter");</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_sem.Wait();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Console.WriteLine (id + " is in!");&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Only three threads</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Thread.Sleep (1000 * (int) id);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// can be here at</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Console.WriteLine (id + " is leaving");&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// a time.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_sem.Release();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 wants to enter</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 is in!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2 wants to enter</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2 is in!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>3 wants to enter</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>3 is in!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>4 wants to enter</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>5 wants to enter</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1 is leaving</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>4 is in!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2 is leaving</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>5 is in!</p>
<!-- /wp:paragraph -->

<!-- wp:core-embed/wordpress {"url":"https://blogs.msdn.microsoft.com/ericlippert/2009/03/06/locks-and-exceptions-do-not-mix/","type":"wp-embed","providerNameSlug":"fabulous-adventures-in-coding","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed-wordpress wp-block-embed is-type-wp-embed is-provider-fabulous-adventures-in-coding wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
https://blogs.msdn.microsoft.com/ericlippert/2009/03/06/locks-and-exceptions-do-not-mix/
</div></figure>
<!-- /wp:core-embed/wordpress -->

<!-- wp:embed {"url":"https://stackoverflow.com/questions/4978850/monitor-vs-lock"} -->
<figure class="wp-block-embed"><div class="wp-block-embed__wrapper">
https://stackoverflow.com/questions/4978850/monitor-vs-lock
</div></figure>
<!-- /wp:embed -->

<!-- wp:paragraph -->
<p>Basically, we all have a difficult choice to make whenever doing multi-threaded programming. We can (1) automatically release locks upon exceptions, exposing inconsistent state and living with the resulting bugs (bad) (2) maintain locks upon exceptions, deadlocking the program (arguably often worse) or (3) carefully implement the bodies of locks that do mutations so that in the event of an exception, the mutated resource is rolled back to a pristine state before the lock is released. (Good, but hard.)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This is yet another reason why <strong>the body of a lock should do as little as possible</strong>. Usually the rationale for having small lock bodies is to get in and get out quickly, so that anyone waiting on the lock does not have to wait long. But an even better reason is because small, simple lock bodies minimize the chance that the thing in there is going to throw an exception. It's also easier to rewrite mutating lock bodies to have rollback behaviour if they don't do very much to begin with.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>And of course, this is yet another reason why aborting a thread is pure evil. Try to never do so!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Recall that lock(obj){body} was a syntactic sugar for</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Monitor.Enter(object);try{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>// Your code here...}finally{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Monitor.Exit(object);}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>However, keep in mind that Monitor can also聽<strong>Wait()</strong>聽and聽<strong>Pulse()</strong>, which are often useful in complex multithreading situations.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The problem here is that if the compiler generates a no-op instruction between the monitor enter and the try-protected region then it is possible for the runtime to throw a thread abort exception after the monitor enter but before the try. In that scenario, the finally never runs so the lock leaks, probably eventually deadlocking the program. It would be nice if this were impossible in unoptimized and optimized builds.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>However in C# 4 its implemented differently:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>bool lockWasTaken = false;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>var temp = obj;</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>try {</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Monitor.Enter(temp, ref lockWasTaken);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>//your code</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>finally</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>if (lockWasTaken)</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Monitor.Exit(temp);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>implicit in this codegen is the belief that a deadlocked program is the worst thing that can happen</strong>. That's not necessarily true! <strong>Sometimes deadlocking the program is the better thing to do -- the lesser of two evils. </strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The purpose of the lock statement is to help you protect the integrity of a mutable resource that is shared by multiple threads. But suppose an exception is thrown halfway through a mutation of the locked resource. Our implementation of lock does not magically roll back the mutation to its pristine state, and it does not complete the mutation. Rather, control immediately branches to the finally, releasing the lock and allowing every other thread that is patiently waiting to immediately view the messed-up partially mutated state! If that state has privacy, security, or human life and safety implications, the result could be very bad indeed. In that case it is possibly better to deadlock the program and protect the messed-up resource by denying access to it entirely. But that's obviously not good either.</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":1} -->
<h1><strong>Signaling with Event Wait Handles</strong></h1>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Event wait handles are used for <em>signaling</em>. Signaling is when one thread waits until it receives notification from another.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The most important difference is that an AutoResetEvent will only allow one single waiting thread to continue. A ManualResetEvent on the other hand will keep allowing threads, several at the same time even, to continue until you tell it to stop (Reset it).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The ManualResetEvent is the door, which needs to be closed (reset) manually. The AutoResetEvent is a tollbooth, allowing one car to go by and automatically closing before the next one can get through.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Just imagine that the AutoResetEvent executes WaitOne() and Reset() as a single atomic operation.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>CountdownEvent</strong> lets you wait on more than one thread. The class is new to Framework 4.0 and has an efficient fully managed implementation.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong> Comparison of Signaling Constructs</strong><br><br>ken to signal and wait on the construct once on the same thread (assuming no blocking), as measured on an Intel Core i7 860.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>AutoResetEvent</strong> object can call <strong>Set</strong> on it to release one blocked thread.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You can create an <strong>AutoResetEvent</strong> in two ways. The first is via its constructor:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>var auto = new AutoResetEvent (false);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>(Passing <strong>true</strong> into the constructor is equivalent to immediately calling <strong>Set</strong> upon it.) The second way to create an <strong>AutoResetEvent</strong> is as follows:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>var auto = new EventWaitHandle (false, EventResetMode.AutoReset);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In the following example, a thread is started whose job is simply to wait until signaled by another thread:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>class BasicWaitHandle{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static EventWaitHandle _waitHandle = new AutoResetEvent (false);</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static void Main()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>new Thread (Waiter).Start();</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Thread.Sleep (1000);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Pause for a second...</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_waitHandle.Set();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Wake up the Waiter.</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>static void Waiter()</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>{</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Console.WriteLine ("Waiting...");</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>_waitHandle.WaitOne();&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <em>// Wait for notification</em></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Console.WriteLine ("Notified");</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>}}</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Waiting... <em>(pause)</em> Notified.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2><strong>Wait Handles and the Thread Pool</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>If your application has lots of threads that spend most of their time blocked on a wait handle, you can reduce the resource burden by calling <strong>ThreadPool.RegisterWaitForSingleObject</strong>. This method accepts a delegate that is executed when a wait handle is signaled. While it’s waiting, it doesn’t tie up a thread:</p>
<!-- /wp:paragraph -->

<!-- wp:html -->
<p>static ManualResetEvent _starter = new ManualResetEvent (false);</p><p>&nbsp;</p><p>public static void Main(){</p><p>&nbsp;</p><p>RegisteredWaitHandle reg = ThreadPool.RegisterWaitForSingleObject</p><p>&nbsp;</p><p>(_starter, Go, "Some Data", -1, true);</p><p>&nbsp;</p><p>Thread.Sleep (5000);</p><p>&nbsp;</p><p>Console.WriteLine ("Signaling worker...");</p><p>&nbsp;</p><p>_starter.Set();</p><p>&nbsp;</p><p>Console.ReadLine();</p><p>&nbsp;</p><p>reg.Unregister (_starter);&nbsp;&nbsp; </p><p>&nbsp;<em>// Clean up when we’re done.</em></p><p>}</p><p>&nbsp;</p><p>public static void Go (object data, bool timedOut){</p><p>&nbsp;</p><p>Console.WriteLine ("Started - " + data);</p><p>&nbsp;</p><p><em>// Perform task...</em>}</p>
<!-- /wp:html -->
