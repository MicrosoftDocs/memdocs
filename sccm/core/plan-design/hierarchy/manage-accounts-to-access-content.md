---
title: "Accounts to access content"
titleSuffix: "Configuration Manager"
description: "Learn about the accounts where clients access System Center Configuration Manager content."
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Manage accounts to access content in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before deploying content in System Center Configuration Manager, consider how clients will access that content from distribution points. This article describes the following accounts used for this purpose:

-   **Network Access Account**. Used by clients to connect to a distribution point and access content. By default, clients first try their computer account.

     This account is also used by pull-distribution points to obtain content from a source distribution point in a remote forest.  

-   **Package Access Account**. By default, Configuration Manager grants access to content on a distribution point to the built-in accounts named **Users** and **Administrators**. You can set up additional permissions to restrict access.  

-   **Multicast Connection Account**. Used for operating system deployments.  

##  <a name="bkmk_NAA"></a> Network Access Account  
 Client computers use the Network Access Account when they cannot use their local computer account to access content on distribution points. For example, this applies to workgroup clients and computers from untrusted domains. This account might also be used during operating system deployment when the computer installing the operating system does not yet have a computer account on the domain.  

-   Clients only use the Network Access Account for accessing resources on the network.  

-   At each primary site, you can set up multiple accounts for use as a Network Access Account.  

-   Clients first try to access content on a distribution point by using their *computername*$ account. If this account fails, clients then attempt to use a Network Access Account. Clients continue to attempt to use the Network Access Account, even if it has previously failed.  

### Permissions
Grant this account the minimum appropriate permissions to access the software for the content that the client requires.  

-   The account must have the **Access this computer from the network** right on the distribution point.  

-   Create the account in any domain that provides the necessary access to resources. The Network Access Account must always include a domain name. Pass-through security is not supported for this account. If you have distribution points in multiple domains, create the account in a trusted domain.  

> [!TIP]  
>  To avoid account lockouts, do not change the password on an existing Network Access Account. Instead, create a new account, and set up the new account in Configuration Manager. When sufficient time has passed for all clients to have received the new account details, remove the old account from the network shared folders, and delete the account.  

> [!IMPORTANT]  
>  Do not grant this account interactive rights to sign in.  
>   
>  Do not grant this account the right to join computers to the domain. If you must join computers to the domain during a task sequence, use the Task Sequence Editor Domain Joining Account.  

### To configure the Network Access Account  

1.  In the Configuration Manager console, choose **Administration** >   **Site Configuration** >  **Sites**, and then select the site.  

2.  On the **Settings** group, choose **Configure Site Components** > **Software Distribution**.  

3.  Choose the **Network Access Account** tab. Set up one or more accounts, and then choose **OK**.  

##  <a name="bkmk_Paa"></a> Package Access Accounts  
 Package Access Accounts let you set NTFS file system permissions to specify the users and user groups that can access package content on distribution points. By default, Configuration Manager grants access only to the generic **Users** and **Administrators** accounts. You can control access for client computers, however, by using additional Windows accounts or groups. Mobile devices don't use the Package Access Accounts, because these devices always retrieve package content anonymously.  

 By default, when Configuration Manager copies the content files in a package to a distribution point, it grants **Read** access to the local **Users** group and **Full Control** to the local **Administrators** group. The actual permissions that are required depend on the package. If you have clients in workgroups or in untrusted forests, those clients use the Network Access Account to access the package content. Ensure that the Network Access Account has permissions to the package by using the defined Package Access Accounts.  

 Use accounts in a domain that can access the distribution points. If you create or modify the account after the package is created, you must redistribute the package. Updating the package does not change the NTFS file system permissions on the package.  

 You do not have to add the Network Access Account as a Package Access Account, because membership of the **Users** group adds it automatically. Restricting the Package Access Account to only the Network Access Account does not prevent clients from accessing the package.  

### To manage access accounts  

1.  In the Configuration Manager console, choose **Software Library**.  

2.  In the **Software Library** workspace, determine the type of content for which you want to manage access accounts, and follow the steps provided:  

    -   **Applications**: Expand **Application Management**, choose **Applications**, and then select the applications for which to manage access accounts.  

    -   **Packages**: Expand **Application Management**, choose **Packages**, and then select the packages for which to manage access accounts.  

    -   **Deployment Packages**: Expand **Software Updates**, choose **Deployment Packages**, and then select the deployment packages for which to manage access accounts.  

    -   **Driver Packages**: Expand **Operating Systems**, choose **Driver Packages**, and then select the driver packages for which to manage access accounts.  

    -   **Operating System Images**: Expand **Operating Systems**, choose **Operating System Images**, and then select the operating system images for which to manage access accounts.  

    -   **Operating System Installers**: Expand **Operating Systems**, choose **Operating System Installers**, and then select the operating system installers for which to manage access accounts.  

    -   **Boot Images**: Expand **Operating Systems**, choose **Boot Images**, and then select the boot images for which to manage access accounts.  

3.  Right-click the selected object, and then choose **Manage Access Accounts**.  

4.  In the **Add Account** dialog box, specify the account type that will be granted access to the content, and then specify the access rights associated with the account.  

    > [!NOTE]  
    >  When you add a user name for the account, and Configuration Manager finds both a local user account and a domain user account with that name, Configuration Manager sets access rights for the domain user account.  

##  <a name="bkmk_multi"></a> Multicast Connection Account  
 The Multicast Connection Account is used by distribution points that are set up for multicast to read information from the site database.  

-   You specify an account to use when you set up Configuration Manager database connections for multicast.  

-   By default, the computer account of the distribution point is used, but you can set up a user account instead.  

-   You must specify a user account whenever the site database is in an untrusted forest.  

-   The account must have **Read** permissions to the site database.  

For example, if your data center has a perimeter network in a forest other than the site server and site database, you can use this account to read the multicast information from the site database.

If you create this account, create it as a low-rights, local account on the computer that runs Microsoft SQL Server.  

> [!IMPORTANT]  
>  Do not grant this account interactive rights to sign in.  
