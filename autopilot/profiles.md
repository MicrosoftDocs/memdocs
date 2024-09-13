---
title: Configure Autopilot profiles
description: Learn how to configure device profiles for Windows Autopilot deployment.
ms.subservice: autopilot
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
  - essentials-manage
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Configure Autopilot profiles

After the [device group](enrollment-autopilot.md) is created, a Windows Autopilot deployment profile can be applied to each device in the group. Deployment profiles determine the deployment mode, and customize the out-of-box experience (OOBE) for end users.

Autopilot profiles can be created via:

1. [Microsoft 365 admin center](https://admin.microsoft.com/).
1. [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. [Intune graph](/graph/api/resources/intune-graph-overview).

For Intune managed devices, pre-provisioning, self-deploying, and co-management profiles can only be created and assigned in Intune.

## Create an Autopilot deployment profile

Autopilot deployment profiles are used to configure the Autopilot devices. Up to 350 profiles can be created per tenant.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment Profiles**

1. In the **Windows Autopilot deployment profiles** screen, select the **Create Profile** drop down menu and then select either **Windows PC** or **HoloLens**. This article explains how to set up Autopilot for Windows PC. For more information about Autopilot and HoloLens, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

1. In the **Create profile** screen, on the **Basics** page, enter a **Name** and optional **Description**.

1. If all devices in the assigned groups should automatically register to Autopilot, set **Convert all targeted devices to Autopilot** to **Yes**. All corporate owned, non-Autopilot devices in assigned groups register with the Autopilot deployment service. Personally owned devices aren't registered to Autopilot. Allow 48 hours for the registration to be processed. When the device is unenrolled and reset, Autopilot enrolls it again. After a device is registered in this way, disabling this setting or removing the profile assignment won't remove the device from the Autopilot deployment service. The device must instead be [removed directly](add-devices.md#delete-autopilot-devices).

    > [!NOTE]
    >
    > Using the setting **Convert all targeted devices to Autopilot** doesn't automatically convert existing Microsoft Entra hybrid device in the assigned groups into a Microsoft Entra device. The setting only registers the devices in the assigned groups for the Autopilot service.

1. Select **Next**.

1. On the **Out-of-box experience (OOBE)** page, for **Deployment mode**, select one of these two options:

    - **User-driven**: Devices with this profile are associated with the user enrolling the device. User credentials are required to enroll the device.

    - **Self-deploying**: Devices with this profile aren't associated with the user enrolling the device. User credentials aren't required to enroll the device. When a device has no user associated with it, user-based compliance policies don't apply to it. When self-deploying mode is used, only compliance policies targeting the device are applied.

    :::image type="content" source="images/create-profile-out-of-box.png" alt-text="Screenshot of OOBE page.":::

    > [!NOTE]
    >
    > Options that are dimmed or shaded in the selected deployment mode aren't currently supported.

1. In the **Join to Microsoft Entra ID as** box, select **Microsoft Entra joined**.

1. Configure the following options:

    - **Microsoft Software License Terms**: Select whether or not to show the EULA to users.

    - **Privacy settings**: Select whether or not to show privacy settings to users.

      > [!IMPORTANT]
      >
      > The default value for the Diagnostic Data setting is set to Full during the out-of-box experience. For more information, see [Windows Diagnostics Data](/windows/privacy/windows-diagnostic-data).

    - **Hide change account options**: Select **Hide** to prevent change account options from displaying on the company sign-in and domain error pages. This option requires [company branding to be configured in Microsoft Entra ID](/azure/active-directory/fundamentals/customize-branding).

    - **User account type**: Select the user's account type (**Administrator** or **Standard** user). We allow the user joining the device to be a local Administrator by adding them to the local Admin group. We don't enable the user as the default administrator on the device.

    - **Allow pre-provisioned deployment** ([Requirements](pre-provision.md#requirements)): Select **Yes** to allow pre-provisioning support.

      > [!NOTE]
      >
      > When setting **Allow pre-provisioned deployment** to **No**, it's still possible to press the Windows key five times during OOBE to invoke pre-provisioning and progress down that path. However, Intune enforces this setting and a pre-provisioning failure with error code 0x80180005 occurs.

    - **Language (Region)**: Select the language to use for the device. This option is available in all Deployment modes.

    - **Automatically configure keyboard**: If a **Language (Region)** is selected, select **Yes** to skip the keyboard selection page. This option is available in all Deployment modes.

        > [!NOTE]
        >
        > Language and keyboard settings requires ethernet connectivity. Wi-fi connectivity isn't supported because of the requirement to select a language, locale, and keyboard to make that Wi-fi connection.

    - **Apply device name template** (requires Microsoft Entra join type): Select **Yes** to create a template to use when naming a device during enrollment. Names must be 15 characters or less, and can have letters, numbers, and hyphens. Names can't be all numbers. Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number. Or, use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add. Only a prefix can be provided for hybrid devices in a [domain join profile](./windows-autopilot-hybrid.md#create-and-assign-a-domain-join-profile).

1. Select **Next**.

1. On the **Assignments** page, select **Selected groups** for **Assign to**.

    :::image type="content" source="images/create-profile-assignments.png" alt-text="Screenshot of Assignments page.":::

1. Select **Select groups to include**, and select the groups to include in this profile.

1. To exclude any groups, select **Select groups to exclude**, and select the groups to exclude.

   > [!NOTE]
   >
   > When the assignment **All Devices** is used, exclusions aren't supported. Attempting to exclude groups while targeting to all devices might cause assignment problems and might require uploading device hashes again.

1. Select **Next**.

1. On the **Review + Create** page, select **Create** to create the profile.

    :::image type="content" source="images/create-profile-review.png" alt-text="Screenshot of Review page.":::

### Assignment of Autopilot deployment profiles to devices

Intune periodically checks for new devices in the assigned groups, and then begin the process of assigning deployment profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Microsoft Entra ID groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.

Before deploying a device, ensure that a Windows Autopilot deployment profile is assigned to the device. To ensure the process is complete:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, monitor the **Profile Status** column for a device that just had a deployment profile assigned to it. The profile status changes from **Unassigned** to **Assigning** and finally to **Assigned**.

1. Once the device is showing **Assigned**, open the properties of the device by selecting it.

1. In the device properties pane that opens, ensure that **Date assigned** is populated. If **Date assigned** isn't yet populated, wait until it populates before deploying the device.

## Edit an Autopilot deployment profile

After the Autopilot deployment profile is created, certain parts of the deployment profile can be edited.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment profiles**.

1. Select the profile to edit.

1. Select **Properties** to change the name or description of the deployment profile. Select **Save** after making changes.

1. Select **Settings** to make changes to the OOBE settings. Select **Save** after making changes.

    > [!NOTE]
    >
    > Changes to the profile are applied to devices assigned to that profile. However, the updated profile won't be applied to a device that is already enrolled in Intune until after the device is reset and enrolled again.

If a device is registered in Autopilot and a profile isn't assigned, it receives the default Autopilot profile. If a device shouldn't go through Autopilot, the Autopilot registration must be removed.

## Autopilot profile priority

If a group is assigned to multiple Autopilot profiles, the device would receive the oldest created profile to resolve the conflict. If no other profile is applicable to the device and there's a default profile (any Autopilot profile assigned to all devices), then the default profile is applied. If a device is assigned to a security group that isn't assigned to Autopilot profile, then it would receive the default profile targeted to all devices. To see when an Autopilot profile is created:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment Profiles**.

1. In the **Windows Autopilot deployment profiles** screen, under **Name**, select the Autopilot profile name where the create date needs to be viewed.

1. When the Windows Autopilot deployment profile screen opens, the date the Windows Autopilot deployment profile was created is displayed under **Essentials** and next to **Created**.

## Autopilot deployments report

Details on each device deployed through Windows Autopilot can be seen through a report. To see the report, go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Windows Autopilot deployment status**. The data is available for 30 days after deployment.

This report is in preview. Only new Intune enrollment events trigger device deployment records. Deployments that don't trigger a new Intune enrollment don't appear in this report. This case includes any kind of reset that maintains enrollment and the user portion of Autopilot pre-provisioning.

## Autopilot profile tutorials

The following articles are tutorials on configuring and assigning a Windows Autopilot deployment profile for each of the Windows Autopilot scenarios via Intune:

- [User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Autopilot profile](tutorial/user-driven/azure-ad-join-autopilot-profile.md).
- [User-driven Microsoft Entra hybrid join: Create and assign user-driven Microsoft Entra hybrid join Autopilot profile](tutorial/user-driven/hybrid-azure-ad-join-autopilot-profile.md).
- [Pre-provision Microsoft join: Create and assign a pre-provisioned Microsoft Entra join Autopilot profile](tutorial/pre-provisioning/azure-ad-join-autopilot-profile.md).
- [Pre-provision Microsoft Entra hybrid join: Create and assign a pre-provisioned Microsoft Entra hybrid join Autopilot profile](tutorial/pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md).
- [Self-deploying mode: Create and assign self-deploying Autopilot profile](tutorial/self-deploying/self-deploying-autopilot-profile.md).

## Related content

- [How are Windows Autopilot device profiles downloaded?](troubleshooting-faq.yml#how-are-windows-autopilot-device-profiles-downloaded-)
- [Registering devices](add-devices.md).
