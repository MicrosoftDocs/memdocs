---
# required metadata

title: Windows Update settings you can manage with Intune Update Ring policies for Windows 10/11 devices. 
description: View the settings for Windows Update that you can manage through Intune policy for Update rings.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 07/15/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davguy; bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier3
- M365-identity-device-management
- sub-updates
---


# Settings for Windows Update that you can manage through Intune policy for Update rings

When you use Intune policies for *Update rings*, you're configuring the Windows settings that manage how and when devices will install Windows updates. If a Windows update setting has a Windows 10 or Windows 11 version dependency, the version dependency is noted in the settings details.

Following are the Windows Update settings for Windows 10 and Windows 11 Updates that you can [manage with update rings](windows-10-update-rings.md) with Microsoft Intune.

## Update settings

Update settings control what bits a device will download, and when. For more information about the behavior of each setting, see the Windows reference documentation.  

- **Microsoft product updates**  
  **Default**:  Allow  
  Windows Update CSP: [Update/AllowMUUpdateService](/windows/client-management/mdm/policy-csp-update#allowmuupdateservice)

  - **Allow** - Select *Allow* to scan for app updates from Microsoft Update.  
  - **Block** - Select Block to prevent scanning for app updates.  

- **Windows drivers**  
  **Default**:  Allow  
  Windows Update CSP: [Update/ExcludeWUDriversInQualityUpdate](/windows/client-management/mdm/policy-csp-update#excludewudriversinqualityupdate)  

  - **Allow** - Select *Allow* include Windows Update drivers during updates.  
  - **Block** - Select Block to prevent scanning for drivers.  

- **Quality update deferral period (days)**  
  **Default**: 0  
  Windows Update CSP: [Update/DeferQualityUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferqualityupdatesperiodindays)  

  Specify the number of days from 0 to 30 for which Quality Updates are deferred. This period is in addition to any deferral period that is part of the service channel you select. The deadline calculation for both quality and feature updates is based off the time the client's update scan initially discovered the update. See [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines)

  Quality Updates are typically fixes and improvements to existing Windows functionality.  

- **Feature update deferral period (days)**  
  **Default**: 0  
  Windows Update CSP: [Update/DeferFeatureUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-update#deferfeatureupdatesperiodindays)  

  Specify the number of days for which Feature Updates are deferred. This period is in addition to any deferral period that is part of the service channel you select. The deferral period begins when Microsoft releases the update.

  Supported deferral period:  

  - *Windows version 1709 and later* - 0 to 365 days  
  
  Feature Updates are typically new features for Windows.  

- **Upgrade Windows 10 devices to Latest Windows 11 release**  
  **Default**: No

  When set to *Yes*, eligible Windows 10 devices will upgrade to the most current Windows 11 release. For more information on eligibility, see [Windows 11 Specs and System Requirements | Microsoft](https://www.microsoft.com/windows/windows-11-specifications).

- **Set feature update uninstall period (2 – 60 days)**  
  **Default**: 10  
  Windows Update CSP: [Update/ConfigureFeatureUpdateUninstallPeriod](/windows/client-management/mdm/policy-csp-update#configurefeatureupdateuninstallperiod)  

  Configure a time after which feature updates can't be uninstalled.  

  After this period expires, the previous update bits are removed from the device, and it can no longer uninstall to a previous update version.  

  For example, consider an update ring with a feature update uninstall period of 20 days. After 25 days, you decide to roll back the latest feature update and use the Uninstall option.  Devices that installed the feature update over 20 days ago can't uninstall it as they've removed the necessary bits as part of their maintenance. However, devices that only installed the feature update up to 19 days ago can uninstall the update if they successfully check in to receive the uninstall command before exceeding the 20-day uninstall period.  

- **Enable pre-release builds**  
  **Default**: Not Configured  

  When configuring *Update ring settings*, you can choose to enable **Enable pre-release builds**. Devices that receive this setting as *Enabled* will move to the pre-release build you specify, and will also reboot. When enabled, specify one of the following prerelease builds:  
  - **Windows Insider - Release Preview** (*default*)
  - **Beta Channel**
  - **Dev Chanel**

  For information about pre-release builds, see [Windows Insider](https://insider.windows.com/understand-flighting).

## User experience settings  

User experience settings control the end-user experience for device restart and reminders. For more information about the behavior of each setting, see the Windows Update CSP documentation.  

- **Automatic update behavior**  
  **Default**: Auto install at maintenance time  
  Windows Update CSP: [Update/AllowAutoUpdate](/windows/client-management/mdm/policy-csp-update#allowautoupdate)  

  Choose how automatic updates are installed and, if necessary, when to restart the device.  

  Supported options:  

  - **Notify download** - Notify the user before downloading the update. Users choose to download and install updates.  
  
    > [!IMPORTANT]  
    > If the user takes no action, the update will not install until the deadline you have configured is reached.

  - **Auto install at maintenance time** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, users are prompted to restart for up to seven days, and then restart is forced.  

    This option can restart a device automatically after the update installs. Use the **Active hours** settings to define a period during which the automatic restarts are blocked:  

    - **Active hours start** - Specify a start time for suppressing restarts due to update installations.  
      **Default**: 8 AM  
      Windows Update CSP: [Update/ActiveHoursStart](/windows/client-management/mdm/policy-csp-update#activehoursstart)  
  
    - **Active hours end** - Specify an end time for suppressing reboots due to update installations.  
      **Default**: 5 PM  
      Windows Update CSP: [Update/ActiveHoursEnd](/windows/client-management/mdm/policy-csp-update#activehoursend)  

  - **Auto install and restart at maintenance time** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used, which is the default for unmanaged devices.

    This option can restart a device automatically after the update installs. Use of the **Active hours** settings aren't described in Windows Update settings but are used by Intune to define a period during which the automatic restarts are blocked:  

    - **Active hours start** - Specify a start time for suppressing restarts due to update installations.  
      **Default**: 8 AM  
      Windows Update CSP: [Update/ActiveHoursStart](/windows/client-management/mdm/policy-csp-update#activehoursstart)  
  
    - **Active hours end** - Specify an end time for suppressing reboots due to update installations.  
      **Default**: 5 PM  
      Windows Update CSP: [Update/ActiveHoursEnd](/windows/client-management/mdm/policy-csp-update#activehoursend)  

  - **Auto install and restart at a scheduled time** - Specify an installation day and time. If unspecified, installation runs at 3 AM daily, followed by a 15-minute countdown to a restart. Logged on users can delay countdown and restart.  
    Windows Update CSP: [Update/AllowAutoUpdate](/windows/client-management/mdm/policy-csp-update#allowautoupdate)  

    When set to *Auto install and restart at a scheduled time*, you can configure the following settings:

    - **Automatic behavior frequency** - Use this setting to schedule when updates are installed, including the week, the day, and the time.  
      **Default**: Every week

    - **Scheduled install day** - Specify on which day of the week you want updates to install.  
      **Default**: Any Day  

    - **Scheduled install time** - Specify the time of day when you want updates to install.  
      **Default**: 3 AM
  
      > [!IMPORTANT]  
      > The device might not complete the installation at the specified time because of power policies, user absence, and so on. In this case, it will not attempt installation until the specified time occurs again or until a deadline you have specified is reached.

  - **Auto install and reboot without end-user control** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used. This option sets the end-users control pane to read-only.  

  - **Reset to default** - Restore the original auto update settings on machines that run the Windows 10 October 2018 Update or later, and that run Windows 11. When you *reset to default*, Windows will automatically determine active hours for the device. Using the active hours, Windows then schedules the best time to install updates and restart the system after updates install.

- **Restart checks (EDU Restart)**  
  
  > [!NOTE]
  > In policies where this value is currently set to *Skip*, the value will remain in place until that value is changed to *Allow* and saved. However, When creating new policies, it will not be available, and you can use [Settings catalogue](../configuration/settings-catalog.md) to set this value if required.
  
  **Default**: Allow

  Windows Update CSP: [Update/SetEDURestart](/windows/client-management/mdm/policy-csp-update#setedurestart)  

  - **Allow** - Perform restart checks: Battery level = 40%, User presence, Display Needed, Presentation mode, Full screen mode, phone call state, game mode etc.
  - **Skip** - Will restrict updates to download and install outside of Active Hours. Updates will be allowed to start even if there is a signed-in user or the device is on battery power, providing there is more than 70% battery capacity. Windows will schedule the device to wake from sleep 1 hour after the [Active Hours End](/windows/client-management/mdm/policy-csp-update#activehoursend) time with a 60-minute random delay. Devices will reboot immediately after the updates are installed. If there are still pending updates, the device will continue to retry every hour for 4 hours.

    This option is designed for education devices that remain in carts overnight that are left in sleep mode. It is not designed for 1:1 devices.

- **Option to pause Windows updates**  
  **Default**: Enable  
  Windows Update CSP: [Update/SetDisablePauseUXAccess](/windows/client-management/mdm/policy-csp-update#setdisablepauseuxaccess)  

  - **Enable** - Allow device users to pause the installation of an update for a certain number of days.  
  - **Disable** - Prevent device users from pausing the installation of an update.  

- **Option to check for Windows updates**  
  **Default**: Enable  
  Windows Update CSP: [Update/SetDisableUXWUAccess](/windows/client-management/mdm/policy-csp-update#setdisableuxwuaccess)

  - **Enable** - Allow device users to use Windows Update scan to find updates.
  - **Disable** - Prevent device users from accessing the Windows Update scan.  

- **Change notification Update level**  
  **Default**: Use the default Windows Update notifications  
  Windows Update CSP: [Update/UpdateNotificationLevel](/windows/client-management/mdm/policy-csp-update#updatenotificationlevel)
  
  Specify what level of Windows Update notifications users see. This setting doesn't control how and when updates are downloaded and installed.  

  Supported options:
  - **Not configured**
  - **Use the default Windows Update notifications**
  - **Turn off all notifications, excluding restart warnings**
  - **Turn off all notifications, including restart warnings**  

- **Use deadline settings**  
  **Default**: Not configured  

  Allows configuration of deadline settings.

  - **Not configured**
  - **Allow**
  
  For more details about how deadlines and grace periods work together see [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).
  
  When set to *Allow*, you can configure the following settings for deadlines:

  - **Deadline for feature updates**  
    **Default**: *Not configured*  
    Windows Update CSP: [Update/ConfigureDeadlineForFeatureUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforfeatureupdates)  

    Specifies the number of days a user has before feature updates are installed on their devices automatically (2-30).

  - **Deadline for quality updates**  
    **Default**: *Not configured*  
    Windows Update CSP: [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-update#configuredeadlineforqualityupdates)

    Specifies the number of days a user has before quality updates are installed on their devices automatically (2-30).

  - **Grace period**  
    **Default**: *Not configured*
    Windows Update CSP: [Update/ConfigureDeadlineGracePeriod]( /windows/client-management/mdm/policy-csp-update#configuredeadlinegraceperiod)

    Specifies a minimum number of days after deadline until restarts occur automatically (0-7).

  - **Auto reboot before deadline**  
    **Default**:  Yes
    Windows Update CSP: [Update/ConfigureDeadlineNoAutoReboot](/windows/client-management/mdm/policy-csp-update#configuredeadlinenoautoreboot)

    Specifies whether the device will attempt to automatically reboot outside of active hours before the deadline and grace period are expired. The recommended value is **Yes**, as it enables the system to reboot when the user isn't using the device. Setting this value to **No** forces the system to wait until the deadline and grace period are expired and then restarts the device and this could occur during active hours.

    - **Yes**
    - **No**

<!-- Deleting the following section, as Rings no longer support the option described by the linked content, which is now also removed.>
### Delivery Optimization download mode  

Delivery Optimization is no longer configured as part of a Windows update policy. Delivery Optimization is now set through device configuration. However, previous configurations might remain available in the console. You can remove these previous configurations by editing them to be *Not configured*, but they can't otherwise be modified.

To avoid conflicts between new and old policy, see [Remove Delivery Optimization from Update rings for Windows 10 and later](../configuration/delivery-optimization-windows.md#remove-delivery-optimization-from-windows-update-rings) and then move your settings to a Delivery Optimization profile. 
