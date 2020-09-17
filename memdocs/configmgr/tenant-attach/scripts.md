---
title: Tenant attach - Run scripts (preview) from the admin center
titleSuffix: Configuration Manager
description: "Run scripts for Configuration Manager devices from the admin center."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 6b6c0a9b-01c6-4e3f-9ae4-45c780b46f8b
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_scripts"></a> Tenant attach: Run scripts (preview) from the admin center
<!--CM6234688, IN7220536-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Bring the power of the Configuration Manager on-premises Run Scripts feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment.

:::image type="content" source="./media/6234688-scripts.png" alt-text="Screenshot of script list in the admin center" lightbox="./media/6234688-scripts.png":::


## Prerequisites

Run scripts from the admin center requires the following items:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites)
- A minimum of Configuration Manager version 2006 with [KB4580678 - Tenant attach rollup for Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4580678) installed.
   - All sites in the hierarchy must meet the minimum Configuration Manager version requirement.
- Configuration Manager clients must be running the latest version client.
- To run PowerShell scripts, the client must be running PowerShell version 3.0 or later.
   - If a script you run contains functionality from a later version of PowerShell, the client on which you run the script must be running that later version of PowerShell.
- At least one script that is already created and approved in Configuration Manager.
   - Scripts that have parameters aren't supported at this time and won't be visible in the Microsoft Endpoint Manager admin center.
   - Only scripts that are already created and approved appear in the admin center. For more information on approving scripts, see [Approve or deny a script](../apps/deploy-use/create-deploy-scripts.md#run-script-authors-and-approvers).

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read Resource** permission for the device's **Collection** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.
- To use scripts, you must be a member of the appropriate Configuration Manager security role. For more information, see [Security scopes for run scripts](../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).
- To run scripts, the account must have **Run Script** permissions for **Collections**.

## Run a script

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Scripts** and search for your script by script name. If the script has already been run on the device, it will be listed 
1. Click **Run script** from the page that appears on the right.
   - You'll be notified your script has started. The **Run script** button will be disabled until it's complete.
   - The **State** column is only valid while you're on the page. The state is reset to `Ready` if you navigate to another page.
1. When the script completes, the results will show in the **Output** pane. You can copy the text of the script output.

:::image type="content" source="./media/6234688-script-output.png" alt-text="Script output in the admin center" lightbox="./media/6234688-script-output.png":::

## Next steps

[Install an application from the admin center](applications.md)