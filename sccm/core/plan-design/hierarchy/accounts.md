---
title: "Accounts used"
titleSuffix: "Configuraton Manager"
description: "Identify and manage the Windows groups and the accounts in System Center Configuration Manager."
ms.custom: na
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: 7
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Accounts used in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the following information to identify the Windows groups and the accounts that are used in System Center Configuration Manager, how they are used, and any requirements.  

## Windows groups that Configuration Manager creates and uses  
 Configuration Manager automatically creates, and in many cases automatically maintains, the following Windows groups:  

> [!NOTE]  
>  When Configuration Manager creates a group on a computer that is a domain member, the group is a local security group. If the computer is a domain controller, the group is a domain local group that is shared among all domain controllers in the domain.  


### ConfigMgr_CollectedFilesAccess  
Configuration Manager uses this group to grant access to view files collected by software inventory.  

The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on the primary site server.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Membership|Configuration Manager automatically manages the group membership. Membership includes administrative users that are granted the **View Collected Files** permission to the **Collection** securable object from an assigned security role.|  
|Permissions|By default, this group has **Read** permission to the following folder on the site server: **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### ConfigMgr_DViewAccess  
 This group is a local security group that Configuration Manager creates on the site database server or database replica server. It is not currently used but is reserved for future use.  

### ConfigMgr Remote Control Users  
 Configuration Manager remote tools use this group to store the accounts and groups that you set up in the Permitted Viewers list that is assigned to each client.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on the Configuration Manager client when the client receives a policy that enables remote tools.<br /><br /> After you disable remote tools for a client, this group is not automatically removed. It must be manually deleted from each client computer.|  
|Membership|By default, there are no members in this group. When you add users to the Permitted Viewers list, they are automatically added to this group.<br /><br /> You can use the Permitted Viewers list to manage the membership of this group instead of adding users or groups directly to this group.<br /><br /> In addition to being a permitted viewer, an administrative user must have the **Remote Control** permission to the **Collection** object. You can assign this permission by using the Remote Tools Operator security role.|  
|Permissions|By default, this group does not have permissions to any locations on the computer. It is used only to hold the Permitted Viewers list.|  

### SMS Admins  
 Configuration Manager uses this group to grant access to the SMS Provider, through Windows Management Instrumentation (WMI). Access to the SMS Provider is required to view and change objects in the Configuration Manager console.  

> [!NOTE]  
>  The role-based administration configuration of an administrative user determines which objects they can view and manage when using the Configuration Manager console.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on each computer that has an SMS Provider.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Membership|Configuration Manager automatically manages the group membership. By default, each administrative user in a hierarchy and the site server computer account are members of the SMS Admins group on each SMS Provider computer in a site.|  
|Permissions|SMS Admins rights and permissions are set in the WMI Control MMC snap-in. By default, the SMS Admins group is granted **Enable Account** and **Remote Enable** on the Root\SMS namespace. Authenticated users have **Execute Methods**, **Provider Write**, and **Enable Account**.<br /><br /> Administrative users who will use a remote Configuration Manager console require Remote Activation DCOM permissions on both the site server computer and the SMS Provider computer. It is a best practice to grant these rights to the SMS Admins to simplify administration instead of granting these rights directly to users or groups. For more information, see the [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) section in the [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) article.|  

### SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 Configuration Manager management points that are remote from the site server use this group to connect to the site database. This group provides a management point access to the inbox folders on the site server and the site database.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on each computer that has an SMS Provider.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Membership|Configuration Manager automatically manages the group membership. By default, membership includes the computer accounts of remote computers that have a management point for the site.|  
|Permissions|By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the **%path%\Microsoft Configuration Manager\inboxes** folder on the site server. This group has the additional permission of **Write** to subfolders below the **inboxes** to which the management point writes client data.|  

### SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 Configuration Manager SMS Provider computers that are remote from the site server use this group to connect to the site server.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on the site server.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Membership|Configuration Manager automatically manages the group membership. By default, membership includes the computer account or the domain user account that is used to connect to the site server from each remote computer that has installed an SMS Provider for the site.|  
|Permissions|By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the **%path%\Microsoft Configuration Manager\inboxes** folder on the site server. This group has the additional permission of **Write** or the permissions of **Write** and **Modify** to subfolders below the **inboxes** to which the SMS Provider requires access.<br /><br /> This group also has **Read**, **Read & execute**, **List folder contents**, **Write**, and **Modify** permissions to the folders below **%path%\Microsoft Configuration Manager\OSD\boot** and **Read** permission to the folders below **%path%\Microsoft Configuration Manager\OSD\Bin** on the site server.|  

### SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  
 The File Dispatch Manager on Configuration Manager remote site system computers uses this group to connect to the site server.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on the site server.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Membership|Configuration Manager automatically manages the group membership. By default, membership includes the computer account or the domain user account that is used to connect to the site server from each remote site system computer that runs the File Dispatch Manager.|  
|Permissions|By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the **%path%\Microsoft Configuration Manager\inboxes** folder and subfolders below that location on the site server. This group has the additional permissions of **Write** and **Modify** to the **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** folder on the site server.|  

### SMS_SiteToSiteConnection_&lt;sitecode\>  
 Configuration Manager uses this group to enable file-based replication between sites in a hierarchy. For each remote site that directly transfers files to this site, this group has accounts set up as a **File Replication Account**.  

 The following table lists additional details for this group:  

|Detail|More information|  
|------------|----------------------|  
|Type and location|This group is a local security group created on the site server.|  
|Membership|When you install a new site as a child of another site, Configuration Manager automatically adds the computer account of the new site to the group on the parent site server. Configuration Manager also adds the parent site's computer account to the group on the new site server. If you specify another account for file-based transfers, add that account to this group on the destination site server.<br /><br /> When you uninstall a site, this group is not automatically removed. It must be manually deleted.|  
|Permissions|By default, this group has **full control** to the **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** folder.|  

## Accounts that Configuration Manager uses  
 You can set up the following accounts for Configuration Manager.  

### Active Directory Group Discovery Account  
 The **Active Directory Group Discovery Account** is used to discover local, global, and universal security groups, the membership within these groups, and the membership within distribution groups from the specified locations in Active Directory Domain Services. Distribution groups are not discovered as group resources.  

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that are specified for discovery.  

### Active Directory System Discovery Account  
 The **Active Directory System Discovery Account** is used to discover computers from the specified locations in Active Directory Domain Services.  

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that are specified for discovery.  

### Active Directory User Discovery Account  
 The **Active Directory User Discovery Account** is used to discover user accounts from the specified locations in Active Directory Domain Services.  

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that are specified for discovery.  

### Active Directory Forest Account  
 The **Active Directory Forest Account** is used to discover network infrastructure from Active Directory forests. Central administration sites and primary sites also use it to publish site data to Active Directory Domain Services for a forest.  

> [!NOTE]  
>  Secondary sites always use the secondary site server computer account to publish to Active Directory.  

> [!NOTE]  
>  The Active Directory Forest Account must be a global account to discover and publish to untrusted forests. If you do not use the computer account of the site server, you can select only a global account.  

 This account must have **Read** permissions to each Active Directory forest where you want to discover network infrastructure.  

 This account must have **Full Control** permissions to the System Management container and all its child objects in each Active Directory forest where you want to publish site data.  

### Asset Intelligence Synchronization Point Proxy Server Account  
 The Asset Intelligence synchronization point uses the **Asset Intelligence Synchronization Point Proxy Server Account** to access the Internet via a proxy server or firewall that requires authenticated access.  

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions for the required proxy server or firewall.  

### Certificate Registration Point Account  
 The **Certificate Registration Point Account** connects the certificate registration point to the Configuration Manager database. The computer account of the certificate registration point server is used by default, but you can set up a user account instead. You must specify a user account whenever the certificate registration point is in an untrusted domain from the site server. This account requires only **Read** access to the site database, because the state message system handles write tasks.  

### Capture Operating System Image Account  
 Configuration Manager uses the **Capture Operating System Image Account** to access the folder where captured images are stored when you deploy operating systems. This account is required if you add the step **Capture Operating System Image** to a task sequence.  

 The account must have **Read** and **Write** permissions on the network share where the captured image is stored.  

 If the password for the account is changed in Windows, you must update the task sequence with the new password. The Configuration Manager client receives the new password when it next downloads the client policy.  

 If you use this account, you can create one domain user account with minimal permissions to access the required network resources and use it for all task sequence accounts.  

> [!IMPORTANT]  
>  Do not assign interactive sign-in permissions to this account.  
>   
>  Do not use the Network Access Account for this account.  

### Client Push Installation Account  
 The **Client Push Installation Account** is used to connect to computers and install the Configuration Manager client software if you deploy clients by using client push installation. If this account is not specified, the site server account is used to try to install the client software.  

 This account must be a member of the local **Administrators** group on the computers where the Configuration Manager client software will be installed. This account does not require **Domain Admin** rights.  

 You can specify one or more Client Push Installation Accounts, which Configuration Manager tries in turn until one succeeds.  

> [!TIP]  
>  To more effectively coordinate account updates in large Active Directory deployments, create a new account with a different name, and then add the new account to the list of Client Push Installation Accounts in Configuration Manager. Allow sufficient time for Active Directory Domain Services to replicate the new account, and then remove the old account from Configuration Manager and Active Directory Domain Services.  

> [!IMPORTANT]  
>  Do not grant this account the right to sign in locally.  

### Enrollment Point Connection Account  
 The **Enrollment Point Connection Account** connects the enrollment point to the Configuration Manager site database. The computer account of the enrollment point is used by default, but you can set up a user account instead. You must specify a user account whenever the enrollment point is in an untrusted domain from the site server. This account requires **Read** and **Write** access to the site database.  

### Exchange Server Connection Account  
 The **Exchange Server Connection Account** connects the site server to the specified Exchange Server computer to find and manage mobile devices that connect to Exchange Server. This account requires Exchange PowerShell cmdlets that provide the required permissions to the Exchange Server computer. For more information about the cmdlets, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### Exchange Server Connector Proxy Server Account  
 The Exchange Server connector uses the **Exchange Server Connector Proxy Server Account** to access the Internet via a proxy server or firewall that requires authenticated access.  

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions for the required proxy server or firewall.  

### Management Point Connection Account  
 The **Management Point Connection Account** is used to connect the management point to the Configuration Manager site database so that it can send and retrieve information for clients. The computer account of the management point is used by default, but you can set up a user account instead. You must specify a user account whenever the management point is in an untrusted domain from the site server.  

 Create the account as a low-rights, local account on the computer that runs Microsoft SQL Server.  

> [!IMPORTANT]  
>  Do not grant interactive sign-in rights to this account.  

### Multicast Connection Account  
 Distribution points that are set up for multicast use the **Multicast Connection Account** to read information from the site database. The computer account of the distribution point is used by default, but you can set up a user account instead. You must specify a user account whenever the site database is in an untrusted forest. For example, if your data center has a perimeter network in a forest other than the site server and site database, you can use this account to read the multicast information from the site database.  

 If you create this account, create it as a low-rights, local account on the computer that runs Microsoft SQL Server.  

> [!IMPORTANT]  
>  Do not grant interactive sign-in rights to this account.  

### Network Access Account  
 Client computers use the **Network Access Account** when they cannot use their local computer account to access content on distribution points. For example, this applies to workgroup clients and computers from untrusted domains. This account might also be used during operating system deployment, when the computer that's installing the operating system does not yet have a computer account on the domain.  

> [!NOTE]  
>  The Network Access Account is never used as the security context to run programs, install software updates, or run task sequences. It's used only for accessing resources on the network.  

 Grant this account the minimum appropriate permissions on the content that the client requires to access the software. The account must have the **Access this computer from the network** right on the distribution point or other server that holds the package content. You can configure up to 10 Network Access Accounts per site.  

> [!WARNING]  
>  When Configuration Manager tries to use the computername$ account to download the content and it fails, it automatically tries the Network Access Account again, even if it has previously tried and failed.  

 Create the account in any domain that will provide the necessary access to resources. The Network Access Account must always include a domain name. Pass-through security is not supported for this account. If you have distribution points in multiple domains, create the account in a trusted domain.  

> [!TIP]  
>  To avoid account lockouts, do not change the password on an existing Network Access Account. Instead, create a new account and set up the new account in Configuration Manager. When sufficient time has passed for all clients to have received the new account details, remove the old account from the network shared folders and delete the account.  

> [!IMPORTANT]  
>  Do not grant interactive sign-in rights to this account.
>   
>  Do not grant this account the right to join computers to the domain. If you must join computers to the domain during a task sequence, use the Task Sequence Editor Domain Joining Account.  

### Package Access Account  
 A **Package Access Account** lets you set NTFS permissions to specify the users and user groups that can access a package folder on distribution points. By default, Configuration Manager grants access only to the generic access accounts **Users** and **Administrators**. You can control access for client computers by using additional Windows accounts or groups. Mobile devices always retrieve package content anonymously, so they don't use the Package Access Accounts.  

 By default, when Configuration Manager creates the package share on a distribution point, it grants **Read** access to the local **Users** group and **Full Control** to the local **Administrators** group. The actual permissions required will depend on the package. If you have clients in workgroups or in untrusted forests, those clients use the Network Access Account to access the package content. Make sure that the Network Access Account has permissions to the package by using the defined Package Access Accounts.  

 Use accounts in a domain that can access the distribution points. If you create or change the account after the package is created, you must redistribute the package. Updating the package does not change the NTFS permissions on the package.  

 You do not have to add the Network Access Account as a Package Access Account, because membership of the Users group adds it automatically. Restricting the Package Access Account to only the Network Access Account does not prevent clients from accessing the package.  

### Reporting Services Point Account  
 SQL Server Reporting Services uses the **Reporting Services Point Account** to retrieve the data for Configuration Manager reports from the site database. The Windows user account and password that you specify are encrypted and stored in the SQL Server Reporting Services database.  
>[!NOTE]
>The account you specify must have Log on Locally permissions on the computer hosting the Reporting Services database.

### Remote Tools Permitted Viewer Accounts  
 The accounts that you specify as **Permitted Viewers** for remote control are a list of users who are allowed to use remote tools functionality on clients.  

### Site System Installation Account  
 The site server uses the **Site System Installation Account** to install, reinstall, uninstall, and set up site systems. If you set up the site system to require the site server to initiate connections to this site system, Configuration Manager also uses this account to pull data from the site system computer after the site system and any site system roles are installed. Each site system can have a different Site System Installation Account, but you can set up only one Site System Installation Account to manage all site system roles on that site system.  

 This account requires local administrative permissions on the site systems that admins will install and set up. Additionally, this account must have **Access this computer from the network** in the security policy on the site systems that admins will install and set up.  

> [!TIP]  
>  If you have many domain controllers and these accounts are used across domains, check that the accounts have replicated before you set up the site system.  
>   
>  When you specify a local account on each site system to be managed, this configuration is more secure than using domain accounts, because it limits the damage that attackers can do if the account is compromised. However, domain accounts are easier to manage. Consider the trade-off between security and effective administration.  

### SMTP Server Connection Account  
 The site server uses the **SMTP Server Connection Account** to send email alerts when the SMTP server requires authenticated access.  

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions to send emails.  

### Software Update Point Connection Account  
 The site server uses the **Software Update Point Connection Account** for the following two software update services:  

-   Windows Server Update Services (WSUS) Configuration Manager, which sets up settings like product definitions, classifications, and upstream settings.  

-   WSUS Synchronization Manager, which requests synchronization to an upstream WSUS server or Microsoft Update.  

The Site System Installation Account can install components for software updates, but it cannot perform software update-specific functions on the software update point. If you cannot use the site server computer account for this functionality because the software update point is in an untrusted forest, you must specify this account in addition to the Site System Installation Account.  

This account must be a local admin on the computer where WSUS is installed. It must also be part of the local WSUS Administrators group.  

### Software Update Point Proxy Server Account  
 The software update point uses the **Software Update Point Proxy Server Account** to access the Internet via a proxy server or firewall that requires authenticated access.  

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions for the required proxy server or firewall.  

### Source Site Account  
 The migration process uses the **Source Site Account** to access the SMS Provider of the source site. This account requires **Read** permissions to site objects in the source site to gather data for migration jobs.  

 If you upgrade Configuration Manager 2007 distribution points or secondary sites that have co-located distribution points to System Center Configuration Manager distribution points, this account must also have **Delete** permissions to the **Site** class to successfully remove the distribution point from the Configuration Manager 2007 site during the upgrade.  

> [!NOTE]  
>  Both the Source Site Account and the Source Site Database Account are identified as **Migration Manager** in the **Accounts** node of the **Administration** workspace in the Configuration Manager console.  

### Source Site Database Account  
 The migration process uses the **Source Site Database Account** to access the SQL Server database for the source site. To gather data from the SQL Server database of the source site, the Source Site Database Account must have the **Read** and **Execute** permissions to the source site's SQL Server database.  

> [!NOTE]  
>  If you use the System Center Configuration Manager computer account, ensure that all the following are true for this account:  
>   
> -   It is a member of the security group **Distributed COM Users** in the domain where the Configuration Manager 2007 site resides.  
> -   It is a member of the **SMS Admins** security group.  
> -   It has the **Read** permission to all Configuration Manager 2007 objects.  

> [!NOTE]  
>  Both the Source Site Account and Source Site Database Account are identified as **Migration Manager** in the **Accounts** node of the **Administration** workspace in the Configuration Manager console.  

### Task Sequence Editor Domain Joining Account  
 The **Task Sequence Editor Domain Joining Account** is used in a task sequence to join a newly imaged computer to a domain. This account is required if you add the step **Join Domain or Workgroup** to a task sequence, and then select **Join a domain**. This account can also be set up if you add the step **Apply Network Settings** to a task sequence, but it is not required.  

 This account requires the **Domain Join** right in the domain that the computer is joining.  

> [!TIP]  
>  If you require this account for your task sequences, you can create one domain user account with minimal permissions to access the required network resources and use it for all task sequence accounts.  

> [!IMPORTANT]  
>  Do not assign interactive sign-in permissions to this account.  
>   
>  Do not use the Network Access Account for this account.  

### Task Sequence Editor Network Folder Connection Account  
 A task sequence uses the **Task Sequence Editor Network Folder Connection Account** to connect to a shared folder on the network. This account is required if you add the step **Connect to Network Folder** to a task sequence.  

 This account requires permissions to access the specified shared folder. It must be a user domain account.  

> [!TIP]  
>  If you require this account for your task sequences, you can create one domain user account with minimal permissions to access the required network resources and use it for all task sequence accounts.  

> [!IMPORTANT]  
>  Do not assign interactive sign-in permissions to this account.  
>   
>  Do not use the Network Access Account for this account.  

### Task Sequence Run As Account  
 The **Task Sequence Run As Account** is used to run command lines in task sequences and use credentials other than the local system account. This account is required if you add the step **Run Command Line** to a task sequence but do not want the task sequence to run with local system account permissions on the managed computer.  

 Set up the account to have the minimum permissions required to run the command line that's specified in the task sequence. The account requires interactive sign-in rights, and it usually requires the ability to install software and access network resources.  

> [!IMPORTANT]  
>  Do not use the Network Access Account for this account.  
>   
>  Never make the account a domain admin.  
>   
>  Never set up roaming profiles for this account. When the task sequence runs, it downloads the roaming profile for the account. This leaves the profile vulnerable to access on the local computer.  
>   
>  Limit the scope of the account. For example, create different Task Sequence Run As Accounts for each task sequence so that if one account is compromised, only the client computers to which that account has access are compromised.  
>   
>  If the command line requires administrative access on the computer, consider creating a local admin account solely for the Task Sequence Run As Account on all computers that run the task sequence. Delete the account as soon as you no longer need it.  
