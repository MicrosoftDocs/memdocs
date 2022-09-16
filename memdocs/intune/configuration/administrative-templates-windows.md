---
# required metadata

title: Use ADMX templates on Windows 10/11 devices in Microsoft Intune
description: Use Administrative templates in Microsoft Intune and Endpoint Manager to create groups of settings for Windows 10/11 client devices. Use these settings in a device configuration profile. You can control Office programs, Microsoft Edge, secure Internet Explorer, access OneDrive, use remote desktop, enable Auto-Play, set power management settings, use HTTP printing, control user sign-in, and change the event log size.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Use Windows 10/11 templates to configure group policy settings in Microsoft Intune

**Administrative Templates** in Microsoft Intune include thousands of settings that control features in Microsoft Edge version 77 and later, Internet Explorer, Google Chrome, Microsoft Office programs, remote desktop, OneDrive, passwords, PINs, and more. These settings allow administrators to create group policies using the cloud.

This feature applies to:

- Windows 11
- Windows 10

The Intune templates are 100% cloud-based, are built in to Intune (no downloading), and don't require any customizations, including using OMA-URI. They offer a straight-forward way to configure the settings, and find the settings you want:

- The **Windows settings** are similar to group policy (GPO) settings in Active Directory (AD). These settings are built in to Windows, and are [ADMX-backed settings](/windows/client-management/mdm/understanding-admx-backed-policies) that use XML.

- The **Office and Microsoft Edge** settings are ADMX-ingested, and use the same Office administrative template files and Microsoft Edge administrative template files that you would download in on-premises environments.

- You can import custom and third party ADMX and ADML files. For more information, including the steps, go to [Import custom or partner ADMX files](administrative-templates-import-custom.md).

When managing devices in your organization, you want to create groups of settings that apply to different device groups. You also want a simple view of the settings you can configure. You can complete this task using **Administrative Templates** in Microsoft Intune. 

As part of your mobile device management (MDM) solution, use these template settings as a one-stop shop to manage your Windows client devices.

This article lists the steps to create a template for Windows client devices, and shows how to filter all the available settings in Intune. When you create the template, it creates a device configuration profile. You can then assign or deploy this profile to Windows client devices in your organization.

## Before you begin

- Some of these settings are available starting with Windows 10 version 1709 (RS2/build 15063). Some settings aren't included in all the Windows editions. For the best experience, it's suggested to use Windows 10 Enterprise version 1903 (19H1/build 18362) and newer.

- The Windows settings use the [Windows policy CSPs](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies). The CSPs work on different editions of Windows, such as Home, Professional, Enterprise, and so on. To see if a CSP works on a specific edition, go to [Windows policy CSPs](/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

- There are two ways to create an administrative template: Using a template, or using the Settings Catalog. This article focuses on using the **Administrative Templates** template. The Settings Catalog has more Administrative Template settings available.

  For the specific steps to use the Settings Catalog, see [Use the settings catalog to configure settings](settings-catalog.md).

## Create the template

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: To use a logical grouping of settings, select **Templates** > **Administrative Templates**. To see all the settings, select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **ADMX: Windows 10/11 admin template that configures xyz settings in Microsoft Edge**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **All settings** to see an alphabetical list of all the settings. Or, configure settings that apply to devices (**Computer configuration**), and settings that apply to users **(User configuration**):

    :::image type="content" source="./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png" alt-text="Apply ADMX template settings to users and devices in Microsoft Intune and Endpoint Manager admin center.":::

    > [!NOTE]
    > If you're using the **Settings catalog**, then select **Add settings**, and expand **Administrative Templates**. Select any setting to see what you can configure.
    > 
    > :::image type="content" source="./media/administrative-templates-windows/settings-catalog-administrative-templates.png" alt-text="Expand administrative templates in Settings catalog in Microsoft Intune and Endpoint Manager admin center.":::
    > 
    > For more information on creating policies using the Settings Catalog, see [Use the settings catalog to configure settings](settings-catalog.md).

8. When you select **All settings**, every setting is listed. Scroll down to use the before and next arrows to see more settings:

    :::image type="content" source="./media/administrative-templates-windows/administrative-templates-sample-settings-list.png" alt-text="See a sample list of settings and use previous and next buttons in Endpoint Manager admin center and Microsoft Intune.":::

9. Select any setting. For example, filter on **Office**, and select **Activate Restricted Browsing**. A detailed description of the setting is shown. Choose **Enabled**, **Disabled**, or leave the setting as **Not configured** (default). The detailed description also explains what happens when you choose **Enabled**, **Disabled**, or **Not configured**.

    > [!TIP]
    > The Windows settings in Intune correlate to the on-premises group policy path you see in Local Group Policy Editor (`gpedit`).

10. When you select **Computer configuration** or **User configuration**, the setting categories are shown. You can select any category to see the available settings.

    For example, select **Computer configuration** > **Windows components** > **Internet Explorer** to see all the device settings that apply to Internet Explorer:

    :::image type="content" source="./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png" alt-text="See all device settings that apply to Internet Explorer in Microsoft Intune and Endpoint Manager admin center":::

11. Select **OK** to save your changes.

    Continue to go through the list of settings, and configure the settings you want in your environment. Here are some examples:

    - Use the **VBA Macro Notification Settings** setting to handle VBA macros in different Microsoft Office programs, including Word and Excel.
    - Use the **Allow file downloads** setting to allow or prevent downloads from Internet Explorer.
    - Use **Require a password when a computer wakes (plugged in)** to prompt users for a password when devices wake from sleep mode.
    - Use the **Download unsigned ActiveX controls** setting to block users from downloading unsigned ActiveX controls from Internet Explorer.
    - Use the **Turn off System Restore** setting to allow or prevent users from running a system restore on the device.
    - Use the **Allow importing of favorites** setting to allow or block users from importing favorites from another browser into Microsoft Edge.
    - And much more...

12. Select **Next**.
13. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

14. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles in Intune](device-profile-assign.md).

    If the profile is assigned to user groups, then configured ADMX settings apply to any device that the user enrolls, and signs in to. If the profile is assigned to device groups, then configured ADMX settings apply to any user that signs into that device. This assignment happens if the ADMX setting is a computer configuration (`HKEY_LOCAL_MACHINE`), or a user configuration (`HKEY_CURRENT_USER`). With some settings, a computer setting assigned to a user may also impact the experience of other users on that device.

    For more information, see [User groups vs. device groups when assigning policies](device-profile-assign.md#user-groups-vs-device-groups).

    Select **Next**.

15. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Find some settings

There are thousands of settings available in these templates. To make it easier to find specific settings, use the built-in features:

- In your template, select the **Settings**, **State**, **Setting type**, or **Path** columns to sort the list. For example, select the **Path** column, and use the next arrow to see the settings in the `Microsoft Excel` path.

- In your template, use the **Search** box to find specific settings. You can search by setting, or path. For example, select **All settings**, and search for `copy`. All the settings with `copy` are shown:

  :::image type="content" source="./media/administrative-templates-windows/search-copy-settings.png" alt-text="Search for copy to show all the device settings in administrative templates in Microsoft Intune and Endpoint Manager admin center.":::

  In another example, search for `microsoft word`. You see the settings you can set for the Microsoft Word program. Search for `explorer` to see the Internet Explorer settings you can add to your template.

- You can also narrow your search by only selecting **Computer configuration** or **User configuration**.

  For example, to see all the available Internet Explorer user settings, select  **User configuration**, and search for `Internet Explorer`. Only the IE settings that apply to users are shown:

  :::image type="content" source="./media/administrative-templates-windows/show-all-internet-explorer-settings-user-configuration.png" alt-text="In the ADMX template, select user configuration, and search or filter for Internet Explorer in Microsoft Intune.":::

## Create a Known Issue Rollback (KIR) policy

On your enrolled devices, you can use administrative templates to create a Known Issue Rollback (KIR) policy, and deploy this policy to your Windows devices. For the specific steps, go to [Deploy a KIR activation using Microsoft Intune ADMX policy ingestion to managed devices](/troubleshoot/windows-client/group-policy/use-group-policy-to-deploy-known-issue-rollback#deploy-a-kir-activation-using-microsoft-intune-admx-policy-ingestion-to-the-managed-devices).

For more information on KIR, and what it is, go to:

- [Known Issue Rollback: Helping you keep Windows devices protected and productive](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/known-issue-rollback-helping-you-keep-windows-devices-protected/ba-p/2176831)
- [How to use on-premises Group Policy or Intune to deploy a Known Issue Rollback](/troubleshoot/windows-client/group-policy/use-group-policy-to-deploy-known-issue-rollback)

## Next steps

- The template is created, but may not be doing anything yet. Be sure to [assign the template (also called a profile)](device-profile-assign.md) and [monitor the policy status](device-profile-monitor.md).

- [Update Office using administrative templates](administrative-templates-update-office.md).
- [Restrict USB devices using administrative templates](administrative-templates-restrict-usb.md).
- [Create Microsoft Edge policy using ADMX](administrative-templates-configure-edge.md).
- [Import custom or partner ADMX files](administrative-templates-import-custom.md).
- [Tutorial: Use the cloud to configure group policy on Windows client devices with ADMX templates and Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
