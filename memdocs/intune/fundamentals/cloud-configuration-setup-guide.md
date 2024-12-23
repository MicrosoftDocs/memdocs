---
# required metadata

title: Windows cloud configuration step by step guide
description: Use this Windows 10/11 cloud configuration step-by-step setup guide to create your own cloud configuration deployment. You create the Microsoft Entra group and policies using Microsoft Intune, including the enrollment profile, compliance policy, and security baseline. You also deploy apps and resources that users need to do their jobs.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rashok
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

Windows 10/11 in cloud configuration (cloud config) is a device configuration for Windows client devices. It's designed to simplify the end user experience. For more information about what cloud config is, including the minimum requirements, go to [Windows cloud configuration guided scenario overview](cloud-configuration.md).

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
> For a overview on Windows 10/11 in cloud configuration and its uses, go to [Windows 10/11 in cloud configuration](https://aka.ms/cloud-config).

There are two ways to deploy cloud config:

- **Option 1 - Automatic**: Use the guided scenario to automatically create all the groups and policies with their configured values. For more information on this option, go to [Windows cloud configuration guided scenario overview](cloud-configuration.md).
- **Option 2 - Manual** (this article): Use the steps in this article to deploy cloud config yourself.

This guide helps you create your own cloud configuration deployment. The following sections describe how to use Microsoft Intune to set up cloud config:

1. [Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group)
2. [Configure device enrollment](#step-2---configure-device-enrollment)
3. [Deploy a script to configure Known Folder Move and remove built-in apps](#step-3---configure-onedrive-known-folder-move-and-deploy-a-script-to-remove-built-in-apps)
4. [Deploy apps](#step-4---deploy-apps)
5. [Deploy endpoint security settings](#step-5---deploy-endpoint-security-settings)
6. [Configure Windows Update settings](#step-6---configure-windows-update-settings)
7. [Deploy a Windows compliance policy](#step-7---deploy-a-windows-compliance-policy)
8. [Optional configurations](#step-8---optional-configurations)

## Step 1 - Create a Microsoft Entra group

The first step is to create a Microsoft Entra security group that receives the configurations you deploy.

This dedicated group helps you organize devices and manage your cloud config resources in Intune. Microsoft recommends that you deploy only the configurations in this guide. Then, as needed, add more essential apps and other device configurations.

Use the following steps to create the group:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Groups** > **All groups** > **New group**.
3. For **Group type**, select **Security**.
4. Enter a **Group name**, like `Cloud config PCs`.
5. For **Membership type**, select **Assigned**.
6. If you want, you can add devices to your new group now. Select **No members selected** and add members to your group.

    You can also start with an empty group and add devices later.

7. Select **Create**.

> [!TIP]
> When the group is created, you can add preregistered Windows Autopilot devices to this group.

### Existing devices

If you have existing devices enrolled in Intune that you want to use with cloud config, then it's recommended to start fresh with these devices. Specifically:

- Remove existing apps and profiles deployed to these devices.
- Reset these devices.
- Re-enroll the device in Intune and deploy your cloud config.

These extra steps are recommended for existing devices because they provide a streamlined user experience. Then, you can add other essential apps and ensure devices have only what users need.

## Step 2 - Configure device enrollment

In this step, you enable MDM automatic enrollment in Intune and configure how devices enroll in Intune.

If you already use Windows Autopilot, then skip this step, and go to [Step 3 - Deploy a script to configure Known Folder Move and remove built-in apps](#step-3---configure-onedrive-known-folder-move-and-deploy-a-script-to-remove-built-in-apps) (in this article).

### ✅ 1 - Enable automatic enrollment

Enable automatic enrollment for the organization users that you want to use cloud config. Automatic enrollment is required for cloud config. For more information on automatic enrollment, go to [Enrollment guide -  Windows automatic enrollment](../fundamentals/deployment-guide-enrollment-windows.md#windows-automatic-enrollment).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **By platform** > **Windows** > **Device onboarding** > **Enrollment** > **Automatic Enrollment**.
3. Under **MDM user scope**, select one of the following:

    - Select **All** to apply the cloud configuration to all Windows devices that users in your organization use. In most cloud config scenarios, **All** is selected.
    - Select **Some** to apply the cloud configuration to devices used by a subset of users in your organization. If you want to apply your cloud config in a staged approach, then **Some** might be a good choice.

4. Don't configure the MAM user scope, MAM terms of user URL, MDM discovery URL, and MAM compliance URL settings. Leave these settings blank. MAM settings aren't configured for cloud config.
5. Select **Save** to save your changes.

### ✅ 2 - Choose how devices enroll and configure users to be standard users on devices

After Windows automatic enrollment is enabled in Intune, the next step is to determine how devices enroll in Intune. When they enroll, they're available to receive your cloud config policies. You also need to configure users to be standard users on their devices. Standard users can only install apps that your organization approves.

For enrollment, you have three options. Select one enrollment option.

- Use Windows Autopilot (recommended)
- Bulk enroll using a provisioning package
- Use the Microsoft Entra ID in the out-of-box experience (OOBE)

This section provides more information on these enrollment options and configuring users as standard users on their devices.

#### Enrollment option 1: Windows Autopilot user-driven enrollment (recommended)

It's recommended to use Windows Autopilot enrollment and the Enrollment Status Page (ESP). This enrollment method and the ESP provide a consistent end user experience.

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
    2. Select **Devices** > **By platform** > **Windows** > **Device onboarding** > **Enrollment** > **Windows Autopilot Deployment Program** > **Deployment profiles**.
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
    2. Select **Devices** > **By platform** > **Windows** > **Device onboarding** > **Enrollment** > **General** > **Enrollment Status Page**.
    3. Select **Create** and enter a name for the **Enrollment Status Page**.
    4. In the **Settings** tab, enter the following values, and then select **Next**:

        | Setting |    Value |
        | --- | --- |
        | Show app and profile configuration process |    Yes |
        | Show an error when installation takes longer than specified number of minutes    | 60 |
        | Show custom message when time limit error occurs    | Yes - You can also change the default message. |
        | Allow users to collect logs about installation errors    | Yes |
        | Block device user until all apps and profiles are installed    | Yes |
        | Allow users to reset device if installation error occurs    | Yes |
        | Allow users to use device if installation error occurs |     No |
        | Block device user until these required apps are installed if they are assigned to the user/device |    All |

        > [!NOTE]  
        > If an installation error occurs, it's recommended to block users from using the device. Blocking users makes sure they can only start using the device after cloud config is fully applied.
        >
        > If an installation error occurs, based on your deployment needs, you can allow the user to use the device. If you do allow using the device, when the device checks in with Intune, Intune continues trying to apply the configurations.

    5. In **Assignments**, assign the Enrollment Status Page to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

        Select **Next**.

    6. Select **Create** to create and assign the Enrollment Status Page.

#### Enrollment option 2: Bulk enrollment using a provisioning package

You can enroll devices using a provisioning package created using Windows Configuration Designer or the **[Set up School PCs](/education/windows/use-set-up-school-pcs-app)** app.

For more information on bulk enrollment, go to [Bulk enrollment for Windows devices](../enrollment/windows-bulk-enroll.md).

With bulk enrollment:

- After the devices enroll in Intune, then you add them to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article). When they're added to the group, they receive your cloud config.
- All users are automatically standard users on the device.
- There isn't an Enrollment Status Page. Users can't view the progress as all the cloud configuration settings are applying. Users can start using the device before cloud config is fully applied.
- Before you distribute devices to users, Microsoft recommends that you verify that the settings and apps are on the devices.

#### Enrollment option 3: Enroll using Microsoft Entra ID in the out-of-box experience (OOBE)

With MDM automatic enrollment enabled in Intune, during the OOBE, users sign in with their Microsoft Entra accounts. When they sign-in, enrollment automatically starts.

With this enrollment option, you:

1. Configure a Microsoft Intune custom profile to restrict local administrators on devices. The [Policy CSP](/windows/client-management/mdm/policy-csp-localusersandgroups) includes a sample policy definition XML that you can use in your custom profile.

    > [!TIP]
    > In this custom profile, there's another setting that adds a group that can be local admins on the device. This local admin group should only include IT administrators in your environment.

2. Assign the custom profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).  

## Step 3 - Configure OneDrive Known Folder Move and deploy a script to remove built-in apps

When you configure OneDrive **Known Folder Move**, user files and data are automatically saved in OneDrive. When you remove built-in Windows apps and the Microsoft Store, the Start menu and device experience are simplified.

This step helps simplify the Windows user experience. 

### ✅ 1 - Configure OneDrive Known Folder Move with an Administrative Template

With **Known Folder Move**, users data (files and folders) is saved to OneDrive. When users sign in to another device, OneDrive automatically synchronizes the data to the new device. Users don't have to manually move their files.

> [!NOTE]  
> Due to a sync issue with OneDrive **Known Folder Move** and SharedPC configuration, Microsoft doesn't recommend using Windows in cloud configuration with a device that has multiple users signing in and out.

To configure **Known Folder Move**, use an ADMX template in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Select **Windows 10 and later** for platform and select **Templates** for profile type.
4. Select **Administrative Templates** and select **Create**.
5. Enter a name for the profile and select **Next**.
6. In **Configuration settings**, search for the settings in the following table and select their recommended values:

    | Setting name | Value |
    | --- | --- |
    | Silently move Windows known folders to OneDrive Enabled Tenant ID | Enter your organization's tenant ID. <br/><br/>Your tenant ID is shown in Microsoft Entra admin center > [Properties page](https://go.microsoft.com/fwlink/?linkid=2155017) > **Tenant ID**.|
    | Show notification to users after folders have been redirected | Yes. You can also choose to hide the notification. |
    | Silently sign in users to the OneDrive sync app with their Windows credentials | Enabled |
    | Prevent users from moving their Windows known folders to OneDrive | Enabled |
    | Prevent users from redirecting their Windows known folders to their PC | Enabled |
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
3. Select **Devices** > **By platform** > **Windows** > **Manage devices** > **Scripts and remediations** > **Platform scripts** tab > **Add**.
4. In **Basics**, enter a name for your script policy and select **Next**.
5. In **Script settings**, upload the script you downloaded. Leave the other settings unchanged and select **Next**.
6. Assign the script to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

#### Microsoft Store app

If you previously removed the Microsoft Store app, you can redeploy it using Microsoft Intune. To re-add the Microsoft Store app (or any other apps you want to re-add), add the Microsoft Store app to your private organization app repository. Then, deploy the app to devices using Intune. The Microsoft Store app helps keep apps updated. For information about how to configure access to the Microsoft Store app, see [Manage access to private store](/microsoft-store/manage-access-to-private-store).  

Your private organization app repository can be the Intune Company Portal app or website.  

Using Intune, on Windows 10/11 Enterprise and Education devices, you can block end users from installing Microsoft Store apps outside of your organization's private app repository.

To prevent these outside apps, use the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Select **Windows 10 and later** for platform and select **Settings catalog** for profile type. Select **Create**.
4. In **Basics**, enter a name for your profile.
5. In **Configuration settings**, select **Add settings**. Then:

    1. In the settings picker, search for `private store`. In the search results under the Microsoft App Store category, select **Require Private Store Only**.
    2. Set the **Require Private Store Only** setting to **Only Private store is enabled**.
    3. Select **Next**.

6. In **Assignments**, assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
7. In **Review + create**  review your profile and select **Create**.

## Step 4 - Deploy apps

This step deploys Microsoft Edge and Microsoft Teams. You can deploy other essential apps in this step. Remember, only deploy what users need.

### ✅ 1 - Deploy Microsoft Edge

1. [Add Microsoft Edge to Intune](../apps/apps-windows-edge.md).
2. For **App settings**, select the **Stable Channel**.
3. Assign the Microsoft Edge app to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

### ✅ 2- Deploy Microsoft Teams

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Windows**.
3. Select **Add** to create a new app.
4. For **Microsoft 365 Apps**, select **Windows 10 and later** > **Select**.
5. For **Suite Name**, enter a name or use the suggested name. Select **Next**.
6. For **Configure app suite**, only select Teams.

    If you want to deploy other Microsoft 365 apps, then select them from this list. Remember, only deploy what users need.

    > [!TIP]  
    > You don't need to choose OneDrive. OneDrive is built into Windows 10/11 Pro, Enterprise, and Education.

7. For **App suite information**, configure the following settings:

    | Setting | Value |
    | --- | --- |
    | Architecture | 64-bit <br/><br/> Cloud config also works with 32-bit. Microsoft recommends choosing 64-bit. |
    | Update channel | Current channel |
    | Remove other versions | Yes |
    | Version to install | Latest |

8. For **Properties**, configure the following settings:

    | Setting | Value |
    | --- | --- |
    | Use shared computer activation | Yes |
    | Accept the Microsoft Software License Terms on behalf of users | Yes|
  
9. Select **Next**.
10. Assign the suite to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Step 5 - Deploy endpoint security settings

This step configures endpoint security settings to help keep devices secure, including the built-in Windows security baseline and BitLocker settings.

### ✅ 1 - Deploy the Windows 10/11 MDM security baseline

For Windows in cloud configuration, it's recommended to use the Windows 10/11 [security baseline](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines). There are some setting values you can change based on your organization's preference.

Configure the security baseline in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Security baselines** > **Security baseline for Windows 10 and later**.
3. Select **Create profile** to create a new security baseline.
4. Enter a name for your security baseline and select **Next**.
5. Accept the default configuration settings. Or, you can change the following settings based on your organization needs:

    | Setting category | Setting | Reason for changing |
    | --- | --- | --- |
    | Browser | Block Password Manager | If you want to allow end users to use password managers, then disable this setting. |
    | Remote Assistance | Remote Assistance solicited | This setting allows your support staff to remotely connect to devices. Microsoft recommends disabling this setting unless it's required. |
    | Firewall | All Firewall settings | If you need to allow certain connections to devices based on your organization's needs, then change the default Firewall settings. |

    Select **Next**.

6. In **Assignments**, select the group that you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
7. Select **Create** to create and assign the baseline.

### ✅ 2 - Deploy more BitLocker settings with a drive encryption endpoint security profile

There are more BitLocker settings that help keep your devices secure. Configure these BitLocker settings in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.
3. For **Platform**, select **Windows 10 and later**.
4. For **Profile**, select **BitLocker** > **Create**.
5. In **Basics**, enter a name for your profile.
6. In **Configuration settings**, select the following settings:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | **BitLocker – Base settings** | Enable full disk encryption for OS and fixed data drives | Yes |
    | &nbsp; | &nbsp; | &nbsp; |
    | **BitLocker – Fixed Drive Settings** | BitLocker fixed drive policy | Configure |
    | &nbsp; | Block write access to fixed data drives not protected by BitLocker | Yes |
    | &nbsp; | Configure encryption method for fixed data-drives | AES 128bit XTS |
    | &nbsp; | &nbsp; | &nbsp; |
    | **BitLocker – OS Drive Settings** | BitLocker system drive policy | Configure |
    | &nbsp; | Startup authentication required | Yes |
    | &nbsp; | Compatible TPM startup | Allowed |
    | &nbsp; | Compatible TPM startup PIN | Allowed |
    | &nbsp; | Compatible TPM startup key | Required |
    | &nbsp; | Compatible TPM startup key and PIN | Allowed |
    | &nbsp; | Disable BitLocker on devices where TPM is incompatible | Yes |
    | &nbsp; | Configure encryption method for Operating System drives | AES 128bit XTS |
    | &nbsp; | &nbsp; | &nbsp; |
    | **BitLocker – Removable Drive Settings** | BitLocker removable drive policy | Configure |
    | &nbsp; | Configure encryption method for removable data-drives | AES 128bit CBC |
    | &nbsp; | Block write access to removable data-drives not protected by BitLocker | Yes |

7. In **Assignments**, assign the profile to the group that you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).
8. Select **Create** to create and assign the profile.

## Step 6 - Configure Windows Update settings

This step uses a Windows Update Ring to keep devices automatically updated. The settings in this guide align with the recommended settings in the Windows [Update Baseline](/windows/deployment/update/update-baseline).

Configure the Update ring in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage updates** > **Windows 10 and later updates** > **Update rings** tab > **Create profile**.
3. In **Basics**, enter a name for the update ring.
4. In **Update ring settings**, configure the following values and select **Next**:

    | Setting | Value |
    | --- | --- |
    | Servicing channel | Semi-annual channel |
    | Microsoft product updates | Allow |
    | Windows drivers | Allow |
    | Quality update deferral period (days) | 0 |
    | Feature update deferral period (days) | 0 |
    | Set feature update uninstall period | 10 |
    | Automatic update behavior | Reset to default |
    | Restart checks | Allow |
    | Option to pause Windows updates | Enable |
    | Option to check for Windows updates | Enable |
    | Require user approval to dismiss restart notification | No |
    | Remind user prior to required auto-restart with dismissible reminder (hours) | Leave this setting unconfigured |
    | Remind user prior to required auto-restart with permanent reminder (minutes) | Leave this setting unconfigured |
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
2. Select **Devices** > **Compliance** > **Create Policy**.
3. For **Platform**, select **Windows 10 and later** > **Create**.
4. In **Basics**, enter a name for the compliance policy. Select **Next**.
5. In **Compliance settings**, configure the following values, and select **Next**:

    | Setting category | Setting | Value |
    | --- | --- | --- |
    | **Device Health** | Require BitLocker | Require |
    | &nbsp; | Require Secure Boot to be enabled on the device | Require |
    | &nbsp; | Require code integrity | Require |
    | &nbsp; | &nbsp; | &nbsp; |
    | **System Security** | Firewall | Require |
    | &nbsp; | Antivirus | Require |
    | &nbsp; | Antispyware | Require |
    | &nbsp; | Require a password to unlock mobile devices | Require |
    | &nbsp; | Simple passwords | Block |
    | &nbsp; | Password type | Alphanumeric |
    | &nbsp; | Minimum password length | 8 |
    | &nbsp; | Maximum minutes of inactivity before password is required | 1 Minute |
    | &nbsp; | Password expiration (days) | 41 |
    | &nbsp; | Number of previous passwords to prevent reuse | 5 |
    | &nbsp; | &nbsp; | &nbsp; |
    | **Defender** | Microsoft Defender Antimalware | Require |
    | &nbsp; | Microsoft Defender Antimalware security intelligence up-to-date | Require |
    | &nbsp; | Real-time protection | Require |

6. In **Actions for noncompliance**, for the **Marking device noncompliant** action, configure **Schedule (days after noncompliance)** to `1` day. You can configure a different grace period based on your organization preferences.

    If you use Conditional Access policies in your organization, then it's recommended to configure a grace period. Grace periods prevent noncompliant devices from immediately losing access to organization resources.

7. You can add an action to email users informing them of noncompliance with steps to get compliant.
8. Assign the compliance policy to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Step 8 - Optional configurations

There are optional policies you can create and deploy with your cloud config. This section describes these optional policies.

### ✅ Configure a tenant domain name

Configure devices to automatically use your tenant's domain name for user sign-ins. When you add a domain name, users don't have to type their full UPN to sign in.

Add the tenant domain name in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. For platform, select **Windows 10 and later**.
4. For Profile type, select **Templates** > **Device restrictions** > **Create**.
5. Enter a name for the profile and select **Next**.
6. In **Configuration settings**, for **Password**, configure the **Preferred Microsoft Entra tenant domain**. Enter the Microsoft Entra domain name that users should use to sign in to devices.
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

For more information on these settings, go to [OneDrive settings recommended for Known Folder Move](/sharepoint/ideal-state-configuration).

### ✅ Configure recommended Microsoft Edge settings

There are some Microsoft Edge app settings that can be configured for a better user experience. You can configure these settings based on requirements or preference for the end user experience.

To configure these recommended settings, use Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Select **Windows 10 and later** for platform and **Templates** for profile type.
4. Select **Administrative Templates** and select **Create**.
5. Enter a name for the profile and select **Next**.
6. In **Configuration settings**, search for the following settings and configure them to their recommended values:

    | Setting Category | Setting | Value(s) |
    | --- | --- | --- |
    | &nbsp; | Configure Internet Explorer integration | Enabled, Internet Explorer mode |
    | &nbsp; | &nbsp; |
    | **SmartScreen settings** | Configure Microsoft Defender SmartScreen | Enabled |
    | &nbsp; | Force Microsoft Defender SmartScreen checks on downloads from trusted sources | Enabled |
    | &nbsp; | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |

    > [!NOTE]
    > The SmartScreen settings are also enforced by Microsoft Defender. When you configure the SmartScreen settings through the Microsoft Edge app, Microsoft Edge directly enforces the settings.

7. Assign the profile to the group you created in [Step 1 - Create a Microsoft Entra group](#step-1---create-a-microsoft-entra-group) (in this article).

## Monitor the status of cloud config

When you apply cloud config to your devices, you can use Intune to monitor the status of apps and device configurations.

### Script status

You can monitor the installation status of your deployed scripts:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **By platform** > **Windows** > **Scripts and remediations** > **Platform scripts**.
2. Select the script you deployed.
3. In the script details page, select **Device status**. The script installation details are shown.

### App installations

You can monitor the installation status of your deployed apps:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** > **Windows** > **Windows apps**.
2. Select an app you deployed, like the Microsoft 365 App Suite.
3. Select **Device install status** or **User install status**. The app installation details are shown.

For information on troubleshooting app issues on individual devices, go to [Troubleshooting Intune app installation issues](/troubleshoot/mem/intune/app-management/troubleshoot-app-install).

### Security baseline

You can monitor the installation status of your deployed security baseline. For more information, go to [Monitor security baselines and profiles in Intune](../protect/security-baselines-monitor.md).

### Disk encryption profile

In [Step 5 - Deploy endpoint security settings](#step-5---deploy-endpoint-security-settings) (in this article), you might have configured and deployed BitLocker settings.

You can monitor the status of this BitLocker profile:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Disk encryption**.
2. Select the disk encryption profile you deployed in cloud config.
3. Select **Device install status** or **User install status**. The profile details are shown.

### Windows Update settings

You can monitor the status of the Windows Update ring policy:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage updates** > **Windows 10 and later updates** > **Update rings** tab.
2. Select the update ring you deployed as part of cloud config.
3. Select **Device status**, **User status**, or **End user update status**. The update ring settings details are shown.

For more information on reporting for Windows Update rings, go to [Reports for Update rings for Windows 10 and later policy](../protect/windows-update-reports.md#reports-for-update-rings-for-windows-10-and-later-policy).

### Compliance policy

You can monitor the status of the compliance policy:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Compliance**.
2. Select the compliance policy you deployed as part of cloud config.

The device compliance monitoring view has detailed information on the assignment status and assignment failures of your compliance policies. It also has views to quickly find noncompliant devices and take action.

For more in-depth information on monitoring compliance policies in Intune, go to [Monitor results of your Intune Device compliance policies](../protect/compliance-policy-monitor.md).

## Related content

- [Windows cloud configuration guided scenario overview](cloud-configuration.md)
