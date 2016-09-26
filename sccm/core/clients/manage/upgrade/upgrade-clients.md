---
title: "Upgrade clients in System Center Configuration Manager"
ms.custom: na
ms.date: 03/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: 8
author: Mtillman

---
# Upgrade clients in System Center Configuration Manager
You can use different methods to upgrade the System Center Configuration Manager client software on Windows computers, UNIX and Linux servers, and Mac computers in your enterprise. The following sections outlines the advantages and disadvantages of each client upgrade method to help you determine which will work best for your organization.  

> [!TIP]  
>  If you are upgrading your server infrastructure from a previous version of Configuration Manager \(such as Configuration Manager 2007 or System Center 2012 Configuration Manager\), we recommend that you complete the server upgrades including installing all current branch updates, before upgrading the Configuration Manager clients.   The latest current branch update contains the latest version of the client, so it's best to do client upgrades after you have installed all of the Configuration Manager updates you want to use.  

## Group Policy installation  
 **Supported client platform:** Windows  

 **Advantages**  

-   Does not require computers to be discovered before the client can be upgraded.  

-   Can be used for new client installations or for upgrades.  

-   Computers can read client installation properties that have been published to Active Directory Domain Services.  

-   Does not require you to configure and maintain an installation account for the intended client computer.  

 **Disadvantages**  

-   Can cause high network traffic if a large number of clients are being upgraded.  

-   If the Active Directory schema is not extended for Configuration Manager, you must use Group Policy settings to add client installation properties to computers in your site.  

 For more information, see [How to Install Configuration Manager Clients by Using Group Policy](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP).  

## Logon script installation  
 **Supported client platform:** Windows  

 **Advantages**  

-   Does not require computers to be discovered before the client can be installed.  

-   Can be used for new client installations or for upgrades.  

-   Supports using command-line properties for CCMSetup.  

 **Disadvantages**  

-   Can cause high network traffic if a large number of clients are being upgraded over a short time period.  

-   Can take a long time to upgrade on all client computers if users do not frequently log on to the network.  

 For more information, see [How to Install Configuration Manager Clients by Using Logon Scripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## Manual installation  
 **Supported client platform:** Windows, UNIX/Linus, Mac OS X  

 **Advantages**  

-   Does not require computers to be discovered before the client can be upgraded.  

-   Can be useful for testing purposes.  

-   Supports using command-line properties for CCMSetup.  

 **Disadvantages**  

-   No automation, therefore time consuming.  

 For more information, see the following topics:  

-   [How to Install Configuration Manager Clients Manually](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [How to upgrade clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [How to upgrade clients on Mac computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## Upgrade installation (application management)  
 **Supported client platform:** Windows  

> [!NOTE]  
>  You cannot upgrade Configuration Manager 2007 clients by using this method. In this scenario, you can deploy the Configuration Manager client as a package from the Configuration Manager 2007 site, or you can use automatic client upgrade which automatically creates and deploys a package that contains the latest version of the client.  

 **Advantages**  

-   Supports using command-line properties for CCMSetup.  

 **Disadvantages**  

-   Can cause high network traffic when distributing the client to large collections.  

-   Can only be used to upgrade the client software on computers that have been discovered and assigned to the site.  

 For more information, see [How to Install Configuration Manager Clients by Using a Package and Program](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## Automatic client upgrade  

> [!NOTE]  
>  Can be used to upgrade Configuration Manager 2007 clients to System Center Configuration Manager clients. A Configuration Manager 2007client can assign to a Configuration Manager site, but cannot perform any actions besides automatic client upgrade.  

 **Supported client platform:** Windows  

 **Advantages**  

-   Can be used to automatically keep clients in your site at the latest version.  

-   Requires minimal administration by the administrative user.  

 **Disadvantages**  

-   Can only be used to upgrade the client software and cannot be used to install a new client.  

-   Not suitable for upgrading many clients simultaneously.  

-   Applies to all clients in the hierarchy that are assigned to a site. Cannot be scoped by collection.  

-   Limited scheduling options.  

 For more information, see [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## Client testing  
 **Supported client platform:** Windows  

 **Advantages**  

-   Can be used to test new client versions in a smaller preproduction collection.  

-   When testing is complete, clients in preproduction are promoted to production and automatically upgraded across the Configuration Manager site.  

 **Disadvantages**  

-   Can only be used to upgrade the client software and cannot be used to install a new client.  

 [How to test client upgrades in a preproduction collection in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  

