---
layout: post
title: Parallelism and multicore
date: 2018-10-27 23:18
author: tmasabari
comments: true
categories: [Hardware, Multithreading, OS, Parallel and Threads, Processor, Processors, Thread]
---
<!-- wp:paragraph -->
<div class="votecell post-layout--left"> </div>
<div class="answercell post-layout--right">
<div class="post-text">
<p><strong>Parallelism</strong> is when tasks <em>literally</em> run at the same time, e.g., on a multicore processor. </p>
<ul>
<li>This <strong>requires hardware with multiple processing units</strong>.</li>
<li>To <strong>make programs faster</strong> by performing several computations at the same time</li>
</ul>
<div class="votecell post-layout--left">
<div class="vote"><strong style="font-size: 1rem;">Concurrency</strong><span style="font-size: 1rem;"> is when two or more tasks can start, run, and complete <strong>in overlapping time periods.</strong> </span></div>
<ul>
<li class="vote"><span style="font-size: 1rem;">It doesn't necessarily mean they'll ever both be running at the same instant. For example, </span><em style="font-size: 1rem;">multitasking </em><span style="font-size: 1rem;">on a single-core machine. </span><span style="font-size: 1rem;">A more generalized form of parallelism that can include <strong>time-slicing</strong> as a form of <strong>virtual parallelism</strong>.</span></li>
<li>To make programs more usable.</li>
<li>If an operating system is called a multi-tasking operating system, this is a synonym for supporting concurrency.</li>
</ul>
</div>
<div class="answercell post-layout--right">
<div class="post-text">
<p>&nbsp;</p>
</div>
</div>
</div>
</div>
<p><strong>Parallel computing</strong> is a type of <a href="https://en.wikipedia.org/wiki/Computing">computation</a> in which many calculations or the execution of <a href="https://en.wikipedia.org/wiki/Process_(computing)">processes </a>are carried out <strong>simultaneously</strong>.<sup><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-1">[1]</a></sup>  </p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
<li>In parallel computing, a large computational task is divided into several, very similar small subtasks that can be processed independently at a same time and whose results are combined afterwards, upon completion.</li>
<li>In contrast, in concurrent computing, the various processes often do not address related tasks; when they do, as is typical in <a href="https://en.wikipedia.org/wiki/Distributed_computing">distributed computing</a>, the separate tasks may have a varied nature and often require some <a href="https://en.wikipedia.org/wiki/Inter-process_communication">inter-process communication</a> during execution.
<ul>
<li>it is possible to have parallelism without concurrency (such as <a href="https://en.wikipedia.org/wiki/Bit-level_parallelism">bit-level parallelism</a>), and</li>
<li>concurrency without parallelism (such as multitasking by <a href="https://en.wikipedia.org/wiki/Time-sharing">time-sharing</a> on a single-core CPU).<sup><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-waza-5">[5]</a><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-6">[6]</a></sup> </li>
</ul>
</li>
<li>There are several different forms of parallel computing: <a href="https://en.wikipedia.org/wiki/Bit-level_parallelism">bit-level</a>, <a href="https://en.wikipedia.org/wiki/Instruction-level_parallelism">instruction-level</a>, <a href="https://en.wikipedia.org/wiki/Data_parallelism">data</a>, and <a href="https://en.wikipedia.org/wiki/Task_parallelism">task parallelism</a></li>
</ul>
<!-- /wp:list -->

<!-- wp:list -->
<ul>
<li>Parallel computers can be roughly classified according to the level at which the hardware supports parallelism, with <a href="https://en.wikipedia.org/wiki/Multi-core">multi-core</a> and <a href="https://en.wikipedia.org/wiki/Symmetric_multiprocessing">multi-processor</a> computers having multiple <a href="https://en.wikipedia.org/wiki/Processing_element">processing elements</a> within a single machine, while <a href="https://en.wikipedia.org/wiki/Computer_cluster">clusters</a>, <a href="https://en.wikipedia.org/wiki/Massively_parallel_(computing)">MPPs</a>, and <a href="https://en.wikipedia.org/wiki/Grid_computing">grids</a> use multiple computers to work on the same task.</li>
<li>
<p><strong>Hardware</strong> Paralellism can be achieved at several levels. Ordered by decreasing granularity :</p>
<ol>
<li>multi-host</li>
<li>multi-processor</li>
<li>multi-core</li>
<li>multi-threads ("Hyper-Threading", i.e. "HT") (EDIT: I voluntarity omit the case of vectorized compuations where several ALUs can be <em>driven</em> by the same core)</li>
</ol>
</li>
</ul>
<h2>Multitasking OS</h2>
<ul>
<li>Multitasking is a common feature of computer operating systems. It allows more efficient use of the computer hardware; where a program is waiting for some external event such as a user input or an <a href="https://en.wikipedia.org/wiki/Input/output">input/output</a> transfer with a peripheral to complete, the central processor can still be used with another program.</li>
<li>In <a href="https://en.wikipedia.org/wiki/Computing">computing</a>, <strong>multitasking</strong> is the <a href="https://en.wikipedia.org/wiki/Concurrent_computing">concurrent</a> execution of multiple tasks (also known as <a href="https://en.wikipedia.org/wiki/Process_(computing)">processes</a>) over a certain period of time. New tasks can interrupt already started ones before they finish, instead of waiting for them to end. As a result, a computer executes segments of multiple tasks in an interleaved manner, while the tasks share common processing resources such as <a href="https://en.wikipedia.org/wiki/Central_processing_unit">central processing units</a> (CPUs) and <a href="https://en.wikipedia.org/wiki/Main_memory">main memory</a>.</li>
<li>Multitasking automatically interrupts the running program, saving its state (partial results, memory contents and computer register contents) and loading the saved state of another program and transferring control to it.</li>
<li>This<strong> "<a href="https://en.wikipedia.org/wiki/Context_switch">context switch</a>"</strong> may be initiated at fixed time intervals (pre-emptive multitasking), or the running program may be coded to signal to the supervisory software when it can be interrupted (cooperative multitasking).</li>
<li>What is actually involved in a context switch varies between these senses and between processors and operating systems. For example, in the <a href="https://en.wikipedia.org/wiki/Linux_kernel">Linux kernel</a>, context switching involves switching registers, stack pointer, and <a href="https://en.wikipedia.org/wiki/Program_counter">program counter</a>, but is independent of <a href="https://en.wikipedia.org/wiki/Address_space">address space</a> switching, though in a process switch an address space switch also happens.<sup><a href="https://en.wikipedia.org/wiki/Context_switch#cite_note-1">[1]</a><a href="https://en.wikipedia.org/wiki/Context_switch#cite_note-2">[2]</a></sup></li>
<li><strong>Preemptive multitasking</strong> allows the computer system to more reliably guarantee to each process a regular "slice" of operating time. It also allows the system to deal rapidly with important external events like incoming data, which might require the immediate attention of one or another process. Operating systems were developed to take advantage of these hardware capabilities and run multiple processes preemptively.</li>
<li>Multitasking does not require <a href="https://en.wikipedia.org/wiki/Parallel_computing">parallel execution</a> of multiple tasks at exactly the same time; instead, it allows more than one task to advance over a given period of time.<sup><a href="https://en.wikipedia.org/wiki/Computer_multitasking#cite_note-1">[1]</a></sup> Even on <a href="https://en.wikipedia.org/wiki/Multiprocessor">multiprocessor</a> computers, multitasking allows many more tasks to be run than there are CPUs.</li>
</ul>
<p>&nbsp;</p>
<h2>Multi-threading</h2>
<!-- /wp:paragraph -->

<!-- wp:list --><!-- /wp:list -->

<!-- wp:list --><!-- /wp:list -->

<!-- wp:paragraph -->
<ul>
<li>A process is a program (you probably know this).</li>
<li>Multithreading is the process of having more than one thread per process (many processes will not make more than one thread because they do not have to).</li>
<li>Programs that support multithreading <strong>can use more than one core</strong> if more than one is available.</li>
<li>Windows does not have a hard limit on the number of threads you can create</li>
<li><a href="https://en.wikipedia.org/wiki/Thread_(computer_science)">Threads</a> were born from the idea that the most efficient way for cooperating processes to <strong>exchange data would be to share their entire memory space</strong>.</li>
<li>Thus, threads are effectively <strong>processes that run in the same memory context</strong> and share other resources with their <a href="https://en.wikipedia.org/wiki/Parent_process">parent processes</a>, such as open files.</li>
<li>Threads are described as <em>lightweight processes</em> because switching between threads does not involve changing the memory context.<sup><a href="https://en.wikipedia.org/wiki/Computer_multitasking#cite_note-6">[6]</a></sup><sup><a href="https://en.wikipedia.org/wiki/Computer_multitasking#cite_note-7">[7]</a></sup><sup><a href="https://en.wikipedia.org/wiki/Computer_multitasking#cite_note-8">[8]</a></sup></li>
<li>A running thread will consume all of a core. The only reason your CPU isnt running at 100% all the time is that the operating system knows how to suspend the processor, which basically makes it stop everything and wait until something happens (such as an IO event or a clock tick).</li>
<li>Only one thread can run on a core at once. Different threads running is actually just threads jumping onto the CPU and running for short periods of time, then being switched out with other threads which also need to run.</li>
</ul>
<h3><span id="Parallel_programming_languages" class="mw-headline">Parallel programming languages</span></h3>
<ul>
<li><a title="" href="https://en.wikipedia.org/wiki/List_of_concurrent_and_parallel_programming_languages">Concurrent programming languages</a>, <a title="Library (computing)" href="https://en.wikipedia.org/wiki/Library_(computing)">libraries</a>, <a title="Application programming interface" href="https://en.wikipedia.org/wiki/Application_programming_interface">APIs</a>, and <a title="Parallel programming model" href="https://en.wikipedia.org/wiki/Parallel_programming_model">parallel programming models</a> (such as <a title="Algorithmic skeleton" href="https://en.wikipedia.org/wiki/Algorithmic_skeleton">algorithmic skeletons</a>) have been created for programming parallel computers.</li>
<li>These can generally be divided into classes based on the assumptions they make about the <strong>underlying memory architecture</strong>—
<ul>
<li>shared memory,</li>
<li>distributed memory, or</li>
<li>shared distributed memory.</li>
</ul>
</li>
<li>Shared memory programming languages communicate by manipulating shared memory variables.</li>
<li>Distributed memory uses <a title="Message passing" href="https://en.wikipedia.org/wiki/Message_passing">message passing</a>. </li>
<li><a title="POSIX Threads" href="https://en.wikipedia.org/wiki/POSIX_Threads">POSIX Threads</a> and <a title="OpenMP" href="https://en.wikipedia.org/wiki/OpenMP">OpenMP</a> are two of the most widely used shared memory APIs, whereas <a title="Message Passing Interface" href="https://en.wikipedia.org/wiki/Message_Passing_Interface">Message Passing Interface</a> (MPI) is the most widely used message-passing system API.<sup id="cite_ref-56" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-56">[56]</a></sup> </li>
<li>One concept used in programming parallel programs is the <a title="Futures and promises" href="https://en.wikipedia.org/wiki/Futures_and_promises">future concept</a>, where one part of a program promises to deliver a required datum to another part of a program at some future time.</li>
</ul>
<h4><span id="Automatic_parallelization" class="mw-headline">Automatic parallelization</span></h4>
<ul>
<li>Automatic parallelization of a sequential program by a <a title="Compiler" href="https://en.wikipedia.org/wiki/Compiler">compiler</a> is the <a class="mw-redirect" title="Holy grail" href="https://en.wikipedia.org/wiki/Holy_grail">holy grail</a> of parallel computing. Despite decades of work by compiler researchers, automatic parallelization has <strong>had only limited success.</strong><sup id="cite_ref-57" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-57"><strong>[</strong>57]</a></sup></li>
<li>Mainstream parallel programming languages remain <strong>either <a title="Explicit parallelism" href="https://en.wikipedia.org/wiki/Explicit_parallelism">explicitly parallel</a> or (at best) <a title="Implicit parallelism" href="https://en.wikipedia.org/wiki/Implicit_parallelism">partially implicit</a></strong>, in which a programmer gives the <strong>compiler <a title="Directive (programming)" href="https://en.wikipedia.org/wiki/Directive_(programming)">directives </a>for parallelization</strong>.</li>
<li>A few fully implicit parallel programming languages exist—<a title="SISAL" href="https://en.wikipedia.org/wiki/SISAL">SISAL</a>, Parallel <a title="Haskell (programming language)" href="https://en.wikipedia.org/wiki/Haskell_(programming_language)">Haskell</a>, <a title="SequenceL" href="https://en.wikipedia.org/wiki/SequenceL">SequenceL</a>, <a title="System C" href="https://en.wikipedia.org/wiki/System_C">System C</a> (for <a class="mw-redirect" title="FPGA" href="https://en.wikipedia.org/wiki/FPGA">FPGAs</a>), <a class="new" title="Mitrion-C (page does not exist)" href="https://en.wikipedia.org/w/index.php?title=Mitrion-C&amp;action=edit&amp;redlink=1">Mitrion-C</a>, <a title="VHDL" href="https://en.wikipedia.org/wiki/VHDL">VHDL</a>, and <a title="Verilog" href="https://en.wikipedia.org/wiki/Verilog">Verilog</a>.</li>
</ul>
<p>&nbsp;</p>
<h2>Basics of parallel programming</h2>
<ul>
<li>A thread is a basic unit for execution: a thread is scheduled by operating system and executed by CPU.</li>
<li>A process is a sort of container that holds multiple threads. Multiple threads are separate 'chains' of commands within one process.</li>
<li>From CPU point of view threads are more or less like processes. Each thread has its own set of registers, memory(optional) and its own stack.</li>
<li>Threads running on the same core are not technically parallel. They only appear to be executed in parallel, as the CPU switches between them very fast (for us, humans). This switch is what is called context switch.</li>
<li>Now, threads executing on different cores are executed in parallel.</li>
<li>Most modern CPUs have a number of cores, however, most modern OSes (windows, linux and friends) usually execute much larger number of threads, which still causes context switches.</li>
<li>Even if no user program is executed, still OS itself performs context switches for maintanance work.</li>
</ul>
<ol>
<li>
<p>Both multi-processing or multi-threading is for parallel processing. More precisely, to exploit thread-level parallelism.</p>
</li>
<li>
<p>Multi-threading could mean <strong>hardware multi-threading</strong> (one example is HyperThreading). </p>
</li>
<li>
<p>Context switching is needed to implement <strong>multi-tasking</strong> even in a physically single core by time division.</p>
</li>
<li>
<p>The number of threads that can physically run simultaneously is just identical to # of <strong>logical processors</strong>.  <span style="font-size: 1rem;">Say there are two physical cores and four very busy threads. In this case, two threads are just waiting until they will get the chance to use CPU. </span></p>
</li>
</ol>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>History of parallel computers</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>In the early days of computing a CPU would only have <a href="https://www.makeuseof.com/tag/processor-core-makeuseof-explains-2/">a single core</a>. This meant that the CPU was limited to just a single set of tasks. This is one of the reasons that computing was often a relatively slow and time consuming, <a href="https://www.makeuseof.com/tag/a-brief-history-of-computers-that-changed-the-world/">but world changing</a> affair. </li>
<li>Multi-CPU was the first version: You'd have one or more mainboards with one or more CPU chips on them.
<ul>
<li>A dual-core processor for example is really just two separate CPUs on a single chip. By increasing the amount of cores, CPUs were able to handle multiple processes simultaneously.</li>
<li>The main problem here was that the CPUs would have to expose some of their internal data to the other CPU so they wouldn't get in their way.</li>
<li>The main problem with multi-CPU is that code running on them will eventually access the RAM. <strong>There are N CPUs but only one bus to access the RAM.</strong></li>
<li>So you must have some hardware which makes sure that
<ul>
<li>a) each CPU gets a fair amount of RAM access,</li>
<li>b) that accesses to the same part of the RAM don't cause problems and</li>
<li>c) most importantly, that CPU 2 will be notified when CPU 1 writes to some memory address which CPU 2 has in its internal cache. If that doesn't happen, CPU 2 will happily use the cached value, oblivious to the fact that it is outdated</li>
</ul>
</li>
<li>This is what effectively makes multi-CPU so complicated. Side effects of this can lead to a performance which is worse than what you'd get if the whole code ran only on a single CPU.</li>
</ul>
</li>
<li>The next step was hyper-threading. One chip on the mainboard but it had some parts twice internally so it could execute two instructions at the same time.</li>
<li>The current development is multi-core. It's basically the original idea (several complete CPUs) but in a single chip. </li>
<li>We’ve reached a practical limit as far as processor speeds go, manufacturers have started dumping more cores onto a cpu, which works pretty similar to having multiple CPUs installed in a system.</li>
<li>The advantage:
<ul>
<li>Chip designers can easily put lot of the additional wires for the sync signals into the chip (instead of having to route them out on a pin, then over the crowded mainboard and up into a second chip to synchronize the caches;</li>
<li>you could even copy data from one cache to another (updating <em style="font-size: 1rem;">parts</em><span style="font-size: 1rem;"> of a cache line without having to flush and reload it), etc. Or the cache logic could make sure that all CPUs get the same cache line when they access the same part of real RAM, simply blocking CPU 2 for a few nanoseconds until CPU 1 has made its changes.</span></li>
</ul>
</li>
<li>The main reason why multi-core is simpler than multi-cpu is that on a mainboard, you simply can't run all wires between the two chips which you'd need to make sync effective. Plus a signal only travels 30cm/ns tops (speed of light; in a wire, you usually have much less).</li>
<li>And don't forget that, on a multi-layer mainboard, signals start to influence each other (<strong>crosstalk</strong>). We like to think that 0 is 0V and 1 is 5V but in reality, <strong>"0" is something between -0.5V (overdrive when dropping a line from 1-&gt;0) and .5V and "1" is anything above 0.8V.</strong></li>
</ul>
<ul>
<li>Super computers today are multi-cpu, multi-core: They have lots of mainboards with usually 2-4 CPUs on them, each CPU is multi-core and each has its own RAM.</li>
</ul>
<h3><strong>Hyperthreading</strong></h3>
<ul>
<li>The CPU is fast, but memory is slow to respond. When the CPU requires instructions or data to be fetched from the memory chips, it has to wait doing nothing at all for a period of time in which <strong>it could have executed hundreds of instructions before the first byte of data comes in from memory</strong>.</li>
<li>In layman’s terms, <strong>hyper-threading allows a single physical core to act as two virtual cores</strong>, thus performing multiple tasks simultaneously.</li>
<li>Hyper-threading keeps track of two contexts at once in a single core, exposing more parallelism to the out-of-order CPU core.</li>
<li>This keeps the execution units fed with work, even when one thread is stalled on a cache miss, branch mispredict, or waiting for results from high-latency instructions.</li>
<li>To implement Hyperthreading, the CPU only has to duplicate the part of its circuitry that holds the data and the current instruction location of the currently running program. It's a way to get more total throughput without replicating much hardware, but if anything it slows down each thread individually.</li>
<li>Each thread in the computer stores its status and data in the CPU chip. To switch threads, the operating system has to take this data out of the CPU, store it away, and load up data for the other thread. Switching from one thread to another takes a few hundred instructions, but this is not a problem when the CPU can execute billions of instructions a second while a hard drive or network performs only about 30 operations per second. The overhead of thread switching for I/O is trivial.</li>
<li>However, do note that physical cores are faster than virtual cores. A quad-core CPU will perform much better than a dual-core CPU with hyper-threading!</li>
</ul>
<h3>Turbo Boost</h3>
<ul>
<li>Turbo Boost is Intel’s proprietary technology to intelligently <strong>increase a processor’s clock speed if the application demands it</strong>. For example, if you are playing a game and your system requires some extra horsepower, Turbo Boost will kick in to compensate.</li>
<li>Turbo Boost is useful for those who run resource-intensive software like video editors or video games, but it doesn’t have much of an effect if you’re just going to be browsing the web and using Microsoft Office.</li>
<li>Cache is the processor’s own memory and acts like its private RAM. It’s one of <a href="https://www.makeuseof.com/tag/5-little-known-specs-that-could-be-slowing-down-your-pc/">the little-known specs that slows down your PC</a>. <strong>Just like with RAM, more cache size is better.</strong> So if the processor is performing one task over and over, it will keep that task in its cache. If a processor can store more tasks in its private memory, it can do them faster if they come up again.</li>
</ul>
<p><img class="alignnone  wp-image-1799 " src="/wp-content/uploads/2018/10/img_5bd6825d7bb06.png" alt="" width="357" height="311" /><img class="alignnone  wp-image-1800 " style="font-size: 1rem;" src="/wp-content/uploads/2018/10/img_5bd682bf55ca5.png" alt="" width="308" height="283" /></p>
<p><img class="wp-image-1798  aligncenter" src="/wp-content/uploads/2018/10/img_5bd68087708fd.png" alt="" width="420" height="261" /></p>
<p>Intel Core i7 processors support</p>
<ol>
<li>Intel quad-core technology,</li>
<li>Intel HyperThreading Technology,</li>
<li>provides Intel QuickPath interconnect link to the chipset and</li>
<li>have integrated memory controller supporting three channel to DDR3 memory.</li>
</ol>
<p>&nbsp;</p>
<h2>Type of parallel computers</h2>
<ul>
<li>A <strong>distributed computer</strong> (also known as a distributed memory multiprocessor) is a distributed memory computer system in which the processing elements are connected by a network. Distributed computers are highly scalable.</li>
<li>The terms <strong>"<a title="Concurrent computing" href="https://en.wikipedia.org/wiki/Concurrent_computing">concurrent computing</a>", "parallel computing", and "distributed computing" have a lot of overlap</strong>, and no clear distinction exists between them.<sup id="cite_ref-40" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-40">[40]</a></sup> The same system may be characterized both as "parallel" and "distributed"; the processors in a typical distributed system run concurrently in parallel.<sup id="cite_ref-41" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-41">[41]</a></sup></li>
<li>A <strong>cluster</strong> is a group of loosely coupled computers that work together closely, so that in some respects they can be regarded as a single computer.<sup id="cite_ref-42" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-42">[42]</a></sup> Clusters are composed of multiple standalone machines connected by a network. While machines in a cluster do not have to be symmetric, <a title="Load balancing (computing)" href="https://en.wikipedia.org/wiki/Load_balancing_(computing)">load balancing</a> is more difficult if they are not. <strong>87% of all <a title="TOP500" href="https://en.wikipedia.org/wiki/TOP500">Top500</a> supercomputers are clusters.</strong><sup id="cite_ref-44" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-44">[44]</a></sup></li>
<li>A <strong>massively parallel processor (MPP)</strong> is a single computer with many networked processors. In an MPP, "each CPU contains its own memory and copy of the operating system and application. Each subsystem communicates with the others via a high-speed interconnect."<sup id="cite_ref-47" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-47">[47]</a></sup></li>
<li><strong>Grid computing</strong> is the most distributed form of parallel computing. It makes use of computers communicating over the <a title="Internet" href="https://en.wikipedia.org/wiki/Internet">Internet</a>to work on a given problem. Because of the low bandwidth and extremely high latency available on the Internet, distributed computing typically deals only with <a title="Embarrassingly parallel" href="https://en.wikipedia.org/wiki/Embarrassingly_parallel">embarrassingly parallel</a> problems.</li>
<li>Most grid computing applications use <a title="Middleware" href="https://en.wikipedia.org/wiki/Middleware">middleware</a> (software that sits between the operating system and the application to manage network resources and standardize the software interface).</li>
<li><a title="" href="https://en.wikipedia.org/wiki/Reconfigurable_computing">Reconfigurable computing</a> is the use of a <a title="Field-programmable gate array" href="https://en.wikipedia.org/wiki/Field-programmable_gate_array">field-programmable gate array</a> (FPGA) as a co-processor to a general-purpose computer. An FPGA is, in essence, a computer chip that can rewire itself for a given task.</li>
<li><strong>General-purpose computing on <a title="Graphics processing unit" href="https://en.wikipedia.org/wiki/Graphics_processing_unit">graphics processing units</a> (GPGPU)</strong> is a fairly recent trend in computer engineering research. GPUs are co-processors that have been heavily optimized for <a title="Computer graphics" href="https://en.wikipedia.org/wiki/Computer_graphics">computer graphics</a> processing.<sup id="cite_ref-50" class="reference"><a href="https://en.wikipedia.org/wiki/Parallel_computing#cite_note-50">[50]</a></sup> Computer graphics processing is a field dominated by data parallel operations—particularly <a title="Linear algebra" href="https://en.wikipedia.org/wiki/Linear_algebra">linear algebra</a> <a title="Matrix (mathematics)" href="https://en.wikipedia.org/wiki/Matrix_(mathematics)">matrix</a> operations. The technology consortium Khronos Group has released the <a title="OpenCL" href="https://en.wikipedia.org/wiki/OpenCL">OpenCL</a> specification, which is a framework for writing programs that execute across platforms consisting of CPUs and GPUs. <a class="mw-redirect" title="AMD" href="https://en.wikipedia.org/wiki/AMD">AMD</a>, <a title="Apple Inc." href="https://en.wikipedia.org/wiki/Apple_Inc.">Apple</a>, <a title="Intel" href="https://en.wikipedia.org/wiki/Intel">Intel</a>, <a title="Nvidia" href="https://en.wikipedia.org/wiki/Nvidia">Nvidia</a> and others are supporting <a title="OpenCL" href="https://en.wikipedia.org/wiki/OpenCL">OpenCL</a>.</li>
<li>A vector processor is a CPU or computer system that can execute the same instruction on large sets of data. Vector processors have high-level operations that work on linear arrays of numbers or vectors.Modern <a class="mw-redirect" title="Instruction set" href="https://en.wikipedia.org/wiki/Instruction_set">processor instruction sets</a> do include some vector processing instructions, such as with <a title="Freescale Semiconductor" href="https://en.wikipedia.org/wiki/Freescale_Semiconductor">Freescale Semiconductor</a>'s <a title="AltiVec" href="https://en.wikipedia.org/wiki/AltiVec">AltiVec</a> and <a title="Intel" href="https://en.wikipedia.org/wiki/Intel">Intel</a>'s <a title="Streaming SIMD Extensions" href="https://en.wikipedia.org/wiki/Streaming_SIMD_Extensions">Streaming SIMD Extensions</a> (SSE).</li>
</ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<h2>References</h2>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
<li><a href="https://en.wikipedia.org/wiki/Parallel_computing">https://en.wikipedia.org/wiki/Parallel_computing</a></li>
<li><a href="https://en.wikipedia.org/wiki/Concurrent_computing">https://en.wikipedia.org/wiki/Concurrent_computing</a></li>
<li><a href="https://en.wikipedia.org/wiki/Computer_multitasking">https://en.wikipedia.org/wiki/Computer_multitasking</a></li>
<li><a href="https://people.cs.clemson.edu/~mark/multithreading.html">https://people.cs.clemson.edu/~mark/multithreading.html</a></li>
<li><a href="https://www.makeuseof.com/tag/intel-core-i3-vs-i5-vs-i7-one-really-need/">https://www.makeuseof.com/tag/intel-core-i3-vs-i5-vs-i7-one-really-need/</a></li>
<li><a href="https://www.makeuseof.com/tag/cpu-technology-explained/">https://www.makeuseof.com/tag/cpu-technology-explained/</a></li>
<li><a href="https://software.intel.com/en-us/articles/intel-sdm#combined">Intel® 64 and IA-32 Architectures Software Developer Manuals</a></li>
<li><a href="https://stackoverflow.com/questions/1713554/threads-processes-vs-multithreading-multi-core-multiprocessor-how-they-are">https://stackoverflow.com/questions/1713554/threads-processes-vs-multithreading-multi-core-multiprocessor-how-they-are</a></li>
<li><a href="https://stackoverflow.com/questions/11835046/multithreading-and-multicore-differences">https://stackoverflow.com/questions/11835046/multithreading-and-multicore-differences</a></li>
<li><a href="https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism">https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism</a></li>
<li><a href="http://www.haskell.org/haskellwiki/Parallelism_vs._Concurrency">http://www.haskell.org/haskellwiki/Parallelism_vs._Concurrency</a></li>
<li><a href="https://stackoverflow.com/questions/10245337/how-is-parallelism-on-a-single-thread-core-possible">https://stackoverflow.com/questions/10245337/how-is-parallelism-on-a-single-thread-core-possible</a></li>
<li><a href="https://stackoverflow.com/questions/10245337/how-is-parallelism-on-a-single-thread-core-possible">https://stackoverflow.com/questions/10245337/how-is-parallelism-on-a-single-thread-core-possible</a></li>
<li><a href="https://stackoverflow.com/questions/680684/multi-cpu-multi-core-and-hyper-thread">https://stackoverflow.com/questions/680684/multi-cpu-multi-core-and-hyper-thread</a></li>
<li><a href="http://rtigger.com/blog/2009/06/19/thread-programming-vs-parallel-programming">http://rtigger.com/blog/2009/06/19/thread-programming-vs-parallel-programming</a></li>
</ul>
<!-- /wp:list -->
