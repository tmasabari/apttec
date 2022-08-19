---
layout: post
title: Refactor legacy code
date: 2018-10-27 07:27
author: tmasabari
comments: true
categories: [Uncategorized]
---
<div class="wp-block-image">
<figure class="aligncenter"><img class="wp-image-1763 aligncenter" src="/wp-content/uploads/2018/10/image-1.png" alt="" width="357" height="201" /></figure>
</div>
<p><!-- /wp:image --><!-- wp:list --></p>
<ul>
<li><strong>With refactoring, by definition, you don't change what your software does, you change how it does it.</strong></li>
<li>Whenever you have to make a change to legacy code (for a new feature or a bug fix), take the time to remove its legacy status.</li>
<li>Trying to pre-emptively update your existing legacy code is a <a href="http://en.wiktionary.org/wiki/fool%27s_errand#Noun">fool's errand</a>.</li>
</ul>
<p><!-- /wp:list --><!-- wp:heading {"level":3} --></p>
<h3>Approaches to refactor the code</h3>
<p><!-- /wp:heading --><!-- wp:list --></p>
<ul>
<li>For instance, that routine that's 1000 lines (I have a few that are over 5000), it is overly complex and is a piece of spaghetti. It would only (yet another four letter word) take a couple of days to re-factor it into a few 100 line routines and a few more 20 lines helpers, right? WRONG.</li>
<li>Hidden in those 1000 lines is 100 bug fixes, each one an undocumented user requirement or an obscure edge case. It's 1000 lines because the original 100-line routine did not do the job.</li>
<li>When it is broke, you need to be very careful when you fix it - as you make it better, that you don't accidentally change something else.</li>
<li>Note that "broke" may include code that is unmaintainable, but working correctly, that depends on the system and its use.</li>
<li>Ask "what happens if I screw this up and make it worse", because one day you will, and you will have to tell the bosses' boss why you chose to do that.</li>
<li>These systems can always be made better. You will have a budget to work to, a timeline, whatever. If you don't - go and make one.</li>
<li>Stop making it better when the money/time has run out. Add a feature, give yourself time to make it a little better. Fix a bug - again, spend a little extra time and make it better. </li>
</ul>
<p><!-- /wp:list --><!-- wp:paragraph --></p>
<p>The book is divided into three parts:</p>
<p><!-- /wp:paragraph --><!-- wp:list --></p>
<ul>
<li>an introductory part discussing the high-level mechanics of program change,</li>
<li>a sequence of chapters offering answers to commonly-encountered maintenance challenges (for example, "How Do I Add A Feature" or "I Need to Make a Change, but I Don't Know What Tests to Write"),</li>
<li>and a final part detailing 24 different refactorings that developers can use for breaking dependencies.</li>
</ul>
<p> </p>

<p><br /><br /><!--StartFragment--></p>
<h2>References</h2>
<p><!-- /wp:heading --><!-- wp:list --></p>
<ul>
<li><a href="https://softwareengineering.stackexchange.com/questions/122014/what-are-the-key-points-of-working-effectively-with-legacy-code/122024">https://softwareengineering.stackexchange.com/questions/122014/what-are-the-key-points-of-working-effectively-with-legacy-code/122024</a></li>
</ul>
<p><!--EndFragment--><br /><br /></p>
