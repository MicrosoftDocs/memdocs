---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: conceptual
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

### Update to device icons in Company Portal and Intune apps on Android<!-- 6057023  -->
We're updating the device icons in the Company Portal and Intune apps on Android devices to create a more modern look and feel and to align with the Microsoft Fluent Design System. For related information, see [Update to icons in Company Portal app for iOS/iPadOS and macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### S/MIME for Outlook on iOS and Android Enterprise devices managed without enrollment<!-- 6517155  -->
You'll be able to enable S/MIME for Outlook on iOS and Android Enterprise devices using app configuration policies for devices managed without enrollment. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed apps**. Additionally, you can choose whether or not to allow users to change this setting in Outlook. For more information about Outlook configuration settings, see [Microsoft Outlook configuration settings](../apps/app-configuration-policies-outlook.md).

### iOS Company Portal will support Apple's Automated Device Enrollment without user affinity<!-- 7282707  --> 
iOS Company Portal will be supported on devices enrolled using Apple's Automated Device Enrollment without requiring an assigned user. An end user can sign in to the iOS Company Portal to establish themselves as the primary user on an iOS/iPadOS device enrolled without device affinity. For more information about Automated Device Enrollment, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

### Win32 app installation notifications and the Company Portal<!-- 7485945  -->
End users will be able to decide whether the applications shown in the [Microsoft Intune Web Company Portal](https://portal.manage.microsoft.com/) should be opened by the Company Portal app or the Web Company Portal. This option is only available if the end user has the Company Portal app installed and launches a Web Company Portal application outside of a browser.

### The Company Portal adds Configuration Manager application support<!-- 4297660 -->
The Company Portal now supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This support will help administrators consolidate their different end-user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## Device configuration

### Set device compliance state from third-party MDM partners<!-- 6361689   -->
Microsoft 365 customers who own third-party MDM solutions will be able to enforce Conditional Access policies for Microsoft 365 apps on iOS and Android via integration with Microsoft Intune Device Compliance service. Third-party MDM vendor will leverage the Intune Device Compliance service to send device compliance data to Intune. Intune will then evaluate to determine if the device is trusted and set the conditional access attributes in Azure AD.  Customers will be required to set Azure AD Conditional Access policies from within the Microsoft Endpoint Manager admin center or the Azure AD portal.  


### New VPN settings for Windows 10 and newer devices<!-- 6602122  -->
When you create a VPN profile using the IKEv2 connection type, there are new settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Base VPN**):

- **Device Tunnel**: Allows devices to automatically connect to VPN without requiring any user interaction, including user logon. This feature requires you to enable **Always On**, and use **Machine certificates** as the authentication method.
- Cryptography suite settings: Configure the algorithms used to secure IKE and child security associations, which allow you to match client and server settings.

To see the settings you can configure, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:
- Windows 10 and newer

### New features for Managed Home Screen on Android Enterprise device owner dedicated devices (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
On Android Enterprise devices, administrators will be able to use device configuration profiles to customize the Managed Home Screen on dedicated devices using multi-app kiosk mode (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only** > **Device Restrictions** for profile > **Device experience**).

Specifically, you can:

- Customize icons, change the screen orientation, and show app notifications on badge icons <!--7414175-->
- Hide the Managed Settings entry point <!--7133328-->
- Easier access the debug menu <!--7133720-->
- Create an allowed list of Wi-Fi networks <!-- 7134873-->
- Easier access to the device information <!-- 7135184-->

For more information, see [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise device owner, dedicated devices (COSU)

<!-- ***********************************************-->
## Device enrollment

### Corporate-owned, personally enabled devices (preview)<!--4442275 -->
Intune will support Android Enterprise corporate-owned devices with a work profile for OS versions Android 8 and above. Corporate-owned devices with a work profile is one of the corporate management scenarios in the Android Enterprise solution set. This scenario is for single user devices intended for corporate and personal use. This corporate-owned, personally-enabled (COPE) scenario offers:

- work and personal profile containerization
- device-level control for admins
- a guarantee for end users that their personal data and applications will remain private

The first public preview release will include a subset of the features that will be included in the generally available release. Additional features will be added on a rolling basis. The features that will be available in the first preview include:

- Enrollment: Admins can create multiple enrollment profiles with unique tokens that do not expire. Device enrollment can be done through NFC, token entry, QR code, Zero Touch, or Knox Mobile Enrollment.
- Device configuration: A subset of the existing fully managed and dedicated device settings.
- Device compliance: The compliance policies that are currently available for fully managed devices.
- Device Actions: Delete device (factory reset), reboot device, and lock device.  
- App management: App assignments, app configuration, and the associated reporting capabilities 
- Conditional Access



<!-- ***********************************************-->
## Device management

### Device compliance logs now in English<!--6014904 -->
The IntuneDeviceComplianceOrg logs only have enumerations for ComplianceState, OwnerType, and DeviceHealthThreatLevel. In a future update, these logs will have English information in the columns.

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Tenant attach: Device timeline in the admin center<!--7220536, CM7141381 -->
When Configuration Manager synchronizes a device to Microsoft Endpoint Manager through tenant attach, you'll be able to see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### Tenant attach: Install an application from the admin center<!-- 7220536, CM6024389 -->
You'll be able to initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Management admin center. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### Tenant attach: CMPivot from the admin center<!--7220536, CM6024392 -->
You'll be able to bring the power of [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### Tenant attach: Run Scripts from the admin center<!--7220536, CM6234688 -->
You'll be able to bring the power of the Configuration Manager on-premises [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### New merge logic for Windows 10 devices<!--179048-->
Today, if a customer reimages a device and then re-enrolls it, multiple records for the device will appear in the Microsoft Endpoint Manager admin console. New merge logic is in development to merge such duplicate records for Windows 10 devices.

### Updates to the remote lock action for macOS devices<!--7032805 -->
Updates to the remote lock action for macOS devices will include:
- The recovery pin will be displayed for 30 days before deletion (instead of seven days).
- If an admin has a second browser open and tries to trigger the command again from a different tab or browser, Intune will allow the command to go through. But the reporting status will be set to failed rather than generating a new pin.
- The admin won't be able to issue another remote lock command if the previous command is still pending or if the device hasn’t checked back in.
These changes are designed to prevent the correct pin from being overwritten after multiple remote lock commands.

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Additional Data Warehouse v1.0 properties<!-- 6125732   -->
Additional properties are available using the Intune Data Warehouse v1.0. The following properties are now exposed via the [devices](../developer/reports-ref-devices.md#devices) entity:
- `ethernetMacAddress` -  The unique network identifier of this device.
- `office365Version` - The version of Office 365 that is installed on the device.

The following properties are now exposed via the [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) entity:
- `physicalMemoryInBytes` - The physical memory in bytes.
- `totalStorageSpaceInBytes` - Total storage capacity in bytes.

For more information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that are being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## Role-based access control

### Scope tag support for customization policies<!--6182440 -->
You'll be able to assign scope tags to Customization policies. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration**> **Customization** where you will see **Scope tags** configuration options.

### Assign profile and Update profile permission changes<!--7177586 -->
Role-based access control permissions will be changing for Assign profile and Update profile:
- Assign profile: Admins with this permission will be able to also assign the profiles to tokens and assign a default profile to a token.
- Update profile: Admins with this permission will be able to update existing profiles only.

<!-- ***********************************************-->
## Security

### App protection policy support for Symantec Endpoint Security and Check Point Sandblast<!--  4452423, 4731168 -->

In October of 2019, Intune app protection policy added the capability to use data from some of our Microsoft Threat Defense partners (MTD partners). We are adding support for the following partners, to use an app protection policy to block, or selectively wipe the user's corporate data based on the health of a device:

- **Check Point Sandblast** on Android, iOS and iPadOS
- **Symantec Endpoint Security** on Android, iOS and iPadOS

For information about using app protection policy with MTD partners, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Store the recovery key for a macOS device that was encrypted with FileVault before enrolling with Intune<!--5239424   -->
Soon, end users of a macOS device that wasn’t encrypted by FileVault policy from Intune, or was encrypted prior to being enrolled with Intune, won’t need to decrypt their device so it can then be re-encrypted by Intune. Instead, the current encryption can stay in place and the user can go to the Company Portal website where they can choose *Store recovery key* to submit their personal recovery key for the encrypted macOS device. Upon submission of a valid key, Intune will rotate the personal key to generate a new key, which remains available to the user through the Company Portal website, the iOS/ Company Portal, the Android Company Portal, or the Intune app. Users can then access those locations from any device to view the key should they become locked out of their macOS device.

### Hide the personal recovery key from a device user during macOS FileVault disk encryption<!--  5475632  -->
We’re adding a new setting called *Hide recovery key* to the endpoint security disk encryption policy for FileVault (**Endpoint security** > **Disk encryption** > **Create profile** > **macOS** > **FileVault**). When you enable the new setting, Intune hides the personal recovery key from the user of the macOS device during encryption. By hiding the key at this time, you can help keep it secure as users won’t be able to write it down while waiting for the device to encrypt. Instead, if recovery is needed, a user can always use any device to view their personal recovery key through the Intune Company Portal website.

### Improved view of security baseline details for devices<!-- 5536846   -->
We're working to improve the display of details for security baseline settings, when you drill into the details for a device (**Endpoint security** > **Devices**).  For each assigned security baseline, you’ll be able to view a flat list of details for each setting that includes setting categories, setting names, and the state of each setting on that device.

### Manage source locations for definition updates with endpoint security antivirus policy for Windows 10 devices<!-- 6347801  -->  
We’re adding two new settings to the *Updates* category of endpoint security antivirus policy for Windows 10 devices what can help you manage how devices get update definitions (**Endpoint security** > ** Antivirus** > **Create Policy** > **Windows 10 and later** > **Microsoft Defender Antivirus**).

With the new settings, you’ll be able to add UNC file shares as download source locations for definition updates, and define the order in which different source locations are contacted. The new settings will manage the following Defender CSPs:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### Endpoint detection and response policy for onboarding Tenant Attached devices to MDATP is moving out of preview<!-- 7303816   -->
As part of endpoint security in Intune, the Endpoint detection and response (EDR) policies support for use with devices managed by Configuration Manager will soon move out of preview and become Generally Available (**Endpoint security** > **Endpoint detection and response** > **Create Policy** > **Windows 10 and windows Server**). When you configure [Tenant Attach for Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md), you can then use the EDR policies to onboard devices managed by Configuration Manager to Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). 

### Improvements for the security baselines node<!-- 7433136   -->
To improve the usability of the security baseline node in the Microsoft Endpoint Manager admin center, we’re removing the *Overview* tab for each baseline and will instead open the baselines **Profile** tab (**Endpoint security** > **Security baselines** > *baseline*).

The *Overview* page for each baseline displays charts and tiles that aggregate results from the last baseline version you deployed. That information is duplicated from what you see if you drill-in to a version for more details. After the *Overview* page is removed, those charts and aggregate details will remain available when you drill into the version directly.  

### Firewall rule migration tool preview<!-- 6423187  -->
As a public preview, we're working on a PowerShell based tool that will migrate Windows Defender Firewall rules. When you install and run the tool, it automatically creates Endpoint security Firewall Rule policies for Intune that are based on the current configuration of a Windows 10 client.

### New settings for the Device Control profile in endpoint security Attack surface reduction policy<!--7032084 -->
We’re adding several settings for Windows 10 devices to the Device control profile for endpoint security Attack surface Reduction policy (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Windows 10 and later** > **Device control**). 

The new settings will be the same as those settings that are available today in [Device restriction profiles](../configuration/device-restrictions-windows-10.md) for *Device configuration*. The settings being added to the *Device control* profile should include various Bluetooth settings.  


<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
