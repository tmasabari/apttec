---
layout: post
title: AWS Storage - EBS, Gateway, EFS, Glacier, S3 & Import Export
date: 2018-03-26 09:13
author: tmasabari
comments: true
categories: [AWS, Storage]
---
<h3>Storage and Content Delivery</h3>
<ol>
 	<li><a href="http://www.apttec.com/data-center-storage-devices/">Types of physical storage devices in data centers</a></li>
 	<li>
<p id="xcGQZDq"><img class="alignnone wp-image-1330 " src="/wp-content/uploads/2018/03/img_5ab893ce4d744.png" alt="" width="426" height="240" /></p>
</li>
 	<li>Simple Storage Service (S3)
<ol>
 	<li>elastic - offers unlimited data storage space in the cloud.</li>
 	<li>is an object-based online storage service</li>
 	<li>charged based up on consumption</li>
 	<li>can be accessed from anywhere, internet, within aws instances/services etc</li>
 	<li><strong>static web server</strong></li>
 	<li>regional buckets</li>
 	<li>file in amazon s3 is referred as object
<ol>
 	<li>actual data is not visible to amazon</li>
 	<li>metadata - name value pairs - custom meta dat</li>
</ol>
</li>
 	<li>bucket
<ol>
 	<li>logical container of multiple objects</li>
 	<li> can have max 100 buckets</li>
 	<li>object size can be up to 5 TB</li>
</ol>
</li>
 	<li>Types of storage class
<ol>
 	<li>S3 standard - active dat</li>
 	<li>S3 standard rare access - general purpose &amp; enduring but not much active</li>
 	<li>Amazon glacier - long term archiving</li>
</ol>
</li>
 	<li> configurable policies to select type of storage, data would be migrated to most appropriate storage class without any change in the application</li>
 	<li>Price
<ol>
 	<li>volume of storage</li>
 	<li>bandwidth used</li>
 	<li>number of http requets (get, put, post)</li>
</ol>
</li>
 	<li>can use both SOAP, REST APIs, to retrieve and upload objects</li>
</ol>
</li>
 	<li>EBS
<ol>
 	<li>like hard disk</li>
 	<li>can be connected to only one instance at a time</li>
</ol>
</li>
 	<li>Elastic File System
<ol>
 	<li>file storage service supports latest network file system- NFSv4 protocol</li>
 	<li>is a storage for <strong>one or multiple</strong> EC2 instances.</li>
 	<li>charge only for data storage
<ol>
 	<li>manage content repositories</li>
 	<li>manage multiple dev/test environments</li>
 	<li>scale performance of bigdata applications</li>
</ol>
</li>
 	<li>manage users accessing data and shared datasets from remote location</li>
 	<li>Create shared folder <strong>accessed by multiple instances at a time. act as common data store</strong>
<p id="VpaQsVm"><img class="alignnone wp-image-990 " src="/wp-content/uploads/2018/03/img_5aab1d18337ff.png" alt="" width="298" height="186" /></p>
</li>
</ol>
</li>
 	<li>Amazon Glacier is the long-term backup/archiving service in the cloud.
<ol>
 	<li>Cost vs performance</li>
 	<li>store less frequently used data</li>
 	<li>
<p id="bPzkSqX"><img class="alignnone size-full wp-image-991 " src="/wp-content/uploads/2018/03/img_5aab1e0255d8c.png" alt="" /></p>
</li>
</ol>
</li>
 	<li>Storage gateway
<ol>
 	<li>increase the capacity to store files, such as Word documents.</li>
 	<li>replicate the data on premise data center to cloud
<ol>
 	<li>for example for disaster recovery</li>
</ol>
</li>
 	<li>sync / async replication</li>
</ol>
</li>
 	<li>import/export</li>
 	<li>Amazon Snowball
<ol>
 	<li>to move large amounts of data quickly (petabytes) without a network.</li>
 	<li>Snowball Edge (external storage device) is a new version of Snowball;</li>
 	<li>Amazon Snowmobile (truck) is an Exabyte-scale data transfer service used to move extremely large amounts of data to
AWS.</li>
</ol>
</li>
 	<li>CloudFront is a content delivery service (CDN) that integrates with other Amazon's cloud services to provide an easy way for businesses and developers to distribute data through high-speed transfers.
<ol>
 	<li>Static and dynamic content can be distributed to edge locations using cloudfront
<p id="mRLVAaZ"><img class="alignnone wp-image-989 " src="/wp-content/uploads/2018/03/img_5aab1cb8013b8.png" alt="" width="310" height="193" /></p>
</li>
</ol>
</li>
</ol>
<ul>
 	<li>EC2 instance storage
<ul>
 	<li>ephemeral storage - temporary - content is lost when the system is rebooted</li>
 	<li>used for
<ul>
 	<li>stateless web hosts</li>
 	<li>transcoding</li>
 	<li>cache</li>
 	<li>HPC - High Performance Computing</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3>Elastic Block Storage EBS</h3>
<ul>
 	<li>durable storage devices attached to EC2 instance in the same AZ</li>
 	<li>it acts similar to physical hard drive</li>
 	<li>even though the EC2 instance terminated, the contents will be preserverd unless explicitly dropped.</li>
 	<li>provides option to increase the size at later stage once created.
<ul>
 	<li>But decreasing is not possible</li>
 	<li>increasing the size can't be done dynamically. storage must be disconnected before increasing</li>
</ul>
</li>
 	<li>99.999% availability
<ul>
 	<li>AWS maintains 3 copies of data (notes) for high availability using 3 networks primary network and 2 alternate networks</li>
 	<li>10 GB of data takes 30 GB of storage</li>
 	<li>all are maintained in different buildings of same AZ</li>
</ul>
</li>
 	<li>Benefits
<ul>
 	<li>snapshots - point in time image/backup of the volume
<ul>
 	<li>snapshots are created based upon the region</li>
 	<li><strong>incremental backups to optimize the storage.</strong></li>
 	<li>active snapshot contains the all the data of that point of time. but only the latest can be restored</li>
 	<li>of volume is encrypted snapshot is also encrypted</li>
 	<li>copy the snapshot to S3</li>
 	<li>while generating multiple snapshots only the delta (modified data blocks) is saved</li>
 	<li>snapshots can act as a baseline for new volumes</li>
 	<li>pay for using S3 only</li>
 	<li>can copy snapshots across the regions using snapshot copy command</li>
 	<li>share the snapshots with required AWS accounts</li>
 	<li>snapshot can only include the data acutally written to volume
<ul>
 	<li>excluding the cache data of OS or application</li>
</ul>
</li>
 	<li>to snapshot of root volumes of instances, stop them before taking snapshots</li>
 	<li>Restore
<ul>
 	<li>have snapshot id and access permission</li>
 	<li>new volumes load slowly</li>
 	<li>need not to wait for the data to load fully to the volume
<ul>
 	<li>when the data which is not yet loaded is accessed</li>
 	<li>volume loads it first and then loads rest of the data</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
 	<li>persistence</li>
 	<li>security</li>
 	<li>availability</li>
</ul>
</li>
 	<li>Types - speed performance vs cost
<ul>
 	<li>General purpose SSD
<ul>
 	<li>virtusal desktops, dev, testing system boot volumes, small to medum DBs</li>
 	<li>1GB to 16 TBs</li>
 	<li>low latency - milli seconds</li>
 	<li>burst up to 3000 iops</li>
 	<li>baseline performance 10,000 IOPS</li>
 	<li>throughput 128 MBs for volume size &lt;= 170 GB</li>
</ul>
</li>
 	<li>provisioned iops
<ul>
 	<li>io intensive workloads
<ul>
 	<li>large databases oracle mysql</li>
 	<li>critical apps demands constant iops</li>
 	<li>web sites with signigicant traffic<img class=" wp-image-1276 alignleft" src="/wp-content/uploads/2018/03/img_5ab4eb9d06970.png" alt="" width="135" height="167" />In order to take advantage of this speed, it must be connected to <b>EBS optimized EC2 instances  which has specialized channel of communication</b></li>
 	<li>user can define iops rate
<ul>
 	<li>delivers 10% of rate in 99.9% in a year</li>
</ul>
</li>
</ul>
</li>
 	<li>can specify up to 20,000 iops</li>
 	<li>volume size 4gibibytes - 16 tebibytes</li>
 	<li>throughput range up to 320 MebiB/sec</li>
</ul>
</li>
 	<li>Magnettic
<ul>
 	<li>data is accessed rarely or sequential reads</li>
 	<li>volume size 1gibibytes - 1tebibytes</li>
 	<li>deliver almost 100 iops burst up to several hundred iops</li>
 	<li>throughput range 40 to 90 MebiB/sec</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html">Instance Store</a></h3>
<ul>
 	<li>An <em>instance store</em> provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer.</li>
 	<li>Instance store is ideal for temporary storage of information that changes frequently, such as <strong>buffers, caches, scratch data, and other temporary content,</strong> or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.</li>
 	<li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/add-instance-store-volumes.html">The number and size of available instance store volumes</a> for your instance varies by instance type. Some instance types do not support instance store volumes. For more information about the instance store volumes support by each instance type, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html#instance-store-volumes">Instance Store Volumes</a>. If the instance type you choose for your instance supports instance store volumes, you must add them to the block device mapping for the instance when you launch it. After you launch the instance, you must ensure that the instance store volumes for your instance are formatted and mounted before you can use them.</li>
 	<li>instance store takes usually 5 minutes (compare to 1 minute of EBS). fist all the data in S3 (AMI) copied to instance store. That's why it takes more time.</li>
</ul>
<h3></h3>
<h3>EBS and RAID 0</h3>
<ul>
 	<li>ebs volume can support 16 tb only</li>
 	<li>combine multiple ebs volumes as a single drive</li>
</ul>
<h3>EFS</h3>
<ol>
 	<li>network shared storage connected to multiple instances at a same time</li>
 	<li>mounted drive</li>
 	<li>elastic - no need to specify size. charge as per usage</li>
</ol>
<h3>Glacier</h3>
<ul>
 	<li>Store the data remain for ever but rarely used</li>
 	<li>data backup and archiving</li>
 	<li>secure storage</li>
 	<li>low cost 007 cents per gb per month</li>
 	<li>reduces administrative lisability
<ul>
 	<li>capacity planning</li>
 	<li>data replication</li>
 	<li>hardware provisioning</li>
 	<li>hardware failures</li>
 	<li>hardware migrations</li>
</ul>
</li>
 	<li>data stored as archives
<ul>
 	<li>single file or combination of several files</li>
</ul>
</li>
 	<li>archives are arranged as vaults
<ul>
 	<li>accessed by IAM services</li>
</ul>
</li>
 	<li>data flow is secured by SSL, 256 bit advanced encryption system</li>
 	<li>use cases
<ul>
 	<li>archieves off site enterprise informatoin</li>
 	<li>backup media assets</li>
 	<li>store research and scientific data</li>
 	<li>preserve digital data</li>
 	<li>replacing magnetic tapes</li>
</ul>
</li>
</ul>
<a href="https://aws.amazon.com/storagegateway/faqs/?sc_channel=PS&amp;sc_campaign=acquisition_IN&amp;sc_publisher=google&amp;sc_medium=storage_gateway_b&amp;sc_content=sitelink&amp;sc_detail=aws%20storage%20gateway&amp;sc_category=storage_gateway&amp;sc_segment=storage_gateway_faqs&amp;sc_matchtype=e&amp;sc_country=IN&amp;s_kwcid=AL!4422!3!159808565200!e!!g!!aws%20storage%20gateway&amp;ef_id=WUBEuwAAAHAi4zTe:20180325233938:s">Storage gateway</a>
<ul>
 	<li><em>Amalgamation</em> of onpremisesIT and AWS Storage infra.</li>
 	<li><em>Amalgamation</em> is the combination of one or more entities into a new entity.</li>
</ul>
The AWS Storage Gateway service enables <strong>hybrid storage between on-premises environments and the AWS Cloud</strong>. It seamlessly integrates on-premises enterprise applications and workflows with Amazon’s block and object cloud storage services through industry standard storage protocols.
<ul>
 	<li>provides secure connection between aws storage and on premises storage</li>
 	<li>Storage protocols support</li>
 	<li>minimizes the latency using caching frequently accessed</li>
 	<li>security: stores the data in encrypted form of s3 or amazon galcier</li>
 	<li>use cases</li>
</ul>
<ol>
 	<li> Typical use cases include backup and archiving, disaster recovery, moving data to S3 for in-cloud workloads, and tiered storage.</li>
 	<li>backup applications in encrypted form</li>
 	<li>plan for diaster recovery-mirror of entire production environment</li>
 	<li>share files in corporate environment</li>
</ol>
3 storage interfaces- AWS Storage Gateway supports three storage interfaces: file, volume, and tape
<ol>
 	<li>Gateway cached values - file gateway
<ol>
 	<li>The <i>file gateway </i>enables you to store and retrieve objects in Amazon S3 using file protocols, such as NFS. Objects written through file gateway can be directly accessed in S3.</li>
 	<li>File gateway provides a virtual file server</li>
 	<li> your configured S3 buckets will be available as Network File System (NFS) mount points</li>
 	<li>real time access</li>
 	<li>store in S3</li>
 	<li>user dont have  latency</li>
 	<li>frequently accessed files</li>
</ol>
</li>
 	<li>Gateway stored volumes - volume gateway
<ol>
 	<li>The <i>volume gateway </i>provides block storage to your applications using the iSCSI protocol. Data on the volumes is stored in Amazon S3. To access your iSCSI volumes in AWS, you can take EBS snapshots which can be used to create EBS volumes.</li>
 	<li>Volume gateway provides an iSCSI target, which enables you to create volumes and mount them as iSCSI devices from your on-premises or EC2 application servers. The volume gateway runs in either a cached or stored mode.
<ul>
 	<li>In the cached mode, your primary data is written to S3, while retaining your frequently accessed data locally in a cache for low-latency access.</li>
 	<li>In the stored mode, your primary data is stored locally and your entire dataset is available for low-latency access while asynchronously backed up to AWS.</li>
</ul>
</li>
 	<li>In either mode, you can take point-in-time snapshots of your volumes and store them in Amazon S3, enabling you to make space-efficient versioned copies of your volumes for data protection and various data reuse needs.</li>
 	<li>quick access to data</li>
 	<li>backup data stored both onpremises and S3</li>
 	<li>in case of disaster, data can be retrieved from local or from ec2</li>
</ol>
</li>
 	<li>Gateway virtual tape library - tape gateway
<ol>
 	<li>The <i>tape gateway </i>provides your backup application with an iSCSI virtual tape library (VTL) interface, consisting of a virtual media changer, virtual tape drives, and virtual tapes. Virtual tape data is stored in Amazon S3 or can be archived to Amazon Glacier.</li>
 	<li>Your backup application can read data from or write data to virtual tapes by mounting them to virtual tape drives using the virtual media changer.
<ol>
 	<li>Virtual tapes are available for immediate access and are backed by Amazon S3.</li>
 	<li>You can also archive tapes. Archived tapes are stored in Amazon Glacier.</li>
</ol>
</li>
 	<li>low cost solution</li>
 	<li>archive data in tape based application in aws cloud</li>
 	<li>stores data in virtual tape cartridges</li>
</ol>
</li>
</ol>
&nbsp;
<h3>Import/Export-</h3>
Import/Export- using physical storage devices avoid internet to transfer large volume of data to/from AWS
<ol>
 	<li>uses high speed internal network to load from physical storage to cloud devices</li>
 	<li>reduce network cost.</li>
 	<li>unending network queue</li>
 	<li>data security</li>
 	<li> <a href="https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html">snowball</a>
<p id="TUCQFhm"><img class="size-full wp-image-1275 alignnone" src="/wp-content/uploads/2018/03/img_5ab4e61116f44.png" alt="" /></p>

<ol>
 	<li>This transport is done by shipping the data in the appliances through a regional carrier. The appliances are rugged shipping containers, complete with E Ink shipping labels.</li>
 	<li>In the US regions, Snowballs come in two sizes: 50 TB and 80 TB. All other regions have 80 TB Snowballs only. Snowball doesn't support international shipping or shipping between regions outside of the US</li>
 	<li>managed by key management services</li>
 	<li>5 times cheaper than high speed internet connection</li>
 	<li>if your data transfer time exceeds 1 week go for snowball</li>
 	<li>supports only import to S3</li>
</ol>
</li>
 	<li><a href="https://docs.aws.amazon.com/AWSImportExport/latest/DG/whatisdisk.html">disk</a>
<ol>
 	<li>AWS Import/Export is a good choice if you have 16 terabytes (TB) or less of data to import into Amazon Simple Storage Service or Amazon Elastic Block Store (Amazon EBS). You can also export data from Amazon S3 with AWS Import/Export.</li>
 	<li>After the data export or import completes, we return your storage device.</li>
</ol>
</li>
</ol>
<h2><strong>LAB </strong></h2>
<h3><strong>EBS </strong></h3>
<ul>
 	<li>Create an EBS Volume
<ul>
 	<li>There is separate section Elastic Block Storage in EC2</li>
 	<li>Create Volume
<ul>
 	<li>select volume type - provisioned ssd, stanard ssd,</li>
 	<li>size in gb can be 1 as well</li>
 	<li>specify iops, can specify throughput for certain types</li>
 	<li>Encryption - select based up on industry standard
<ul>
 	<li>either you can let AWS used its key</li>
 	<li>or specify the key in key management system (KMS)</li>
</ul>
</li>
 	<li>Specify the tags for automation &amp; references</li>
</ul>
</li>
 	<li>Attach to EC2 instance
<ul>
 	<li>Actions -&gt; Attach Volume</li>
</ul>
</li>
 	<li>in Widnows
<ul>
 	<li>System management</li>
 	<li>Make disk online</li>
 	<li>Initialize volume</li>
 	<li>Create new simple volume</li>
</ul>
</li>
</ul>
</li>
 	<li>Join multiple volumes
<ul>
 	<li>Create multiple volumes attach them to instances</li>
 	<li>in windows management tool it will be visible as 2 disks</li>
 	<li>make them online &amp; initialize disk</li>
 	<li>Difference is choose <strong>"New Striped Volume"</strong></li>
 	<li>Select both the disks</li>
 	<li>Total storage is combinied size</li>
</ul>
</li>
 	<li>Other options
<ul>
 	<li>Spanned volume</li>
 	<li>Striped volume (RAID 0)</li>
 	<li>Mirrored volume</li>
 	<li>RAID-5 volume</li>
 	<li>Convert GPT disk</li>
 	<li>Convert Dynamic disk</li>
</ul>
</li>
 	<li>
<p id="BWeWTgP"><img class="wp-image-1449 alignright" src="/wp-content/uploads/2018/04/img_5ac78202229c8.png" alt="" width="338" height="271" /></p>
Create snapshots
<ul>
 	<li>if volume is encrypted the snapshot is also encrypted</li>
 	<li>snapshot is charged only for the used storage</li>
 	<li>delete volume
<ul>
 	<li>detach the volume (if not root you can even detach while instance is running</li>
</ul>
</li>
 	<li>create volume
<ul>
 	<li>select snapshot</li>
 	<li>action create volume</li>
 	<li>you can specify the size</li>
</ul>
</li>
 	<li>select volume
<ul>
 	<li>actions -&gt; attach -&gt; select instance</li>
</ul>
</li>
</ul>
</li>
 	<li>
<p class="title"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html"><b>To create an AMI from a snapshot using the console</b></a></p>

<ol>
 	<li>Open the Amazon EC2 console at <a href="https://console.aws.amazon.com/ec2/" target="_blank" rel="noopener">https://console.aws.amazon.com/ec2/</a>.</li>
 	<li>In the navigation pane, under <b>Elastic Block Store</b>, choose <b>Snapshots</b>.</li>
 	<li>Choose the snapshot and choose <b>Actions</b>, <b>Create Image</b>.</li>
 	<li>
<div class="itemizedlist">
<ul class="itemizedlist" type="disc">
 	<li class="listitem"><b>Architecture</b>: Choose <b>i386</b> for 32-bit or <b>x86_64</b> for 64-bit.</li>
 	<li class="listitem"><b>Root device name</b>: Enter the appropriate name for the root volume. For more information, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/device_naming.html">Device Naming on Linux Instances</a>.</li>
 	<li class="listitem"><b>Virtualization type</b>: Choose whether instances launched from this AMI use paravirtual (PV) or hardware virtual machine (HVM) virtualization. For more information, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html">Linux AMI Virtualization Types</a>.</li>
 	<li class="listitem">(PV virtualization type only) <b>Kernel ID</b> and <b>RAM disk ID</b>: Choose the AKI and ARI from the lists. If you choose the default AKI or don't choose an AKI, you must specify an AKI every time you launch an instance using this AMI. In addition, your instance may fail the health checks if the default AKI is incompatible with the instance.</li>
 	<li class="listitem">(Optional) <b>Block Device Mappings</b>: Add volumes or expand the default size of the root volume for the AMI. For more information about resizing the file system on your instance for a larger volume, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html">Extending a Linux File System after Resizing the Volume</a>.In the <b>Create Image from EBS Snapshot</b> dialog box, complete the fields to create your AMI, then choose<b>Create</b>. If you're re-creating a parent instance, then choose the same options as the parent instance.</li>
</ul>
</div></li>
</ol>
</li>
 	<li>
<p id="sharingamis-intro" class="topictitle"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/sharingamis-intro.html">Making an AMI Public</a></p>

<ul>
 	<li>Amazon EC2 enables you to share your AMIs with other AWS accounts. You can allow all AWS accounts to launch the AMI (make the AMI public),</li>
 	<li>or only allow a few specific accounts to launch the AMI (see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/sharingamis-explicit.html">Sharing an AMI with Specific AWS Accounts</a>)</li>
 	<li>To avoid exposing sensitive data when you share an AMI, read the security considerations in <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/building-shared-amis.html">Guidelines for Shared Linux AMIs</a> and follow the recommended actions.</li>
 	<li>
<p class="title"><b>To share a public AMI using the console</b></p>

<ol>
 	<li>Open the Amazon EC2 console at <a href="https://console.aws.amazon.com/ec2/" target="_blank" rel="noopener">https://console.aws.amazon.com/ec2/</a>.</li>
 	<li>In the navigation pane, choose <b>AMIs</b>.</li>
 	<li>Select your AMI from the list, and then choose <b>Actions</b>, <b>Modify Image Permissions</b>.</li>
 	<li>Choose <b>Public</b> and choose <b>Save</b>.</li>
</ol>
</li>
</ul>
</li>
 	<li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/deregister-ami.html">Deregister AMI</a> / Delete Snapshots / Delete instances
<ul>
 	<li>When you deregister an AMI, it doesn't affect any instances that you've already launched from the AMI. You'll continue to incur usage costs for these instances. Therefore, if you are finished with these instances, you should terminate them.</li>
</ul>
</li>
 	<li>
<p class="title"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/deregister-ami.html"><b>To clean up your Amazon EBS-backed AMI</b></a></p>

<ol>
 	<li>Open the Amazon EC2 console at <a href="https://console.aws.amazon.com/ec2/" target="_blank" rel="noopener">https://console.aws.amazon.com/ec2/</a>.</li>
 	<li>In the navigation pane, choose <b>AMIs</b>. Select the AMI, and take note of its ID — this can help you find the correct snapshot in the next step. Choose <b>Actions</b>, and then <b>Deregister</b>. When prompted for confirmation, choose <b>Continue</b>.
<div class="aws-note">
<p class="aws-note">Note</p>
It may take a few minutes before the console removes the AMI from the list. Choose <b>Refresh</b> to refresh the status.

</div></li>
 	<li>In the navigation pane, choose <b>Snapshots</b>, and select the snapshot (look for the AMI ID in the <b>Description</b>column). Choose <b>Actions</b>, and then choose <b>Delete Snapshot</b>. When prompted for confirmation, choose <b>Yes, Delete</b>.</li>
 	<li>(Optional) If you are finished with an instance that you launched from the AMI, terminate it. In the navigation pane, choose <b>Instances</b>. Select the instance, choose <b>Actions</b>, then <b>Instance State</b>, and then <b>Terminate</b>. When prompted for confirmation, choose <b>Yes, Terminate</b>.</li>
</ol>
</li>
 	<li>in cloud watch - events - create snapshot once in a specific duration like each day etc</li>
</ul>
