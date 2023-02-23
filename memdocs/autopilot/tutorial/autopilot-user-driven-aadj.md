---
title: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune
description: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune

*Applies to:*

- Windows 11
- Windows 10

## Overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices will be strictly Azure AD joined. The purpose of this tutorial is to provide in one article a step by step guide for all the steps required for a successful Autopilot user-driven Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Workflow

Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign Autopilot profile> Assign Autopilot device to a user (optional)

> [!NOTE]
>
> The workflow is designed for lab or testing scenarios. However, some of the steps in the workflow are interchangeable. A workflow with some of these steps interchanged may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Register devices as Autopilot devices

Before a device can use Autopilot, it must be registered as an Autopilot device. Registering a devices as an Autopilot device can be thought of as importing the device into Autopilot so that Autopilot can be used on the device. It does not mean that the device has ever used the Autopilot service. It just makes the Autopilot service available to the device.

Also note that a device registered in Autopilot doesn't mean the device is enrolled in Intune. A device may be registered as an Autopilot device but may not exist in Intune. It's not until an Autopilot registered device goes through the Autopilot process for the first time that it becomes enrolled in Intune. After the Autopilot device undergoes the Autopilot process and enrolls in Intune, the Autopilot device subsequently appears as a device in both Azure AD and Intune.

> [!TIP]
>
> For Configuration Manager admins, an Autopilot device before undergoing the Autopilot process for the first time can be thought of as the equivalent of an Unknown Computer.

There are several methods to register a device as an Autopilot device in Intune:

- Manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
  - [PowerShell script](/mem/autopilot/add-devices#powershell)
  - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
  - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)
  
  The above methods of obtaining the hardware hash of a device are well documented. The corresponding documentation can be viewed by selecting the appropriate link listed above.

- Automatically registering device via:
  - An [OEM](/mem/autopilot/oem-registration), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices
  - A [partner](/mem/autopilot/partner-registration)

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be viewed by selecting the appropriate link listed above.

For most organizations, using an OEM or partner to register devices as Autopilot devices is the preferred, most common, and most secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Autopilot devices via the hardware hash is also used.

> [!IMPORTANT]
>
> Assuming that a device isn't currently enrolled Intune, remember that registering a device in Autopilot doesn't make it an Intune enrolled device. That device won't enroll into Intune until Autopilot runs on the device for the first time.

### Importing the CSV file with the hardware hash for devices into Intune

Several of the above methods on obtaining the hardware hash when manually registering devices as Autopilot devices will produce a CSV file that contains the hardware hash of the device. This CSV file with the hardware hash needs to be imported into Intune to register the device as an Autopilot device.

After the CSV files has been created, it can be imported into Intune via the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform: Windows**.

3. Select **Windows enrollment** > **Windows Autopilot Deployment Program: Devices**.

4. In the **Windows Autopilot devices** screen, select **Import**.

5. In the **Add Windows Autopilot devices** pane, under **Specify the path to the list you want to import.**, select the blue select a file folder.

6. Browse to the CSV file obtained using one of the above methods to obtain the hardware hash of a device.

7. After selecting the CSV file, verify that the correct CSV file is selected under **Specify the path to the list you want to import.**, and then select **Import**. Importing can take several minutes.

8. After the import is complete, in the **Windows Autopilot devices** screen, select **Sync**.

   A message will display saying that the sync is in progress. The sync process might take a few minutes to complete, depending on how many devices are being synchronized.

    > [!NOTE]
    >
    > If another sync is attempted within 10 minutes after initiating a sync, an error will be displayed. Syncs can only occur once every 10 minutes. To attempt a sync again, wait at least 10 minutes before trying again.

9. Select **Refresh** to refresh the view. The newly imported devices should display within a few minutes. If the devices aren't yet displayed, wait a few minutes and then select **Refresh** again.

For more information on registering devices as Autopilot devices, see the following articles:

- [Manually register devices with Windows Autopilot](/mem/autopilot/add-devices)
- [Windows Autopilot customer consent](/mem/autopilot/registration-auth)

## Create a device group

Device groups are a collection of devices organized into a Azure AD group. Device groups are used in Autopilot to target devices for specific configurations such what policies to apply to a device and what applications to install on the device.

Device groups can either by dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules
- **Assigned groups** - Devices are manually added to the group and are static

When configuring Autopilot, dynamic groups are primarily used since a large number of devices are usually involved. Adding the devices in automatically rules makes management of the group a lot easier. Adding a large amount of device in manually via an assigned group would be impractical. However, if there is a small number of devices, for example for testing purposes, an assigned group can also be used.

To create a dynamic device group for use with Autopilot, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Groups** > **New group**.

3. In the **New Group** screen, configure the following properties:

    1. **Group type**: Select **Security**.

    2. **Group name** and **Group description**: Enter a name and description for the device group.

    3. **Azure AD roles can be assigned to the group**: Select **No**.

    4. **Membership type**: Select **Dynamic Device**.

    5. **Owners**: Select users that own the group.

    6. **Dynamic device members**: Select **Add dynamic query**. In the **Dynamic membership rules** screen, select **Add expression**.

      > [!NOTE]
      > When selecting **Dynamic Device** in step d, this field will change to **Dynamic device members**.

      Rules on what devices will be added to the device group are entered in the **Dynamic membership rules** screen under **Configure Rules**. Rules can be entered in the rule builder via the drop down boxes or the rule syntax can be directly entered via the **Edit** option in the **Rule syntax** section.

      The most common type of dynamic device group when using Autopilot is a device group that contains all Autopilot devices. A dynamic device group that contains all Autopilot devices has the following syntax:

      `(device.devicePhysicalIDs -any (_ -contains "[ZTDID]"))`

      This rule can be entered in by selecting the **Edit** option in the **Rule syntax** section and then pasting in the rule in the **Edit rule syntax** screen under **Rule syntax**. Once the rule has been pasted in, select **OK**, and then select **Save**.

      For more information on creating rules for dynamic groups, see [Dynamic membership rules for groups in Azure Active Directory](/azure/active-directory/enterprise-users/groups-dynamic-membership).

4. Once the dynamic rule has been entered and saved, in the **New Group** screen, select **Create**. This will finish creating the dynamic group.

> [!NOTE]
> The above steps are creating a dynamic group in Azure AD which is used by Intune and Autopilot. Although the groups can be accessed in the Intune portal, they are Azure AD groups.

> [!TIP]
> For Configuration Manager admins, device groups are similar to device based collections. Dynamic device groups are similar to query based device collections while assigned device groups are similar to direct membership device collections.

For more information on creating groups in Intune, see the following articles:

- [Create device groups](/mem/autopilot/enrollment-autopilot)
- [Add groups to organize users and devices](/mem/intune/fundamentals/groups-add)
- [Manage Azure Active Directory groups and group membership](/azure/active-directory/fundamentals/how-to-manage-groups)

## Configure and assign the Enrollment Status Page (ESP)

The main feature of the Enrollment Status Page (ESP) is to display progress and current status to the end user while the device is being set up and enrolled via the Autopilot process. The other main feature of the ESP is to block a user from signing in and using the device until all required policies and applications are installed. Multiple ESP profiles can be created with different settings and assigned appropriately based on different needs and scenarios.

Out of box there is a default ESP that is assigned to all devices. The default settings in the default ESP is to not show app and profile progress during the Autopilot process. However, it is highly recommended to change this default via a separate custom ESP to show app and profile progress. If the device has many policies and applications that need to be installed and progress is not displayed, it may make end users think that that the device is hung during the setup process due to the amount of time it is taking for all of the policies to be applied and applications to be installed. Additionally, disabling app and profile progress will not block the user from signing into the device and using the device until all policies and applications are installed. This can cause issues if the device is not fully configured and ready for use.

The ESP has two phases:

- Device ESP - ESP that runs during the OOBE process and applies device policies and installs device applications
- User ESP - ESP that runs after Device ESP that sets up user account, applies user policies, and installs user applications

The ESP configuration has the option to only display app and profile progress during the device ESP phase while disabling during the user ESP phase. This is usually done to allow a user to sign into the device sooner and reach the desktop, but at the consequence that not all of the user policies and applications may be installed. For this reason, it is recommended to show app and profile progress during both phases.

To configure and assign the Autopilot Enrollment Status Page (ESP) so that it shows progress during app and profile configurations, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment** > **General: Enrollment Status Page**.

5. In the **Enrollment Status Page**, select **Create**.

6. In the **Basics** page of the **Create profile** screen, enter a **Name** and **Description** for the ESP profile, and then select **Next**.

7. In the **Settings** page, toggle the option **Show app and profile configuration progress** to **Yes**.

8. After toggling the option **Show app and profile configuration progress** to **Yes**, several new options will appear. Configure these options based on the desired behavior for the ESP:

   - **Show an error when installation takes longer than specified number of minutes**: The default time-out is 60 minutes. Enter a higher value if you think more time is needed to install apps on the devices.

   - **Show custom message when time limit or error occur**:
     - **No**: The default message is shown to users when an error occurs. That message is: **Setup could not be completed. Please try again or contact your support person for help.**
     - **Yes**: A custom message is shown to users when an error occurs. Enter a custom message in the provided text box.  

   - **Turn on log collection and diagnostics page for end users**:  
     - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.  
     - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11. Logs and diagnostics may aid with troubleshooting. For this reason. it's recommend to enable this option.

   - **Only show page to devices provisioned by out-of-box experience (OOBE)**:
     - **No**: The ESP is shown on all Intune-managed and co-managed devices that go through the out-of-box experience (OOBE), and to the first user that signs in to each device. Subsequent users who sign in won't see the ESP.
     - **Yes**: The ESP is only shown on devices that go through the out-of-box experience (OOBE).

   - **Block device use until all apps and profiles are installed**:
     - **No**: Users can leave the ESP before Intune is finished setting up the device.
     - **Yes**: Users can't leave the ESP until Intune is done setting up the device. Enabling this option unlocks the following additional options:  

       - **Allow users to reset device if installation error occurs**:  
         - **No**: The ESP doesn't give users the option to reset theirs devices when an installation fails.  
         - **Yes**: The ESP gives users the option to reset their devices when an installation fails.  

       - **Allow users to use device if installation error occurs**:
         - **No**: The ESP doesn't give users the option to bypass the ESP when an installation fails.  
         - **Yes**: The ESP gives users the option to bypass the ESP and use their devices when an installation fails.

       - **Block device use until these required apps are installed if they are assigned to the user/device**:  
         - **All**: All assigned apps must be installed before users can use their devices.  
         - **Selected**: Selected apps must be installed before users can use their devices. After enabling this option, select **Select apps** to select the managed apps from Intune that are required to be installed before users can use their device.

9. Once the different ESP options under the **Settings** page have been configured as desired, select **Next**.

10. In the **Assignments** page, select **Add groups**.

11. In the the **Select groups to include** pane, select the device group(s) to target the ESP profile. This normally would be the device group(s) created in the section [Create a device group](#create-a-device-group). After selecting the device group, select **Select**.

    > [!TIP]
    >
    > After selecting the device group(s), you can select the **Edit filter** option on each device group added to the assignment to further refine what devices are targeted for the ESP profile. For example, this can be useful if you want to exclude some of the devices that are members in the device group(s) selected.

    > [!NOTE]
    >
    > ESPs are assigned to device groups and not directly to individual devices. To assign an ESP to a specific device, the device must be a member of a device group that has an ESP assigned to it.

12. Select **Next**.  

13. In the **Scope tags** page, select **Next**.

    > [!NOTE]
    > **Scope tags** are optional and are a method to control who has access to the ESP configuration. For the purpose of this tutorial, scope tags is being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this screen. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).

14. In the **Review + create** page, review the settings and verify everything is correct and configured as desired. Once verified, select **Create** to save the changes and assign the ESP profile.

> [!TIP]
> For Configuration Manager admins, an ESP is similar and analogous to Configuration Manager client settings.

For more information on the Enrollment Status Page (ESP), see the following articles:

- [Windows Autopilot Enrollment Status Page](/mem/autopilot/enrollment-status)
- [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status)

## Create and assign user-driven Azure AD join Autopilot profile

While the ESP controls what is shown during device and user setup and specifies how soon a user can use their device, the Autopilot profile specifies how the device is configured during Windows Setup, or during OOBE.

When creating an Autopilot profile for the user-driven scenario, devices with this Autopilot profile are associated with the user enrolling the device. User credentials are required to enroll the device.

To create an user-driven Azure AD join Autopilot profile, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select > **Windows enrollment**

5. Under **Windows Autopilot Deployment Program**, select **Deployment Profiles**

6. In the **Windows Autopilot deployment profiles** screen, select  **Create Profile** > **Windows PC**.

7. In the **Basics** page of the **Create profile** screen, type a **Name** and optional **Description** for the Autopilot profile, and then select **Next**.

    > [!NOTE]
    >
    > For the purposes of this tutorial, leave the option **Convert all targeted devices to Autopilot** set to **No**. This tutorial is mainly concentrating on new devices while this option mainly covers existing devices.

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **User-driven**.

      - For **Join to Azure AD as**, select **Azure AD joined**.

      - For **Microsoft Software License Terms**, select **Hide** to skip the EULA page.

      - For **Privacy settings**, select **Hide** to skip the privacy settings.

      - For **Hide change account options**: Choose **Hide**.

      - For **User account type**, choose the desired account type for the user (**Administrator** or **Standard** user). If **Administrator** is chosen, the user will added to the local Admin group.

      - For **Allow pre-provisioned deployment**, select **No**..

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

      - For **Apply device name template**, select **No**. Alternatively, **Yes** can be chosen to apply a device name templated. Be aware of the following if the name template is selected to **Yes**:

        - Names must be 15 characters or less, and can have letters, numbers, and hyphens.
        - Names can't be all numbers.
        - Use the [%SERIAL% macro](/windows/client-management/mdm/accounts-csp) to add a hardware-specific serial number.
        - Use the [%RAND:x% macro](/windows/client-management/mdm/accounts-csp) to add a random string of numbers, where x equals the number of digits to add.

        > [!NOTE]
        >
        > The above settings have been selected to minimize needed user interaction during device setup. However, some of the settings that are hidden can instead be shown as desired.
        >
        > Also note that if language and keyboard settings are shown instead of hidden, they require ethernet connectivity. Wi-fi connectivity isn't supported because of the requirement to choose a language, locale, and keyboard to initiate the Wi-fi connection.

9. Once the options in the **Out-of-box experience (OOBE)** page are configured as desired, select **Next**.

10. On the **Assignments** page, under **Included groups**, choose **Add groups**.

11. In the **Select groups to include** page, choose the device group(s) to assign this Autopilot profile to. This is normally the device group created in the step [Create device group](#create-device-group) above. Once done, select **Select**.

12. In the **Create profile** page, select **Next**.

13. On the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the Autopilot profile.

For more information on creating and assigning Autopilot profiles, see the following articles:

- [Configure Autopilot profiles](/mem/autopilot/profiles)


### Verify device has an Autopilot profile assigned to it

Before deploying a device, ensure that an Autopilot profiles has been assigned to it by checking under **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program** where you should see the profile status change from "Unassigned" to "Assigning" and finally to "Assigned."

> [!NOTE]
> Intune will periodically check for new devices in the assigned groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include AAD groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time will vary depending on all the factors and variables involved in a specific scenario.<br>
<br>

## Assign Autopilot device to a user (optional)

A device that has been registered as an Autopilot device can be also be assigned to a user. If an Autopilot device is assigned to a user, then any user policies and application installs assigned to that user will be applied to the device during the Autopilot process.

To assign an Autopilot device to a user, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

4. In the **Windows | Windows devices** screen, select **Windows enrollment**.

5. Under **Windows Autopilot Deployment Program**, select **Devices**.

6. In the **Windows Autopilot devices** screen, locate the device to assign a user to.

7. Once the desired device has been located, select the box to the left of the device, making sure that there is check mark in the box, and then select **Assign user** in the toolbar above.

8. In the **Select user** page, find and select a user for the device, and then select **Select**. If necessary, use the **Search** box to find the desired user.

    > [!NOTE]
    >
    > The selected user must be an Azure user licensed to use Intune.

9. In the Autopilot device's property page that automatically opens on the right hand side, under **User friendly name**, the user's name should automatically populate based on what is already in Azure AD. However, if the value is empty or a different friendly name is desired, enter the desired friendly name for the user under **User friendly name** and then select **Save**.

10. The user assignment can be verified by selecting the Autopilot device in the **Windows Autopilot devices** screen. Once the Autopilot device is selected, it will highlight and the Autopilot device's property page will automatically open on the right hand side. The assigned user will be listed under **User** and **User friendly name**.

> [!TIP]
>
> For Configuration Manager admins, assigning a user to a device is similar to user device affinity in Configuration Manager.

For more information on assigning a user to an Autopilot device, see the following articles:

- [Assign a user to a specific Autopilot device](/mem/autopilot/enrollment-autopilot#assign-a-user-to-a-specific-autopilot-device)

### Assigning Autopilot device to a user via hardware hash CSV file

Instead of manually assigning a user to an Autopilot device in the Autopilot device's properties, a user can be assigned to the Autopilot device back when the device was imported into Autopilot during the [Register devices as Autopilot devices](#register-devices-as-autopilot-devices) step. This can be done by editing the hardware hash CSV file and adding the **Assigned User** column after the **Hardware Hash** column. The user's User Principal Name (UPN) should then be added as a value under the **Assigned User** column.

> [!IMPORTANT]
>
> Use a plain-text editor such as **Notepad** to edit the CSV file. Don't use Microsoft Excel. Editing the CSV file in Excel won't generate a proper usable file for importing into Intune.

For more information on editing the CSV file to add an assigned user to the Autopilot device, see the following article:

[Manually register devices with Windows Autopilot: Ensure that the CSV file meets requirements](/mem/autopilot/add-devices#ensure-that-the-csv-file-meets-requirements)

## More info

- [Windows Autopilot user-driven mode](/mem/autopilot/user-driven)
