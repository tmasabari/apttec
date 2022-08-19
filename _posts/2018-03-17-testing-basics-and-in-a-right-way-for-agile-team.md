---
layout: post
title: Testing basics and  IN A RIGHT WAY for agile team
date: 2018-03-17 10:51
author: tmasabari
comments: true
categories: [agile testing, Testing, Unit Test, Unit Test]
---
<h3>Type of testing</h3>
<ul>
 	<li><strong>Unit Testing- </strong>To focus on one unit of code, usually a class or a method</li>
 	<li><strong>Integration Testing-</strong>Integration Testing is when a program accesses an external resource to confirm that the code is functioning properly (i.e. database calls or loading a file). <strong>If you are making database calls in your unit tests, then they aren't called unit tests...they are integration tests</strong>.</li>
 	<li><strong>Regression Testing- </strong>Regression testing is finding defects after a major code change has occurred. Those old unit tests may need refactored to match the new code. Of course, if it is new code, I could almost guarantee that at least 25-50% of your unit test code would fail (considering it's a major change to your code base).</li>
 	<li><strong>Load Testing-</strong>load testing is primarily concerned with how well the system runs under a specific load of users or large amounts of data.</li>
</ul>
Here are three of the most common types of automated tests:
<ol>
 	<li>· <b>Unit tests</b>: A single piece of code (usually an object or a function) is tested, isolated from other pieces</li>
 	<li>· <b>Integration tests</b>: Multiple pieces are tested together, for example testing database access code against a test database</li>
 	<li>· <b>Acceptance tests (also called Functional tests)</b>: Automatic testing of the entire application, for example using a tool like Selenium to automatically run a browser.</li>
</ol>
<h3>Testing</h3>
<ul>
 	<li>Often new programmers don’t understand testing. They don’t think it necessary and most developers have no clue about how testing is actually done</li>
 	<li><strong>Testing, at its core, is really about reducing risk.</strong></li>
 	<li>The goal of testing software is <span style="color: #339966;">not to find bugs or to make software better</span>. It’s to reduce the risk by proactively finding and helping to eliminate problems which would most greatly impact the customer using the software.</li>
 	<li><strong>you can never find <em>all</em> the bugs or defects in a piece of software and you can never test <em>every</em> possible input into the software.</strong> (For any non-trivial application.)</li>
 	<li>So, the idea is not to find every single possible thing that is wrong, or even to verify the software against a spec—as some people like to define software testing—because both are impossible.</li>
 	<li>Impact can happen with the frequency of an error or undesired functionality, or it can be because of the severity of the problem.</li>
 	<li>Typically this is achieved by first prioritizing what areas of the software are likely to have the biggest impact (i.e. risk), and then deciding on a set of tests to run which verify the desired functionality.</li>
 	<li>When the actual functionality deviates from the desired functionality, a defect is usually logged and those defects are prioritized based on severity.</li>
</ul>
<h3>Black box testing</h3>
Black box testing is simply <strong>testing as if the software itself was a black box.</strong>

When you do black box testing, you are only concerned with inputs and outputs. You don’t care how the actual outputs are derived. You don’t know anything about the code or how it works.
<h3>White box testing</h3>
With white box testing, you have at least some idea of what is going on inside the software.  <a href="https://simpleprogrammer.com/2010/10/15/the-purpose-of-unit-testing/">Unit testing is not testing at all</a>

Instead <strong>real white box testing is when you understand some of the internals of the system and perhaps have access to the actual source code</strong>, which you use to inform your testing and what you target.

&nbsp;
<h1>Testing in a right way</h1>
WHAT do they test? In my experience, it’s all about avoiding bugs: validation of input data, successful registration process, whether all links work or not, etc. In other words, if it doesn’t cause a bug or exception, we’re good to go.

However, that’s not enough. It’s too narrow. You need to take things a step further into the business world.

In addition to making something work, developers also need to <span style="color: #339966;">test whether that function is actually being used</span>. For that, you usually need to set up some kind of analytics or event tracking system to monitor the usage after the launch. Be prepared to change the functionality or even remove it. After all, that <strong><span style="color: #339966;">extra code is pointless if your client doesn’t employ it</span></strong>, so it’s wise not to get attached.

Also, while testing before the launch, look for the logical errors.
<ul>
 	<li>What doesn’t make sense or is hard to use?</li>
 	<li>What could potentially cause users to not use the function?</li>
 	<li>Too many fields to fill?</li>
 	<li>A too clunky menu navigation?</li>
 	<li>Some buttons missing?</li>
</ul>
Of course, to be able to think in that direction, you need to do extra homework on the business context. Dig a little deeper into the product and its goals, have a few conversations asking client “why,” and possibly even read some articles or books on the subject.

Quite often, it seems that developers see business people as their enemies. Project managers, clients, marketing department, sales people—even if they all work in the same company—there’s a silent war going on.

Usually you can feel it by hearing phrases like:
<ul>
 	<li>“…they’re stupid and constantly changing demands…”</li>
 	<li>“…meeting again? <a href="https://twitter.com/raganwald/status/794527181225357312">They don’t let me do my job!</a>“</li>
 	<li>“…they think it’s a five-minute change, they have no idea…”</li>
 	<li>“…I don’t know how long it will take. It’s done as soon as it’s done…”</li>
</ul>
In reality, the development team and the marketing team should act as one team with a common goal. They should help each other by discussing situations instead of blaming each other.

In my experience, if the project grows to the point of dealing with optimization issues, by that point the client will have a lot of clients, their feedback, analytics numbers, and usually <strong>a new vision</strong> for the next step of growth. Quite often, that means re-creating the project from scratch, not because of those performance issues, but because of business reasons—different functionality, pivoted pricing model, new design, etc
