---
title: Endpoint Protection malware definitions from WSUS
titleSuffix: Configuration Manager
ms.date: 02/10/2022
ms.service: configuration-manager
ms.subservice: protect
ms.topic: how-to
author: BalaDelli
ms.author: baladell
description: Learn how to configure Windows Server Updates Services to auto-approve definition updates.
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Enable Endpoint Protection malware definitions to download from WSUS for Configuration Manager

*Applies to: Configuration Manager (current branch)*

If you use WSUS to keep your antimalware definitions up to date, you can configure it to auto-approve definition updates. Although using Configuration Manager software updates is the recommended method to keep definitions up to date, you can also configure WSUS as a method to allow users to manually update definitions. Use the following procedures to configure WSUS as a definition update source.

## Synchronize definition updates for Configuration Manager

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select **Sites**.

1. Select the site that contains your software update point. In the **Settings** group of the ribbon, select **Configure Site Components**, and then select **Software Update Point**.

1. In the **Software Update Point Component Properties** window, switch to the **Classifications** tab. Select **Definition Updates**.

1. To specify the **Products** updated with WSUS, switch to the **Products** tab.

    - For Windows 10 and later: Under Microsoft > Windows, select **Microsoft Defender Antivirus**.

    - For Windows 8.1 and earlier: Under Microsoft > Forefront, select **System Center Endpoint Protection**.

1. Select **OK** to close the **Software Update Point Component Properties** window.

## Approve definition updates

Endpoint Protection definition updates must be approved and downloaded to the WSUS server before they're offered to clients that request the list of available updates. Clients connect to the WSUS server to check for applicable updates and then request the latest approved definition updates.

### Approve definitions and updates in WSUS

1. In the WSUS administration console, select **Updates**. Then select **All Updates** or the classification of updates that you want to approve.

1. In the list of updates, right-click the update or updates you want to approve for installation, and then select **Approve**.

1. In the **Approve Updates** window, select the computer group for which you want to approve the updates, and then select **Approved for Install**.

### Configure an automatic approval rule

You can also set an automatic approval rule for definition updates and Endpoint Protection updates. This action configures WSUS to automatically approve Endpoint Protection definition updates downloaded by WSUS.

1. In the WSUS administration console, select **Options**, and then select **Automatic Approvals**.

1. On the **Update Rules** tab, select **New Rule**.

1. In the **Add Rule** window, under **Step 1: Select properties**, select the option: **When an update is in a specific classification**.

    1. Under **Step 2: Edit the properties**, select **any classification**.

    1. Clear all options except **Definition Updates**, and then select **OK**.

1. In the **Add Rule** window, under **Step 1: Select properties**, select the option: **When an update is in a specific product**.

    1. Under **Step 2: Edit the properties**, select **any product**.

    1. Clear all options except **System Center Endpoint Protection** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later. Then select **OK**.

1. Under **Step 3: Specify a name**, enter a name for the rule, and then select **OK**.

1. In the **Automatic Approvals** dialog box, select the newly created rule, and then select **Run rule**.

> [!NOTE]
> To maximize performance on your WSUS server and client computers, decline old definition updates. To accomplish this task, you can configure automatic approval for revisions and automatic declining of expired updates. For more information, see [Microsoft Support article 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Create and deploy antimalware policies](endpoint-antimalware-policies.md)
