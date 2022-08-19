---
layout: post
title: AWS IAM - Notes
date: 2018-03-12 08:56
author: tmasabari
comments: true
categories: [AWS]
---
<strong>Security</strong>
<ul>
 	<li><b>Delete your root access keys
</b><b></b></li>
 	<li><b>Activate MFA on your root account
</b><b></b></li>
 	<li><b>Create individual IAM users
</b></li>
 	<li><b>Use groups to assign permissions
</b></li>
 	<li><b>Apply an IAM password policy</b></li>
</ul>
<strong>Best Practices</strong>

When you first create an Amazon Web Services (AWS) account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS account root user and is accessed by signing in with the email address and password that you used to create the account.
We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones. Instead, adhere to the best practice of using the root user only to create your first IAM user. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks
However, you can perform the tasks listed below only when you sign in as the root user of an account.
<ul>
 	<li>Modify root user details. This includes changing the root user's password.</li>
 	<li>Change your AWS support plan.</li>
 	<li>Change or delete your payment options - an IAM user can perform this after you enable billing access for IAM users. For more information, see Activating Access to the Billing and Cost Management Console.</li>
 	<li>View your account's billing information - an IAM user can perform this after you enable billing access for IAM users. For more information, see Activating Access to the Billing and Cost Management Console</li>
 	<li>Close an AWS account.</li>
 	<li>Sign up for GovCloud.</li>
 	<li>Submit a Reverse DNS for Amazon EC2 request. The "this form" link on that page to submit a request works only if you sign in with root user credentials.</li>
 	<li>Create a CloudFront key pair.</li>
 	<li>Create an AWS-created X.509 signing certificate. (You can still make self-created certificates for IAM users.)</li>
 	<li>Transfer an Route 53 domain to another AWS account.</li>
 	<li>Change the Amazon EC2 setting for longer resource IDs. Changing this setting as the root user affects all users and roles in the account. Changing it as an IAM user or IAM role affects only that user or role.</li>
 	<li>Submit a request to perform penetration testing on your AWS infrastructure using the web form. Alternatively, you can submit your request via email without needing root user access.</li>
 	<li>Request removal of the port 25 email throttle on your EC2 instance.</li>
 	<li>Find your AWS account canonical user ID. You can view your canonical user ID from the AWS Management Console only while signed in as the AWS account root user. You can view your canonical user ID as an IAM user with the AWS API or AWS CLI.</li>
 	<li>Reassigning permissions in a resource-based policy (such as an S3 bucket policy) that were revoked by explicitly denying IAM users access. Root users are not blocked by an explicit deny like IAM users can be.</li>
</ul>
&nbsp;

<strong>MFA</strong>

AWS Multi-Factor Authentication (MFA) is a simple best practice that adds an extra layer of protection on top of your user name and password. With MFA enabled, when a user signs in to an AWS website, they will be prompted for their user name and password (the first factor—what they know), as well as for an authentication code from their AWS MFA device (the second factor—what they have). Taken together, these multiple factors provide increased security for your AWS account settings and resources.
Free for Virtual MFA Device code generator on Android, ios, blackberry
Android Google Authenticator; Authy 2-Factor Authentication
iPhone Google Authenticator; Authy 2-Factor Authentication
Windows Phone Authenticator
Blackberry Google Authenticator

<strong>IAM AWS Identity and Access Management (IAM)</strong>
AWS Identity and Access Management is a feature of your AWS account offered at no additional charge. You will be charged only for use of other AWS services by your Users.

<b>When should I use an IAM user, IAM group, or IAM role?</b>

An IAM user has permanent long-term credentials and is used to directly interact with AWS services. An IAM group is primarily a management convenience to manage the same set of permissions for a set of IAM users.

<b>What is an IAM role?
</b>An IAM role is an IAM entity that defines a set of <a href="https://aws.amazon.com/iam/details/manage-permissions/">permissions</a> for making AWS service requests. IAM roles are not associated with a specific user or group. Instead, trusted entities <i>assume </i>roles, such as IAM users, applications, or AWS services such as EC2.

An IAM role is an AWS Identity and Access Management (IAM) entity with permissions to make AWS service requests. IAM roles cannot make direct requests to AWS services; they are meant to be assumed by authorized entities, such as IAM users, applications, or AWS services such as EC2. Use IAM roles to delegate access within or between AWS accounts.

<b>What problems do IAM roles solve?</b>
IAM roles allow you to delegate access with defined permissions to trusted entities without having to share long-term access keys. You can use IAM roles to delegate access to IAM users managed within your account, to IAM users under a different AWS account, or to an AWS service such as EC2.

<b>How much do IAM roles cost?</b>
IAM roles are free of charge. You will continue to pay for any resources a role in your AWS account consumes.

<b>Can I structure a collection of users in a hierarchical way, such as in LDAP?</b>
Yes. You can organize users and groups under paths, similar to object paths in Amazon S3—for example /mycompany/division/project/joe.

<b>How are MFA devices configured for IAM users?</b>
You (the AWS account holder) can order multiple MFA devices. You can then assign these devices to individual IAM users via the IAM APIs, <a href="http://aws.amazon.com/cli/">AWS CLI</a>, or <a href="https://console.aws.amazon.com/iam/home">IAM console</a>.

<b>Q: How do permissions work?</b>

Access control policies are attached to users, groups, and roles to assign permissions to AWS resources. By default, IAM users, groups, and roles have no permissions; users with sufficient permissions must use a policy to grant the desired permissions.

<b>Q: How do I assign commonly used permissions?</b>

AWS provides a set of commonly used permissions that you can attach to IAM users, groups, and roles in your account. These are called AWS managed policies. One example is read-only access for Amazon S3. When AWS updates these policies, the permissions are applied automatically to the users, groups, and roles to which the policy is attached. AWS managed policies automatically appear in the <b>Policies </b>section of the IAM console. When you assign permissions, you can use an AWS managed policy or you can create your own customer managed policy. Create a new policy based on an existing AWS managed policy, or define your own.

<b>Q: How do group-based permissions work?</b>

Use IAM groups to assign the same set of permissions to multiple IAM users. A user can also have individual permissions assigned to them. The two ways to attach permissions to users work together to set overall permissions.

<b>Q: How can I easily remove unnecessary permissions?</b>

To help you determine which permissions are needed, the IAM console now displays <a href="https://blogs.aws.amazon.com/security/post/Tx280RX2WH6WUD7/Remove-Unnecessary-Permissions-in-Your-IAM-Policies-by-Using-Service-Last-Access" target="_blank" rel="noopener">service last accessed data</a> that shows the hour when an IAM entity (a user, group, or role) last accessed an AWS service. Knowing if and when an IAM entity last exercised a permission can help you remove unnecessary permissions and tighten your IAM policies with less effort.

<b>Q: What is identity federation?</b>
AWS Identity and Access Management (IAM) supports identity federation for delegated access to the AWS Management Console or AWS APIs. With identity federation, external identities are granted secure access to resources in your AWS account without having to create IAM users. These external identities can come from your corporate identity provider (such as Microsoft Active Directory or from the AWS Directory Service) or from a web identity provider (such as <a href="http://aws.amazon.com/cognito/" target="_blank" rel="noopener">Amazon Cognito</a>, <a href="http://login.amazon.com/" target="_blank" rel="noopener">Login with Amazon</a>, <a href="https://www.facebook.com/about/login" target="_blank" rel="noopener">Facebook</a>, <a href="https://developers.google.com/+/" target="_blank" rel="noopener">Google</a>, or any <a href="http://openid.net/connect/" target="_blank" rel="noopener">OpenID Connect</a>-compatible provider).

<b>Q: What are federated users?</b>
Federated users (external identities) are users you manage outside of AWS in your corporate directory, but to whom you grant access to your AWS account using temporary security credentials. They differ from IAM users, which are created and maintained in your AWS account.<b></b>

<b>Q: Do you support SAML?</b>
Yes, AWS supports the Security Assertion Markup Language (SAML) 2.0.

<b>Q: How do I control how long a federated user has access to the AWS Management Console?</b>
Depending on the API used to create the temporary security credentials, you can specify a session limit between 15 minutes and 36 hours (for GetFederationToken and GetSessionToken) and between 15 minutes and 12 hours (for AssumeRole* APIs), during which time the federated user can access the console. When the session expires, the federated user must request a new session by returning to your identity provider, where you can grant them access again. Learn more about <a href="http://blogs.aws.amazon.com/security/post/Tx3GL3IZE3FIGB6/Enable-Your-Federated-Users-to-Work-in-the-AWS-Management-Console-for-up-to-12-H" target="_blank" rel="noopener">setting session duration</a>.

<b>Q: What happens when the identity federation console session times out?</b>
The user is presented with a message stating that the console session has timed out and that they need to request a new session. You can specify a URL to direct users to your local intranet web page where they can request a new session. You add this URL when you specify an Issuer parameter as part of your sign-in request. For more information, see <a href="http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-custom-url.html" target="_blank" rel="noopener">Enabling SAML 2.0 Federated Users to Access the AWS Management Console</a>.

<b>Q: What is web identity federation?</b>

Web identity federation allows you to create AWS-powered mobile apps that use public identity providers (such as <a href="http://aws.amazon.com/cognito/" target="_blank" rel="noopener">Amazon Cognito</a>, <a href="http://login.amazon.com/" target="_blank" rel="noopener">Login with Amazon</a>, <a href="https://www.facebook.com/about/login" target="_blank" rel="noopener">Facebook</a>, <a href="https://developers.google.com/+/" target="_blank" rel="noopener">Google</a>, or any <a href="http://openid.net/connect/" target="_blank" rel="noopener">OpenID Connect</a>-compatible provider) for authentication. With web identity federation, you have an easy way to integrate sign-in from public identity providers (IdPs) into your apps without having to write any server-side code and without distributing long-term AWS security credentials with the app.

For more information about web identity federation and to get started, see <a href="http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_oidc.html" target="_blank" rel="noopener">About Web Identity Federation</a>.

<b>How does identity federation using AWS Directory Service differ from using a third-party identity management solution?</b>

<b></b>If you want your federated users to be able to access only the AWS Management Console, using AWS Directory Service provides similar capabilities compared to using a <a href="http://aws.amazon.com/iam/partners/">third-party identity management solution</a>. End users are able to sign in using their existing corporate credentials and access the AWS Management Console. Because AWS Directory Service is a managed service, customers do not need to set up or manage federation infrastructure, but rather need to create an AD Connector directory to integrate with their on-premises directory. If you are interested in providing your federated users access to AWS APIs, use a <a href="http://aws.amazon.com/iam/partners/">third-party offering</a>, or deploy your own <a href="http://aws.amazon.com/iam/details/manage-federation/">proxy server</a>.

&nbsp;

&nbsp;
<ol>
 	<li>https://aws.amazon.com/iam/faqs/</li>
 	<li>https://aws.amazon.com/identity/federation/</li>
</ol>
