---
title: Tenant attach - Create and deploy Antivirus policies from the admin center
titleSuffix: Configuration Manager
description: Create and deploy Antivirus policies from the Microsoft Intune admin center and for Configuration Manager collections.
ms.date: 03/28/2023
ms.topic: install-set-up-deploy
ms.subservice: core-infra
ms.service: configuration-manager
manager: apoorvseth
author: gowdhamankarthikeyan
ms.author: gokarthi
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy Antivirus policies from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

Create Microsoft Defender antivirus policies in the Microsoft Intune admin center and deploy them to Configuration Manager collections.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_av"></a> Assign Microsoft Defender Antivirus policy to a collection

1. In a browser, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Endpoint security** then **Antivirus**.
1. Select **Create Policy**.
1. For the **Platform**, select **Windows 10, Windows 11, and Windows Server (ConfigMgr)**.
1. For the **Profile**, select **Microsoft Defender Antivirus** then **Create**.
1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about available policies, see [Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

## <a name="bkmk_security"></a> Assign Windows Security experience policy to a collection

1. In a browser, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Endpoint security** then **Antivirus**.
1. Select **Create Policy**.
1. For the **Platform**, select **Windows 10, Windows 11, and Windows Server (ConfigMgr)**.
1. For the **Profile**, select **Windows Security experience** then **Create**.
1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about the available settings, see [Settings for Windows Security experience Antivirus policy for tenant attached devices](../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

## <a name="bkmk_exclusion"></a> Antivirus policy exclusions merge
<!--9089764 -->

*(Introduced in Configuration Manager 2103)*

Starting in Configuration Manager 2103, When a tenant attached device is targeted with two or more antivirus policies, the settings for antivirus exclusions will merge before being applied to the client. This change results in the client receiving the exclusions defined in each policy, allowing for more granular control of antivirus exclusions. For earlier versions of Configuration Manager, Antivirus exclusions from a single policy are applied. With this behavior, the last policy applied determines the effective exclusions. <!--9397015-->

To use this functionality, create an antivirus policy from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) that includes some [antivirus exclusions](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#microsoft-defender-antivirus-exclusions). Create a second antivirus policy including only antivirus exclusions that are different from the first policy. Apply both antivirus policies to the same collection. Antivirus exclusions from both policies are applied on clients in the targeted collection.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## <a name="bkmk_mdereports"></a>Endpoint Security reports in Microsoft Intune admin center

Starting in Configuration Manager 2303 release, you can now see Tenant Attached devices data in Endpoint Security reports available in Microsoft Intune admin center.

If you are enabling cloud attach for first time, you can enable this feature in the [onboarding wizard](../../configmgr/cloud-attach/enable.md)

If you have enabled cloud attach currently, you need to use the cloud attach properties to enable data upload for Microsoft Defender for Endpoints reporting using the instructions below:

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Cloud Attach**.
   - For version 2103 and earlier, select the **Co-management** node.
1. In the ribbon, select **Properties** for your co-management production policy.
1. In the **Configure upload** tab, select **Upload to Microsoft Endpoint Manager admin center**. Select **Apply**.
   - The default setting for device upload is **All my devices managed by Microsoft Endpoint Configuration Manager**. If needed, you can limit upload to a single device collection.
   - When a single collection is selected, its child collections are also uploaded.
1. Optionally, you can enable [Endpoint Analytics and Role-based Access Control](../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit)
1. In the **Configure upload** tab, select **Enable Uploading Microsoft Defender for Endpoint data for reporting on devices uploaded to Microsoft Intune admin center**. Select **Apply**.
:::image type="content" source="media/9220597-data-upload-for-mde-reports.png" alt-text="Screenshot of Cloud Attach properties tab showing option to upload Microsoft Defender for Endpoint data to Intune admin center." lightbox="media/9220597-data-upload-for-mde-reports.png":::

### Operational reports in Microsoft Intune admin center

1. In the Intune admin console, go to **Endpoint Security** > **Antivirus**
1. Click on **Unhealthy endpoints** report where you can view the operational report for the thread agent status on devices and users to outline which are in a state that requires your attention.
    - Each record will tell you if malware protection, real-time protection and network protection are enabled or disabled.
    - You can view the state of the device and additional information found in the extra columns to help identify next steps for troubleshooting.
    - You can filter the devices based on management agent using the Managed By column and you can also export the report in csv format for further analysis.
:::image type="content" source="media/9220597-ops-unhealthy-endpoints-report.png" alt-text="Screenshot of unhealthy endpoints operational report in Intune admin center." lightbox="media/9220597-ops-unhealthy-endpoints-report.png":::
1. On the **Active malware** report, you can view the operational report to see the list of devices and users with detected malware with details of the malware category. This will show the malware, state of the device and counts of malware found on the device.
:::image type="content" source="media/9220597-ops-active-malware-report.png" alt-text="Screenshot of active malware operational report in Intune admin center." lightbox="media/9220597-ops-active-malware-report.png":::

### Organizational reports in Microsoft Intune admin center

1. In the Intune admin console, go to **Reports**, **Endpoint Security** > **Microsoft Defender Antivirus**
1. Under the **Summary** section, you will see summary aggregates of Antivirus Agent Status
:::image type="content" source="media/9220597-org-summary-report.png" alt-text="Screenshot of Antivirus agent status Summary organizational report in Intune admin center." lightbox="media/9220597-org-summary-report.png":::
1. Click on **Reports** to access **Antivirus agent status** and **Detected malware** organizational reports.
1. The **Antivirus agent status** report shows the list of devices, users, and antivirus agent status information.
:::image type="content" source="media/9220597-org-antivirus-agent-status-report.png" alt-text="Screenshot of Antivirus agent status organizational report in Intune admin center." lightbox="media/9220597-org-antivirus-agent-status-report.png":::
1. The **Detected malware** report shows the list of devices and users with detected malware with details of the malware category.
:::image type="content" source="media/9220597-org-detected-malware-report.png" alt-text="Screenshot of detected malware organizational report in Intune admin center." lightbox="media/9220597-org-detected-malware-report.png":::

Both the reports can be filtered based on **Managed by** column and the data within these reports will remain in your console up to three days before requiring you to generate again.

## Next steps

- [Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)
- [Settings for Windows Security experience Antivirus policy for tenant attached devices](../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)
- [Create and deploy endpoint security Attack surface reduction policy to tenant attached devices](deploy-asr-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)