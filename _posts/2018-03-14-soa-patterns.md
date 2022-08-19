---
layout: post
title: SOA Patterns
date: 2018-03-14 19:29
author: tmasabari
comments: true
categories: [Architecture, Design, Design, Patterns, Services, SOA]
---
GOF patterns for SOA

https://stackoverflow.com/questions/350404/how-do-the-proxy-decorator-adapter-and-bridge-patterns-differ?noredirect=1&amp;lq=1

&nbsp;

The three design patterns (Adapter, Facade and Bridge) all produce the result of a clean public API.

All four patterns have a lot in common, all four are sometimes informally called <strong>wrappers, or wrapper patterns.</strong>
<ol>
 	<li>All use composition, wrapping subject and</li>
 	<li>delegating the execution to the subject at some point,</li>
 	<li>do mapping one method call to another one.</li>
 	<li>They spare client the necessity of having to construct a different object and copy over all relevant data.</li>
 	<li>If used wisely, they save memory and processor.</li>
 	<li>By promoting loose coupling they make once stable code less exposed to inevitable changes and</li>
 	<li>better readable for fellow developers.</li>
</ol>
<h3>Comparison</h3>
[table id=12 /]

&nbsp;
