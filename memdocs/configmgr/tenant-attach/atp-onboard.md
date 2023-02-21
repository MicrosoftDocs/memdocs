---
title: Tenant attach - Onboard Configuration Manager clients to Microsoft Defender for Endpoint from the Microsoft Intune admin center
titleSuffix: Configuration Manager
description: Deploy Microsoft Defender for Endpoint Detection and Response (EDR) onboarding policies to Configuration Manager managed clients from the admin center.
ms.date: 03/21/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
author: Banreet
ms.author: banreetkaur
ms.localizationpriority: high
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_atp"></a> Tenant attach: Onboard Configuration Manager clients to Microsoft Defender for Endpoint from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

The Microsoft Intune family of products is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Intune admin center**. You can deploy Microsoft Defender for Endpoint onboarding policies to Configuration Manager managed clients. These clients don't require Azure AD or MDM enrollment, and the policy is targeted at ConfigMgr collections rather than Azure AD Groups.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Prerequisites for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]
- [Microsoft Intune and Microsoft Defender for Endpoint integration enabled](../../intune/protect/advanced-threat-protection-configure.md#enable-microsoft-defender-for-endpoint-in-intune)
- Client which meets the minimum requirements for, and is onboarded to [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).<!--Adding MDE License Requirement & MAX 6198973-->

## <a name="bkmk_onboard"></a> Create Microsoft Defender for Endpoint policies

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

1. Select the following platform and profile for your policy:

   - Platform: **Windows 10, Windows 11, and Windows Server (ConfigMgr)**
   - Profile: **Endpoint detection and response (ConfigMgr)**

1. Select **Create**.

1. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

1. On the **Configuration settings** page, configure the settings you want to manage with this profile. The onboarding package is automatically included and isn’t something you can configure.

   When your done configuring settings, select **Next**.

1. On the **Assignments** page, select the collections that will receive this policy. Select collections from Configuration Manager that you’ve synced to Microsoft Intune admin center and enabled for Microsoft Defender for Endpoint policy.

   You can choose not to assign collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

1. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## Next steps

- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)
