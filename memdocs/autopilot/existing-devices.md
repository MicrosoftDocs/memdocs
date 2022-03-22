---
title: Windows Autopilot Deployment for existing devices
description: Modern desktop deployment with Windows Autopilot enables you to easily deploy the latest version of Windows to your existing devices.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.technology: windows
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 03/21/2022
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: how-to
---

# Windows Autopilot Deployment for existing devices

**Applies to**

- Windows 11
- Windows 10

Modern desktop deployment with Windows Autopilot helps you easily deploy the latest version of Windows to your existing devices. The apps you need for work can be automatically installed. Your work profile is synchronized, so you can resume working right away.

This article describes how to convert existing Windows 8.1 domain-joined computers to Windows 10 or Windows 11, and joined to either Azure Active Directory (Azure AD) or Active Directory (hybrid Azure AD join) by using Windows Autopilot.

Converting all targeted devices to Autopilot isn't supported for transforming a hybrid Azure AD device into an Azure AD Autopilot device.

> [!NOTE]
> Windows Autopilot for existing devices only supports user-driven Azure AD and hybrid Azure AD profiles. Self-deploying and pre-provisioning profiles aren't supported.

## Prerequisites

- A currently supported version of Microsoft Endpoint Configuration Manager current branch.
- The [Windows ADK](/windows-hardware/get-started/adk-install)
  For more information, see [Support for the Windows ADK in Configuration Manager](../configmgr/core/plan-design/configs/support-for-windows-adk.md).
- Assigned Microsoft Intune licenses
- Azure AD Premium
- A supported version of Windows 10 or Windows 11 imported into Configuration Manager as an OS image

## Configure the Enrollment Status Page (optional)

If you want, you can set up an [enrollment status page](enrollment-status.md) (ESP) for Autopilot using Intune.

1. Open the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com).

1. Go to **Intune > Device enrollment > Windows enrollment** and [Set up the Enrollment Status Page](../intune/enrollment/windows-enrollment-status.md).

    :::image type="content" source="images/esp-config.png" alt-text="Enrollment status page policy page in Intune.":::

1. Go to **Azure Active Directory > Mobility (MDM and MAM) > Microsoft Intune** and [enable Windows automatic enrollment](../intune/enrollment/windows-enroll.md#enable-windows-automatic-enrollment). Configure the MDM user scope for some or all users.

    :::image type="content" source="images/mdm-config.png" alt-text="Configure MDM enrollment in Azure.":::

## Install required modules

> [!TIP]
> To run the following commands on a computer running Windows Server 2012/2012 R2 or Windows 7/8.1, first download and install the [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616).

1. On an internet-connected Windows PC or server, open an elevated Windows PowerShell command window.

1. Enter the following commands to install the necessary modules:

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module AzureAD -Force
    Install-Module WindowsAutopilotIntune -Force
    Install-Module Microsoft.Graph.Intune -Force
    ```

1. Enter the following commands and provide Intune administrative credentials:

    Make sure the user account you specify has sufficient administrative rights.

    ```powershell
    Connect-MSGraph
    ```

    Windows requests the user and password for your account with a standard Azure AD form. Type your username and password, and then select **Sign in**.

    :::image type="content" source="images/pwd.png" alt-text="Windows form to sign in to your Azure AD account.":::

    If it's the first time you've used Intune Graph APIs, you'll be prompted to enable Microsoft Intune PowerShell read and write permissions. To enable these permissions, select **Consent on behalf or your organization** and then **Accept**.

## Get Autopilot profiles for existing devices

Get all the Autopilot profiles available in your Intune tenant, and display them in JSON format:

```powershell
Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
```

See the following sample output:

```powershell
PS C:\> Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON
{
    "CloudAssignedTenantId": "1537de22-988c-4e93-b8a5-83890f34a69b",
    "CloudAssignedForcedEnrollment": 1,
    "Version": 2049,
    "Comment_File": "Profile Autopilot Profile",
    "CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"ForcedEnrollment\":1,\"CloudAssignedTenantDomain\":\"M365x373186.onmicrosoft.com\"}}",
    "CloudAssignedTenantDomain": "M365x373186.onmicrosoft.com",
    "CloudAssignedDomainJoinMethod": 0,
    "CloudAssignedOobeConfig": 28,
    "ZtdCorrelationId": "7F9E6025-1E13-45F3-BF82-A3E8C5B59EAC"
}
```

Each profile is encapsulated within braces (`{ }`). The previous example displays a single profile.

### JSON file properties

#### Version

_(Number, optional)_

The version number that identifies the format of the JSON file. <!-- For Windows 10 1809, the version specified must be 2049. -->

#### CloudAssignedTenantId

_(GUID, required)_

The Azure AD tenant ID that should be used. This property is the GUID for the tenant, and can be found in properties of the tenant. The value shouldn't include braces.

#### CloudAssignedTenantDomain

_(String, required)_

The Azure AD tenant name that should be used. For example: `tenant.onmicrosoft.com`.

#### CloudAssignedOobeConfig

_(Number, required)_

This property is a bitmap that shows which Autopilot settings were configured.

- 1: SkipCortanaOptIn
- 2: OobeUserNotLocalAdmin
- 4: SkipExpressSettings
- 8: SkipOemRegistration
- 16: SkipEula

#### CloudAssignedDomainJoinMethod

_(Number, required)_

This property specifies whether the device should join Azure AD or Active Directory (hybrid Azure AD join).

- 0: Azure AD-joined
- 1: Hybrid Azure AD-joined

#### CloudAssignedForcedEnrollment

_(Number, required)_

Specifies that the device should require Azure AD join and MDM enrollment.

- 0: Not required
- 1: required

#### ZtdCorrelationId

_(GUID, required)_

A unique GUID (without braces) that's provided to Intune as part of the registration process. This ID is included in the enrollment message as the `OfflineAutoPilotEnrollmentCorrelator`. This attribute is present only if enrollment happens on a device registered with Zero Touch Provisioning via offline registration.

#### CloudAssignedAadServerData

_(Encoded JSON string, required)_

An embedded JSON string used for branding. It requires that you enable Azure AD organization branding.

For example:

`"CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"CloudAssignedTenantDomain\":\"tenant.onmicrosoft.com\"}}`

#### CloudAssignedDeviceName

_(String, optional)_

The name that's automatically assigned to the computer. This name follows the naming pattern convention configured in the Intune Autopilot profile. You can also specify an explicit name to use.

## Create the JSON file

Save the Autopilot profile as a JSON file in ASCII or ANSI format. Windows PowerShell defaults to Unicode format. So, if you redirect output of the commands to a file, also specify the file format. The following PowerShell example saves the file in ASCII format, creates a directory, and saves the profile:

```powershell
Get-AutopilotProfile | ConvertTo-AutopilotConfigurationJSON | Out-File c:\Autopilot\AutopilotConfigurationFile.json -Encoding ASCII
```

> [!IMPORTANT]
> The file name has to be `AutopilotConfigurationFile.json` and encoded as ASCII or ANSI.

You can also save the profile to a text file and edit in Notepad. In Notepad, when you choose **Save as**, select the save as type: **All Files**, and then choose **ANSI** for the **Encoding**.

:::image type="content" source="images/notepad.png" alt-text="Save as ANSI encoding in Notepad.":::

After you save the file, move it to a location for a Microsoft Endpoint Configuration Manager package source.

> [!IMPORTANT]
> You can use multiple JSON profile files, but each one must be named `AutopilotConfigurationFile.json`. This requirement is for OOBE to follow the Autopilot experience.
>
> If you save the file with Unicode or UTF-8 encoding, or save it with a different file name, the Windows OOBE won't follow the Autopilot experience.

## Create a package containing the JSON file

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.

1. On the ribbon, select **Create Package**.

1. In the Create Package and Program Wizard, enter the following details for the package:

    - _Name_: **Autopilot for existing devices config**
    - Select **This package contains source files**
    - _Source folder_: Specify the UNC network path that contains the `AutopilotConfigurationFile.json` file

    For more information, see [Packages and programs in Configuration Manager](../configmgr/apps/deploy-use/packages-and-programs.md).

1. For the program, select the _Program Type_: **Don't create a program**

1. Complete the wizard.

> [!NOTE]
> If you change user-driven Autopilot profile settings in Intune at a later date, make sure to update the JSON file. Then redistribute the associated Configuration Manager package.

## Create a target collection

> [!NOTE]
> You can also choose to reuse an existing collection.

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.

1. On the ribbon, select **Create**, and then choose **Create Device Collection**.

1. In the Create Device Collection Wizard, enter the following **General** details:

    - _Name_: **Autopilot for existing devices collection**
    - _Comment_: Add an optional comment to further describe the collection
    - _Limiting collection_: **All Systems**

      > [!NOTE]
      > You can optionally choose to use an alternative collection for the limiting collection. The device to be upgraded must be running the Configuration Manaber client in the collection that you select.

1. On the **Membership Rules** page, select **Add Rule**. Specify either a direct or query-based collection rule to add the target Windows 8.1 devices to the new collection.

    For example, if the hostname of the computer to be wiped and reloaded is `PC-01` and you want to use **Name** as the attribute:

    1. Select **Add Rule**, select **Direct Rule** to open the Create Direct Membership Rule Wizard, and select **Next** on the Welcome page.
    1. On the **Search for Resources** page, enter **PC-01** as the **Value**.

        :::image type="content" source="images/pc-01a.png" alt-text="Enter PC-01 as the name to locate for a collection direct membership rule.":::

    1. Select **Next**, and select **PC-01** in the **Resources**.

        :::image type="content" source="images/pc-01b.png" alt-text="Select PC-01 as the resource to add to the collection.":::

1. Complete the wizard with the default settings.

For more information, see [How to create collections in Configuration Manager](../configmgr/core/clients/manage/collections/create-collections.md).

## Create a task sequence

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems** and select the **Task Sequences** node.

1. On the **Home** ribbon, select **Create Task Sequence**.

1. Select **Install an existing image package**.

1. In the Create Task Sequence Wizard enter the following details:

    - _Task sequence name_: **Autopilot for existing devices**
    - _Boot Image_: Select an available boot image
    - Select an **Image package** and **Image Index**
    - Enable the option to **Partition and format the target computer before installing the operating system**
    - On the Configure Network page, choose **Join a workgroup** and specify `workgroup` as the **Workgroup**.

        > [!IMPORTANT]
        > The Autopilot for existing devices task sequence will run the **Prepare Windows for capture** action which uses the System Preparation Tool (sysprep). This action fails if the device is joined to a domain.
        >
        > Sysprep runs with the `/Generalize` parameter, which on Windows 10 version 1909 deletes the Autopilot profile file. The device then boots into the OOBE phase instead of Autopilot. To fix this issue, see [Windows Autopilot - known issues](known-issues.md).

    - On the State Migration page, disable all options to capture settings.

        > [!NOTE]
        > Because the Autopilot for existing devices task sequence completes while in Windows PE, User State Migration Toolkit (USMT) data migration isn't supported as there's no way to restore the user state into the new OS. Also, USMT doesn't support Azure AD-joined devices.

    For more information on creating the task sequence, including information on other wizard options, see [Create a task sequence to install an OS](../configmgr/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).

1. Complete the wizard.

## Configure the task sequence

1. Select the **Autopilot for existing devices** task sequence, and in the ribbon select **Edit**.

1. In the Task Sequence Editor, under the **Install Operating System** group, select the **Apply Windows Settings** step.

1. Select **Add**, then choose **New Group**.

1. Change the group **Name** from **New Group** to **Autopilot for existing devices config**.

1. Select **Add**, select **General**, and then choose **Run Command-line**.

1. Verify that the new **Run Command-line** step is nested under the **Autopilot for existing devices config** group.

1. Change the **Name** to **Apply Autopilot for existing devices config file**, and paste the following string as the **Command line** text:

    ```command
    cmd.exe /c xcopy AutopilotConfigurationFile.json %OSDTargetSystemDrive%\windows\provisioning\Autopilot\ /c
    ```

    `AutopilotConfigurationFile.json` must be the name of the JSON file present in the package that was created earlier.

     > [!IMPORTANT]
     > The `AutopilotConfigurationFile.json` file persists on the device across all future device resets. The only way for the JSON file to be fully removed is to do a clean install of the OS.

1. In the **Apply Autopilot for existing devices config file** step, select the **Package** > **Browse**.

1. Select the **Autopilot for existing devices config** package, and select **OK**.

    :::image type="content" source="images/ap-ts-1.png" alt-text="Editing the Autopilot task sequence and viewing the properties of the Run Command line step.":::

1. Under the **Setup Operating System** group, select the **Setup Windows and Configuration Manager** task.

1. Select **Add** and then choose **New Group**.

1. Change **Name** from **New Group** to **Prepare Device for Autopilot**

1. Verify that the **Prepare Device for Autopilot** group is the last step in the task sequence. Use the **Move Down** button if necessary.

1. Select the **Prepare device for Autopilot** group. Select **Add**, select **Images**, and then choose **Prepare ConfigMgr Client for Capture**. There are no settings to configure in this step.

1. Add a second step to the group. Select **Add**, select **Images**, and then choose **Prepare Windows for Capture**. Use the following settings in this step:

    - Disable the option to **Automatically build mass storage driver list**
    - Disable the option to **Don't reset activation flag**

1. Select **OK** to close the Task Sequence Editor and save the changes.

For more information, see [Use the task sequence editor](../configmgr/osd/understand/task-sequence-editor.md) and [Task sequence steps](../configmgr/osd/understand/task-sequence-steps.md).

> [!NOTE]
> On Windows 10 version 1909, the **Prepare Windows for Capture** step deletes the `AutopilotConfigurationFile.json` file. For more information and a workaround, see [Windows Autopilot - known issues](known-issues.md).

## Distribute content to distribution points

Next distribute all content required for the task sequence to distribution points.

1. Select the **Autopilot for existing devices** task sequence, and in the ribbon select **Distribute Content**.

1. On the **Specify the content distribution** page, select **Add** to specify either a **Distribution Point** or **Distribution Point Group**.

1. Specify content destinations that let the devices get the content.

1. When you're finished specifying content distribution, complete the wizard.

For more information, see [Manage task sequences to automate tasks](../configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks.md).

## Deploy the Autopilot task sequence

1. Select the **Autopilot for existing devices** task sequence, and in the ribbon select **Deploy**.

1. In the Deploy Software Wizard, specify the following details:

    - **General**

      - _Task Sequence_: **Autopilot for existing devices**

      - _Collection_: **Autopilot for existing devices collection**

    - **Deployment Settings**

      - _Action_: **Install**.

      - _Purpose_: **Available**. You can optionally select **Required** instead of **Available**. A required purpose isn't recommended during testing.

      - _Make available to the following_: **Only Configuration Manager Clients**.

        > [!NOTE]
        > Choose the option here that is relevant for the context of your test. If the target client doesn't have the Configuration Manager agent or Windows installed, you must select an option that includes PXE or Boot Media.

    - **Scheduling**

      - Set a time for when this deployment will become available

    - **User Experience**

      - Select **Show Task Sequence progress**

    - **Distribution Points**

      - _Deployment options_: **Download content locally when needed by the running task sequence**

1. Complete the wizard.

## Complete the deployment process

1. On the target Windows 8.1 device, go to the **Start** menu, type `Software Center`, and open it.

2. In the Software Library, under **Operating Systems**, select **Autopilot for existing devices**, and then select **Install**. For example:

    :::image type="content" source="images/sc.png" alt-text="Autopilot for existing devices task sequence in Software Center.":::

    :::image type="content" source="images/sc1.png" alt-text="Software Center notice to confirm you want to upgrade the OS on this computer.":::

The task sequence runs and does the following actions:

1. Download content
1. Restart the device
1. Format the drive
1. Install Windows from the specified OS image

    :::image type="content" source="images/up-1.PNG" alt-text="Task sequence installation progress applying image.":::

1. Prepare for Autopilot

    :::image type="content" source="images/up-2.PNG" alt-text="Task sequence installation progress running sysprep.":::

1. After the task sequence completes, the device boots into OOBE for the Autopilot experience:

    :::image type="content" source="images/up-3.PNG" alt-text="Autopilot experience prompting for user account.":::

> [!NOTE]
> If you need to join devices to Active Directory for hybrid Azure AD join scenario, create a **Domain Join** device configuration profile. Target the profile to **All Devices**, since there's no Azure AD device object for the computer to do group-based targeting. For more information, see [User-driven mode for hybrid Azure Active Directory join](user-driven.md#user-driven-mode-for-hybrid-azure-ad-join).

## Register the device for Windows Autopilot

Devices provisioned with Autopilot only receive the guided OOBE Autopilot experience on first boot.

After you update Windows on an existing device, make sure to register the device so it has the Autopilot experience when the PC resets. You can enable automatic registration for an assigned group using the **Convert all targeted devices to Autopilot** setting. For more information, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile).

Also see [Adding devices to Windows Autopilot](add-devices.md).

## How to speed up the deployment process

To remove around 20 minutes from the deployment process, see Michael Niehaus's blog with instructions for [Speeding up Windows Autopilot for existing devices](/archive/blogs/mniehaus/speeding-up-windows-autopilot-for-existing-devices).
