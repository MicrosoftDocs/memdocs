---
# required metadata

title: Set up the Enrollment Status Page
titleSuffix: Microsoft Intune
description: Set up a greeting page for users signing in and enrolling Windows devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/02/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
 
# optional metadata
 
#ROBOTS:
#audience:

ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
---


 
# Set up the Enrollment Status Page  

**Applies to**
- Windows 10  
- Windows 11  
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
The Enrollment Status Page (ESP) displays provisioning progress after a new device is enrolled, and also when new users sign in to the device. The ESP provides a user interface so that the device user can monitor and track setup and enrollment progress. It locks the device during setup and doesn't let the user progress beyond the screen until provisioning is complete. 

You can show the enrollment status page during the default out-of-box experience (OOBE) for Azure AD Join, any [Windows Autopilot](../../autopilot/index.yml) provisioning scenario, or when new users sign into the device for the first time.  

To deploy the enrollment status page, you have to create an enrollment status page profile in Microsoft Intune. Within a profile, you can configure:   

- The visibility of installation progress
- Blocking device access until the provisioning process is completed
- Time limits
- Allowed troubleshooting operations  

This article describes how to create and edit a profile, and describes the information that the enrollment status page tracks.     


## Create new profile 

1. Select **Windows** > **Windows enrollment** > **Enrollment Status Page**.
2. Select **Create**.
3. In **Basics**, enter the following properties:  
     - **Name**: Name your profile so you can easily identify it later. 
     - **Description**: Enter a description for the profile. This setting is optional, but recommended.  
4. Select **Next**. 
5. In **Settings**, configure the following settings:  
 
    - **Show app and profile configuration progress**: Your options:
      - **No**: The enrollment status page doesn't appear during device setup. Select this option if you don't want to show the ESP to users.  
      - **Yes**: The enrollment status page appears during device setup.    
 
     - **Show an error when installation takes longer than specified number of minutes**: The default time-out is 60 minutes. Enter a higher value if you think more time is needed to install apps on your devices.      

     - **Show custom message when time limit or error occur**: Include a message that tells people what happened and who to contact for help. Your options:  
       - **No**: The default message is shown to users when an error occurs. That message is: "Setup could not be completed. Please try again or contact your support person for help."  
       - **Yes**: Your custom message is shown to users when an error occurs. Enter your message in the provided text box.  
 
     - **Turn on log collection and diagnostics page for end users**: The user's logs and diagnostics could aid with troubleshooting, so we recommend turning this on. Your options:  
       - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.  
       - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11.  
 
     - **Only show page to devices provisioned by out-of-box experience (OOBE)**: Your options:
       - **No**: The enrollment status page is shown on all Intune-managed and co-managed devices that go through the out-of-box experience (OOBE), and to the first user that signs in to each device. So subsequent users who sign in don't see the ESP. 
       - **Yes**: The enrollment status page is only shown on devices that go through the out-of-box experience (OOBE).   



       > [!TIP]
       > If you only want the ESP to appear on Autopilot devices during initial device setup, select the **No** option. Then create a new ESP profile, choose the **Yes** option, and target the profile to an Autopilot device group.  


     - **Block device use until all apps and profiles are installed**: Your options:
       - **No**: Users can leave the ESP before Intune is finished setting up the device. 
       - **Yes**: Users can't leave the ESP until Intune is done setting up the device. This option unlocks additional settings for this scenario.  
 
      - **Allow users to reset device if installation error occurs**: Your options:  
        - **No**: The ESP doesn't give users the option to reset theirs devices when an installation fails.  
        - **Yes**: The ESP gives users the option to reset their devices when an installation fails.  
 
      - **Allow users to use device if installation error occurs**: Your options:  
         - **No**: The ESP doesn't give users the option to bypass the ESP when an installation fails.  
         - **Yes**: The ESP gives users the option to bypass the ESP and use their devices when an installation fails.    
 
      - **Block device use until these required apps are installed if they are assigned to the user/device**: Your options:  
         - **All**: All assigned apps must be installed before users can use their devices.  
         - **Selected**: Select-apps must be installed before users can use their devices. Choose this option to select from your managed apps.  
 
6. Select **Next**.   
7. In **Assignments**, select the groups that will receive your profile. Optionally, select **Edit filter** to restrict the assignment further.   

    > [!NOTE]
    > Due to OS restrictions, a limited selection of filters are available for ESP assignments. The picker only shows filters that have rules defined for `osVersion`, `operatingSystemSKU`, and `enrollmentProfileName` properties. Filters that contain other properties aren't available.  

8. Select **Next**.  
 
9. Optionally, in **Scope tags**, assign a tag to limit profile management to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. Then select **Next**.   
 
10. In **Review + create**, review your settings. After you select **Create**, your changes are saved, and the profile is assigned. You can access the profile from your profiles list. 

  The next time each device checks in, the profile is applied.  

## Edit default profile 

Intune applies the default profile to all users and all devices when no other ESP profiles are available to assign. You can configure the default profile to show or hide the ESP.      
 
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices**.
2. Select **Windows** > **Windows enrollment** > **Enrollment Status Page**.  
2. Select the **Default** profile in the table.  
3. Select **Properties**. 
4. Go to the **Settings** section and select **Edit**.  
5. Configure **Show app and profile installation progress** to set the behavior of the default profile. Your options:
   * **No**: The ESP isn't visible to users during initial device setup and sign-in. 
   * **Yes**: The ESP is visible to users during initial device setup and sign-in.

   If you select **Yes**, more settings become available for you to configure.       
6. Select **Review + save**. 
7. Review the summary of changes and then select **Save**.   


## Prioritize profiles       
If you assign a user or device more than one ESP profile, the profile with the highest priority takes precedence over the other profiles.

 Intune applies profiles in the following order:  

1. Intune applies the highest-priority profile assigned to the device. 
2. If no profiles are targeted at the device, Intune applies the highest-priority profile assigned to the user. This only works in scenarios where there is a user. In white glove and self-deploying scenarios, only profiles targeted at devices can be applied.   
3. If no profiles are assigned to the device or user, Intune applies the default ESP profile.    

### Set priority  
To prioritize your profiles:  

1. Hover over the profile in the list with your cursor until you see three vertical dots.  
2. Drag the profile to the desired position in the list.  
 
### Scope tags  
  
Scope tags limit who can see and reprioritize an ESP profile. A scoped user can tell the relative priority of their profile even if they can't see all the other profiles in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).  

## Block access to a device until a specific application is installed

You can specify which apps must be installed before the Enrollment Status Page (ESP) completes.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Enrollment Status Page**.
2. Choose a profile > **Settings**.
3. Choose **Yes** for **Show app and profile installation progress**.
4. Choose **Yes** for **Block device use until all apps and profiles are installed**.
5. Choose **Selected** for **Block device use until these required apps are installed if they're assigned to the user/device**.
6. Choose **Select apps** > choose the apps > **Select** > **Save**.

The apps that are included in this list are used by Intune to filter the list that should be considered blocking.  It doesn't specify what apps should be installed.  For example, if you configure this list to include "App 1," "App 2," and "App 3" and "App 3" and "App 4" are targeted to the device or user, the Enrollment Status Page will track only "App 3."  "App 4" will still be installed, but the Enrollment Status Page will not wait for it to complete.

A maximum of 100 apps can be specified.

## Enrollment Status Page tracking information  

There are three phases where the Enrollment Status Page tracks information for; device preparation, device setup, and account setup.

### Device preparation

For device preparation, the enrollment status page tracks:

- Trusted Platform Module (TPM) key attestation (when applicable)
- Azure Active Directory join process
- Intune (MDM) enrollment
- Installation of the Intune Management Extensions (used to install Win32 apps)

### Device setup

The Enrollment Status Page tracks the following device setup items:

- Security policies
  - Microsoft Edge, Assigned Access, and Kiosk Browser policies are presently tracked.
  - Other policies aren't tracked.
- Applications
  - Per machine Line-of-business (LoB) MSI apps.
  - LoB store apps with installation context = Device.
  - Offline store and LoB store apps with installation context = Device.
  - Win32 applications (Windows 11 and Windows 10 version 1903 and later only) 

  > [!NOTE]
  > It's preferable to deploy the offline-licensed Microsoft Store for Business apps. Don't mix LOB and Win32 apps. Both LOB (MSI) and Win32 installers use TrustedInstaller, which doesn't allow simultaneous installations. If the OMA DM agent starts an MSI installation, the Intune Management Extension plugin starts a Win32 app installation by using the same TrustedInstaller. In this situation, Win32 app installation fails and returns an **Another installation is in progress, please try again later** error message. In this situation, ESP fails. Therefore, don't mix LOB and Win32 apps in any type of Autopilot enrollment.
  > 

- Connectivity profiles
  - VPN or Wi-Fi profiles that are assigned to **All Devices** or a device group in which the enrolling device is a member, but only for Autopilot devices
- Certificate profiles that are assigned to **All Devices** or a device group in which the enrolling device is a member, but only for Autopilot devices

### Account setup

For account setup, the Enrollment Status Page tracks the following items if they're assigned to the current logged in user:

- Security policies
  - Microsoft Edge, Assigned Access, and Kiosk Browser policies are presently tracked.
  - Other policies aren't tracked.
- Applications
  - Per user LoB MSI apps that are assigned to All Devices, All Users, or a user group in which the user enrolling the device is a member.
  - Per machine LoB MSI apps that are assigned to All Users or a user group in which the user enrolling device is a member.
  - LoB store apps, online store apps, and offline store apps that are assigned to any of the following objects:
    - All Devices
    - All Users
    - A user group in which the user enrolling the device is a member with installation context set to User.
  - Win32 applications (Windows 10 version 1903 and newer only) 
- Connectivity profiles
  - VPN or Wi-Fi profiles that are assigned to All Users or a user group in which the user enrolling the device is a member.
- Certificates
  - Certificate profiles that are assigned to All Users or a user group in which the user enrolling the device is a member.

### Known issues

The following are known issues related to the Enrollment Status Page.
- When creating apps that will be deployed during ESP, any reboots that are packaged within the app may cause ESP to hang and fail the deployment. We recommend specifying the reboot behavior in Intune instead of triggering the reboot within the package. 
- Disabling the ESP profile doesn't remove ESP policy from devices and users still get ESP when they log in to device for first time. The policy isn't removed when the ESP profile is disabled. 
- A reboot during Device setup will force the user to enter their credentials before transitioning to Account setup phase. User credentials aren't preserved during reboot. Have the user enter their credentials then the Enrollment Status Page can continue. 
- Enrollment Status Page will always time out during an Add work and school account enrollment on Windows 10 versions earlier than 1903. The Enrollment Status Page waits for Azure AD registration to complete. The issue is fixed on Windows 10 version 1903 and newer.  
- Hybrid Azure AD Autopilot deployment with ESP takes longer than the timeout duration entered in the ESP profile. On Hybrid Azure AD Autopilot deployments, the ESP will take 40 minutes longer than the value set in the ESP profile. For example, you set the timeout duration to 30 minutes in the profile. The ESP can take 30 minutes + 40 minutes.

  This delay gives time for the on-prem AD connector to create the new device record to Azure AD.
  
- Windows logon page isn't pre-populated with the username in Autopilot User Driven Mode. If there's a reboot during the Device Setup phase of ESP:
  - the user credentials aren't preserved
  - the user must enter the credentials again before proceeding from Device Setup phase to the Account setup phase
- ESP is stuck for a long time or never completes the "Identifying" phase. Intune computes the ESP policies during the identifying phase. A device may never complete computing ESP policies if the current user doesn't have an Intune licensed assigned.  
- Configuring Microsoft Defender Application Control causes a prompt to reboot during Autopilot. Configuring Microsoft Defender Application (AppLocker CSP) requires a reboot. When this policy is configured, it may cause a device to reboot during Autopilot. Currently, there's no way to suppress or postpone the reboot.
- When the [DeviceLock policy](/windows/client-management/mdm/policy-csp-devicelock) is enabled as part of an ESP profile, the OOBE or user desktop autologon could fail unexpectantly for two reasons.
  - If the device didn't reboot before exiting the ESP Device setup phase, the user may be prompted to enter their Azure AD credentials. This prompt occurs instead of a successful autologon where the user sees the Windows first login animation.
  - The autologon will fail if the device rebooted after the user entered their Azure AD credentials but before exiting the ESP Device setup phase. This failure occurs because the ESP Device setup phase never completed. The workaround is to reset the device.
- ESP doesn't apply to a Windows device that was enrolled with Group Policy (GPO).
- Scripts that run in user context ('Run this script using the logged on credentials' on the script properties is set to 'yes') may not execute during ESP.  As a workaround, execute scripts in System context by changing this setting to 'no'.

## Troubleshooting  

For troubleshooting help, including how to disable an already-enabled ESP, see [Troubleshoot the Windows Enrollment Status page](/troubleshoot/mem/intune/understand-troubleshoot-esp#troubleshooting).  
