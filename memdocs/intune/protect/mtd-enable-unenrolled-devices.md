---
# required metadata

title: Enable the Mobile Threat Defense connector for unenrolled devices
titleSuffix: Microsoft Intune
description: Enable the Mobile Threat Defense connector in Microsoft Intune for unenrolled devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/17/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Enable the Mobile Threat Defense connector in Intune for unenrolled devices

During Mobile Threat Defense (MTD) setup, you've configured a policy for classifying threats in your Mobile Threat Defense partner console and you've created the app protection policy in Intune. If you've already configured the Intune connector in the MTD partner console, you can now enable the MTD connection for MTD partner applications.

> [!NOTE]
> This article applies to all Mobile Threat Defense partners that support app protection policies:
>
> - Better Mobile (Android,iOS/iPadOS)
> - Check Point Harmony Mobile Protect (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)
> - MVISION Mobile (Android,iOS/iPadOS)
> - Symantec Endpoint Security (Android, iOS/iPadOS)
> - Wandera (Android,iOS/iPadOS)
> - Zimperium (Android,iOS/iPadOS)

## Classic conditional access policies for MTD apps

When you integrate a new application to Intune Mobile Threat Defense and enable the connection to Intune, Intune creates a classic conditional access policy in Azure Active Directory. Each MTD app you integrate, including [Microsoft Defender for Endpoint](advanced-threat-protection.md) or any of our other [MTD partners](mobile-threat-defense.md#mobile-threat-defense-partners), creates a new classic conditional access policy. These policies can be ignored, but shouldn't be edited, deleted, or disabled.

If the classic policy is deleted, you'll need to delete the connection to Intune that was responsible for its creation, and then set it up again. This process recreates the classic policy. It's not supported to migrate classic policies for MTD apps to the new policy type for conditional access.

Classic conditional access policies for MTD apps:

- Are used by Intune MTD to require that devices are registered in Azure AD so that they have a device ID before communicating to MTD partners. The ID is required so that devices and can successfully report their status to Intune.

- Have no effect on any other Cloud apps or Resources.

- Are distinct from conditional access policies you might create to help manage MTD.

- By default, don't interact with other conditional access policies you use for evaluation.

To view classic conditional access policies, in [Azure](https://portal.azure.com/#home), go to **Azure Active Directory** > **Conditional Access** > **Classic policies**.

## To enable the MTD connector

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Mobile Threat Defense**. To set up an integration with a 3rd party Mobile Threat Defense vendor, you must be a Global administrator.

3. On the **Mobile Threat Defense** pane, choose **Add**.

4. Choose your MTD solution as the **Mobile Threat Defense connector to setup** from the drop-down list.

    <!-- ![MTD setup in Intune](PLACEHOLDER, need a new screenshot of this page) -->

5. Enable the toggle options according to your organization's requirements. Toggle options visible will vary depending on the MTD partner.

## Mobile Threat Defense toggle options

You can decide which MTD toggle options you need to enable according to your organization's requirements. Here are more details:

**App Protection Policy Settings**

- **Connect Android devices of version 4.4 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule will evaluate devices including data from this connector.

- **Connect iOS devices version 11 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule will evaluate devices including data from this connector.

**Common Shared Settings**

- **Number of days until partner is unresponsive**: Number of days of inactivity before Intune considers the partner to be unresponsive because the connection is lost. Intune ignores compliance state for unresponsive MTD partners.

> [!TIP]
> You can see the **Connection status** and the **Last synchronized** time between Intune and the MTD partner from the Mobile Threat Defense pane.

## Next Steps

- [Create Mobile Threat Defense (MTD) app protection policy with Intune](mtd-app-protection-policy.md).
