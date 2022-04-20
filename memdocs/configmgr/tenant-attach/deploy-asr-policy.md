---
title: Tenant attach - Create and deploy Attack surface reduction policies from the admin center (preview)
titleSuffix: Configuration Manager
description: "Create and deploy Attack surface reduction policies from the Microsoft Endpoint Manager console and for Configuration Manager collections."
ms.date: 09/29/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew 
ms.author: brenduns
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy Attack surface reduction policies from the admin center (preview)
<!--7323386-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

 Create Attack surface reduction policies in the Microsoft Endpoint Manager console and deploy them to Configuration Manager collections.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_asr"></a> Assign Attack surface reduction policy to a collection

1. In a browser, go to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
1. Select **Endpoint security** > **Attack surface reduction** then **Create Policy**.
1. Create a profile with the following settings:

   - **Platform**: Windows 10 and later (ConfigMgr)
   - **Profile**: Choose one of the following profiles:
     - Attack Surface Reduction Rules (ConfigMgr) (preview)
     - Exploit Protection (ConfigMgr) (preview)
     - Web Protection (ConfigMgr) (preview)

1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about available settings for both profiles, see [Attack surface reduction policy settings for tenant attached devices](../../intune/protect/endpoint-security-asr-profile-settings.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#attack-surface-reduction-configmgr).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## Next steps

- [Attack surface reduction policy settings for tenant attached devices](../../intune/protect/endpoint-security-asr-profile-settings.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json#attack-surface-reduction-configmgr).
- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)