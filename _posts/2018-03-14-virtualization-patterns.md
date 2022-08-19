---
layout: post
title: Patterns - Hardware & Virtualization
date: 2018-03-14 16:43
author: tmasabari
comments: true
categories: [Cloud, Container, Hardware, Virtualization]
---
<h2>Background</h2>
<ul>
 	<li>Decoupling applications from the underlying hardware is the fundamental concept behind virtualization.</li>
 	<li>Containers go a step further and decouple applications from the underlying OS. This enables <strong>cloudlike flexibility, including portability and efficient scaling</strong>.</li>
 	<li>Container virtualization solves one of the main problem that system administrators and developers faced for years. Its this “It was working on dev and qa. But why the hell is it not working on production environment”.</li>
 	<li>Developers are working in much the same way as a race car mechanic would. The goal is to strip all the unnecessary weight off the race car leaving just the bare essentials.</li>
 	<li>Google invested in containers early on. Anything you do on Google today is done in a container—whether it’s Search, Gmail, Google Docs—you get a container of your own for each service.</li>
</ul>
<h2>Basics</h2>
<h3 id="some-definitions">Some Definitions:</h3>
<strong><a href="https://www.techopedia.com/definition/2153/bare-metal">Bare meta</a>l</strong> is a computer system without a base operating system (OS) or installed applications. It is a computer's hardware assembly, structure and components that is installed with either the firmware or basic input/output system (BIOS) software utility or no software at all.
<h3><a href="http://www.cloudcomputingpatterns.org/hypervisor/">Hypervisor</a></h3>
<ul>
 	<li>If multiple applications are deployed on <strong>a physical server</strong> they may have to consider the other applications in their configuration. For example, if applications require the same network ports, access the same directories in the local file system etc. This <strong>sharing of common underlying physical hardware between different applications</strong> shall be simplified while also reducing dependencies of the application on the physical server.</li>
 	<li>A Hypervisor abstracts the hardware of a shared physical server into virtualized hardware.</li>
 	<li>On this virtual hardware, different operating systems and middleware are installed to host applications sharing the physical server while being isolated from each other regarding the use of physical hardware, such as central processing units <strong>(CPU), memory, disk storage, and networking</strong>.</li>
 	<li>
<p id="HKJytXl"><img class="alignnone wp-image-931 " src="/wp-content/uploads/2018/03/img_5aa8c0999aed9.png" alt="" width="311" height="281" /></p>

<ul>
 	<li>A hypervisor might not need OS at all. Multiple hypervisors can be loaded a single physical machine</li>
</ul>
</li>
</ul>
<h2 id="what-are-containers" class="heading-with-anchor">What are Containers</h2>
<p class="lf-text-block lf-block" data-lf-anchor-id="151caeaf05b900bc39a5e04a97315e65:0">Containers are a way to wrap up an application into its own isolated box. For the application in its container, it has no knowledge of any other applications or processes that exist outside of its box. Everything the application depends on to run successfully also lives inside this container. Wherever the box may move, the application will always be satisfied because it is bundled up with everything it needs to run.</p>
<p data-lf-anchor-id="151caeaf05b900bc39a5e04a97315e65:0">Containers are an isolated, resource controlled, and portable runtime environment which runs on a host machine or virtual machine. An application or process which runs in a container is packaged with all the required dependencies and configuration files; It’s given the illusion that there are no other processes running outside of its container.</p>

<ul>
 	<li><strong>Container Host:</strong> Also called the <strong>Host OS</strong>. The Host OS is the operating system on which the container engine (Docker client and Docker daemon) run. In the case of Linux and non-Hyper-V containers, the Host OS shares its kernel with running Docker containers. For Hyper-V each container has its own Hyper-V kernel.</li>
 	<li><strong>Container Repository:</strong> Each time a container image is created, the container image and its dependencies are stored in a local repository. These images can be reused many times on the container host. The container images can also be stored in a public or private registry, such as DockerHub, so that they can be used across many different container hosts.</li>
 	<li><strong>Container OS:</strong> Also called the <strong>Base OS</strong>. The base OS refers to an image that contains an operating system such as Ubuntu, CentOS, or windowsservercore. Typically, you would build your own image on top of a Base OS image so that you can take utilize parts of the OS. Note that windows containers require a Base OS, while Linux containers do not.</li>
 	<li><strong>Windows Container OS Image:</strong> Containers are deployed from images. The container OS image is the first layer in potentially many image layers that make up a container. This image provides the operating system environment. A Container OS Image is immutable. That is, it cannot be modified.</li>
 	<li><strong>Operating System Kernel:</strong> The Kernel manages lower level functions such as memory management, file system, network and process scheduling.</li>
 	<li><strong>Sandbox:</strong> Once a container has been started, all write actions such as file system modifications, registry modifications or software installations are captured in this ‘sandbox’ layer.</li>
 	<li><strong>Container Image:</strong> In many cases you may want to capture this state in Sandbox such that new containers can be created that inherit these changes. That’s what an image is – once the container has stopped you can either discard that sandbox or you can convert it into a new container image.</li>
 	<li>For example, let’s imagine that you have deployed a container from the Windows Server Core OS image. You then install MySQL into this container. Creating a new image from this container would act as a deployable version of the container. This image would only contain the changes made (MySQL), however it would work as a layer on top of the Container OS Image.</li>
 	<li>
<p id="MsIKnez"><img class="wp-image-1061  aligncenter" src="/wp-content/uploads/2018/03/img_5aae82b87175c.png" alt="" width="465" height="231" /></p>
</li>
</ul>
<h3><a href="http://www.cloudcomputingpatterns.org/execution_environment/">Execution Environment</a> (Container)</h3>
<ul>
 	<li>Applications often use similar functions (common libraries), for example, to access networking interfaces, display user interfaces, access storage of the server etc.
<ul>
 	<li>In this case, each <strong>application implements similar components</strong> that could be shared with other applications.</li>
 	<li>Sharing such common functionality between applications would also result in a better utilization of the environment and</li>
 	<li>avoid duplicate implementation of functionality</li>
</ul>
</li>
 	<li>Common functionality is summarized in an <strong>Execution Environment </strong>providing functionality in<strong> platform libraries</strong> to be used in custom application implementations and in the form of the <strong>middleware</strong>.</li>
 	<li> The environment, thus, executes custom application components and provides common functionality for data storages, communication etc.</li>
 	<li>
<p id="LtUXTyp"><img class="wp-image-929  aligncenter" src="/wp-content/uploads/2018/03/img_5aa8be78866d3.png" alt="" width="151" height="163" /></p>
</li>
</ul>
<h2>Different virtualization options</h2>
<p id="eYxDnkJ"><img class="alignleft wp-image-958" src="/wp-content/uploads/2018/03/img_5aa8fb2890114.png" alt="" width="294" height="185" /></p>
<p id="ZDKZBIy"><img class="alignnone  wp-image-1059 " src="/wp-content/uploads/2018/03/img_5aadef6a49de6.png" alt="" width="429" height="212" /></p>

<ul>
 	<li><strong>Bare metal virtualization</strong> the <strong>Hypervisor sits directly on top of the hardware</strong>. The hardware device drivers are part of the hypervisor, and there will be only one memory and CPU manager(that is part of the hypervisor which sitting directly on top of the hardware. This is the reason its called as bare metal virtualization)
<ul>
 	<li>VMware ESX and Citrix Xen Servers are good examples of Bare Metal virtualization.</li>
</ul>
</li>
 	<li><strong>Hosted virtualization</strong>: A software hypervisor installed inside the base operating system, which will intern do the resource allocation and monitoring
<ul>
 	<li>Examples includes VMware Workstation, Microsoft's Virtual PC</li>
 	<li>Although Hosted virtualization is <strong>cheaper</strong>, there are limitations in it, especially in terms of <strong>performance</strong>. This performance impact happens majorly due to the fact that there are multiple memory and cpu managers for a guest operating system.
<ol>
 	<li>First there is a memory and cpu manager that is part of the base operating system(on which our hypervisor sits),</li>
 	<li>then the hypervisor itself has a cpu and memory manager</li>
 	<li>memory and cpu manager of guest OS runs within VM</li>
</ol>
</li>
</ul>
</li>
 	<li><strong>Container Virtualization : </strong>Each container(well call it guest operating system) <strong>shares the same kernel of the base system.</strong>
<ul>
 	<li><span style="font-size: 1rem;">As each containers are sitting on top of the common OS kernel, and sharing most of the base operating system, containers are much smaller and light weight compared to a virtualized guest operating system. </span></li>
 	<li><span style="font-size: 1rem;">As they are light weight an operating system can have many containers running on top of it, compared to the limited number of guest operating system that you can run. </span></li>
 	<li>Examples of Container based virtualization includes <strong>LXC, OpenVz, Parallels Virtuozzo, Solaris Containers</strong>, <strong>Docker</strong>(Uses LXC), <strong>HP-UX</strong> containers etc.</li>
 	<li>The one thing that hypervisors can do that <strong>containers can’t</strong> is to use different <strong>operating systems or kernels</strong>.</li>
 	<li>how often in a production environment do you really want to run multiple operating system VMs on a server? I’d say “Not very damn often.”</li>
</ul>
</li>
</ul>
<h3>Containers Vs VMs</h3>
<ul>
 	<li>Using a totally tuned-up container system, you should expect to see four-to-six times as many server instances as you can using Xen or KVM VMs.</li>
 	<li><strong>Instead of virtualizing hardware, containers rest on top of a single Linux instance</strong>. This means you can “leave behind the useless 99.9% VM junk, leaving you with a small, neat capsule containing your application,”</li>
</ul>
<h3><strong>Linux Containers (LXC)</strong></h3>
<ul>
 	<li>To use containers in Linux you use the <a title="Linux Containers" href="https://linuxcontainers.org/" target="_blank" rel="noopener">LXC userspace tools</a>. With this, applications can run in their own container. Implemented in 2008.</li>
 	<li>As far as the program is concerned, it has its own file system, storage, CPU, RAM, and so on.
So far that sounds remarkably how a VM looks to an application. The key difference is that while the hypervisor abstracts an entire device, containers just abstract the operating system kernel.</li>
 	<li>This isolation of each containers is provided by a major Linux kernel feature called as cgroups and namespace. To do this it uses these Linux kernel features:
<ol>
 	<li>Kernel namespaces (ipc, uts, mount, pid, network, and user)</li>
 	<li>AppArmor and SELinux profiles</li>
 	<li>Seccomp policies</li>
 	<li><strong>Chroots</strong> (using pivot_root) (started in 1979)- change root directory of a process tree to new location in fie system which is only visible to a given process</li>
 	<li><strong>Control groups (cgroups) </strong>(implemented in 2006 by Google and merged to the Linux kernel 2.6.24 in 2007) - for limiting, accounting, and isolating resource usage (CPU, memory, disk I/O, network, etc.) of a collection of processes.</li>
 	<li>Kernel capabilities</li>
</ol>
</li>
 	<li>Linux <strong>security modules</strong> guarantee that access to the host machine and the kernel from the containers is properly managed to <strong>avoid any intrusion activities</strong>.</li>
 	<li>In addition containers can <strong>run different Linux distributions</strong> from its host operating system if both operating systems can run on the same CPU architecture.</li>
 	<li><strong>Namespaces</strong> deal with resource isolation for a single process, while cgroups manage resources for a group of processes.</li>
 	<li>For example, if you have an application that takes up a lot of CPU cycles and memory, such as a scientific computing application, you can put the application in a cgroup to limit its CPU and memory usage.
<ul>
 	<li>By default on a Linux system, all processes are children of the INIT process. Which means all processes are part of a single tree structure.</li>
 	<li>Now in Cgroup method, different process groups, can exist on a single system.</li>
 	<li>So instead of a single process tree of default linux method, cgroup method can have different trees of process structure(with different parents, and childs will inherit stuff from their parents), all isolated from each other.</li>
</ul>
</li>
 	<li>Now there is a feature in Linux kernel which creates <strong>new namespace for each containers</strong>. Now what namespaces is in simple layman terms is that it enables applications to run in their own isolated environments with separate process id lists, network devices, file system, user lists etc.</li>
 	<li>
<div>Few namespace's that you can have in Linux is as below.</div>
<ul>
 	<li>PID (Isolated process id's)</li>
 	<li>Net (Network interfaces)</li>
 	<li>mnt (Mounting file system)</li>
 	<li>Hostname separation</li>
 	<li>Users.</li>
</ul>
</li>
</ul>
<h3>Docker summary</h3>
<ul>
 	<li>Docker, which <strong>started</strong> as an <strong>open source project to build single-application LXC containers</strong>, it later morphed into its <strong>own container runtime environment. </strong></li>
 	<li>Docker also used LXC at the initial stages and later<strong> replaced LXC with it’s own library called libcontainer</strong>. Unlike any other container platform, Docker introduced an entire ecosystem for managing containers.
<ul>
 	<li>This includes a highly efficient, layered container image model,</li>
 	<li>a global and local container registries,</li>
 	<li>a clean REST API, a CLI, etc.</li>
 	<li>took an initiative to implement a container cluster management solution called <strong>Docker Swarm</strong>.</li>
</ul>
</li>
 	<li><strong>Docker Engine (what most people call "Docker")</strong> is a containerization technology. It gives
<ul>
 	<li>Process isolation</li>
 	<li>Network isolation</li>
 	<li>Consistent application environment</li>
</ul>
</li>
 	<li>It’s a <strong>packaging system</strong> for applications.</li>
 	<li><strong>It's open-source engine</strong> can be used to <strong>pack, ship, and run any application</strong> as a <strong>lightweight, portable, self sufficient LXC container</strong> that <strong>runs virtually anywhere</strong>.</li>
 	<li>Basically, <strong>Docker brings cloudlike flexibility to any infrastructure</strong> capable of running containers. Docker enable you to create a <strong>containerized app on your laptop and deploy it to the cloud</strong>. “Containers gives you instant application portability,”</li>
 	<li>Using Docker containers, you can <strong>deploy, replicate, move, and back up a workload</strong> even more quickly and easily than you can do so using virtual machines.</li>
 	<li><strong>Docker Hub</strong> is an image registry. It stores Docker images so you can download them as part of your deployment.</li>
 	<li><strong>Docker Cloud</strong> is an orchestration system for Docker. It can give you
<ul>
 	<li>Scale your applications up and down</li>
 	<li>Connect your applications to each other</li>
 	<li>CI testing, integrated with Docker Hub (this isn't part of orchestration, just another thing it does)</li>
</ul>
</li>
</ul>
<h3><strong>LXC to Docker</strong></h3>
<ul>
 	<li><strong>Portability.</strong> is the single most important advance of Docker over LXC.
<ul>
 	<li>Docker abstracts away more <strong>networking, storage, and OS details</strong> from the application than LXC does.</li>
 	<li>With Docker, the application is<strong> truly independent from the configurations</strong> of these low-level resources.</li>
 	<li>When you move a Docker container from one Docker host to another Docker-enabled machine, Docker <strong>guarantees that the environment for the application will remain the same</strong>.</li>
 	<li>enables developers to set up local development environments that are exactly like a production server</li>
</ul>
</li>
 	<li>Docker containers are designed to be stateless, more so than LXC.

First, Docker does not support persistent storage. Docker gets around this by allowing you to mount host storage as a “Docker volume” from your containers. Because the volumes are mounted, they are not really part of the container environment.</li>
 	<li>Docker containers consist of read-only layers. This means that, once the container image has been created, it does not change.
<ul>
 	<li>During runtime, if the process in a container makes changes to its internal state, a “diff” is made between the internal state and the image from which the container was created.</li>
 	<li>If you run the <code>docker commit</code> command, the diff becomes <strong>part of a new image—not the original image</strong>,</li>
 	<li>but a new image, from which you can create new containers. Otherwise, if you delete the container, the diff disappears.</li>
 	<li> it’s not easy to commit small, application-level changes to a single-process container. You are essentially forced to start a new, updated container.</li>
 	<li>https://stackoverflow.com/questions/34357252/docker-data-volume-vs-mounted-host-directory
The host directory is, by its nature, host-dependent. For this reason, you can’t mount a host directory from Dockerfile because built images should be portable. A host directory wouldn’t be available on all potential hosts.

If you have some persistent data that you want to share between containers, or want to use from non-persistent containers, it’s best to create a named Data Volume Container, and then to mount the data from it.</li>
</ul>
</li>
 	<li>To run a simple multi-tier php web application in Docker, you would need a <strong>PHP container</strong>, an <strong>Nginx container (the web server)</strong>, a <strong>MySQL container</strong> (for the database process), and a few <strong>data containers for storing the database tables and other application data</strong>.
<ul>
 	<li>including easy and more granular updates. Why shut down the database process when all you wanted to update is the web server?</li>
 	<li>you can’t run agents, logging scripts, or an SSH daemon inside the container</li>
</ul>
</li>
</ul>
<table style="width: 749px;">
<tbody>
<tr style="height: 28px;">
<td style="width: 326px; height: 28px;">LXC</td>
<td style="width: 393px; height: 28px;">Docker</td>
</tr>
<tr style="height: 52.5px;">
<td style="width: 326px; height: 52.5px;">LXC containers have a conventional <a href="http://www.yolinux.com/TUTORIALS/LinuxTutorialInitProcess.html" rel="nofollow">init process</a> and can run multiple processes.</td>
<td style="width: 393px; height: 52.5px;">Docker restricts containers to run as a single process. If your application environment consists of X concurrent processes, Docker wants you to run X containers, each with a distinct process.</td>
</tr>
</tbody>
</table>
<h3 id="2016-windows-containers:ba85387dcdeb3e25471a63f45f6b923c">2016 — <a href="https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview">Windows Containers</a></h3>
<ul>
 	<li>released with Microsoft Windows Server 2016. With this implementation Docker would be able to <strong>run Docker containers on Windows natively</strong> without having to run a virtual machine to run Docker (<strong>earlier</strong> Docker ran on Windows <strong>using a Linux VM</strong>).</li>
</ul>
<h3>Linux Vs Windows</h3>
[table id=13 /]
<table style="width: 735px;" cellspacing="0" cellpadding="0">
<tbody>
<tr style="height: 257px;">
<td style="width: 305px; height: 257px;">
<p id="dUuNtMO"><img class="alignnone size-full wp-image-1055 " src="/wp-content/uploads/2018/03/img_5aadd1945a93f.png" alt="" /></p>
</td>
<td style="width: 424px; height: 257px;">
<p id="IHySUtJ"><img class="alignnone wp-image-1056 " src="/wp-content/uploads/2018/03/img_5aadd21e98fbf.png" alt="" width="428" height="359" /></p>
</td>
</tr>
<tr style="height: 432px;">
<td style="width: 305px; height: 432px;">The Host OS is Ubuntu.

The Docker Client and the Docker Daemon (together called the Docker Engine) are running on the Host OS.

Each container shares the Host OS kernel.

CentOS and BusyBox are Linux Base OS images.

The “No OS” container demonstrates that you do not NEED a base OS to run a container in Linux. You can create a Docker file that has a base image of <a href="https://hub.docker.com/_/scratch/">scratch</a>and then runs a binary that uses the kernel directly.</td>
<td style="width: 424px; height: 432px;">The Host OS is Windows 10 or Windows Server.

Each container is hosted in its own light weight Hyper-V VM.

Each container uses the kernel inside the Hyper-V VM which provides an extra layer of separation between containers.</td>
</tr>
</tbody>
</table>
<h3></h3>
<h3>Bare essentials</h3>
Do we need every Linux commands, library, etc inside of our container to run a Hello World script? Probably not. Why not install just the bare essentials required to run the application thats inside of your container.
<h4>Benefits</h4>
<ul>
 	<li>Besides the obvious which is pure size it also makes your <strong>environment small and efficient</strong>.</li>
 	<li>Small images all increase <strong>security</strong> as you reduce your security footprint size.</li>
</ul>
<h2 id="container-orchestrators" class="heading-with-anchor">Container orchestrators</h2>
<p class="lf-text-block lf-block" data-lf-anchor-id="89012c6ff7b92e5a1f38a867474343c5:0">The standard definition of orchestration includes the following tasks:<span class="lf-thread-btn"><a class="fycon-action-view" tabindex="0" aria-label="Write a Sidenote" data-lf-anchor-id="89012c6ff7b92e5a1f38a867474343c5:0">+</a></span></p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="15957d3f4d3a8cbd23c19d5659336671:0">
 	<li>Service discovery: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</li>
 	<li>Scheduling: Given a container image and a resource request, find a suitable machine on which to run the container.</li>
 	<li>Affinity/Anti-affinity: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</li>
 	<li>Health monitoring: Watch for container failures and automatically reschedule them.</li>
 	<li>Failover: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</li>
 	<li>Scaling: Add or remove container instances to match demand, either manually or automatically.</li>
 	<li>Networking: Provide an overlay network for coordinating containers to communicate across multiple host machines.</li>
 	<li class="">Coordinated application upgrades: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</li>
 	<li>Azure offers two container orchestrators:
<ul>
 	<li><a href="https://docs.microsoft.com/en-us/azure/aks/" data-linktype="absolute-path">Azure Container Service (AKS)</a> makes it simple to create, configure, and manage a cluster of virtual machines that are preconfigured to run containerized applications.</li>
 	<li><a href="https://docs.microsoft.com/en-us/azure/service-fabric/" data-linktype="absolute-path">Azure Service Fabric</a> is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</li>
</ul>
</li>
 	<li>
<p id="ZEolXib"><img class="wp-image-1062  aligncenter" src="/wp-content/uploads/2018/03/img_5aae8d56e0aaa.png" alt="" width="496" height="279" /></p>
</li>
</ul>
<h2>Difference between Windows and Linux containers</h2>
<ul>
 	<li>
<h3>Kernel Mode</h3>
&nbsp;
<ul>
 	<li>The Kernel Mode of an operating system has been implemented for drivers that need to have unrestricted access to the underlying hardware.
<ul>
 	<li>Code that is running within the Kernel Mode has direct access to those resources and shares the same memory locations/virtual address space as the operating system and other kernel drivers.</li>
 	<li>Running code in this Kernel Mode is therefore very risky, because data that belongs to the operating system or another driver could be compromised as a result of your kernel mode code accidentally writing data to a wrong virtual address.</li>
 	<li>If a kernel mode driver crashes, the entire operating system crashes.</li>
</ul>
</li>
 	<li>Normal programs (User Mode) have to make use of the operating system API’s to access hardware or memory.
<ul>
 	<li>In the User Mode, the code always runs in a separate process (user space), which has its own dedicated set of memory locations (private virtual address space).</li>
 	<li>A processor running in user mode cannot access virtual addresses that are reserved for the operating system.</li>
</ul>
</li>
 	<li>Each container is just a processor “User Mode” with a couple of additional features such as namespace isolation, resource governance and the concept of a union file system.</li>
 	<li>Before the launch of Windows Server 2016, each Windows operating system we used consisted of a single “User Mode” and “Kernel Mode”. Since the introduction of Windows Server 2016 it is possible to have multiple User Modes running within the same operating system.</li>
 	<li>
<p id="AWEJIZm"><img class="alignnone size-full wp-image-1064 " src="/wp-content/uploads/2018/03/img_5aae9e590c04b.png" alt="" /></p>
</li>
 	<li>Looking at the User Modes of Windows Server 2016, we can identify two different types: the Host User Mode and the Container User Modes (green blocks in the diagram).</li>
 	<li>Goal of the Host User Mode is to host the core Windows services and processes like the user interaction, Session Manager, Event Manager and networking.</li>
 	<li>Same Docker tools and commands for both Windows as Linux containers  (Docker Compose, Docker Swarm)</li>
 	<li>The core of this container technology is the Computer Services (orange block) abstraction, which exposes the low-level container capabilities provided by the kernel via a public API. In fact, these services only contain functionality to launch Windows containers, keep track of them while they are running and manage the functionality required for restarting.</li>
 	<li>The rest of the Container Management functionality is implemented in the Docker Engine like keeping track of all containers, storing container images, volumes etc. This engine directly communicates with the Compute Services container API’s and makes use of the “Go language binding” offered by Microsoft to do so.</li>
</ul>
</li>
 	<li>
<p id="gbhNsPP"><img class="alignnone  wp-image-1063 " src="/wp-content/uploads/2018/03/img_5aae9c347a38e.png" alt="" width="719" height="240" /></p>
</li>
 	<li>Where <strong>Linux</strong> exposes its <strong>kernel</strong> level functionalities <strong>via syscalls</strong>, Microsoft decided to control their <strong>kernel mode</strong> outbound functionalities <strong>via DLL’s</strong> (this is also the reason why Microsoft not really has documented their syscalls).
<ul>
 	<li>the expectation from a lot of DLL’s that some (in)direct referenced system services are running within container for interaction. Within Windows containers you’ll therefor see a bunch of extra System Processes running while Linux containers only have to run the specified Application Processes.</li>
 	<li>To ensure that those necessary System Processes and services are running within the Windows container, within each container a so-called smss process is launched. Goal of this smss process is to start the necessary System Processes and services.</li>
</ul>
</li>
 	<li><strong>OS Architecture: </strong>Looking at the current Windows Server 2016 container implementation a so-called Compute Services abstraction layer is implemented that abstracts the low-level container capabilities from the outside. Reason for this is that Microsoft can change the low-level container API’s without having to change the public API’s that are called by the Docker Engine or other container client tools.</li>
 	<li>"copy-on-write" technology of Docker. The current Windows Server 2016 container implementation therefor does not contain a true Union Filesystem.
<ul>
 	<li>Instead, the current implementation creates a new virtual NTFS disk per container. To keep this virtual disks small, the different file system entries within this virtual NTFS disks are essential symlinks to real files on the filesytem of the container host.</li>
 	<li>Once you change files within a container, those files are persisted into a virtual block device and</li>
 	<li>at the moment that you want to commit this layer of changes, it pulls those changes out of the virtual block device and persists it on the right file system location of the container host.</li>
</ul>
</li>
 	<li>A last difference between the Linux and Windows container implementation is the concept of Hyper-V Containers</li>
</ul>
<h2 id="the-future-of-containers:ba85387dcdeb3e25471a63f45f6b923c">The Future of Containers</h2>
<ul>
 	<li>Google has contributed to container space by implementing cgroups and participating in libcontainer projects. Google may have gained a huge gain in performance, resource utilization, and overall efficiency using containers during past years.</li>
 	<li>Docker, Rocket, and other container platforms cannot run on a single host in a production environment, the reason is that they are exposed to single point of failure.</li>
 	<li>While a collection of containers are run on a single host, if the host fails, all the containers that run on that host will also fail. To avoid this, a <strong>container host cluster</strong> needs to be used.
<ul>
 	<li>Goolge implemented cutting edge, open source container cluster management system called <a href="http://kubernetes.io/" rel="nofollow">Kubernetes</a> in year 2014</li>
 	<li>Docker also started a solution called <a href="https://docs.docker.com/swarm/" rel="nofollow">Docker Swarm</a> in year 2015.</li>
</ul>
</li>
 	<li><a href="http://martinfowler.com/articles/microservices.html" rel="nofollow">Microservices</a> are another groundbreaking technology rather a software architecture which uses containers for their deployment.
<ul>
 	<li>A microservice is nothing new but a lightweight implementation of a web service which can start extremely fast compared to a standard web service.</li>
 	<li>This is done by packaging a unit of functionality (may be a single service/API method) in one service and embedding it into a lightweight web server binary.</li>
</ul>
</li>
</ul>
<h2>References</h2>
<ul>
 	<li>http://www.floydhilton.com/docker/2017/03/31/Docker-ContainerHost-vs-ContainerOS-Linux-Windows.html</li>
 	<li>https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/</li>
 	<li>http://blog.xebia.com/deep-dive-into-windows-server-containers-and-docker-part-2-underlying-implementation-of-windows-server-containers/</li>
 	<li>https://dzone.com/articles/evolution-of-linux-containers-future</li>
 	<li>https://www.slashroot.in/difference-between-hypervisor-virtualization-and-container-virtualization</li>
 	<li>https://www.infoworld.com/article/3204171/linux/what-is-docker-linux-containers-explained.html</li>
 	<li>https://blog.smartbear.com/web-monitoring/why-containers-instead-of-hypervisors/</li>
 	<li>https://www.brianchristner.io/docker-image-base-os-size-comparison/</li>
 	<li><a href="https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/">About windows containers</a></li>
 	<li><a href="http://blog.xebia.com/deep-dive-into-windows-server-containers-and-docker-part-2-underlying-implementation-of-windows-server-containers/">Deep dive into the implementation Windows Containers including multiple User Modes and “copy-on-write” to save resources</a></li>
 	<li><a href="https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/#the-copy-on-write-strategy">How Linux containers save resources by using “copy-on-write”</a></li>
 	<li>https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-overview</li>
</ul>
