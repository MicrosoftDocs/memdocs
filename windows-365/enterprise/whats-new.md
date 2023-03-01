---
# required metadata
title: What's new in Windows 365 Enterprise
titleSuffix:
description: Find out what's new in Windows 365 Enterprise
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/28/2023
ms.topic: reference
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# What's new in Windows 365 Enterprise

Learn what new features are available in Windows 365 Enterprise.

> [!NOTE]
> Each monthly update may take up to a week to rollout to all customers.

<!-- Common categories:  
### App management
### Device configuration
### Device provisioning
### Device management
### Device security
### Apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
### End user experience
### Windows 365 Government
### Windows 365 app
-->

<!-- ########################## -->
## Week of February 27, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Windows 365 app is now generally available<!--41929443-->

The Windows 365 app has moved out of preview and into general availability. For more information, see [Installing the Windows 365 app](https://support.microsoft.com/topic/cbb0d4d5-69d4-4f00-b050-6dc7a02d02d0).

#### Improved video playback by using multimedia redirection is now generally available<!--43524455-->

Improved video playback performance on your Cloud PCs by using multimedia redirection (MMR) has moved out of preview and into general availability. For more information, see [Video playback improvement](troubleshooting.md#video-playback-improvements).

#### Cloud PC web client: improved feedback interface for end users<!--43309221-->

The Cloud PC web client (accessible from windows365.microsoft.com) has an improved feedback interface for end users to provide feedback.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Hardware acceleration for the windows365.microsoft.com web client<!--43105503-->

On the windows365.microsoft.com web client, you can now benefit from hardware acceleration. This option is turned on by default and improves motion performance for activities like scrolling, moving windows, or playback of video.

#### Configure installed language and region for provisioning Cloud PCs in GCC/H environments<!--43290793 -->

When creating a provisioning policy, admins can now configure the installed language and region for new Cloud PCs in US Government Community Cloud (GCC) and GCC High environments. For more information, see [Provide users a localized Windows experience](provide-localized-windows-experience.md)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Add more Azure Network Connections to a provisioning policy<!--42906565-->

A new Azure Network Connection (ANC) option lets you add more ANCs to a provisioning policy and define a priority order for their use. By preparing multiple ANCs in different Azure regions, admins can make provisioning more reliable in the rare case capacity constraints in a region.

#### GCC/H support for geography option in Windows 365 provisioning policy<!-- 41400209-->

The **Geography** setting in provisioning policies is now supported for US Government Community Cloud (GCC) and GCC High environments. For more information, see [Create provisioning policies](create-provisioning-policy.md).

<!-- ########################## -->
## Week of February 20, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### Citrix HDX Plus support is now generally available<!--38310774 -->
Windows 365 support for Citrix HDX Plus has moved out of preview and into general availability. For more information, see [Set up Citrix HDX Plus for Windows 365 Enterprise](set-up-citrix.md).

<!-- ########################## -->
## Week of February 6, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Nested virtualization now supports 4vCPU Cloud PCs<!--42948140-->

Windows 365 nested virtualization now supports 4vCPU Cloud PCs. For more information, see [Set up virtualization-based workloads support](nested-virtualization.md).

<!-- ########################## -->
## Week of January 30, 2023 (Service release 2301)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Windows 365 app now supports Windows 10<!--42212516-->

The [Windows 365](https://support.microsoft.com/topic/cbb0d4d5-69d4-4f00-b050-6dc7a02d02d0) app now supports Windows 10.

#### Microsoft Teams: Share application windows from Windows 365 Cloud PC<!--43105503-->

In Microsoft Teams, you can now share specific windows from your Cloud PC desktop. Previously, you could only share the full Cloud PC desktop.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Open Cloud PCs in a Remote Desktop app from windows365.microsoft.com<!--42949050-->

From windows365.microsoft.com, you can now open a Cloud PC in a Remote Desktop app. For more information, see [Access a Cloud PC](../end-user-access-cloud-pc.md#home-page).

#### Improved feedback interface for end users<!--42949123-->

windows365.microsoft.com has improved the interface for end users to provide feedback.

#### Get Cloud PC connection details from windows365.microsoft.com<!--43105503-->

On windows365.microsoft.com, you can now get Cloud PC connection details like transport protocol, round-trip time, frame rate, and more.

<!-- ########################## -->
## Week of January 16, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Windows 365 Government support for forensic auditing of Cloud PCs<!--41237533-->

Forensic auditing is now available for Windows 365 Government. For more information, see [Digital forensics and Windows 365 Enterprise Cloud PCs](digital-forensics.md) and [Place a Cloud PC under review](place-cloud-pc-under-review.md).


<!-- ########################## -->
## Week of January 2, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Support for custom Windows 365 RBAC roles now generally available<!--42650520  -->

Support for custom Windows 365 role-based access control (RBAC) roles has moved out of preview and into general availability. These custom roles are also now supported for Windows 365 Government (Government Community Cloud and Government Community Cloud High). For more information, see [Custom roles](role-based-access.md#custom-roles).

<!-- ########################## -->
## Week of December 12, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Provision Azure Active Directory Join Cloud PCs with single sign-on (public preview)<!--42104318-->

Windows 365 now supports creating Azure Active Directory Join Cloud PCs that use single sign-on for Cloud PC login. Existing Cloud PCs won’t have single sign-on configured. For more information, see [Create provisioning policy](create-provisioning-policy.md) and [Edit provisioning policy](edit-provisioning-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Configure installed language and region for provisioning Cloud PCs generally available<!--42137636-->

Language pre-configuration for Cloud PCs has moved out of preview and into general availability. Admins can select the **Language & Region pack** under **Configuration** in their provisioning policy to pre-configure the language for the endpoint devices. For more information, see [Use a provisioning policy to set up a default display language on Cloud PCs](use-provisioning-policy-default-display-language.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New Third-party connector column on All devices page<!--42555983-->

There's a new column on the **All devices page**: **Third-party connector**. For more information, see [Device management overview for Cloud PCs](device-management-overview.md).

#### Retry Citrix agent installation<!--42555983-->

You can now use the **Retry Citrix agent installation** option instead of doing a full provisioning retry. For more information, see [Retry Citrix agent installation](retry-citrix-agent-installation.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Windows 365 deployment options

We’ve published a new help documentation article. For more information, see [Windows 365 deployment options](deployment-options.md).

<!-- ########################## -->
## Week of December 5, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for RDP Shortpath for public networks now generally available<!--41057892-->
Support for RDP Shortpath for public networks has moved out of preview and into general availability. For more information about RDP Shortpath, see [Use RDP Shortpath for public networks with Windows 365](rdp-shortpath-public-networks.md).

<!-- ########################## -->
## Week of November 28, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New Geography option in Windows 365 provisioning policy<!-- 41400209-->

The new **Geography** setting gives admins two ways to choose Azure regions during provisioning.

- You can select a specific region to make sure that your Cloud PCS are only provisioned in that region.
- You can select **Automatic** to let the Windows 365 service automatically select a region (within the Geography) at the time of provisioning.

Existing provisioning policies will automatically populate the **Geography** and **Region** settings based on existing settings. No admin action is required.  

For more information, see [Create provisioning policies](create-provisioning-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Windows 365 app

#### Updated Windows 365 app installation to install dependent applications<!--42190185-->

The Windows 365 app installation process has been updated to automatically install dependent applications.

#### Azure Active Directory policy updated for Windows 365 app<!--42190185-->

The Azure Active Directory (Azure AD) policy has been updated so that no extra Conditional Access policy change is required to use the Windows 365 app.

<!-- ########################## -->
## Week of November 14, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Use the Enrollment Status Page with Cloud PCs

We’ve published a new help documentation article. For more information, see [Use the Enrollment Status Page with Cloud PCs](enrollment-status-page.md).

<!-- ########################## -->
## Week of November 7, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 Government now supports Windows 11 and Secure boot<!--42089070-->

Windows 365 Government now supports the following features:

- Creating Cloud PCs that use [Secure boot](/windows-hardware/design/device-experiences/oem-secure-boot).
- Windows 11 options in the gallery images list.
- Creating custom images running Windows 11 (must be Generation 2 virtual machines).

<!-- ########################## -->
## Week of October 24, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Point-in-time restore now generally available<!--37063579-->

Point-in-time restore has moved out of preview and into general availability. For more information, see [Point-in-time restore for Windows 365 Enterprise](restore-overview.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New supported Azure region: UAE North<!--41670300-->

A new Azure region is now supported for Windows 365 Cloud PC provisioning: UAE North.

For more information about supported Azure regions, see [Supported Azure regions for Cloud PC provisioning](requirements.md#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ########################## -->
## Week of October 17, 2022

<!-- ***********************************************-->
### Monitor and troubleshoot

#### New Azure Network Connection health check<!--41752775-->

A new check has been added the Azure Network Connection health checks: **UDP connection server reachable**. For more information, see [Azure network connections health checks](health-checks.md).

#### Forensic auditing of Cloud PCs now generally available<!--41237533-->

Forensic auditing has moved out of preview and into general availability. For more information, see [Digital forensics and Windows 365 Enterprise Cloud PCs](digital-forensics.md) and [Place a Cloud PC under review](place-cloud-pc-under-review.md).

<!-- ########################## -->
## Week of October 10, 2022

<!-- ***********************************************-->
### Apps

#### Windows 365 app in public preview<!--41161804-->

A new app to sign in to and manage your Windows 365 Cloud PCs is now in public preview. The app provides functionality similar to the windows365.microsoft.com web site for accessing and managing your Cloud PCs. For more information, see [Installing the Windows 365 app](https://support.microsoft.com/topic/cbb0d4d5-69d4-4f00-b050-6dc7a02d02d0). 

<!-- ***********************************************-->
### Device provisioning

#### Support for US Government environments<!--35234096 -->

Government organizations can now use Windows 365 services first in US Government Community Cloud (GCC) High environments and later in GCC environments. All Windows 365 dependency services must also be used by the organization within the associated Government environment. For more information, see [What is Windows 365 Government?](introduction-windows-365-government.md)

<!-- ***********************************************-->
### Partners

#### Use Citrix HDX Plus with Windows 365 Enterprise<!--41294492-->

You can now use Citrix HDX Plus with Windows 365 Enterprise Cloud PCs. For more information, see [Set up Citrix HDX Plus for Windows 365 Enterprise](set-up-citrix.md).

<!-- ***********************************************-->
### Monitor and troubleshoot

#### Cloud PC utilization report<!--40636545 -->

A new report is now available for Cloud PCs. The **Cloud PC utilization** report shows how many hours users have been connected to their Cloud PCs. Information for individual Cloud PCs and aggregated data is also shown. For more information, see [Cloud PC utilization report](report-cloud-pc-utilization.md).

#### Cloud PC with connection quality issues report<!--40636545 -->

A new report is now available for Cloud PCs. The **Cloud PCs with connection quality issues** report shows information for round-trip time, available bandwidth, and remoting sign-in time. Information for individual Cloud PCs and aggregated data is also shown. For more information, see [Cloud PC connection quality report](report-cloud-pc-connection-quality.md).

<!-- ########################## -->
## Week of September 26, 2022 (Service release 2209)

<!-- ***********************************************-->
### Monitor and troubleshoot

#### System alerts and email notifications (preview)<!--40932899 -->

You can now set up system alerts and automated emails to be notified when certain events, warnings, or errors occur in the Windows 365 service. A subset of critical Cloud PC issues will be sent automatically to admins. In addition, you can define alert rules, such as target audience (devices, user groups, tenants), thresholds, frequency, and notification channels. For more information, see [Alerts](alerts.md).

<!-- ***********************************************-->
### Miscellaneous

#### Allow list URL change for Windows 365<!--41400001 -->

We've added a new endpoint which the Windows 365 service requires to be accessible: *.infra.windows365.microsoft.com". This is part of ongoing endpoint consolidation work to reduce the number of FQDNs required to be accessible for the service.

<!-- ########################## -->
## Week of September 19, 2022

<!-- ***********************************************-->
### Device management

#### Downsize Cloud PCs (Preview)<!--41076858 -->

You can now downsize a Cloud PC's RAM and specifications (except disk size). For more information, see [Resize a Cloud PC](resize-cloud-pc.md).

<!-- ***********************************************-->
### Device provisioning

#### Windows 365 Cloud PC support for Windows 11 Enterprise version 22H2<!--41359336-->

New gallery images are now available that include support for Windows 11 version 22H2. The following gallery images can be used for newly provisioned Cloud PCs:

- Win11 22H2 + M365 Apps
- Win11 22H2 + Optimizations

<!-- ########################## -->
## Week of August 29, 2022 (Service release 2208)

<!-- ***********************************************-->
### Monitor and troubleshoot

#### New health check: Localization language package readiness<!--41089729  -->

The **Azure network connection** tab has a new health check: **Localization language package readiness**. This health check verifies that the operating system and Microsoft 365 language packages can install.  It also makes sure that the localization package download link is reachable. For more information, see [Azure network connection health checks](health-checks.md).

#### Review Cloud PC connectivity health checks and errors in Microsoft Intune admin center<!--38469622 -->

You can now review connectivity health checks and errors in the Microsoft Intune admin center to help you understand if your users are experiencing connectivity issues. You’ll also get a troubleshooting tool to help resolve connectivity issues. To see the checks, select **Devices** > **Windows 365** > **Azure network connections** > select a connection in the list > **Overview**. This feature is rolling out to all customers over the next few weeks.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New supported Azure regions: East Asia, Korea Central, Norway East, Switzerland North<!--37678838-->

New Azure regions are now supported for Windows 365 Cloud PC provisioning: East Asia, Korea Central, Norway East, and Switzerland North.

For more information about supported Azure regions, see [Supported Azure regions for Cloud PC provisioning](requirements.md#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ########################## -->
## Week of August 22, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Restrict Office 365 services to Cloud PCs

We’ve published a new help documentation article. For more information, see [Restrict Office 365 services to Cloud PCs](restrict-office-365-cloud-pcs.md).

<!-- ########################## -->
## Week of August 15, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Language and region configuration now also applies to Microsoft 365 Apps<!--40673170-->

Provisioning policies configured for language now also apply to Microsoft 365 Apps. When a user first signs in, their Microsoft 365 Apps will use the configured language. For more information, see [Provide a localized Windows experience](provide-localized-windows-experience.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Remoting connection report in Endpoint Analytics now generally available<!--38310774 -->
The remoting connection report in Endpoint Analytics has moved out of preview and into general availability. For more information, see [Remoting connection report](report-remoting-connection.md).

#### Resource performance report in Endpoint Analytics now generally available<!-- 40028465 -->

The resource performance report in Endpoint Analytics has moved out of preview and into general availability. For more information, see [Resource performance report](report-resource-performance.md).

<!-- ########################## -->
## Week of August 8, 2022

### Documentation

#### New documentation article: Windows 365 security

We’ve published a new help documentation article. For more information, see [Windows 365 security](security.md).

<!-- ########################## -->
## Week of July 25, 2022

### Resize action support for more Cloud PCs<!--40263425  -->

The resize action now supports Cloud PCs that are Azure Active Directory joined.

<!-- ########################## -->
## Week of July 18, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Cloud PC Outlook mail sync setting<!--40423390-->

For newly provisioned and reprovisioned Cloud PCs, you can now set the Outlook mail sync setting to 6 or 12 months.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 11 optimized image now available for Windows 365 Cloud PCs<!--39890525 -->

You can now choose the **Windows 11 Enterprise + OS Optimizations** image when creating a new provisioning policy. This feature is rolling out to all customers over the next few weeks.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Provision Cloud PCs with Secure Boot<!--38012584-->

Support for creating Cloud PCs that use [Secure boot](/windows-hardware/design/device-experiences/oem-secure-boot) functionality is now available in Europe, APAC, and North American regions. Existing Cloud PCs won't have secure boot automatically enabled.

<!-- ########################## -->
## Week of July 4, 2022 (Service release 2206)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Support for virtualization-based workloads now generally available<!--39989666 -->
Support for virtualization-based workloads has moved out of preview and into general availability. For more information, see [Set up virtualization-based workloads on your Cloud PC](nested-virtualization.md).

<!--***********************************************-->
### End user experience

#### Transfer files from your Cloud PC by using windows365.microsoft.com web client<!--40096523-->
You can use the windows365.microsoft.com web client to transfer files to and from your Cloud PC. For more information, see [Transfer files to and from a Cloud PC](../end-user-access-cloud-pc.md#transfer-files-to-and-from-a-cloud-pc).

<!-- ***********************************************-->
### Monitor and troubleshoot

#### New health check: verify that Intune enrollment restrictions allow Windows enrollment<!--39998861 -->

The **Azure network connection** tab has a new health check: **Intune enrollment restrictions allow Windows enrollment**. This health check verifies that Intune enrollment restrictions are configured to allow Windows enrollment. Windows 365 Enterprise requires Intune enrollment during provisioning.

<!-- ########################## -->
## Week of June 6, 2022 (Service release 2205)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Forensic auditing of Cloud PCs<!--38726407-->

You can now place a Cloud PC under review. This action starts a process to create a secure snapshot of a Cloud PC. You can then analyze the snapshot using electronic discovery solutions. For more information, see [Digital forensics and Windows 365 Enterprise Cloud PCs](digital-forensics.md) and [Place a Cloud PC under review](place-cloud-pc-under-review.md).

<!-- ########################## -->
## Week of May 16, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for RDP Shortpath for public networks<!--39316531-->

Windows 365 Enterprise Cloud PCs now support RDP Shortpath for public networks. For more information about RDP Shortpath, see [Use RDP Shortpath for public networks (preview) with Windows 365](rdp-shortpath-public-networks.md).

#### Windows 365 ending support for Windows 10 version 1909 (19H2)<!--39606471-->

Windows 365 no longer supports Windows 10 version 1909 (19H2).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### User experience

#### Windows 365 Cloud PC support for Teams background effects<!--39892746-->

Windows 365 Cloud PCs now support background effects in Teams. For more information, see the blog [Microsoft Teams background effects generally available on Windows 365](https://techcommunity.microsoft.com/t5/windows-365/microsoft-teams-background-effects-generally-available-on/m-p/3403274).

#### Windows 365 Cloud PC support for Teams multi-window and Call me <!--39892759-->

Windows 365 Cloud PCs now support multi-window and Call Me in Teams. For more information, see the blog [Teams Multi-window support and Call Me generally available on Windows 365]( https://techcommunity.microsoft.com/t5/windows-365/teams-multi-window-support-and-call-me-generally-available-on/m-p/3403252).

<!-- ########################## -->
## Week of May 9, 2022 (Service release 2204)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for Azure AD joined Cloud PCs now general available<!--38765480 -->
Support for Azure AD joined Cloud PCs has moved out of preview and into general availability.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Provision Cloud PCs with Secure Boot<!--38012584 -->

Cloud PC support for [Secure boot](/windows-hardware/design/device-experiences/oem-secure-boot) functionality is now rolling out in Asia Pacific (APAC) regions and Europe. This feature will roll out to all customers over the next few months.

<!-- ########################## -->
## Week of May 2, 2022

### Documentation

#### New documentation article: Manage Windows 365 Cloud PCs with Configuration Manager

We’ve published a new help documentation article. For more information, see [Manage Windows 365 Cloud PCs with Configuration Manager](manage-cloud-pcs-using-configuration-manager.md).

<!-- ########################## -->
## Week of April 18, 2022

### On-premises network connection has been renamed to Azure network connection<!--38457869 -->

The term **on-premises network connection** has been renamed to **Azure network connection** in all user interfaces, documentation, and communications.

### Change Cloud PC time zone<!--38902639 -->

Non-admin users can now change their Cloud PC’s time zone.

<!-- ########################## -->
## Week of April 11, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts

#### Windows365-PSScripts GitHub repository is now open for contributions

The Windows365-PSSCripts GitHub repository is now open. It contains Windows 365-related scripts to help admins manage Cloud PCs. You can also contribute your own scripts to help others use Windows 365.

For more information, see the [Windows365-PSScripts GitHub repository readme](https://github.com/microsoft/Windows365-PSScripts).

<!-- ########################## -->
## Week of April 4, 2022 (Service release 2203)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

[!INCLUDE [Live captions for Microsoft Teams on Windows 365 Cloud PCs](../includes/whats-new-live-captions-teams.md)]

#### Nested virtualization (preview)<!--37800910 -->

For most currently supported regions, Windows 365 8vCPU/32GB licenses now support nested virtualizations for different developer scenarios to use systems like WSL/Hyper-V. Southeast Asia and West US 2 aren't currently supported for this feature. For more information, see [Set up nested virtualization on your Cloud PC](nested-virtualization.md).

#### Improve video playback by using multimedia redirection<!--38686511-->

You can improve video playback performance on your Cloud PCs by using multimedia redirection (MMR). For more information, see [Video playback improvement](troubleshooting.md#video-playback-improvements).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### windows365.microsoft.com now generally available<!--38195529-->

The [windows365.microsoft.com](https://windows365.microsoft.com/) web client has moved out of preview and into general availability.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Upload a custom image without an Azure network connection<!--8341750 -->

Customers using Azure Active Directory (Azure AD) Join without bringing an Azure virtual network can now upload custom images directly on the image tab in Microsoft Endpoint Manager. Previously, to upload an image, customers needed to create an ANC for the destination Azure subscription that provides the image.

#### Cloud PC name appended to the network interface name<!--38793957-->

A Cloud PC’s name is now appended to the network interface name within the Azure portal. This naming makes it easier to find the IP address for the Cloud PC when an Azure network connection is selected. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End-user experience

[!INCLUDE [End user feedback and log collection](../includes/whats-new-feedback-log-collection.md)]

<!-- ########################## -->
## Week of March 24, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New remote action: Remote Help<!--38310389-->

The [Remote Help remote action](/mem/intune/remote-actions/remote-help) (in the Microsoft Intune admin center) lets admins start a remote session into an end user’s Cloud PC.

<!-- ########################## -->
## Week of February 28, 2022 (Service release 2202)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Point-in-time restore (preview)<!--37063579-->

Administrators and users can now restore a Cloud PC to a state from a previous point in time. Multiple near-term and long-term restore points are available. For more information, see [Point-in-time restore for Windows 365 Enterprise](restore-overview.md).

#### Higher Cloud PC screen resolution option (preview)<!--38301718 -->

Cloud PC users can now choose a higher screen resolution when they connect to their Cloud PC from https://windows365.microsoft.com.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Windows 365 approved partners

We’ve published a new help documentation article. For more information, see [Windows 365 approved partners](../partners.md).

<!-- ########################## -->
## Week of February 14, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Windows 365 identity and authentication

We’ve published a new help documentation article. For more information, see [Windows 365 identity and authentication](identity-authentication.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for Azure AD joined Cloud PCs<!-- 35060203 36751258-->

Windows 365 Enterprise now supports Cloud PCs that are Azure AD joined. These devices can run in either:

- A Microsoft-hosted network:
  - You don’t need to bring any Azure infrastructure
  - You don't need to create an Azure network connection
- Your own network (using an Azure network connection)

#### Configure installed language and region for provisioning Cloud PCs<!--37095808 -->

When creating a provisioning policy, admins can now configure the installed language and region for new Cloud PCs. Previously, Cloud PCs were only created with English (United States). For more information, see [Provide users a localized Windows experience](provide-localized-windows-experience.md)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Use Collect diagnostics to collect more details from Windows 365 devices through Intune remote actions<!--37678745 -->

Intune’s remote action to Collect diagnostics now collects more details from Windows 365 Cloud PCs.

The new details for Windows 365 Cloud PCs include the following registry data:

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\AddIns\WebRTC Redirector
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Teams\

To learn more about the **Collect diagnostics** remote action, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New supported Azure regions: US Central and German West Central<!--37678838 -->

Two new Azure regions are now for Windows 365 Cloud PC provisioning: US Central and German West Central.

For more information about supported Azure regions, see [Supported Azure regions for Cloud PC provisioning](requirements.md#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ########################## -->
## Week of January 17, 2022

#### New documentation article: Optimize Cisco Webex on a Windows 365 Cloud PC<!--37106382-->

We’ve published a new help documentation article. For more information, see [Optimize Cisco Webex on a Windows 365 Cloud PC](cisco-webex-support.md).

<!-- ########################## -->
## Week of January 10, 2022

#### New documentation: Data encryption in Windows 365<!--36626607-->

We've added information to the help documentation about encryption for Windows 365 Cloud PCs. For more information, see [Data encryption in Windows 365](encryption.md).

<!-- ########################## -->
## Week of January 3, 2022

#### New documentation: Gallery image update cycle<!--36626607-->

We've added information to the help documentation about the update cycle for Windows 365 Cloud PC gallery images. For more information, see [Gallery image update cycle](device-images.md#gallery-image-update-cycle).

<!-- ########################## -->
## Week of December 13, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Cloud PCs in grace period count towards active Cloud PC license usage<!-- 37017463-->

Cloud PCs that are in grace period now count towards your active Cloud PC license usage. This policy makes sure that your organization’s active Cloud PC allocation matches the total available licenses in your tenant.

For more information about grace period, see [Device management overview](device-management-overview.md) and [End grace period](end-grace-period.md).

<!-- ########################## -->
## Week of November 29, 2021 (Service release 2111)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Operating system end of support status for Cloud PCs<!--36852572 -->

The **Provisioning policies** page has a new column: **Image status**. It tells you if the device image for each provisioning policy uses an operating system (OS) that is supported by Microsoft Windows security and other updates. For more information, see [Lifecycle policies and end of support for Cloud PC OS](end-of-support.md).

#### New documentation article: Optimize Zoom on a Windows 365 Cloud PC<!--37106382-->

We’ve published a new help documentation article. For more information, see [Optimize Zoom on a Windows 365 Cloud PC](zoom-support.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Two new security baseline settings for Windows 11 Cloud PCs<!--36989243 -->

Windows 365 Enterprise now supports the following Windows 11 security baseline settings:

- **Tamper Protection**: Helps protect Cloud PCs from bad actors bypassing security features like anti-virus protection.

- **Script Scanning**: Helps identify possible threats by intercepting scripts and scanning them before they’re run.

For more information about the security baseline updates for Windows 11, see [Windows 11 Security baseline](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/windows-11-security-baseline/ba-p/2810772). For more information about setting security baselines for Cloud PCs, see [Deploy security baselines](deploy-security-baselines.md).

<!-- ########################## -->
## Week of November 1, 2021 (Service release 2110)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Improved user interface for online access to Cloud PCs<!--36735456 -->

The user interface on [windows365.microsoft.com](https://windows365.microsoft.com) has been improved with:

- Faster load times.
- Higher performance reliability.
- Local resource settings (printer, microphone, clipboard).
- Alternative keyboard settings.
- Edit settings in-session.
- Accessibility support.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Provisioning maximum timeout changed to five hours<!--36461463-->

To improve reliability, the maximum provisioning timeout has been changed to five hours.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Custom Windows 365 RBAC roles in public preview<!--36222579  -->

Custom Windows 365 role-based access control (RBAC) roles are now available in the Microsoft Intune admin center. You can mix-and-match Windows 365 permissions to create custom roles for your organization's needs. You can also create both Windows 365 and Intune custom roles and give granular admin permissions to admins for both services. For more information, see [Custom roles](role-based-access.md#custom-roles).

<!-- ########################## -->
## Week of October 11, 2021 (Service release 2109)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Resize support for preview and trial licenses<!--36228235-->

If you have a combination of paid and free trial licenses, the Resize remote action will use your paid licenses first. When those licenses run out, it will use your trial licenses. For more information, see [Resize a Cloud PC](resize-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Health check improvement<!--36461502-->

The **DNS can resolve Active Directory domain** health check has been improved. A new step has been added to look for the following Azure Active Directory DNS record. If it can’t be found, the check fails.

_ldap._tcp.yourDomain.com -type SRV

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Windows 365 Administrator role<!--5827123-->

The Windows 365 Administrator role is now available for admins by using role assignment in the Microsoft Intune admin center and Azure Active Directory (Azure AD) for Windows. With this role, admins can broadly manage Windows 365 Enterprise Cloud PCs, users, devices, and groups. This new role is in addition to the other existing roles that Windows 365 currently supports: Azure AD Global Admin, Intune Admin, and Cloud PC granular roles in Microsoft Endpoint Manager. For more information, see [Role-based access control](role-based-access.md).

<!-- ########################## -->
## Week of October 4, 2021
<!-- vvvvvvvvvvvvvvvvvvvvvv -->

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for Windows 11<!--35091970 -->

Windows 365 Enterprise now supports Windows 11 as a Cloud PC operating system.

Windows 11 Cloud PCs require Generation 2 (Gen2) virtual machines. For information about converting existing Generation 1 custom device images to Gen2, see [Convert an existing custom device image to a generation 2 virtual machine](device-images-convert-generation-2.md).

## Week of September 13, 2021
<!-- vvvvvvvvvvvvvvvvvvvvvv -->

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New PowerShell script for installing languages on custom device images<!--35726116-->

The [Windows365LanguagesInstaller PowerShell script](https://www.powershellgallery.com/packages/Windows365LanguagesInstaller) can install 38 additional languages on your custom device images. For more information, see [Provide a localized Windows experience](create-custom-image-languages.md#add-languages-to-windows-using-a-script-and-capture-the-image).

<!-- ########################## -->
## Week of September 6, 2021 (Service release 2108)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### End grace period option<!--34841603-->

Certain conditions put a Cloud PC into a seven-day grace period. At the end of this time, the Cloud PC will be deprovisioned and user will lose access.

You can now immediately end the grace period for individual Cloud PCs. By ending the grace period manually, you won’t have to wait the full seven days to remove user access from the Cloud PC.

For more information on grace periods, see [End grace period](end-grace-period.md).

<!-- ########################## -->
## Week of August 30, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Resource performance report in Endpoint Analytics<!-- 32978343 -->

Endpoint analytics has a new report named **Resource performance**. The **Resource performance report** includes metrics for CPU and RAM performance on Cloud PCs. For more information, see [Resource performance report](report-resource-performance.md).

#### Remoting connection report in Endpoint Analytics<!-- 33039368 -->

Endpoint analytics has a new report named **Remoting connection report**. This report includes the following metrics:

- **Cloud PC Sign in time (sec)** provides the total time users take to connect to the cloud PC.
- **Round Trip Time (ms)** provides insights on the speed and reliability of network connections from the user location.

For more information, see [Remoting connection report](report-remoting-connection.md).

<!-- ########################## -->
## Week of August 2, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--### Feature area alpha-->

### Windows 365 now generally available<!--10393594 -->

Windows 365 is a new service from Microsoft that automatically creates Cloud PCs for your end users. Cloud PCs are a new hybrid personal computing category that uses both the power of the cloud and the accessing device to provide a full and personalized Windows virtual machine. Admins can use Microsoft Endpoint Manager to define the configurations and applications that are provisioned for each user’s Cloud PC. End users can access their Cloud PC from any device and any location. Windows 365 stores the end user’s Cloud PC and data in the cloud, not on the device, providing a secure experience.

For more information about Windows 365, see [Windows 365](https://www.microsoft.com/windows-365?rtc=1).

<!-- ########################## -->
## Next steps

For details about Windows 365 licensing, see [Windows 365 pricing](https://www.microsoft.com/windows-365/enterprise/compare-plans-pricing).
