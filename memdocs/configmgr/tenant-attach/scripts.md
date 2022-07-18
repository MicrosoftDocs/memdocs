---
title: Tenant attach - Run Scripts from the admin center
titleSuffix: Configuration Manager
description: Run scripts for Configuration Manager devices from the admin center.
ms.date: 07/11/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# <a name="bkmk_scripts"></a> Tenant attach: Run Scripts from the admin center
<!--CM6234688, IN7220536-->
*Applies to: Configuration Manager (current branch)*

Bring the power of the Configuration Manager on-premises Run Scripts feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device in real time. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment.

:::image type="content" source="./media/6234688-scripts.png" alt-text="Screenshot of script list in the admin center" lightbox="./media/6234688-scripts.png":::

## Prerequisites

Running Scripts from the admin center requires the following items:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites)
- A supported version of Configuration Manager installed.
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
- An [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned to the user <!--7980141-->
- To use scripts, you must be a member of the appropriate Configuration Manager security role. For more information, see [Security scopes for run scripts](../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).
- To run scripts, the account must have **Run Script** permissions for **Collections**.

## Run a script

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Scripts**.
   
   Scripts that were recently run that directly targeted the device will already be listed. The list includes scripts run from the admin center, SDK, or the Configuration Manager console. Scripts initiated from the on-premises console, against collections containing the device won't be shown, unless the scripts were also initiated specifically for the single device.

   :::image type="content" source="./media/6234688-run-script.png" alt-text="Running the script from the admin center" lightbox="./media/6234688-run-script.png":::

1. Choose **Run script**.
   
   Scripts that are available to the admin based on the scopes assigned in Configuration Manager will be listed.
1. Select **Run** to run the script.

1. You'll be notified your script has started. You don't have to wait for the script to finish before sending another to the device.
1. Select **Refresh** on the main page to update the list with latest script state, and last run time.

1. When the script completes, you can select the script to display the results in the **Output** pane. You can copy the text of the script output. Select **Re-run script** if you want the script to run again.

   :::image type="content" source="./media/6234688-script-output.png" alt-text="Script output in the admin center" lightbox="./media/6234688-script-output.png":::

## Next steps

[Install an application from the admin center](applications.md)

[Learn more about PowerShell script security](../apps/deploy-use/learn-script-security.md)