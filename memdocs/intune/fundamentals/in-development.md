---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
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

### Improvements to Devices page of iOS/iPadOS and macOS Company Portals<!-- 6055001  -->
We have made several improvements to the user experience of the **Devices** page of the Company Portal app for iOS/iPadOS and Mac. We revamped the **Devices** page to have a more modern feel and a better organization of device information. By using a single column with defined section headers, your organization's iOS/iPadOS and macOS users will be able to easily check the status of their devices to ensure they stay secure and maintain access to their organization's resources. Additionally, we added clearer messaging and additional troubleshooting steps for users whose devices fall out of compliance. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Improvements to the Company Portal for macOS enrollment experience<!-- 6444452  -->
The Company Portal for macOS enrollment experience will have a simpler enrollment process that aligns more closely with the Company Portal for iOS enrollment experience. Device users will see:  
- A sleeker user interface.  
- An improved enrollment checklist.  
- Clearer instructions about how to enroll their devices.  
- Improved troubleshooting options.  

For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Use Autonomous Single App Mode settings to configure the iOS Company Portal to be a sign-in/sign-out app<!-- 7055619  -->
You will be able to configure the iOS Company Portal to use autonomous single app mode (ASAM). You can use the ASAM settings in the Microsoft Endpoint Manager console to configure the iOS Company Portal to go in and out of single app mode upon sign-out and sign-in. When the Company Portal is in ASAM, users will not be able to use any other app or the home button on the device until they sign into the Company Portal. Upon sign-out, the Company Portal will go back into single app mode. 

To configure the Company Portal to be in ASAM in the Microsoft Endpoint Manager, select **Devices** > **Configuration profiles** > **Create profile**. Select **iOS/iPadOS** as the platform and select **Device restrictions** as the profile. In the **Configuration Settings** tab, select **Autonomous Single App Mode**. Set the **App name** to `Company Portal` and set the **App Bundle ID** to `com.app.CompanyPortal`. For more information, see [Autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) and [single app mode](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## Device configuration

### Set device compliance state from third-party MDM partners<!-- 6361689   -->
You’ll soon be able to allow the compliance state of iOS or Android devices managed by third-party Mobile Device Management (MDM) partners to be set in Azure Active Directory (Azure AD).

When Intune is configured for partner compliance, compliance data for devices managed by the third-party MDM partner is sent to Intune for compliance evaluation. The results are then passed to Azure AD where the compliance data is used to enforce your conditional access policies for those devices.

Support will soon include the following partners:
- VMware WorkspaceONE (previously known as AirWatch)

To enable a device compliance partner you’ll use a new node in the Microsoft Endpoint Manager admin center: **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management** where you’ll select **Add Compliance Partner**.

### Add a link to your company portal support website to emails for noncompliance<!-- 7225498    -->
We're adding a new setting to the email notification template that will add the link to your company portal website to email notifications that are sent to users of non-compliant devices. (**Endpoint security** > **Device compliance** > **Notifications** > **Create notification**).  Users who receive an email due to having a noncompliant device can use the link to open a website to learn more about why their device isn’t compliant.

### New FileVault setting for macOS Endpoint Protection device configuration policy<!-- 5459801   -->
We're adding a new setting to the FileVault category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) template: Hide recovery key. (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform* and then **Endpoint protection** for the *Profile type*). This setting hides the personal key from the end user during FileVault 2 encryption. A device user can view their personal recovery key at any time from the iOS company portal app or from the company portal website for the encrypted macOS device. To view the personal recovery key they can go to device details, and click on *get recovery key*.

This setting won't be available in previously created policy. You'll need to re-create FileVault policies to configure this setting to make use of it. 

### Configure content caching on macOS devices<!-- 7106872 -->
On macOS devices, you can create a configuration profile that configures content caching (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile). Use these settings to delete cache, allow shared cache, set a cache limit on the disk, and more.

For more information on content caching, see [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (opens Apple's web site).

To see the settings you can currently configure, go to [macOS device feature settings in Intune](../configuration/macos-device-features-settings.md).

Applies to:
- macOS

### Allow websites using TLS 1.0 and 1.1 to open in Safari on iOS/iPadOS and macOS devices<!-- 6524777  -->
On iOS/iPadOS and macOS devices, you can configure the **Allow deprecated TLS 1.0/1.1 behavior in Safari** setting (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Device restrictions** for profile type > **General**). 

Websites are deprecating support for TLS 1.0 and 1.1, and are only supporting TLS 1.2. This restriction allows users to use websites in Safari that haven't upgraded to TLS 1.2.

Applies to:
- iOS/iPadOS 13.4 and newer
- macOS 10.15.4 and newer

To see the other settings you can restrict, see [iOS/iPadOS](../configuration/device-restrictions-ios.md) and [macOS](../configuration/device-restrictions-macos.md) device restrictions.

### New VPN settings for Windows 10 and newer devices<!-- 6602122  -->
When you create a VPN profile using the IKEv2 connection type, there are new settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Base VPN**):

- **Device Tunnel**: Allows devices to automatically connect to VPN without requiring any user interaction, including user log on. This feature requires you to enable **Always On**, and use **Machine certificates** as the authentication method.
- Cryptography suite settings: Configure the algorithms used to secure IKE and child security associations, which allow you to match client and server settings.

To see the settings you can configure, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:
- Windows 10 and newer

### Block Shared iPad temporary sessions on Shared iPad devices<!-- 6613794 -->
In Intune, there's a new **Block Shared iPad temporary sessions** setting that blocks temporary sessions on Shared iPad devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Shared iPad**). When enabled, end users can't use the Guest account. They must sign in to the device with their Managed Apple ID and password. 

For more information on the settings you can configure, see [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:
- Shared iPad devices running iOS/iPadOS 13.4 and newer

### Use Microsoft Launcher as the default launcher for fully managed Android Enterprise devices<!-- 4927976  -->
On Android Enterprise device owner devices, you can set Microsoft Launcher as the default launcher for fully managed devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device owner** > **Device restrictions** for profile > **Device experience**). To configure all other Microsoft Launcher settings, use app configuration policies. 

Also, there are some other UI updates, including **Dedicated devices** being renamed to **Device experience**.

To see all the settings you can restrict, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md). 

Applies to:
- Android Enterprise device owner fully managed devices (COBO)

### Add new schema settings, and search for existing schema settings using OEMConfig on Android Enterprise<!-- 6394386  -->
In Intune, you can use OEMConfig to manage settings on Android Enterprise devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile). When you use the **Configuration designer**, the properties in the app schema are shown. Now, in the **Configuration designer**, you can:
- Add new settings to the app schema.
- Search for new and existing settings in the app schema.

For more information on OEMConfig profiles in Intune, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:
- Android Enterprise

<!-- ***********************************************-->
## Device enrollment

### Automated Device Enrollment sync errors<!-- 6988214 -->
New errors will be reported for iOS/iPadOS and macOS devices, including
- Invalid characters in the phone number or if that field is empty. 
- Invalid or empty configuration name for the profile. 
- Invalid/expired cursor value or if no cursor is found.
- Rejected or expired token. 
- The department field is empty or the length is too long. 
- Profile is not found by Apple and a new one needs to be created. 
- A count of removed Apple Business Manager devices will be added to the overview page where you see the status of your devices.

### Bring-your-own-devices can use VPN to deploy<!--5015344 -->
The new  Autopilot profile **Skip Domain Connectivity Check** toggle lets you deploy Hybrid Azure AD Join devices without access to your corporate network using your own 3rd party Win32 VPN client. To see the new toggle, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > **Windows enrollment** > **Deployment profiles** > **Create profile** > **Out-of-box experience (OOBE)**.

### Shared iPads for Business<!--6367326 -->
You'll be able to use Intune and Apple Business Manager to easily and securely set up Shared iPad so that multiple employees can share devices. Apple's [Shared iPad](https://developer.apple.com/education/shared-ipad/) provides a personalized experience for multiple users while preserving user data. Using a Managed Apple ID, users can access their apps, data, and settings after signing into any Shared iPad in their organization. Shared iPad works with federated identities.

To see this feature, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment program tokens** > choose a token > **Profiles** > **Create profile** > **iOS**. On the **Management Settings** page, select **Enroll without User Affinity** and you'll see the **Shared iPad** option.

**Applies to:** iPadOS 13.4 and later. This release added support for temporary sessions with Shared iPad so that users can access a device without a Managed Apple ID. Upon logout, the device erases all user data so that the device is immediately ready for use, eliminating the need for a device wipe. 

<!-- ***********************************************-->
## Device management

### Change primary user on co-managed devices<!--7319183 -->
You'll be able to change a device's primary user for co-managed Windows devices. For more information on how to find and change it, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md).

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Setting the Intune primary user also sets the Azure AD owner property<!--7319227 -->
This upcoming feature automatically sets the owner property on newly-enrolled Hybrid Azure AD joined devices at the same time that the Intune primary user is set. For more information on the primary user, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md).

This is a change to the enrollment process and only applies to newly enrolled devices. For existing Hybrid Azure AD Joined devices, you must manually update the Azure AD Owner property. To do this, you can use the [Change primary user feature](../remote-actions/find-primary-user.md#change-a-devices-primary-user) or [a script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

When Windows 10 devices become Hybrid Azure Azure Directory Joined, the first user of the device becomes the primary user in Endpoint Manager.  Currently, the user isn't set on the corresponding Azure AD device object. This causes an inconsistency when comparing the *owner* property from an Azure AD portal with the *primary user* property in Microsoft Endpoint Manager admin center. The Azure AD owner property is used for securing access to BitLocker recovery keys. The property isn't populated on Hybrid Azure AD Joined devices. This limitation prevents set up of self-service of BitLocker recovery from Azure AD. This upcoming feature solves this limitation.

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

### Remote lock pin availability for macOS devices<!--7281557-->
The availability for macOS device remote lock pins will be increased from 7 days to 30 days.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that is being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).