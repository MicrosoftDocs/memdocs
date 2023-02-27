---
# required metadata

title: Enable Mobile Threat Defense connector in Microsoft Intune
titleSuffix: Microsoft Intune
description: Enable the connector between your Mobile Threat Defense (MTD) partner and Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/21/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: dbb6a37e-ba47-4b69-922c-d25e66c279f6

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Enable the Mobile Threat Defense connector in Intune

During Mobile Threat Defense (MTD) setup, you've configured a policy for classifying threats in your Mobile Threat Defense partner console and you've created the device compliance policy in Intune. If you've already configured the Intune connector in the MTD partner console, you can now enable the MTD connection for MTD partner applications.

> [!NOTE]
> This topic applies to all Mobile Threat Defense partners.

## Classic conditional access policies for MTD apps

When you integrate a new application to Intune Mobile Threat Defense and enable the connection to Intune, Intune creates a classic conditional access policy in Azure Active Directory. Each MTD app you integrate, including [Microsoft Defender for Endpoint](advanced-threat-protection.md) or any of our other [MTD partners](mobile-threat-defense.md#mobile-threat-defense-partners), creates a new classic conditional access policy. These policies can be ignored, but shouldn't be edited, deleted, or disabled.

If the classic policy is deleted, you'll need to delete the connection to Intune that was responsible for its creation, and then set it up again. This process recreates the classic policy. It's not supported to migrate classic policies for MTD apps to the new policy type for conditional access.

Classic conditional access policies for MTD apps:

- Are used by Intune MTD to require that devices are registered in Azure AD so that they have a device ID before communicating to MTD partners. The ID is required so that devices and can successfully report their status to Intune.

- Have no effect on any other Cloud apps or Resources.

- Are distinct from conditional access policies you might create to help manage MTD.

- By default, don't interact with other conditional access policies you use for evaluation.

To view classic conditional access policies, in [Azure](https://portal.azure.com/#home), go to **Azure Active Directory** > **Conditional Access** > **Classic policies**.

## To enable the Mobile Threat Defense connector

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Mobile Threat Defense**. To set up an integration with a third-party Mobile Threat Defense vendor, you must be an Azure *Global administrator* or be assigned the *Endpoint Security Manager* built-in admin role for Intune.

3. On the **Mobile Threat Defense** pane, select **Add**.

4. For **Mobile Threat Defense connector to setup**, select your MTD solution from the drop-down list.

5. Enable the toggle options according to your organization's requirements. Toggle options visible will vary depending on the MTD partner.  For example, the following image shows the options that are available for Symantec Endpoint Protection:

   :::image type="content" source="./media/mtd-connector-enable/enable-mtd-connector-1.png" alt-text="Screen shot example that shows the MDM Compliance Policy Settings for the MDT connector.":::

## Mobile Threat Defense toggle options

You can decide which MTD toggle options you need to enable according to your organization's requirements. Not all of the following options are supported by all Mobile Threat Defense partners:

**Compliance policy evaluation**

- **Connect Android devices version _\<supported versions>_ and above to _\<MTD partner name>_**: When you enable this option, compliance policies using the Device Threat Level rule for Android devices (on supported OS versions) will evaluate devices including data from this connector.

- **Connect iOS/iPadOS devices version _\<supported versions>_ and above to _\<MTD partner name>_**: When you enable this option, compliance policies using the Device Threat Level rule for iOS/iPadOS devices (on supported OS versions) will evaluate devices including data from this connector.

- **Enable App Sync for iOS Devices**: Allows this Mobile Threat Defense partner to request metadata of iOS applications from Intune to use for threat analysis purposes. This iOS device must be MDM-enrolled device and will provide updated app data during device check-in. You can find standard Intune policy check-in frequencies in the [Refresh cycle times](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned). 

  > [!NOTE]  
  > App Sync data is sent to Mobile Threat Defense partners at an interval based on device check-in, and should **not** be confused with the refresh interval for the [Discovered Apps report](../apps/app-discovered-apps.md#details-of-discovered-apps).

- **Send full application inventory data on personally-owned iOS/iPadOS Devices​**: This setting controls the application inventory data that Intune shares with this Mobile Threat Defense partner when the partner syncs app data and requests the app inventory list.

  Choose from the following options:

  - **On** - Allows this Mobile Threat Defense partner to request a list of iOS/iPadOS applications from Intune for personally-owned iOS/iPadOS devices. This list includes unmanaged apps (apps not deployed through Intune) and the apps that were deployed through Intune. 
  - **Off** - Data about unmanaged apps isn't provided to the partner. Intune does share data for the apps that are deployed through Intune.

  This setting has no effect for corporate devices. For corporate devices, Intune sends data about both managed and unmanaged apps when requested by this MTD vendor.

- **Block unsupported OS versions**: Block if the device is running an operating system less than the minimum supported version. Details of the minimum supported version would be shared within the docs for the Mobile Threat Defense vendor.

**App protection policy evaluation**

- **Connect Android devices of version *\<supported versions>* to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the "Max allowed threat level" rule will evaluate devices including data from this connector.

- **Connect iOS devices version *\<supported versions>* to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the "Max allowed threat level" rule will evaluate devices including data from this connector.

To learn more about using Mobile Threat Defense connectors for Intune App Protection Policy evaluation, see [Set up Mobile Threat Defense for unenrolled devices](mtd-enable-unenrolled-devices.md).

**Common Shared Settings**

- **Number of days until partner is unresponsive**: Number of days of inactivity before Intune considers the partner to be unresponsive because the connection is lost. Intune ignores compliance state for unresponsive MTD partners.

> [!IMPORTANT]
> When possible, we recommend that you add and assign the MTD apps before creating the device compliance and the Conditional Access policy rules. This helps ensures that the MTD app is ready and available for end users to install before they can get access to email or other company resources.

> [!TIP]
> You can see the **Connection status** and the **Last synchronized** time between Intune and the MTD partner from the Mobile Threat Defense pane.

## Next steps

- [Create Mobile Threat Defense (MTD) device compliance policy with Intune](mtd-device-compliance-policy-create.md).
