---
title: How to close your account
titleSuffix: Configuration Manager
description: How to remove Desktop Analytics from your Azure account
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# How to close your account

If you set up Desktop Analytics in your environment, and then decide you need to remove it, use this process to close your account.

## Prerequisites

Only a **Global Administrator** can close or reactivate the account in the Azure portal.

## Process to offboard

1. Open the [Desktop Analytics portal](https://aka.ms/desktopanalytics) in Microsoft 365 Device Management as a user with the **Global Administrator** role.

1. In the **Global Settings** menu, select **Connected services**. In the enroll devices section, select the option to **Offboard**.

1. If you decide to continue, your account is closed.

> [!Important]
> Only continue with the rest of this article after 90 days, or if you won't reactivate.
>
> If you want to completely close your account without waiting for 90 days, first [Reset](account-reset.md) your account.

## Reactivate

For the next 90 days, any administrator from your organization who accesses the Desktop Analytics portal will see a notice that you opted to offboard.

A global administrator can reactivate the account within 90 days. To restore Desktop Analytics for your organization, select the option to **Take me back**.

## Delete the solution

> [!Warning]
> Only continue with the rest of this article after 90 days, or if you won't reactivate. If you delete and disconnect these other components, don't try to reactivate.

1. Sign in to the [Azure portal](https://portal.azure.com) as a user with the **Global administrator** role.

1. Search in **All resources** for the name of your Desktop Analytics workspace. This name is what you created when signing up for the service.

1. Delete `Microsoft365Analytics(YourWorkspaceName)` of type **Solution**.

The Desktop Analytics data ages out based on your data retention policy for the workspace. You can continue using any other solutions in same workspace.

> [!Important]  
> If you're using the Log Analytics workspace with other solutions, don't delete the workspace.

## Remove user and app access

1. Sign in to the [Azure portal](https://portal.azure.com) as a user with the **Global administrator** role. Go to **Azure Active Directory**.

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

### Delete collections for the pilot and production deployments

1. In the Configuration Manager console, select **Device Collections** in the **Assets and Compliance** workspace.

1. Delete any collections you're no longer using. By default, the collections are located under the **Deployment Plans** folder.  

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
- Mobile device management (MDM), such as [Microsoft Intune](/intune/device-restrictions-windows-10#reporting-and-telemetry)

For more information, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> When you apply these changes, devices immediately stop sending diagnostic data. It may take 24-48 hours for Microsoft to stop processing insights for your workspace. Microsoft deletes this data from its cloud services within 30 days or less.