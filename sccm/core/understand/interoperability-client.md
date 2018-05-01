---
title: Extended interoperability client
titleSuffix: Configuration Manager
description: Learn about using the extended interoperability client for long-term support of a static Configuration Manager client with a current branch site.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby

---

# Use the Configuration Manager client software for extended interoperability with future versions of a Current Branch site

*Applies to: System Center Configuration Manager (Current Branch)*  

Business requirements might not allow you to regularly update the Configuration Manager client on some devices. For example, you might need to comply with change management policies, or the device might be mission-critical. Accommodate these needs by installing a new client for long-term use, called the extended interoperability client (EIC). Only use the EIC for specific devices that can't be frequently updated, like kiosk or point-of-sale devices. Continue to use [automatic client upgrade](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) for most of your clients. 

## How this scenario works

Typically, when you install a new [in-console update](/sccm/core/servers/manage/install-in-console-updates) for Configuration Manager, clients automatically update their client software so they can use those new features. With this scenario, you still update to the current branch receiving the new features and updates. Most devices update the Configuration Manager client software with each version update you install. However, on a subset of critical systems that you do not want to receive client software updates, you install the extended interoperability client. These clients don't install new client software until you explicitly deploy a new version of the client software to them.



## Supported versions
The following table lists the versions of the Configuration Manager client that are supported for this scenario:

| Version  | Availability date  | Support end date  |
|---------|---------|---------|
|1802<br/>5.00.8634     | May 1, 2018        | No earlier than May 1, 2020        |
|1606<br/>5.00.8412     | November 18, 2016        | May 1, 2019        |

> [!TIP]  
> The EIC is supported for at least two years from the date of release. For more information on release dates, see [Support for System Center Configuration Manager current branch versions](/sccm/core/servers/manage/current-branch-versions-supported)).  

Plan to update the extended interoperability client on devices that you manage with the current branch before support for the client expires. To do so, download a new version of the client from Microsoft, and then deploy that updated client software to your devices that use the current extended interoperability client.



## How to use the EIC

1. Obtain a supported version of the EIC from the `\SMSSETUP\Client` folder of the Configuration Manager update installation media. Ensure that you copy the entire contents of the folder.  

2. Manually install the EIC on those devices. For more information, see [Manually install the client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).  

    > [!Important]  
    > When upgrading version 1606 clients to version 1802, use the CCMSETUP option **/AlwaysExcludeUpgrade:True**. Otherwise the client may receive policy from the management point to automatically upgrade before the exclusion policy.

3. Add these devices to a collection, and exclude that collection from automatic client upgrades. For more information, see [Use automatic client upgrade](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

> [!TIP]  
> To find Configuration Manager media in the [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), go to the **Downloads and Keys** tab, search for `System Center Config`, and then select **System Center Config Mgr (current branch)**.



## Limitations of the extended interoperability client

- Updates for the extended interoperability client software are not available by using in-console updates. For more information on how to update EIC clients, see [How to use the EIC](#how-to-use-the-eic).  

- The EIC only supports the following features:  

   - Software updates  
   - Hardware and software inventory
   - Packages and programs



## Next steps

To ensure that clients are installed correctly on the devices you want, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients).
