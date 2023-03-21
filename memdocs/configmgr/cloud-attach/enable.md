---
title: Enable cloud attach
titleSuffix: Configuration Manager
description: Enable cloud attach for Configuration Manager
ms.date: 08/15/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: high
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Enable cloud attach for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Starting in version 2111, it's simpler to cloud attach your Configuration Manager environment. You can choose a streamlined set of recommended defaults, or customize your cloud attach features. If you're not running version 2111 yet, use the [Tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), [Endpoint analytics](../../analytics/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), and [Co-management](../comanage/tutorial-co-manage-clients.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) articles to enable cloud attach features.

:::image type="content" source="./media/10964629-cloud-attach-wizard.png" alt-text="Screenshot of the cloud attach configuration wizard":::

## <a name="bkmk_attach"></a> Simplified cloud attach configuration
<!--10964629-->
(*Applies to version 2111 or later*)

By using the recommended default settings, your eligible devices will be cloud attached. You'll enable capabilities like rich analytics, cloud console, and real-time device querying. The default settings include the following features:

- Enables automatic enrollment of all eligible devices into Intune
    - Enrolls your clients into [co-management](../comanage/tutorial-co-manage-clients.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), with all [workloads](../comanage/workloads.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) pointed to Configuration Manager
    - Devices are eligible if they meet the [prerequisites for co-management](../comanage/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json#prerequisites). These devices are listed in the built-in **Co-management Eligible Devices** collection. <!--12377291-->
    - This option is the only one currently available for China21Vianet (Azure China Cloud).
- Enables [Endpoint analytics](../../analytics/scores.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Enables automatic upload of all your devices to Microsoft Intune admin center ([tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json))
- Enables Uploading of Microsoft Defender for Endpoint data for [reporting](../tenant-attach/deploy-antivirus-policy.md#bkmk_mdereports) on devices uploaded to Microsoft Intune admin center

> [!IMPORTANT]
> When you attach your Configuration Manager site with a Microsoft Intune tenant, the site sends more data to Microsoft. [Tenant attach data collection](../tenant-attach/data-collection.md) article summarizes the data that is sent.

> [!Note]
> Ensure that prerequisites for each of the cloud attach features are met. For more information about prerequisites, see, [prerequisites for tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), [prerequisites for Endpoint analytics](../../analytics/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json), and [prerequisites for co-management](../comanage/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json#prerequisites).
## Cloud attach using the default settings

Use the following steps to cloud attach your environment with the default settings:
  
1. From the Configuration Manager console, go to **Administration** > **Cloud services** > **Cloud Attach**.
1. Select **Configure Cloud Attach** from the ribbon to open the wizard.
1. Select your **Azure environment** from the following list:
   - Azure Public Cloud
   - Azure US Government Cloud
   - Azure China Cloud
      - Endpoint analytics and device upload to Microsoft Intune admin center can't be enabled for Azure China Cloud

1. Select **Sign In**. Sign into your account when prompted.
1. Ensure that **Use default settings (recommended)** is selected, then choose **Next** and **Yes** when the app registration notice appears.  
1. Review the summary and select **Next** to cloud attach your environment and complete the wizard.

## Cloud attach using custom settings
<!--10964629-->
(*Applies to version 2111 or later*)

Use the following steps to cloud attach your environment with custom settings:

1. From the Configuration Manager console, go to **Administration** > **Cloud services** > **Cloud Attach**.
1. Select **Configure Cloud Attach** from the ribbon to open the wizard.
1. Select your **Azure environment** from the following list:
   - Azure Public Cloud
   - Azure US Government Cloud
   - Azure China Cloud
      - Endpoint analytics and device upload to Microsoft Intune admin center can't be enabled for Azure China Cloud
1. Select **Sign In**. Sign into your account when prompted.
1. Choose the **Customize settings** option to enable cloud features individually.
1. By default, Configuration Manager uses your credentials to register an app in your Azure AD tenant. This app to authorize synchronization of data between your on-premises site and Intune. To use an app that you already created, select  **Optionally import a separate web app to synchronize Configuration Manager client data to Microsoft Endpoint Manager admin center**. For more information, see [Import a previously created Azure AD application](#bkmk_aad_app).

1. Choose **Next** to continue. You may also be prompted to confirm Azure AD application registration. Select **Yes** to confirm the app registration.
1. The **Devices** section of the **Configure Upload** page, enables [tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json). Tenant attach uploads your Configuration Manager devices to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) cloud-based console. You can take certain actions on uploaded devices such as run queries, run scripts, install apps, or display an event timeline for the device.

   **Select which devices to upload to Microsoft Endpoint Manager** has the following two options:
   - **All devices managed my Microsoft Endpoint Configuration Manager (recommended)**: Upload all devices
   - **Specific Collection**: Upload a specific collection, including any subcollections.
1. The **Endpoint Analytics** section of the **Configure Upload** page, enables [Endpoint analytics](../../analytics/scores.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) for devices uploaded to Microsoft Endpoint Manager. Endpoint analytics reports focus on the quality of the experience you're delivering to your users and helps you identify issues to proactively make improvements.

   Ensure the **Enable Endpoint Analytics for devices uploaded to Microsoft Endpoint Manager** option is selected to enable Endpoint Analytics.

1. In the **Role-based access control** section of the **Configure Upload** page, determine if you need to clear the checkbox for the **Enforce Configuration Manager RBAC for cloud console requests that interact with Configuration Manager** option. (*Introduced in version 2207*)
   - This option is used for setting Intune as the role-based access control authority for tenant-attached clients. For more information about configuring this option, see [Intune role-based access control for tenant-attached clients](use-intune-rbac.md).

     > [!IMPORTANT]
     > When this checkbox is cleared, [settings in Intune need to be configured](use-intune-rbac.md) too.

1. Check the option to **Enable Uploading Microsoft Defender for Endpoint data for reporting on devices uploaded to Microsoft Intune admin center** if you want to use [Endpoint Security reports in Intune admin center](deploy-antivirus-policy.md#bkmk_mdereports)

1. Select **Next** to get to the **Enablement** page for [co-management](../comanage/tutorial-co-manage-clients.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json). Co-management simplifies management by enrolling devices into Intune and allowing you to lift selected [workloads](../comanage/workloads.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) to the cloud. For instance, you can choose to enable workloads for [Conditional Access](../comanage/quickstart-conditional-access.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) so only trusted users can access organizational resources on trusted devices using trusted apps.

   Choose your co-management setting from the following options under **Automatic enrollment in Intune**:
      - **All**: Enrolls all eligible devices into Intune
        - Devices are eligible if they meet the [prerequisites for co-management](../comanage/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json#prerequisites). These devices are listed in the built-in **Co-management Eligible Devices** collection. <!--12377291-->
      - **Pilot**: Enrolls all eligible devices in a specified collection into Intune
         - Select **Browse** to choose the collection for **Intune auto enrollment**
      - **None**: Don't enable co-management or enroll any clients
      
    > [!NOTE]
    > Enrolling devices, doesn't move any workloads to Intune. [Specify workloads to move](../comanage/how-to-switch-workloads.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) by editing the co-management settings in the **Cloud Attach** node when you're ready.
1. When you're finished with your selections, select **Next** to display the **Summary** page. Select **Next** after reviewing the summary to cloud attach your Configuration Manager environment.

[!INCLUDE [Import a previously created Azure AD application](../tenant-attach/includes/import-azure-app.md)]

## Next steps

Learn more about the following cloud attach features:

- [Co-management](../comanage/tutorial-co-manage-clients.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Endpoint analytics](../../analytics/scores.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Tenant attach](../tenant-attach/device-sync-actions.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
