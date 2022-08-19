---
layout: post
title: 5 1 Security SSIS Kerberos - docx
date: 2018-03-20 10:10
author: tmasabari
comments: true
categories: [Security]
---
<h3><a href="http://www.techrepublic.com/article/understanding-and-selecting-authentication-methods/ "><strong>Authentication</strong></a></h3>
Computer/network security hinges on two very simple goals:
<ul>
 	<li>Keeping unauthorized persons from gaining access to resources</li>
 	<li>Ensuring that authorized persons <em>can</em> access the resources they need</li>
</ul>
<h2><strong>Authentication vs. authorization
</strong></h2>
There is a difference between authentication and authorization. With authentication, the system proves that you are who you say you are. With authorization, the system verifies that you have rights to do what you want to do.

While authentication verifies the user’s identity, authorization verifies that the user in question has the correct permissions and rights to access the requested resource. As you can see, the two work together. Authentication occurs first, then authorization.

For example, when a user who belongs to a Windows domain logs onto the network,
<ol>
 	<li>his or her identity is verified via one of several authentication types.</li>
 	<li>Then the user is issued an access token, which contains information about the security groups to which the user belongs.</li>
 	<li>When the user tries to access a network resource (open a file, print to a printer, etc.), the access control list (ACL) associated with that resource is checked against the access token.</li>
 	<li>If the ACL shows that members of the Managers group have permission to access the resource, and the user’s access token shows that he or she is a member of the Managers group, that user will be granted access (unless the user’s account, or a group to which the user belongs, has been explicitly <em>denied </em>access to the resource).</li>
</ol>
<u><a href="https://technet.microsoft.com/en-gb/library/dn751046.aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-gb/library/dn751046.aspx</a></u>

The Windows platform capitalizes on the ability to use a single user identity (maintained by Active Directory) across the network by locally caching user credentials in the operating system’s Local Security Authority (LSA). When a user logs on to the domain, Windows authentication packages transparently use the credentials to provide single sign-on when authenticating the credentials to network resources. For more information about credentials, see <u><a href="https://technet.microsoft.com/en-gb/library/dn751047.aspx" target="_blank" rel="noopener">Credentials Processes in Windows Authentication</a></u>.
<h2>Security principals and accounts</h2>
In Windows, any user, service, group, or computer that can initiate action is a security principal. Security principals have accounts, which can be local to a computer or be domain-based. For example, Windows client domain-joined computers can participate in a network domain by communicating with a domain controller even when no human user is logged on. To initiate communications, the computer must have an active account in the domain. Before accepting communications from the computer, the local security authority on the domain controller authenticates the computer’s identity, and then defines the computer’s security context just as it would for a human security principal. This security context defines the identity and capabilities of a user or service on a particular computer or a user, service, group, or computer on a network. For example, it defines the resources, such as a file share or printer, that can be accessed and the actions, such as Read, Write, or Modify, that can be performed by a user, service, or computer on that resource. For more information, see <u><a href="https://technet.microsoft.com/en-gb/library/dn486814.aspx" target="_blank" rel="noopener">Security Principals Technical Overview</a></u>.

Users, groups of users, objects, and services can all have individual accounts or share accounts. Accounts can be member of groups and can be assigned specific rights and permissions. Accounts can be restricted to the local computer, workgroup, network, or be assigned membership to a domain.
<h3><strong>security groups</strong></h3>
Built-in accounts and the security groups, of which they are members, are defined on each version of Windows. By using security groups, you can assign the same security permissions to many users who are successfully authenticated, which simplifies access administration.

This process ensures consistent security permissions across all members of a group. By using security groups to assign permissions means that access control of resources remains constant and easy to manage and audit. By adding and removing users who require access from the appropriate security groups as needed, you can minimize the frequency of changes to access control lists (ACLs).

Standalone managed service accounts and virtual accounts were introduced in Windows Server 2008 R2 and Windows 7 to provide necessary applications, such as Microsoft Exchange Server and Internet Information Services (IIS), with the isolation of their own domain accounts, while eliminating the need for an administrator to manually administer the service principal name (SPN) and credentials for these accounts. Group managed service accounts were introduced in Windows Server 2012 and provides the same functionality within the domain but also extends that functionality over multiple servers. When connecting to a service hosted on a server farm, such as Network Load Balance, the authentication protocols supporting mutual authentication require that all instances of the services use the same principal.

<u><a href="http://dba.stackexchange.com/questions/72858/what-are-the-risks-if-any-of-sharing-a-service-account-on-more-than-one-server" target="_blank" rel="noopener">http://dba.stackexchange.com/questions/72858/what-are-the-risks-if-any-of-sharing-a-service-account-on-more-than-one-server</a></u>

Risk mitigation would indicate creating a separate account for each service on each machine. The level of work required to create the accounts necessary is extremely minimal, but the <em>unknown</em> risks that accompany not doing so are quite high, according to Microsoft's own recommendations.

Microsoft Best Practices recommend using separate service accounts for all services.

Isolate Services

Isolating services reduces the risk that one compromised service could be used to compromise others. To isolate services, consider the following guidelines:

Run separate SQL Server services under separate Windows accounts. Whenever possible, use separate, low-rights Windows or Local user accounts for each SQL Server service. For more information, see Configure Windows Service Accounts and Permissions.

Security Note: Always run SQL Server services by using the lowest possible user rights. Use a MSA or virtual account when possible. When MSA and virtual accounts are not possible, use a specific low-privilege user account or domain account instead of a shared account for SQL Server services. Use separate accounts for different SQL Server services. Do not grant additional permissions to the SQL Server service account or the service groups. Permissions will be granted through group membership or granted directly to a service SID, where a service SID is supported.

"MSA" in the above paragraph refers to "Managed Service Accounts" which is the default for installations on Windows 7 or Windows Server 2008 R2 and above. Managed Service Accounts are defacto unique to each machine.

<u><a href="https://servergeeks.wordpress.com/2012/10/29/service-account-in-ad/" target="_blank" rel="noopener">https://servergeeks.wordpress.com/2012/10/29/service-account-in-ad/</a></u>
<table>
<tbody>
<tr>
<td>Account

Type</td>
<td>Description</td>
</tr>
<tr>
<td>Built-in local user account</td>
<td>A built-in user account is a user account that is created automatically during installation. The following three built-in user accounts are used by most services:

The Local System account (also called the System account) is a member of the local Administrators group.

The Local Service account has access rights similar to members of the Users group. This account accesses network services using a null session with no credentials. For this reason, this account might not provide sufficient network access for some services.

The Network Service account has access rights similar to members of the Users group. This account accesses network resources using the credentials of the computer account.

When using built-in local user accounts:

Accounts are automatically created.

You do not need to manage or reset account passwords.

Multiple services use the same user account, making it difficult to customize security for a specific service.</td>
</tr>
<tr>
<td>Domain user account</td>
<td>You can create domain user accounts for use by services. With domain user accounts:

User accounts are managed centrally in Active Directory.

You can create a single user account for a single service, or share a user account for multiple services.

You can grant only the specific privileges required by the service.

You must manage account passwords. For example, you will need to periodically reset the account password on the account as well as reset the password used by the service.</td>
</tr>
<tr>
<td>Managed service account

<img class="wp-image-1095" src="/wp-content/uploads/2018/03/image1-3.png" alt="image1 3" />

AND

&nbsp;

Virtual account</td>
<td>A managed service account is a new account type available in Windows Server 2008 R2 and Windows 7. A managed service account provides the same benefits of using a domain user account with these improvements:

Passwords are managed and reset automatically.

When the domain is running at the Windows Server 2008 R2 functional level, the service principal name (SPN) doesn’t need to be managed as with local accounts.

When using a managed service account:

A user account can be used on only one computer (you must create at least one account per computer).

<img class="wp-image-1090" src="/wp-content/uploads/2018/03/image2.png" alt="image2" />

Each account can be used by multiple services on a computer. You can also create a separate account for each service.

A virtual account is a new account type available in Windows Server 2008 R2 and Windows 7 Virtual accounts:

Are not created or deleted.

Use a single account for a single service. If you have multiple services that use virtual accounts, there will be a different account for each service.

To configure a service to use a virtual service account, simply edit the service properties and configure the account to use an account name of NT SERVICE<em>ServiceName </em>(where<em>ServiceName </em>matches the name of the service).</td>
</tr>
</tbody>
</table>
<h2>Authentication in trust relationships between domains</h2>
Most organizations that have more than one domain have a legitimate need for users to access shared resources that are located in a different domain, just as the traveler is permitted travel to different regions in the country. Controlling this access requires that users in one domain can also be authenticated and authorized to use resources in another domain.

To provide authentication and authorization capabilities between clients and servers in different domains, there must be a trust between the two domains. Trusts are the underlying technology by which secured Active Directory communications occur and are an integral security component of the Windows Server network architecture.

When a trust exists between two domains, the authentication mechanisms for each domain trust the authentications coming from the other domain. Trusts help provide for controlled access to shared resources in a resource domain—the trusting domain—by verifying that incoming authentication requests come from a trusted authority—the trusted domain. In this way, trusts act as bridges that let only validated authentication requests travel between domains.

How a specific trust passes authentication requests depends on how it is configured. Trust relationships can be one-way, by providing access from the trusted domain to resources in the trusting domain, or two-way, by providing access from each domain to resources in the other domain. Trusts are also either nontransitive, in which case trust exists only between the two trust partner domains, or transitive, in which case trust automatically extends to any other domains that either of the partners trusts.
<h2>Service Accoun<strong>ts</strong></h2>
A service account is a user account that is created explicitly to provide a security context for services running on Windows Server operating systems. The security context determines the service's ability to access local and network resources. The Windows operating systems rely on services to run various features. These services can be configured through the applications, the Services snap-in, or Task Manager, or by using Windows PowerShell.
<ul>
 	<li><u><a href="https://technet.microsoft.com/en-gb/library/dn617203.aspx#BKMK_StandaloneManagedServiceAccounts" target="_blank" rel="noopener">Standalone managed service accounts</a></u></li>
 	<li><u><a href="https://technet.microsoft.com/en-gb/library/dn617203.aspx#BKMK_GroupManagedServiceAccounts" target="_blank" rel="noopener">Group managed service accounts</a></u></li>
 	<li><u><a href="https://technet.microsoft.com/en-gb/library/dn617203.aspx#BKMK_VirtualServiceAccounts" target="_blank" rel="noopener">Virtual accounts</a></u></li>
</ul>
<h3>Standalone managed service accounts</h3>
A managed service account is designed to isolate domain accounts in crucial applications, such as Internet Information Services (IIS), and eliminate the need for an administrator to manually administer the service principal name (SPN) and credentials for the accounts.

To use managed service accounts, the server on which the application or service is installed must be running at least <u>Windows Server 2008 R2</u>. One managed service account can be used for services on a single computer. Managed service accounts <u>cannot be shared between multiple computers</u>, and they cannot be used in server clusters where a service is replicated on <u>multiple cluster nodes</u>. For this scenario, you must use a group managed service account.
<h3>Group managed service accounts</h3>
Group managed service accounts are an extension of the standalone managed service accounts, which were introduced in Windows Server 2008 R2. These are managed domain accounts that provide automatic password management and simplified service principal name (SPN) management, including delegation of management to other administrators.

When connecting to a service that is hosted on a server farm, such as Network Load Balancing, the authentication <u>protocols that support mutual authentication require all instances of the services to use the same principal</u>. When group managed service accounts are used as service principals, the Windows Server operating system manages the password for the account instead of relying on the administrator to manage the password.
<h3>Virtual accounts</h3>
Virtual accounts were introduced in Windows Server 2008 R2 and Windows 7, and are managed local accounts that provide the following features to simplify service administration:
<ul>
 	<li>The virtual account is automatically managed.</li>
 	<li>The virtual account can access the network in a domain environment.</li>
 	<li>No password management is required. For example, if the default value is used for the service accounts during SQL Server setup on Windows Server 2008 R2, a virtual account that uses the instance name as the service name is established in the format NT SERVICE&lt;SERVICENAME&gt;.</li>
</ul>
Services that run as virtual accounts access network resources by using the credentials of the computer account in the format &lt;domain_name&gt;&lt;computer_name&gt;$.
<h2><strong>Authentication methods and protocols
</strong></h2>
There are a large number of authentication methods and protocols that can be used, depending on the application and security requirements. In the following sections, we will discuss:
<h3>User authentication methods</h3>
<ul>
 	<li>Kerberos</li>
 	<li>SSL</li>
 	<li>Microsoft NTLM</li>
</ul>
<h3>Remote authentication</h3>
<ul>
 	<li>The Password Authentication Protocol (PAP)</li>
 	<li>The Shiva PAP (SPAP)</li>
 	<li>Challenge Handshake Authentication Protocol (CHAP)</li>
 	<li>Microsoft CHAP (MS-CHAP)</li>
 	<li>The Extensible Authentication Protocol (EAP)</li>
</ul>
<h3>Other authentication methods</h3>
<ul>
 	<li>RADIUS</li>
 	<li>Certificate services</li>
</ul>
<strong>Kerberos
</strong>Kerberos was developed at MIT to provide secure authentication for UNIX networks. It has become an Internet standard and is supported by Microsoft’s latest network operating system, Windows 2000. Kerberos uses temporary certificates called tickets, which contain the credentials that identify the user to the servers on the network. In the current version of Kerberos, v5, the data contained in the tickets is encrypted, including the user’s password.

A Key Distribution Center (KDC) is a service that runs on a network server, which issues a ticket called a Ticket Granting Ticket (TGT) to the clients that authenticates to the Ticket Granting Service (TGS). The client uses this TGT to access the TGS (which can run on the same computer as the KDC). The TGS issues a service or session ticket, which is used to access a network service or resource.

<strong>Microsoft NTLM (NT LAN Manager)
</strong>NTLM authentication is used by Windows NT servers to authenticate clients to an NT domain. Windows 2000 uses <u>Kerberos authentication by default but retains support for NTLM for authentication of pre-Windows 2000</u> Microsoft servers and clients on the network. UNIX machines connecting to Microsoft networks via an SMB client also use NTLM to authenticate.

NTLM uses a method called challenge/response, using the credentials that were provided when the user logged on each time that user tries to access a resource. This means the user’s credentials do not get transferred across the network when resources are accessed, which increases security. The client and server must reside in the same domain or there must be a trust relationship established between their domains in order for authentication to succeed.

Secure Sockets Layer (SSL) <u><a href="http://developer.netscape.com/docs/manuals/security/sslin/index.htm" target="_blank" rel="noopener">http://developer.netscape.com/docs/manuals/security/sslin/index.htm</a></u>
The SSL protocol is another Internet standard, often used to provide secure access to Web sites, using a combination of public key technology and secret key technology. Secret key encryption (also called symmetric encryption) is faster, but asymmetric public key encryption provides for better authentication, so SSL is designed to benefit from the advantages of both. It is supported by Microsoft, Netscape, and other major browsers, and by most Web server software, such as IIS and Apache.

SSL operates at the application layer of the DoD networking model. This means applications must be written to use it, unlike other security protocols (such as IPSec) that operate at lower layers. The Transport Layer Security (TLS) Internet standard is based on SSL.

SSL authentication is <u>based on digital certificates that allow Web servers and clients to verify each other’s identities before they establish a connection</u>. (This is called <strong>mutual authentication</strong>.) Thus, two types of certificates are used: client certificates and server certificates.

Certificate services
Digital certificates consist of data that is used for authentication and securing of communications, especially on unsecured networks (for example, the Internet). Certificates associate a public key to a user or other entity (a computer or service) that has the corresponding private key.

Certificates are issued by certification authorities (CAs), which are trusted entities that “vouch for” the identity of the user or computer. The CA digitally signs the certificates it issues, using its private key. The certificates are only valid for a specified time period; <u>when a certificate expires, a new one must be issued. The issuing authority can also revoke certificates</u>.

Certificate services are part of a network’s Public Key Infrastructure (PKI). Standards for the most commonly used certificates are based on the X.509 specifications.

<strong>Single Sign-On (SSO)
</strong>Single Sign-On (SSO) is a feature that allows a user to use one password (or smart card) to authenticate to multiple servers on a network without reentering credentials. This is an obvious convenience for users, who don’t have to remember multiple passwords or keep going through the authentication process over and over to access different resources.
<h1><strong>Windows Authentication</strong></h1>
<u><a href="https://technet.microsoft.com/en-gb/library/hh831472.aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-gb/library/hh831472.aspx</a></u>

In a networking context, <u>authentication is the act of proving identity to a network application or resource</u>. Typically, identity is proven by a cryptographic operation that uses either a key only the user knows — as with public key cryptography — or a shared key. The server side of the authentication exchange compares the signed data with a known cryptographic key to validate the authentication attempt.

Storing the cryptographic keys in a secure central location makes the authentication process scalable and maintainable. <u>Active Directory Domain Services is the recommended and default technology for storing identity information (including the cryptographic keys that are the user’s’ credentials).</u> Active Directory is required for default NTLM and Kerberos implementations.

The Windows operating system implements a default set of authentication protocols, including Kerberos, NTLM, Transport Layer Security/Secure Sockets Layer (TLS/SSL), and Digest, as part of an extensible architecture.
<h2>Server Manager</h2>
Many authentication features can be configured using <u>Group Policy</u>, which can be installed <u>using Server Manager</u>. The Windows Biometric Framework feature is installed using Server Manager. Other server roles which are dependent upon authentication methods, such as Web Server (IIS) and Active Directory Domain Services, can also be installed using Server Manager.

<u><a href="https://technet.microsoft.com/en-gb/library/dn751044.aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-gb/library/dn751044.aspx</a></u>

The Local Security Authority (LSA) is a protected subsystem that authenticates and signs in users to the local computer. In addition, LSA maintains information about all aspects of local security on a computer (these aspects are collectively known as the <u>local security policy</u>). It also provides various services for translation between names and security identifiers (SIDs).

The security subsystem keeps track of the security policies and the accounts that are on a computer system. In the case of a domain controller, these policies and accounts are those that are in effect for the domain in which the domain controller is located. These policies and accounts are stored in Active Directory. The LSA subsystem provides services for validating access to objects, checking user rights, and generating audit messages.
<h2><strong>SSPI</strong></h2>
In Windows Server, <u>applications authenticate users by using the </u><em><a href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms721625(v=vs.85).aspx#_security_security_support_provider_interface_gly" target="_blank" rel="noopener">Security Support Provider Interface</a></em> (SSPI) <u>to abstract calls for authentication</u>. SSPI functions as a common interface to several Security Support Providers (SSPs):<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-1" target="_blank" rel="noopener">[1]</a></u> A Security Support Provider is a <u><a href="https://en.wikipedia.org/wiki/Dynamic-link_library" target="_blank" rel="noopener">dynamic-link library</a></u> (DLL) that makes one or more security packages available to applications. Thus, developers do not need to understand the complexities of specific authentication protocols or build authentication protocols into their applications.

The following SSPs are installed with Windows: <u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface" target="_blank" rel="noopener">https://en.wikipedia.org/wiki/Security_Support_Provider_Interface</a></u>
<ul>
 	<li><u><a href="https://en.wikipedia.org/wiki/NTLMSSP" target="_blank" rel="noopener">NTLM</a></u> (Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_NT_3.51" target="_blank" rel="noopener">Windows NT 3.51</a></u>) (msv1_0.dll) - Provides <u><a href="https://en.wikipedia.org/wiki/NTLM" target="_blank" rel="noopener">NTLM</a></u> challenge/response authentication for client-server domains prior to <u><a href="https://en.wikipedia.org/wiki/Windows_2000" target="_blank" rel="noopener">Windows 2000</a></u> and for non-domain authentication (<u><a href="https://en.wikipedia.org/wiki/Server_Message_Block" target="_blank" rel="noopener">SMB</a></u>/CIFS).<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-2" target="_blank" rel="noopener">[2]</a></u></li>
 	<li><u><a href="https://en.wikipedia.org/wiki/Kerberos_(protocol)" target="_blank" rel="noopener">Kerberos</a></u> (Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_2000" target="_blank" rel="noopener">Windows 2000</a></u> and updated in <u><a href="https://en.wikipedia.org/wiki/Windows_Vista" target="_blank" rel="noopener">Windows Vista</a></u> to support <u><a href="https://en.wikipedia.org/wiki/Advanced_Encryption_Standard" target="_blank" rel="noopener">AES</a></u>) <u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-3" target="_blank" rel="noopener">[3]</a></u> (kerberos.dll) - Preferred for mutual client-server domain authentication in Windows 2000 and later.<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-4" target="_blank" rel="noopener">[4]</a></u></li>
 	<li><u><a href="https://en.wikipedia.org/wiki/SPNEGO" target="_blank" rel="noopener">Negotiate</a></u> (Introduced in Windows 2000) (secur32.dll) - Selects Kerberos and if not available, NTLM protocol. Negotiate SSP provides <u><a href="https://en.wikipedia.org/wiki/Single_sign-on" target="_blank" rel="noopener">single sign-on</a></u> capability, sometimes referred to as <u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication" target="_blank" rel="noopener">Integrated Windows Authentication</a></u> (especially in the context of IIS).<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-5" target="_blank" rel="noopener">[5]</a></u> On <u><a href="https://en.wikipedia.org/wiki/Windows_7" target="_blank" rel="noopener">Windows 7</a></u> and later, NEGOExts is introduced which negotiates the use of installed custom SSPs which are supported on the client and server for authentication.</li>
 	<li>Secure Channel (aka SChannel) - Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_2000" target="_blank" rel="noopener">Windows 2000</a></u> and updated in <u><a href="https://en.wikipedia.org/wiki/Windows_Vista" target="_blank" rel="noopener">Windows Vista</a></u> to support stronger AES encryption and <u><a href="https://en.wikipedia.org/wiki/Elliptic_curve_cryptography" target="_blank" rel="noopener">ECC</a></u> <u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-6" target="_blank" rel="noopener">[6]</a></u> This provider uses SSL/TLS records to encrypt data payloads. (schannel.dll)</li>
 	<li><u><a href="https://en.wikipedia.org/wiki/Private_Communications_Technology" target="_blank" rel="noopener">PCT</a></u> (obsolete) and Microsoft's implementation of <u><a href="https://en.wikipedia.org/wiki/TLS/SSL" target="_blank" rel="noopener">TLS/SSL</a></u> - <u><a href="https://en.wikipedia.org/wiki/Public_key_cryptography" target="_blank" rel="noopener">Public key cryptography</a></u> SSP that provides encryption and secure communication for authenticating clients and servers over the internet.<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-7" target="_blank" rel="noopener">[7]</a></u> Updated in Windows 7 to support TLS 1.2.</li>
 	<li><u><a href="https://en.wikipedia.org/wiki/Digest_access_authentication" target="_blank" rel="noopener">Digest SSP</a></u> (Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_XP" target="_blank" rel="noopener">Windows XP</a></u>) (wdigest.dll) - Provides challenge/response based HTTP and <u><a href="https://en.wikipedia.org/wiki/Simple_Authentication_and_Security_Layer" target="_blank" rel="noopener">SASL</a></u> authentication between Windows and non-Windows systems where Kerberos is not available.<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-8" target="_blank" rel="noopener">[8]</a></u></li>
 	<li>Credential (CredSSP) (Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_Vista" target="_blank" rel="noopener">Windows Vista</a></u> and available on Windows XP SP3) (credssp.dll) - Provides SSO and <u><a href="https://en.wikipedia.org/wiki/Network_Level_Authentication" target="_blank" rel="noopener">Network Level Authentication</a></u> for <u><a href="https://en.wikipedia.org/wiki/Remote_Desktop_Services" target="_blank" rel="noopener">Remote Desktop Services</a></u>.<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-9" target="_blank" rel="noopener">[9]</a></u></li>
 	<li>Distributed Password Authentication (DPA) - (Introduced in Windows 2000) (msapsspc.dll) - Provides internet authentication using <u><a href="https://en.wikipedia.org/wiki/Public_key_certificate" target="_blank" rel="noopener">digital certificates</a></u>.<u><a href="https://en.wikipedia.org/wiki/Security_Support_Provider_Interface#cite_note-10" target="_blank" rel="noopener">[10]</a></u></li>
 	<li>Public Key Cryptography User-to-User (PKU2U) (Introduced in <u><a href="https://en.wikipedia.org/wiki/Windows_7" target="_blank" rel="noopener">Windows 7</a></u>) (pku2u.dll) - Provides peer-to-peer authentication using digital certificates between systems that are not part of a domain.</li>
</ul>
SSPI is the implementation and proprietary variant of the Generic Security Service API (GSSAPI). SSPI provides a mechanism by which a distributed application can call one of several security providers to obtain an authenticated connection without knowledge of the details of the security protocol.
<h2>Integrated Windows Authentication (IWA)<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-1" target="_blank" rel="noopener">[1]</a></u><strong> </strong></h2>
<u><a href="https://technet.microsoft.com/library/cc758557(v=WS.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/library/cc758557(v=WS.10).aspx</a></u>

(formerly called NTLM, and also known as Windows NT Challenge/Response authentication). IWA is also known by several names like <em><a href="https://en.wikipedia.org/wiki/HTTP" target="_blank" rel="noopener">HTTP</a></em><em> </em><em>Negotiate authentication</em>, <em>NT Authentication</em>,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-2" target="_blank" rel="noopener">[2]</a></u> <em>NTLM Authentication</em>,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-3" target="_blank" rel="noopener">[3]</a></u> <em>Domain authentication</em>,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-4" target="_blank" rel="noopener">[4]</a></u> <em>Windows Integrated Authentication</em>,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-5" target="_blank" rel="noopener">[5]</a></u> <em>Windows NT Challenge/Response authentication</em>,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-6" target="_blank" rel="noopener">[6]</a></u> or simply <em>Windows Authentication</em>.

The term is used more commonly for the automatically authenticated connections between Microsoft <u><a href="https://en.wikipedia.org/wiki/Internet_Information_Services" target="_blank" rel="noopener">Internet Information Services</a></u>, <u><a href="https://en.wikipedia.org/wiki/Internet_Explorer" target="_blank" rel="noopener">Internet Explorer</a></u>, and other <u><a href="https://en.wikipedia.org/wiki/Active_Directory" target="_blank" rel="noopener">Active Directory</a></u> aware applications.

The current Windows user information on the client computer is supplied by the web browser through a cryptographic exchange involving hashing with the Web server. Unlike Basic or Digest authentication, initially, it does not prompt users for a user name and password. If the authentication exchange initially fails to identify the user, the web browser will prompt the user for a Windows user account user name and password.

Integrated Windows Authentication works with most modern web browsers,<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-8" target="_blank" rel="noopener">[8]</a></u> but <u>does not work over some HTTP </u><u><a href="https://en.wikipedia.org/wiki/Proxy_server" target="_blank" rel="noopener">proxy servers</a></u>.<u><a href="https://en.wikipedia.org/wiki/Integrated_Windows_Authentication#cite_note-iisDocumentation-7" target="_blank" rel="noopener">[7]</a></u> Therefore, it is best for use in <u><a href="https://en.wikipedia.org/wiki/Intranet" target="_blank" rel="noopener">intranets</a></u> where all the clients are within a single <u><a href="https://en.wikipedia.org/wiki/Windows_Server_domain" target="_blank" rel="noopener">domain</a></u>. It may work with other web browsers if they have been configured to pass the user's logon credentials to the server that is requesting authentication. Where a proxy itself requires NTLM authentication, some applications like Java may not work because the protocol is not described in RFC-2069 for proxy authentication.
<h2><strong>Authentication Goals and Plan</strong></h2>
Windows provides many different methods to achieve this goal as described below.
<table>
<tbody>
<tr>
<td><strong>To…</strong></td>
<td><strong>Feature</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td>Authenticate within an Active Directory domain</td>
<td>Kerberos</td>
<td>Windows Server implement the Kerberos version 5 authentication protocol and extensions for public key authentication. The Kerberos authentication client is implemented as a (SSP) and can be accessed through the (SSPI). Initial user authentication is integrated with the Winlogon single sign-on architecture. The <u>(KDC) is integrated with other Windows Server security services running on the domain controller</u>. The KDC uses the domain’s Active Directory directory service database as its security account database. Active Directory is required for default Kerberos implementations.

For additional resources, see <u><a href="https://technet.microsoft.com/en-gb/library/hh831553.aspx" target="_blank" rel="noopener">Kerberos Authentication Overview</a></u>.</td>
</tr>
<tr>
<td>Secure authentication on the web</td>
<td>TLS/SSL as implemented in the Schannel Security Support Provider</td>
<td>The (TLS) protocol versions 1.0, 1.1, and 1.2, (SSL) protocol, versions 2.0 and 3.0, Datagram Transport Layer Security protocol version 1.0, and the Private Communications Transport (PCT) protocol, version 1.0, are based on public key cryptography. The Secure Channel (Schannel) provider authentication protocol suite provides these protocols. All Schannel protocols use a client and server model.

For additional resources, see <u><a href="https://technet.microsoft.com/en-gb/library/hh831381.aspx" target="_blank" rel="noopener">TLS/SSL (Schannel SSP) Overview</a></u>.</td>
</tr>
<tr>
<td>Authenticate to a web service or application</td>
<td>Integrated Windows Authentication

Digest Authentication</td>
<td>For additional resources, see <u><a href="https://technet.microsoft.com/library/cc758557(v=WS.10).aspx" target="_blank" rel="noopener">Integrated Windows Authentication</a></u> and <u><a href="https://technet.microsoft.com/library/cc738318(v=ws.10).aspx" target="_blank" rel="noopener">Digest Authentication</a></u>, and <u><a href="https://technet.microsoft.com/library/cc783131(v=ws.10).aspx" target="_blank" rel="noopener">Advanced Digest Authentication</a></u>.</td>
</tr>
<tr>
<td>Authenticate to legacy applications</td>
<td>NTLM</td>
<td>NTLM is a challenge-response style authentication protocol.In addition to authentication, the NTLM protocol optionally provides for session security—specifically message integrity and confidentiality through signing and sealing functions in NTLM.

For additional resources, see <u><a href="https://technet.microsoft.com/en-gb/library/hh831571.aspx" target="_blank" rel="noopener">NTLM Overview</a></u>.</td>
</tr>
<tr>
<td>Leverage multifactor authentication</td>
<td>Smart card support

Biometric support</td>
<td>Smart cards are a tamper-resistant and portable way to provide security solutions for tasks such as client authentication, logging on to domains, code signing, and securing e-mail.

Biometrics relies on measuring an unchanging physical characteristic of a person to uniquely identify that person. Fingerprints are one of the most frequently used biometric characteristics, with millions of fingerprint biometric devices that are embedded in personal computers and peripherals.

For additional resources, see <u><a href="https://technet.microsoft.com/en-gb/library/hh831433.aspx" target="_blank" rel="noopener">Smart Card Overview</a></u> and <u><a href="https://technet.microsoft.com/en-gb/library/hh831396.aspx" target="_blank" rel="noopener">Windows Biometric Framework Overview [W8]</a></u>.</td>
</tr>
<tr>
<td>Provide local management, storage and reuse of credentials</td>
<td>Credentials management

Local Security Authority

Passwords</td>
<td>Credential management in Windows ensures that credentials are stored securely. Credentials are collected on the Secure Desktop (for local or domain access), through apps or through websites so that the correct credentials are presented every time a resource is accessed.

For additional resources, see <u><a href="https://technet.microsoft.com/en-gb/library/hh994565.aspx" target="_blank" rel="noopener">Cached and Stored Credentials Technical Overview</a></u> and <u><a href="https://technet.microsoft.com/en-gb/library/hh831800.aspx" target="_blank" rel="noopener">Passwords Overview</a></u>.</td>
</tr>
<tr>
<td>Extend modern authentication protection to legacy systems</td>
<td>Extended Protection for Authentication</td>
<td>This feature enhances the protection and handling of credentials when authenticating network connections by using Integrated Windows Authentication (IWA).

For additional resources, see <u><a href="http://support.microsoft.com/kb/968389" target="_blank" rel="noopener">Extended Protection for Authentication</a></u>.</td>
</tr>
</tbody>
</table>
<h2><strong>Authentication types</strong></h2>
<u>Basic Authentication</u>

<u><a href="https://technet.microsoft.com/en-us/library/cc784037(v=ws.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-us/library/cc784037(v=ws.10).aspx</a></u><u> </u>

The Basic authentication method is a <u>widely used industry-standard method</u> for collecting user name and password information. When you use Basic authentication, the browser displays a dialog box into which users are required to enter a previously assigned Windows account user name — which includes a Windows domain name, for example, Domain1User1 — and password, which are also known as <em>credentials</em>. The browser then attempts to establish a connection to a server using the user's credentials. The plaintext password is Base64-encoded before it is sent over the network. Basic authentication is not recommended unless you are confident that the connection between the user and your Web server has been secured, for example, with a dedicated line or an SSL connection.

<u>Digest authentication </u><u><a href="https://technet.microsoft.com/en-us/library/cc738318(v=ws.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-us/library/cc738318(v=ws.10).aspx</a></u><u> </u>

Digest authentication offers the <u>same functionality as Basic authentication</u>; however, Digest authentication provides a security improvement because a user's credentials are not sent across the network in plaintext. Digest authentication <u>sends credentials across the network as a Message Digest 5 (MD5) hash</u>, which is also known as the MD5 message digest, in which the credentials cannot be deciphered from the hash.

<u>Advanced Digest authentication </u><u><a href="https://technet.microsoft.com/library/cc783131(v=ws.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/library/cc783131(v=ws.10).aspx</a></u><u> </u>

When Advanced Digest authentication is enabled, user credentials are stored on the domain controller as an MD5 hash. Advanced Digest authentication does not require that credentials are stored using reversible encryption. Instead, Advanced Digest authentication stores a few precalculated hashes in Active Directory, so user passwords cannot feasibly be discovered by anyone with access to the domain controller, including the domain administrator.

it is recommended over Digest authentication for the following reasons:
<ul>
 	<li>Subauthentication is not required for Advanced Digest authentication, because Advanced Digest authentication uses the Windows Security Support Provider Interface (SSPI) traditional implementation for security.</li>
 	<li>Reversible password encryption is not required for Advanced Digest authentication. In Windows Server 2003, the Active Directory extended schema properties ensure that every newly created user account automatically has the Advanced Digest authentication hashed and stored as a field in the AltSecId property of the user object.</li>
 	<li>A worker process with an application that uses Advanced Digest authentication does not have to run with LocalSystem as the process identity, because subauthentication is not required.</li>
</ul>
<u>Authentication for SQL Server</u>

Windows Authentication is the preferred method for users to authenticate to SQL Server.   In an Active Directory environment, <u>Kerberos authentication is always attempted first</u>. Kerberos authentication is not available for SQL Server 2005 clients using named pipes.
<h1><strong>Kerberos authentication</strong></h1>
<u><a href="http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx" target="_blank" rel="noopener">http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx</a></u>
<ul>
 	<li>Kerberos is the default method of network authentication for services in Windows Server 2003.</li>
 	<li><u>A service can use Kerberos, only if that service first registers a service principal name (SPN)</u> in Active Directory.</li>
 	<li>By default, Active Directory registers the NetBIOS, or computer, name of the server, but if the SPN is different, you must manually register the service.</li>
 	<li>Before Kerberos can authenticate a service, the <u>service must be registered on only one account object</u>. If the logon account name of a service instance changes, the service must be reregistered under the new account. Therefore, only one application pool that has the service registered can authenticate with Kerberos.</li>
</ul>
<h2><strong>Principal Names</strong></h2>
<ul>
 	<li>Kerberos defines two different types of accounts (or Principals). The two different names given to these types of accounts are User Principal Name (UPN), and Service Principal Name (SPN). We would typically relate these two types of principals to Active Directory users and computers.</li>
 	<li>Only user accounts have a UPN defined on their account. When looking at a user account if you click on the Account tab, the UPN is derived from the combining of the two fields listed for “User logon name”. A User Principal Name must be unique across the entire forest otherwise when the KDC goes to look up the Users Account via UPN it will get back more than one account and cause authentication failures for all users that have the same UPN. The UPN of an Active Directory object is an attribute of the object, and can only hold a single value. The attribute name is userPrincipalName. An example of a UPN is:<u><a target="_blank" rel="noopener">rob@contoso.com</a></u>.</li>
 	<li>Service Principal Names MUST be unique across the entire Active Directory forest, and <u>can be assigned to either User accounts or Computer accounts</u>. Only computer accounts automatically have Service Principal Names defined.</li>
</ul>
<h3><strong>Service Accounts</strong></h3>
<ul>
 	<li>Service Principal Names define what services run under the accounts security context. For example some of the services that a computer might have are File server / CIFS (Common Internet File System), if it is a domain controller it is going to have an LDAP SPN, and Active Directory Replication SPN, and FRS SPN. Service Principal Names can be defined on user accounts when a Service or application is running under that users Security context. Typically these types of user accounts are known as “Service Accounts”. It is very import that you understand that Service Principal Names MUST be unique throughout the entire Active Directory forest.</li>
 	<li>Some typical scenarios when a user account has a Service Principal Name defined are:
<ul>
 	<li>When SQL Server Service is using a user account or “Service Account” instead of the default of “LocalSystem”. An example is: MSSQLSvc/sqlsrvr.contoso.com:1433</li>
 	<li>When an IIS Web Application Pool is running as a specified user account rather than as the default of “Network Service”. An example is: http/websrvr.contoso.comSPN</li>
</ul>
</li>
</ul>
<u><a href="https://geertbaeten.wordpress.com/2013/06/03/kerberos-authentication-and-delegation-serviceprincipalnames/" target="_blank" rel="noopener">https://geertbaeten.wordpress.com/2013/06/03/kerberos-authentication-and-delegation-serviceprincipalnames/</a></u>

A service principal name (SPN) is the <u>name</u> by which a client uniquely identifies an instance of a service. The Kerberos authentication service <u>can use an SPN to authenticate a service</u>.

SPNs are unique identifiers for services that run on servers; they are registered with a service class that identifies the account’s type of service. The SPN identifies information such as the <u>computer on which the service runs, the account under which the service runs, and in some cases the port on which it runs</u>. There are host SPNs that cover default services, when the local system or network service built-in accounts are used and the URL uses the computer name.

<u><a href="http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx" target="_blank" rel="noopener">http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx</a></u>
<h2><strong>SPN Purpose</strong></h2>
A service principal name (SPN) is the name by which a Kerberos client uniquely identifies an instance of a service for a given Kerberos target computer. If you install multiple instances of a service on computers throughout a forest, each instance must have its own SPN. A <u>given service instance can have multiple SPNs if there are multiple names that clients might use for authentication</u>. For example, an SPN always includes the name of the host computer on which the service instance is running, so a service instance might register an SPN for each name or alias of its host.

An SPN tells the Kerberos system that a certain AD service account may access the service itself. In essence to elevate its rights from a dumb service account to an account with actual rights inside the service.

Sounds weird but I’ll try to give an example:

A user logs on to a webservice. The webservice itself connects to a SQL service. If I were to use standard behaviour then the user would access the webservice but when the webservice goes to the SQL, it has to do this with its own service account name.

This means I have to implement the security inside the webservice whilest I might want to delegate that to SQL (f.e. user 1 has dataset 1 and user 2 has a completely different dataset 2). The SQL sees the webservice service account logging on and can’t see which enduser is in fact the requestor. If however the webservice can log on to SQL using the enduser credentials then the problem is solved. This is called impersonation. The webservice creates a new connection to the SQL but impersonates the enduser. Of course you can see the security risk involved so therefor this kind of behaviour is blocked by default. By using SPNs and setting the delegation settings in AD, you can create an explicit “allow” for this app to behave that way. Impersonation is not the only reason to use SPNs but it is a common one.
<h2><strong>To add/list SPNs</strong></h2>
Some tools that can be used to list the Service Principal names on an Active Directory object are: LDP, LDIFDE (These two are great utilities if you want to query LDAP for all objects that have the SPN defined on them.), next is ADSIEdit, or SetSPN. The last two are great utilities if you want to see what SPNs are registered on a given object.

You have two options for configuring SPNs. You can use the Setspn command-line utility. If you prefer a GUI, you can open ADSI Edit from the Administrative Tools program group. Both of these tools install by default on a DC running Server 2008 or later. If you're running Windows 2003, these tools are available only when you install the<u><a href="http://technet.microsoft.com/en-us/library/baa79cdd-83b0-4f10-9356-b2d14462d5b2" target="_blank" rel="noopener">Windows Support Tools</a></u>. Regardless of which tool you use, you must be a domain administrator to configure SPNs.
<h3><strong>syntax</strong></h3>
<strong>   </strong>Add SPN: setspn -S <em>ServiceClass</em>/<em>Host</em>:<em>Port</em> <em>ServiceAccount</em>

List SPN:  setspn -L <em>ServiceAccount</em>
<ul>
 	<li>(The -S-option will check that there is no duplicate SPN before adding it to AD. Replaces the -A option used in the past).</li>
</ul>
Other common options: In our example we used a new command line switch, -S, introduced in Windows Server 2008 that checks for the existence of the SPN before creating the SPN on the account. If the SPN already exists, the new SPN is not created and you see an error message.

If duplicate SPNs are found, you have to resolve the issue by either using a different DNS name for the web application, thereby changing the SPN, or by removing the existing SPN from the account it was discovered on.
<ul>
 	<li>-D
<ul>
 	<li>Removes a previously set SPN</li>
</ul>
</li>
 	<li>-L
<ul>
 	<li>List the SPNs for a certain account</li>
</ul>
</li>
 	<li>-A
<ul>
 	<li>Add an SPN =&gt; similar to -S but -A does not verify if there is already a duplicate SPN</li>
 	<li>Warning: to avoid problems later on it is better to use -S; unless if you’re using an older version of Windows (2003 f.e.) as the -S option is not available there</li>
</ul>
</li>
</ul>
The parameters for this syntax include:
<ul>
 	<li>ServiceClass: There are different types of SPNs, and each service that runs on a computer must have the appropriate SPN service class assigned to it. If a  <u>Reporting Services service account is a domain account, you must use the HTTP SPN </u>service class.</li>
 	<li>Host: The host parameter specifies the name (either the computer name or a virtual name (alias)) on which the service is running. These names are defined by DNS Host records or your local Hostfile (host.ini). An <u>SPN must be set for each name that is referenced in a URL, such as the NetBIOS name or the fully qualified domain name</u> (FQDN).  Be aware that NetBIOS names are not guaranteed to be unique in a forest, so an SPN that contains a NetBIOS name may not be unique.</li>
</ul>
Example: If report server is hosted on server (Contoso), then you need SPNs for NetBIOS (Contoso) and FQDN (Contoso.Domain.Corp.Company.com).
<ul>
 	<li>Port: Specifies the port on which the service runs. An optional TCP or UDP port number to differentiate between multiple instances of the same service class on a single host computer. Omit this component if the service uses the default port for its service class. Although you can omit this for services that use a default port (such as port 80 for HTTP), it is recommended to always include this parameter. Port is required for other SPNs, but not for HTTP SPNs. To fix this issue you can configure Web sites (Reporting Services /SharePoint Sites) to use Host Header. This avoids conflicts between SPNs.</li>
 	<li>ServiceAccount: &lt;domain&gt;/&lt;accountname&gt; OR &lt;accountname&gt;@&lt;domain.tld&gt; Specifies the domain user name under which the service runs. If you are in a cross-domain environment, you must also include the domain in the <u>format </u><em>domainuser</em>. If you are using the <u>local system or network service built-in account with a virtual name, you must enter the machine name rather than a built-in account</u> for Service account.
<ul>
 	<li>The distinguished name or objectGUID of an object in Active Directory Domain Services, such as a service connection point (SCP).</li>
 	<li>The DNS name of the domain for a service that provides a specified service for a domain as a whole.</li>
 	<li>The DNS name of an SRV or MX record.</li>
</ul>
</li>
</ul>
<h2><strong>List of SPNs</strong></h2>
<u><a href="http://blogs.msdn.com/b/crm/archive/2009/08/06/configuring-service-principal-names.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/crm/archive/2009/08/06/configuring-service-principal-names.aspx</a></u>

There are well-known service class names, such as "www" for a Web service or "ldap" for a directory service. Do not configure service principal names with HTTPS even if the web application uses SSL.

Some typical services:
<ul>
 	<li>HOST/ (set automatically when adding a server to AD)</li>
 	<li>HTTP/ (see below)</li>
 	<li>MSSQLSvc/ (see below)</li>
</ul>
Not so typical:
<ul>
 	<li>LDAP/ (no need to tamper with this, ADDS will automatically set the correct ones)</li>
 	<li>DNS/ (idem if DNS is AD integrated)</li>
 	<li>GC/ (idem)</li>
</ul>
Examples of SPN registrations:
<ul>
 	<li><strong>HTTP/www.contoso.com</strong> – Any page on the Web site on the default TCP port 80 for www.contoso.com, that is<a href="http://www.contoso.com/" target="_blank" rel="noopener">http://www.contoso.com/</a><a href="http://www.contoso.com/" target="_blank" rel="noopener"> </a><img class="wp-image-1097" src="/wp-content/uploads/2018/03/image3.png" alt="image3" /><a href="http://www.contoso.com/" target="_blank" rel="noopener"> </a>.</li>
 	<li><strong>HTTP/www.contoso.com:8080</strong> – Any page on the Web site on the non-standard TCP port 8080 for www.contoso.com, that is http://www.contoso.com.</li>
 	<li><strong>HOST/WORKSTATION5</strong> - Any service running on the computer with NetBIOS name WORKSTATION5</li>
 	<li><strong>HOST/SERVER7.contoso.com</strong> - Any service running on the computer with hostname SERVER7.contoso.com</li>
 	<li><strong>TERMSRV/FRONTRM.contoso.com</strong> - The Remote Desktop Protocol (RDP) service running on the computer with hostname FRONTRM.contoso.com</li>
 	<li><strong>MSSQLSvc/SQLSERVER2.fabrikam.com:1433</strong> – The SQL Server listening on SQLSERVER2.fabrikam.com, port 1433.</li>
 	<li><strong>cifs/KHWIN7.fabrikam.com</strong> – The file share on the computer with hostname KHWIN7.fabrikam.com</li>
</ul>
<h3><strong>Built-in SPNs Recognized for Computer Accounts</strong></h3>
<u><a href="https://technet.microsoft.com/en-us/library/cc772815(WS.10).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-us/library/cc772815(WS.10).aspx</a></u>
<ul>
 	<li><u><a href="https://technet.microsoft.com/en-GB/library/cc731241.aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-GB/library/cc731241.aspx</a></u>
These SPNs are recognized for computer accounts if the computer has a host SPN. Unless they are explicitly placed on objects, a <u>host SPN can substitute for any of the above SPNs</u>.</li>
 	<li>Service Principal Names (SPNs) are <u>not case sensitive when used by Microsoft Windows-based computers</u>. However, an SPN can be used by any type of computer system. Many of these computer systems, especially <u>UNIX-based systems, are case-sensitive</u> and require the proper case to function properly. Care should be taken to use the proper case particularly when an SPN can be used by a non-Windows-based computer.</li>
</ul>
<table>
<tbody>
<tr>
<td><strong>SPN</strong></td>
<td><strong>SPN</strong></td>
<td><strong>SPN</strong></td>
<td><strong>SPN</strong></td>
</tr>
<tr>
<td>alerter</td>
<td>http</td>
<td>policyagent</td>
<td>scm</td>
</tr>
<tr>
<td>appmgmt</td>
<td>ias</td>
<td>protectedstorage</td>
<td>seclogon</td>
</tr>
<tr>
<td>browser</td>
<td>iisad</td>
<td>rasman</td>
<td>snmp</td>
</tr>
<tr>
<td>cifs</td>
<td>min</td>
<td>remoteaccess</td>
<td>spooler</td>
</tr>
<tr>
<td>cisvc</td>
<td>messenger</td>
<td>replicator</td>
<td>tapisrv</td>
</tr>
<tr>
<td>clipsrv</td>
<td>msiserver</td>
<td>rpc</td>
<td>time</td>
</tr>
<tr>
<td>dcom</td>
<td>mcsvc</td>
<td>rpclocator</td>
<td>trksvr</td>
</tr>
<tr>
<td>dhcp</td>
<td>netdde</td>
<td>rpcss</td>
<td>trkwks</td>
</tr>
<tr>
<td>dmserver</td>
<td>netddedsm</td>
<td>rsvp</td>
<td>ups</td>
</tr>
<tr>
<td>dns</td>
<td>netlogon</td>
<td>samss</td>
<td>w3svc</td>
</tr>
<tr>
<td>dnscache</td>
<td>netman</td>
<td>scardsvr</td>
<td>wins</td>
</tr>
<tr>
<td>eventlog</td>
<td>nmagent</td>
<td>scesrv</td>
<td>www</td>
</tr>
<tr>
<td>eventsystem</td>
<td>oakley</td>
<td>schedule</td>
<td></td>
</tr>
<tr>
<td>fax</td>
<td>plugplay</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>
<h1><strong>Impersonation </strong></h1>
Impersonation is a process in which user accesses the <strong>local</strong> resources(Ex:Files,DB…) by using the identity of another user. Local resources is important – if you want to access some files, then that’s fine, but if you want to access a <u>remote</u> database, you’re going to <u>need Delegation</u> as well.

<u><a href="https://msdn.microsoft.com/en-us/library/aa376391(VS.85).aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/aa376391(VS.85).aspx</a></u> <em><a href="https://msdn.microsoft.com/en-us/library/ms721588(v=vs.85).aspx#_security_impersonation_gly" target="_blank" rel="noopener">Impersonation</a></em> is the ability of a thread to execute using different security information than the process that owns the thread. Typically, a thread in a server application impersonates a client. This allows the server thread to act on behalf of that client to access objects on the server or validate access to the client's own objects.
<h1>Delegated authentication</h1>
<u><a href="https://msdn.microsoft.com/en-us/library/dd568720.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/dd568720.aspx</a></u><em> Delegation</em> is when a front-end service forwards a client request to a back-end service so that the back-end service can also impersonate the client. Impersonation is typically used to check whether a client is authorized to perform a particular action, while delegation is a way of flowing impersonation capabilities, along with the client’s identity, to a back-end service. You can use delegation as a Windows domain feature with Kerberos-based authentication.

In Windows, delegated authentication occurs when a network service accepts an authentication request from a user and assumes the identity of that user in order to initiate a new connection to a second network service. To support delegated authentication, you must establish front-end or first-tier servers, such as web servers, that are responsible for handling client authentication requests and back-end or n-tier servers, such as large databases, that are responsible for storing information. You can delegate the right to set up delegated authentication to users in your organization to reduce the administrative load on your administrators.
<h2><strong>Kerberos delegation </strong></h2>
Kerberos delegation is the act of principal (Service) impersonating another principal (user) to gain access to a 3rd principal (service). In other words, User connecting to an IIS Server that queries a SQL Server as the user who is requesting some data from the web server.

There are two different types of delegation.
<ul>
 	<li>Unconstrained (Windows 2000/2003/2008 Servers can do this type of delegation.)</li>
 	<li>Constrained (Windows 2003/2008 Servers in 2003 Domain Functional Level (or higher) can do this type of delegation.)</li>
</ul>
<h2>Constrained delegation</h2>
Constrained delegation gives administrators the ability to specify and enforce application trust boundaries by <u>limiting the scope where application services can act on behalf of a user</u>. You can specify particular services from which a computer that is trusted for delegation can request resources. The flexibility to constrain authorization rights for services helps improve application security design by reducing the opportunities for compromise by untrusted services.

For more information about constrained delegation, see <u><a href="https://technet.microsoft.com/en-gb/library/jj553400.aspx" target="_blank" rel="noopener">Kerberos Constrained Delegation Overview</a></u>.
<h2>Protocol transition</h2>
Protocol transition assists application designers by letting applications support different authentication mechanisms at the user authentication tier and by switching to the Kerberos protocol for security features, such as mutual authentication and constrained delegation, in the subsequent application tiers.
<h1><strong>Trusted Subsystem</strong></h1>
A trusted subsystem model is where the database server trusts the <u>Web application identity</u>. The Web application identity is trusted to make calls on behalf of the original caller. (See Figure 3.)

<img class="wp-image-1094" src="/wp-content/uploads/2018/03/image4.gif" alt="image4" />

<strong>Figure 3. Trusted subsystem model</strong>
<h2><strong>Trusted Subsystem Advantages</strong></h2>
The advantages of the trusted subsystem model include:
<ul>
 	<li><strong>Scalability.</strong> The trusted subsystem model supports <u>efficient connection pooling</u>. Connection pooling allows multiple clients to reuse available pooled connections. Connection pooling works with this model because all back-end resources accessed use the security context of the application's service account, regardless of the caller's identity.</li>
 	<li><strong>Minimal back-end ACL management.</strong> <u>Only the service account accesses back-end resources</u> (for example, databases). ACLs are configured for this single identity.</li>
 	<li><strong>No direct data access.</strong> In the trusted subsystem model, only the service account is granted access to the back-end resources. As a result, <u>users cannot directly access back-end data</u> without going through the application (and being subjected to application authorization).</li>
</ul>
<h2><strong>Trusted Subsystem Disadvantages</strong></h2>
The trusted subsystem model has the following disadvantages:
<ul>
 	<li><strong>Auditing.</strong> To perform auditing at the back end, <u>you can explicitly pass (at the application level) the identity of the original caller</u> to the back end, and have the auditing performed there. With this approach, you have to trust the middle tier and you have a potential <u>repudiation risk.</u> Alternatively, you can generate an audit trail in the middle tier, and then correlate it with back-end audit trails. To use this approach, you must ensure that the server clocks are synchronized.</li>
 	<li><strong>Increased risk from server compromise.</strong> In the trusted subsystem model, the <u>middle-tier service is granted broad access to back-end resources</u>. As a result, a compromised middle-tier service could make it easier for an attacker to gain broad access to back-end resources.</li>
</ul>
<h2><strong>Impersonation / Delegation vs. Trusted Subsystem</strong></h2>
When you design the authentication that you require in your application, consider whether to use impersonation to use the original caller's identity for access to back-end resources, or whether to use the trusted subsystem model, where the Web or application server is responsible for authenticating users and the server then uses a service identity to access back-end resources. The two techniques have different advantages and disadvantages as explained in the following subsections.
<h3>Impersonation / Delegation</h3>
The impersonation and delegation model also has advantages and disadvantages.
<h4><em>Impersonation / Delegation Advantages</em></h4>
The advantages of the impersonation / delegation model include:
<ul>
 	<li><strong>Auditing.</strong> You benefit from operating system auditing. This allows administrators to track which users have attempted to access specific resources.</li>
 	<li><strong>Auditing across tiers.</strong> The user's <u>security context is maintained across the physical tiers of your application</u>, which allows administrators to audit across tiers. Generally, auditing is considered most authoritative if the audits are generated at the precise time of resource access and by the same routines that access the resource.</li>
 	<li><strong>Granular access controls.</strong> You can configure granular access in the database. You can restrict individual user accounts independently of one another in the database.</li>
</ul>
<h4><em>Impersonation / Delegation Disadvantages</em></h4>
The disadvantages of the impersonation / delegation model include:
<ul>
 	<li><strong>Scalability. </strong>The impersonation / delegation model does not allow you to make efficient use of database connection pooling because database access is performed by using <u>connections that are tied to the individual security contexts of the original callers. This significantly limits the application's ability to scale to large numbers of users</u>.</li>
 	<li><strong>Increased administration effort.</strong> ACLs on back-end resources need to be maintained in such a way that <u>each user is granted the appropriate level of access</u>. When the number of back-end resources increases (and the number of users increases), a significant administration effort is required to manage ACLs.</li>
</ul>
<h1><strong>Implementing Delegation</strong></h1>
<u><a href="http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx" target="_blank" rel="noopener">http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx</a></u> <u><a href="https://msdn.microsoft.com/en-us/library/dd568720.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/dd568720.aspx</a></u>

The first step in setting up delegation is to create any necessary service principal names (SPN). To make delegation more secure, Active Directory uses Kerberos to authenticate services.

Why Kerberos ?

<u><a href="http://blogs.msdn.com/b/besidethepoint/archive/2010/05/09/double-hop-authentication-why-ntlm-fails-and-kerberos-works.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/besidethepoint/archive/2010/05/09/double-hop-authentication-why-ntlm-fails-and-kerberos-works.aspx</a></u>
<h2><strong>Delegation Requirements</strong></h2>
The following list describes the requirements for delegation.
<table>
<tbody>
<tr>
<td><strong>Location</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td>Client</td>
<td>
<ol>
 	<li>The requesting application must support the Kerberos authentication protocol.</li>
 	<li>The user account making the request must be configured on the domain controller. Confirm that the following option is not selected: <strong>Account is sensitive and cannot be delegated</strong>.</li>
</ol>
</td>
</tr>
<tr>
<td>Servers</td>
<td>
<ol>
 	<li>The service accounts must be trusted for delegation on the domain controller.</li>
 	<li>The service accounts must have SPNs registered on the domain controller. If the service account is a domain user account, the domain administrator must register the SPNs.</li>
</ol>
</td>
</tr>
</tbody>
</table>
<strong>Table 3:</strong> Delegation requirements in the Reporting Services deployment.

<strong>To verify settings for domain user accounts used to access reports/application</strong>
<ol>
 	<li>Go to the <strong>Control Panel</strong>.</li>
 	<li>From <strong>Administrative Tools</strong>,<strong> </strong>open <strong>Active Directory Users and Computers</strong>.</li>
 	<li>Locate the domain user account, right-click the user account, and then click <strong>Properties</strong>.</li>
 	<li>On the <strong>Account</strong> tab, under <strong>Account options</strong>, verify that the following option is not selected: <strong>Account is sensitive and cannot be delegated</strong>.</li>
</ol>
<img class="wp-image-1100" src="/wp-content/uploads/2018/03/image5.png" alt="image5" />

<strong>Figure 7: </strong>The <strong>Account</strong> tab in the <strong>User Properties</strong> dialog box

<strong>Note:</strong> If the <strong>Delegation</strong> tab is not visible, there is no SPN configured for the account. Add an SPN and then perform the procedure.

<strong>To verify the middle tier computer is trusted for delegation</strong>
<ol>
 	<li>Go to the <strong>Control Panel</strong>.</li>
 	<li>From <strong>Administrative Tools</strong>, open <strong>Active Directory Users and Computers</strong>.</li>
 	<li>Locate the middle tier computer. Right-click the computer, and then click <strong>Properties</strong>.</li>
 	<li>On the <strong>Delegation</strong> tab, verify that the following option is selected:<strong>Trust this computer for delegation to any service (Kerberos only)</strong></li>
</ol>
<img class="wp-image-1099" src="/wp-content/uploads/2018/03/image14.png" alt="image14" />

<strong>Figure 8: </strong>The <strong>Delegation </strong>tab in the <strong>Computer Properties </strong>dialog box.

<strong>To verify that the domain account used as the service account on the middle tier is trusted for delegation</strong>
<ol>
 	<li>Go to the <strong>Control Panel</strong>.</li>
 	<li>From <strong>Administrative Tools</strong>, open <strong>Active Directory Users and Computers</strong>.</li>
 	<li>Locate the domain account used as the service account, right-click the user account, and then click <strong>Properties. </strong></li>
 	<li>On the <strong>Delegation</strong> tab, verify that the following options is<strong> </strong>selected: <strong>Trust this computer for delegation to any service (Kerberos only)</strong>.</li>
</ol>
<img class="wp-image-1092" src="/wp-content/uploads/2018/03/image13.png" alt="image13" />

<strong>Figure 9: </strong>The <strong>Delegation</strong> tab in the <strong>SQL Service Properties</strong> dialog box
<h2><strong>Verify Service Account Group Membership or Local Security Policy Settings</strong></h2>
After installation, the Reporting Services Service Account SID is assigned to the SQLServerReportServerUser$Server$MSRS10.MSSQLSERVER local group, which is then assigned to the IIS group. If they are not added by default, add the account to the groups mentioned below.
<ul>
 	<li>IIS_WPG group (if you have a SharePoint integrated mode deployment and are using IIS 6.0).</li>
 	<li>IIS_IUSRS group (if you have a SharePoint integrated mode deployment and are using IIS 7.0).</li>
 	<li>The appropriate local policy rights (if you have a native mode deployment). The appropriate local policy rights are: Log on as a service; Access this computer from the network; and Impersonate a client after authentication.</li>
</ul>
The IIS_WPG user group provides the minimum set of privileges and permissions that are required to start and run worker processes in IIS. For more information about the IIS_WPG group, see <u><a href="http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/12a3d96c-65ea-4210-96ad-86a801f6a88c.mspx?mfr=true" target="_blank" rel="noopener">Configuring Application Pool Identity in IIS 6.0 (IIS 6.0)</a></u>.

<strong>To verify membership in the IIS_WPG or IIS_IUSRS group (IIS 6.0 or IIS 7.0 only)</strong>
<ol>
 	<li>On the middle tier computer or computers, open <strong>Local Users and Groups</strong>.</li>
 	<li>Click <strong>Start</strong>, point to <strong>Administrative Tools</strong>, and then click <strong>Computer Management</strong>.</li>
 	<li>In the tree, expand <strong>Local Users and Groups</strong>, and then click <strong>Groups</strong>.</li>
 	<li>Right-click <strong>IIS_WPG</strong> or <strong>IIS_IUSRS</strong>;<strong> </strong>verify that the <strong>Members</strong> list includes the service account.</li>
</ol>
<strong>To verify local policy rights</strong>
<ol>
 	<li>On the middle tier computer(s), open <strong>Local Security Policy</strong>.</li>
 	<li>Click <strong>Start</strong>, point to <strong>Administrative Tools</strong>, and then click <strong>Local Security Policy</strong>.</li>
 	<li>In the tree, expand <strong>Local Policies</strong>, and then click <strong>User Rights Assignment</strong>.</li>
 	<li>In the right pane, verify that the <strong>Security Setting</strong> column includes the service account next to the appropriate policies.</li>
</ol>
<h2><strong>Delegation Setting up for SQL Server</strong></h2>
<u><a href="http://blogs.msdn.com/b/psssql/archive/2010/06/23/my-kerberos-checklist.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/psssql/archive/2010/06/23/my-kerberos-checklist.aspx</a></u> <u><a href="http://blogs.msdn.com/b/psssql/archive/2010/03/09/what-spn-do-i-use-and-how-does-it-get-there.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/psssql/archive/2010/03/09/what-spn-do-i-use-and-how-does-it-get-there.aspx</a></u>
<h3><strong>Verifying the authentication</strong></h3>
[19:47:55] Sabarinathan Arthanari:

SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid;

[19:48:34] Sabarinathan Arthanari:

select c.session_id, s.login_name, c.auth_scheme, c.net_transport, st.text

from sys.dm_exec_connections c

JOIN sys.dm_exec_sessions s ON c.session_id = s.session_id

JOIN sys.dm_exec_requests r ON c.session_id = r.session_id

cross apply sys.dm_exec_sql_text(r.sql_handle) as st

If you need to get data to SSRS from a source (such as SQL Server or Analysis Services) that uses a different account to access the data, you must also add a SPN for that account. For example, if you have a report that pulls data from an Analysis Services cube, you must add the SPN using domain account that pulls the data. Use below links to know how to register SPNs for

SQL Server: <u><a href="http://support.microsoft.com/kb/319723" target="_blank" rel="noopener">http://support.microsoft.com/kb/319723</a></u>

<u><a href="http://technet.microsoft.com/en-us/library/ms191153.aspx" target="_blank" rel="noopener">http://technet.microsoft.com/en-us/library/ms191153.aspx</a></u>

Analysis Services: <u><a href="http://support.microsoft.com/kb/917409" target="_blank" rel="noopener">http://support.microsoft.com/kb/917409</a></u>

<u><a href="https://msdn.microsoft.com/en-gb/library/ms191153(v=sql.110).aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-gb/library/ms191153(v=sql.110).aspx</a></u>

To use Kerberos authentication with SQL Server requires both the following conditions to be true:
<ul>
 	<li>The client and server computers must be part of the <u>same Windows domain, or in trusted domains</u>.</li>
 	<li>A Service Principal Name (SPN) must be registered with Active Directory, which assumes the role of the Key Distribution Center in a Windows domain. <u>The SPN, after it is registered, maps to the Windows account that started the SQL Server instance service.</u> If the SPN registration has not been performed or fails, the Windows security layer cannot determine the account associated with the SPN, and Kerberos authentication will not be used.</li>
</ul>
The supported SPN formats

<strong>Named instance</strong>
<ul>
 	<li><em>MSSQLSvc/FQDN</em>:[<em>port</em> <strong>|</strong> <em>instancename</em>],</li>
</ul>
<strong>Default instance</strong>
<ul>
 	<li><em>MSSQLSvc/FQDN</em>:<em>port</em> <strong>|</strong> <em>MSSQLSvc/FQDN</em></li>
</ul>
where:
<ul>
 	<li><em>MSSQLSvc</em> is the service that is being registered.</li>
 	<li><em>FQDN</em> is the fully qualified domain name of the server.</li>
 	<li><em>port</em> is the TCP port number.</li>
 	<li><em>instancename</em> is the name of the SQL Server instance.</li>
</ul>
When a client wants to connect to a service, it locates an instance of the service, composes an SPN for that instance, connects to the service, and presents the SPN for the service to authenticate.

To determine the authentication method of a connection, execute the following query.

Transact-SQL

SELECT net_transport, auth_scheme

FROM sys.dm_exec_connections

WHERE session_id = @@SPID;
<h3><strong>SSIS</strong></h3>
<u><a href="http://blogs.msdn.com/b/psssql/archive/2010/06/23/my-kerberos-checklist.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/psssql/archive/2010/06/23/my-kerberos-checklist.aspx</a></u> <u><a href="http://www.sqlscientist.com/2014/01/setup-kerberos-authentication-for-sql.html" target="_blank" rel="noopener">http://www.sqlscientist.com/2014/01/setup-kerberos-authentication-for-sql.html</a></u>

<u><a href="http://blogs.msdn.com/b/psssql/archive/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package.aspx" target="_blank" rel="noopener">http://blogs.msdn.com/b/psssql/archive/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package.aspx</a></u>

<u><a href="http://thesqldude.com/2011/12/30/how-to-sql-server-bulk-insert-with-constrained-delegation-access-is-denied/" target="_blank" rel="noopener">http://thesqldude.com/2011/12/30/how-to-sql-server-bulk-insert-with-constrained-delegation-access-is-denied/</a></u>

<u><a href="https://connect.microsoft.com/SQLServer/feedback/details/767088/with-the-new-ability-to-execute-ssis-packages-from-tsql-kerberos-delegation-should-be-supported" target="_blank" rel="noopener">https://connect.microsoft.com/SQLServer/feedback/details/767088/with-the-new-ability-to-execute-ssis-packages-from-tsql-kerberos-delegation-should-be-supported</a></u>

"When <strong>xp_cmdshell</strong> is invoked by a user who is a member of the <strong>sysadmin</strong> fixed server role, <strong>xp_cmdshell</strong>will be executed under the security context in which the SQL Server service is running. When the user is not a member of the <strong>sysadmin</strong> group, <strong>xp_cmdshell</strong> will impersonate the SQL Server Agent proxy account, which is specified using <strong>xp_sqlagent_proxy_account</strong>. If the proxy account is not available, <strong>xp_cmdshell</strong>will fail. This is true only for Microsoft® Windows NT® 4.0 and Windows 2000. On Windows 9.x, there is no impersonation and <strong>xp_cmdshell</strong> is always executed under the security context of the Windows 9.x user who started SQL Server."
<h3><strong>Package executions</strong></h3>
<ul>
 	<li>Run the package within SSDT.</li>
 	<li>Open SSDT using Run as different user option. Provide a different credential other than yours and run the package again.</li>
 	<li>Run the package from Integration Services Catalog</li>
 	<li>Create an SQL Server Agent Job to run the package using SQL Server Agent Service Account.</li>
 	<li>Create an SQL Server Agent Job to run the package using a proxy account.</li>
</ul>
For every execution mentioned above, you will receive an email with the user account that was used to execute the package.
<h4><strong>SQL Server Agent Job Without Proxy:</strong></h4>
When you run an SSIS package from within an <em>SQL Server Agent Job</em>, the job step by default runs under <em>SQL Server Agent Service Account</em>. The user account associated SQL Server Agent Service can be found by navigating to <em>Windows Start Administrative Tools Services</em>, look for the service SQL Server Agent () and find the user account listed under <em>Log On As</em>
<h4><strong>SQL Server Agent Job With Proxy:</strong></h4>
You could also run an SQL Server Agent Job under different credentials by creating a proxy account. When job steps are executed under proxy account, the package in the job step will execute under the credential specified on the proxy account.

Below SO answer provides step-by-step instructions to create proxy account to run SQL Server Agent Jobs.
<h4><strong>Integration Catalog Services:</strong></h4>
When you right-click on a package under <em>Integration Services Catalog SSISDB &lt;Folder name&gt; Projects &lt;Project name&gt; Pakages &lt;Package name&gt;</em> and select Execute... to run a package, the package will <u>run under the credentials used to connect to SQL Server Management Studio</u>.

Note that if you try to run a package using SQL Server Authentication, you will get the below error message:

The operation cannot be started by an account that uses SQL Server Authentication. Start the operation with an account that uses Windows Authentication.

<u><a href="http://stackoverflow.com/questions/6712811/how-do-i-create-a-step-in-my-sql-server-agent-job-which-will-run-my-ssis-package/6713464#6713464" target="_blank" rel="noopener">How do I create a step in my SQL Server Agent Job which will run my SSIS package?</a></u>

SSDT / SSMS

Under Windows Start All Programs Microsoft SQL Server 2012, if you click SQL Server Data Tools it will run under your credentials. To run under different user account, you could press Ctrl + Shiftto select <strong>Run as different user</strong> option
<h4><strong>How SSIS 2012 and later work</strong></h4>
When you run a package that is hosted in the SSIS Catalog, it will cause a child process to get spawned from the SQL Service itself. This process is the ISServerExec.exe.

<img class="wp-image-1088" src="/wp-content/uploads/2018/03/image6.png" alt="image6" />

The other thing to note is that this <u>process context is the context of the session that launched the package</u>, <strong>not</strong> the SQL Server Process Context (service account).  Here you can see that the ISServerExec is running as corp.grh.ints.ccpp.prod.d2 where as the SQL Service is running as corp.grh.ints.v0d2-msqlclf-10.sr.

<img class="wp-image-1091" src="/wp-content/uploads/2018/03/image7.png" alt="image7" />

<u>This is the case regardless of how you execute the package.  This could be through the SSMS GUI, via Stored Procedure or even by way of DTExec</u>.  If you want it to run under the context of the SQL Service account, you can “fake it” by doing a runas like operation  on a process (Command Prompt, SSMS or SQL Agent Job security account).

So, I have two domains (battlestar.local &amp; cylons.battlestar.local).  The SQL Server in the Parent Domain (battlestar.local) is using a Service account from the child domain (cylons.battelstar.local).  From a delegation standpoint, we are using <strong>full delegation</strong>.  I’ll touch on Constrained Delegation later on. To make sure that everyone understand what I mean by full delegation, with the CYLONSsqlservice AD Object, I have the following setting:

<img class="wp-image-1102" src="/wp-content/uploads/2018/03/image8.png" alt="image8" />

<u><a href="https://msdn.microsoft.com/en-us/library/aa337083(v=sql.110).aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/aa337083(v=sql.110).aspx</a></u>
<h4>Delegation Is Not Supported</h4>
SQL Server Integration Services does not support the delegation of credentials, sometimes referred to as a double hop. In this scenario, you are working on a client computer, Integration Services is installed on a second computer, and SQL Server is installed on a third computer. Although SQL Server Management Studio successfully passes your credentials from the client computer to the second computer on which Integration Services is running, Integration Services cannot delegate your credentials from the second computer to the third computer on which SQL Server is running.
<h2><strong>SharePoint Server 2010</strong></h2>
<u><a href="https://technet.microsoft.com/en-us/library/gg502602(v=office.14).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-us/library/gg502602(v=office.14).aspx</a></u>
<h2><strong>Setting up SSRS </strong></h2>
Examples
<ol>
 	<li><u><a href="https://technet.microsoft.com/en-us/library/gg502598(v=office.14).aspx" target="_blank" rel="noopener">https://technet.microsoft.com/en-us/library/gg502598(v=office.14).aspx</a></u></li>
 	<li><u><a href="http://sqlmag.com/sql-server-reporting-services/understanding-sql-server-reporting-services-authentication" target="_blank" rel="noopener">http://sqlmag.com/sql-server-reporting-services/understanding-sql-server-reporting-services-authentication</a></u></li>
 	<li><u><a href="http://sqlmag.com/sql-server-reporting-services/implement-kerberos-delegation-ssrs" target="_blank" rel="noopener">http://sqlmag.com/sql-server-reporting-services/implement-kerberos-delegation-ssrs</a></u></li>
 	<li><u><a href="http://www.databasejournal.com/features/mssql/article.php/3696506/Setting-Up-Delegation-for-Linked-Servers.htm" target="_blank" rel="noopener">http://www.databasejournal.com/features/mssql/article.php/3696506/Setting-Up-Delegation-for-Linked-Servers.htm</a></u></li>
</ol>
<u><a href="http://sqlmag.com/sql-server-reporting-services/understanding-sql-server-reporting-services-authentication" target="_blank" rel="noopener">http://sqlmag.com/sql-server-reporting-services/understanding-sql-server-reporting-services-authentication</a></u>

You can find RSReportServer.config file in the Program FilesMicrosoft SQL ServerMSRS11.&lt;instance&gt; folder. Add below lines to be tested
&lt;Authentication&gt;

&lt;AuthenticationTypes&gt;

&lt;RSWindowsNegotiate/&gt; &lt;!-- default if service account is either NetworkService or LocalSystem--&gt;
&lt;RSWindowsKerberos/&gt;

&lt;RSWindowsNTLM/&gt;&lt;!-- default if service account is <u>neither</u> NetworkService <u>nor</u> LocalSystem. do not support Kerberos or to work around Kerberos authentication--&gt;

&lt;/AuthenticationTypes&gt;

&lt;EnableAuthPersistence&gt;true&lt;/EnableAuthPersistence&gt;

&lt;/Authentication&gt;

<u><a href="http://stackoverflow.com/questions/15348649/how-to-authenticate-ssrs-externally-using-automatic-ntlm-credential-passing" target="_blank" rel="noopener">http://stackoverflow.com/questions/15348649/how-to-authenticate-ssrs-externally-using-automatic-ntlm-credential-passing</a></u>

SSRS will <u>fail to authenticate over the internet with automatic NTLM credential</u> passing if the &lt;RSWindowsNegotiate/&gt; authentication type is present in the &lt;Authentication&gt; section of the rsreportserver.config file.

Comment out the &lt;RSWindowsNegotiate/&gt; Authentication Type to resolve this issue.

(C:Program FilesMicrosoft SQL ServerMSRS10_50.MSSQLSERVERReporting ServicesReportServerrsreportserver.config)

&lt;Authentication&gt;

&lt;AuthenticationTypes&gt;

&lt;RSWindowsNTLM/&gt;

&lt;!-- &lt;RSWindowsNegotiate/&gt; --&gt;

&lt;/AuthenticationTypes&gt;

&lt;RSWindowsExtendedProtectionLevel&gt;Off&lt;/RSWindowsExtendedProtectionLevel&gt;

&lt;RSWindowsExtendedProtectionScenario&gt;Proxy&lt;/RSWindowsExtendedProtectionScenario&gt;

&lt;EnableAuthPersistence&gt;true&lt;/EnableAuthPersistence&gt;

&lt;/Authentication&gt;

<u><a href="https://msdn.microsoft.com/en-gb/library/cc281253.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-gb/library/cc281253.aspx</a></u>

You can confirm that you are encountering a Kerberos authentication error by removing &lt;<strong> RSWindowsNegotiate</strong> /&gt; from your configuration file and reattempting the connection.
<ul>
 	<li>Use NTLM. NTLM will generally work in cases where Kerberos authentication fails. To use NTLM, remove<strong>RSWindowsNegotiate</strong> from the RSReportServer.config file and verify that only <strong>RSWindowsNTLM</strong> is specified. If you choose this approach, you can continue to use a domain user account for the Report Server service even if you do not define an SPN for it.</li>
</ul>
<h3>RSWindowsNegotiate<strong> </strong></h3>
Using RSWindowsNegotiate is your <u>best option</u> because it provides the greatest flexibility for multiple clients in an intranet environment. Although a domain administrator needs to configure Kerberos authentication, using it is advantageous because the authenticated identity is retained without passing credentials from server to server in a distributed environment, which is an effective defensive security measure. NTLM authentication allows clients to connect to the report server securely, but it doesn't allow the report server to forward credentials to another server when external data sources are associated with reports.

<u>Even if Kerberos authentication is correctly configured</u>, any of the following conditions in your environment can cause the <u>client to bypass Kerberos and use NTLM</u> authentication instead:
<ul>
 	<li>The Report Server service account is a domain account, but the domain administrator <u>hasn't registered a service principal name (SPN) </u>for the service account.</li>
 	<li>The <u>connection request is sent to a local report server or an IP address rather than a host header or server name</u>.</li>
 	<li>The firewall blocks the Kerberos authentication port (88/TCP).</li>
 	<li>Kerberos isn't enabled in the report server's OS.</li>
 	<li>The client is Microsoft Internet Explorer (IE) and the connection request uses a Fully Qualified Domain Name (FQDN) or localhost rather than the report server's network name.</li>
</ul>
<table>
<tbody>
<tr>
<td><strong>Important</strong></td>
</tr>
<tr>
<td>Using <strong>RSWindowsNegotiate</strong> will result in a Kerberos authentication error if you configured the Report Server service to run under a domain user account and you did not register a Service Principal Name (SPN) for the account. For more information, see <u><a href="https://msdn.microsoft.com/en-gb/library/cc281253.aspx#proxyfirewallRSWindowsNegotiate" target="_blank" rel="noopener">Resolving Kerberos Authentication Errors When Connecting to a report server</a></u> in this topic.</td>
</tr>
</tbody>
</table>
<h3><strong>Verify Kerberos Authentication</strong></h3>
Once you have configured the middle tier and back end tier computers in your environment, verify that Kerberos authentication is working.

<strong>To verify Kerberos authentication</strong>
<ol>
 	<li>Open <strong>Report Manager</strong> (if in a native mode deployment) or a SharePoint library (if in a SharePoint integrated mode deployment) that contains reports or report items.</li>
 	<li>To browse <strong>Report Manager</strong> or the SharePoint library, use a client or a server in your current domain.</li>
 	<li>Run a report that uses a data source that is configured for Windows Integrated Authentication.</li>
</ol>
If there is a log on problem (either from a remote server or in SharePoint integration mode) or if the report fails to render, the possible errors include a 401.1 Access Denied page or a blank page. To fix the problem, add a registry key for the disableloopbackcheck by following the instructions in the support article: <u><a href="http://support.microsoft.com/kb/896861" target="_blank" rel="noopener">You receive error 401.1 when you browse a Web site...</a></u>. If method 1 in the article solves the problem, delete the key that was added in method 1, and then add a new key by following method 2 in same article.

&nbsp;

&nbsp;
<h1><strong>References</strong></h1>
<u><a href="https://msdn.microsoft.com/en-us/library/ff647405.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/ff647405.aspx</a></u>

<u><a href="https://msdn.microsoft.com/en-us/library/ff647076.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/ff647076.aspx</a></u>

<u><a href="https://www.simple-talk.com/dotnet/asp.net/introducing-single-sign-on-to-an-existing-asp.net-mvc-application/" target="_blank" rel="noopener">https://www.simple-talk.com/dotnet/asp.net/introducing-single-sign-on-to-an-existing-asp.net-mvc-application/</a></u>

<u><a href="https://msdn.microsoft.com/en-us/library/dd577079.aspx" target="_blank" rel="noopener">https://msdn.microsoft.com/en-us/library/dd577079.aspx</a></u>

<u><a href="http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on" target="_blank" rel="noopener">http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on</a></u>
