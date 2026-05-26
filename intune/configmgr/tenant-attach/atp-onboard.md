---
title: Tenant attach - Onboard Configuration Manager clients to Microsoft Defender for Endpoint from the Microsoft Intune admin center
description: Deploy Microsoft Defender for Endpoint Detection and Response (EDR) onboarding policies to Configuration Manager managed clients from the admin center.
ms.date: 05/13/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.subservice: core-infra
ms.collection: tier3
---

# Tenant attach: Onboard Microsoft Configuration Manager clients to Microsoft Defender for Endpoint from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

The Microsoft Intune family of products is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Intune admin center**. You can deploy Defender for Endpoint onboarding policies to Configuration Manager managed clients. These clients don't require Microsoft Entra ID or MDM enrollment, and the policy is targeted at Configuration Manager collections rather than Microsoft Entra groups.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Prerequisites for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]
- [Microsoft Intune and Microsoft Defender for Endpoint integration enabled](../../device-security/microsoft-defender/configure-integration.md#connect-defender-for-endpoint-to-intune)
- Client which meets the [minimum requirements for Microsoft Defender for Endpoint](/defender-endpoint/minimum-requirements#licensing-requirements) and is onboarded.<!--Adding MDE License Requirement & MAX 6198973-->

## Create Defender for Endpoint policies

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

1. Select the following platform and profile for your policy:

   - Platform: **Windows 10, Windows 11, and Windows Server (ConfigMgr)**
   - Profile: **Endpoint detection and response (ConfigMgr)**

1. Select **Create**.

1. On the **Basics** page, enter a name and description for the profile, and then choose **Next**.

1. On the **Configuration settings** page, configure the settings you want to manage with this profile. The onboarding package is automatically included and isn't something you can configure.

   When you're done configuring settings, select **Next**.

1. On the **Assignments** page, select the collections that receive this policy. Select collections from Configuration Manager that you synced to Intune admin center and enabled for Defender for Endpoint policy.

   You can choose not to assign collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

1. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

[!INCLUDE [Device status for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-device-status.md)]

## Next steps

- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)
