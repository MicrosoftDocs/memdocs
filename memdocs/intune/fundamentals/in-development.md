---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 10/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:

ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page: 

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**This article was last updated on the date listed under the title above.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## App management

### Configure whether a required iOS app is removable<!-- 8391462  -->
You will be able to configure whether a required iOS app is installed as a removable app by end users. The new setting will apply to iOS store, LOB and built-in apps. You will be able to find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > **Add**. When setting the app assignments, you will be able to select **Install as removable**. The default value is **yes**, which means the app is removable. Existing required installs on iOS 14 will be updated to the default (removable) setting value when this setting is implemented. For more information about iOS apps, see [Microsoft Intune app management](..\apps\app-management.md).

### New show previews setting for app notifications on iOS/iPadOS devices<!-- 8351845  -->
On iOS/iPadOS devices, there's a **Show Previews** setting (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **App Notifications**). Use this setting to choose when recent app notification previews are shown on devices.

For more information on app notification settings, and other settings you can configure, see [device settings to use common iOS/iPadOS features](../configuration/ios-device-features-settings.md).

Applies to:
- iOS/iPadOS 14.0 and newer (supervised)

<!-- ***********************************************-->
## Device configuration

### Use NetMotion as a VPN connection type for Android Enterprise devices<!-- 7764263 -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile** or **Android Enterprise Work Profile** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise Work Profile
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

### On-demand rules with Microsoft Tunnel for iOS<!-- 8460915  -->
We're adding support to the Microsoft Tunnel to use on-demand rules for iOS devices. On-demand rules are configured in device configuration VPN profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** > **VPN**).

With on-demand rules you can specify the use of the VPN when conditions are met for specific FQDNs or IP addresses. 
 
<!-- ***********************************************-->
## Device enrollment

### Ending support for iOS 11<!--7327321 -->
After iOS 14 releases, Intune enrollment and the Company Portal app will support iOS versions 12 and later. Older versions won't be supported but will continue to receive policies.

### Ending support for macOS 10.12<!--7327326 -->
After macOS 11 releases, Intune enrollment and the Company Portal will support macOS versions 10.13 and later. Older versions won't be supported.

### Hide more Apple Automated Device Enrollment Setup Assistant Screens<!--7786092 -->
You'll be able to set Automated Device Enrollment (ADE) profiles to hide these Setup Assistant Screens for iOS/iPadOS 14.0+ and macOS 11+ devices:
- Restore Completed, for iOS/iPadOS 14.0+.
- Software Update Completed, for iOS/iPadOS 14.0+.
- Accessibility, for macOS 11+ (the mac device must be connected to an Ethernet).

<!-- ***********************************************-->
## Device management

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

### Subnet ID and IP addresses on Properties page for corporate-owned Windows devices<!--5265589 -->
Subnet ID and IP addresses will be displayed on the **Properties** page for corporate-owned Windows devices. To see them, go to [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > choose a corporate-owned Windows device > **Properties**.

### Personally-owned work profile terminology<!--8361769 -->
To avoid confusion, the term for the *work profile* Android Enterprise management scenario will be changed to "personally-owned devices with a work profile" or *personally-owned work profile* throughout the Intune documentation and user interface. This is to differentiate it from the "corporate-owned work profile" (COPE) management scenario.


<!-- ***********************************************-->
## Intune apps

 
### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->
The Company Portal app will store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager console. Users who have opted in to receive Company Portal push notifications will be able to view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [Device ownership notifications](../apps/company-portal-app.md#device-ownership-notification).

### Improvements to work profile messaging in Company Portal for Android<!--8378333 -->
We're updating messaging in Company Portal for Android to better introduce and explain how work profile works. The new messaging appears:  
1. After the work profile setup flow. Users will see a new informational screen explaining where to find work apps, with links to help documentation.
2. When a user accidentally re-enables the Company Portal app in the personal profile. We redesigned a screen (**Your device now has a profile just for work**) with clearer explanations and new illustrations to guide users to their work apps, with links to help documentation.
3. On the **Help** page > **Frequently Asked Questions** section, there's a new link to help documentation about how to set up work profile and find apps. 


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Noncompliant policies report to troubleshoot devices in error or noncompliant<!-- 6471368  -->
There's a new operational report to help troubleshoot errors and conflicts for compliance policies targeting devices. The "Noncompliant policies" report will show the list of compliance policies and the number of devices in an error or noncompliant state.

Administrators can use this report to:

- Drill down in a policy to see the list of devices and users in a failed state.
- Drill down to see the list of settings and setting information causing a failure.
- Filter, sort, and search across all records in the report.
- Identify when issues are occurring, and streamline troubleshooting.

For more information on monitoring and reporting, see [Monitor device compliance policies](../protect/compliance-policy-monitor.md) and [Intune reports](../fundamentals/reports.md).


### Account protection policy changes in Endpoint security<!--  7492116   --> 
We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)
 
After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Policy merge support for USB device ID’s in Device control profiles for endpoint security Attack surface reduction policy<!-- 7339038   -->
We’re expanding support for *policy merge* of Windows Defender Antivirus exclusions to support USB device ID’s. This support will be added to the *Device control* profile for the endpoint security Attack surface reduction policy. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > for **Platform** select *Windows 10 and later* > **Device control**).

With policy merge, the device ID's that are listed as part of different Device control profiles will merge into a single list for each device or user. That list is based on the individual policies that apply to a specific user or device. This merge will help to prevent conflicts between profiles and policies, and existing policies that were in conflict will no longer be in conflict for the device ID lists. 


### New co-management eligibility organizational report<!-- 7854306  -->
The **Co-management eligibility** report provides an eligibility evaluation for devices that can be co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management eligibility**. For related report information, see [Intune reports](../fundamentals/reports.md).

### New co-management device workloads organizational report<!-- 7854306  -->
The **Co-management device workloads** report provides a report of devices that are currently co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management device workloads**. For related report information, see [Intune reports](../fundamentals/reports.md).

### New Intune operational report to help troubleshoot configuration profile issues<!-- 6471222  -->
A new operational report will be available in public preview to help troubleshoot errors and conflicts for configuration profiles that have been targeted to devices. The **Assignment failures** report will show a list of configuration profiles for the tenant and the number of devices in a state of error or conflict. Using this information, you can drill down to a profile to see a list of devices and users in a failure state related to the profile. Additionally, you can drill down even further to view a list of settings and setting details related to the cause of the failure. You have the ability to filter, sort, and search across all of the records throughout the report. This report will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor** > **Assignment failures (preview)**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

### Reporting updates for Windows Virtual Desktop VMs<!--5736314 -->
The following settings will display as **Not applicable** in the Policy reports:
- BitLocker settings
- Device encryption
- Defender Application Guard settings
- Defender Tamper Protection
- Wi-Fi profiles

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Scripting-->


<!-- ***********************************************-->
## Security

### Improvements to settings in Attack surface reduction rule profiles <!-- 7319334  -->
We’re improving the settings in the Attack surface reduction rule profiles which are part of endpoint securities Attack surface reduction policy.  (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Windows 10 or later** for platform > **Attack surface reduction rules**).

The improvements include:

- Adding a new option of **Warn** to each applicable setting in the profile.
- For applicable settings, the configuration options will be consistent, supporting the following values:
  - **Disable** – The setting is off.
  - **Block** - Executable content downloaded from email and webmail clients will be blocked.
  - **Audit** - Windows events will be raised instead of blocking.
  - **Warn** - On devices that run Windows 10 version 1809 or later, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Block* behavior.
  - **Not configured** - The setting is off.
  - **User defined**

### Improved Antivirus status operations report for endpoint security<!-- 7771023    -->
We’re adding new details to the *Antivirus status operations* report for Windows Defender Antivirus, which is an endpoint security policy report. (**Reports** > **Microsoft Defender Antivirus** > **Antivirus agent status**).
 
The following new columns of information will be available for each device:
- Product status – The status of Windows Defender on the device.
- Tamper protection – Is tamper protection enabled or disabled.
- Virtual machine – Is the device a virtual machine, or physical device.

### Improved rule merge for Attack surface reduction rules<!--7798290  -->
We’re improving the conflict resolution behavior when rules merge for our *Attack surface reduction rules* profile, which is part of the endpoint security Attack Surface Reduction policy. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Windows 10 or later** for platform > **Attack surface reduction rules**).

With the new merge behavior, the values for settings that are part of different Attack surface reduction rule profiles that apply to a device will be merged into a single list. That list then applies to the device. This merge behavior will help prevent conflicts between profiles, and existing policies that were in conflict will no longer be in conflict. 

### New setting for Device Control profile for endpoint security<!-- 8456551    -->
We’re adding a new setting, **Block write access to removable storage** to the *Device control* profile for Attack surface reduction policy in endpoint security. (**Endpoint security** > **Attack surface reduction** > **Windows 10 or later** > **Device Control**).

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
