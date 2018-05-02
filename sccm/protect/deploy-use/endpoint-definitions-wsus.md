---
title: "Endpoint Protection malware definitions from WSUS"
titleSuffix: "Configuration Manager"
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: aczechowski
description: Learn how to configure Windows Server Updates Services to auto-approve definition updates.
manager: dougeby
ms.author: aaroncz
---

# Enable Endpoint Protection malware definitions to download from Windows Server Update Services (WSUS) for Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
 If you use WSUS to keep your antimalware definitions up to date, you can configure it to auto-approve definition updates. Although using Configuration Manager software updates is the recommended method to keep definitions up to date, you can also configure WSUS as a method to allow users to manually initiate definition updated. Use the following procedures to configure WSUS as a definition update source.

## To synchronize Endpoint Protection definition updates in Configuration Manager software updates

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.

3.  Select the site that contains your software update point. In the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**.

4.  On the **Classifications** tab of the **Software Update Point Component Properties** dialog box, select the **Definition Updates** check box.

5.  Specify the **Products** updated with WSUS:

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.

6.  Click **OK** to close the **Software Update Point Component Properties** dialog box.

 Use the following procedure to configure Endpoint Protection updates when your WSUS server is not integrated into your Configuration Manager environment.

## To synchronize Endpoint Protection definition updates in standalone WSUS

1.  In the WSUS administration console, expand **Computers**, click **Options**, and then click **Products and Classifications**.

2.  Specify the **Products** updated with WSUS:

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.

3.  On the **Classifications** tab of the **Products and Classifications** dialog box, select the **Definition Updates** and **Updates** check boxes.

## Approving Definition Updates
 Endpoint Protection definition updates must be approved and downloaded to the WSUS server before they are offered to clients that request the list of available updates. Clients connect to the WSUS server to check for applicable updates and then request the latest approved definition updates.

### To approve definitions and updates in WSUS

1.  In the WSUS administration console, click **Updates**, and then click **All Updates** or the classification of updates that you want to approve.

2.  In the list of updates, right-click the update or updates you want to approve for installation, and then click **Approve**.

3.  In the **Approve Updates** dialog box, select the computer group for which you want to approve the updates, and then click **Approved for Install**.

 In addition to manual approval, you can also set an automatic approval rule for definition updates and Endpoint Protection updates. This will configure WSUS to automatically approve Endpoint Protection definition updates downloaded by WSUS.

### To configure an automatic approval rule

1.  In the WSUS administration console, click **Options**, and then click **Automatic Approvals**.

2.  On the **Update Rules** tab, click **New Rule**.

3.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific classification** check box.

4.  Under **Step 2: Edit the properties**, click **any classification**.

5.  Clear all check boxes except **Definition Updates**, and then click **OK**.

6.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific product** check box.

7.  Under **Step 2: Edit the properties**, click **any product**.

8.  Clear all check boxes except **Forefront Endpoint Protection** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later, and then click **OK**.

9. Under **Step 3: Specify a name**, enter a name for the rule, and then click **OK**.

10. In the **Automatic Approvals** dialog box, select the check box for the newly created rule and then click **Run rule**.

> [!NOTE]
>  To maximize performance on your WSUS server and client computers, decline old definition updates. To accomplish this task, you can configure automatic approval for revisions and automatic declining of expired updates. For more information, see [Microsoft Knowledge Base article 938947](http://go.microsoft.com/fwlink/p/?LinkId=204078).

> [!div class="button"]
[Next step >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Back >](endpoint-configure-alerts.md)
