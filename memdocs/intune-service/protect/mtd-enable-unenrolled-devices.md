---
# required metadata

title: Enable the Mobile Threat Defense connector for unenrolled devices
titleSuffix: Microsoft Intune
description: Enable the Mobile Threat Defense connector in Microsoft Intune for unenrolled devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/20/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Enable the Mobile Threat Defense connector in Intune for unenrolled devices

During Mobile Threat Defense (MTD) setup, you've configured a policy for classifying threats in your Mobile Threat Defense partner console and you've created the app protection policy in Intune. If you've already configured the Intune connector in the MTD partner console, you can now enable the MTD connection for MTD partner applications.

[!INCLUDE [mtd-mam-note](../../intune/protect/includes/mtd-mam-note.md)]

## Classic Conditional Access policies for Mobile Threat Defense (MTD) apps

When you integrate a new Mobile Threat Defense application with Intune and enable the connection to Intune, Intune creates a classic Conditional Access policy in Microsoft Entra ID. Each third-party MTD partner you integrate with creates a new classic Conditional Access policy. These policies can be ignored, but shouldn't be edited, deleted, or disabled. 

> [!NOTE]
>
> As of the August 2023 Intune service release (2308), classic Conditional Access (CA) policies are no longer created for the **Microsoft Defender for Endpoint** connector. If your tenant has a classic CA policy that was previously created for integration with Microsoft Defender for Endpoint, it can be deleted. Classic CA policies continue to be needed for 3rd party MTD partners.

If the classic policy is deleted, delete the connection to Intune that was responsible for its creation and then set it up again. This process recreates the classic policy. It isn't supported to migrate classic policies for MTD apps to the new policy type for Conditional Access.

Classic Conditional Access policies for MTD apps:


- Are used by Intune MTD to require that devices are registered in Microsoft Entra ID, and that they have a device ID before they communicate with the MTD partner. The ID is required so that devices and can successfully report their status to Intune.
- Have no effect on any other Cloud apps or Resources.
- Are distinct from Conditional Access policies you might create to help manage MTD.
- By default, don't interact with other Condition

To view classic Conditional Access policies, in [Azure](https://portal.azure.com/#home), go to **Microsoft Entra ID** > **Conditional Access** > **Classic policies**.

## To enable the Mobile Threat Defense connector

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Mobile Threat Defense**. To set up an integration with a third-party Mobile Threat Defense vendor, your account must be assigned the *Endpoint Security Manager* built-in admin role for Intune, or be assigned a custom role that includes the *Read* and *Modify* rights for the Intune *Mobile Threat Defense* permission.

3. On the **Mobile Threat Defense** pane, select **Add**.

4. For **Mobile Threat Defense connector to setup**, select your MTD partner solution from the drop-down list..

5. Enable the toggle options according to your organization's requirements. The toggle options that are visible can vary depending on the MTD partner.

## Mobile Threat Defense toggle options

> [!NOTE]
>
> Ensure your tenant's MDM Authority is [set to Intune](../fundamentals/mdm-authority-set.md#set-mdm-authority-to-intune) to see the full list of toggle options.

You can decide which MTD toggle options you need to enable according to your organization's requirements. Here are more details:

**App Protection Policy Settings**:

- **Connect Android devices of version 4.4 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule evaluate devices including data from this connector.

- **Connect iOS devices version 11 and above to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the Device Threat Level rule evaluate devices including data from this connector.

**Common Shared Settings**:

- **Number of days until partner is unresponsive**: Number of days of inactivity before Intune considers the partner to be unresponsive because the connection is lost. Intune ignores compliance state for unresponsive MTD partners.

> [!TIP]
>
> You can see the **Connection status** and the **Last synchronized** time between Intune and the MTD partner from the Mobile Threat Defense pane.

## Next Steps

- [Create Mobile Threat Defense (MTD) app protection policy with Intune](mtd-app-protection-policy.md).
