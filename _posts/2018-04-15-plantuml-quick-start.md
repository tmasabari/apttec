---
layout: post
title: PlantUML - Quick Start
date: 2018-04-15 19:17
author: tmasabari
comments: true
categories: [Architecture, Design, PlantUML, UML]
---
<h2>1 Introduction</h2>
<ul>
 	<li>PlantUML is an open source tool that can create a variety of diagrams, including
sequence diagrams.</li>
 	<li>Each sequence diagram is created from a set of instructions contained in a text file. Any
editor that does not introduce formatting characters (e.g., notepad, wordpad) may be
used to create or edit the files. Most useful tools is VS Code.</li>
 	<li>Each sequence diagram will have its own text file. PlantUML creates corresponding graphic file(s) based on the instructions found in the text file.</li>
 	<li>Requirements</li>
 	<li>The only requirement to run PlantUML is to have a<a href="https://java.com/en/"> Java Runtime Environment (JRE)</a>
installed on your PC.</li>
 	<li>PlantUML can be downloaded at: http://plantuml.sourceforge.net/index.html</li>
 	<li>Download the latest compiled jar file as well as the reference manual to a folder of your
choosing on your PC.</li>
</ul>
<h2>2 PlantUML Text File</h2>
<ul>
 	<li>This file contains processing instructions starting with @startuml on the first line and @enduml on the last line.</li>
 	<li>These instructions are in theme file can be included in your sequence diagrams text file using the instruction: <code>!include ConexxusSkinParam.txt</code></li>
 	<li>
<h3>Formattings</h3>
<ul>
 	<li>PlantUML ignores blank lines and whitespace at the beginning of a line. Liberal use of whitespace to offset logical blocks in the text file can enhance readability.</li>
</ul>
</li>
 	<li>
<h3>Comments</h3>
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
 	<li></li>
</ul>
<h2>3 Theme File</h2>
<ul>
 	<li>So that all sequence diagrams are consistent, use PlantUML defaults along with the instructions:</li>
</ul>
<h2>4 Diagramming - General</h2>
<ul>
 	<li>
<h3>Sections</h3>
<ul>
 	<li>Title
<ul>
 	<li>
<table>
<tbody>
<tr>
<th>keyword</th>
<th>usage</th>
<th>image</th>
</tr>
<tr>
<td><code class="highlighter-rouge">title</code></td>
<td>Title</td>
<td><img src="http://ogom.github.io/draw_uml/assets/img/diagrams/parts/title.png" alt="parts_usecase" /></td>
</tr>
</tbody>
</table>
</li>
</ul>
</li>
</ul>
</li>
 	<li>
<h3>Declarations</h3>
<ul>
 	<li>Although PlantUML does not require you to define interfaces / participants (i.e., entities), it is recommended best practice to define all participants together and before they are used.</li>
 	<li>If the participant name is long or needs spaces, declare the participant using a short name and the display name. The short name can be used in diagram specific processing instructions.</li>
 	<li>To control the layout of the diagram, you can add spaces in the display name to better
position the participants.</li>
 	<li><code>participant POS as " POS "
participant OPT as " OPT "
participant LH as "Loyalty Host"</code></li>
</ul>
</li>
 	<li>
<h3>Notes</h3>
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
 	<li>
<h3>Dividers</h3>
<ol>
 	<li>Use a divider to separate a sequence diagram into logical or functional sections. A divider is specified by <code>“==”</code> on both sides of the text to display.</li>
 	<li><strong>Splitting Diagrams</strong>
<ul>
 	<li>When a sequence diagram is too long to fit on a page without losing readability, split it into one or more graphic files using the keyword <code>newpage</code>.</li>
 	<li>Each additional graphic file generated will have 00x appended (e.g., example.png, example_001.png, example_002.png).</li>
 	<li>Place a divider at the bottom of the first page and at the top of the second page to make it clear that the diagram is split.</li>
</ul>
</li>
 	<li>If whitespace between messages is required in the diagram, use one or more <code>"|||"</code>.</li>
</ol>
</li>
</ul>
<h3>5 Diagramming - Sequence</h3>
<ul>
 	<li>Represent the messages and orders of the interacts.
<table>
<thead>
<tr>
<th>keyword</th>
<th>usage</th>
<th>image</th>
</tr>
</thead>
<tbody>
<tr>
<td><code class="highlighter-rouge">-&gt;</code></td>
<td>Message</td>
<td><img src="http://ogom.github.io/draw_uml/assets/img/diagrams/parts/message_line.png" alt="parts_usecase" /></td>
</tr>
<tr>
<td><code class="highlighter-rouge">&lt;--</code></td>
<td>Return</td>
<td><img src="http://ogom.github.io/draw_uml/assets/img/diagrams/parts/return_line.png" alt="parts_usecase" /></td>
</tr>
</tbody>
</table>
</li>
 	<li>
<h3>Messages</h3>
<ul>
 	<li>Messages between participants are specified by defining the two participants,
<ul>
 	<li>the direction,</li>
 	<li>the line type, and</li>
 	<li>the corresponding text to display above the message.</li>
</ul>
</li>
 	<li><strong>Mandatory messages</strong> are rendered with solid lines, indicated in the instructions by “-&gt;”.</li>
 	<li><strong>Optional steps</strong> are rendered with dashed lines, indicated in the instruction by “--&gt;”.</li>
</ul>
</li>
 	<li>
<h3>Lifelines</h3>
<ul>
 	<li>Use the keywords activate and deactivate to control the lifeline of a participant.</li>
 	<li>The lifeline should be inactive (will be shown as dashed) when not in use.</li>
 	<li>These keywords act on the previous message. Therefore place the activate keyword after the message that starts the lifeline and the deactivate keyword after the message the ends the lifeline.</li>
 	<li>Messages normally connect two (and only two) participants. Messages should not pass through another active participant.</li>
</ul>
</li>
 	<li>
<h3>Groupings</h3>
<ul>
 	<li>Messages can be grouped together in a box by using the keyword group, specifying the text to include in the grouping, ending with the keyword end. The explanation can be formatted to force a new line with ‘\n’.</li>
 	<li>
<p id="nIxTjae"><img class="alignnone size-full wp-image-1470 " src="/wp-content/uploads/2018/04/img_5ad357c641415.png" alt="" /></p>
</li>
</ul>
</li>
 	<li>
<h3>Vertical boxes</h3>
<ul>
 	<li>Participants may be grouped together in a vertical box to draw attention to functionality,
purpose or architectural considerations. Use the keywords box and end box in the
participant declarations to define where the box should be drawn.</li>
 	<li><code>box "B and C may be integrated into \n one device"
participant B as " B "
participant C as " C "
end box
participant D as " D "</code></li>
</ul>
</li>
</ul>
<h2>References</h2>
<ul>
 	<li>https://www.conexxus.org/sites/default/files/UsingPlantUML.pdf</li>
</ul>
