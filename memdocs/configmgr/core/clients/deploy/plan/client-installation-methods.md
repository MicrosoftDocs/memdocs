---
title: Client installation methods
titleSuffix: Configuration Manager
description: Learn about the methods of installing the Configuration Manager client.
ms.date: 10/18/2024
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: concept-article
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Client installation methods in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can use different methods to install the Configuration Manager client software. Use one method, or a combination of methods. This article describes each method, so you can learn which one works best for your organization.  

## Client push installation  

**Supported client platform**: Windows  

#### Advantages  

-   Can be used to install the client on a single computer, a collection of computers, or to the results from a query.  

-   Can be used to automatically install the client on all discovered computers.  

-   Automatically uses client installation properties defined on the **Client** tab in the **Client Push Installation Properties** dialog box.  

#### Disadvantages  

-   Can cause high network traffic when pushing to large collections.  

-   Can only be used on computers that have been discovered by Configuration Manager.  

-   Can't be used to install clients in a workgroup.  

-   A client push installation account must be specified that has administrative rights to the intended client computer.  

-   Windows Firewall must be configured with exceptions on client computers.   

-   You can't cancel client push installation. Configuration Manager tries to install the client on all discovered resources. It retries any failures for up to seven days.  

For more information, see [How to install clients with client push](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## Software update point-based installation  

**Supported client platform**: Windows  

#### Advantages  

-   Can use your existing software updates infrastructure to manage the client software.  

-   If Windows Server Update Services (WSUS) and group policy settings in Active Directory Domain Services are configured correctly, it can automatically install the client software on new computers.  

-   Doesn't require computers to be discovered before the client can be installed.  

-   Computers can read client installation properties that have been published to Active Directory Domain Services.  

-   If the client is removed, this method reinstalls it.  

-   Doesn't require you to configure and maintain an installation account for the intended client computer.  

#### Disadvantages  

-   Requires a functioning software updates infrastructure as a prerequisite.  

-   Must use the same server for client installation and software updates. This server must reside in a primary site.  

-   To install new clients, you must configure a group policy object in Active Directory Domain Services with the client's active software update point and port.  

-   If the Active Directory schema isn't extended for Configuration Manager, you must use group policy settings to provision computers with client installation properties.  

For more information, see [How to install clients with software update-based installation](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## Group policy installation  

**Supported client platform**: Windows  

#### Advantages  

-   Doesn't require computers to be discovered before the client can be installed.  

-   Can be used for new client installations or for upgrades.  

-   Computers can read client installation properties that have been published to Active Directory Domain Services.  

-   Doesn't require you to configure and maintain an installation account for the intended client computer.  

#### Disadvantages  

-   If a large number of clients are being installed, it can cause high network traffic.  

-   If the Active Directory schema isn't extended for Configuration Manager, you must use group policy settings to add client installation properties to computers in your site.  

For more information, see [How to install clients with group policy](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## Logon script installation  

**Supported client platform**: Windows  

#### Advantages  

-   Doesn't require computers to be discovered before the client can be installed.  

-   Supports using command-line properties for CCMSetup.  

#### Disadvantages  

-   If a large number of clients are being installed over a short time period, it can cause high network traffic.  

-   If users don't frequently log on to the network, it can take a long time to install on all client computers.  

For more information, see [How to install clients with logon scripts](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## Manual installation  

**Supported client platform**: Windows, macOS X  

#### Advantages  

-   Doesn't require computers to be discovered before the client can be installed.  

-   Can be useful for testing purposes.  

-   Supports using command-line properties for CCMSetup.  

#### Disadvantages  

-   No automation, therefore time consuming.  

For more information about how to manually install the client on each of platform, see the following articles:  

-   [How to deploy clients to Windows computers](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [How to deploy clients to Macs](../deploy-clients-to-macs.md)  



## Microsoft Intune MDM installation

**Supported client platforms**: Windows 10 or later

#### Advantages  

-   Doesn't require computers to be discovered before the client can be installed.  

-   Doesn't require you to configure and maintain an installation account for the intended client computer.  

-   Can use modern authentication with Microsoft Entra ID.  

-   Can install and assign computers on the internet.  

-   Can automate with Windows Autopilot and Microsoft Intune for co-management.  

#### Disadvantages

- Requires additional technologies outside of Configuration Manager.

- Requires the device have access to the internet, even if it is not internet-based.

For more information, see the following articles:

- [How to install clients to Intune MDM-managed Windows devices](../deploy-clients-to-windows-computers.md#bkmk_mdm)

- [Install and assign Configuration Manager clients using Microsoft Entra ID for authentication](../deploy-clients-cmg-azure.md)
