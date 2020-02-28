---
# required metadata

title: Use templates for Windows 10 devices in Microsoft Intune - Azure | Microsoft Docs
description: Use Administrative templates in Microsoft Intune to create groups of settings for Windows 10 devices. Use these settings in a device configuration profile to control Office programs, Microsoft Edge, secure features in Internet Explorer, control access to OneDrive, use remote desktop features, enable Auto-Play, set power management settings, use HTTP printing, use different user sign in options, and control the event log size.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use Windows 10 templates to configure group policy settings in Microsoft Intune

When managing devices in your organization, you want to create groups of settings that apply to different device groups. For example, you have several device groups. For GroupA, you want to assign a specific set of settings. For GroupB, you want to assign a different set of settings. You also want a simple view of the settings you can configure.

You can complete this task using **Administrative Templates** in Microsoft Intune. The administrative templates include hundreds of settings that control features in Microsoft Edge version 77 and later, Internet Explorer, Microsoft Office programs, remote desktop, OneDrive, passwords and PINs, and more. These settings allow group administrators to manage group policies using the cloud.

The Windows settings are similar to group policy (GPO) settings in Active Directory (AD). These settings are built in to Windows, and are [ADMX-backed settings](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) that use XML. The Office and Microsoft Edge settings are ADMX-ingested, and use the ADMX settings in [Office administrative template files](https://www.microsoft.com/download/details.aspx?id=49030) and [Microsoft Edge administrative template files](https://www.microsoftedgeinsider.com/enterprise). But, the Intune templates are 100% cloud-based. They offer a simple and straight-forward way to configure the settings, and find the settings you want.

**Administrative Templates** are built in to Intune, and don't require any customizations, including using OMA-URI. As part of your mobile device management (MDM) solution, use these template settings as a one-stop shop to manage your Windows 10 devices.

This article lists the steps to create a template for Windows 10 devices, and shows how to filter all the available settings in Intune. When you create the template, it creates a device configuration profile. You can then assign or deploy this profile to Windows 10 devices in your organization.

## Before you begin

- Some of these settings are available starting with Windows 10 version 1703 (RS2). Some settings aren't included in all the Windows editions. For the best experience, it's suggested to use Windows 10 Enterprise version 1903 (19H1) and newer.

- The Windows settings use [Windows policy CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). The CSPs work on different editions of Windows, such as Home, Professional, Enterprise, and so on. To see if a CSP works on a specific edition, go to [Windows policy CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## Create a template

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a name for the profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Administrative Templates**.

4. Select **Create**. In the new window, select the drop-down list, and select **All products**. From the list, you can also filter the settings to only show **Windows** settings, only show **Office** settings, or only show **Edge version 77 or later** settings:

    > [!div class="mx-imgBorder"]
    > ![Filter the list to show all Windows or all Office settings in administrative templates in Intune](./media/administrative-templates-windows/administrative-templates-choose-windows-office-all-products.png)

    > [!NOTE]
    > Microsoft Edge settings apply to:
    >
    > - Microsoft Edge version 77 and newer. To configure Microsoft Edge version 45 and earlier, see [Microsoft Edge Browser device restriction settings](device-restrictions-windows-10.md#microsoft-edge-browser).
    > - Windows 10 RS4 and newer with [KB 4512509](https://support.microsoft.com/kb/4512509) installed
    > - Windows 10 RS5 and newer with [KB 4512534](https://support.microsoft.com/kb/4512534) installed
    > - Windows 10 19H1 and newer with [KB 4512941](https://support.microsoft.com/kb/4512941) installed

5. Every setting is listed, and you can use the before and next arrows to see more settings:

    > [!div class="mx-imgBorder"]
    > ![See a sample list of settings and use previous and next buttons](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

    > [!TIP]
    > The Windows settings in Intune correlate to the on-premises group policy path you see in Local Group Policy Editor (`gpedit`).

6. Select any setting. For example, filter on **Office**, and select **Activate Restricted Browsing**. A detailed description of the setting is shown. Choose **Enabled**, **Disabled**, or leave the setting as **Not configured** (default). The detailed description also explains what happens when you choose **Enabled**, **Disabled**, or **Not configured**.
7. Select **OK** to save your changes.

Continue to go through the list of settings, and configure the settings you want in your environment. Here are some examples:

- Use the **VBA Macro Notification Settings** setting to handle VBA macros in different Microsoft Office programs, including Word and Excel.
- Use the **Allow file downloads** setting to allow or prevent downloads from Internet Explorer.
- Use **Require a password when a computer wakes (plugged in)** to prompt users for a password when devices wake from sleep mode.
- Use the **Download unsigned ActiveX controls** setting to block users from downloading unsigned ActiveX controls from Internet Explorer.
- Use the **Turn off System Restore** setting to allow or prevent users from running a system restore on the device.
- Use the **Allow importing of favorites** setting to allow or block users from importing favorites from another browser into Microsoft Edge.
- And much more...

## Find some settings

There are hundreds of settings available in these templates. To make it easier to find specific settings, use the built-in features:

- In your template, select the **Settings**, **State**, **Setting type**, or **Path** columns to sort the list. For example, select the **Path** column, and use the next arrow to see the settings in the `Microsoft Excel` path:

  > [!div class="mx-imgBorder"]
  > ![Click path to show all the settings grouped by the group policy or ADMX path in administrative templates in Intune](./media/administrative-templates-windows/path-filter-shows-excel-options.png)

- In your template, use the **Search** box to find specific settings. You can search by setting, or path. For example, search for `copy`. All the settings with `copy` are shown:

  > [!div class="mx-imgBorder"]
  > ![Search for copy to show all the Windows and Office settings in administrative templates in Intune](./media/administrative-templates-windows/search-copy-settings.png) 

  In another example, search for `microsoft word`. You see all the settings you can set for the Microsoft Word program. Search for `explorer` to see all the Internet Explorer settings you can add to your template.

## Next steps

The template is created, but it's not doing anything yet. Next, [assign the template, also called a profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

[Update Office 365 using administrative templates](administrative-templates-update-office.md).

[Tutorial: Use the cloud to configure group policy on Windows 10 devices with ADMX templates and Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
