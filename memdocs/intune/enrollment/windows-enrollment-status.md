---
# required metadata

title: Set up the Enrollment Status Page in the admin center
titleSuffix: Microsoft Intune
description: Set up a greeting page for users signing in and enrolling Windows devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/02/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
 
# optional metadata
 
#ROBOTS:
#audience:

ms.reviewer: jubaptis
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---


 
# Set up the Enrollment Status Page  

**Applies to**
- Windows 10  
- Windows 11  
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
The enrollment status page (ESP) displays the provisioning status to people enrolling Windows devices and signing in for the first time. You can configure the ESP to block device use until all required policies and applications are installed. Device users can look at the ESP to track how far along their device is in the setup process. 

The ESP can be deployed during the default out-of-box experience (OOBE) for Azure Active Directory (Azure AD) Join, and any [Windows Autopilot](../../autopilot/index.yml) provisioning scenario.  

To deploy the ESP to devices, you have to create an ESP profile in Microsoft Intune. Within the profile, you can configure the ESP settings that control:  

- Visibility of installation progress indicators     
- Device access during provisioning   
- Time limits  
- Allowed troubleshooting operations    

This article describes the information that the enrollment status page tracks and how to create an ESP profile.

## Windows CSP  
ESP uses the [EnrollmentStatusTracking configuration service provider (CSP)](/windows/client-management/mdm/enrollmentstatustracking-csp) and [FirstSyncStatus CSP](/windows/client-management/mdm/dmclient-csp) to track app installation.  

## Create new profile 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices**.
2. Select **Windows** > **Windows enrollment** > **Enrollment Status Page**.
3. Select **Create**.
4. In **Basics**, enter the following properties:  
     - **Name**: Name your profile so you can easily identify it later. 
     - **Description**: Enter a description for the profile. This setting is optional, but recommended.  
5. Select **Next**. 
6. In **Settings**, configure the following settings:  
 
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
 
     - **Only show page to devices provisioned by out-of-box experience (OOBE)**: Use this setting to stop the enrollment status page from reappearing to every new user who signs into the device. Your options:  
       - **No**: The enrollment status page is shown during the device phase and the out-of-box experience (OOBE). The page is also shown during the [user phase](#account-setup) to every user who signs into the device for the first time.  
       - **Yes**: The enrollment status page is shown during the device phase and the OOBE. The page is also shown during the user phase, but only to the first user who signs into the device. It is not shown to subsequent users who sign into the device.   

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

      - **Only fail selected blocking apps in technician phase**: Your options:  
         - **No**: Only blocking apps will fail deployment during the technician phase of pre-provisioning.   
         - **Yes**: Intune will attempt to install required apps targeted to the device, or user (if assigned and installed in device context), during the technician phase of pre-provisioning. If installation is unsuccessful, these apps won't fail the deployment unless they are part of the blocking apps you previously selected. 
 
6. Select **Next**.   
7. In **Assignments**, select the groups that will receive your profile. Optionally, select **Edit filter** to restrict the assignment further.   

    > [!NOTE]
    > Due to OS restrictions, a limited selection of filters are available for ESP assignments. The picker only shows filters that have rules defined for `osVersion`, `operatingSystemSKU`, and `enrollmentProfileName` properties. Filters that contain other properties aren't available.  

8. Select **Next**.  
 
9. Optionally, in **Scope tags**, assign a tag to limit profile management to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. Then select **Next**.   

    > [!NOTE]
    > Scope tags limit who can see and reprioritize ESP profiles in the admin center. A scoped user can tell the relative priority of their profile even if they can't see all of the other profiles in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).  
 
10. In **Review + create**, review your settings. After you select **Create**, your changes are saved, and the profile is assigned. Once deployed, the profile will be applied the next time the devices check in. You can access the profile from your profiles list. 


## Edit default profile 

Intune applies the default profile to all users and all devices when no other ESP profiles are available to assign. You can configure the default profile to show or hide the ESP.      
 
1. Select the default profile.  
3. Select **Properties**. 
4. Go to the **Settings** section and select **Edit**.  
5. Configure **Show app and profile installation progress** to set the behavior of the default profile. Your options:
   * **No**: The ESP isn't visible to users during initial device setup and sign-in. 
   * **Yes**: The ESP is visible to users during initial device setup and sign-in.

   If you select **Yes**, more settings become available for you to configure.       
6. Select **Review + save**. 
7. Review the summary of changes and then select **Save**.   


## Prioritize profiles       
If you assign a user or device more than one ESP profile, the profile with the highest priority takes precedence over the other profiles. The profile set to 1 has the highest priority.

 Intune applies profiles in the following order:  

1. Intune applies the highest-priority profile assigned to the device. 
2. If no profiles are targeted at the device, Intune applies the highest-priority profile assigned to the user. This only works in scenarios where there is a user. In white glove and self-deploying scenarios, only profiles targeted at devices can be applied.   
3. If no profiles are assigned to the device or user, Intune applies the default ESP profile.    

To prioritize your profiles:  

1. Hover over the profile in the list with your cursor until you see three vertical dots.  
2. Drag the profile to the desired position in the list.   

## Block access to a device until a specific application is installed

Specify the apps that must be installed before the user can exit the ESP. You can choose up to 100 apps.   

1. Choose an enrollment status page profile, and then select **Settings**.
4. Choose **Yes** for **Show app and profile installation progress**.
5. Choose **Yes** for **Block device use until all apps and profiles are installed**.
6. Choose **Selected** for **Block device use until these required apps are installed if they're assigned to the user/device**.
7. Choose **Select apps** > choose the apps > **Select** > **Save**.

The apps that are included in this list are used by Intune to filter the list that should be considered blocking.  It doesn't specify what apps should be installed.  For example, if you configure this list to include "App 1," "App 2," and "App 3" and "App 3" and "App 4" are targeted to the device or user, the ESP will track only "App 3."  "App 4" will still be installed, but the ESP will not wait for it to complete.

## ESP tracking     

The enrollment status page tracks these phases of provisioning: 

* Device preparation
* Device setup
* Account setup  

This section describes the types of information, apps, and policies tracked during each phase.  

### Device preparation

During device preparation, the enrollment status page tracks these tasks for the device user: 

* Secure your hardware
* Join your organization's network
* Register your device for mobile management    

#### Secure your hardware
This task ensures that the device completes the Trusted Platform Module (TPM) key attestation and validates its identity with Azure AD. Azure AD sends a token to the device, which is used during Azure AD join. 

This step is required for self-deploying mode and white glove deployment. It isn't needed for Windows Autopilot scenarios in user-driven mode.   

#### Join your organization's network  
The device uses the token received in the previous step to join Azure AD. This step is required in self-deploying mode and white glove deployment. Devices in user-driven mode have already completed this task by time they open the ESP.  

### Register your device for mobile management
The device enrolls in Microsoft Intune for mobile device management (MDM). 

This step is required in self-deploying mode and white glove deployment. Devices in user-driven mode have already completed this step by time they open the ESP. 

After enrollment, the device calculates the policies and apps required to track in the next phase. For Windows 10, version 1903 and later versions, the device also creates the tracking policy for the SideCar agent, and installs the Intune Management Extension that's used to install Win32 apps.  

### Device setup

The enrollment status page tracks these items during the device setup phase:

* Security policies  
* Certificate profiles  
* Network connection  
* Apps  

#### Security policies
ESP doesn't track security policies, such as device restrictions, but these policies are installed in the background. The ESP does track Microsoft Edge, Assigned Access, and Kiosk Browser policies. 

  > [!TIP]
  >  When complete, the status for security policies appears on the ESP as **(1 of 1) completed**.  

#### Certificates  
The ESP tracks the installation of SCEP certificate profiles targeted at devices.  

#### Network connections    
The ESP tracks VPN and Wi-Fi profiles targeted at devices.  

#### Apps  
The ESP tracks the installation of apps deployed in a device context, and includes:   

  - Per machine line-of-business (LoB) MSI apps
  - LoB store apps where installation context = device 
  - Win32 applications for Windows 10, version 1903 and later, and Windows 11.
  - Winget application installed during Windows Autopilot


  > [!NOTE]
  > Don't mix LOB and Win32 apps. Both LOB (MSI) and Win32 installers use TrustedInstaller, which doesn't allow simultaneous installations. If the OMA DM agent starts an MSI installation, the Intune Management Extension plugin starts a Win32 app installation by using the same TrustedInstaller. In this situation, Win32 app installation fails and returns an **Another installation is in progress, please try again later** error message. In this situation, ESP fails. Therefore, don't mix LOB and Win32 apps in any type of Autopilot enrollment.  

### Account setup

During the account setup phase, the ESP tracks apps and policies targeted at users, including: 

* Security policies  
* Certificates
* Network connections
* Apps 

  > [!TIP]
  > Before installation begins, the device creates a tracking policy and calculates all apps and policies that need to be tracked. While that's happening, the ESP shows subtasks in an **Identifying** state.  

#### Security policies  
ESP doesn't track security policies, such as device restrictions, but these policies are installed in the background. The ESP does track Microsoft Edge, Assigned Access, and Kiosk Browser policies.  

#### Certificates   
The ESP tracks the installation of SCEP certificate profiles assigned to users.  

#### Network connections 
The ESP tracks Wi-Fi profiles assigned to users.  

#### Apps  
During this phase, the ESP tracks the installation of apps assigned to the user. The ESP tracks Win32 apps for Windows 10, version 1903 and later.   

It also tracks the following types of apps when they're assigned to all devices, all users, or a user group that includes the enrolling device user:  

  - Per user LoB MSI apps     
  - Per machine LoB MSI apps   
  - LoB store apps, online store apps, and offline store apps 

Win32 and UWP apps assigned to the device with user installation context aren't tracked during provisioning if you're using Hybrid Azure AD join.   

### Known issues

This section lists the known issues for the enrollment status page.  

- When creating apps that will be deployed during ESP, any reboots that are packaged within the app may cause ESP to hang and fail the deployment. We recommend specifying the reboot behavior in Intune instead of triggering the reboot within the package. 
- Disabling the ESP profile doesn't remove ESP policy from devices and users still get ESP when they log in to device for first time. The policy isn't removed when the ESP profile is disabled. 
- A reboot during device setup forces the user to enter their credentials before the account setup phase. User credentials aren't preserved during reboot. Instruct the device users to enter their credentials to continue to the account setup phase.  
- The ESP always times out on devices running Windows 10, version 1903 and earlier, and
enrolled via the *Add work and school account* option. The ESP waits for Azure AD registration to complete. The issue is fixed on Windows 10 version 1903 and later.  
- Hybrid Azure AD Autopilot deployment with ESP takes longer than the timeout duration entered in the ESP profile. On Hybrid Azure AD Autopilot deployments, the ESP takes 40 minutes longer than the value set in the ESP profile. For example, you set the timeout duration to 30 minutes in the profile. The ESP can take 30 minutes + 40 minutes. This delay gives the on-premises AD connector time to create the new device record to Azure AD.  
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

For help with errors or messages related to the ESP, including how to disable an already-enabled ESP, see [Troubleshoot the Windows Enrollment Status page](/troubleshoot/mem/intune/understand-troubleshoot-esp#troubleshooting).  
