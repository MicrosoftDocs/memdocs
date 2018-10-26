---
title: Accounts used
titleSuffix: Configuraton Manager
description: Identify and manage the Windows groups and the accounts used in Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Accounts used in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the following information to identify the Windows groups and the accounts that are used in Configuration Manager, how they're used, and any requirements.  

- [Windows groups that Configuration Manager creates and uses](#bkmk_groups)  
    - [ConfigMgr_CollectedFilesAccess](#configmgrcollectedfilesaccess)  
    - [ConfigMgr_DViewAccess](#configmgrdviewaccess)  
    - [ConfigMgr Remote Control Users](#configmgr-remote-control-users)  
    - [SMS Admins](#sms-admins)  
    - [SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>](#bkmk_remotemp)  
    - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>](#bkmk_remoteprov)  
    - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>](#bkmk_remotestat)  
    - [SMS_SiteToSiteConnection_&lt;sitecode\>](#bkmk_filerepl)  

- [Accounts that Configuration Manager uses](#bkmk_accounts)
    - [Active Directory group discovery account](#active-directory-group-discovery-account)  
    - [Active Directory system discovery account](#active-directory-system-discovery-account)  
    - [Active Directory user discovery account](#active-directory-user-discovery-account)  
    - [Active Directory forest account](#active-directory-forest-account)  
    - [Certificate registration point account](#certificate-registration-point-account)  
    - [Capture OS image account](#capture-os-image-account)  
    - [Client push installation account](#client-push-installation-account)  
    - [Enrollment point connection account](#enrollment-point-connection-account)  
    - [Exchange Server connection account](#exchange-server-connection-account)  
    - [Management point connection account](#management-point-connection-account)  
    - [Multicast connection account](#multicast-connection-account)  
    - [Network access account](#network-access-account)  
    - [Package access account](#package-access-account)  
    - [Reporting services point account](#reporting-services-point-account)  
    - [Remote tools permitted viewer accounts](#remote-tools-permitted-viewer-accounts)  
    - [Site system installation account](#site-system-installation-account)  
    - [Site system proxy server account](#site-system-proxy-server-account)  
    - [SMTP server connection account](#smtp-server-connection-account)  
    - [Software update point connection account](#software-update-point-connection-account)  
    - [Source site account](#source-site-account)  
    - [Source site database account](#source-site-database-account)  
    - [Task sequence domain join account](#task-sequence-domain-join-account)  
    - [Task sequence network folder connection account](#task-sequence-network-folder-connection-account)  
    - [Task sequence run as account](#task-sequence-run-as-account)  



## <a name="bkmk_groups"></a> Windows groups that Configuration Manager creates and uses  

 Configuration Manager automatically creates, and in many cases automatically maintains, the following Windows groups:  

> [!NOTE]  
>  When Configuration Manager creates a group on a computer that's a domain member, the group is a local security group. If the computer is a domain controller, the group is a domain local group. This type of group is shared among all domain controllers in the domain.  


### ConfigMgr_CollectedFilesAccess  

Configuration Manager uses this group to grant access to view files collected by software inventory.  

For more information, see [Introduction to software inventory](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

#### Type and location
This group is a local security group created on the primary site server.

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Membership
Configuration Manager automatically manages the group membership. Membership includes administrative users that are granted the **View Collected Files** permission to the **Collection** securable object from an assigned security role.

#### Permissions
By default, this group has **Read** permission to the following folder on the site server: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### ConfigMgr_DViewAccess  

 This group is a local security group that Configuration Manager creates on the site database server or database replica server for a child primary site. The site creates it when you use distributed views for database replication between sites in a hierarchy. It contains the site server and SQL Server computer accounts of the central administration site.

 For more information, see [Data transfers between sites](/sccm/core/servers/manage/data-transfers-between-sites).


### ConfigMgr Remote Control Users  

 Configuration Manager remote tools use this group to store the accounts and groups that you set up in the **Permitted Viewers** list. The site assigns this list to each client.  

For more information, see [Introduction to remote control](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).

#### Type and location
This group is a local security group created on the Configuration Manager client when the client receives a policy that enables remote tools.

After you disable remote tools for a client, this group isn't automatically removed. Manually delete it after disabling remote tools.

#### Membership
By default, there are no members in this group. When you add users to the **Permitted Viewers** list, they're automatically added to this group.

Use the **Permitted Viewers** list to manage the membership of this group instead of adding users or groups directly to this group.

In addition to being a permitted viewer, an administrative user must have the **Remote Control** permission to the **Collection** object. Assign this permission by using the **Remote Tools Operator** security role.  

#### Permissions
By default, this group doesn't have permissions to any locations on the computer. It's used only to hold the **Permitted Viewers** list.  


### SMS Admins  

 Configuration Manager uses this group to grant access to the SMS Provider through WMI. Access to the SMS Provider is required to view and change objects in the Configuration Manager console.  

> [!NOTE]  
>  The role-based administration configuration of an administrative user determines which objects they can view and manage when using the Configuration Manager console.  

For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### Type and location
This group is a local security group created on each computer that has an SMS Provider. 

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Membership
Configuration Manager automatically manages the group membership. By default, each administrative user in a hierarchy and the site server computer account are members of the **SMS Admins** group on each SMS Provider computer in a site.

#### Permissions
You can view the rights and permissions for the SMS Admins group in the **WMI Control** MMC snap-in. By default, this group is granted **Enable Account** and **Remote Enable** on the `Root\SMS` WMI namespace. Authenticated users have **Execute Methods**, **Provider Write**, and **Enable Account**.

When you use a remote Configuration Manager console, configure **Remote Activation** DCOM permissions on both the site server computer and the SMS Provider. Grant these rights to the **SMS Admins** group. This action simplifies administration instead of granting these rights directly to users or groups. For more information, see [Configure DCOM permissions for remote Configuration Manager consoles](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 
Management points that are remote from the site server use this group to connect to the site database. This group provides a management point access to the inbox folders on the site server and the site database.  

#### Type and location
This group is a local security group created on each computer that has an SMS Provider.

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Membership
Configuration Manager automatically manages the group membership. By default, membership includes the computer accounts of remote computers that have a management point for the site.

#### Permissions
By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the following folder on the site server: `C:\Program Files\Microsoft Configuration Manager\inboxes`. This group has the additional permission of **Write** to subfolders below **inboxes**, to which the management point writes client data.


### <a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 
Remote SMS Provider computers use this group to connect to the site server.  

#### Type and location
This group is a local security group created on the site server.

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Membership
Configuration Manager automatically manages the group membership. By default, membership includes the computer account or a domain user account. It uses this account to connect to the site server from each remote SMS Provider.

#### Permissions
By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the following folder on the site server: `C:\Program Files\Microsoft Configuration Manager\inboxes`. This group has the additional permissions of **Write** and **Modify** to subfolders below the inboxes. The SMS Provider requires access to these folders.

This group also has **Read** permission to the subfolders on the site server below `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

It also has the following permissions to the subfolders below `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Read**  
- **Read & execute**  
- **List folder contents**  
- **Write**  
- **Modify**   


### <a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  

The file dispatch manager component on Configuration Manager remote site system computers uses this group to connect to the site server.  

#### Type and location
This group is a local security group created on the site server.

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Membership
Configuration Manager automatically manages the group membership. By default, membership includes the computer account or the domain user account. It uses this account to connect to the site server from each remote site system that runs the file dispatch manager.

#### Permissions
By default, this group has **Read**, **Read & execute**, and **List folder contents** permission to the following folder and its subfolders on the site server: `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

This group has the additional permissions of **Write** and **Modify** to the following folder on the site server: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;sitecode\>  
 Configuration Manager uses this group to enable file-based replication between sites in a hierarchy. For each remote site that directly transfers files to this site, this group has accounts set up as a **File Replication Account**.  

#### Type and location
This group is a local security group created on the site server.

#### Membership
When you install a new site as a child of another site, Configuration Manager automatically adds the computer account of the new site server to this group on the parent site server. Configuration Manager also adds the parent site's computer account to the group on the new site server. If you specify another account for file-based transfers, add that account to this group on the destination site server.

When you uninstall a site, this group isn't automatically removed. Manually delete it after uninstalling a site.

#### Permissions
By default, this group has **Full control** to the following folder: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="bkmk_accounts"></a> Accounts that Configuration Manager uses  

 You can set up the following accounts for Configuration Manager.  


### Active Directory group discovery account  

 The site uses the **Active Directory group discovery account** to discover the following objects from the locations in Active Directory Domain Services that you specify:
 - Local, global, and universal security groups
 - The membership within these groups
 - The membership within distribution groups
    - Distribution groups aren't discovered as group resources

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that you specify for discovery.  

 For more information, see [Active Directory group discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutGroup).


### Active Directory system discovery account  

 The site uses the **Active Directory system discovery account** to discover computers from the locations in Active Directory Domain Services that you specify.  

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that you specify for discovery.  

 For more information, see [Active Directory system discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutSystem).


### Active Directory user discovery account  
 
 The site uses the **Active Directory user discovery account** to discover user accounts from the locations in Active Directory Domain Services that you specify.  

 This account can be a computer account of the site server that runs discovery, or a Windows user account. It must have **Read** access permission to the Active Directory locations that you specify for discovery.  

 For more information, see [Active Directory user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser). 


### Active Directory forest account  

 The site uses the **Active Directory forest account** to discover network infrastructure from Active Directory forests. Central administration sites and primary sites also use it to publish site data to Active Directory Domain Services for a forest.  

 > [!NOTE]  
 >  Secondary sites always use the secondary site server computer account to publish to Active Directory.  

 To discover and publish to untrusted forests, the Active Directory forest account must be a global account. If you don't use the computer account of the site server, you can select only a global account.  

 This account must have **Read** permissions to each Active Directory forest where you want to discover network infrastructure.  

 This account must have **Full Control** permissions to the **System Management** container and all its child objects in each Active Directory forest where you want to publish site data. For more information, see [Prepare Active Directory for site publishing](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

 For more information, see [Active Directory forest discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutForest).


### Certificate registration point account  

 The certificate registration point uses the **Certificate registration point account** to connect to the Configuration Manager database. It uses its computer account by default, but you can configure a user account instead. When the certificate registration point is in an untrusted domain from the site server, you must specify a user account. This account requires only **Read** access to the site database, because the state message system handles write tasks.  

 For more information, see [Introduction to certificate profiles](/sccm/protect/deploy-use/introduction-to-certificate-profiles).


### Capture OS image account  

 When you capture an OS image, Configuration Manager uses the **Capture OS image account** to access the folder where you store captured images. If you add the **Capture OS Image** step to a task sequence, this account is required.  

 The account must have **Read** and **Write** permissions on the network share where you store captured images.  

 If you change the password for the account in Windows, update the task sequence with the new password. The Configuration Manager client receives the new password when it next downloads the client policy.  

 If you need to use this account, create one domain user account. Grant it minimal permissions to access the required network resources, and use it for all capture task sequences.  

 > [!IMPORTANT]  
 >  Don't assign interactive sign-in permissions to this account.  
 >   
 >  Don't use the network access account for this account.  

 For more information, see [Create a task sequence to capture an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


### Client push installation account  

 When you deploy clients by using the client push installation method, the site uses the **Client push installation account** to connect to computers and install the Configuration Manager client software. If you don't specify this account, the site server tries to use its computer account.  

 This account must be a member of the local **Administrators** group on the target client computers. This account doesn't require **Domain Admin** rights.  

 You can specify more than one client push installation account. Configuration Manager tries each one in turn until one succeeds.  

> [!TIP]  
>  If you have a large Active Directory environment and need to change this account, use the following process to more effectively coordinate this account update: 
> 1. Create a new account with a different name   
> 2. Add the new account to the list of client push installation accounts in Configuration Manager  
> 3. Allow sufficient time for Active Directory Domain Services to replicate the new account  
> 4. Then remove the old account from Configuration Manager and Active Directory Domain Services  

> [!IMPORTANT]  
>  Don't grant this account the right to sign in locally.  

 For more information, see [Client push installation](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).


### Enrollment point connection account  

 The enrollment point uses the **Enrollment point connection account** to connect to the Configuration Manager site database. It uses its computer account by default, but you can configure a user account instead. When the enrollment point is in an untrusted domain from the site server, you must specify a user account. This account requires **Read** and **Write** access to the site database.  

 For more information, see [Install site system roles for on-premises MDM](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).


### Exchange Server connection account  

 The site server uses the **Exchange Server connection account** to connect to the specified Exchange Server. It uses this connection to find and manage mobile devices that connect to Exchange Server. This account requires Exchange PowerShell cmdlets that provide the required permissions to the Exchange Server computer. For more information about the cmdlets, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### Management point connection account  

 The management point uses the **Management point connection account** to connect to the Configuration Manager site database. It uses this connection to send and retrieve information for clients. The management point uses its computer account by default, but you can configure a user account instead. When the management point is in an untrusted domain from the site server, you must specify a user account.  

 Create the account as a low-rights, local account on the computer that runs Microsoft SQL Server.  

> [!IMPORTANT]  
>  Don't grant interactive sign-in rights to this account.  


### Multicast connection account  

 Multicast-enabled distribution points use the **Multicast connection account** to read information from the site database. The server uses its computer account by default, but you can configure a user account instead. When the site database is in an untrusted forest, you must specify a user account. For example, if your data center has a perimeter network in a forest other than the site server and site database, use this account to read the multicast information from the site database.  

 If you need this account, create it as a low-rights, local account on the computer that runs Microsoft SQL Server.  

> [!IMPORTANT]  
>  Don't grant interactive sign-in rights to this account.  

 For more information, see [Use multicast to deploy Windows over the network](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).


### Network access account  

 Client computers use the **network access account** when they can't use their local computer account to access content on distribution points or peers. It mostly applies to workgroup clients and computers from untrusted domains. This account is also used during OS deployment, when the computer that's installing the OS doesn't yet have a computer account on the domain.  

> [!Important]  
>  The network access account is never used as the security context to run programs, install software updates, or run task sequences. It's used only for accessing resources on the network.  

 A Configuration Manager client first tries to use its computer account to download the content. If it fails, it then automatically tries the network access account. It continues to try using the network access account, even if it has previously failed.  

<!--Starting in version 1806...-->

#### Permissions

 Grant this account the minimum appropriate permissions on the content that the client requires to access the software. The account must have the **Access this computer from the network** right on the distribution point or peer that stores the package content. You can configure up to 10 network access accounts per site.  

 Create the account in any domain that provides the necessary access to resources. The network access account must always include a domain name. Pass-through security isn't supported for this account. If you have distribution points in multiple domains, create the account in a trusted domain.  

> [!TIP]  
> To avoid account lockouts, don't change the password on an existing network access account. Instead, create a new account and set up the new account in Configuration Manager. When sufficient time has passed for all clients to have received the new account details, remove the old account from the network shared folders and delete the account.  

> [!IMPORTANT]  
>  Don't grant interactive sign-in rights to this account.  
>   
>  Don't grant this account the right to join computers to the domain. If you must join computers to the domain during a task sequence, use the [Task sequence domain join account](#task-sequence-domain-join-account).  

#### Configure the network access account  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Then select the site.  

2.  On the **Settings** group of the ribbon, select **Configure Site Components**, and choose **Software Distribution**.  

3.  Choose the **Network access account** tab. Set up one or more accounts, and then choose **OK**.  


### Package access account  

 A **Package access account** lets you set NTFS permissions to specify the users and user groups that can access package content on distribution points. By default, Configuration Manager grants access only to the generic access accounts **User** and **Administrator**. You can control access for client computers by using additional Windows accounts or groups. Mobile devices always retrieve package content anonymously, so they don't use a package access account.  

 By default, when Configuration Manager copies the content files to a distribution point, it grants **Read** access to the local **Users** group, and **Full Control** to the local **Administrators** group. The actual permissions required depend on the package. If you have clients in workgroups or in untrusted forests, those clients use the network access account to access the package content. Make sure that the network access account has permissions to the package by using the defined package access accounts.  

 Use accounts in a domain that can access the distribution points. If you create or modify the account after you create the package, you must redistribute the package. Updating the package doesn't change the NTFS permissions on the package.  

 You don't have to add the network access account as a package access account, because membership of the **Users** group adds it automatically. Restricting the package access account to only the network access account doesn't prevent clients from accessing the package.  

#### Manage package access accounts  

1.  In the Configuration Manager console, choose **Software Library**.  

2.  In the **Software Library** workspace, determine the type of content for which you want to manage access accounts, and follow the steps provided:  

    -   **Application**: Expand **Application Management**, choose **Applications**, and then select the application for which to manage access accounts.  

    -   **Package**: Expand **Application Management**, choose **Packages**, and then select the package for which to manage access accounts.  

    -   **Software update deployment package**: Expand **Software Updates**, choose **Deployment Packages**, and then select the deployment package for which to manage access accounts.  

    -   **Driver package**: Expand **Operating Systems**, choose **Driver Packages**, and then select the driver package for which to manage access accounts.  

    -   **OS image**: Expand **Operating Systems**, choose **Operating System Images**, and then select the operating system image for which to manage access accounts.  

    -   **OS upgrade package**: Expand **Operating Systems**, choose **Operating system upgrade packages**, and then select the OS upgrade package for which to manage access accounts.  

    -   **Boot image**: Expand **Operating Systems**, choose **Boot Images**, and then select the boot image for which to manage access accounts.  

3.  Right-click the selected object, and then choose **Manage Access Accounts**.  

4.  In the **Add Account** dialog box, specify the account type that will be granted access to the content, and then specify the access rights associated with the account.  

    > [!NOTE]  
    >  When you add a user name for the account, and Configuration Manager finds both a local user account and a domain user account with that name, Configuration Manager sets access rights for the domain user account.  


### Reporting services point account  
 
 SQL Server Reporting Services uses the **Reporting services point account** to retrieve the data for Configuration Manager reports from the site database. The Windows user account and password that you specify are encrypted and stored in the SQL Server Reporting Services database.  

 > [!NOTE]  
 > The account you specify must have **Log on locally** permissions on the computer hosting the SQL Reporting Services database.

 For more information, see [Introduction to reporting](/sccm/core/servers/manage/introduction-to-reporting).


### Remote tools permitted viewer accounts  

 The accounts that you specify as **Permitted Viewers** for remote control are a list of users who are allowed to use remote tools functionality on clients.  

For more information, see [Introduction to remote control](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).


### Site system installation account  

 The site server uses the **Site system installation account** to install, reinstall, uninstall, and set up site systems. If you set up the site system to require the site server to initiate connections to this site system, Configuration Manager also uses this account to pull data from the site system after it installs the site system and any roles. Each site system can have a different installation account, but you can set up only one installation account to manage all roles on that site system.  

 This account requires local administrative permissions on the target site systems. Additionally, this account must have **Access this computer from the network** in the security policy on the target site systems.  

 > [!TIP]  
 >  If you have many domain controllers and these accounts are used across domains, before you set up the site system, check that Active Directory has replicated these accounts.  
 >   
 >  When you specify a local account on each site system to be managed, this configuration is more secure than using domain accounts. It limits the damage that attackers can do if the account is compromised. However, domain accounts are easier to manage. Consider the trade-off between security and effective administration.  


### Site system proxy server account
<!--SCCMDocs issue #648-->
 The following site system roles use the **Site system proxy server account** to access the internet via a proxy server or firewall that requires authenticated access:

- Asset Intelligence synchronization point
- Exchange Server connector
- Service connection point
- Software update point

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions for the required proxy server or firewall.  

 For more information, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support).


### SMTP server connection account  

 The site server uses the **SMTP server connection account** to send email alerts when the SMTP server requires authenticated access.  

> [!IMPORTANT]  
>  Specify an account that has the least possible permissions to send emails.  

 For more information, see [Use alerts and the status system](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### Software update point connection account  

 The site server uses the **Software update point connection account** for the following two software update services:  

-   Windows Server Update Services (WSUS), which sets up settings like product definitions, classifications, and upstream settings.  

-   WSUS Synchronization Manager, which requests synchronization to an upstream WSUS server or Microsoft Update.  

The [site system installation account](#site-system-installation-account) can install components for software updates, but it can't perform software update-specific functions on the software update point. If you can't use the site server computer account for this functionality because the software update point is in an untrusted forest, you must specify this account in addition to the site system installation account.  

This account must be a local administrator on the computer where you install WSUS. It must also be part of the local **WSUS Administrators** group.  

For more information, see [Plan for software updates](/sccm/sum/plan-design/plan-for-software-updates).


### Source site account  

 The migration process uses the **Source site account** to access the SMS Provider of the source site. This account requires **Read** permissions to site objects in the source site to gather data for migration jobs.  

 If you have Configuration Manager 2007 distribution points or secondary sites with colocated distribution points, when you upgrade them to Configuration Manager (current branch) distribution points, this account must also have **Delete** permissions to the **Site** class. This permission is to successfully remove the distribution point from the Configuration Manager 2007 site during the upgrade.  

> [!NOTE]  
>  Both the source site account and the [source site database account](#source-site-database-account) are identified as **Migration Manager** in the **Accounts** node of the **Administration** workspace in the Configuration Manager console.  

 For more information, see [Migrate data between hierarchies](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### Source site database account  

 The migration process uses the **Source site database account** to access the SQL Server database for the source site. To gather data from the SQL Server database of the source site, the source site database account must have the **Read** and **Execute** permissions to the source site's SQL Server database.  

 If you use the Configuration Manager (current branch) computer account, make sure that all the following are true for this account:  
   
 - It's a member of the **Distributed COM Users** security group in the same domain as the Configuration Manager 2007 site  
 - It's a member of the **SMS Admins** security group  
 - It has the **Read** permission to all Configuration Manager 2007 objects  

> [!NOTE]  
>  Both the source site account and the [source site database account](#source-site-database-account) are identified as **Migration Manager** in the **Accounts** node of the **Administration** workspace in the Configuration Manager console.  

 For more information, see [Migrate data between hierarchies](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### Task sequence domain join account 

 Windows Setup uses the **Task sequence domain join account** to join a newly imaged computer to a domain. This account is required by the [Join Domain or Workgroup](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup) task sequence step with the **Join a domain** option. This account can also be set up with the [Apply Network Settings](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyNetworkSettings) step, but it isn't required.  

 This account requires the **Domain Join** right in the target domain.  

> [!TIP]  
>  Create one domain user account with the minimal permissions to join the domain, and use it for all task sequences.  

> [!IMPORTANT]  
>  Don't assign interactive sign-in permissions to this account.  
>   
>  Don't use the network access account for this account.  


### Task sequence network folder connection account  

 The task sequence engine uses the **Task sequence network folder connection account** to connect to a shared folder on the network. This account is required by the [Connect to Network Folder](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) task sequence step.  

 This account requires permissions to access the specified shared folder. It must be a domain user account.  

> [!TIP]  
>  Create one domain user account with minimal permissions to access the required network resources, and use it for all task sequences.  

> [!IMPORTANT]  
>  Don't assign interactive sign-in permissions to this account.  
>   
>  Don't use the network access account for this account.  


### Task sequence run as account  

 The task sequence engine uses the **Task sequence run as account** to run command lines with credentials other than the Local System account. This account is required by the [Run Command Line](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) task sequence step with the option **Run this step as the following account**.  

 Set up the account to have the minimum permissions required to run the command line that you specify in the task sequence. The account requires interactive sign-in rights. It usually requires the ability to install software and access network resources.  

> [!IMPORTANT]  
>  Don't use the network access account for this account.  
>   
>  Never make the account a domain admin.  
>   
>  Never set up roaming profiles for this account. When the task sequence runs, it downloads the roaming profile for the account. This leaves the profile vulnerable to access on the local computer.  
>   
>  Limit the scope of the account. For example, create different task sequence run as accounts for each task sequence. Then if one account is compromised, only the client computers to which that account has access are compromised.  
>   
>  If the command line requires administrative access on the computer, consider creating a local administrator account solely for this account on all computers that run the task sequence. Delete the account once you no longer need it.  

