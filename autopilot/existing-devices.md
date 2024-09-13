---
title: Windows Autopilot for existing devices
description: Modern desktop deployment with Windows Autopilot enables easily deploying the latest version of Windows to existing devices.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/27/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot deployment for existing devices

Modern desktop deployment with Windows Autopilot helps easily deploy the latest version of Windows to existing devices. Apps used by the organization can be automatically installed. If Windows user data is managed with OneDrive for work or school, data is synchronized, so users can resume working right away.

**Windows Autopilot for existing devices** allows reimaging and provisioning a Windows device for Autopilot user-driven mode using a single, native Configuration Manager task sequence. The existing device can be on-premises domain-joined. The end result is a Windows device joined to either Microsoft Entra ID or Active Directory (Microsoft Entra hybrid join).

> [!NOTE]
>
> The JSON file for Windows Autopilot for existing devices only supports user-driven Microsoft Entra ID and user-driven hybrid Microsoft Entra Autopilot profiles. Self-deploying and pre-provisioning Autopilot profiles aren't supported with JSON files due to these scenarios requiring TPM attestation.
>
> However, during the Windows Autopilot for existing devices deployment, if the following conditions are true:
>
> - Device is already a Windows Autopilot device before the deployment begins
> - Device has an Autopilot profile assigned to it
>
> then the assigned Autopilot profile takes precedence over the JSON file installed by the task sequence. In this scenario, if the assigned Autopilot profile is either a self-deploying or pre-provisioning Autopilot profile, then the self-deploying and pre-provisioning scenarios are supported.

> [!TIP]
>
> Using Autopilot for existing devices could be used as a method to convert existing hybrid Microsoft Entra devices into Microsoft Entra devices. Using the setting **Convert all targeted devices to Autopilot** in the Autopilot profile doesn't automatically convert existing hybrid Microsoft Entra device in the assigned groups into a Microsoft Entra device. The setting only registers the devices in the assigned groups for the Autopilot service.

## Requirements

- A currently supported version of Microsoft Configuration Manager current branch.

- Assigned Microsoft Intune licenses.

- Microsoft Entra ID P1 or P2.

- A supported version of Windows imported into Configuration Manager as an [OS image](/mem/configmgr/osd/get-started/manage-operating-system-images).

- The [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616) is required for Windows Server 2012/2012 R2 when running the PowerShell commands and scripts that [installs the required modules](#install-required-modules).

- Enrollment restrictions aren't configured to block personal devices. For more information, see [What are enrollment restrictions?: Blocking personal Windows devices](/mem/intune/enrollment/enrollment-restrictions-set#blocking-personal-windows-devices). <!-- INADO-27343099 -->

## Configure the Enrollment Status Page (optional)

If desired, an [enrollment status page](enrollment-status.md) (ESP) for Autopilot can be set up using Intune.

1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Go to **Devices** > **Device onboarding** | **Enrollment**. Make sure **Windows** is selected at the top and then under **Windows Autopilot**, select **Enrollment Status Page** and [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status).

1. Go to **Microsoft Entra ID** > **Manage** | **Mobility (MDM and WIP)** > **Microsoft Intune** and [enable Windows automatic enrollment](/mem/intune/enrollment/windows-enroll#enable-windows-automatic-enrollment). Configure the MDM user scope for some or all users.

## Install required modules

> [!NOTE]
>
> The PowerShell code snippets in this section were updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when they're first used. It was also updated to force using an updated version of the WindowsAutoPilot module. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

1. On an internet-connected Windows PC or server, open an elevated Windows PowerShell command window.

1. Enter the following commands to install and import the necessary modules:

    ```powershell
    Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    Install-Module -Name WindowsAutopilotIntune -MinimumVersion 5.4.0 -Force
    Install-Module -Name Microsoft.Graph.Groups -Force
    Install-Module -Name Microsoft.Graph.Authentication -Force
    Install-Module -Name Microsoft.Graph.Identity.DirectoryManagement -Force

    Import-Module -Name WindowsAutopilotIntune -MinimumVersion 5.4
    Import-Module -Name Microsoft.Graph.Groups
    Import-Module -Name Microsoft.Graph.Authentication
    Import-Module -Name Microsoft.Graph.Identity.DirectoryManagement
    ```

1. Enter the following commands and provide Intune administrative credentials:

    Make sure the specified user account has sufficient administrative rights.

    ```powershell
    Connect-MgGraph -Scopes "Device.ReadWrite.All", "DeviceManagementManagedDevices.ReadWrite.All", "DeviceManagementServiceConfig.ReadWrite.All", "Domain.ReadWrite.All", "Group.ReadWrite.All", "GroupMember.ReadWrite.All", "User.Read"
    ```

    Windows requests the username and password for the account with a standard Microsoft Entra ID form. Type the username and password, and then select **Sign in**.

    :::image type="content" source="images/pwd.png" alt-text="Windows form to sign in to a Microsoft Entra account.":::

    The first time Intune Graph APIs are used on a device, it prompts to enable Microsoft Intune PowerShell read and write permissions. To enable these permissions, select **Consent on behalf or your organization** and then **Accept**.

## Get Autopilot profiles for existing devices

Get all the Autopilot profiles available in the Intune tenant, and display them in JSON format:

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

| Property | Type | Required | Description |
| --- | --- | --- | --- |
| **Version** | Number | Optional | The version number that identifies the format of the JSON file. |
| **CloudAssignedTenantId** | GUID | Required | The Microsoft Entra tenant ID that should be used. This property is the GUID for the tenant, and can be found in properties of the tenant. The value shouldn't include braces. |
| **CloudAssignedTenantDomain** | String | Required | The Microsoft Entra tenant name that should be used. For example: `tenant.onmicrosoft.com`. |
| **CloudAssignedOobeConfig** | Number | Required | This property is a bitmap that shows which Autopilot settings were configured.<br><br><ul><li>1: SkipCortanaOptIn</li><li>2: OobeUserNotLocalAdmin</li><li>4: SkipExpressSettings</li><li>8: SkipOemRegistration</li><li>16: SkipEula</li></ul> |
| **CloudAssignedDomainJoinMethod** | Number | Required | This property specifies whether the device should join Microsoft Entra ID or Active Directory (Microsoft Entra hybrid join).<br><br><ul><li>0: Microsoft Entra joined</li><li>1: Microsoft Entra hybrid joined</li></ul> |
| **CloudAssignedForcedEnrollment** | Number | Required | Specifies that the device should require Microsoft Entra join and MDM enrollment.<br><br><ul><li>0: Not required</li><li>1: required</li></ul>|
| **ZtdCorrelationId** | GUID | Required | A unique GUID (without braces) provided to Intune as part of the registration process. This ID is included in the enrollment message as the `OfflineAutopilotEnrollmentCorrelator`. This attribute is present only if enrollment happens on a device registered with Zero Touch Provisioning via offline registration. |
| **CloudAssignedAadServerData** | Encoded JSON string | Required |An embedded JSON string used for branding. It requires enabling Microsoft Entra organization branding. For example:<br><br>`"CloudAssignedAadServerData": "{\"ZeroTouchConfig\":{\"CloudAssignedTenantUpn\":\"\",\"CloudAssignedTenantDomain\":\"tenant.onmicrosoft.com\"}}` |
| **CloudAssignedDeviceName** | String | Optional | The name automatically assigned to the computer. This name follows the naming pattern convention configured in the Intune Autopilot profile. An explicit name can also be specified. |

## Create the JSON file

Save the Autopilot profile as a JSON file in ASCII or ANSI format. Windows PowerShell defaults to Unicode format. If redirecting output of the commands to a file, also specify the file format. The following PowerShell example saves the file in ASCII format. The Autopilot profiles appear in a subfolder under the folder specified by the `$targetDirectory` variable. By default, the `$targetDirectory` variable is `C:\AutoPilot`, but it can be changed to another location if desired. The subfolder has the name of the Autopilot profile from Intune. If there are multiple Autopilot profiles, each profile has its own subfolder. In each folder, there's a JSON file named **`AutopilotConfigurationFile.json`**

```powershell
Connect-MgGraph -Scopes "Device.ReadWrite.All", "DeviceManagementManagedDevices.ReadWrite.All", "DeviceManagementServiceConfig.ReadWrite.All", "Domain.ReadWrite.All", "Group.ReadWrite.All", "GroupMember.ReadWrite.All", "User.Read"
$AutopilotProfile = Get-AutopilotProfile
$targetDirectory = "C:\Autopilot"
$AutopilotProfile | ForEach-Object {
    New-Item -ItemType Directory -Path "$targetDirectory\$($_.displayName)"
    $_ | ConvertTo-AutopilotConfigurationJSON | Set-Content -Encoding Ascii "$targetDirectory\$($_.displayName)\AutopilotConfigurationFile.json"
}
```

> [!TIP]
>
> When the PowerShell cmdlet **Out-File** is used to redirect the JSON output to a file, it uses Unicode encoding by default. This cmdlet might also truncate long lines. Use the **Set-Content** cmdlet with the `-Encoding ASCII` parameter to set the proper text encoding.

> [!IMPORTANT]
>
> The file name has to be `AutopilotConfigurationFile.json` and encoded as ASCII or ANSI.

The profile can also be saved to a text file and edit in Notepad. In Notepad, when choosing **Save as**, select the save as type: **All Files**, and then select **ANSI** for the **Encoding**.

:::image type="content" source="images/notepad.png" alt-text="Save as ANSI encoding in Notepad.":::

After saving the file, move it to a location for a Microsoft Configuration Manager package source.

> [!IMPORTANT]
>
> The configuration file can only contain one profile. Multiple JSON profile files can be used, but each one must be named `AutopilotConfigurationFile.json`. This requirement is for OOBE to follow the Autopilot experience. To use more than one Autopilot profile, create separate Configuration Manager packages.
>
> Windows OOBE doesn't follow the Autopilot experience if the file is saved with one of the following criteria:
>
> - Unicode encoding.
> - UTF-8 encoding.
> - A file name other than `AutopilotConfigurationFile.json`.

## Create a package containing the JSON file

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.

1. On the ribbon, select **Create Package**.

1. In the Create Package and Program Wizard, enter the following details for the package:

    - *Name*: **Autopilot for existing devices config**
    - Select **This package contains source files**
    - *Source folder*: Specify the UNC network path that contains the `AutopilotConfigurationFile.json` file

    For more information, see [Packages and programs in Configuration Manager](/mem/configmgr/apps/deploy-use/packages-and-programs).

1. For the program, select the *Program Type*: **Don't create a program**

1. Complete the wizard.

> [!NOTE]
>
> If the user-driven Autopilot profile settings in Intune are changed at a later date, make sure to recreate and update the JSON file. After updating the JSON file, redistribute the associated Configuration Manager package.

## Create a target collection

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.

1. On the ribbon, select **Create**, and then select **Create Device Collection**. An existing collection can also be used. If using an existing collection, proceed to the [Create a task sequence](#create-a-task-sequence) section.

1. In the Create Device Collection Wizard, enter the following **General** details:

    - *Name*: **Autopilot for existing devices collection**
    - *Comment*: Add an optional comment to further describe the collection
    - *Limiting collection*: **All Systems** or if desired, an alternate collection.

1. On the **Membership Rules** page, select **Add Rule**. Specify either a direct or query-based collection rule to add the target Windows devices to the new collection.

    For example, if the hostname of the computer to be wiped and reloaded is `PC-01`, and **Name** is being used as the attribute:

    1. Select **Add Rule**, select **Direct Rule** to open the Create Direct Membership Rule Wizard, and select **Next** on the Welcome page.

    1. On the **Search for Resources** page, enter **PC-01** as the **Value**.

    1. Select **Next**, and select **PC-01** in the **Resources**.

1. Complete the wizard with the default settings.

For more information, see [How to create collections in Configuration Manager](/mem/configmgr/core/clients/manage/collections/create-collections).

## Create a task sequence

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems** and select the **Task Sequences** node.

1. In the **Home** ribbon, select **Create Task Sequence**.

1. In the **Create new task sequence** page, select the option to **Deploy Windows Autopilot for existing devices**.

1. In the **Task sequence information** page, specify the following information:

    - A name for the task sequence. For example, **Autopilot for existing devices**.
    - Optionally add a description to better describe the task sequence.
    - Select a boot image. For more information on supported boot image versions, see [Support for the Windows ADK in Configuration Manager](/mem/configmgr/core/plan-design/configs/support-for-windows-adk).

1. In the **Install Windows** page, select the Windows **Image package**. Then configure the following settings:

    - **Image index**: Select either Enterprise, Education, or Professional, as required by the organization.

    - Enable the option to **Partition and format the target computer before installing the operating system**.

    - **Configure task sequence for use with Bitlocker**: If this option is enabled, the task sequence includes the steps necessary to enable BitLocker.

    - **Product key**: If a product key needs to be specified for Windows activation, enter it here.

    - Select one of the following options to configure the local administrator account in Windows:
        - **Randomly generate the local administrator password and disable the account on all support platforms (recommended)**
        - **Enable the account and specify the local administrator password**

1. In the **Install the Configuration Manager client** page, add any necessary Configuration Manager client installation properties for the environment. For example, since the device is a Workgroup device and not domain joined during the Windows Autopilot for existing devices task sequence, the [SMSMP](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmp) or [SMSMPLIST](/mem/configmgr/core/clients/deploy/about-client-installation-properties#smsmplist) parameters might be needed to run certain tasks such as the **Install Application** or **Install Software Updates** tasks.

1. The **Include updates** page selects by default the option to **Do not install any software updates**.

1. In the **Install applications** page, applications to install during the task sequence can be selected. However, Microsoft recommends that to mirror the signature image approach with this scenario. After the device provisions with Autopilot, apply all applications and configurations from Microsoft Intune or Configuration Manager co-management. This process provides a consistent experience between users receiving new devices and those using Windows Autopilot for existing devices.

1. In the **System Preparation** page, select the package that includes the Autopilot configuration file. By default, the task sequence restarts the computer after it runs Windows Sysprep. The option to **Shutdown computer after this task sequence completes** can also be selected. This option allows preparation of a device and then delivery to a user for a consistent Autopilot experience.

1. Complete the wizard.

The Windows Autopilot for existing devices task sequence results in a device joined to Microsoft Entra ID.

> [!NOTE]
>
> For Windows Autopilot for existing devices task sequence, the **Create Task Sequence Wizard** purposely skips configuring and adding the **Apply Network Settings** task. If the **Apply Network Settings** task isn't specified in a task sequence, it uses Windows default behavior, which is to join a workgroup.
>
> The Windows Autopilot for existing devices task sequence runs the **Prepare Windows for capture** step, which uses the Windows System Preparation Tool (Sysprep). If the device is joined to a domain, Sysprep fails, so therefore the Windows Autopilot for existing devices task sequence joins a workgroup. For this reason, it isn't necessary to add the **Apply Network Settings** task to a Windows Autopilot for existing devices task sequence.

For more information on creating the task sequence, including information on other wizard options, see [Create a task sequence to install an OS](/mem/configmgr/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

If the task sequence is viewed, it's similar to the default task sequence to apply an existing OS image. This task sequence includes the following extra steps:

- **Apply Windows Autopilot configuration**: This step applies the Autopilot configuration file from the specified package. It's not a new type of step, it's a **Run Command Line** step to copy the file.

- **Prepare Windows for Capture**: This step runs Windows Sysprep, and has the setting to **Shutdown the computer after running this action**. For more information, see [Prepare Windows for Capture](/mem/configmgr/osd/understand/task-sequence-steps#prepare-windows-for-capture).

For more information on editing the task sequence, see [Use the task sequence editor](/mem/configmgr/osd/understand/task-sequence-editor) and [Task sequence steps](/mem/configmgr/osd/understand/task-sequence-steps).

> [!NOTE]
>
> The **Prepare Windows for Capture** step deletes the `AutopilotConfigurationFile.json` file. For more information and a workaround, see [Modify the task sequence to account for Sysprep command line configuration](tutorial/existing-devices/create-autopilot-task-sequence.md#modify-the-task-sequence-to-account-for-sysprep-command-line-configuration) and [Windows Autopilot - known issues: Windows Autopilot for existing devices doesn't work](known-issues.md#windows-autopilot-for-existing-devices-doesnt-work).

To make sure the user's data is backed up before the Windows upgrade, use OneDrive for work or school [known folder move](/onedrive/redirect-known-folders).

## Distribute content to distribution points

Next distribute all content required for the task sequence to distribution points.

1. Select the **Autopilot for existing devices** task sequence, and in the ribbon select **Distribute Content**.

1. On the **Specify the content destination** page, select **Add** to specify either a **Distribution Point** or **Distribution Point Group**.

1. Specify content destinations that let the devices get the content.

1. After specifying content distribution, complete the wizard.

For more information, see [Manage task sequences to automate tasks](/mem/configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks).

## Deploy the Autopilot task sequence

1. Select the **Autopilot for existing devices** task sequence, and in the ribbon select **Deploy**.

1. In the Deploy Software Wizard, specify the following details:

    - **General**

      - *Task Sequence*: **Autopilot for existing devices**

      - *Collection*: **Autopilot for existing devices collection**

    - **Deployment Settings**

      - *Action*: **Install**.

      - *Purpose*: **Available**.

      - *Make available to the following*: **Only Configuration Manager Clients**.

        > [!NOTE]
        >
        > Select the option here that is relevant for the context of testing. If the target client doesn't have the Configuration Manager agent or Windows installed, the task sequence needs to be started via PXE or Boot Media.

    - **Scheduling**

      - Set a time for when this deployment becomes available

    - **User Experience**

      - Select **Show Task Sequence progress**

    - **Distribution Points**

      - *Deployment options*: **Download content locally when needed by the running task sequence**

1. Complete the wizard.

## Complete the deployment process

1. On the target Windows device, go to the **Start** menu, enter `Software Center`, and open it.

1. In the Software Library, under **Operating Systems**, select **Autopilot for existing devices**, and then select **Install**.

The task sequence runs and does the following actions:

1. Downloads content.

1. Restarts the device into WinPE.

1. Formats the drive.

1. Installs Windows from the specified OS image.

1. Prepares for Autopilot.

1. After the task sequence completes, the device boots into OOBE for the Autopilot experience:

> [!NOTE]
>
> If devices need to be joined to Active Directory as part of a Microsoft Entra hybrid join scenario, don't do so through the task sequence and the **Apply Network Settings** Task. Instead, create a **Domain Join** device configuration profile. Since there's no Microsoft Entra device object for the computer to do group-based targeting, target the profile to **All Devices**. For more information, see [User-driven mode for Microsoft Entra hybrid join](user-driven.md#user-driven-mode-for-microsoft-entra-hybrid-join).

## Register the device for Windows Autopilot

Devices provisioned with Autopilot only receive the guided OOBE Autopilot experience on first boot.

After Windows is updated on an existing device, make sure to register the device so it has the Autopilot experience when the PC resets. Automatic registration can be enabled for a device by using the **Convert all targeted devices to Autopilot** setting in the Autopilot profile that is assigned to a group that the device is a member of. For more information, see [Create an Autopilot deployment profile](profiles.md#create-an-autopilot-deployment-profile).

Also see [Adding devices to Windows Autopilot](add-devices.md).

> [!NOTE]
>
> - Typically, the target device isn't registered with the Windows Autopilot service. If the device is already registered, the assigned profile takes precedence. The Autopilot for existing devices profile only applies if the online profile times out.
> <!--9105086-->
> - When the assigned profile is applied, the **enrollmentProfileName** property of the device object in Microsoft Intune and Microsoft Entra ID match the Windows Autopilot profile name.
>
> - When the Windows Autopilot for existing devices profile is applied, the **enrollmentProfileName** property of the device object in Microsoft Intune and Microsoft Entra ID are **OffilineAutoPilotProfile-\<ZtdCorrelationId\>**.

## How to speed up the deployment process

To speed up the deployment process, see [Windows Autopilot deployment for existing devices: Speed up the deployment process](tutorial/existing-devices/speed-up-deployment.md) section of the [Autopilot Tutorial](tutorial/autopilot-scenarios.md).

## Tutorial

For a detailed tutorial on configuring Windows Autopilot for existing devices, see the following article:

[Step by step tutorial for Windows Autopilot deployment for existing devices in Intune and Configuration Manager](tutorial/existing-devices/existing-devices-workflow.md)

## Related content

- [New Windows Autopilot capabilities and expanded partner support simplify modern device deployment](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/new-windows-autopilot-capabilities-and-expanded-partner-support/ba-p/260430).
