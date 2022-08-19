---
layout: post
title: Async- asynchronous programming and multithreading?
date: 2018-03-09 13:11
author: tmasabari
comments: true
categories: [C#, Interview Preparation, Parallel Programming, Prepare, QuickRefresh, Task, Threading]
---
<h2 id="asyncprogramming">What is Asynchronous Programming</h2>
Async programming is a concurrent programming technique, which allows the working <strong>process</strong> to run separately from the calling application. As soon as the work completes, it informs the main thread about the result, whether it was successful or not.

By using async programming, we can avoid performance bottlenecks and enhance the responsiveness of our application.

How so?

Now, when we send a request to the main thread, it delegates a waiting to a background thread, thus freeing itself for another request. Eventually, a background thread finishes its job and returns it to the main thread. Then the main thread returns the result to the requester.

It is very important to understand that if we send a request to an endpoint and it takes the application three or more seconds to process that request, we probably won’t be able to execute this request any faster in async mode. It is going to take the same amount of time as the sync request.

The only advantage is that in the async mode the main thread won’t be blocked three or more seconds, and thus it will be able to process other requests.

Here is the visual representation of the asynchronous workflow:
<p id="sylACiQ"><img class="alignnone size-full wp-image-1817 " src="/wp-content/uploads/2018/10/img_5bd7c91bb4e12.png" alt="" /></p>

<h2 id="asyncawait">Async, Await Keywords and Return Types</h2>
For example, if we want to create a method in an asynchronous manner, we need to add the <code>async</code> keyword next to the method’s return type:
<div id="crayon-5bd7c6c1d6b25743793895" class="crayon-syntax crayon-theme-visualstudiodark crayon-font-consolas crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums " data-settings="show">
<div class="crayon-nums-content">
<div class="crayon-num" data-line="crayon-5bd7c6c1d6b25743793895-1">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-5bd7c6c1d6b25743793895-1" class="crayon-line"><span class="crayon-m">async</span> <span class="crayon-v">Task</span><span class="crayon-o">&lt;</span><span class="crayon-v">IEnumerable</span><span class="crayon-o">&lt;</span><span class="crayon-v">Owner</span><span class="crayon-o">&gt;&gt;</span> <span class="crayon-e">GetAllOwnersAsync</span><span class="crayon-sy">(</span><span class="crayon-sy">)</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
By using the <code>async</code> keyword, we are enabling the <code>await</code> keyword and modifying the way of how method results are handled (from synchronous to asynchronous):
<div id="crayon-5bd7c6c1d6b2f291170008" class="crayon-syntax crayon-theme-visualstudiodark crayon-font-consolas crayon-os-pc print-yes notranslate" data-settings=" minimize scroll-mouseover">
<div class="crayon-main">
<table class="crayon-table">
<tbody>
<tr class="crayon-row">
<td class="crayon-nums " data-settings="show">
<div class="crayon-nums-content">
<div class="crayon-num" data-line="crayon-5bd7c6c1d6b2f291170008-1">1</div>
</div></td>
<td class="crayon-code">
<div class="crayon-pre">
<div id="crayon-5bd7c6c1d6b2f291170008-1" class="crayon-line"><span class="crayon-r">await</span> <span class="crayon-e">FindAllAsync</span><span class="crayon-sy">(</span><span class="crayon-sy">)</span><span class="crayon-sy">;</span></div>
</div></td>
</tr>
</tbody>
</table>
</div>
</div>
In asynchronous programming we have three return types:
<ul>
 	<li><code>Task&lt;TResult&gt;</code>, for an async method that returns a value</li>
 	<li><code>Task</code>, to use it for an async method that does not return a value</li>
 	<li><code>void</code>, which we can use for an event handler</li>
</ul>

<hr />

https://stackoverflow.com/questions/34680985/what-is-the-difference-between-asynchronous-programming-and-multithreading

Many people are taught that multithreading and asynchrony are the same thing, but they are not.

An analogy usually helps. You are cooking in a restaurant. An order comes in for eggs and toast.
<ul>
 	<li>Synchronous: you cook the eggs, then you cook the toast.</li>
 	<li>Asynchronous, single threaded: you start the eggs cooking and set a timer. You start the toast cooking, and set a timer. While they are both cooking, you clean the kitchen. When the timers go off you take the eggs off the heat and the toast out of the toaster and serve them.</li>
 	<li>Asynchronous, multithreaded: you hire two more cooks, one to cook eggs and one to cook toast. Now you have the problem of coordinating the cooks so that they do not conflict with each other in the kitchen when sharing resources. And you have to pay them.</li>
</ul>
Now does it make sense that multithreading is only one kind of asynchrony? <strong>Threading is about workers; asynchrony is about tasks</strong>. In multithreaded workflows you assign tasks to workers. In asynchronous single-threaded workflows you have a graph of tasks where some tasks depend on the results of others; as each task completes it invokes the code that schedules the next task that can run, given the results of the just-completed task. But you (hopefully) only need one worker to perform all the tasks, not one worker per task.

It will help to realize that many tasks are not processor-bound. For processor-bound tasks it makes sense to hire as many workers (threads) as there are processors, assign one task to each worker, assign one processor to each worker, and have each processor do the job of nothing else but computing the result as quickly as possible. But for tasks that are not waiting on a processor, you don't need to assign a worker at all. You just wait for the message to arrive that the result is available and <em>do something else while you're waiting</em>. When that message arrives then you can schedule the continuation of the completed task as the next thing on your to-do list to check off.

So let's look at Jon's example in more detail. What happens?
<ul>
 	<li>Someone invokes DisplayWebSiteLength. Who? We don't care.</li>
 	<li>It sets a label, creates a client, and asks the client to fetch something. The client returns an object representing the task of fetching something. That task is in progress.</li>
 	<li>Is it in progress on another thread? Probably not. Read <a href="http://blog.stephencleary.com/2013/11/there-is-no-thread.html" rel="noreferrer">Stephen's article</a> on why there is no thread.</li>
 	<li>Now we await the task. What happens? We check to see if the task has completed between the time we created it and we awaited it. If yes, then we fetch the result and keep running. Let's suppose it has not completed. <strong>We sign up the remainder of this method as the continuation of that task and return</strong>.</li>
 	<li>Now control has returned to the caller. What does it do? Whatever it wants.</li>
 	<li>Now suppose the task completes. How did it do that? Maybe it was running on another thread, or maybe the caller that we just returned to allowed it to run to completion on the current thread. Regardless, we now have a completed task.</li>
 	<li>The completed task asks the correct thread -- again, likely the <em>only</em> thread -- to run the continuation of the task.</li>
 	<li>Control passes immediately back into the method we just left at the point of the await. Now there <em>is</em> a result available so we can assign <code>text</code> and run the rest of the method.</li>
</ul>
It's just like in my analogy. Someone asks you for a document. You send away in the mail for the document, and keep on doing other work. When it arrives in the mail you are signalled, and when you feel like it, you do the rest of the workflow -- open the envelope, pay the delivery fees, whatever. You don't need to hire another worker to do all that for you.

<span class="comment-copy">A better example would be to say, that the cook cooks the eggs, but orders a different company to make the toasts. So the cook has just to look if the toasts has arrived every x minutes and at the rest time continues cooking his eggs. Then you have asynchronous with single thread</span>

&nbsp;

http://blog.stephencleary.com/2013/11/there-is-no-thread.html
<blockquote>To quote the <a href="http://www.amazon.com/gp/product/0735648735/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=0735648735&amp;linkCode=as2&amp;tag=stepheclearys-20">Tomes</a> of <a href="http://www.amazon.com/gp/product/0735665877/ref=as_li_ss_tl?ie=UTF8&amp;camp=1789&amp;creative=390957&amp;creativeASIN=0735665877&amp;linkCode=as2&amp;tag=stepheclearys-20">Knowledge</a>, “Regardless of the type of I/O request, internally I/O operations issued to a driver on behalf of the application are performed asynchronously”.</blockquote>
With the IRP “pending”, the OS returns to the library, which returns an incomplete task to the button click event handler, which suspends the async method, and the UI thread continues executing.

We have followed the request down into the abyss of the system, right out to the physical device.

The write operation is now “in flight”. How many threads are processing it?

None.

There is no device driver thread, OS thread, BCL thread, or thread pool thread that is processing that write operation. <strong>There is no thread.</strong>

<hr />

https://www.codeproject.com/Articles/996857/Asynchronous-programming-and-Threading-in-Csharp-N
<ol>
 	<li><code>Task.Factory.StartNew</code> method: Prior to .NET 4.5 (in .NET 4) this was the primary method to create and schedule a task.</li>
 	<li><code>Task.Run</code> or <code>Task.Run&lt;T&gt;</code> Method: From .NET 4.5 this method should be used. This method is sufficient for most of the common cases.</li>
 	<li><code>Task.FromResult</code> method: If the result is already computed, we can use this method to create a task.</li>
</ol>
<h3>What is an async method in C#?</h3>
An async method is a method that returns to the calling method before completing all its work, and then completes its work while the calling method continues its execution.

An async method has the following characteristics:

– An async method must have the async keyword in its method header, and it must be before the return type.
– This modifier doesn’t do anything more than signal that the method contains one or more await expressions.
– It contains one or more await expressions. These expressions represent tasks that can be done asynchronously.
– It must have one of the following three return types.
− void :If the calling method just wants the async method to execute, but doesn’t need any further interaction with it
− Task : If the calling method doesn’t need a return value from the async method, but needs to be able to check on the async method’s state
− Task :If the calling method is to receive a value of type T back from the call, the return type of the async method must be Task
– An async method can have any number of formal parameters of any types but it cannot be out or ref parameters.
– The name of an async method should end with the suffix Async.
– Other than Methods, lambda expressions and anonymous methods can also act as async objects.

You can read more on async and await <a href="http://www.csharpstar.com/async-await-keyword-csharp/" target="_blank" rel="noopener">here</a>.
<pre class="notranslate" lang="cs"><span class="code-keyword">static</span> <span class="code-keyword">void</span> Main(string[] args)
        {
            CallWithAsync();
            Console.ReadKey();           
        }

        <span class="code-keyword">async</span> <span class="code-keyword">static</span> <span class="code-keyword">void</span> CallWithAsync()
        {
            <span class="code-keyword">try</span>
            {
                CancellationTokenSource source = <span class="code-keyword">new</span> CancellationTokenSource();
                source.CancelAfter(TimeSpan.FromSeconds(<span class="code-digit">1</span>));
                <span class="code-keyword">var</span> t1 = <span class="code-keyword">await</span> GreetingAsync(<span class="code-string">"</span><span class="code-string">Bulbul"</span>, source.Token);
            }
            <span class="code-keyword">catch</span> (OperationCanceledException ex)
            {
                Console.WriteLine(ex.Message);
            }
        }

        <span class="code-keyword">static</span> Task&lt;string&gt; GreetingAsync(<span class="code-keyword">string</span> name, CancellationToken token)
        {
            <strong><span class="code-keyword">return</span> Task.Run&lt;string&gt;(() =<span class="code-keyword">&gt;</span>
            {
                <span class="code-keyword">return</span> Greeting(name, token);
            });</strong>
        }

        <span class="code-keyword">static</span> <span class="code-keyword">string</span> Greeting(<span class="code-keyword">string</span> name, CancellationToken token)
        {
            Thread.Sleep(<span class="code-digit">3000</span>);
            token.ThrowIfCancellationRequested();
            <span class="code-keyword">return</span> <span class="code-keyword">string</span>.Format(<span class="code-string">"</span><span class="code-string">Hello, {0}"</span>, name);
        }


</pre>
<p class="lf-text-block lf-block" data-lf-anchor-id="07a53c2547ba26d33a83ac46414a4bd3:0">https://docs.microsoft.com/en-us/dotnet/csharp/async</p>
<p class="lf-text-block lf-block" data-lf-anchor-id="07a53c2547ba26d33a83ac46414a4bd3:0">If the work you have is <strong>I/O-bound</strong>, use <code>async</code> and <code>await</code> <em>without</em> <code>Task.Run</code>. You <em>should not</em> use the Task Parallel Library. The reason for this is outlined in the <a href="https://docs.microsoft.com/en-us/dotnet/standard/async-in-depth" data-linktype="relative-path">Async in Depth article</a>.</p>
<p class="lf-text-block lf-block" data-lf-anchor-id="27c93c25459be4fb32038d46516b4f73:0">If the work you have is <strong>CPU-bound</strong> and you care about responsiveness, use <code>async</code> and <code>await</code> but spawn the work off on another thread <em>with</em> <code>Task.Run</code>. If the work is appropriate for concurrency and parallelism, you should also consider using the Task Parallel Library.</p>
<p class="lf-text-block lf-block x-hidden-focus" data-lf-anchor-id="0d31e96754b2e6f53165194640266291:0">Blocking the current thread as a means to wait for a Task to complete can result in deadlocks and blocked context threads, and can require significantly more complex error-handling. The following table provides guidance on how to deal with waiting for Tasks in a non-blocking way:<span class="lf-thread-btn"><a class="fycon-action-view" tabindex="0" aria-label="Write a Sidenote" data-lf-anchor-id="0d31e96754b2e6f53165194640266291:0">+</a></span></p>

<table>
<thead>
<tr>
<th>Use this...</th>
<th>Instead of this...</th>
<th>When wishing to do this</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>await</code></td>
<td><code>Task.Wait</code> or <code>Task.Result</code></td>
<td>Retrieving the result of a background task</td>
</tr>
<tr>
<td><code>await Task.WhenAny</code></td>
<td><code>Task.WaitAny</code></td>
<td>Waiting for any task to complete</td>
</tr>
<tr>
<td><code>await Task.WhenAll</code></td>
<td><code>Task.WaitAll</code></td>
<td>Waiting for all tasks to complete</td>
</tr>
<tr>
<td><code>await Task.Delay</code></td>
<td><code>Thread.Sleep</code></td>
<td class="">Waiting for a period of time</td>
</tr>
</tbody>
</table>
<h3><a href="http://www.csharpstar.com/csharp-interview-questions-part-7/">How can you cancel an Async operation in C#?</a></h3>
You can cancel your own async operation.There are two classes in the System.Threading.Tasks namespace that are designed for this purpose: CancellationToken and CancellationTokenSource.

A CancellationToken object contains the information about whether a task should be cancelled or not.
A task that has a CancellationToken object needs to periodically inspect it to see what the token’s state is. If the CancellationToken object’s
IsCancellationRequested property is set to true, the task should halt its operations and return.
A CancellationToken is nonreversible and can only be used once. That is, once it’s IsCancellationRequested property is set to true, it can’t be changed.
A CancellationTokenSource object creates a CancellationToken object, which can then be given to various tasks. Any objects holding a cancellationTokenSource can call its Cancel method, which sets the CancellationToken’s IsCancellationRequested property to true.

You can read more on Async and await <a href="http://www.csharpstar.com/async-await-keyword-csharp/" target="_blank" rel="noopener">here</a>.

https://www.codeguru.com/csharp/csharp/cs_misc/down-and-dirty-.net-task-parallel-library-multithreading-in-a-multicore-world.html

https://blogs.msdn.microsoft.com/pfxteam/2011/10/24/task-run-vs-task-factory-startnew/
