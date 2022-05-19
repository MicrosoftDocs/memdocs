---
title: Tenant attach - Create and deploy Antivirus policies from the admin center
titleSuffix: Configuration Manager
description: "Create and deploy Antivirus policies from the Microsoft Endpoint Manager console and for Configuration Manager collections."
ms.date: 04/08/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy Antivirus policies from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

Create Microsoft Defender antivirus policies in the Microsoft Endpoint Manager console and deploy them to Configuration Manager collections.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_av"></a> Assign Microsoft Defender Antivirus policy to a collection

1. In a browser, go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
1. Select **Endpoint security** then **Antivirus**.
1. Select **Create Policy**.
1. For the **Platform**, select **Windows 10, Windows 11, and Windows Server (ConfigMgr)**.
1. For the **Profile**, select **Microsoft Defender Antivirus** then **Create**.
1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about available policies, see [Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

## <a name="bkmk_security"></a> Assign Windows Security experience policy to a collection

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

1. In a browser, go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
1. Select **Endpoint security** then **Antivirus**.
1. Select **Create Policy**.
1. For the **Platform**, select **Windows 10, Windows 11, and Windows Server (ConfigMgr)**.
1. For the **Profile**, select **Windows Security experience (preview)** then **Create**.
1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about the available settings, see [Settings for Windows Security experience Antivirus policy for tenant attached devices](../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

## <a name="bkmk_exclusion"></a> Antivirus policy exclusions merge
<!--9089764 -->

*(Introduced in Configuration Manager 2103)*

Starting in Configuration Manager 2103, When a tenant attached device is targeted with two or more antivirus policies, the settings for antivirus exclusions will merge before being applied to the client. This change results in the client receiving the exclusions defined in each policy, allowing for more granular control of antivirus exclusions. For earlier versions of Configuration Manager, Antivirus exclusions from a single policy are applied. With this behavior, the last policy applied determines the effective exclusions. <!--9397015-->

To use this functionality, create an antivirus policy from the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/) that includes some [antivirus exclusions](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#microsoft-defender-antivirus-exclusions). Create a second antivirus policy including only antivirus exclusions that are different from the first policy. Apply both antivirus policies to the same collection. Antivirus exclusions from both policies are applied on clients in the targeted collection.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## Next steps

- [Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)
- [Settings for Windows Security experience Antivirus policy for tenant attached devices](../../intune/protect/antivirus-windows-security-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)
- [Create and deploy endpoint security Attack surface reduction policy to tenant attached devices](deploy-asr-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)