---
layout: post
title: Threads vs Parallel programming
date: 2018-10-29 14:00
author: tmasabari
comments: true
categories: [C#, Parallel Programming, Task, Threading, Uncategorized]
---
<h2>Threads vs Parallel programming</h2>
if we want stuff running <strong>concurrently or asynchrounously, we use threads</strong> (or the method we call spawns a thread for us). Which is all fine and good, as far as we’re concerned we have two (or more) seperate methods running at the same time that can do tasks independent of the main application’s thread.
<p id="ygnDvAw"><img class="alignnone  wp-image-1805 " src="/wp-content/uploads/2018/10/img_5bd6c2dda191e.png" alt="" width="344" height="95" /></p>

<ul>
 	<li>As you can see, each thread is actually running at different times, it just happens so fast that we don’t really notice it. The OS is assigning each process to a core, and then each thread within the process gets a chunk of time to execute on the designated core.</li>
 	<li>Threads are executed in single core more, so l<strong>oad given to the core is not split based on balance.</strong> It is allocated based on the sequence , threads are allocated more to perform in single core , after the core is heavy load. remaining threads are then in remaining core.</li>
 	<li><strong>Allocation of thread execution in core has to be handled manually by developers</strong> and it is more complex to find which core is heavy loaded , and  which core we have to execute the thread.</li>
</ul>
<p id="gctkUoa"><img class="alignnone  wp-image-1806 " src="/wp-content/uploads/2018/10/img_5bd6c36d0be55.png" alt="" width="361" height="87" /></p>

<ul>
 	<li>With parallel programming, an application <strong>has access to all cores/cpus</strong> available to a system, and delegates what runs where and at what time.</li>
 	<li>You might also notice that we now <strong>have “tasks” instead of threads</strong> – this is another key component of parallel programming.</li>
 	<li><strong>Instead of one big method</strong> that does what it needs to and then terminates when it’s done (i.e. a thread), we have a series of tasks that can either run asynchronously or be dependent on one another.</li>
 	<li>Once we have these tasks and dependancies defined, the <strong>parallel framework takes care of the execution plan</strong> for us.</li>
</ul>
Because each processing item is broken down into tasks,
<ul>
 	<li>tasks that can run parallel are executed at the same time</li>
 	<li>the tasks that are dependent on one another simply execute after their parent task is finished</li>
</ul>
Another neat thing to note is that the LINQ methods are going to be reworked to PLINQ methods, so they can automatically take advantage of this parallel processing model without having to change much of your code
<ul>
 	<li>Running tasks in parallel does not actually alter the program flow. It will run different tasks on different threads so that they can be executed on multiple CPU cores, in order to improve overall throughput of the program, but as far as the typical programmer is concerned, these tasks aren't really running in the "background" as they would be with a thread.</li>
 	<li>You don't have to change your program's structure or do anything special to be notified when the work completes. You have no control over what happens <em>inside</em> the parallel block, but you do know that the block will not return control until all parallel tasks are complete.</li>
 	<li>Although Parallel Extensions are great for this, it bears mentioning that <strong>PX are of no use whatsoever when you actually <em>need</em> to run a task in the background</strong>, such as implementing scheduler, or delegating to a worker thread in order to keep a UI responsive. You still need to use threads or async components for those.</li>
</ul>
<h2>References</h2>
<ul>
 	<li><a href="http://rtigger.com/blog/2009/06/19/thread-programming-vs-parallel-programming">http://rtigger.com/blog/2009/06/19/thread-programming-vs-parallel-programming</a></li>
 	<li><a href="http://dotnetvisio.blogspot.com/2013/07/difference-between-multi-threading-and.html">http://dotnetvisio.blogspot.com/2013/07/difference-between-multi-threading-and.html</a></li>
 	<li><a href="https://stackoverflow.com/questions/2331659/threading-vs-parallel-processing">https://stackoverflow.com/questions/2331659/threading-vs-parallel-processing</a></li>
</ul>
