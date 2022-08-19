---
layout: post
title: PlantUML - N Tier architecture Diagram
date: 2018-04-16 14:07
author: tmasabari
comments: true
categories: [Architecture, Code, Design, PlantUML, UML]
---
<h2>1 Introduction</h2>
<ul>
 	<li>PlantUML is an open source tool that can create a variety of diagrams, including
sequence diagrams.</li>
 	<li>Each diagram is created from a set of instructions contained in a text file.</li>
 	<li>Anyeditor that does not introduce formatting characters (e.g., notepad, wordpad) may be used to create or edit the files.</li>
 	<li>.NET programmers can use VS Code with PlantUML plugin.</li>
 	<li>PlantUML can be downloaded at <a href="http://plantuml.sourceforge.net/index.html">http://plantuml.sourceforge.net/index.html</a></li>
</ul>
<h2>2. Quick reference</h2>
<ul>
 	<li>All frequently used symbols are documented in the page <a href="http://ogom.github.io/draw_uml/plantuml/" target="_blank" rel="nofollow noopener">http://ogom.github.io/draw_uml/plantuml/</a></li>
 	<li>PlantUML file contains processing instructions starting with @startuml on the first line and @enduml on the last line.</li>
 	<li>You can create a common theme file and include in your code files. <code>!include Theme.txt</code></li>
 	<li><b>Indentations, white spaces, line continuation</b>
<ul>
 	<li>PlantUML ignores blank lines and whitespace at the beginning of a line. Liberal use of whitespace to offset logical blocks in the text file can enhance readability.</li>
 	<li>Place backslash at the end of the line "\". Preprocessor will concatenate subsequent line to the current line</li>
</ul>
</li>
 	<li><strong>Comments</strong>
<ul>
 	<li>Comments can be included in the file by starting the line with a single quote (').</li>
 	<li>To put a comment on several lines you can start with /' and end the quote with '/
<ul>
 	<li><code>'This is a short comment
/' This is how you can
span multiple lines
of comments
'/ </code></li>
</ul>
</li>
</ul>
</li>
 	<li><strong>Declarations</strong>
<ul>
 	<li>Although PlantUML does not require you to define elements / interfaces / participants (i.e., entities), it is recommended best practice to define all participants together and before they are used.</li>
 	<li>If the element name is long or needs spaces, declare the participant using a short name and the display name. The short name can be used in diagram specific processing instructions.</li>
 	<li>To control the layout of the diagram, you can add spaces in the display name to better
position the participants.</li>
 	<li><code>participant POS as " POS "
participant OPT as " OPT "
participant LH as "Loyalty Host"</code></li>
</ul>
</li>
 	<li><strong>Notes</strong>
<ul>
 	<li>Text for notes can be split over multiple lines by inserting new lines (\n) into the note text. Alternatively, the keyword note may be used, followed by the note text on one or more lines, followed by keyword end note.</li>
 	<li><code>note right of OPT: right of OPT\non two lines
</code></li>
 	<li><code>note over POS
over POS
on two lines
end note</code></li>
 	<li>
<p id="QecsUuR"><img class="alignnone size-full wp-image-1468 " src="/wp-content/uploads/2018/04/img_5ad354ac6abbb.png" alt="" /></p>
</li>
</ul>
</li>
 	<li><strong>Splitting Diagrams</strong>
<ul>
 	<li>When a diagram is too long to fit on a page without losing readability, split it into one or more graphic files using the keyword <code>newpage</code>.</li>
 	<li>Each additional graphic file generated will have 00x appended (e.g., example.png, example_001.png, example_002.png).</li>
 	<li>Place a divider at the bottom of the first page and at the top of the second page to make it clear that the diagram is split.</li>
</ul>
</li>
</ul>
<h2>3. N Tier architecture Diagram</h2>
<ul>
 	<li>I created as typical N Tier architecture using PlantUML's diagram. Please find the code below.</li>
</ul>

[sourcecode]
@startuml MultiTierArchiteture

' Include section with id mail of PlantUMLTheme.pu
!include PlantUMLTheme.pu!theme

title
&amp;lt;u&amp;gt;Generic Multi Tier Architeture&amp;lt;/u&amp;gt;
end title

caption Prepared by Sabarinathan A.

/'
'When a line ends with a backslash, the preprocessor will merge the two lines.
'http://forum.plantuml.net/3104/sequence-diagram-messages-on-multiple-lines
Try to keep 2 items together, so they are at the same level in the diagram.
http://mrhaki.blogspot.in/2016/12/plantuml-pleasantness-keeping-elements.html
'/

Cloud &quot;External Consumers &amp;amp;lt;&amp;amp;amp;people&amp;amp;gt;&quot; {
actor Clients
[Identity Providers] &amp;amp;lt;&amp;amp;gt; as IdentityProvider
[Single Sign On Services] &amp;amp;lt;&amp;amp;gt; as SSOServer

}
Cloud &quot;Third Parties &amp;amp;lt;&amp;amp;amp;people&amp;amp;gt;&quot; {
[Third party application] &amp;amp;lt;&amp;amp;gt; as ThirdPartyApp
}

Folder N-TierArchitecture {
node &quot;UI Tier in DMZ&quot; {
[Front End Controllers] &amp;amp;lt;&amp;amp;gt; as UILayer
}
node &quot;Application Tier&quot; {
queue Messaging
[Core Business Logic] &amp;amp;lt;&amp;amp;gt; as BusinessServices
[UOW with Generic Repository] &amp;amp;lt;&amp;amp;gt; as DataAccessLayer
}

node &quot;Data Tier&quot; {
'[Cache] &amp;amp;lt;&amp;amp;gt; as CacheServer
Database CacheServer
Database OLTPDatabase

}
}
[Mail server] &amp;amp;lt;&amp;amp;gt; as Mail
[Remote Services] &amp;amp;lt;&amp;amp;gt; as ThirdPartyServices

note as ArchitectureNote
**N-Tier architecture**
*A layer is a reusable portion of code that performs a specific function.
*Each layer has specific function and interacts with only the layer directly below.
end note

note as BLLNote
**Patterns in Services and Business Layer**
* Facade - single point of entry - unified interface to a set of interfaces in a subsystem
*Factory: Define an interface for creating an object,
but let subclasses decide which class to instantiate.
Factory Method lets a class defer instantiation to subclasses.
* Dependency Injection DI - allows removing hard-coded dependencies
making it possible to change them, whether at run-time or compile-time.
* Strategy: Allow algorithm selection at runtime.
Encapsulate related algorithms and let the algorithm vary and evolve from the class using it.
Separate the implementation from the delivery of its results.
end note

note as DALNote
**Patterns in Data Access Layer**
* Unit Of Work (UoW) with Generic Repository
* CRUD Methods for domain objects Used in Data layer
* Alternative storage implementations may be easily interchanged.
end note
'================================

Clients --&amp;amp;gt; IdentityProvider
Clients --&amp;amp;gt; SSOServer
Clients ---&amp;amp;gt; UILayer : HTTP

IdentityProvider --&amp;amp;gt; UILayer
SSOServer --&amp;amp;gt; UILayer

ThirdPartyApp ---&amp;amp;gt; UILayer : HTTP

UILayer --&amp;amp;gt; Messaging : HTTP
Messaging -&amp;amp;gt; BusinessServices

BusinessServices --&amp;amp;gt; DataAccessLayer

DataAccessLayer &amp;amp;lt;-- CacheServer
CacheServer &amp;amp;lt;-- OLTPDatabase 'http://mrhaki.blogspot.in/2017/10/plantuml-pleasantness-align-multi-line.html '\n \l \r for left and right alignments DataAccessLayer ---&amp;amp;gt; OLTPDatabase

BusinessServices ----&amp;amp;gt; Mail
BusinessServices ----&amp;amp;gt; ThirdPartyServices

ArchitectureNote . UILayer
BLLNote . BusinessServices
DALNote . DataAccessLayer

@enduml
[/sourcecode]

<h2>3. UML Diagram Output</h2>
<p id="hLidoyH"><img class="size-full wp-image-1484 aligncenter" src="/wp-content/uploads/2018/04/img_5ad461832b410.png" alt="" /></p>
