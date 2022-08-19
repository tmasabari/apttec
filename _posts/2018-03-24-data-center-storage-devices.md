---
layout: post
title: Data center physical storage devices
date: 2018-03-24 12:17
author: tmasabari
comments: true
categories: [Hardware, Storage]
---
<ol>
 	<li>Types of physical storage devices in data centers
<ol>
 	<li>Direct Attached Storage (DAS) - hard disks</li>
 	<li>Network Attached Storage (NAS)</li>
 	<li>Storage Area Network (SAN)</li>
</ol>
</li>
 	<li>A <strong>block device</strong> is a handle to the raw disk. /dev/sda</li>
 	<li>A <strong>filesystem</strong> is layered on top of the block device in order to store data. You can then mount this. <code>mount /dev/sda1 /mnt/somepath</code>.</li>
 	<li><strong>DAS</strong> is a block device from a disk which is physically [directly] attached to the host machine.
<ul>
 	<li>You must place a filesystem upon it before it can be used.</li>
 	<li>Technologies to do this include IDE, SCSI, SATA, etc.</li>
</ul>
</li>
 	<li><strong>SAN</strong> is a block device which is delivered over the network.
<ol>
 	<li>Virtually any low level protocol can be encapsulated into network packets and sent remotely to allow to access the hard disk as it was connected locally. Then you can read your data by block numbers or simply create a file-system on the new block device.</li>
 	<li>Like DAS you must still place a filesystem upon it before it can used.</li>
 	<li>Technologies to do this include FibreChannel, iSCSI, FoE, etc.</li>
</ol>
</li>
 	<li><strong>NAS</strong> is a filesystem delivered over the network.
<ul>
 	<li>It is ready to mount and use.</li>
 	<li>Technologies to do this include NFS , DOS/Windows - CIFS/aka.SMB, Apple - AFP etc.</li>
 	<li>All of this interfaces explicitly prohibit remote lookups of block addresses (for security reasons first) and normally such interfaces are not even implemented.</li>
 	<li>The system on which these are mounted does not see them as local storage, it sees them as network storage. This is important because many programs will not allow the use of network storage for various things.</li>
</ul>
</li>
 	<li>
<p id="ruomqBN"><img class="alignnone wp-image-1048 " src="/wp-content/uploads/2018/03/img_5aad26e259e06.png" alt="" width="272" height="318" /></p>
</li>
 	<li>
<p id="DysmydS"><img class="alignnone size-full wp-image-1050 " src="/wp-content/uploads/2018/03/img_5aad2848b35b8.png" alt="" /></p>
</li>
 	<li>http://www.rfwireless-world.com/Terminology/difference-between-DAS-NAS-and-SAN.html
<table>
<tbody>
<tr>
<th><b>feature</b></th>
<th><b>DAS</b></th>
<th><b>NAS</b></th>
<th><b>SAN</b></th>
</tr>
<tr>
<td>Full Name</td>
<td>Direct Access Storage</td>
<td>Network Attached Storage</td>
<td>Storage Area Network</td>
</tr>
<tr>
<td>Storage type</td>
<td>Sectors</td>
<td>Shared files</td>
<td>Blocks</td>
</tr>
<tr>
<td>Data Transmission</td>
<td>IDE/SCSI</td>
<td>TCP/IP, Ethernet</td>
<td>Fiber Channel, IP</td>
</tr>
<tr>
<td>Access Mode</td>
<td>Clients or servers</td>
<td>Clients or servers</td>
<td>Servers</td>
</tr>
<tr>
<td>Capacity in Bytes</td>
<td>10<sup>9</sup></td>
<td>10<sup>9</sup> to 10<sup>12</sup></td>
<td>&gt; 10<sup>12</sup></td>
</tr>
<tr>
<td>Complexity</td>
<td>Easy</td>
<td>Moderate</td>
<td>Difficult</td>
</tr>
<tr>
<td>Management cost (per GB)</td>
<td>High</td>
<td>Moderate</td>
<td>Low</td>
</tr>
</tbody>
</table>
</li>
</ol>
