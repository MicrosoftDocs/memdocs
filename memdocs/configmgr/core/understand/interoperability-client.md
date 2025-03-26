---
title: Extended interoperability client
titleSuffix: Configuration Manager
description: Learn about using the extended interoperability client for long-term support of a static Configuration Manager client with a current branch site.
ms.date: 06/22/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Use the Configuration Manager client software for extended interoperability with future versions of a Current Branch site

*Applies to: Configuration Manager (current branch)*

Business requirements might not allow you to regularly update the Configuration Manager client on some devices. For example, you need to follow change management policies, or the device is mission-critical. Accommodate these needs by installing a new client for long-term use, called the extended interoperability client (EIC). Only use the EIC for specific devices that can't be frequently updated, like kiosk or point-of-sale devices. Continue to use [automatic client upgrade](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) for most of your clients.

## How it works

Typically, when you install a new [in-console update](../servers/manage/install-in-console-updates.md) for Configuration Manager, clients automatically update their client software so they can use those new features. With this scenario, you still update to the current branch receiving the new features and updates. Most devices update the Configuration Manager client software with each version update you install. However, on a subset of critical systems that you don't want to receive client software updates, you install the extended interoperability client. These clients don't install new client software until you explicitly deploy a new version of the client software to them.

## Supported versions

The following table lists the versions of the Configuration Manager client that are supported for this scenario:

| Version | Availability date | Support end date |
|---------|---------|---------|
| 2103<br/>5.00.9049 | April 5, 2021 | No earlier than April 2023 |
| 1902<br/>5.00.8790 | March 27, 2019 | March 27, 2022 |

> [!TIP]
> The EIC is supported for at least two years from the date of release. For more information on release dates, see [Support for Configuration Manager current branch versions](../servers/manage/current-branch-versions-supported.md).

Plan to update the extended interoperability client on devices that you manage with the current branch before support for the client expires. To do so, download a new version of the client from Microsoft, and then deploy that updated client software to your devices that use the current extended interoperability client.

## How to use the EIC

1. Add these devices to a collection, and exclude that collection from automatic client upgrades. For more information, see [How to exclude clients from upgrade](../clients/manage/upgrade/exclude-clients-windows.md).

1. Obtain a supported version of the EIC from the `\SMSSETUP\Client` folder of the Configuration Manager update installation media. Make sure that you copy the entire contents of the folder.

1. Manually install the EIC on those devices. For more information, see [Manually install the client](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## Limitations

- Updates for the extended interoperability client software aren't available by using in-console updates. For more information on how to update the EIC, see [How to upgrade an excluded client](../clients/manage/upgrade/exclude-clients-windows.md#how-to-upgrade-an-excluded-client).

- The EIC only supports the following features:

  - Software updates
  - Hardware and software inventory
  - Packages and programs

## Next steps

[How to exclude clients from upgrade](../clients/manage/upgrade/exclude-clients-windows.md)

To make sure that clients are installed correctly on the devices you want, see [How to monitor clients](../clients/manage/monitor-clients.md).
