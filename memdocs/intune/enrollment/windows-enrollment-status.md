---
# required metadata

title: Set up an Enrollment Status Page
titleSuffix: Microsoft Intune
description: Set up a greeting page for users enrolling Windows 10 devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/26/2019
ms.topic: conceptual
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
ms.collection: M365-identity-device-management
---


 
# Set up an Enrollment Status Page
 
[!INCLUDE [azure_portal](../includes/azure_portal.md)]
 
The Enrollment Status Page (ESP) displays installation information about Windows 10 devices (version 1803 and later) during initial device enrollment. For example:
- when using [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/) 
- or anytime a managed device is started for the first time after an Enrollment Status Page policy has been applied. 

The Enrollment Status Page helps users understand the status of their device during device setup. You can create multiple Enrollment Status Page profiles and apply them to different groups that contain users. Profiles can be set to:
- Show installation progress.
- Block usage until installation completes.
- Specify what a user can do if device setup fails.

You can also set the priority order for each profile to account for conflicting profile assignments to the same user.

> [!NOTE]
> The Enrollment Status Page can only be targeted to a user who belongs to an assigned group and the policy is set on the device at the time of enrollment for all users that use the device.  Device targeting for Enrollment Status Page profiles is not currently supported.

## Available settings

 The following settings can be configured to customize behavior of the Enrollment Status Page:

<table>
<th align="left">Setting<th align="left">Yes<th align="left">No
<tr><td>Show app and profile installation progress<td>The enrollment status page is displayed.<td>The enrollment status page isn't displayed.
<tr><td>Block device use until all apps and profiles are installed<td>The settings in this table are made available to customize behavior of the enrollment status page, so that the user can address potential installation issues.
<td>The enrollment status page is displayed with no additional options to address installation failures.
<tr><td>Allow users to reset device if installation error occurs<td>A <b>Reset device</b> button is displayed if there's an installation failure.<td>The <b>Reset device</b> button isn't displayed if there's an installation failure.
<tr><td>Allow users to use device if installation error occurs<td>A <b>Continue anyway</b> button is displayed if there's an installation failure.<td>The <b>Continue anyway</b> button isn't displayed if there's an installation failure.
<tr><td>Show timeout error when installation takes longer than specified number of minutes<td colspan="2">Specify the number of minutes to wait for installation to complete. A default value of 60 minutes is entered.
<tr><td>Show custom message when an error occurs<td>A text box is provided where you can specify a custom message to display if an installation error occurs.<td>The default message is displayed: <br><b>Installation exceeded the time limit set by your organization. Try again or contact your IT support person for help.<b>
<tr><td>Allow users to collect logs about installation errors<td>If there's an installation error, a <b>Collect logs</b> button is displayed. <br>If the user clicks this button, they're asked to choose a location to save the log file <b>MDMDiagReport.cab</b><td>The <b>Collect logs</b> button isn't displayed if there's an installation error.
<tr><td>Block device use until these required apps are installed if they're assigned to the user/device<td colspan="2">Choose <b>All</b> or <b>Selected</b>. <br><br>If <b>Selected</b> is chosen, a <b>Select apps</b> button appears that lets you choose which apps must be installed before enabling the device.
</table>

## Turn on default Enrollment Status Page for all users

To turn on the Enrollment Status Page, follow the steps below.
 
1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Enrollment Status Page**.
2. In the **Enrollment Status Page** blade, choose **Default** > **Settings**.
3. For **Show app and profile installation progress**, choose **Yes**.
4. Choose the other settings that you want to turn on and then choose **Save**.

## Create Enrollment Status Page profile and assign to a group

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Enrollment Status Page** > **Create profile**.
2. Provide a **Name** and **Description**.
3. Choose **Create**.
4. Choose the new profile in the **Enrollment Status Page** list.
5. Choose **Assignments** > **Select groups** > choose the groups that you want to adopt this profile > **Select** > **Save**.
6. Choose **Settings** > choose the settings you want to apply to this profile > **Save**.

## Set the enrollment status page priority

A user can be in many groups and have many Enrollment Status Page profiles. To handle such conflicts, you can set the priorities for each profile. While enrolling, if someone has more than one Enrollment Status Page profile, only the highest priority profile is applied to the enrolling device.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Enrollment Status Page**.
2. Hover over the profile in the list.
3. Using the three vertical dots, drag the profile to the desired position on the list.

## Block access to a device until a specific application is installed

You can specify which apps need to be installed before the user can access the desktop.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Windows** > **Windows enrollment** > **Enrollment Status Page**.
2. Choose a profile > **Settings**.
3. Choose **Yes** for **Show app and profile installation progress**.
4. Choose **Yes** for **Block device use until all apps and profiles are installed**.
5. Choose **Selected** for **Block device use until these required apps are installed if they're assigned to the user/device**.
6. Choose **Select apps** > choose the apps > **Select** > **Save**.

The apps that are included in this list are used by Intune to filter the list that should be considered blocking.  It does not specify what apps should be installed.  For example, if you configure this list to include "App 1," "App 2," and "App 3" and "App 3" and "App 4" are targeted to the device or user, the Enrollment Status Page will track only "App 3."  "App 4" will still be installed, but the Enrollment Status Page will not wait for it to complete.

A maximum of 25 apps can be specified.

## Enrollment Status Page tracking information

There are three phases where the Enrollment Status Page tracks information for; device preparation, device setup, and account setup.

### Device preparation

For device preparation, the enrollment status page tracks:
- Trusted Platform Module (TPM) key attestations (when applicable)
- progress in joining Azure Active Directory
- enrolling into Intune
- installation of Intune management extensions

### Device setup

The Enrollment Status Page tracks the following device setup items (if they're assigned to All Devices or a device group in which the enrolling device is a member):
- Security policies
  - One configuration service provider (CSP) for all enrollments.
  - Actual CSPs configured by Intune aren't tracked here.
- Applications
  - Per machine Line-of-business (LoB) MSI apps.
  - LoB store apps with installation context = Device.
  - Offline store and LoB store apps with installation context = Device.
  - Win32 applications (Windows 10 version 1903 and newer only) 
- Connectivity profiles
  - VPN or Wi-Fi profiles that are assigned to **All Devices** or a device group in which the enrolling device is a member, but only for Autopilot devices
- Certificate profiles that are assigned to **All Devices** or a device group in which the enrolling device is a member, but only for Autopilot devices

### Account setup
For account setup, the Enrollment Status Page tracks the following items if they're assigned to the current logged in user:
- Security policies
  - One CSP for all enrollments.
  - Actual CSPs configured by Intune aren't tracked here.
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

### Troubleshooting
Top questions for troubleshooting.

- Why were my applications not installed during Device setup phase during Autopilot deployment that is using Enrollment Status Page?
  - To guarantee applications are installed during an Autopilot Device setup phase, ensure that:
      - The apps are assigned to an Azure AD group containing the device, using a "required" assignment.
      - You either specify **Block device use until all apps and profiles are installed** or include the app in the **Block device use until these required apps are installed** list.
      - The apps install in device context and have no user-context applicability rules.

- Why is the Enrollment Status Page showing for non-Autopilot deployments, for example when a user logs in for the first time on a Configuration Manager co-management enrolled device?  
  - The Enrollment Status Page lists installation status for all enrollment methods, including
      - Autopilot
      - Configuration Manager co-management
      - when any new user logs into the device that has Enrollment Status Page policy applied for the first time
      - when the **Only show page to devices provisioned by out-of-box experience (OOBE)** setting is on and the policy is set, only the first user who signs into the device gets the Enrollment Status Page

- How can I disable the Enrollment Status Page if it has been configured on the device?
  - Enrollment status page policy is set on a device at the time of enrollment. To disable the Enrollment Status Page, you must disable user and device Enrollment Status Page sections. You disable the sections by creating custom OMA-URI settings with the following configurations.

      Disable user Enrollment Status Page:

      ```
      Name:  Disable User ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipUserStatusPage
      Data type:  Boolean
      Value:  True 
      ```
      Disable device Enrollment Status Page:

      ```
      Name:  Disable Device ESP (choose a name you desire)
      Description:  (enter a description)
      OMA-URI:  ./Vendor/MSFT/DMClient/Provider/MS DM Server/FirstSyncStatus/SkipDeviceStatusPage
      Data type:  Boolean
      Value:  True 
      ```
- How can I collect log files?
  - There are two ways Enrollment Status Page log files can be collected:
      - Enable the ability for users to collect logs in the ESP policy. When a timeout occurs in the Enrollment Status Page, the end user can choose the option to **Collect logs**. By inserting a USB drive, the log files can be copied to the drive
      - Open a command prompt by entering Shift-F10 key sequence, then enter the following commandline to generate the log files: 

      ```
      mdmdiagnosticstool.exe -area Autopilot -cab <pathToOutputCabFile>.cab 
      ```

### Known issues
Below are known issues. 
- Disabling the ESP profile doesn't remove ESP policy from devices and users still get ESP when they log in to device for first time. The policy isn't removed when the ESP profile is disabled. You must deploy OMA-URI to disable the ESP. See above for instructions on how to disable ESP using OMA-URI. 
- A reboot during Device setup will force the user to enter their credentials before transitioning to Account setup phase. User credentials aren't preserved during reboot. Have the user enter their credentials then the Enrollment Status Page can continue. 
- Enrollment Status Page will always time out during an Add work and school account enrollment on Windows 10 versions less than 1903. The Enrollment Status Page waits for Azure AD registration to complete. The issue is fixed in Windows 10 version 1903 and newer.  
- Hybrid Azure AD Autopilot deployment with ESP takes longer than the timeout duration defined in the ESP profile. On Hybrid Azure AD Autopilot deployments, the ESP will take 40 minutes longer than the value set in the ESP profile. This delay gives time for the on-prem AD connector to create the new device record to Azure AD. 
- Windows logon page isn't pre-populated with the username in Autopilot User Driven Mode. If there's a reboot during the Device Setup phase of ESP:
    - the user credentials aren't preserved
    - the user must enter the credentials again before proceeding from Device Setup phase to the Account setup phase
- ESP is stuck for a long time or never completes the "Identifying" phase. Intune computes the ESP policies during the identifying phase. A device may never complete computing ESP policies if the current user doesn't have an Intune licensed assigned.  
- Configuring Microsoft Defender Application Control causes a prompt to reboot during Autopilot. Configuring Microsoft Defender Application (AppLocker CSP) requires a reboot. When this policy is configured, it may cause a device to reboot during Autopilot. Currently, there's no way to suppress or postpone the reboot.
- When the DeviceLock policy (https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) is enabled as part of an ESP profile, the OOBE or user desktop autologon could fail unexpectantly for two reasons.
  - If the device didn't reboot before exiting the ESP Device setup phase, the user may be prompted to enter their Azure AD credentials. This prompt occurs instead of a successful autologon where the user sees the Windows first login animation.
  - The autologon will fail if the device rebooted after the user entered their Azure AD credentials but before exiting the ESP Device setup phase. This failure occurs because the ESP Device setup phase never completed. The workaround is to reset the device.

## Next steps
After you set up Windows enrollment pages, learn how to manage Windows devices. For more information, see [What is Microsoft Intune device management?](../remote-actions/device-management.md)
