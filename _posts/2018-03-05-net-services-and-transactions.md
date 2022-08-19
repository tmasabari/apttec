---
layout: post
title: .NET Services and Transactions
date: 2018-03-05 13:07
author: tmasabari
comments: true
categories: [Interview Preparation, Services, ServiceTransaction, Transactions]
---
<h2 style="text-align: justify;">Background</h2>
The intention of this article is to collect the notes on 'implementing transactions across different .NET service frameworks' and include my own experiences as quick refresh guide.
<ol style="text-align: justify;">
 	<li>From version 2, .NET Framework has the <strong>TransactionScope class</strong>. The TransactionScope class in the System.Transactions namespace. It's leveraged by below 3 .NET services frameworks. <strong>TransactionScope </strong>is supported from .NET Core 2.0</li>
 	<li>WCF uses <strong>[TransactionFlow]</strong> attribute to transaction propagation.</li>
 	<li>For an XML Web service, you can declare the Web service's transactional behavior by setting the <a href="https://msdn.microsoft.com/en-us/library/system.web.services.webmethodattribute.transactionoption(v=vs.100).aspx">TransactionOption</a> property of the <a href="https://msdn.microsoft.com/en-us/library/system.web.services.webmethodattribute(v=vs.100).aspx">WebMethod</a> attribute. Web service methods that call other Web service methods participate in different transactions, because <strong>transactions do not flow across Web service methods</strong>.</li>
 	<li>There is an <strong>custom implementation to pass transactions</strong> via HTTP / REST / WEB API</li>
</ol>
<h2 style="text-align: justify;">Basic Idea</h2>
<h3 style="text-align: justify;">Dependencies</h3>
<ol style="text-align: justify;">
 	<li>In <strong>Windows servers</strong>, MSDTC-Distributed Transaction Coordinator/Control Services manage the distributed transactions.</li>
 	<li>In order to enlist transactions belonging to different application domains and event different servers, we can rely on <strong>Distributed Transaction Coordinators</strong> (DTC).</li>
 	<li>The major caveat to this is that MS DTC will <strong>need to be enabled and configured at client and server</strong>. This is only really achievable if your <strong>services are being invoked within a Windows Active Directory Domain</strong>.</li>
 	<li>When the application are hosted in different servers, in order to use the DTC, those servers must be on <strong>same Network Domain</strong>.</li>
 	<li>DTC needs bidirectional communication, in order to coordinate the principal transaction with other transactions. Violation this precondition end up with the error message. To check this precondition you can simply <strong>ping </strong>one server from another and vice-versa.</li>
</ol>
<h3 style="text-align: justify;">Configuration</h3>
<p style="text-align: justify;">You need to configure security settings, both your local and remote servers, for MSDTC, and make sure services are running.</p>
<p style="text-align: justify;"><em><strong>ControlPanel &gt; AdministritiveTools &gt;ComponentServices &gt; DistributedTransactionCoordinator &gt; LocalDTC</strong></em></p>
<p style="text-align: justify;"><img class="alignnone wp-image-733" src="/wp-content/uploads/2018/03/temp-1-274x300.png" alt="" width="422" height="461" /></p>
<p style="text-align: justify;"><em>Some options for the Security tab are described bellow:</em></p>

<div style="text-align: justify;">
<table class="grid">
<thead>
<tr>
<th>Property Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Network DTC Access</td>
<td>If not selected, MSDTC will not allow any remote transaction</td>
</tr>
<tr>
<td>Allow Remote Clients</td>
<td>If it is checked, MSDTC will allow to coordinate remote clients for transaction.</td>
</tr>
<tr>
<td>Allow Remote Administration</td>
<td>Allow remote computers to access and configure these settings.</td>
</tr>
<tr>
<td>Allow Inbound</td>
<td>Allow computers to flow transaction to local computers. This option is needed where MSDTC is hosted for a resource manager like SQL Server.</td>
</tr>
<tr>
<td>Allow Outbound</td>
<td>Allow computers to flow transaction to remote computers. It is needed for a client computer where transaction is initiated.</td>
</tr>
<tr>
<td>Mutual Authentication</td>
<td>Local and Remote computers communicate with encrypted messages. They establish a secured connection with the Windows Domain Account for message communication.</td>
</tr>
<tr>
<td>Incoming Calling Authentication Required</td>
<td>If mutual authentication cannot be established but the incoming caller is authenticated then communication will be allowed. It supports only Windows 2003/XP ServicePack-2.</td>
</tr>
<tr>
<td>No Authentication Required</td>
<td>It allows any non-authenticated non-encrypted communication.</td>
</tr>
<tr>
<td><span style="color: #0000ff;">Enable XA Transaction</span></td>
<td><span style="color: #0000ff;">Allows different operating systems to communicate with MSDTC with XA Starndard.</span></td>
</tr>
<tr>
<td>DTC Logon Account</td>
<td>DTC Service running account. Default account is Network Service.</td>
</tr>
</tbody>
</table>
</div>
<h3 style="text-align: justify;">TransactionScope</h3>
<ul>
 	<li style="text-align: justify;">Before the launch of .NET Framework 2.0 we used <code>SqlTransaction</code> to manage transactions.</li>
 	<li>The managed functionality of COM+ is exposed in the .net via assembly name called as<strong>'System.EnterpriseServices'</strong> which is part of framework class library</li>
 	<li><span style="color: #ff0000;">From version 2, .</span>NET Framework has the <code>TransactionScope</code> class. The TransactionScope class in the <b>System.Transactions</b> namespace.</li>
 	<li>The <a href="https://msdn.microsoft.com/en-us/library/system.transactions.transactioninterop(v=vs.110).aspx">TransactionInterop</a> class exists to provide support for working with transactions between process boundaries, leveraging MS DTC.  Facilitates interaction between <a href="https://msdn.microsoft.com/en-us/library/system.transactions(v=vs.110).aspx">System.Transactions</a> and components that were previously written to interact with MSDTC, COM+, or <a href="https://msdn.microsoft.com/en-us/library/system.enterpriseservices(v=vs.110).aspx">System.EnterpriseServices</a>.</li>
</ul>
<blockquote>Note:
<ul>
 	<li>One important note, many times we are confused when using a DDL statement (Data Definition Language) in a transaction and a question arises, will it support DDL transaction? The answer is yes. You can use a DDL statement like create/alter/ drop statement in the transaction. You can even use a <code><code></code></code><strong>Truncate</strong><strong> </strong>statement inside the transaction.</li>
 	<li><code>TranactionScope</code> is not limited for only databases. It will support other data sources like FileSystem, MSMQ, etc.</li>
 	<li><a href="http://txfnet.codeplex.com/">Transactional NTFS(TxF)</a> .NET is a open source project. You can use this library for creating/writing/coping file/directory inside transactionscope and it will support transaction automatically.</li>
 	<li>If custom code needs to support TranactionScope, IEnlistmentNotification needs to be implemented.</li>
</ul>
</blockquote>
<p style="text-align: justify;">Use of <code>TransactionScope</code> in a .NET application is very, very simple. Any one can use it by following these steps:</p>

<ol style="text-align: justify;">
 	<li>Add a System.Transactions assembly reference to the project. Import the <b><i>system.Transactions </i></b>namespace in your application.</li>
 	<li>If you want to specify the isolation level or timeout for the transaction, create a <strong>TransactionOptions</strong> instance and set it's isolation level and <strong>TimeOut</strong> properties.</li>
 	<li>Create a transactional scope/area with the help of the <code>TransactionScope</code> class starting with a <code>using</code>statement.</li>
 	<li>If you want to specify nesting behavior for transaction declare TransactionScopeOptionvariable and assign it a suitable value.</li>
 	<li>Writing code which needs to have transactional support. For example, Open connections to each database that you need to update, and perform update operations as required by application, if all updates succeed, call the <b>Complete</b> method on the <b>TransactionScope</b> object close the using block. Use a <a href="http://msdn.microsoft.com/en-us/library/system.transactions.transactionscope.aspx" rel="nofollow"><code>TransactionScope</code></a> object and different connections (one for each database). The transaction will escalate to a distributed one automatically.</li>
 	<li>Execute the <code>TransactionScope.Complete</code> method to commit and finish a transaction.</li>
</ol>
<pre class="notranslate" lang="cs"><span class="code-keyword">var</span> option = <span class="code-keyword">new</span> TransactionOptions();
option.IsolationLevel = IsolationLevel.ReadCommitted; // your isolation level
option.Timeout = TimeSpan.FromMinutes(<span class="code-digit">5</span>); // your time out value
<span class="code-keyword">using</span> (<span class="code-keyword">var</span> scope = <span class="code-keyword">new</span> TransactionScope(
  TransactionScopeOption.Required, option))
{
    //application transaction

<span class="code-comment">    //</span><span class="code-comment">either 1 of following lines can be used to rollback</span>
    Transaction.Current.Rollback();
    scope.Dispose();
    <span class="code-comment">//</span><span class="code-comment">if Complete is not called (if below line is not executed) </span>
    <span class="code-comment">//transaction will </span><span class="code-comment">automatically be rolled back</span>
    <span class="code-comment">//</span><span class="code-comment">scope.Complete();
</span>}</pre>
<p style="text-align: justify;">Three very important properties are:</p>

<ol style="text-align: justify;">
 	<li><strong>Isolation Level:</strong> It defines the locking mechanism and policy to read data inside another transaction.</li>
 	<li><strong>Timeout:</strong> How much time object will wait for a transaction to be completed. <strong>Never confuse it with </strong>the <strong><code>SqlCommand</code></strong> <strong><code>Timeout</code></strong> property. <code>SqlCommand</code> <code>Timeout</code> defines how much time the <code>SqlCommand</code> object will wait for a database operation (select/insert/update/delete) to be completed.</li>
 	<li><strong>TransactionScopeOption:</strong> It is an enumeration. There are three options available in this enumeration:</li>
</ol>
<table class="ArticleTable">
<thead>
<tr>
<th>No</th>
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td height="41">1</td>
<td height="41"><code>Required</code></td>
<td height="41">It is default value for <code>TransactionScope</code>. If any already exists any transaction then it will join with that transaciton otherwise create new one.</td>
</tr>
<tr>
<td>2</td>
<td><code>RequiredNew</code></td>
<td>When select this option a new transaction is always created. This transaction is independent with its outer transaction.</td>
</tr>
<tr>
<td>3</td>
<td><code>Suppress</code></td>
<td>When select this option, no transaction will be created.</td>
</tr>
</tbody>
</table>
<pre id="pre290428" class="notranslate" lang="xml"><span class="code-keyword">&lt;</span><span class="code-leadattribute">system.transactions</span><span class="code-keyword">&gt;</span>    
    <span class="code-keyword">&lt;</span><span class="code-leadattribute"><strong>defaultSettings</strong></span> timeout<span class="code-keyword">="</span><span class="code-keyword">30"</span><span class="code-keyword">/</span><span class="code-keyword">&gt;</span>
    <span class="code-keyword">&lt;</span><span class="code-leadattribute"><strong>machineSettings</strong></span> maxTimeout<span class="code-keyword">="</span><span class="code-keyword">1200"</span><span class="code-keyword">/</span><span class="code-keyword">&gt;</span>
<span class="code-keyword">&lt;</span><span class="code-leadattribute">/system.transactions</span><span class="code-keyword">&gt;</span></pre>
<h3 style="text-align: justify;">Custom IEnlistmentNotification implementation</h3>
<pre id="pre18403" class="notranslate" lang="cs"><span class="code-keyword">public</span> <span class="code-keyword">class</span> DirectoryCreator : IEnlistmentNotification
{
    <span class="code-keyword">public</span> <span class="code-keyword">string</span> _directoryName; 
    <span class="code-keyword">private</span> <span class="code-keyword">bool</span> _isCommitSucceed = <span class="code-keyword">false</span>;
    <span class="code-keyword">public</span> DirectoryCreator(<span class="code-keyword">string</span> directoryName)
    {
        _directoryName = directoryName;
        Transaction.Current.EnlistVolatile(<span class="code-keyword">this</span>, EnlistmentOptions.None);
    }
    <span class="code-keyword">public</span> <span class="code-keyword">void</span> Commit(Enlistment enlistment)
    {
        Directory.CreateDirectory(_directoryName);
        _isCommitSucceed = <span class="code-keyword">true</span>;
        enlistment.Done();
    }
    <span class="code-keyword">public</span> <span class="code-keyword">void</span> InDoubt(Enlistment enlistment)
    {
        enlistment.Done();
    }
    <span class="code-keyword">public</span> <span class="code-keyword">void</span> Prepare(PreparingEnlistment preparingEnlistment)
    {
        preparingEnlistment.Prepared();
    }
    <span class="code-keyword">public</span> <span class="code-keyword">void</span> Rollback(Enlistment enlistment)
    {
        <span class="code-keyword">if</span> (_isCommitSucceed))
            Directory.Delete(_directoryName);
        enlistment.Done();
    }
}</pre>
<h1><strong><b>Enable Transactions in </b></strong><strong><b>Services</b></strong></h1>
<h2><strong><b>Web Services Transaction can't be passed</b></strong></h2>
<ul>
 	<li>The transaction support for Web services leverages the support found in the common language runtime, which is based on the same distributed transaction model found in <strong>Microsoft Transaction Server (MTS) and COM+ Services</strong>. The model is based on declaratively deciding whether an object participates in a transaction, rather than writing specific code to handle committing and rolling back a transaction.</li>
 	<li>For an XML Web service created using ASP.NET, you can declare the Web service's transactional behavior by setting the <a href="https://msdn.microsoft.com/en-us/library/system.web.services.webmethodattribute.transactionoption(v=vs.100).aspx">TransactionOption</a> property of the <a href="https://msdn.microsoft.com/en-us/library/system.web.services.webmethodattribute(v=vs.100).aspx">WebMethod</a> attribute applied to the Web service method.</li>
 	<li><strong>XML Web service is a legacy technology. XML Web services and XML Web service clients should now be created using </strong><a href="http://go.microsoft.com/fwlink/?LinkID=127777">Windows Communication Foundation </a>.</li>
 	<li>Web service methods can participate in a <strong>transaction only as the root of a new transaction</strong>. As the root of a new transaction, all interactions with resource managers, such as servers running Microsoft SQL Server, Microsoft Message Queuing (also known as MSMQ), and Microsoft Host Integration Server maintain the ACID properties required to run robust distributed applications.</li>
 	<li>Web service methods that call other Web service methods participate in different transactions, because <strong>transactions do not flow across Web service methods</strong>.</li>
</ul>
Steps
<ol>
 	<li>Add reference to System.EnterpriseServices</li>
 	<li>Add references to the System.Web.Services
and System.EnterpriseServices namespaces.</li>
 	<li>Declare a Web service method, setting the TransactionOption property of the WebMethodAttribute attribute to System.EnterpriseServices.TransactionOption.RequiresNew .
[ WebMethod(TransactionOption=TransactionOption.RequiresNew)]
public int DeleteAuthor(string lastName)</li>
 	<li>A physical transaction occurs when a transactional object accesses a data resource, such as a database or message queue. The <strong>transaction that is associated with the object automatically flows to the appropriate resource manager</strong>.</li>
 	<li>A .NET Framework data provider, such as the .NET Framework Data Provider for SQL Server or the .NET Framework Data Provider for OLE DB, looks up the transaction in the object's context and <strong>enlists in the transaction through the Distributed Transaction Coordinator (DTC)</strong>. The entire transaction occurs automatically.</li>
 	<li>In Visual Studio .NET, a proxy class is generated when a Web Reference is added. If the client call the service via proxy, transactions are taken care automatically. When the method that implements the Web service method is <strong>not</strong> called due to an Internet request for the file with an .asmx extension in which it resides or is associated with, the value of the <strong>TransactionOption property has no effect</strong>.</li>
 	<li>If an exception is thrown while the Web service method is executing, the transaction is automatically aborted; conversely, if no exception occurs, the transaction is automatically committed.</li>
</ol>
<h2><strong><b>Rest</b></strong></h2>
<ul>
 	<li>Distributed transactions over WCF <strong><b>RESTful services are directly </b></strong>not possible<strong><b> b</b></strong>ecause there is simply no way to propagate and manage the transaction state over plain HTTP requests.</li>
 	<li>You may want to look into plain WCF services, over HTTP (wsHttpBinding) or TCP/IP (net.tcp), or even give a look on <a href="http://msdn.microsoft.com/en-us/library/cc668792.aspx">WCF Data Services</a>.</li>
 	<li>This <a href="https://code.msdn.microsoft.com/Distributed-Transactions-c7e0a8c2">article</a> show a possible solution to obtain the same <strong>behaviour with WebAPI in order to enlist</strong>, under a client transaction, operations performed in different application domain, permitting participation of different process in same transaction.</li>
</ul>
&nbsp;
<h3>Steps</h3>
<ol>
 	<li>Client creates the primary transaction. Main transaction token is passed as header to the services.
var token = TransactionInterop.<span style="color: #0000ff;">GetTransmitterPropagationToken</span>(Transaction.Current);request.Headers.Add("TransactionToken", Convert.ToBase64String(token));</li>
 	<li>Each service retrieve a transaction propagation token in header by using filter OnActionExecuting</li>
 	<li> Create a transaction scope and promote the current transaction to a distributed transaction.
var <span style="color: #ff0000;">transaction </span>= TransactionInterop.<span style="color: #0000ff;">GetTransactionFromTransmitterPropagationToken</span>(transactionToken);
var transactionScope = new <span style="color: #ff9900;">TransactionScope</span>(<span style="color: #ff0000;">transaction</span>);
actionContext.Request.Properties.Add(TransactionId, transactionScope);</li>
 	<li>Using OnActionExecuted filter of WebAPI, commit or rollback the remote transaction</li>
</ol>
&nbsp;
<h1><strong><b>WCF</b></strong></h1>
<p style="font-weight: 400;">To add transaction support to a WCF service, you will take the following actions:</p>

<ol style="font-weight: 400;">
 	<li>Enable transactions on the binding. This is required.</li>
 	<li>Add transaction support to the service contract. This is required.</li>
 	<li>Add transaction support to the code (class/method) that implements the service contract. This is required.</li>
 	<li>Configure transactions in the implementation code. This is optional.</li>
</ol>
&nbsp;

1. Binding

<strong>All</strong> of the WCF supplied bindings support transactions, <strong>with the exception of the BasicHttpBinding and NetPeerTcpBinding</strong> bindings. You must use a binding that supports transactions. Example:

&lt;bindings&gt;<span style="color: #ff0000;">&lt;wsHttpBinding&gt;&lt;binding name="TransactionalBind" transactionFlow="true"/</span>&gt;&lt;/wsHttpBinding&gt;&lt;/bindings&gt;

2. TransactionFlow in Contracts

The TransactionFlow attribute specifies whether the operation supports transactions. There are three possible values for this attribute:
<ol>
 	<li>NotAllowed : The operation cannot participate in a transaction. This is the default value for this attribute.- Use it for database/io read operations</li>
 	<li>Allowed : The operation will participate in a transaction if the client creates one.</li>
 	<li>Mandatory : In order to call this operation, the<span style="color: #ff0000;"> client must create a transaction.</span></li>
</ol>
<p class="MtpsCodeSnippet" style="padding-left: 60px;">Interface
[OperationContract]
[TransactionFlow(TransactionFlowOption.NotAllowed)]
List&lt;Customer&gt; GetCustomers();</p>
<p class="MtpsCodeSnippet" style="padding-left: 60px;">[OperationContract]
[TransactionFlow(TransactionFlowOption.<span style="color: #ff0000;">Mandatory</span>)]
string PlaceOrder(Order order);</p>
3. Attributes in ServiceBehavior
<ol>
 	<li>When you added the <strong>TransactionFlow</strong> attribute to the service contract, you enabled clients to start a transaction. Here in class definition, you are instructing the WCF runtime to include these methods in transactions. Both steps are required to add transaction support to the service.</li>
 	<li>Setting the <strong>TransactionScopeRequired</strong> property to <strong>true</strong> specifies that clients cannot call these methods unless they are part of a transaction.</li>
 	<li>Setting the <strong>TransactionAutoComplete</strong> property to <strong>true</strong> specifies that the transaction will complete automatically if no exceptions occur. This is the default value for this property.</li>
 	<li>Setting the <strong>TransactionAutoComplete</strong> property to <strong>false</strong> specifies that the transaction will not complete and passed back to client if no exceptions occur.  /if error occurs it will abort the transaction back at the client.</li>
</ol>
<p style="padding-left: 60px;">Class Definition
[ServiceBehavior(
<strong>TransactionIsolationLevel= System.Transactions.IsolationLevel.Serializable</strong>,  <strong>TransactionTimeout</strong>="00:00:30")]
public class OrdersService : IOrdersService {</p>
[OperationBehavior(<strong>TransactionScopeRequired</strong>=true,<strong>TransactionAutoComplete</strong>=true)]
public string PlaceOrder(Order order)<i></i>

&nbsp;
<h4 style="text-align: justify;">Points of Interest</h4>
<ol style="text-align: justify;">
 	<li>Distributed transactions requiring the Microsoft Distributed Transaction Coordinator service are not supported on SQL Server running on Linux. SQL Server to SQL Server <i><strong>Linked Servers</strong></i> are supported if a DTC transaction is not required.</li>
</ol>
<h2 style="text-align: justify;">References</h2>
<ol>
 	<li style="text-align: justify;">https://code.msdn.microsoft.com/Distributed-Transactions-c7e0a8c2</li>
 	<li style="text-align: justify;">https://www.codeproject.com/Articles/690136/All-About-TransactionScope</li>
 	<li style="text-align: justify;">Transactions in ASP.NET XML Web Services https://msdn.microsoft.com/en-us/library/85f292h1(v=vs.100).aspx</li>
 	<li style="text-align: justify;">XML Web Service https://msdn.microsoft.com/en-us/library/0b80z9xk(v=vs.100).aspx</li>
 	<li style="text-align: justify;">https://social.msdn.microsoft.com/Forums/en-US/4cbdb3fd-b7ea-4c1f-91a0-2e56b22b591e/transactions-using-enterpriseservices-or-systemtransactions-which-to-use?forum=windowstransactionsprogramming</li>
 	<li style="text-align: justify;">https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/</li>
 	<li>http://www.codeproject.com/Articles/38793/Steps-to-Enable-Transactions-in-WCF</li>
 	<li>Transactions in WCF Services https://msdn.microsoft.com/en-us/library/ff384250.aspx</li>
 	<li>http://stackoverflow.com/questions/11299273/transactions-with-asp-net-web-api</li>
 	<li>.NET core 2.0 https://docs.microsoft.com/en-us/dotnet/api/system.transactions.transactionscope?view=netcore-2.0</li>
 	<li>todo <a href="https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-transactions-overview">Distributed transactions across cloud databases</a></li>
 	<li>https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/distributed-transactions</li>
</ol>
