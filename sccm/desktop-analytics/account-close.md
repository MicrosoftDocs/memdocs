---
title: How to close your account
titleSuffix: Configuration Manager
description: How to remove Desktop Analytics from your Azure account
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
---

# How to close your account

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

If you set up Desktop Analytics in your environment, and then decide you need to remove it, use this process to close your account.

## Contact support

The first step is to contact Microsoft Support. Open a support case to close your Desktop Analytics account. Don't continue with additional steps until you receive confirmation that Microsoft closed your account.

## Delete the solution

1. Sign in to the [Azure portal](https://portal.azure.com) as a user with the **Company Admin** role.

1. Search in **All resources** for the name of your Desktop Analytics workspace. This name is what you created when signing up for the service.

1. Delete `Microsoft365Analytics(YourWorkspaceName)` of type **Solution**.

The Desktop Analytics data ages out based on your data retention policy for the workspace. You can continue using any other solutions in same workspace.

> [!Important]  
> If you're using the Log Analytics workspace with other solutions like Windows Analytics, don't delete the workspace.

## Remove user and app access

1. Sign in to the [Azure portal](https://portal.azure.com) as a user with the **Company Admin** role. Go to **Azure Active Directory**.

1. In **Roles and administrators**, search for the **Desktop Analytics administrator** role. Remove its members.

1. In **Groups**, remove the members of the following groups:

    - **M365 Analytics Client Admins (Log Analytics Owners)**
    - **M365 Analytics Client Admins (Log Analytics Contributors)**

1. In **Enterprise applications**, delete or revoke access permissions for the following apps:

    - `MaLogAnalyticsReader`

    - The ConfigMgr app. To find the name of this app, go to the Configuration Manager console. In the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Open the properties of the **Desktop Analytics** service, and switch to the **Applications** tab. The **Web app** is this Azure app.

        > [!Important]  
        > Before you make changes to this app in Azure AD, make sure that you're not reusing it with another service in Configuration Manager.

## Disconnect Configuration Manager

1. Open the Configuration Manager console as a user with the **Full administrator** role.

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.

1. Delete the Desktop Analytics service.

## Reconfigure clients

### Unenroll devices

On enrolled devices, remove the CommercialID value from the following Windows Registry keys:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### Windows diagnostic data configuration

If you don't want your devices to continue sending diagnostic data:

- Windows 10: set the diagnostic data level to **Security**
- Windows 7 SP1 or 8.1: disable the **Commercial Data Opt-in Key**

Set these values using one of the following methods:

- Group policy, in **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**
- Mobile device management (MDM), such as [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> When you apply these changes, devices immediately stop sending diagnostic data. It may take 24-48 hours for Microsoft to stop processing insights for your workspace. Microsoft deletes this data from its cloud services within 30 days or less.
