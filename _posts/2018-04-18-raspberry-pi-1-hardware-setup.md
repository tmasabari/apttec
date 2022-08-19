---
layout: post
title: Raspberry Pi 1 : Hardware Setup
date: 2018-04-18 08:15
author: tmasabari
comments: true
categories: [Uncategorized]
---
This series of article is for the software engineers who are also interested in electronics/robotics.
<p id="ufvttOB"><img class="size-full wp-image-1494 alignleft" src="/wp-content/uploads/2018/04/img_5ad6b494c1a7c.png" alt="" /></p>
<a href="https://en.wikipedia.org/wiki/Raspberry_Pi" target="_blank" rel="nofollow noopener">Raspberry Pi</a> is the credit card size computer. We may compare it with P3 , 512 MB desktop PC system box. Few people use it as a standalone server or computer. You may find some of the uses in the following <a href="http://www.magnatecha.com/things-i-do-with-my-raspberry-pi/" target="_blank" rel="nofollow noopener">link</a>. I connected my external hard disk to it and I’m using it as a <a href="http://simonthepiman.com/how_to_setup_windows_file_server.php" target="_blank" rel="nofollow noopener">file server</a> for my laptop and other PCs.

As a software engineer, my plan is to use Raspberry Pi to code high level language to learn, create and control the basic electronic/digital/robotic circuits via GPIO interface in the shortest period of time.

In order to get started with the Raspberry Pi, please purchase Raspberry Pi Model B. People from Tamilnadu, India can order from <a href="http://www.simplelabs.co.in/" target="_blank" rel="nofollow noopener">Simple Labs</a> (and for me they delivered within 24 hours even to the remote location in Tamilnadu).

Price of Raspberry Pi in India as of 19<sup>th</sup> September 2013 is:
<ul>
 	<li><strong>RASPBERRY PI – MODEL B – 512MB – Rs.3,465.00</strong> (with free GPIO cable)</li>
 	<li><strong>Low Cost Case for Raspberry Pi – Rs.262.50</strong></li>
</ul>
As I have a laptop, I planned to use it as <a href="http://www.penguintutor.com/linux/raspberrypi-headless" target="_blank" rel="nofollow noopener">headless device</a> (means using it with remote desktop, without separate monitor, keyboard, mouse). Even for that, you may need to purchase additional components, wires and connectors.
<ol>
 	<li>SDHC memory card or Micro SD card with adapter (4 GB min/32 GB Max). Please ensure that card is of Class 10 type. As memory card will be used as permanent storage, Class 10 is essential to achieve high disk I/O performance. Cheap Class 4 type card will degrade the disk I/O performance.
<p id="RYRIEep"><img class="size-full wp-image-1496 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b4ad51d7f.png" alt="" /></p>
</li>
 	<li>5 V 2 Amp DC adapter (1 Amp is also OK)
<ul>
 	<li>All recent model mobile phones comes with micro USB male adapter. Please check the Ampere rating, it should be at least 1 Amp(otherwise in peak power consumption, Raspberry Pi may restart)
<p id="ioINWXg"><img class="size-full wp-image-1497 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b4c430f54.png" alt="" /></p>
</li>
 	<li>You may connect the board to normal PC/laptop via USB to micro USB cable also. But your PC/laptop should support power ratings as mentioned earlier.
<p id="TOCssHh"><img class="size-full wp-image-1498 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b4d6ac9c3.png" alt="" /></p>
</li>
</ul>
</li>
 	<li>RJ 45 network cable to connect with Laptop/PC/Hub/Switch:
<p id="vKFaegK"><img class="size-full wp-image-1499 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b4ebb0c44.png" alt="" /></p>
</li>
 	<li>(optional) Normal mobile earphone to listen to audio from raspberry:
<p id="YiKAHgh"><img class="size-full wp-image-1500 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b4f8671dc.png" alt="" /></p>
</li>
</ol>
Connecting the wires/components is a straight forward process. If you need detailed description, please check the following references:
<ol>
 	<li><a title="RPi Hardware Basic Setup" href="http://elinux.org/RPi_Hardware_Basic_Setup" target="_blank" rel="nofollow noopener">RPi Hardware Basic Setup</a></li>
 	<li><a title="FAQs" href="http://www.raspberrypi.org/faqs" target="_blank" rel="nofollow noopener">FAQs</a></li>
</ol>
<h4>Assembling the Case</h4>
&nbsp;
<p id="XQrOzHg"><img class="size-full wp-image-1502 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b512e1fef.png" alt="" /></p>
&nbsp;

<strong>Raspberry Pi Ports</strong>

<img class="size-full wp-image-1501 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b506c560e.png" alt="" />

<strong>Assembled Raspberry Pi</strong>
<p id="YSjoZRl"><img class="size-full wp-image-1503 aligncenter" src="/wp-content/uploads/2018/04/img_5ad6b523acf57.png" alt="" /></p>
The next part in this series will be installing the OS. Meanwhile, please check <a href="http://www.youtube.com/embed/prSRAzmaIAY?version=3&amp;rel=1&amp;fs=1&amp;showsearch=0&amp;showinfo=1&amp;iv_load_policy=1&amp;wmode=transparent">the video of Hello World output</a> from Raspberry Pi GPIO using C Language.
