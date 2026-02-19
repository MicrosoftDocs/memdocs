---
title: Set up the Enrollment Status Page in the admin center copy
description: Set up a greeting page for users signing in and enrolling Windows devices copy.
ms.date: 01/20/2026
ms.topic: how-to
ms.reviewer: madakeva, davguy
ms.collection:
- M365-identity-device-management
- highpri
---

# Set up the Enrollment Status Page

The enrollment status page (ESP) shows the provisioning status to people enrolling Windows devices and signing in for the first time. You can configure the ESP to block device use until all required policies and applications are installed. Device users can look at the ESP to track the setup progress on their device.

The ESP can be deployed during the default out-of-box experience (OOBE) for Microsoft Entra join, and any [Windows Autopilot](/autopilot/index) provisioning scenario.

To deploy the ESP to devices, create an ESP profile in Microsoft Intune, and configure the ESP settings that control:

- Visibility of installation progress indicators
- Device access during provisioning
- Time limits
- Allowed troubleshooting operations

This article describes the information that the enrollment status page tracks and how to create an ESP profile in Microsoft Intune.

## Before you begin

- ESP uses the [EnrollmentStatusTracking configuration service provider (CSP)](/windows/client-management/mdm/enrollmentstatustracking-csp) and [FirstSyncStatus CSP](/windows/client-management/mdm/dmclient-csp) to track app installation.
- You can create maximum of 51 ESP profiles (Default + 50) in a tenant.

## Create new profile

Use the following steps to create an Intune profile that configures the enrollment status page.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > expand **Device onboarding** > ***Enrollment**.
1. In the **Windows** tab, under **Windows Autopilot**, select **Enrollment Status Page**.
1. Select **Create**.
1. In **Basics**, enter the following properties:
    - **Name**: Name your profile so you can easily identify it.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
1. Select **Next**.
1. In **Settings**, configure the following settings:

    - **Show app and profile configuration progress**: Your options:
      - **No**: The enrollment status page doesn't appear during device setup. Select this option if you don't want to show the configuration progress to users.
      - **Yes**: The enrollment status page appears during device setup. More options become available if you select this option.

    - **Show an error when installation takes longer than specified number of minutes**: A time-out error message is shown after your desired time. The default time-out is 60 minutes. Enter a higher value if you think more time is needed to install apps on your devices.

    - **Show custom message when time limit or error occur**: Include a custom message that tells people what happened and who to contact for help. Your options:
      - **No**: The `Setup could not be completed. Please try again or contact your support person for help.` default message is shown to users when an error occurs.
      - **Yes**: Your custom message is shown to users when an error occurs. Enter your message in the provided text box.

    - **Turn on log collection and diagnostics page for end users**: We recommended turning on this option since the user's logs and diagnostics could aid with troubleshooting. Your options:
      - **No**: The collect logs button isn't shown to users when an installation error occurs. The Windows Autopilot diagnostics page isn't shown on devices running Windows 11.
      - **Yes**: The collect logs button is shown to users when an installation error occurs. The Windows Autopilot diagnostics page is shown on devices running Windows 11.

    - **Only show page to devices provisioned by out-of-box experience (OOBE)**: Use this setting to stop the enrollment status page from reappearing to every new user who signs into the device. Your options:
      - **No**: The enrollment status page is shown during the device phase and the out-of-box experience (OOBE). The page is also shown during the [user phase](#account-setup) to every user who signs into the device for the first time.
      - **Yes**: The enrollment status page is shown during the device phase and the OOBE. The page is also shown during the user phase, but only to the first user who signs into the device. It isn't shown to subsequent users who sign into the device.

    - **Install Windows quality updates (might restart the device)**: Use this setting to control checking and installation from Windows Updates for the available quality updates, also known as monthly security update releases. Your options:
      - **Yes**: At the end of OOBE, the device checks Windows Updates for any missing and applicable monthly security update releases. During this process, if updates are found, a page shows the update progress.
      - **No**: Monthly security update releases aren't installed during OOBE and the device continues to the desktop as usual. Messages regarding installation of monthly security update releases aren't displayed since they aren't installed.

      > [!IMPORTANT]
      >
      > - This setting only supports [current supported versions of Windows 11](/windows/release-health/windows11-release-information).
      > - When set to **Yes**, monthly security update releases are installed during OOBE after the ESP completes. ESP applies any Update rings policies and then applies the quality updates. So, your organization policy is honored.
      > - For more details on this setting, see [Windows monthly security update release details](#windows-monthly-security-update-release-details) (in this article).

    - **Block device use until all apps and profiles are installed**: Your options:
      - **No**: Users can leave the ESP before Intune is finished setting up the device.
      - **Yes**: Users can't leave the ESP until Intune is done setting up the device. This option unlocks more settings for this scenario.

    - **Allow users to reset device if installation error occurs**: Your options:
      - **No**: The ESP doesn't give users the option to reset their devices when an installation fails.
      - **Yes**: The ESP gives users the option to reset their devices when an installation fails.

    - **Allow users to use device if installation error occurs**: Your options:
      - **No**: The ESP doesn't give users the option to bypass the ESP when an installation fails.
      - **Yes**: The ESP gives users the option to bypass the ESP and use their devices when an installation fails.

    - **Block device use until these required apps are installed if they are assigned to the user/device**: Your options:
      - **All**: All assigned apps must be installed before users can use their devices.
      - **Selected**: The selected apps must be installed before users can use their devices. Choose **Select apps** to start a *Blocking apps* list with more settings related to blocking apps.

    - **Only fail selected blocking apps in technician phase**: Use this setting with Windows Autopilot pre-provisioned deployments to control how your required apps are prioritized during the [Technician Flow](/autopilot/pre-provision#technician-flow). This setting is only available if *blocking apps* are added and only applies to devices going through pre-provisioning. Your options:
      - **No**: An attempt is made to install the blocking apps. Windows Autopilot deployment fails if a blocking app fails to install. No attempt is made to install nonblocking apps. When the end user receives the resealed device and signs in for the first time, the ESP attempts to install the nonblocking apps.
      - **Yes**: An attempt is made to install all required apps. Windows Autopilot deployment fails if a blocking app fails to install. If a nonblocking app targeted to the device fails to install, the ESP ignores it and deployment continues as normal. When the end user signs into the resealed device for the first time, the ESP reattempts to install the apps that it couldn't during the Technician Flow. This setting is the default setting for pre-provisioned deployments.

      > [!TIP]
      > When using this feature, expect provisioning time to increase during the Technician Flow. The more apps assigned, the longer it could take. If you're using a non-Microsoft provider to provision your devices, tell them about the potential for increased provisioning time. Increase the ESP time-out duration to prevent deployment from failing due to a time-out.

1. Select **Next**.
1. In **Assignments**, select the groups to receive your profile. Optionally, select **Edit filter** to restrict the assignment further.

    > [!NOTE]
    > Due to OS restrictions, a limited selection of filters are available for ESP assignments. The picker only shows filters that have rules defined for `model`, `manufacturer`, `osVersion`, `operatingSystemSKU`, `deviceOwnership`, and `enrollmentProfileName` properties. `model` and `manufacturer` are available with Windows 11, version 23H2 with KB5035942 or later, or version 22H2 with KB5035942 or later. Filters that contain other properties aren't available.

1. Select **Next**.

1. Optional. In **Scope tags**, assign a tag to limit profile management to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. Then select **Next**.

    Scope tags limit who can see and reprioritize ESP profiles in the admin center. A scoped user can tell the relative priority of their profile even if they can't see all of the other profiles in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

1. In **Review + create**, review your settings. After you select **Create**, your changes are saved, and the profile is assigned. Once deployed, the profile applies the next time the devices check in. You can access the profile from your profiles list.

## Edit default profile

Intune applies the default profile to all users and all devices when no other ESP profiles are available to assign. You can configure the default profile to show or hide the ESP.

1. Select the default profile.
1. Select **Properties**.
1. Go to the **Settings** section and select **Edit**.
1. Configure **Show app and profile installation progress** to set the behavior of the default profile. Your options:
   - **No**: The ESP isn't visible to users during initial device setup and sign-in.
   - **Yes**: The ESP is visible to users during initial device setup and sign-in.

   If you select **Yes**, more settings become available for you to configure.
1. Select **Review + save**.
1. Review the summary of changes and then select **Save**.

## Windows monthly security update release details

When you configure the enrollment status page, you can choose to install [monthly security update releases](/windows/deployment/update/release-cycle#monthly-security-update-release), also known as quality updates, during the OOBE. By default, these quality updates aren't installed during OOBE.

On Windows 11 versions with the `2025-06 D` quality update, the control that enables this feature is part of the operating system. On other Windows 11 versions, the feature is in the `2025-11 D` zero day package (ZDP) that's automatically installed before the ESP is displayed. So, to install quality updates during OOBE, you only need to configure the ESP policy in Intune.

> [!NOTE]
> The operating system control is included in the following `2025-06 D` operating system updates:
>
> | OS version | KB article |
> | --- | --- |
> | Windows 11, version 25H2 | Automatically included |
> | Windows 11, version 24H2 | [KB5060829](https://support.microsoft.com/topic/june-26-2025-kb5060829-os-build-26100-4484-preview-e31ba7c2-ff65-4863-a462-a66e30840b1a) |
> | Windows 11, version 23H2 <br/> Windows 11, version 22H2 | [KB5060826](https://support.microsoft.com/topic/june-26-2025-kb5060826-os-builds-22621-5549-and-22631-5549-preview-65d38dd2-e149-4462-9699-e2482f60b16b) |

### What you need to know

- The **Install Windows quality updates** OS enforcement is included in the `2026-01 B` quality update.

- The **Install Windows quality updates** Intune setting only installs monthly security update releases. It doesn't install the other types of updates listed at [Types of update releases](/windows/deployment/update/release-cycle#types-of-update-releases).

- The **Install Windows quality updates** Intune setting can be configured on new and existing ESP profiles.

  - On new ESP profiles, the setting default is **Yes**.
  - On existing ESP profiles, the setting default is **No**.

    To install the quality updates during OOBE, edit the existing ESP profile and set the **Install Windows quality updates** setting to **Yes**.

- Installing the quality updates during OOBE adds 20-40 minutes to the provisioning process and might require restarts. If a restart occurs, the user isn't automatically signed into Windows. Restarts can break some autologon provisioning scenarios. In these scenarios, we recommend you set **Install Windows quality updates** to **No**.

- Monthly security update releases aren't installed during OOBE when the device is on a metered network.

> [!IMPORTANT]
> To ensure that monthly security update releases are installed, set the **Block device use until all apps and profiles are installed** ESP profile setting to **Yes**. When set to **No**, the device might exit ESP before the following items are applied:
> - Windows Update for Business (WUfB) policies
> - Monthly security update releases
>
> **No** can result in monthly security update releases not being installed during OOBE, even when **Install Windows quality updates** is set to **Yes**.

### Supported configurations

Devices that meet all of the following conditions honor the **Install Windows quality updates** setting. Devices that don't meet the following conditions don't honor the **Install Windows quality updates** setting and they won't install monthly security update releases during OOBE.

- Running a [currently supported version of Windows 11](/windows/release-health/windows11-release-information).
- Assigned an ESP profile with the **Install Windows quality updates** Intune setting configured to **Yes**.
- One of the following two assignments:
  - Assigned to devices that are registered for Windows Autopilot.
  - For devices that aren't registered with Windows Autopilot, devices that are assigned using the **All Devices** assignment.    
- The **Install Windows quality updates** setting doesn't support user-targeted ESP profiles. The device uses the highest priority device-targeted profile, which is typically the default ESP profile. If the ESP page is disabled, quality updates won't install. If the ESP page is enabled, it follows the **Install Windows quality updates** setting and value you configured.

The following specific scenarios aren't supported and the **Install Windows quality updates** setting isn't honored:

- **Windows Autopilot device preparation** - Windows Autopilot device preparation doesn't use ESP, so this setting isn't applicable. Monthly security update releases can't be installed during OOBE.
- **Windows Autopilot for pre-provisioned deployment Technician Flow** - Monthly security update releases aren't installed during the [Technician Flow](/autopilot/pre-provision#technician-flow) portion of a Windows Autopilot for pre-provisioned deployment. However, the **Install Windows quality updates** setting is honored during the [User Flow](/autopilot/pre-provision#user-flow) portion of a Windows Autopilot for pre-provisioned deployment.

### Update rings and Windows Autopatch

Update rings settings, such as monthly security update release deferrals and pauses, are honored. The ESP page doesn't exit until ring settings are synced. This process ensures sure that the right settings are used when Windows Update scan occurs. If a device isn't registered as a Windows Autopilot device, the **All Devices** assignments must be used for both the Update Rings and ESP profile settings.

If using Windows Autopatch, Update rings policies need to be configured as described. Since Autopatch groups don't support assigning to **All Devices**, use one of the following two methods instead:

- Use Update Rings policies from the **Devices | Windows Updates** screen with **All Devices** assigned.
- Use groups of devices registered with Windows Autopilot in Autopatch Groups.

Expedited updates aren't part of the installation of monthly security update releases during OOBE. Devices assigned to an expedited update policy will initiate the expedited update sometime after OOBE completes if the expedited updates aren't part of monthly security update releases.

> [!TIP]
> By using Update Rings to manage updates, administrators don't need to go to both the ESP and Update Rings to pause an update. Pausing an update via Update Rings pauses the update on both devices being provisioned, for example running Windows Autopilot, and devices that are already enrolled.

## Prioritize profiles

If you assign a user or device more than one ESP profile, the profile with the highest priority takes precedence over the other profiles. The profile set to 1 has the highest priority. Intune applies the default ESP profile when no other profiles are assigned to the device or user.

 Intune applies profiles in the following order:

1. Intune applies the highest-priority profile assigned to the device.
1. If no profiles are targeted at the device, Intune applies the highest-priority profile assigned to the user. This only works in scenarios where there's a user. In pre-provisioning and self-deploying scenarios, Intune only applies profiles targeted at devices.
1. If no profiles are assigned to the device or user, Intune applies the default ESP profile.

To prioritize your profiles:

1. Hover over the profile in the list with your cursor until you see three vertical dots.
1. Drag the profile to the desired position in the list.

## Block access to a device until a specific application is installed

Specify the apps that must be installed before the user can exit the ESP. You can choose up to 100 apps.

1. Choose an enrollment status page profile, and then select **Settings**.
1. Choose **Yes** for **Show app and profile installation progress**.
1. Choose **Yes** for **Block device use until all apps and profiles are installed**.
1. Choose **Selected** for **Block device use until these required apps are installed if they're assigned to the user/device**.
1. Choose **Select apps** > choose the apps > **Select** > **Save**.

The apps in this list are used by Intune to filter the list that should be considered blocking. It doesn't specify what apps should be installed.  For example, if you configure this list to include:

- App 1
- App 2
- App 3

And **App 3** and **App 4** are targeted to the device or user, the ESP tracks only **App 3**. **App 4** is still installed during pre-provisioning flows, but the ESP doesn't wait for it to complete. In other scenarios, such as user-driven and self-deploying mode, and when **App 4** is a Win32, Microsoft Store, or Enterprise app catalog app, it doesn't get installed until after ESP completes.

## ESP tracking

The enrollment status page tracks these phases of provisioning:

- Device preparation
- Device setup
- Account setup

This section describes the types of information, apps, and policies tracked during each phase.

### Device preparation

During device preparation, the enrollment status page tracks these tasks for the device user:

- Secure your hardware
- Join your organization's network
- Register your device for mobile management

#### Secure your hardware

This task ensures that the device completes the Trusted Platform Module (TPM) key attestation and validates its identity with Microsoft Entra ID. Microsoft Entra ID sends a token to the device, which is used during Microsoft Entra join.

This step is required for Windows Autopilot self-deploying mode and Windows Autopilot pre-provisioning deployment. It isn't needed for Windows Autopilot scenarios in user-driven mode.

#### Join your organization's network

The device uses the token received in the previous step to join Microsoft Entra ID. This step is required in Windows Autopilot self-deploying mode and Windows Autopilot pre-provisioning deployment. Devices in user-driven mode have already completed this task by time they open the ESP.

### Register your device for mobile management

The device enrolls in Microsoft Intune for mobile device management (MDM).

This step is required in Windows Autopilot self-deploying mode and Windows Autopilot pre-provisioning deployment. Devices in user-driven mode have already completed this step by time they open the ESP.

After enrollment, the device calculates the policies and apps required to track in the next phase. For Windows 10, version 1903 and later versions, the device also creates the tracking policy for the SideCar agent, and installs the Intune Management Extension used to install Win32 apps.

### Device setup

The enrollment status page tracks these items during the device setup phase:

- Security policies
- Certificate profiles
- Network connection
- Apps

#### Device setup: Security policies

ESP doesn't track security policies, such as device restrictions, but these policies are installed in the background. The ESP does track Microsoft Edge, Assigned Access, and Kiosk Browser policies.

  > [!TIP]
  >
  > When complete, the status for security policies appears on the ESP as **(1 of 1) completed**.

#### Device setup: Certificates

The ESP tracks the installation of SCEP certificate profiles targeted at devices.

#### Device setup: Network connections

The ESP tracks VPN and Wi-Fi profiles targeted at devices.

#### Device setup: Apps

The ESP tracks the installation of apps deployed in a device context and targeted to devices, and includes:

- Per machine line-of-business (LoB) MSI apps.
- LoB store apps where installation context = device.
- Win32 applications for [currently supported versions of Windows](/windows/release-health/supported-versions-windows-client).
- WinGet applications.

> [!NOTE]
>
> Don't mix LOB and Win32 apps. Both LOB (MSI) and Win32 installers use TrustedInstaller, which doesn't allow simultaneous installations. If the OMA DM agent starts an MSI installation, the Intune Management Extension plugin starts a Win32 app installation by using the same TrustedInstaller. In this situation, Win32 app installation fails and returns an **Another installation is in progress, please try again later** error message. In this situation, ESP fails. Therefore, don't mix LOB and Win32 apps when using Windows Autopilot.
>
> If mixing LOB and Win32 apps is required, consider using [Windows Autopilot device preparation](/autopilot/device-preparation/overview), which doesn't use ESP so therefore supports mixing of LOB and Win32 apps.

### Account setup

During the account setup phase, the ESP tracks apps and policies targeted at users, including:

- Security policies
- Certificates
- Network connections
- Apps

  > [!TIP]
  >
  > Before installation begins, the device creates a tracking policy and calculates all apps and policies that need to be tracked. While that's happening, the ESP shows subtasks in an **Identifying** state.

#### Account setup: Security policies

ESP doesn't track security policies, such as device restrictions, but these policies are installed in the background. The ESP does track Microsoft Edge, Assigned Access, and Kiosk Browser policies.

#### Account setup: Certificates

The ESP tracks the installation of SCEP certificate profiles assigned to users.

#### Account setup: Network connections

The ESP tracks Wi-Fi profiles assigned to users.

#### Account setup: Apps

During this phase, the ESP tracks the installation of apps assigned to the user. The ESP tracks Win32 apps for Windows 10, version 1903 and later.

It also tracks the following types of apps when they're assigned to all devices, all users, or a user group that includes the enrolling device user:

- Per user LoB MSI apps.
- Per machine LoB MSI apps.
- LoB store apps, online store apps, and offline store apps.

If you're using Microsoft Entra hybrid join, Win32 and UWP apps assigned to the device with user installation context aren't tracked during provisioning.

### Known issues

This section lists the known issues for the enrollment status page.

- When creating apps that are deployed during ESP, any reboots that are packaged within the app might cause ESP to hang and fail the deployment. We recommend specifying the reboot behavior in Intune instead of triggering the reboot within the package.
- Disabling the ESP profile doesn't remove ESP policy from devices and users still get ESP when they sign in to device for first time. The policy isn't removed when the ESP profile is disabled.
- A reboot during device setup forces the user to enter their credentials before the account setup phase. User credentials aren't preserved during reboot. Instruct the device users to enter their credentials to continue to the account setup phase.
- The ESP always times out on devices running Windows 10, version 1903 and earlier, and
enrolled via the *Add work and school account* option. The ESP waits for Microsoft Entra registration to complete. The issue is fixed on Windows 10 version 1903 and later.
- Hybrid Microsoft Entra Windows Autopilot deployment with ESP takes longer than the time-out duration entered in the ESP profile. On Hybrid Microsoft Entra Windows Autopilot deployments, the ESP takes 40 minutes longer than the value set in the ESP profile. For example, you set the time-out duration to 30 minutes in the profile. The ESP can take 30 minutes + 40 minutes. This delay gives the on-premises AD connector time to create the new device record to Microsoft Entra ID.
- Windows sign in page isn't prepopulated with the username in Windows Autopilot User Driven Mode. If there's a reboot during the Device Setup phase of ESP:
  - the user credentials aren't preserved
  - the user must enter the credentials again before proceeding from Device Setup phase to the Account setup phase
- ESP is stuck for a long time or never completes the "Identifying" phase. Intune computes the ESP policies during the identifying phase. A device might never complete computing ESP policies if the current user doesn't have an Intune licensed assigned.
- Configuring Microsoft Defender Application Control causes a prompt to reboot during Windows Autopilot. Configuring Microsoft Defender Application (AppLocker CSP) requires a reboot. When this policy is configured, it might cause a device to reboot during Windows Autopilot. Currently, there's no way to suppress or postpone the reboot.
- When the [DeviceLock policy](/windows/client-management/mdm/policy-csp-devicelock) is enabled as part of an ESP profile, the OOBE or user desktop autologon could fail unexpectedly for two reasons.
  - If the device didn't reboot before exiting the ESP Device setup phase, the user might be prompted to enter their Microsoft Entra credentials. This prompt occurs instead of a successful autologon where the user sees the Windows first sign-in animation.
  - The autologon will fail if the device rebooted after the user entered their Microsoft Entra credentials but before exiting the ESP Device setup phase. This failure occurs because the ESP Device setup phase never completed. The workaround is to reset the device.
- ESP doesn't apply to a Windows device that was enrolled with Group Policy (GPO).
- Scripts that run in user context (**Run this script using the logged on credentials** on the script properties is set to **yes**) might not execute during ESP. As a workaround, execute scripts in System context by changing this setting to **no**.
- Microsoft 365 Apps might cause the ESP to hang during app installation, specifically when:
  - You add Microsoft 365 Apps to Microsoft Intune by using the *Microsoft 365 Apps (Windows 10 and later)* app type.
  - The ESP is tracking the installation of Microsoft 365 Apps.
  - Microsoft 365 Apps begin installing during the installation of another Win32 app being tracked.

  To prevent the ESP from hanging during installation and causing a failed deployment, we recommend deploying Microsoft 365 Apps with Microsoft Intune by using the *Win32* app type.

## Troubleshooting

For help with errors or messages related to the ESP, including how to disable an already-enabled ESP, see [Troubleshoot the Windows Enrollment Status page](/troubleshoot/mem/intune/understand-troubleshoot-esp#troubleshooting).
