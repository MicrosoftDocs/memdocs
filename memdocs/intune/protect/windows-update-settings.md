---
# required metadata

title:  Windows for Business Update settings for  Microsoft Intune - Azure | Microsoft Docs
description: WUfB settings for Windows 10 devices that you can deploy using Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---


# Windows update settings for Intune  

View the Windows 10 Update settings you can [configure and manage](windows-update-for-business-configure.md) with Microsoft Intune.  

When you configure settings for Windows 10 update rings in Intune, you're configuring the Windows Update settings. If a Windows update setting has a Windows 10 version dependency, the version dependency is noted in the settings details.  

## Update settings  

Update settings control what bits a device will download, and when. For more information about the behavior of each setting, see the Windows reference documentation.  

- **Servicing channel**  
  **Default**: Semi-Annual Channel  
  Windows Update CSP: [Update/BranchReadinessLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-branchreadinesslevel)  

  Set the channel (branch) from which the device receives Windows updates. Different channels can use different deferral periods before updates are delivered.  

  For example, the *Semi-Annual Channel* has a six-month deferral. If you use this channel with no additional deferrals from this body of settings, the device installs the update six-months after its release.  

  Supported update channels:  

  - Semi-Annual Channel  
  - Semi-Annual Channel (targeted)  
  - Windows Insider – Fast  
  - Windows Insider – Slow  
  - Release Windows Insider  

  If you select an Insider channel, Intune automatically configures the Windows update setting [Update/ManagePreviewBuilds](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-managepreviewbuilds) so that the insider build will work.  


  > [!IMPORTANT]  
  > Beginning with Windows version 1903, the use of the *Semi-Annual Channel (targeted)* (SAC-T), is retired. With this change, SAC-T merges with the *Semi-Annual Channel*. To learn more about this change and how it affects Windows Update for Business, see the Windows IT Pro Blog post [Windows Update for Business and the retirement of SAC-T](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Windows-Update-for-Business-and-the-retirement-of-SAC-T/ba-p/339523).  
 
- **Microsoft product updates**  
  **Default**:  Allow  
  Windows Update CSP: [Update/AllowMUUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowmuupdateservice)

  - **Allow** - Select *Allow* to scan for app updates from Microsoft Update.  
  - **Block** - Select Block to prevent scanning for app updates.  

- **Windows drivers**  
  **Default**:  Allow  
  Windows Update CSP: [Update/ExcludeWUDriversInQualityUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-excludewudriversinqualityupdate)  

  - **Allow** - Select *Allow* include Windows Update drivers during updates.  
  - **Block** - Select Block to prevent scanning for drivers.  

- **Quality update deferral period (days)**  
  **Default**: 0  
  Windows Update CSP: [Update/DeferQualityUpdatesPeriodInDays](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-deferqualityupdatesperiodindays)  

  Specify the number of days from 0 to 30 for which Quality Updates are deferred. This period is in addition to any deferral period that is part of the service channel you select. The deferral period begins when the policy is received by the device.  

  Quality Updates are typically fixes and improvements to existing Windows functionality.  

- **Feature update deferral period (days)**  
  **Default**: 0  
  Windows Update CSP: [Update/PauseFeatureUpdatesPeriodInDays](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-deferfeatureupdatesperiodindays)  

  Specify the number of days for which Feature Updates are deferred. This period is in addition to any deferral period that is part of the service channel you select. The deferral period begins when the policy is received by the device.  

  Supported deferral period:  

  - *Windows version 1709 and later* - 0 to 365 days  
  - *Windows version 1703* - 0 to 180 days  

  Feature Updates are typically new features for Windows.  

- **Set feature update uninstall period (2 – 60 days)**  
  **Default**: 10  
  Windows Update CSP: [Update/ConfigureFeatureUpdateUninstallPeriod](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configurefeatureupdateuninstallperiod)  

  Configure a time after which feature updates can't be uninstalled.  

  After this period expires, the previous update bits are removed from the device, and it can no longer uninstall to a previous update version.  

  For example, consider an update ring with a feature update uninstall period of 20 days. After 25 days you decide to roll back the latest feature update and use the Uninstall option.  Devices that installed the feature update over 20 days ago can't uninstall it as they've removed the necessary bits as part of their maintenance. However, devices that only installed the feature update up to 19 days ago can uninstall the update if they successfully check in to receive the uninstall command before exceeding the 20-day uninstall period.  

## User experience settings  

User experience settings control the end-user experience for device restart and reminders. For more information about the behavior of each setting, see the   Windows Update CSP documentation.  

- **Automatic update behavior**  
  **Default**: Auto install at maintenance time  
  Windows Update CSP: [Update/AllowAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowautoupdate)  

  Choose how automatic updates are installed and, if necessary, when to restart the device.  

  Supported options:  

  - **Notify download** - Notify the user before downloading the update. Users choose to download and install updates.  

  - **Auto install at maintenance time** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, users are prompted to restart for up to seven days, and then restart is forced.  

    This option can restart a device automatically after the update installs. Use the **Active hours** settings to define a period during which the automatic restarts are blocked:  

    - **Active hours start** - Specify a start time for suppressing restarts due to update installations.  
      **Default**: 8 AM  
      Windows Update CSP: [Update/ActiveHoursStart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursstart)  
  
    - **Active hours end** - Specify an end time for suppressing reboots due to update installations.  
      **Default**: 5 PM  
      Windows Update CSP: [Update/ActiveHoursEnd](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursend)  

  - **Auto install and restart at maintenance time** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used. (This is the default for unmanaged devices.)  

    This option can restart a device automatically after the update installs. Use of the **Active hours** settings aren't described in Windows Update settings but are used by Intune to define a period during which the automatic restarts are blocked:  

    - **Active hours start** - Specify a start time for suppressing restarts due to update installations.  
      **Default**: 8 AM  
      Windows Update CSP: [Update/ActiveHoursStart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursstart)  
  
    - **Active hours end** - Specify an end time for suppressing reboots due to update installations.  
      **Default**: 5 PM  
      Windows Update CSP: [Update/ActiveHoursEnd](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursend)  

  - **Auto install and restart at scheduled time** - Specify an installation day and time. If unspecified, installation runs at 3 AM daily, followed by a 15-minute countdown to a restart. Logged on uses can delay countdown and restart.   
  Windows Update CSP: [Update/AllowAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowautoupdate)  

    This option supports additional settings.  

    - **Automatic behavior frequency** - Use this setting to schedule when updates are installed, including the week, the day, and the time.  
      **Default**: Every week

    - **Scheduled install day** - Specify on which day of the week you want updates to install.  
      **Default**: Any Day  

    - **Scheduled install time** - Specify the time of day when you want updates to install.  
      **Default**: 3 AM  

  - **Auto install and reboot without end-user control** - Updates download automatically and then install during Automatic Maintenance when the device isn't in use or running on battery power. When restart is required, the device restarts when not being used. This option sets the end-users control pane to read-only.  

  - **Reset to default** - Restore the original auto update settings on Windows 10 machines that run the October 2018 Update or later.  


- **Restart checks**  
  **Default**: Allow  
  Windows Update CSP: [Update/SetEDURestart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setedurestart)  

  To skip these checks when you restart a device, select **Skip**. 
  
  This setting has different results depending on the devices version of Windows:  
 
  - *Windows version 1703 and earlier* - When you restart a device, there are some checks that occur, including checking for active users, battery levels, running games, and more.  
  
  - *Windows version 1709 and later* - During Active Hours, the following processes don't run for updates: scan, download, install, and reboot. After Active Hours, the update processes do run and can wake the device from sleep, scan, download, install, and reboot the device as long as the battery checks and power checks pass. 

- **Block user from pausing Windows updates**  
  **Default**: Allow  
  Windows Update CSP: [Update/SetDisablePauseUXAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setdisablepauseuxaccess)  

  - **Allow** - Allow device users to pause the installation of an update.  
  - **Block** - Prevent device users from pausing the installation of an update.  

- **Block user from scanning for Windows updates**  
  **Default**: Allow  
  Windows Update CSP: [Update/SetDisableUXWUAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setdisableuxwuaccess) 

  - **Allow** - Allow device users to use Windows Update scan to find and download updates, and install features.
  - **Block** - Prevent device users from accessing the Windows Update scan, downloading updates, and installing features.  

- **Require user's approval to restart outside of work hours**  
  **Default**: Not configured  
  Windows Update CSP: [Update/AutoRestartRequiredNotificationDismissal](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-autorestartrequirednotificationdismissal)
  
  - **Not configured**  
  - **Required** - Require that a user approves a device restart outside of work hours.  
   
- **Remind user prior to required auto-restart with dismissible reminder (hours)**  
  **Default**: 4  
  Windows Update CSP: [Update/ScheduleRestartWarning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-schedulerestartwarning)  

  Specify how long in advance of an automatic restart to display a dismissible notification to a device user about that restart. Values of **2**, **4**, **8**, **12**, or **24** hours are supported.  
  
  When you clear the default value, this setting becomes *Not configured*.  

- **Remind user prior to required auto-restart with permanent reminder (minutes)**  
  **Default**: 15  
  Windows Update CSP: [Update/ScheduleImminentRestartWarning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduleimminentrestartwarning)  

  Specify how long in advance of an automatic restart to display a non-dismissible warning to a device user about that restart. Values of **15**, **30** or **60** minutes are supported.  

  When you clear the default value, this setting becomes *Not configured*.  

- **Change Update notification level**  
  **Default**: Use the default Windows Update notifications  
  Windows Update CSP: [Update/UpdateNotificationLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updatenotificationlevel)
  
  Specify what level of Windows Update notifications users see. This setting doesn't control how and when updates are downloaded and installed.  

  Supported options:
  - **Not configured**
  - **Use the default Windows Update notifications**
  - **Turn off all notifications, excluding restart warnings**
  - **Turn off all notifications, including restart warnings**  

- **Use deadline settings**  
  **Default**: Not configured  
 
  Allows user to use deadline settings.  

  - **Not configured**
  - **Allow**

  When set to *Allow*, you can configure the following settings for deadlines:

  - **Deadline for feature updates**  
    **Default**: *Not configured*  
    Windows Update CSP: [Update/ConfigureDeadlineForFeatureUpdates](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)  

    Specifies the number of days a user has before feature updates are installed on their devices automatically (2-30).

  - **Deadline for quality updates**  
    **Default**: *Not configured*  
    Windows Update CSP: [Update/ConfigureDeadlineForQualityUpdates](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)

    Specifies the number of days a user has before quality updates are installed on their devices automatically (2-30).

  - **Grace period**  
    **Default**: *Not configured*
    Windows Update CSP: [Update/ConfigureDeadlineGracePeriod]( https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod)

    Specifies a minimum number of days after deadline until restarts occur automatically (2-7).

  - **Auto reboot before deadline**  
    **Default**:  Yes
    Windows Update CSP: [Update/ConfigureDeadlineNoAutoReboot](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlinenoautoreboot)

    Specifies whether the device should auto reboot before deadline.
    - **Yes**
    - **No**

### Delivery optimization download mode  

Delivery optimization is no longer configured as part of a Windows 10 Update Ring under Software Updates. Delivery optimization is now set through device configuration. However, previous configurations remain available in the console. You can remove these previous configurations by editing them to be *Not configured*, but they can't otherwise be modified. 

To avoid conflicts between new and old policy, see [Remove Delivery Optimization from Windows 10 Update Rings](../configuration/delivery-optimization-windows.md#remove-delivery-optimization-from-windows-10-update-rings) and then move your settings to a Delivery optimization profile.
