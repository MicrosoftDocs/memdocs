---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Integrate Upgrade Readiness with Configuration Manager to access Windows upgrade compatibility data and target devices for upgrade or remediation.
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Integrate Upgrade Readiness with Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> The Windows Analytics service is retired as of January 31, 2020. For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics is the evolution of Windows Analytics. For more information, see [What is Desktop Analytics](../../../desktop-analytics/overview.md).

If your Configuration Manager site had a connection to Upgrade Readiness, you need to remove it and reconfigure clients.

## <a name="bkmk_remove"></a> Remove Upgrade Readiness connection

1. Open the Configuration Manager console as a user with the **Full administrator** role.

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.

1. Delete the Windows Analytics service.

## Reconfigure clients

### Unenroll devices

First, review the site's default or any custom client device settings in the **Windows Analytics** group. For example, disable the following setting: **Manage Windows telemetry settings with Configuration Manager**.

> [!IMPORTANT]
> If you plan to use Desktop Analytics, it configures Windows diagnostic data settings on clients. Use the Azure services connection wizard to configure these settings for use with Desktop Analytics. For more information, see [How to connect Configuration Manager with Desktop Analytics](../../../desktop-analytics/connect-configmgr.md).

On enrolled devices, remove the CommercialID value from the following Windows Registry keys:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### Windows diagnostic data configuration

If you don't want your devices to continue sending diagnostic data:

- Windows 10: set the diagnostic data level to **Security**
- Windows 7 SP1 or 8.1: disable the **Commercial Data Opt-in Key**

Set these values using one of the following methods:

- Group policy, in **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**
- Mobile device management (MDM), such as [Microsoft Intune](/intune/device-restrictions-windows-10#reporting-and-telemetry)

For more information, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> When you apply these changes, devices immediately stop sending diagnostic data. It may take 24-48 hours for Microsoft to stop processing insights for your workspace. Microsoft deletes this data from its cloud services within 30 days or less.
