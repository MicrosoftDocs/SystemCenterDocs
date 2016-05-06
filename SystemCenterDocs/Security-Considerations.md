---
title: Security Considerations
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdf6fae3-a940-4c86-b428-a5611796c3ab
---
# Security Considerations
Most of the work in preparing the environment for [!INCLUDE[om12long](./Token/om12long_md.md)] goes into security\-related tasks. This section covers those tasks at a cursory level. For more information, see the [Index to Security\-related Information for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=244660).

Preparing the security\-related tasks involves the following:

-   Understanding, planning, and preparing for monitoring across trust boundaries.

-   Understanding, planning, and preparing for monitoring UNIX or Linux computers.

-   Planning and preparing the service accounts, user accounts, and security groups that you will need.

-   Understanding and preparing the network ports as required by your design.

## Trust Boundaries
Active Directory domains form the basic unit of a Kerberos trust boundary as seen by [!INCLUDE[om12short](./Token/om12short_md.md)]. This boundary is automatically expanded to other domains in the same name space \(the same Active Directory tree\), and between domains that are in different Active Directory trees but still in the same Active Directory forest via transitive trusts. The trust boundary can be further expanded between domains in different Active Directory forests through the use of across forest trusts.

### Kerberos
The Kerberos authentication protocol, which is supported by Windows 2000 domain controllers and above, can only occur within a trust boundary. Kerberos authentication is the mechanism used to perform the [!INCLUDE[om12short](./Token/om12short_md.md)] agent\/server mutual authentication. Agent\/server mutual authentication is mandated in [!INCLUDE[om12shell](./Token/om12shell_md.md)] for all agent\/server communication.

An [!INCLUDE[om12short](./Token/om12short_md.md)] management group does have the ability to perform discovery and monitoring outside of the Kerberos trust boundary that it is in. However, because the default authentication protocol for Windows\-based computers that are not joined to an Active Directory domain is NTLM, another mechanism must be used to support mutual authentication. This is done through the exchange of certificates between agents and servers.

### Certificates
When [!INCLUDE[om12short](./Token/om12short_md.md)] communication needs to occur across trust boundaries, such as when a server that you want to monitor lies in a different, untrusted, Active Directory domain than the management group that is performing the monitoring, certificates can be used to satisfy the mutual authentication requirement. Through manual configuration, certificates can be obtained and associated with the computers and the [!INCLUDE[om12short](./Token/om12short_md.md)] services running on them. When a service that needs to communicate with a service on a different computer starts and attempts to authenticate, the certificates will be exchanged and mutual authentication completed.

> [!IMPORTANT]
> The certificates used for this purpose must ultimately trust the same root certification authority \(CA\).

For more information about how to obtain and make use of certificates for mutual authentication, see [Deploying a Gateway Server](assetId:///b890d6e8-1363-423d-bf2b-7c7cf6d6ce5b).

## Certification Authority
To get the necessary certificates, you will need access to a certification authority \(CA\). This can be either Microsoft Certificate Services or a third\-party certification service such as VeriSign.

### Microsoft Certificate Services
There are four types of Microsoft CAs:

-   Enterprise root

-   Enterprise subordinate

-   Stand\-alone root

-   Stand\-alone subordinate

-   Both enterprise types of CAs require Active Directory Domain Services; stand\-alone CAs do not. Either type of CA can issue the necessary certificates for agent\/server mutual authentication across trust boundaries.

Customarily, a CA infrastructure consists of a root CA that signs its own certificates and certifies itself and one or more subordinate CAs, which are certified by the root. The subordinate CA servers are the ones that a service certificate requests, while the root is taken offline and held for safekeeping. For more information about designing certificates, see [Infrastructure Planning and Design](http://go.microsoft.com/fwlink/p/?LinkId=86400) and [Authentication and Data Encryption for Windows Computers](assetId:///8ee895a9-7bac-4274-80b8-092475a83c67).

## Monitoring UNIX and Linux computers
[!INCLUDE[om12long](./Token/om12long_md.md)] can monitor UNIX and Linux computers. Because the UNIX and Linux computers are not participating in the Active Directory domain that the management group is in a variation of the certificate method of mutual authentication, discussed before, is used.

### Establishing Mutual Authentication with UNIX and Linux computers
You will use the Discovery wizard to find UNIX and Linux computers and add them to the management group as managed objects. During the Discovery wizard process, [!INCLUDE[om12short](./Token/om12short_md.md)] has the discovered UNIX and Linux computer generate a self\-signed certificate which is used for mutual authentication with the management server. The certificate generation, signing and exchange process works like this when SSH discovery is enabled:

1.  The Discovery Wizard process on the management server has the discovered UNIX or Linux computer generate a self\-signed certificate.

2.  The discovering management server issues a get certificate request to the UNIX or Linux computer.

3.  The UNIX or Linux computer returns the certificate to the management server

4.  The discovering management server creates a key pair and a self\-signed certificate of its own. The management server only generates a key pair and a self\-signed certificate when it discovers its first UNIX or Linux computer. The management server then imports its own certificate into its trusted certificate store. The discovering management server then signs the UNIX or Linux certificate with its private key. Any subsequent signing of UNIX or Linux computer certificates by the management server will reuse the management server’s private key that was generated on the first signing.

5.  The discovering management server then issues a put certificate request which puts the now management server\-signed certificate back onto the UNIX or Linux computer that initially generated it. The UNIX or Linux computer WSMAN communication layer is then restarted to make the new UNIX\\Linux computer generated certificate active.

6.  Now when the management server requests that the UNIX or Linux computer authenticate itself, the UNIX or Linux computer will provide the trusted certificate to the management server and the management server will read the signature on the certificate that it is presented with, see that it trusts this signature \(because the signature is its own private key that is stored in its own trusted certificate store\) and accept this certificate as proof that the UNIX OR LINUX computer is who the management server thinks it is.

7.  The discovering management server will use UNIX or Linux credentials as configured in the appropriate Run As Profile to authenticate itself with the UNIX or Linux computer. See the [Planning for UNIX or Linux Run As Profiles](assetId:///9c0f4ce0-8cfc-4994-97e4-5e0e29c1b6c5#BKMK_Planning) section for more details.

> [!IMPORTANT]
> The preceding order of operations is for the low security version of UNIX or Linux discovery.

### <a name="BKMK_Planning"></a>Planning for UNIX or Linux Run As Profiles
After the UNIX or Linux computer is being managed by the discovering management server, the management pack discoveries and workflows begin to run. These workflows require the use of credentials to complete successfully. These credentials, what objects, classes or group they will be applied to and the computers that they will be distributed to are contained in Run As Profiles. There are two Run As Profiles that are imported when the UNIX management packs are imported into your management group; they are:

-   Unix Action Account profile – This Run As profile and its associated UNIX or Linux credentials are used for low security activities on the designated UNIX or Linux computers.

-   Unix Privileged Account profile – This Run As profile and its associated UNIX or Linux credentials are used for activities that are protected by a higher level of security and therefore require an account that has higher privileges on the UNIX or Linux computer. This can be \(but does not have to be\) the root account.

You will need to configure these profiles with the appropriate UNIX or Linux computer credentials for the management pack workflows that use them to function correctly.

## Accounts and Groups
Over the lifetime of your [!INCLUDE[om12short](./Token/om12short_md.md)] deployment, you will potentially need many accounts and security groups. During [!INCLUDE[om12short](./Token/om12short_md.md)] Setup, you are only prompted for four. You need to consider additional accounts when planning out role\-based security assignments, notifications, and alternate credentials to run processes. For guidance on planning role\-based security assignments, see [Planning the Operations Manager for System Center 2012 Deployment](assetId:///d6edb9b4-5db8-40c2-be00-a32445732d50).

### Role\-Based Security Accounts and Groups
[!INCLUDE[om12short](./Token/om12short_md.md)] controls access to monitored groups, tasks, views, and administrative functions through the assignment of user accounts to roles. A role in [!INCLUDE[om12short](./Token/om12short_md.md)] is the combination of a profile type \(operator, advanced operator, administrator\) and a scope \(what data the role has access to\). Typically, Active Directory security groups are assigned to roles, and then individual accounts are assigned to those groups. Prior to deploying, plan out Active Directory security groups that can be added to these and any custom\-created roles so that you can then add individual user accounts to the security groups.

[!INCLUDE[om12short](./Token/om12short_md.md)] provides the following role definitions out\-of\-the\-box.

|Role name|Profile type|Profile description|Role scope|
|-------------|----------------|-----------------------|--------------|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Administrators: Created at setup; cannot be deleted; must contain one or more global groups|Administrator|Has full privileges to [!INCLUDE[om12short](./Token/om12short_md.md)]; no scoping of the Administrator profile is supported|Full access to all [!INCLUDE[om12short](./Token/om12short_md.md)] data, services, administrative, and authoring tools|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Advanced Operators: Created at setup; globally scoped; cannot be deleted|Advanced Operator|Has limited change access to [!INCLUDE[om12short](./Token/om12short_md.md)] configuration; ability to create overrides to rules; monitors for targets or groups of targets within the configured scope|Access to all groups, views, and tasks currently present and those imported in the future|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Authors: Created at setup; globally scoped; cannot be deleted|Author|Has ability to create, edit, and delete tasks, rules, monitors, and views within configured scope|Access to all groups, views, and tasks currently present and those imported in the future|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Operators: Created at setup; globally scoped; cannot be deleted|Operator|Has ability to interact with alerts, run tasks, and access views according to configured scope|Access to all groups, views, and tasks currently present and those imported in the future|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Read\-Only Operators: Created at setup; globally scoped; cannot be deleted|Read\-Only Operator|Has ability to view alerts and access views according to configured scope|Access to all groups and views currently present and those imported in the future|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Report Operators: Created at setup; globally scoped|Report Operator|Has ability to view reports according to configured scope|Globally scoped|
|[!INCLUDE[om12short](./Token/om12short_md.md)] Report Security Administrators: Integrates SQL Server Reporting Services security with [!INCLUDE[om12short](./Token/om12short_md.md)] user roles; gives [!INCLUDE[om12short](./Token/om12short_md.md)] administrators the ability to control access to reports; cannot be scoped|Report Security Administrator|Enables integration of SQL Server Reporting Services security with [!INCLUDE[om12short](./Token/om12short_md.md)] roles|No scope|

You can add Active Directory security groups or individual accounts to any of these predefined roles. If you do, those individuals will be able to exercise the given role privileges across the scoped objects.

> [!NOTE]
> The predefined roles are globally scoped, giving them access to all groups, views, and tasks \(except for Report Security Administrator\).

[!INCLUDE[om12short](./Token/om12short_md.md)] also allows you to create custom roles based on the Operator, Read\-Only Operator, Author, and Advanced Operator profiles. When you create the role, you can further narrow the scope of groups, tasks, and views that the role can access. For example, you can create a role entitled "Exchange Operator" and narrow the scope to only Exchange\-related groups, views, and tasks. User accounts assigned to this role will only be able to run Operator\-level actions on Exchange\-related objects.

### Notification Accounts and Groups
Individuals in your company that will interact with [!INCLUDE[om12short](./Token/om12short_md.md)] frequently, such as an Exchange administrator who has been assigned to the Exchange Operator role, need a way to discover new alerts. This can be done by either watching the Operations console for new alerts or by [!INCLUDE[om12short](./Token/om12short_md.md)] informing them about the alert via supported communications channels. [!INCLUDE[om12short](./Token/om12short_md.md)] supports notifications through e\-mail, instant messaging, Short Message Service, or pager messages. Notifications on what the role needs to know go out to recipients that you specify in [!INCLUDE[om12short](./Token/om12short_md.md)]. An [!INCLUDE[om12short](./Token/om12short_md.md)] recipient is merely an object that has a valid address to receive the notification, such as an SMTP address for e\-mail notifications.

Therefore, it is logical to combine role assignment with notification group membership via an e\-mail\-enabled security group. For example, create an Exchange Administrators security group and populate it with individuals that have the knowledge and permissions to fix things in Exchange. Assign this security group to a custom\-created Exchange Administrator role so they have access to the data and are e\-mail\-enabled. Then, create a recipient by using the SMTP address of the e\-mail\-enabled security group.

### Service Accounts
At the time of deployment, you need to have the following service accounts ready. If you use domain accounts and your domain Group Policy object \(GPO\) has the default password expiration policy set as required, you will either have to change the passwords on the service accounts according to the schedule, or use low maintenance system accounts, or configure the accounts so that the passwords never expire.

|Account name|Requested when|Used for|Low maintenance|High security|
|----------------|------------------|------------|-------------------|-----------------|
|Management server Action Account|management server setup|Collecting data from providers, running responses|Local system|Low privilege domain account|
|Data Access Service and Configuration Service Account|management server setup|Writing to operational database, running services|Local system|Low privilege domain account|
|Local Administrator Account for target devices|Discovery and push agent install|Installing agents|Domain or local administrator account|Domain or local administrator account|
|Agent Action Account|Discovery and push agent install|Gathering information and running responses on managed computers|Local system|Low privilege domain account|
|Data Warehouse Write Action Account|Reporting Server setup|Writing to the Reporting Data Warehouse database|Low privilege domain account|Low privilege domain account|
|Data Reader Account|Reporting Server setup|Querying SQL Reporting Services database|Low privilege domain account|Low privilege domain account|

### <a name="BKMK_Service_Principal_Names"></a>Service Principal Names
When you deploy [!INCLUDE[om12short](./Token/om12short_md.md)], you may need to register a Service Principal Name \(SPN\) in some configurations. SPNs are used by Kerberos authentication for the client to mutually authenticate with the server. For more information, see [What Are Service Publication and Service Principal Names?](http://go.microsoft.com/fwlink/p/?linkID=245905).

When you install [!INCLUDE[om12short](./Token/om12short_md.md)], you select an account for the **System Center Configuration service and System Center Data Access service**. For more information, see [Deploying System Center 2012 \- Operations Manager](assetId:///d81818d2-534e-475c-98e1-65496357d5a5).

> [!CAUTION]
> Do not modify the default Active Directory permissions to allow an account to do unrestricted modifications of its own SPN.

If you select the Local System as the System Center Data Access service account, the account can create the appropriate SPN. No additional configuration is necessary.

If you use a domain account, you must register an SPN for each management server. Use the SETSPN command line tool. For more information about running that tool, see [Setspn Overview](http://go.microsoft.com/fwlink/p/?linkID=154899).

Register both the netbios name and fully qualified domain name of the management server, using the following syntax:

<pre>setspn –a MSOMSdkSvc/<netbios name> <DAS account domain>\<DAS account name>
setspn –a MSOMSdkSvc/<fqdn> <DAS account domain>\<DAS account name></pre>

> [!TIP]
> You can list the SPNs registered to user account or computer with the following syntax:
> 
> `setspn –l <DAS account name>`
> 
> `setspn –l <fqdn>`

If you are using Network Load Balancing or using a hardware load balancer, the System Center Data Access service must run under a domain account. In addition to the setup already described, you must also register the load balanced name, using the following syntax:

`setspn –a MSOMSdkSvc/<load balanced name> <DAS account domain>\<DAS account name>`

> [!NOTE]
> All of the System Center Data Access services running behind the load balancer must be running with the same domain account.

### Run As Accounts
Agents on monitored computers can run tasks, modules, and monitors on demand as well as in response to predefined conditions. By default, all tasks run by using the Agent Action account credentials. In some cases, the Agent Action account may have insufficient rights and privileges to run a given action on the computer. [!INCLUDE[om12short](./Token/om12short_md.md)] supports the running of tasks by agents in the context of an alternate set of credentials called a Run As Account. A Run As Account is an object that is created in [!INCLUDE[om12short](./Token/om12short_md.md)], just like a recipient is, and maps to an Active Directory user account. A Run As Profile is then used that maps the Run As Account to a specific computer. When a rule, task, or monitor that has been associated with a Run As Profile at the development time of a management pack needs to run on the targeted computer, it does so by using the specified Run As Account.

Out\-of\-the\-box, [!INCLUDE[om12short](./Token/om12short_md.md)] provides a number of Run As Accounts and Run As Profiles, and you can create additional ones as necessary. You may also choose to modify the Active Directory credentials that a Run As Account is associated with. This will require planning, creating, and maintaining additional Active Directory credentials for this purpose. You should treat these accounts as service accounts with respect to password expiration, Active Directory Domain Services, location, and security.

You will need to work with management pack authors as they develop requests for Run As Accounts. For more information, see the [Index to Security\-related Information for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=244660).

## See Also
[Environmental Prerequisites for Operations Manager for System Center 2012](assetId:///95d59f73-5aa9-4616-b98c-30680406959a)


