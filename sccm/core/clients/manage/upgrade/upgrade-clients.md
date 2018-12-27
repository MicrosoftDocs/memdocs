---
title: "Upgrade clients"
titleSuffix: "Configuration Manager"
description: "Get information about how to upgrade clients in System Center Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Upgrade clients in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can use different methods to upgrade the System Center Configuration Manager client software on Windows computers, UNIX and Linux servers, and Mac computers. Here are the advantages and disadvantages of each method.  

> [!TIP]  
>  If you are upgrading your server infrastructure from a previous version of Configuration Manager \(such as Configuration Manager 2007 or System Center 2012 Configuration Manager\), we recommend that you complete the server upgrades including installing all current branch updates, before upgrading the Configuration Manager clients. This way, you'll also have the most recent version of the client software.  

## Group Policy installation  
 **Supported client platform:** Windows  

 **Advantages**  

- Does not require computers to be discovered before the client can be upgraded.  

- Can be used for new client installations or for upgrades.  

- Computers can read client installation properties that have been published to Active Directory Domain Services.  

- Does not require you to configure and maintain an installation account for the intended client computer.  

  **Disadvantages**  

- Can cause high network traffic if you're upgrading a lot of clients.  

- If the Active Directory schema is not extended for Configuration Manager, you must use [Group Policy settings](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) to add client installation properties to computers in your site.  


## Logon script installation  
 **Supported client platform:** Windows  

 **Advantages**  

- Does not require computers to be discovered before the client can be installed.  

- Can be used for new client installations or for upgrades.  

- Supports using command-line properties for CCMSetup.  

  **Disadvantages**  

- Can cause high network traffic if you're upgrading a lot of clients in a short time.  

- Can take a long time to upgrade all client computers if users do not frequently log on to the network.  

  For more information, see [How to Install Configuration Manager Clients by Using Logon Scripts](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## Manual installation  
 **Supported client platform:** Windows, UNIX/Linus, Mac OS X  

 **Advantages**  

- Does not require computers to be discovered before the client can be upgraded.  

- Can be useful for testing purposes.  

- Supports using command-line properties for CCMSetup.  

  **Disadvantages**  

- No automation, therefore time consuming.  

  For more information, see the following topics:  

- [How to Install Configuration Manager Clients Manually](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [How to upgrade clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [How to upgrade clients on Mac computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## Upgrade installation (application management)  
 **Supported client platform:** Windows  

> [!NOTE]  
>  You cannot upgrade Configuration Manager 2007 clients with this method. In this scenario, you can deploy the Configuration Manager client as a package from the Configuration Manager 2007 site, or you can use automatic client upgrade which automatically creates and deploys a package that contains the latest version of the client.  

 **Advantages**  

- Supports using command-line properties for CCMSetup.  

  **Disadvantages**  

- Can cause high network traffic if you distribute the client to large collections.  

- Can only be used to upgrade the client software on computers that have been discovered and assigned to the site.  

  For more information, see [How to Install Configuration Manager Clients by Using a Package and Program](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## Automatic client upgrade  

> [!NOTE]  
>  Can be used to upgrade Configuration Manager 2007 clients to System Center Configuration Manager clients. A Configuration Manager 2007 client can assign to a Configuration Manager site, but cannot perform any actions besides automatic client upgrade.  

 **Supported client platform:** Windows  

 **Advantages**  
- Because of the randomization over the specified period, only auto-upgrade is suitable for large-scale client upgrades. Other methods are either too slow on large scale, or don’t have randomization. 

    > [!Note]
    > Client piloting isn’t good for large scale as it doesn’t randomize at all.  
- Can be used to automatically keep clients in your site at the latest version.  

- Requires minimal administration.  

  **Disadvantages**  

- Can only be used to upgrade the client software and cannot be used to install a new client.  

- Applies to all clients in the hierarchy that are assigned to a site. Cannot be scoped by collection.  

- Limited scheduling options.  

  For more information, see [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## Client testing  
 **Supported client platform:** Windows  

 **Advantages**  

- Can be used to test new client versions in a smaller pre-production collection.  

- When testing is complete, clients in pre-production are promoted to production and automatically upgraded across the Configuration Manager site.  

  **Disadvantages**  

- Can only be used to upgrade the client software and cannot be used to install a new client.  

  [How to test client upgrades in a pre-production collection in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
