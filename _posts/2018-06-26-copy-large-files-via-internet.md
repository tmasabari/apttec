---
layout: post
title: Copy large files via Internet
date: 2018-06-26 17:10
author: tmasabari
comments: true
categories: [Tips and Tricks]
---
<p style="text-align: justify;">Recently, while copying large files to SharePoint document library via Internet I ran into the issue "The semaphore timeout period has expired". You find more details about this issue in the <a href="https://www.easeus.com/storage-media-recovery/the-semaphore-timeout-period-has-expired.html" target="_blank" rel="nofollow noopener">link</a>.</p>
<p style="text-align: justify;">One possible solution is to compress the files and split them up to the size as per the limitation of the network bandwidth. We can easily achieve this via the 7Zip tool.</p>
Follow below steps and utilities to copy the large files over Internet.
<ul style="text-align: justify;">
 	<li>Install 7 zip utility</li>
 	<li>Copy your files to a folder and move to the folder using the CD command</li>
 	<li>Use below command to compress the files individually using ultra compression method and split the files upto 50 MB in length
FOR %i IN (*.*) DO "C:\Program Files\7-Zip\7z.exe" a "%~ni.7z" "%i" -m0=lzma2 -mx=9 -aoa -v50m</li>
 	<li>Following portion of the command takes all files in the current directory and compresses them individually
FOR %i IN (*.*) DO "C:\Program Files\7-Zip\7z.exe" a "%~ni.7z" "%i"</li>
 	<li>Following portion of the command uses ultra compression level and lzma2 method (-m0=lzma2 -mx=9 -aoa )</li>
 	<li>Following portion of the command splits the file to 50 MB chunks. (-v50m)</li>
 	<li>RoboCopy is the tool to copy files between different drives with a lot of failover options. You can find more details in <a href="https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy" target="_blank" rel="nofollow noopener">link</a>. You can download the GUI tool from <a href="http://www.upway2late.com/#/downloads" target="_blank" rel="nofollow noopener">here</a>.</li>
 	<li>You can map the Sharepoint folder to your local drive. Please find more details in this <a href="https://bitwizards.com/Thought-Leadership/Blog/2015/December-2015/How-to-Map-SharePoint-Document-Libraries-as-Networ" target="_blank" rel="nofollow noopener">link</a>.</li>
 	<li>Use RoboCopy to copy the files from</li>
</ul>
<p style="text-align: justify;"></p>

<h2 style="text-align: justify;"><strong>References</strong></h2>
<ul style="text-align: justify;">
 	<li><a href="https://superuser.com/questions/311937/how-do-i-create-separate-zip-files-for-each-selected-file-directory-in-7zip" target="_blank" rel="nofollow noopener">https://superuser.com/questions/311937/how-do-i-create-separate-zip-files-for-each-selected-file-directory-in-7zip</a></li>
 	<li><a href="https://www.easeus.com/storage-media-recovery/the-semaphore-timeout-period-has-expired.html" target="_blank" rel="nofollow noopener">https://www.easeus.com/storage-media-recovery/the-semaphore-timeout-period-has-expired.html</a></li>
 	<li><a href="https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy" target="_blank" rel="nofollow noopener">https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy</a></li>
 	<li><a href="http://www.upway2late.com/#/downloads" target="_blank" rel="nofollow noopener">http://www.upway2late.com/#/downloads</a></li>
 	<li><a href="https://bitwizards.com/Thought-Leadership/Blog/2015/December-2015/How-to-Map-SharePoint-Document-Libraries-as-Networ" target="_blank" rel="nofollow noopener">https://bitwizards.com/Thought-Leadership/Blog/2015/December-2015/How-to-Map-SharePoint-Document-Libraries-as-Networ</a></li>
</ul>
<p style="text-align: justify;"></p>
