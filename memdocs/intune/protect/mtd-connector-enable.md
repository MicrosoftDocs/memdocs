---
# required metadata

title: Enable Mobile Threat Defense connector in Microsoft Intune
titleSuffix: Microsoft Intune
description: Enable the connector between your Mobile Threat Defense (MTD) partner and Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/05/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
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
- sub-mtd-apps
---

# Enable the Mobile Threat Defense connector in Intune

Microsoft Intune can integrate data from a Mobile Threat Defense (MTD) partner for use by device compliance policies and device Conditional Access rules. You can use this information to help protect corporate resources like Exchange and SharePoint, by blocking access from compromised mobile devices.

After you [setup your MTD Partner](../protect/mobile-threat-defense.md#mobile-threat-defense-partners) and configure the Intune connector in the MTD partner console, you can then enable the MTD connection for that MTD partner application from within the Intune admin center.

Applies to:

- All [Intune Mobile Threat Defense partners](../protect/mobile-threat-defense.md#mobile-threat-defense-partners).

## Required role-based access control permissions

To successfully enable the Mobile Threat Defense connector, you must use an account that is assigned [Role-based access control](../fundamentals/role-based-access-control.md) (RBAC) permissions equivalent to the *Endpoint Security Manager* built-in admin role for Intune. If you use a custom role, ensure it includes the *Read* and *Modify* rights for the Intune *Mobile Threat Defense* permission.

## To enable the Mobile Threat Defense connector

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Mobile Threat Defense**.

3. On the **Mobile Threat Defense** pane, select **Add**.

4. For **Mobile Threat Defense connector to setup**, select your MTD partner solution from the drop-down list.

   > [!NOTE]
   >
   > As of the August 2023 Intune service release (2308), classic Conditional Access (CA) policies are no longer created for the **Microsoft Defender for Endpoint** connector. As of April 2024 Intune service release (2404), classic CA policies are no longer needed for 3rd party **Mobile Threat Defense** connectors either. If your tenant has a classic CA policy that was previously created for integration with Microsoft Defender for Endpoint or 3rd party Mobile Threat Defense connectors, it can be deleted.

5. Enable the toggle options according to your organization's requirements. The toggle options that are visible can vary depending on the MTD partner. For example, the following image shows the available options that are available for Symantec Endpoint Protection:

   :::image type="content" source="./media/mtd-connector-enable/enable-mtd-connector-1.png" alt-text="Screen shot example that shows the MDM Compliance Policy Settings for the MDT connector.":::

## Mobile Threat Defense toggle options

> [!NOTE]
>
> Ensure your tenant's MDM Authority is [set to Intune](../fundamentals/mdm-authority-set.md#set-mdm-authority-to-intune) to see the full list of toggle options.

The available options for connectors are divided into three categories. When a partner doesn't support a category, that category isn't available:

- Compliance policy evaluation
- App protection policy evaluation
- Shared settings

Enable the toggles for those options your organization requires.

### Compliance policy evaluation

- **Connect Android devices version _\<supported versions>_ and above to _\<MTD partner name>_**: When you enable this option, compliance policies using the Device Threat Level rule for Android devices (on supported OS versions) evaluate devices including data from this connector.

- **Connect iOS/iPadOS devices version _\<supported versions>_ and above to _\<MTD partner name>_**: When you enable this option, compliance policies using the Device Threat Level rule for iOS/iPadOS devices (on supported OS versions) evaluate devices including data from this connector.

- **Enable App Sync for iOS Devices**: Allows this Mobile Threat Defense partner to request metadata of iOS applications from Intune to use for threat analysis purposes. This iOS device must be MDM-enrolled device and provides updated app data during device check-in. You can find standard Intune policy check-in frequencies in the [Refresh cycle times](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

  > [!NOTE]
  >
  > App Sync data is sent to Mobile Threat Defense partners at an interval based on device check-in, and should **not** be confused with the refresh interval for the [Discovered Apps report](../apps/app-discovered-apps.md#details-of-discovered-apps).

- **Send full application inventory data on personally-owned iOS/iPadOS Devices​**: This setting controls the application inventory data that Intune shares with this Mobile Threat Defense partner. Data is shared when the partner syncs app data and requests the app inventory list.

  Choose from the following options:

  - **On** - Allows this Mobile Threat Defense partner to request a list of iOS/iPadOS applications from Intune for personally-owned iOS/iPadOS devices. This list includes unmanaged apps (apps not deployed through Intune) and the apps that were deployed through Intune.
  - **Off** - Data about unmanaged apps isn't provided to the partner. Intune does share data for the apps that are deployed through Intune.

  This setting has no effect for corporate devices. For corporate devices, Intune sends data about both managed and unmanaged apps when requested by this MTD vendor.

- **Block unsupported OS versions**: Block if the device is running an operating system less than the minimum supported version. Details of the minimum supported version would be shared within the docs for the Mobile Threat Defense vendor.

### App protection policy evaluation

- **Connect Android devices of version *\<supported versions>* to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the "Max allowed threat level" rule evaluate devices including data from this connector.

- **Connect iOS devices version *\<supported versions>* to *\<MTD partner name>* for app protection policy evaluation**: When you enable this option, app protection policies using the "Max allowed threat level" rule evaluate devices including data from this connector.

To learn more about using Mobile Threat Defense connectors for Intune App Protection Policy evaluation, see [Set up Mobile Threat Defense for unenrolled devices](mtd-enable-unenrolled-devices.md).

### Shared settings

- **Number of days until partner is unresponsive**: Number of days of inactivity before Intune considers the partner to be unresponsive because the connection is lost. Intune ignores compliance state for unresponsive MTD partners.

> [!IMPORTANT]
> When possible, we recommend that you add and assign the MTD apps *before* creating the device compliance and the Conditional Access policy rules. This helps ensures that the MTD app is ready and available for end users to install before they can get access to email or other company resources.

> [!TIP]
> You can see the **Connection status** and the **Last synchronized** time between Intune and the MTD partner from the Mobile Threat Defense pane.

## Next steps

- [Create Mobile Threat Defense (MTD) device compliance policy with Intune](mtd-device-compliance-policy-create.md)
