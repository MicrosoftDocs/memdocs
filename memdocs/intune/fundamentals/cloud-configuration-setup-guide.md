---
# required metadata

title: Windows cloud configuration step by step guide
description: Use this Windows 10/11 cloud configuration step-by-step setup guide to create your own cloud configuration deployment. You create the Microsoft Entra group and policies using Microsoft Intune, including the enrollment profile, compliance policy, and security baseline. You also deploy apps and resources that users need to do their jobs.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/24/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: royork
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- intune-scenario
---

# Windows 10/11 in cloud configuration step by step setup guide

Windows 10/11 in cloud configuration (cloud config) is a device configuration for Windows client devices. Cloud config is designed to simplify the end user experience. For more information about what cloud config is, including the minimum requirements, see [Windows cloud configuration guided scenario overview](cloud-configuration.md).

With cloud config, you use Microsoft Intune policies to turn a Windows client device into a cloud-optimized device. Windows 10/11 in cloud configuration:

- Optimizes devices for the cloud by configuring them to enroll into Intune management with Microsoft Entra. User data is stored in OneDrive automatically with **Known Folder Move** configured.
- Installs Microsoft Teams and Microsoft Edge on devices.
- Configures end users to be standard users on devices, giving IT more control over the apps installed on devices.
- Removes built-in apps and the Microsoft Store app, simplifying the end user experience.
- Applies endpoint security settings and a compliance policy. These policies help keep devices secure and help IT monitor device health.
- Ensures that devices are automatically updated through Windows Update for Business.
- Optionally, you can also:

  - Add other Microsoft 365 apps, like Outlook, Word, Excel, PowerPoint.
  - Add essential line of business (LOB) apps that end users need to be successful. Microsoft recommends keeping these apps to a minimum to keep the configuration simple.
  - Add essential resources, like Wi-Fi profiles, VPN connections, certificates, and printer drivers that are necessary for user workflows.

> [!TIP]
> For an overview on Windows 10/11 in cloud configuration and its uses, see [Windows 10/11 in cloud configuration](https://aka.ms/cloud-config).

There are two ways to deploy cloud config:

- **Option 1 - Automatic**: Use the guided scenario to automatically create all the groups and policies with their configured values. For more information on this option, see [Windows cloud configuration guided scenario overview](cloud-configuration.md).
- **Option 2 - Manual** (this article): Use the steps in this article to deploy cloud config yourself.

This guide helps you create your own cloud configuration deployment. The following sections describe how to use Microsoft Intune to set up cloud config:

1. [Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group)
2. [Configure device enrollment](#step-2---configure-device-enrollment)
3. [Deploy a script to configure Known Folder Move and remove built-in apps](#step-3---configure-onedrive-known-folder-move-and-deploy-a-script-to-remove-built-in-apps)
4. [Deploy apps](#step-4---deploy-apps)
5. [Deploy endpoint security settings](#step-5---deploy-endpoint-security-settings)
6. [Configure Windows Update settings](#step-6---configure-windows-update-settings)
7. [Deploy a Windows compliance policy](#step-7---deploy-a-windows-compliance-policy)
8. [View the optional configurations](#step-8---optional-configurations)

## Prerequisites

- [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]

## Step 1 - Create a Microsoft Entra group

The first step is to create a Microsoft Entra security group that receives the configurations you deploy.

This dedicated group helps you organize devices and manage your cloud config resources in Intune. Microsoft recommends that you deploy only the configurations in this guide. Then, as needed, add more essential apps and other device configurations.

Use the following steps to create the group:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Groups** > **New group**.
3. Enter the following values:

    - **Group type**: Select **Security**.
    - **Group name**: Enter a group name, like `Cloud config PCs`.
    - **Membership type**: Select **Assigned**.
    - **Members**: If you want, you can add devices to your new group now. Select **No members selected** and add members to your group. You can also start with an empty group and add devices later.

4. Select **Create**.

> [!TIP]
> When the group is created, you can add preregistered Windows Autopilot devices to this group.

### Existing devices

If you have existing devices enrolled in Intune that you want to use with cloud config, then we recommend you start fresh with these devices. Specifically:

- Remove existing apps and profiles deployed to these devices.
- Reset these devices.
- Re-enroll the device in Intune and deploy your cloud config.

These extra steps are recommended for existing devices because they provide a streamlined user experience. Then, you can add other essential apps and ensure devices have only what users need.

## Step 2 - Configure device enrollment

In this step, you enable MDM automatic enrollment in Intune and configure how devices enroll in Intune.

If you already use Windows Autopilot, then skip this step, and see [Step 3 - Deploy a script to configure Known Folder Move and remove built-in apps](#step-3---configure-onedrive-known-folder-move-and-deploy-a-script-to-remove-built-in-apps) (in this article).

### ✅ 1 - Enable automatic enrollment

Enable automatic enrollment for the organization users that you want to use cloud config. Automatic enrollment is required for cloud config. For more information on automatic enrollment, see [Enrollment guide -  Windows automatic enrollment](../fundamentals/deployment-guide-enrollment-windows.md#windows-automatic-enrollment).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Device onboarding** > **Enrollment** > **Windows** tab > **Automatic Enrollment**.
3. Under **MDM user scope**, select one of the following:

    - Select **All** to apply the cloud configuration to all Windows devices that users in your organization use. In most cloud config scenarios, **All** is selected.
    - Select **Some** to apply the cloud configuration to devices used by a subset of users in your organization. If you want to apply your cloud config in a staged approach, then **Some** might be a good choice.

4. Don't configure the MAM user scope, MAM terms of user URL, MDM discovery URL, or MAM compliance URL settings. Leave these settings blank. MAM settings aren't configured for cloud config.
5. Select **Save** to save your changes.

### ✅ 2 - Choose how devices enroll and configure users to be standard users on devices

After Windows automatic enrollment is enabled in Intune, the next step is to determine how devices enroll in Intune. When they enroll, they're available to receive your cloud config policies. You also need to configure users to be standard users on their devices. Standard users can only install apps that your organization approves.

For enrollment, you have three options. Select one enrollment option.

- Use Windows Autopilot (recommended)
- Bulk enroll using a provisioning package
- Use the Microsoft Entra ID in the out-of-box experience (OOBE)

This section provides more information on these enrollment options and configuring users as standard users on their devices.

# [Windows Autopilot](#tab/autopilot)

Microsoft recommends you use Windows Autopilot user-driven enrollment and the Enrollment Status Page (ESP). This enrollment method and the ESP provide a consistent end user experience.

- You preregister the devices with the Windows Autopilot deployment service. With Windows Autopilot, admins configure how devices start up and enroll into device management.
- The Intune Windows Autopilot policy configures the **out-of-box experience (OOBE)**. In the OOBE, you select users to be standard users.
- The Intune Windows Autopilot policy configures the Enrollment Status Page (ESP). The ESP shows the configuration progress. Users stay on the ESP until all cloud config settings are applied to the device.

To set up Windows Autopilot user-driven enrollment, use the following steps:

1. **Add devices to Windows Autopilot**.

    Register your devices in Windows Autopilot using the steps at [Step 3 - Register devices to Windows Autopilot](/autopilot/tutorial/user-driven/azure-ad-join-register-device) (opens a Windows Autopilot article).

    > [!NOTE]
    > The [Step 3 - Register devices to Windows Autopilot](/autopilot/tutorial/user-driven/azure-ad-join-register-device) Windows Autopilot article is part of a series of steps. For this cloud config, only follow [Step 3 - Register devices to Windows Autopilot](/autopilot/tutorial/user-driven/azure-ad-join-register-device) to register your devices. Don't follow the other steps in series. The other steps in that Windows Autopilot series are for a different Windows Autopilot scenario.

    You can also [manually register devices to use Windows Autopilot](/autopilot/add-devices). Manually registering devices is often used to repurpose existing hardware that wasn't previously set up with Windows Autopilot.

2. **Create and assign a Windows Autopilot deployment profile in Intune**.

    1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
    2. Select **Devices** > **Device onboarding** > **Enrollment** > **Windows** tab > **Windows Autopilot** > **Deployment profiles**.
    3. Select **Create profile** > **Windows PC**. Enter a name for the profile.
    4. For the **Convert all targeted devices to Autopilot** setting, select **Yes**. Select **Next**.

        You can apply cloud config to devices enrolled using enrollment methods other than Windows Autopilot. When you add those devices (non-Windows Autopilot devices) to your group, the devices are converted to Windows Autopilot. The next time the devices are reset and go through the Windows out-of-box experience (OOBE), they enroll through Windows Autopilot.

    5. In the **out-of-box experience (OOBE)** tab, enter the following values, and then select **Next**:

        | Setting    | Value |
        | --- | --- |
        | Deployment mode |    User-driven |
        | Join to Microsoft Entra ID as    | Microsoft Entra joined |
        | Microsoft Software License Terms | Hide |
        | Privacy settings    | Hide |
        | Hide change account options    | Hide |
        | User account type    | Standard |
        | Allow pre-provisioned deployment    | No |
        | Language (Region)    | Operating system default |
        | Automatically configure keyboard    | Yes |
        | Apply device name template    | Optional. You can apply a device name template. Use a name prefix that can help you identify your cloud config devices, like `Cloud-%SERIAL%`.` |

    6. Assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article), and then select **Next**.
    7. Review the new profile and then select **Create**.

3. **Create and assign an Enrollment Status Page in Intune**.
  
    1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
    2. Select **Devices** > **Device onboarding** > **Enrollment** > **Windows** tab > **Windows Autopilot** > **Enrollment Status Page**.
    3. Select **Create**, enter a name for the **Enrollment Status Page** > **Next**.
    4. In the **Settings** tab, enter the following values, and then select **Next**:

        | Setting |    Value |
        | --- | --- |
        | Show app and profile configuration process |    Yes |
        | Show an error when installation takes longer than specified number of minutes    | 60 |
        | Show custom message when time limit error occurs    | Yes - You can also change the default message. |
        | Turn on log collection and diagnostics page for end users    | Yes |
        | Block device user until all apps and profiles are installed    | Yes |
        | Allow users to reset device if installation error occurs    | Yes |
        | Allow users to use device if installation error occurs |     No |
        | Block device user until these required apps are installed if they are assigned to the user/device |    All |

        > [!NOTE]  
        > If an installation error occurs, we recommend you block users from using the device. Blocking users makes sure they can only start using the device after cloud config is fully applied.
        >
        > If an installation error occurs, based on your deployment needs, you can allow the user to use the device. If you do allow using the device, when the device checks in with Intune, Intune continues trying to apply the configurations.

    5. In **Assignments**, assign the Enrollment Status Page to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

        Select **Next**.

    6. Select **Create** to create and assign the Enrollment Status Page.

# [Provisioning package](#tab/provpack)

You can bulk enroll devices using a provisioning package created using Windows Configuration Designer or the **[Set up School PCs](/education/windows/use-set-up-school-pcs-app)** app.

For more information on bulk enrollment, see [Bulk enrollment for Windows devices](../enrollment/windows-bulk-enroll.md).

With bulk enrollment:

- After the devices enroll in Intune, then you add them to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article). When they're added to the group, they receive your cloud config.
- All users are automatically standard users on the device.
- There isn't an Enrollment Status Page. Users can't view the progress as all the cloud configuration settings are applying. Users can start using the device before cloud config is fully applied.
- Before you distribute devices to users, Microsoft recommends that you verify that the settings and apps are on the devices.

# [Out-of-box experience](#tab/oobe)

With MDM automatic enrollment enabled in Intune, during the out-of-box experience (OOBE), users sign in with their Microsoft Entra accounts. When they sign-in, enrollment automatically starts.

With this enrollment option, you:

1. Configure a Microsoft Intune [custom profile](../configuration/custom-settings-windows-10.md) that restricts local administrators on devices. The [Policy CSP](/windows/client-management/mdm/policy-csp-localusersandgroups) includes a sample policy definition XML that you can use in your custom profile.

    > [!TIP]
    > In this custom profile, there's another setting that adds a group that can be local admins on the device. This local admin group should only include IT administrators in your environment.

2. Assign the custom profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).  

---

## Step 3 - Configure OneDrive Known Folder Move and deploy a script to remove built-in apps

When you configure OneDrive **Known Folder Move**, user files and data are automatically saved in OneDrive. When you remove built-in Windows apps and the Microsoft Store, the Start menu and device experience are simplified.

This step helps simplify the Windows user experience. 

### ✅ 1 - Configure OneDrive Known Folder Move with an Administrative Template

With **Known Folder Move**, users data (files and folders) is saved to OneDrive. When users sign in to another device, OneDrive automatically synchronizes the data to the new device. Users don't have to manually move their files.

> [!NOTE]  
> Due to a sync issue with OneDrive **Known Folder Move** and SharedPC configuration, Microsoft doesn't recommend using Windows in cloud configuration with a device that has multiple users signing in and out.

To configure **Known Folder Move**, create a settings catalog policy in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter a name for the profile and select **Next**.
6. In **Configuration settings**, select **Add settings**. Select and configure the following settings and recommended values:

    ??I assume device settings, not user??

    | Setting | Value |
    | --- | --- |
    | Prevent users from moving their Windows known folders to OneDrive | Enabled |
    | Prevent users from redirecting their Windows known folders to their PC | Enabled |
    | Silently move Windows known folders to OneDrive | Enabled <br/><br/> This setting is listed twice. Select the option that only has **Show notification to users after folders have been redirected (Device)** and **Tenant ID (Device)**. |
    | Show notification to users after folders have been redirected: (Device) | Yes. You can also choose to hide the notification. |
    | Tenant ID: (Device) | Enter your organization's tenant ID. <br/><br/>Your tenant ID is shown in Microsoft Entra admin center > [Properties page](https://go.microsoft.com/fwlink/?linkid=2155017) > **Tenant ID**. |
    | Silently sign in users to the OneDrive sync app with their Windows credentials | Enabled |
    | Use OneDrive Files On-Demand | Enabled |

7. Assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

### ✅ 2 - Deploy a script to remove built-in apps

Microsoft created a Windows PowerShell script that:

- Removes built-in apps from devices.
- Removes the Microsoft Store app from devices.

The script is deployed to devices using in Intune. To add and deploy the script, use the following steps:

1. Download the [Cloud config Window PowerShell app removal script](https://go.microsoft.com/fwlink/?linkid=2153583). This script removes the Microsoft Store app and the built-in apps.

    > [!NOTE]
    > If you want to keep the Microsoft Store app on devices, then you can use the [script that removes built-in apps but keeps the Microsoft Store](https://go.microsoft.com/fwlink/?linkid=2157781) instead. To use this script, download it instead and follow the same steps. This script tries to remove built-in apps but might not remove all of them. You might need to modify the script to remove all built-in apps on your devices.

2. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Devices** > **Manage devices** > **Scripts and remediations** > **Platform scripts** tab > **Add** > **Windows 10 and later**.
4. In **Basics**, enter a name for your script policy and select **Next**.
5. In **Script settings**, upload the script you downloaded. Leave the other settings unchanged and select **Next**.
6. Assign the script to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

#### Microsoft Store app

If you previously removed the Microsoft Store app, you can redeploy it using Microsoft Intune. To re-add the Microsoft Store app (or any other apps you want to re-add), add the Microsoft Store app to your private organization app repository. Then, deploy the app to devices using Intune. The Microsoft Store app helps keep apps updated.

Your private organization app repository can be the [Intune Company Portal app or website](../apps/company-portal-app.md).  

Using Intune, on Windows 10/11 Enterprise and Education devices, you can block end users from installing Microsoft Store apps outside of your organization's private app repository.

To prevent these outside apps, use the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter a name for the profile and select **Next**.
6. In **Configuration settings**, select **Add settings**. Select and configure the following settings with the recommended values:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | Microsoft App Store | Require Private Store Only | Only Private store is enabled |

7. In **Assignments**, assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
8. In **Review + create**  review your profile and select **Create**.

## Step 4 - Deploy apps

This step deploys Microsoft Edge and Microsoft Teams. You can deploy other essential apps in this step. Remember, only deploy what users need.

### ✅ 1 - Deploy Microsoft Edge

1. [Add Microsoft Edge to Intune](../apps/apps-windows-edge.md).
2. For **App settings**, select the **Stable Channel**.
3. Assign the Microsoft Edge app to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

### ✅ 2- Deploy Microsoft Teams

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Platforms** > **Windows** > **Create**.
3. In **App type**, see **Microsoft 365 Apps** > select **Windows 10 and later** > **Select**.
4. In **App suite information**, enter a **Suite Name** > **Next**.
5. In **Configure app suite**, configure the following settings:

    | Setting | Value |
    | --- | --- |
    | Select Office apps | Teams <br/><br/>If you want to deploy other Microsoft 365 apps, then select them from this list. Remember, only deploy what users need. |
    | Architecture | 64-bit <br/><br/> Cloud config also works with 32-bit. Microsoft recommends choosing 64-bit. |
    | Default file format | ?? **Office Open Document Format** or **Office Open XML Format** ??|
    | Update channel | Current channel |
    | Remove other versions | Yes |
    | Version to install | Latest |
    | Use shared computer activation | Yes |
    | Accept the Microsoft Software License Terms on behalf of users | Yes|
  
6. Select **Next**.
7. Assign the suite to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Step 5 - Deploy endpoint security settings

This step configures endpoint security settings to help keep devices secure, including the built-in Windows security baseline and BitLocker settings.

### ✅ 1 - Deploy the Windows 10/11 MDM security baseline

For Windows in cloud configuration, we recommend you use the Windows 10/11 [security baseline](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines). There are some setting values you can change based on your organization's preference.

Configure the security baseline in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Security baselines** > **Security baseline for Windows 10 and later**.
3. Select **Create profile** to create a new security baseline.
4. In **Basics**, enter a name for your security baseline and select **Next**.
5. In **Configuration settings**, accept the default configuration settings. Or, you can change the following settings based on your organization needs:

    | Setting category | Setting | Reason for changing |
    | --- | --- | --- |
    | Browser | Allow Password Manager | If you want to allow end users to use password managers, then allow this setting. |
    | Remote Assistance ?? | Remote Assistance solicited | This setting allows your support staff to remotely connect to devices. Microsoft recommends disabling this setting unless your organization requires it. |
    | Firewall | All Firewall settings | If you need to allow certain connections to devices based on your organization's needs, then change the default Firewall settings. |

    Select **Next**.

6. In **Assignments**, select the group that you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
7. Select **Create** to create and assign the baseline.

### ✅ 2 - Deploy more BitLocker settings with a drive encryption endpoint security profile

There are more BitLocker settings that help keep your devices secure. Configure these BitLocker settings in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows**.
    - **Profile type**: Select **BitLocker**.

4. Select **Create**.
5. In **Basics**, enter a name for the profile and select **Next**.
6. In **Configuration settings**, select and configure the following settings and recommended values:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | **BitLocker** | Require Device Encryption | Enabled |
    | &nbsp; | &nbsp; | &nbsp; |
    | **BitLocker Drive Encryption** | Choose drive encryption method and cipher strength | Enabled |
    | &nbsp; | Select the encryption method for fixed data-drives | XTS-AES 128-bit |
    | &nbsp; | Select the encryption method for operating system drives | XTS-AES 128-bit  |
    | &nbsp; | Select the encryption method for removable data drives | AES-CBC 128-bit |
    | &nbsp; | &nbsp; | &nbsp; |
    | **Operating System Drives** | BitLocker system drive policy ?? | Configure |
    | &nbsp; | Require additional authentication at startup | Enabled |
    | &nbsp; | Allow BitLocker without a compatible TPM  | False |
    | &nbsp; | Configure TPM startup key and PIN | Allow startup key and PIN with TPM |
    | &nbsp; | Configure TPM startup key | Require startup key with TPM |
    | &nbsp; | Configure TPM startup PIN | Allow startup PIN with TPM |
    | &nbsp; | Configure TPM startup | Allow TPM |
    | &nbsp; | &nbsp; | &nbsp; |
    | **Fixed Data Drives** | Choose how BitLocker-protected fixed drives can be recovered | Enabled |
    | &nbsp; | Deny write access to fixed drives not protected by BitLocker | Enabled |
    | &nbsp; | &nbsp; | &nbsp; |
    | **Removable Drive Settings** | BitLocker removable drive policy ?? | Configure |
    | &nbsp; | Deny write access to removable drives not protected by BitLocker | Enabled |

7. In **Assignments**, assign the profile to the group that you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
8. Select **Create** to create and assign the profile.

## Step 6 - Configure Windows Update settings

This step uses a Windows Update Ring to keep devices automatically updated. The settings in this guide align with the recommended settings in the Windows [Update Baseline](/windows/deployment/update/update-baseline).

Configure the Update ring in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage updates** > **Windows updates** > **Update rings** tab > **Create profile**.
3. In **Basics**, enter a name for the update ring. Select **Next**.
4. In **Update ring settings**, configure the following values and select **Next**:

    | Setting | Value |
    | --- | --- |
    | ?? Servicing channel | Semi-annual channel |
    | Microsoft product updates | Allow |
    | Windows drivers | Allow |
    | Quality update deferral period (days) | 0 |
    | Feature update deferral period (days) | 0 |
    | Set feature update uninstall period | 10 |
    | Automatic update behavior | Reset to default |
    | ?? Restart checks | Allow |
    | Option to pause Windows updates | Enable |
    | Option to check for Windows updates | Enable |
    | ?? Require user approval to dismiss restart notification | No |
    | ?? Remind user prior to required auto-restart with dismissible reminder (hours) | Leave this setting unconfigured |
    | ?? Remind user prior to required auto-restart with permanent reminder (minutes) | Leave this setting unconfigured |
    | Change notification update level | Use the default Windows Update notifications |
    | Use deadline settings | Allow |
    | Deadline for feature updates | 7 |
    | Deadline for quality updates | 2 |
    | Grace period | 2 |
    | Auto reboot before deadline | Yes |

5. Assign the Update ring to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Step 7 - Deploy a Windows compliance policy

Configure a compliance policy to help monitor device compliance and health. The policy reports on noncompliance and still allow users to use devices. You can choose how to address noncompliance with other actions based on your organization's processes.

Create the compliance policy in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Compliance** > **Create Policy**.
3. For **Platform**, select **Windows 10 and later** > **Create**.
4. In **Basics**, enter a name for the compliance policy. Select **Next**.
5. In **Compliance settings**, configure the following settings and values, and select **Next**:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | **Device Health** | BitLocker | Require |
    | &nbsp; | Secure Boot | Require |
    | &nbsp; | Code integrity | Require |
    | &nbsp; | &nbsp; | &nbsp; |
    | **System Security** | Require a password to unlock mobile devices | Require |
    | &nbsp; | Simple passwords | Block |
    | &nbsp; | Password type | Alphanumeric |
    | &nbsp; | ?? Password Complexity | ?? |
    | &nbsp; | Minimum password length | 8 |
    | &nbsp; | Maximum minutes of inactivity before password is required | 1 Minute |
    | &nbsp; | Password expiration (days) | 41 |
    | &nbsp; | Number of previous passwords to prevent reuse | 5 |
    | &nbsp; | Firewall | Require |
    | &nbsp; | Antivirus | Require |
    | &nbsp; | Antispyware | Require |
    | &nbsp; | Microsoft Defender Antimalware | Require |
    | &nbsp; | Microsoft Defender Antimalware security intelligence up-to-date | Require |
    | &nbsp; | Real-time protection | Require |

6. In **Actions for noncompliance**:

    - **Marking device noncompliant** action: Set **Schedule (days after noncompliance)** to `1` day. You can configure a different grace period based on your organization preferences.

      If you use Conditional Access policies in your organization, then we recommend you configure a grace period. Grace periods prevent noncompliant devices from immediately losing access to organization resources.

    - (Optional) **Send email to end users** action: You can add an action to email users informing them of noncompliance with steps to get compliant.

      To learn more about this feature, see [Configure actions for noncompliant devices in Intune](../protect/actions-for-noncompliance.md).

7. Assign the compliance policy to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Step 8 - Optional configurations

There are optional policies you can create and deploy with your cloud config. This section describes these optional policies.

### ✅ Configure a tenant domain name

Configure devices to automatically use your tenant's domain name for user sign-ins. When you add a domain name, users don't have to type their full UPN to sign in.

Add the tenant domain name in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Device restrictions**.

4. Select **Create**.
5. In **Basics**, enter a name for the profile and select **Next**.
6. In **Configuration settings**, configure the following settings and values, and select **Next**:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | **Password** | Preferred Microsoft Entra tenant domain | Enter the Microsoft Entra domain name that users should use to sign in to devices, like `contoso.com`. |

7. Assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

### ✅ Deploy other essential productivity and line of business (LOB) apps

You might have a few essential LOB apps that all devices need. Choose a minimum number of these apps to deploy. If you deliver apps using a virtualization solution, then also deploy the virtualization client app to devices.

There are no restrictions on the number or size of other apps that can be deployed with the apps added to your cloud configuration. But, Microsoft recommends keeping these other apps to a minimum based on what users need for their roles. Assign these essential apps to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

You might need specific LOB apps on some of your devices. Or, there might be some apps that have complex packaging or procedure requirements. For these scenarios, consider moving these apps out of your cloud config deployment. Or, keep the devices that need these apps in your existing Windows management model.

Cloud config is recommended for devices that need just a few key apps, along with collaboration and browsing.

### ✅ Deploy resources that users need for organization access

Configure essential resources that users might need, which depends on your organization's processes. Essential resources can include certificates, printers, VPN connections, and Wi-Fi profiles.

In Intune, assign these resources to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

### ✅ Configure recommended settings for OneDrive Known Folder Move

There are more settings that improve the user experience for OneDrive **Known Folder Move**. The settings aren't required for **Known Folder Move** to work but are helpful.

For more information on these settings, see [OneDrive settings recommended for Known Folder Move](/sharepoint/ideal-state-configuration).

### ✅ Configure recommended Microsoft Edge settings

There are some Microsoft Edge app settings that can be configured for a better user experience. You can configure these settings based on requirements or preference for the end user experience.

To configure these recommended settings, use Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter a name for the profile and select **Next**.
6. In **Configuration settings**, select **Add settings**. Select and configure the following settings and recommended values:

    | Setting Category | Setting | Value |
    | --- | --- | --- |
    | **Microsoft Edge** | Configure Internet Explorer integration ??User or device?? | Enabled, Internet Explorer mode |
    | &nbsp; | &nbsp; | &nbsp; |
    | **Microsoft Edge\SmartScreen settings** | Configure Microsoft Defender SmartScreen ??User or device??| Enabled |
    | &nbsp; | Configure Microsoft Defender SmartScreen to block potentially unwanted apps ??User or device??| Enabled |
    | &nbsp; | Force Microsoft Defender SmartScreen checks on downloads from trusted sources ??User or device??| Enabled |

    > [!NOTE]
    > Microsoft Defender also enforced the SmartScreen settings. When you configure the SmartScreen settings through the Microsoft Edge app, Microsoft Edge directly enforces the settings.

7. Assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Monitor the status of cloud config

When you apply cloud config to your devices, you can use Intune to monitor the status of apps and device configurations.

### Script status

You can monitor the installation status of your deployed scripts:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Devices** > **Manage devices** > **Scripts and remediations** > **Platform scripts** tab.
2. Select the script you deployed.
3. In the script details page, select **Device status**. The script installation details are shown.

### App installations

You can monitor the installation status of your deployed apps:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Apps** > **Platforms** > **Windows**.
2. Select an app you deployed, like the Microsoft 365 App Suite.
3. Select **Device install status** or **User install status**. The app installation details are shown.

For information on troubleshooting app issues on individual devices, see [Troubleshooting Intune app installation issues](/troubleshoot/mem/intune/app-management/troubleshoot-app-install).

### Security baseline

You can monitor the installation status of your deployed security baseline. For more information, see [Monitor security baselines and profiles in Intune](../protect/security-baselines-monitor.md).

### Disk encryption profile

In [Step 5 - Deploy endpoint security settings](#step-5---deploy-endpoint-security-settings) (in this article), you might have configured and deployed BitLocker settings.

You can monitor the status of this BitLocker profile:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Endpoint security** > **Manage** > **Disk encryption**.
2. Select the disk encryption profile you deployed in cloud config.
3. Select **Device install status** or **User install status**. The profile details are shown.

### Windows Update settings

You can monitor the status of the Windows Update ring policy:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Devices** > **Manage updates** > **Windows updates** > **Update rings** tab.
2. Select the update ring you deployed as part of cloud config.
3. Select **Device status**, **User status**, or **End user update status**. The update ring settings details are shown.

For more information on reporting for Windows Update rings, see [Reports for Update rings for Windows 10 and later policy](../protect/windows-update-reports.md#reports-for-update-rings-for-windows-10-and-later-policy).

### Compliance policy

You can monitor the status of the compliance policy:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Devices** > **Manage devices** > **Compliance**.
2. Select the compliance policy you deployed as part of cloud config.

The device compliance monitoring view has detailed information on the assignment status and assignment failures of your compliance policies. It also has views to quickly find noncompliant devices and take action.

For more in-depth information on monitoring compliance policies in Intune, see [Monitor results of your Intune Device compliance policies](../protect/compliance-policy-monitor.md).

## Related content

- [Windows cloud configuration guided scenario overview](cloud-configuration.md)
