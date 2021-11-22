---
title: Enable cloud attach
titleSuffix: Configuration Manager
description: Enable cloud attach for Configuration Manager
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
---

# Enable cloud attach for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Starting in version 2111, it's simpler to cloud attach your Configuration Manager environment. You can choose to use a set of streamlined recommended defaults or customize your cloud attach features.

## <a name="bkmk_attach"></a> Simplified cloud attach configuration
<!--10964629-->
(*Applies to version 2111 or later*)

We've simplified the process to cloud attach your Configuration Manager environment. You can now choose to use a streamlined set of recommended defaults when cloud attaching your environment. By using the recommended default settings, your eligible devices will be cloud attached and you'll enable capabilities like rich analytics, cloud console, and real-time device querying. The default settings include the following features:

- Enables automatic enrollment of all eligible devices into Intune
    - Enrolls your clients into [co-management](../comanage/tutorial-co-manage-clients.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), with all [workloads](../comanage/workloads.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) pointed to Configuration Manager
- Enables [Endpoint analytics](../../analytics/scores.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Enables automatic upload of all your devices to Microsoft Endpoint Manager admin center ([tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json))

:::image type="content" source="./media/10964629-cloud-attach-wizard.png" alt-text="Screenshot of the cloud attach configuration wizard":::

## Cloud attach using the default settings

Use the following steps to cloud attach your environment with the default settings:
  
1. From the Configuration Manager console, go to **Administration** > **Cloud services** > **Cloud Attach**.
1. Select **Configure Cloud Attach** from the ribbon to open the wizard.
1. Select your **Azure environment** from the following list:
   - Azure Public Cloud
   - Azure US Government Cloud
   - Azure China Cloud

1. Select **Sign In**. Sign into your account when prompted.
1. Ensure that **Use default settings (recommended)** is selected, then choose **Next** and **Yes** when the app registration notice appears.  
1. Review the summary and select **Next** to cloud attach your environment and complete the wizard.


## Cloud attach using custom settings

