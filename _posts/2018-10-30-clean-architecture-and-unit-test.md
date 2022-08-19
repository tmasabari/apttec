---
layout: post
title: Clean architecture and Unit test
date: 2018-10-30 20:23
author: tmasabari
comments: true
categories: [Architecture, Architecture, clean, Clean architecture, Clean architecture, Testing, Todo, todo, Unit Test, Unit Test]
---
<!-- wp:heading -->
<h2>Todo: Must read and refactor</h2>
<ol>
<li><a href="https://github.com/thangchung/blog-core">https://github.com/thangchung/blog-core</a></li>
<li><a href="https://gist.github.com/ygrenzinger/14812a56b9221c9feca0b3621518635b">https://gist.github.com/ygrenzinger/14812a56b9221c9feca0b3621518635b</a></li>
<li><a href="https://gist.github.com/ygrenzinger/14812a56b9221c9feca0b3621518635b">https://gist.github.com/ygrenzinger/14812a56b9221c9feca0b3621518635b</a></li>
</ol>
<h2>Need</h2>
<ul>
<li><strong>Separation of Concerns:</strong> Avoid mixing different code responsibilities in the same (method | class | project). The Big Three<br />§Data Access<br />§Business Rules and Domain Model<br />§User Interface</li>
<li><strong>Single Responsibility Principle</strong>
<ul>
<li>Classes should focus on a single responsibility – a single reason to change.</li>
<li>Works in tandem with Separation of Concerns</li>
</ul>
</li>
<li><strong>Don’t Repeat Yourself</strong>
<ul>
<li>§Refactor repetitive code into functions</li>
<li>§Group functions into cohesive classes</li>
<li>§Group classes into folders and namespaces by
<ul>
<li>§ Responsibility</li>
<li>§ Level of abstraction § Etc.</li>
</ul>
</li>
<li>§ Further group class folders into projects</li>
</ul>
</li>
<li><strong>Dependencies</strong>
<ul>
<li><strong>Invert (and inject) Dependencies: </strong>Both high level classes and implementation-detail classes should depend on <strong>abstractions (interfaces).</strong></li>
<li>Classes should follow <strong>Explicit Dependencies Principle</strong>: Request all dependencies via their constructor.</li>
<li>Corollary: <strong>Abstractions/interfaces must be defined somewhere accessible by:</strong><br />§ Low level implementation services<br />§ High level business services<br />§ User interface entry points</li>
</ul>
</li>
<li>Make the right thing easy and the wrong thing hard.
<ul>
<li>UI classes shouldn’t depend directly on infrastructure classes<br /> How can we structure our solution to help enforce this?</li>
<li>Business/domain classes shouldn’t depend directly on infrastructure classes<br /> How can our solution design help?</li>
<li>Repetition of (query logic, validation logic, policies, error handling, anything) is a problem<br /> What patterns can we apply to make avoiding repetition easier than<br />copy/pasting?</li>
</ul>
</li>
</ul>
<h2>N Tier Architecture and transitive dependency</h2>
<p><img class="wp-image-1836  alignleft" src="/wp-content/uploads/2018/10/img_5bd992ed579f0.png" alt="" width="392" height="243" /></p>
<p id="SvvDWvB"><img class="alignnone  wp-image-1837 " src="/wp-content/uploads/2018/10/img_5bd9934dd5aae.png" alt="" width="222" height="156" /></p>
<p>Transitive dependencies</p>
<h2> </h2>
<h2>Clean Architecture</h2>
<p id="ARYrEoL"><img class="wp-image-1828  aligncenter" src="/wp-content/uploads/2018/10/img_5bd871bcca11b.png" alt="" width="451" height="222" /></p>
<h3>Rules</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>The Application <strong>Core</strong> contains the Domain Model</li>
<li>All projects depend on the Core project; dependencies point inward toward this core</li>
<li>Inner projects define interfaces; outer projects implement them</li>
<li><strong>Avoid</strong> direct dependency on <strong>Infrastructure</strong> project (except from Integration tests)</li>
</ul>
<h3>Features</h3>
<ul>
<li>Database Independent
<ul>
<li>The vast majority of the code has no knowledge of what database, if any, might be used by the application.</li>
<li>Often, this knowledge will exist in a single class, in a single project that no other project references.</li>
</ul>
</li>
<li>UI Independent
<ul>
<li>Only the UI project cares about the UI. The rest of the system is UI-agnostic.</li>
</ul>
</li>
<li>Testable
<ul>
<li>Apps built using this approach, and especially the core domain model and its business rules, are extremely testable.</li>
</ul>
</li>
<li>Framework Independent.
<ul>
<li> You can use this architecture with ASP.NET (Core), Java, Python, etc. It doesn’t rely on any software library or proprietary code base.</li>
</ul>
</li>
</ul>
<h2>Core &amp; Domain Model vs Business logic</h2>
<ul>
<li>Not just “business logic”</li>
<li>A model of the problem space composed of Entities, Interfaces, Services, and more.</li>
<li>Interfaces define contracts for working with domain objects</li>
<li>Everything in the application (including infrastructure and data access) depends on these i<strong>nterfaces and domain objects</strong></li>
</ul>
<p>&nbsp;</p>
<p id="TLGQcay"><img class="wp-image-1831  aligncenter" src="/wp-content/uploads/2018/10/img_5bd8768b630ed.png" alt="" width="419" height="218" /></p>
<p id="qjzKHaB"><img class="wp-image-1832  aligncenter" src="/wp-content/uploads/2018/10/img_5bd876a74a01e.png" alt="" width="467" height="224" /></p>
<p id="CCJrmrx"><img class="wp-image-1833  aligncenter" src="/wp-content/uploads/2018/10/img_5bd876c9bd164.png" alt="" width="469" height="226" /></p>
<p id="leHHCQk"><img class="wp-image-1830  aligncenter" src="/wp-content/uploads/2018/10/img_5bd87635d5290.png" alt="" width="468" height="281" /></p>
<p>Nuget Package: Ardalis.GuardClauses (<a href="https://github.com/ardalis/GuardClauses">https://github.com/ardalis/GuardClauses</a>)</p>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Features</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li>Framework Independent.◦ You can use this architecture with ASP.NET (Core), Java, Python, etc. It doesn’t rely on any software library or proprietary code base.</li>
<li>Database Independent◦ The vast majority of the code has no knowledge of what database, if any, might be used by the application. Often, this knowledge will exist in a single class, in a single project that no other project references.</li>
<li>UI Independent◦ Only the UI project cares about the UI. The rest of the system is UI-agnostic.</li>
<li>Testable◦ Apps built using this approach, and especially the core domain model and its business rules, are extremely testable.</li>
</ul>
<p><img class="wp-image-1825  aligncenter" src="/wp-content/uploads/2018/10/img_5bd8711787dc9.png" alt="" width="518" height="380" /></p>
<p><img class="wp-image-1827  aligncenter" src="/wp-content/uploads/2018/10/img_5bd8717a52e82.png" alt="" width="415" height="258" /></p>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>References</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul>
<li><a href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html</a></li>
<li>Template code <a href="https://github.com/ardalis/CleanArchitecture">https://github.com/ardalis/CleanArchitecture</a></li>
<li>Detailed architecture PDF <a href="https://devintxcontent.blob.core.windows.net/showcontent/Speaker%20Presentations%20Fall%202017/Clean%20Architecture%20with%20ASP.NET%20Core.pdf">https://devintxcontent.blob.core.windows.net/showcontent/Speaker%20Presentations%20Fall%202017/Clean%20Architecture%20with%20ASP.NET%20Core.pdf</a></li>
<li>Yet to read</li>
<li>.net core <a href="https://paulovich.net/2018/05/15/clean-architecture-for-net-applications/">https://paulovich.net/2018/05/15/clean-architecture-for-net-applications/</a></li>
<li><a href="https://fullstackmark.com/post/18/building-aspnet-core-web-apis-with-clean-architecture">https://fullstackmark.com/post/18/building-aspnet-core-web-apis-with-clean-architecture</a></li>
</ul>
<!-- /wp:list -->
