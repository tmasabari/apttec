---
layout: post
title: Automate MS Office documents using OpenXML
date: 2019-12-20 20:34
author: tmasabari
comments: true
categories: [Office Automation, Uncategorized]
---
<!-- wp:paragraph -->
<p>What is OpenXML SDK?</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>OpenXML SDK is a simple .NET dll file and associated XML document.</li><li>' The Open XML SDK 2.5 Productivity Tool for Microsoft Office' is a .NET GUI application to view the document contents in tree structure and generate the code based upon contents.<ul><li> Automatically generate Open XML SDK code based on document content. User will be able to directly copy, compile and run the code to re-generate the same document or specific parts of the documents.</li><li>Compare two documents and list the differences in the document part structure as well as the content difference inside the parts.</li><li>Automatically generate Open XML SDK code based on the content differences between two documents. User will be able to copy, compile and run the code on the source document to generate the target document.</li><li>Validate a document, part of a document or a segment of content inside a part against Office 2007, Office 2010, or Office 2013</li><li>Provide documentations on the following:Open XML SDK Reference</li><li>ECMA376 v1 Open XML File Formats standard</li><li>Microsoft Office implementation notes (which document the implementer notes between the ECMA376 v1 and Microsoft Office 2007 SP2 implementation) </li></ul></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>The  ' The Open XML SDK 2.5 Productivity Tool' can open below following types of documents:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Word documents: .docx, .docm, .dotx, .dotm</li><li>Excel documents: .xlsx, .xlsm, .xltx, .xltm</li><li>Powerpoint documents: .pptx, .pptm, .potx, .potm</li></ul>
<!-- /wp:list -->

<!-- wp:image {"id":1908,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="/wp-content/uploads/2019/12/OpenXML-SDK-Developer-Tool.png" alt="" class="wp-image-1908"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>The .docx files are simple zip files. You can just rename the file to .zip extension and unzip the file to view the folders and files.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>In order to mail merge the data to the document, the code has to replace the mailmerge fields with actual data. The sample difference between the original document and the merged document is as shown below.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1910,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="/wp-content/uploads/2019/12/image-1.png" alt="" class="wp-image-1910"/></figure>
<!-- /wp:image -->

<!-- wp:list -->
<ul><li>Merge fields contains list of fldchar tags.</li><li>Starts with fldchar tag with attribute type="begin".</li><li>It can contain multiple  fldchar tag with attribute type ="preserve". The combined text will provide the meta data information of the field.</li><li>In between separate and end, list of field codes which has text.</li><li>Ends with fldchar tag with attribute type="end".</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>In order to mail merge, just remove all these fields and insert a new text filed with the data from the database.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I will explain the code in subsequent posts.</p>
<!-- /wp:paragraph -->
