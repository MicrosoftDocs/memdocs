---
# required metadata

title: Windows cloud configuration setup guide
description: Use this Windows 10/11 cloud configuration setup guide to create your own cloud configuration deployment and policies using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/22/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
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

# Cloud config setup guide
## Introduction
This document outlines the configuration recommendations for Windows 10 / 11 in cloud configuration ("cloud config"). Cloud config is a cloud-optimized Windows device configuration for Windows 10 / 11 devices designed to simplify the end user experience and the IT endpoint management experience. You can find out more about cloud config [here](https://aka.ms/cloudconfigguiide).

You can deploy cloud config using a [guided scenario in the Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2249463).

You can also use the steps in this document to deploy cloud config yourself. Windows 10 / 11 in cloud configuration will: 
- Optimize devices for the cloud by configuring them to enroll into Intune management with Azure Active Directory. User data is stored in OneDrive automatically with Known Folder Move configured.
- Install Microsoft Teams and Microsoft Edge on devices. 
- Configure end users to be standard users on devices, giving IT more control over the apps installed on devices. 
- Remove built-in apps and the Microsoft Store app, simplifying the end user experience. 
- Apply endpoint security settings and a compliance policy to help keep devices secure and help IT monitor device health. 
- Ensure that devices are automatically updated through Windows Update for Business.
- You can also optionally configure:
  -   Additional Microsoft 365 applications (such as Outlook, Word, Excel, PowerPoint).
  -   Essential line-of-business apps that end users need to be successful. Microsoft recommends keeping these apps to a minimum to keep the configuration simple.
  -   Essential resources such as Wi-Fi profiles, VPN connections, certificates, and printer drivers that are necessary for users’ workflows. 

The following sections describe how to use Microsoft Intune to set up this configuration, covering these key steps: 
  1.	Create a Microsoft Entra ID group 
  2.	Configure device enrollment
  3.	Deploy a script to configure Known Folder Move and remove built-in apps
  4.	Deploy apps
  5.	Deploy endpoint security settings
  6.	Configure Windows Update settings
  7.	Deploy a Windows compliance policy
  8.	Additional optional configurations
     
## Step 1: Create a Microsoft Entra ID group 
Create a Microsoft Entra ID security group that will receive the configurations you deploy in this document. This dedicated group will help you organize devices and easily manage your cloud config resources in Microsoft Intune. Microsoft recommends starting by deploying only the configurations recommended in this guide, and adding on essential apps and other device configurations as necessary. 
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Groups** > **All groups** > **New group**.
  3.	For **Group type**, select **Security**.
  4.	Enter a Group name. For example, “Cloud config PCs”.
  5.	For **Membership type**, select **Assigned**.
  6.	You can add devices to your new group now if you want. Select **No members selected** and add to your group using the selector. You can also start with an empty group now and add devices later anytime.
  7.	Select **Create**.

In the next steps, you will create configurations that you will assign to this group. You can add these devices to this group that will receive cloud config: 
  •	Pre-registered Windows Autopilot devices 
  •	Devices that you have already enrolled. 

It's recommended to remove apps and profiles you might have already targeted to devices, and resetting and re-enrolling these devices after deploying cloud config to start fresh. This will provide the most streamlined user experience. You can then add additional essential apps and ensure devices have just what users need while keeping the device configuration standardized. 

## Step 2: Configure Device Enrollment 
### Enable MDM Automatic enrollment 

Enable automatic enrollment for the users in your organization that you want to use cloud config. 

  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Devices** > **Overview** > **Windows** > **Windows enrollment** and select **Automatic Enrollment**. 
  3.	Under **MDM user scope**, select one of the following:
      i. Select **Some** if you want to apply the cloud configuration to devices used by a subset of users in your organization. Select the groups of users that will use devices with the cloud configuration applied.
    	**Note:** At a minimum, select the users for whom you would like to apply the cloud configuration. You can enable auto-enrollment for more users. [Learn more about Windows automatic enrollment](https://go.microsoft.com/fwlink/?linkid=2153696).
    	ii.	Select **All** if you want to apply the cloud configuration to all Windows devices that users in your organization will use.
  4. Select **Save** to save your changes.
  5. AM settings are not configured as part of this setup. The settings for MAM user scope, MAM terms of user URL, MDM discovery URL, and MAM compliance URL can be left unchanged.

### Choose how devices will be enrolled and configure users to be standard users on devices

Select one of the following options for how to enroll devices and configure users as standard users on their devices. 

#### Enrollment Option 1: Windows Autopilot user-driven enrollment (recommended) 
Pre-register devices using Windows Autopilot to configure how they will start up and enroll into device management. It is recommended to use Autopilot enrollment and the Enrollment Status Page so admins can get devices ready to go before they have been enrolled. This enrollment method provides a consistent end user experience by displaying a status page during device setup while cloud config is fully applied. 

##### Add Windows Autopilot devices 
Follow the instructions to [register devices to Windows Autopilot](https://go.microsoft.com/fwlink/?linkid=2153584) to add your pre-registered Autopilot devices to Intune (the other necessary steps in that document are covered in this document with specific recommended settings, using the group you created in Step 1 to assign devices).

Register devices to Autopilot - Enrollment in Intune with Windows Autopilot - Windows Education | Microsoft Learn

You can [manually register devices to use Windows Autopilot](https://go.microsoft.com/fwlink/?linkid=2153585). You may be doing this if you are repurposing existing hardware that you had previously not set up with Autopilot.

##### Create and assign a Windows Autopilot deployment profile 
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Devices** > **Windows** > **Windows enrollment** > **Windows Autopilot Deployment Program** > **Deployment profiles** 
  3.	Select **Create profile** > **Windows PC**. Enter a name for the profile. 
  4.	For the setting **Convert all targeted devices to Autopilot**, select **Yes** and Select **Next**. 
You can apply cloud config to devices enrolled using enrollment methods other than Autopilot. When you add those devices to your group, they will be converted to Autopilot. The next time they go through the Windows Out of Box Experience (OOBE) after being reset, they will enroll through Autopilot. 
  5.	In the **Out-of-box experience (OOBE)** tab, enter the following values and then select **Next**: 

| Setting	| Value |
| --- | --- |
| Deployment mode |	User-driven |
| Join to Azure AD as	| Azure AD joined |
| Microsoft Software License Terms | Hide |
| Privacy settings	| Hide |
| Hide change account options	| Hide |
| User account type	| Standard |
| Allow pre-provisioned deployment	| No |
| Language (Region)	| Operating system default |
| Automatically configure keyboard	| Yes |
| Apply device name template	| (Optional) You can apply a device name template. Use a name prefix that can help you identify your devices with this configuration, for example: Cloud-%SERIAL% |

  5.	Assign the profile to the group you created in Step 1 (Create a Microsoft Entra ID group), and then select **Next**. 
  6.	Review the new profile and then select **Create**. 

##### Create and assign an Enrollment Status Page
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Devices** > **Windows** > **Windows enrollment** > **General** > **Enrollment Status Page **
  3.	Select **Create** and enter a name for this **Enrollment Status Page**. 
  4.	In the **Settings** tab, enter the following values and then select **Next**. 

| Setting |	Value |
| --- | --- |
| Show app and profile configuration process |	Yes |
| Show an error when installation takes longer than specified number of minutes	| 60 |
| Show custom message when time limit error occurs	| Yes (you can modify the default message) | 
| Allow users to collect logs about installation errors	| Yes | 
| Block device user until all apps and profiles are installed	| Yes | 
| Allow users to reset device if installation error occurs	| Yes | 
| Allow users to use device if installation error occurs | 	No | 
| Block device user until these required apps are installed if they are assigned to the user/device |	All | 


> [!NOTE]  
> It's recommended to block users from using the device if an installation error occurs to ensure they can only get started after cloud config is fully applied. Based on your deployment needs, you can allow the user to use the device even if an installation error occurs. If you do this, Intune will continue to attempt to apply configurations when the device checks in with Intune again. 


  4.	In the **Assignments** tab, assign the Enrollment Status Page to the group you created in Step 1 (Create a Microsoft Entra ID group), and then select **Next**. 
  5.	Select **Create** to create and assign the Enrollment Status Page. 

#### Alternative device enrollment options 
It's recommended to use Autopilot to pre-configure device settings and keep the user on a status page before all configurations are applied to the device. The following alternative options are available, with some differing steps to ensure users are standard users on their devices. If you configured device enrollment through Windows Autopilot, skip to the next step. 

#### Enrollment Option 2: Bulk enrollment using a provisioning package 
You can enroll devices using a provisioning package created using Windows Configuration Designer or the Set up School PCs app. Using this enrollment method, all users are automatically standard users on the device. 

[Learn more about bulk enrollment for Windows devices. ](https://go.microsoft.com/fwlink/?linkid=2153476)

With this enrollment method, you will need to add devices to the group you created at the beginning of this process after they are enrolled so they can receive cloud config. There is no Enrollment Status Page displayed with this enrollment option, so users can’t see progress as all cloud configuration settings are delivered and may start using the device before it is fully applied. Microsoft recommends that IT verify that devices have settings and apps delivered before distributing devices to users. 

#### Enrollment Option 3: Enrollment via Microsoft Entra ID sign-in in the Out-of-box Experience (OOBE) 
With MDM Auto-enrollment enabled in your environment, users can enroll devices by simply signing in with their Microsoft Entra ID accounts during OOBE. With this enrollment method, you configure a custom profile using Microsoft Intune to restrict local administrators on devices. Be sure to specify a group containing only IT administrators in your environment to be local administrators. [Policy CSP documentation](https://go.microsoft.com/fwlink/?linkid=2153477) includes sample policy definition XML that you use in your custom profile. Assign the custom profile you create to the group you created in Step 1.  

## Step 3: Configure OneDrive Known Folder Move and deploy a script to remove built-in apps 

This step helps simplify the Windows user experience. When you configure OneDrive Known Folder Move, user files and data are automatically saved in OneDrive. When you remove built-in Windows 10 apps and the Microsoft Store, the Start menu and device experience are simplified. 
### Configure OneDrive Known Folder move with an Administrative Template

> [!NOTE]  
> Due to a sync issue with OneDrive Known Folder Move and SharedPC configuration, Microsoft does not recommend using Windows in cloud configuration with a device on which multiple users will be signing in and out. 

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2. Select **Devices** > **Windows** > **Configuration profiles** > **Create profile**
  3.	Select **Windows 10 and later** for platform and select **Templates** for profile type.
  4.	Select **Administrative Templates** and select **Create**.
  5.	Enter a name for the profile and select **Next**.
  6.	In the **Configuration settings** tab, search for the settings in the following table and select their recommended values.

> [!NOTE]  
> Your tenant ID can be found in the Tenant ID box on the [Properties page](https://go.microsoft.com/fwlink/?linkid=2155017) in the Microsoft Entra admin center.

| Setting name | Value |
| --- | --- |
| Silently move Windows known folders to OneDrive Enabled Tenant ID | Enter your organization’s tenant ID |
| Show notification to users after folders have been redirected | Yes (you can choose to hide the notification) |
| Silently sign in users to the OneDrive sync app with their Windows credentials | Enabled |
| Prevent users from moving their Windows known folders to OneDrive | Enabled |
| Prevent users from redirecting their Windows known folders to their PC | Enabled |
| Use OneDrive Files On-Demand | Enabled |
  7. Assign the profile to the group you created at the start of this process.
   
### Deploy a script to remove built-in apps 
Microsoft has created a PowerShell script that will remove built-in apps when deploying cloud config. Use the following steps to deploy it. The script also removes the Microsoft Store app from devices to further simplify the user experience. 

> [!NOTE]  
> If you want to keep the Microsoft Store on devices, you can deploy the alternate script that removes built-in apps but keeps the Microsoft Store. If you have already removed the Microsoft Store, you can redeploy it using Microsoft Intune and the Microsoft Store for Business or Microsoft Store for Education. You can also block end users from installing Store apps outside of your organization’s private store on Windows 10 / 11 Enterprise and Windows 10 / 11 Education. See Step 8: Additional optional configuration in this document for more details.
> 
> You can redeploy individual apps that are removed using this script by adding them to your Microsoft Store for Business or Microsoft Store for Education inventory and assigning them to devices using Microsoft Intune. If you do this, Microsoft recommends also keeping the Store app on devices to ensure Store apps stay updated. The provided script will attempt to remove built-in apps but may not remove all of them. You may need to modify the script to remove all built-in apps on your devices. 

  1.	[Download the PowerShell script here](https://go.microsoft.com/fwlink/?linkid=2153583). 
     An alternate version of the recommended script which removes built-in apps, but keeps the Microsoft Store, is available [here](https://go.microsoft.com/fwlink/?linkid=2157781). 

> [!NOTE]  
> The cloud config guided scenario in the Microsoft Intune admin center deploys the recommended script that removes the Microsoft Store along with built-in apps. If you use the guided scenario to deploy cloud config but want to deploy the alternate script, delete the script deployed through the guided scenario and replace it with the alternate script by following these steps. Assign the alternate script to the same group you deployed cloud config to using the guided scenario. 

  2.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  3.	Select **Devices** > **Windows** >  **Scripts** > **Platform scripts** > **Create** to create a new script. 
  4.	In the **Basics** tab, enter a name for your script and select **Next**. 
  5.	In the **Script settings** tab, upload the script you downloaded in Step 1. Leave the other settings unchanged and select **Next**. 
  6.	Assign the script to the group you created in Step 1 (Create a Microsoft Entra ID group).
   
## Step 4: Deploy apps 
### Microsoft Edge 
  1.	Follow the steps at [add Microsoft Edge for Windows 10 to Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2152870).
  2.	For **App settings**, select the Stable Channel. 
  3.	Assign the Edge app to the group you created in Step 1 (Create a Microsoft Entra ID group). 

### Microsoft Teams and additional Microsoft 365 apps 
#### Configure Teams installation through the Microsoft 365 Suite app in Intune. 
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Apps** > Windows. 
  3.	Select **Add** to create a new app. 
  4.	For **Microsoft 365 Apps**, select **Windows 10 and later** and select **Select**. 
  5.	Enter a name for **Suite Name** or leave the suggested name unchanged. Select **Next**. 
  6.	For **Configure app suite**, unselect all apps except for Teams.
     
> [!TIP]  
   > Optional: If you want to deploy additional Microsoft 365 apps, choose them from this list:  
   >
   > - Excel, OneNote, Outlook, PowerPoint, Word

> [!NOTE]  
> You don’t need to choose OneDrive from this list. It’s built in to Windows 10 / 11 Pro, Enterprise, and Education.

  7.	For **App suite information**, configure these settings:

| Setting | Value | 
| --- | --- |
| Architecture | 64-bit (cloud config also works with 32-bit. Microsoft recommends choosing 64-bit.) |
| Update channel | Current channel | 
| Remove other versions | Yes |
| Version to install | Latest |

  7.	For **Properties**, configure these settings:

| Setting | Value |
| --- | --- |
| Use shared computer activation | Yes |
| Accept the Microsoft Software License Terms on behalf of users | Yes|
  
  9. Select **Next**.
  10. Assign the suite to the group you created in Step 1 (Create a Microsoft Entra ID group).
   
## Step 5: Deploy endpoint security settings 
### Deploy the Windows [security baseline](https://go.microsoft.com/fwlink/?linkid=2249271) 
For Windows in cloud configuration, it is recommended to use the default Windows security baseline configurable in Microsoft Intune, with a few settings changed based on your organization’s preference. 
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Endpoint security** > **Security baselines** > **Security baseline for Windows 10 and later**. 
  3.	Select **Create profile** to create a new security baseline. 
  4.	Enter a name for your security baseline and select **Next**. 
  5.	Accept the default configuration settings by selecting **Next**. 
You can adjust some of the following settings based on your organization’s needs: 
| Setting category | Setting | Reason for changing |
| --- | --- | --- |
| Browser | Block Password Manager | You might consider allowing end users to use password managers. |
| Remote Assistance | Remote Assistance solicited | You may need to configure these settings if you want to allow your support staff to remotely connect to devices to assist with issues. Microsoft recommends keeping this disabled unless it is required. |
| Firewall | All Firewall settings | Consider changing the default Firewall settings if you need to allow certain connections to devices based on your organization’s needs. |

  6.	In the Assignments tab, select the group that you created in Step 1 (Create a Microsoft Entra ID group).
  7.	Select **Create** to create and assign the baseline. 

### Deploy additional BitLocker settings with a drive encryption endpoint security profile 
Some additional BitLocker settings help keep your devices secure. 
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Endpoint security** > **Disk encryption** > **Create Policy**. 
  3.	For Platform, select **Windows 10 and later**. 
  4.	For Profile, select **BitLocker** and select **Create**. 
  5.	In the Basics tab, enter a name for your profile. 
  6.	In the Configuration settings tab, select the following settings.

| Setting category | Setting | Value |
| --- | --- | --- |
| BitLocker – Base settings | Enable full disk encryption for OS and fixed data drives | Yes |
| BitLocker – Fixed Drive Settings | BitLocker fixed drive policy | Configure |
| | Block write access to fixed data drives not protected by BitLocker | Yes |
| | Configure encryption method for fixed data-drives | AES 128bit XTS |
| BitLocker – OS Drive Settings | BitLocker system drive policy | Configure |
| | Startup authentication required | Yes |
| | Compatible TPM startup | Allowed |
| | Compatible TPM startup PIN | Allowed |
| | Compatible TPM startup key | Required |
| | Compatible TPM startup key and PIN | Allowed |
| | Disable BitLocker on devices where TPM is incompatible | Yes |
| | Configure encryption method for Operating System drives | AES 128bit XTS |
| BitLocker – Removable Drive Settings | BitLocker removable drive policy | Configure |
| | Configure encryption method for removable data-drives | AES 128bit CBC |
| | Block write access to removable data-drives not protected by BitLocker | Yes |
 
  7.	In the Assignments step, assign the profile to the group that you created in Step 1 (Create a Microsoft Entra ID group). 
  8.	Select **Create** to create and assign the profile.
   
## Step 6: Configure Windows Update settings 
### Windows Update Ring 
Configure a Windows update ring to keep devices automatically updated. The settings in this guide align with the recommended settings in the Windows [Update Baseline](https://go.microsoft.com/fwlink/?linkid=2249660).

  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Devices** > **Update rings for Windows 10 and later** > **Create profile**. 
  3.	In the **Basics** tab, enter a name for the update ring. 
  4.	In the **Update ring settings** tab, configure the following values and select **Next**.

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

  6.	Assign the Update Ring to the group you created in Step 1 (Create a Microsoft Entra ID group).
   
## Step 7: Deploy a Windows compliance policy 
Configure a compliance policy to help monitor device compliance and health. The policy will be configured to report on noncompliance while still allowing users to use devices. You can choose how to address noncompliance with additional actions based on the organization’s processes.
  1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2.	Select **Devices** > **Compliance Policies** > **Policies** > **Create Policy**. For **Platform**, select **Windows 10 and later** > **Create**. 
  3.	In the **Basics** tab, enter a name for the compliance policy and select **Next**. 
  4.	In the **Compliance settings** tab, configure the following values and select **Next**.

| Setting category | Setting | Value |
| --- | --- | --- |
| Device Health | Require BitLocker | Require |
| | Require Secure Boot to be enabled on the device | Require |
| | Require code integrity | Require |
| System Security | Firewall | Require |
| | Antivirus | Require |
| | Antispyware | Require |
| | Require a password to unlock mobile devices | Require |
| | Simple passwords | Block |
| | Password type | Alphanumeric |
| | Minimum password length | 8 |
| | Maximum minutes of inactivity before password is required | 1 Minute |
| | Password expiration (days) | 41 |
| | Number of previous passwords to prevent reuse | 5 |
| Defender | Microsoft Defender Antimalware | Require |
| | Microsoft Defender Antimalware security intelligence up-to-date | Require |
| | Real-time protection | Require | 

  5.	In the **Actions for noncompliance** tab, for the Action “Marking device noncompliant”, configure Schedule (days after noncompliance) to 1 (day). You can configure a different grace period based on your organization’s preferences. If you are using Conditional Access policies in your organization, it is recommended to configure a grace period so noncompliant devices do not immediately lose access to organization resources. 
  6.	You can add an action to email users informing them of noncompliance with instructions on remediation. 
  7.	Assign the compliance policy to the group you created in Step 1 (Create a Microsoft Entra ID group). 

## Step 8: Optional additional configuration 
### Deploy additional essential productivity and line-of-business apps 
You may have a few essential line-of-business apps that all devices need. Choose a minimum number of these apps to deploy. If you are delivering apps through a virtualization solution, deploy the virtualization client app to devices. 
While there are no restrictions on the number or size of additional apps that can be deployed on top of the other apps defined in the cloud configuration, Microsoft recommends keeping these additional apps to a minimum based on what users need for their roles. Assign these essential apps to the group you created at the start of this process. 

You may find that you need to deploy several line-of-business to some of your devices, or that these apps have complex packaging or procedure requirements. Consider moving these apps out of your cloud config deployment or keeping the devices that need these apps in your existing Windows management model. Cloud config is recommended for devices that need just a few key apps on top of collaboration and browsing. 

### Deploy resources that users might need to access organization resources 
Be sure to configure essential resources that users may need depending on your organization’s processes. These include certificates, printers, VPN connections, and Wi-Fi profiles. In Microsoft Intune, assign these resources to the group you created at the start of this process. 

### Configure preferred tenant domain name 
Configure devices to automatically use your tenant’s domain name for user sign-ins, so users don’t have to type their whole UPN to sign in. 
1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2.	Select **Devices** > **Windows** > **Configuration profiles** and select **Create profile**. 
3.	For platform, select **Windows 10 and later**. For Profile type, select **Templates** > **Device restrictions** > **Create**. 
4.	Enter a name for the profile and select **Next**. 
5.	In the **Configuration settings** tab, for **Password**, configure the **Preferred Microsoft Entra ID tenant domain** – enter the domain name that users will use to sign in to devices. 
6.	Assign the profile to the group you created at the start of this process.

### Configure recommended settings for OneDrive Known Folder Move 
Refer to this document with [additional OneDrive settings recommended for Known Folder Move](https://go.microsoft.com/fwlink/?linkid=2153589). These are not required configurations for Known Folder Move to work, but may help provide a better user experience. 

#### Configure recommended Edge app settings 
A few app settings for Edge can be configured to provide the best user experience. The following table lists the recommended settings. You can configure additional settings based on requirements or preference for the user experience. The SmartScreen settings are also enforced by Microsoft Defender. Configuring them through the Edge app will enable the Edge app to enforce them directly. 

| Setting Category | Setting | Value(s) | 
| --- | --- | --- |
| N/A | Configure Internet Explorer integration | Enabled, Internet Explorer mode |
| SmartScreen settings | Configure Microsoft Defender SmartScreen | Enabled | 
| SmartScreen settings | Force Microsoft Defender SmartScreen checks on downloads from trusted sources | Enabled | 
| SmartScreen settings | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |

Follow these steps to configure these recommended settings: 

1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2.	Select to **Devices** > **Windows** > **Configuration profiles** > **Create profile**.
3.	Select **Windows 10 and later** for platform and **Templates** for profile type.
4.	Select **Administrative Templates** and select **Create**. 
5.	Enter a name for the profile and select **Next**. 
6.	In the **Configuration settings** tab, search for the settings in the table above and configure them to their recommended values. 
7.	Assign the profile to the group you created at the start of this process.
   
### Redeploy the Microsoft Store app if needed 
If you removed the Microsoft Store using the recommended script in Step 3 and you want to restore it, you can do so using Microsoft Intune and the Microsoft Store for Business or Microsoft Store for Education. Add the Microsoft Store app to your organization’s app inventory and deploy it to devices using Microsoft Intune. 

[Learn more about how to deploy Microsoft Store apps using Microsoft Store for Business or Microsoft Store for Education](https://go.microsoft.com/fwlink/?linkid=2157972).
[Get the Microsoft Store app on the Microsoft Store for Business](https://go.microsoft.com/fwlink/?linkid=2157677). 
[Get the Microsoft Store app on the Microsoft Store for Education](https://go.microsoft.com/fwlink/?linkid=2157678).

#### Block users from installing Microsoft Store apps on Windows 10 / 11 Enterprise and Windows 10 / 11 Education 
If you keep or redeploy the Microsoft Store on devices, you can prevent users from installing apps outside of your organization’s private store on Windows 10 / 11 Enterprise and Windows 10 / 11 Education. 
1.	Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2.	Select **Devices** > **Windows** > **Configuration profiles** > **Create profile**. 
3.	Select **Windows 10 and later** for platform and select **Settings catalog** for profile type. Select **Create**. 
4.	In the **Basics** tab, enter a name for your profile. 
5.	In the **Configuration settings** tab, select **Add settings**. 
6.	In the settings picker, search for “private store”. In the search results under the Microsoft App Store category, select **Require Private Store Only**. 
7.	In the **Configuration settings** tab, set the **Require Private Store Only** setting to **Only Private store is enabled** and select **Next**. 
8.	In the **Assignments** tab, assign the profile to the group you created in Step 1. 
9.	In the **Review + create** tab, review your profile and select **Create**.

## Monitoring the status of cloud config 
Now that you have applied cloud config to your devices, you can use Microsoft Intune to monitor the status of apps and device configurations. 

### Script status 
Use Microsoft Intune to monitor the installation status of the script deployed to remove built-in Windows apps. In Microsoft Intune, go to Devices > Windows > PowerShell scripts and select the script you deployed from the list. In the script details page, choose Device status to view details on the installation of the script on managed devices. 

### App installations 
App installation status can be monitored by navigating to an app in Microsoft Intune and checking its device and/or user install status. 
In Microsoft Intune, go to Apps > Windows > Windows apps. Select one of the apps that you deployed as part of the cloud configuration (for example, the Microsoft 365 App Suite). Choose Device install status or User install status to view details on the installation status of the app. 
You can also use [troubleshooting tools to diagnose issues](https://go.microsoft.com/fwlink/?linkid=2153588) that individual devices or users may be experiencing. 

### Security baseline 
You can use the Microsoft Intune admin center to [monitor the status of the security baseline](https://go.microsoft.com/fwlink/?linkid=2153695) you deployed.

### Disk encryption profile (additional BitLocker settings) 
In the Microsoft Intune admin center, select **Endpoint security** > **Disk encryption** and select the disk encryption profile you deployed as part of cloud config. Select **Device install status** or **User install status** to view details on the installation status of the profile. 

### Windows Update settings 
In the Microsoft Intune admin center, select **Devices** > **Update rings for Windows 10 and later** and select the update ring you deployed as part of cloud config. Select **Device status**, **User status**, or **End user update status** to monitor the status of your update ring settings. 

### Compliance policy 
Monitor device health using Microsoft Intune to assess and take action on devices in a noncompliant state. In the Microsoft Intune admin center, from the Dashboard, select the **Device compliance** tile on the default dashboard. The device compliance monitoring view provides detailed information on the assignment status and assignment failures of your compliance policies, along with views to quickly find noncompliant devices and take action.
