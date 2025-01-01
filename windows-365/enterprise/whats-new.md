---
# required metadata
title: What's new in Windows 365 Enterprise
titleSuffix:
description: Find out what's new in Windows 365 Enterprise
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/18/2024
ms.topic: conceptual
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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
> Each monthly update may roll out over several weeks and might not be immediately available to all customers.

For information about Windows App and its features, see [What's new in Windows App](/windows-app/whats-new?tabs=windows).

For more information about public preview items, see [Public preview in Windows 365](../public-preview.md).

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
## Week of December 17, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Restore, restart, and troubleshoot actions in the Cloud PCs that aren't available report<!--46873590-->

You can now use the **Bulk device actions** command on the **Cloud PCs that aren't available** report to restore, restart, and troubleshoot actions directly from the report. For more information, see [Cloud PCs that aren't available report](report-cloud-pcs-not-available.md).

<!-- ########################## -->
## Week of December 9, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Move selected Cloud PCs to a new region<!--50290712-->

You can now move selected Cloud PCs to a new region. This is instead of moving all Cloud PCs in a provisioning policy.

<!-- ########################## -->
## Week of December 2, 2024 (Service release 2411)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Intune scope tags are now generally available<!--51133268-->

Windows 365 support for [Intune scope tags](/mem/intune/fundamentals/scope-tags) has moved out of preview and into general availability. For more information, see [Scope tags](role-based-access.md#scope-tags).

#### Create and share restore points for up to 5,000 Cloud PCs<!--53500693-->

You can now bulk create restore points for up to 5,000 Cloud PCs. You can then share the restore points to a specified Azure storage account. For more information, see [Create multiple manual restore points in bulk](create-manual-restore-point.md#create-multiple-manual-restore-points-in-bulk). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Dedicated and shared data on Connected Frontline Cloud PCs report<!--54334437--> 

The Connected Frontline Cloud PCs report now shows:

- Separate data for dedicated versus shared Frontline Cloud PCs.
- The user that is currently connected and their session length
- Ability to restart Frontline Cloud PCs to disconnect user from their session and bring concurrency below threshold limits.

For more information see [Connected Frontline Cloud PCs](report-connected-frontline-cloud-pcs.md).

#### Cloud PC actions report support for moving Cloud PCs<!--53672561-->

You can use the Cloud PC actions report to see the status of moving Cloud PCs to new regions.

#### Windows 365 Government supports bulk Troubleshoot action<!--54758451-->

The Troubleshoot remote action can now be used in bulk with Windows 365 Government. For more information, see [Remotely manage Windows 365 devices](remotely-manage-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Azure network connection limit increased<!--54859923-->

The Azure network connection limit for each tenant has been increased. For more information, see [Maximum azure network connections](azure-network-connections.md#maximum-azure-network-connections).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Windows 365 now supports Israel Central<!--54918015-->

Windows 365 Enterprise now supports the Israel Central region in the Middle East geography. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ########################## -->
## Week of November 19, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Frontline

#### Windows 365 Frontline in shared mode (preview)<!--52583422-->

Windows 365 Frontline in shared mode gives you the ability to provision a collection of Cloud PCs that can be used across multiple users mapped to a Microsoft Entra ID group. One active Cloud PC is permitted per license. For more information, see [Windows 365 Frontline in shared mode](introduction-windows-365-frontline.md#windows-365-frontline-in-shared-mode-preview).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Configure client device redirection settings for Windows App on iOS/iPadOS/Android using Microsoft Intune<!--51893843-->

You can now use Microsoft Intune Mobile Application Management to check for device posture and manage redirections for Windows App on iOS, iPadOS, and Android (preview). You can use Microsoft Intune on both corporate managed and personal devices.

For more information, see [Configure client device redirection settings for Windows App and the Remote Desktop app using Microsoft Intune](/azure/virtual-desktop/client-device-redirection-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Support for FIDO devices and passkeys on macOS and iOS<!--53495787-->

Windows App and the Remote Desktop app for macOS and iOS now support FIDO devices and passkeys for Microsoft Entra ID sign in on brokered and unbrokered devices.
For more information see [Support for FIDO2 authentication with Microsoft Entra ID](/entra/identity/authentication/concept-fido2-compatibility#native-application-support).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### Use Citrix HDX Plus with Windows 365 Frontline<!--54445358-->

You can now use Citrix HDX Plus with Windows 365 Frontline Cloud PCs.

<!-- ########################## -->
## Week of October 28, 2024 (Service release 2410)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Bulk Troubleshoot action now generally available<!--51893512-->

The Troubleshoot action in bulk has moved out of preview and into general availability.

For more information, see [Remotely manage Windows 365 devices](remotely-manage-cloud-pc.md).

#### Microsoft Remote Desktop iOS client now supports Yubikey smart card redirection<!--49237449-->

The Microsoft Remote Desktop iOS client now supports smart card redirection for YubiKeys using USB-C or Lightning connector. This enables in-session smart card usage.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

### Update to Cloud PC action status report<!--49451077-->

The Cloud PC action status report now shows batches of devices on which actions were triggered. You can see the batch current progress. For more information, see [Cloud PC actions report ](report-cloud-pc-actions.md).

### Azure network connections inactive state<!--52127015-->

Azure network connections that meet either of the following conditions for more than four weeks are now marked as inactive:

- ANCs that aren't associated with provisioning policies.
- ANCs with provisioning policies that have no Cloud PCs associate with them.

#### Cloud PC connection quality report now available for Windows 365 Government<!--46738280-->

The Cloud PC connection quality report is now available for Windows 365 Government, both Government Community Cloud (GCC) and GCC-High. For more information, see [Cloud PC connection quality report](report-cloud-pc-connection-quality.md). 

<!-- ########################## -->
## Week of October 21, 2024

#### Windows 365 support for AVC mixed mode when MMR isn't enabled (preview)<!--50205898-->

AVC Mixed Mode is now available in the default graphics profile. When MMR isn't enabled, AVC/h.264 is used to encode detected image content instead of the RemoteFX image encoder. This improves performance when encoding images relative to bitrate and framerate in network-constrained scenarios.

<!-- ########################## -->
## Week of October 14, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### New Windows 365 IP subnet for RDP connectivity<!--53404845-->

Core TCP-based RDP traffic for Cloud PC connections uses the *.wvd.microsoft.com wildcard fully qualified domain name (FQDN). The FQDN remains unchanged, but the underlying IP addresses associated with it will shortly be changed to a single subnet. This will simplify optimization of this traffic and reduce the need for future change management.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Call redirection<!--53718424-->

Windows 365 now supports multimedia redirection call redirection. For more information, see [Use multimedia redirection](/azure/virtual-desktop/multimedia-redirection).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### HP Anyware for Windows 365 is now generally available<!--51133111-->

HP Anyware for Windows 365 has moved out of preview and into general availability.

For more information, see [Set up HP Anyware for Windows 365 Enterprise](hp-anyware-set-up.md)


<!-- ########################## -->
## Week of September 30, 2024 (Service release 2409)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Unavailable Cloud PCs report added to Reporting overview page<!--53687085-->

The **Cloud PCs that aren't available** report has been added to the **Reports** > **Cloud PC overview** page.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Windows 11 24H2 cloud PCs gallery images<!--53461426-->

The latest Windows Enterprise 24H2 images are available for provisioning new devices. You can update your provisioning policies to use either of the following images:

- Windows 11 Enterprise 24H2
- Windows 11 Enterprise + Microsoft 365 Apps 24H2


<!-- ########################## -->
## Week of September 23, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 11 Cloud PCs now support EN-NZ<!--54032315-->

Windows 365 Cloud PCs now support EN-NZ for Windows 11.

<!-- ########################## -->
## Week of September 16, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for symmetric NAT with RDP Shortpath<!--43602619-->

RDP Shortpath in Windows 365 now supports establishing an indirect UDP connection using Traversal Using Relays around NAT (TURN) for symmetric NAT. TURN is a popular standard for device-to-device networking for low latency, high-throughput data transmission with Azure Communication Services. For more information about TURN and Azure Communication Services, see [Network Traversal Concepts](/azure/communication-services/concepts/network-traversal). For more information about RDP Shortpath, see [Use RDP Shortpath for public networks with Windows 365](rdp-shortpath-public-networks.md).

### Windows 365 support for HEVC video coding<!--51599459-->
Windows 365 will support Hardware High Efficiency Video Coding (HEVC) h.265 4:2:0 on Compatible GPU-enabled Cloud PCs. For more information, see [Enable GPU acceleration for Azure Virtual Desktop](/azure/virtual-desktop/enable-gpu-acceleration?tabs=intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows App

#### Windows App is now generally available<!--46667283-->

Windows App has moved out of preview and into general availability.

For more information, see [What is Windows App?](/windows-app/overview)

<!-- ########################## -->
## Week of August 26, 2024 (Service release 2408)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Azure Monitor support on Windows 365 Cloud PCs<!--53421756-->

Azure Monitor Agent can now  be installed on Windows 365 Enterprise and Windows 365 Government Cloud PCs. For more information, see [Azure Monitor overview](/azure/azure-monitor/overview).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Session lock experience configuration for single sign-on<!--48440155-->

You can now configure the remote session lock experience when single sign-on is enabled between the default disconnect behavior and showing the remote lock screen. For more information, see [Configure single sign-on for Windows 365 using Microsoft Entra authentication](configure-single-sign-on.md).

#### Windows 365 support for Microsoft Purview Customer Key is now generally available<!--46980464-->

Windows 365 support for encrypting Cloud PCs by setting up Microsoft Purview Customer Key has moved out of preview and into general availability. For more information, see [Service encryption with Microsoft Purview Customer Key](/purview/customer-key-overview).

<!-- ########################## -->
## Week of August 5, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### Updated documentation article: Windows 365 service resilience<!--51365224-->

We’ve created a new article explaining Windows 365 service resilience. For more information, see [Windows 365 service resilience](resilience.md).

<!-- ########################## -->
## Week of July 29, 2024 (Service release 2407)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Uni-directional clipboard support is now generally available<!--49083399-->

Uni-directional clipboard support for Cloud PCs has moved out of preview and is now generally available. For more information, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

#### Closing port 3389 by default for newly provisioned and reprovisioned Cloud PCs<!--51154043-->

To help secure your Windows 365 environment, the inbound port 3389 is now closed by default.

#### Windows 365 support for AVC mixed mode when MMR isn't enabled (preview)<!--50205898-->

Windows 365 now supports AVC mixed mode when MMR is not enabled.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Windows 365 Government now supports Customer Lockbox<!--48802385-->

Windows 365 Government now supports Microsoft Purview Customer Lockbox.

For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New Intune report and device action for Windows enrollment attestation (public preview)<!--51490340-->

Use the new device attestation status report in Microsoft Intune to find out if a device has attested and enrolled securely while being hardware-backed. For more information, see [Device attestation status report](/mem/intune/fundamentals/reports#device-attestation-status-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### Support for Omnissa Horizon clients and the Blast protocol with Windows 365 Enterprise is now generally available<!--51899029-->

Support for Omnissa (previously VMware) Horizon clients and the Blast protocol with Windows 365 Enterprise Cloud PCs has moved out of preview and into general availability. For more information, see [Set up Omnissa Horizon for Windows 365 Enterprise](set-up-vmware-horizon.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New GPU offerings for Cloud PCs are now generally available<!--46699074-->

New GPU offerings for Window 365 Enterprise Cloud PCs have moved out of preview and into general availability. For more information, see [GPU Cloud PCs](gpu-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Frontline

#### The Windows 365 Frontline concurrency buffer is now generally available<!--50220027-->

The Windows 365 concurrency buffer has moved out of preview and into general availability.

<!-- ########################## -->
## Week of July 23, 2024

### Updated default settings for Windows 365 security baselines<!--49685126-->

Several Windows 365 Security baseline default values have changed. For a full list of all the updated settings, see [List of the settings in the Windows 365 Cloud PC security baseline in Intune](/mem/intune/protect/security-baseline-settings-windows-365).

<!-- ########################## -->
## Week of July 15, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Cloud PC support for FIDO devices and passkeys on macOS and iOS (preview)<!--51858977-->

Windows 365 Cloud PCs now support FIDO devices and passkeys for Microsoft Entra ID sign in on macOS and iOS.

<!-- ########################## -->
## Week of July 8, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

### Chroma subsampling default change to 4:2:0<!--50308895-->

To reduce monitor support issues, the Windows 365 service now defaults the chroma subsampling at 4:2:0. (instead of the previous 4:4:4). For more information, see [Change the default chroma value for Windows 365 Cloud PCs](chroma-value-change-default.md).

<!-- ########################## -->
## Week of July 1, 2024

<!-- ########################## -->
### Apps

#### Windows 365 Cloud PC gallery images use new Teams VDI<!--51726416-->

Windows 365 Cloud PC gallery images now use the new Teams Virtualized Desktop Infrastructure (VDI). For more information, see [Microsoft Teams on a Cloud PC](teams-on-cloud-pc.md) and [New VDI solution for Teams](/MicrosoftTeams/vdi-2).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Cross region disaster recovery<!--5184001500-->

Windows 365 now supports cross region disaster recovery. For more information, see [Cross region disaster recovery in Windows 365](cross-region-disaster-recovery.md).

<!-- ########################## -->
## Week of June 24, 2024 (Service release 2406)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Boot and Windows 365 Switch now support battery status redirection<!--51748880-->

Windows 365 Boot and Windows 365 Switch now support battery status redirection. Cloud PCs now show the local PC's battery status.

#### Upgrade Windows 365 licenses in Microsoft admin center<!--45415383-->

Customers that have Modern Microsoft Cloud Agreements can upgrade their existing Windows 365 licenses in the Microsoft Admin Center.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Single sign-on Windows 365 clients authentication change<!--49918010-->

Single sign-on for Windows 365 is transitioning to use the Windows Cloud Login Entra ID cloud app for Windows authentication starting with the Windows and Web clients. For more information, see [Set Conditional Access policies](set-conditional-access-policies.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Windows 365 Government now supports Cloud PC utilization report<!--49200860-->

Windows 365 Government now supports the Cloud PC utilization report. For more information,  see [Cloud PC utilization report](report-cloud-pc-utilization.md).

#### Cloud PC size recommendation report is now generally available<!--50219942-->

The Cloud PC size recommendation report has moved out of preview and is now generally available. For more information, see [Cloud PC recommendations report](report-cloud-pc-recommendations.md).

<!-- ########################## -->
## Week of June 3, 2024 (Service release 2405)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Windows 365 support for Microsoft Purview forensic evidence <!--50309017-->

Windows 365 now supports [Microsoft Purview forensic evidence](/purview/insider-risk-management-forensic-evidence). For more information, see [Set up forensic evidence](forensic-evidence-set-up.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Troubleshoot action now supports bulk<!--50276472-->

The Troubleshoot remote action can now be used in bulk. For more information, see [Remotely manage Windows 365 devices](remotely-manage-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Government Community Cloud

#### New Windows 365 Frontline offers for GCC<!--50390472-->

New Windows 365 Frontline offers are now available for Government Community Cloud (GCC) customers using the Azure Commercial cloud.

<!-- ########################## -->
## Week of May 27, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New Windows 365 Cloud PC images available in the gallery<!--48537480-->

New Cloud PC gallery images for Windows 10 and Windows 11 are now available. These improved images have harmonized optimizations with Windows 365 apps images for better policy management:

- Win 10 Enterprise Cloud PC: 21H2, 22H2,
- Win 11 Enterprise Cloud PC: 21H2, 22H2, 23H2

#### Manage redirections for Cloud PCs on Android devices<!--49090100-->

You can now  use the Intune admin center to manage redirections for Android users who access their Cloud PCs using Microsoft Remote Desktop.

#### Manage redirections for Cloud PCs on iOS/iPadOS devices<!--49090121-->

You can now use the Intune admin center to manage redirections for iOS/iPadOS users who access their Cloud PCs using Microsoft Remote Desktop and Windows App.

<!-- ########################## -->
## Week of May 20, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Cloud PC gallery images now pre-install new Microsoft Teams<!--49222964-->

Gallery images for Windows 365 Cloud PCs now come with the new Microsoft Teams pre-installed (not Teams (Classic)). This applies to Windows Enterprise 11 23H2 and 22H2. For more information, see [Gallery images](device-images.md#gallery-images).

<!-- ########################## -->
## Week of May 6, 2024 (Service release 2404)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### FQDNs removed from requirement list<!--48907341-->

Many required FQDNs were previously moved to the *.infra.windows365.microsoft.com wildcard FQDN. The old FQDNs are now being removed. For an updated list of FQDNs, see [Network requirements](requirements-network.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Cloud PCs that aren't available report is now generally available<!--46738272-->

The **Cloud PCs that aren't available report** has moved out of preview and into general availability. For more information, see [Cloud PCs that aren't available report](report-cloud-pcs-not-available.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Intune scope tags (preview)<!--48907552-->

Windows 365 now supports [Intune scope tags](/mem/intune/fundamentals/scope-tags). For more information, see [Scope tags](role-based-access.md#scope-tags).

<!-- ########################## -->
## Week of April 10, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### Use HP Anyware for Windows 365 Enterprise (preview)<!--48782170-->

You can now use HP Anyware for Windows 365 Enterprise Cloud PCs. For more information, see [Set up HP Anyware for Windows 365 Enterprise](hp-anyware-set-up.md).

<!-- ########################## -->
## Week of April 1, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Step-up licenses now support storage<!--48555915-->

For Windows 365, step-up licenses now support storage. For more information, see [Resize with Step-up Licenses](resize-cloud-pc.md#resize-with-step-up-licenses).

<!-- ########################## -->
## Week of March 26, 2024 (Service release 2403)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Concurrency buffer for Windows 365 Frontline Cloud PCs<!--48929001-->

A new concurrency buffer lets you exceed the max concurrency count for a limited time under certain circumstances, like during shift changes. For more information, see [Exceeding the maximum concurrency limit](introduction-windows-365-frontline.md#exceeding-the-maximum-concurrency-limit).

#### Maintenance windows (public preview)<!--48851694-->

You can now set maintenance windows for running remote actions on Cloud PCs. This will notify users in-session about the impending remote action period. For more information, see [Cloud PC maintenance windows](cloud-pc-maintenance-windows.md).

#### Bulk remote action support<!--49086004-->

You can now use bulk actions with the following remote actions: Restore, Restart, Resize, and Reprovision. For more information, see [Remotely manage Windows 365 devices](remotely-manage-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Microsoft Purview Data Loss Prevention support for Windows 365 Enterprise<!--49070474-->

Microsoft Purview Data Loss Prevention (DLP) now supports Windows 365 Enterprise. For more information, see [Endpoint DLP support for virtualized environments](/purview/endpoint-dlp-getting-started#endpoint-dlp-support-for-virtualized-environments).

#### Windows 365 Boot shared mode supports FIDO<!--49080360-->

Windows 365 Boot shared mode now supports FIDO. For more information, see [How-to: Password-less FIDO2 Security Key Sign-in to Windows 10 HAADJ Devices](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/how-to-password-less-fido2-security-key-sign-in-to-windows-10/ba-p/1434583).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### Updated documentation article: Known issues<!--49423094-->

We’ve updated the article [Known issues: Windows 365 Enterprise and Frontline](known-issues-enterprise.md#teams-isnt-enforcing-screen-capture-protection), add a known issue for Teams isn't enforcing screen capture.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### Microsoft Graph APIs support for Windows 365 v1.0 workloads<!--47055302-->

In addition to Beta workloads, the Microsoft Graph APIs now support Windows 365 as v1.0 workloads. For more information, see [Use Microsoft Entra ID to access the Windows 365 APIs in Microsoft Graph](permission-scopes.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Cloud PC utilization report creation date<!--49175145-->

The Cloud PC utilization report now shows the Cloud PC creation date. For more information, see [Cloud PC utilization report](report-cloud-pc-utilization.md).

#### Cloud PC size recommendation report (public preview)<!--45433311-->

A new Intune admin center report recommends appropriate sizes for Cloud PCs to better fit your organization's needs. For more information, see [Cloud PC recommendations report](report-cloud-pc-recommendations.md).

#### Improvements to Cloud PC connection quality report are now generally available<!--46738280-->

Improvements to the Cloud PC connection quality report have moved out of preview and into general availability. These improvements include:

- a more comprehensive view of the overall performance of their Cloud PCs.
- a more detailed view of devices when they are in a state of poor performance due to high round trip times.
- Tenant level visibility to most recent/current for:
  - Round Trip Time.
  - Bandwidth.
  - Connection Time.
  - UDP Utilization.
- Connection specific detail on client IP and associated CPC Gateway.
- Filters for all columns.

For more information, see [Cloud PC connection quality report](report-cloud-pc-connection-quality.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Frontline

#### Windows 365 Frontline support for power on/off in bulk<!--49473730-->

You can now use bulk actions to turn on/off Windows 365 Frontline Cloud PCs.

<!-- ########################## -->
## Week of March 11, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### Updated documentation article: Forced browser sign-in setting for Cloud PC gallery images<!--49401955-->

We’ve updated the article [Device images overview](device-images.md#gallery-images), noting that gallery images have [forced browser sign-in](/deployedge/microsoft-edge-policies#browsersignin) pre-applied.

<!-- ########################## -->
## Week of March 4, 2024 (Service release 2402)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Alerts for Windows 365 Frontline maximum concurrent Cloud PCs<!--45903013-->

A new alert notifies admins when the maximum concurrent Cloud PCs are active for Windows 365 Frontline subscriptions.

#### Cloud PC utilization report now generally available<!-- 46738247-->

The **Cloud PC utilization** report has moved out of preview and into general availability. For more information, see [Cloud PC utilization report](report-cloud-pc-utilization.md).

#### Device action data kept for 90 days<!--48439987-->

On the **Overview** page for individual Cloud PCs, the **Actions** will show actions performed within the last 90 days.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Switch

#### Windows 365 Switch support for Windows 365 Frontline<!--46816178-->

Windows 365 Switch now supports Windows 365 Frontline Cloud PCs. For more information, see [Windows 365 Switch](windows-365-switch-overview.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Offline Windows 365 Frontline Cloud PCs update sync<!--48663450-->

Windows 365 Frontline Cloud PCs that haven’t been used for seven days are now automatically turned on and synced with Windows Update client policies.

#### Admins can remotely power on and off Windows 365 Frontline Cloud PCs<!--48801654-->

Admins can now power on and off Windows 365 Frontline Cloud PCs using remote actions. For more information, see [Remotely manage Windows 365 devices](remotely-manage-cloud-pc.md).

#### Uni-directional clipboard support (preview)<!--48897413-->

You can now configure uni-directional clipboard for Cloud PCs that have Windows Insider Build 25898 or later. For more information, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Customer Lockbox support is now generally available<!--47499839-->

Windows 365 Enterprise and Frontline support for Microsoft Purview Customer Lockbox has moved out of preview and is now generally available.

For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

<!-- ########################## -->
## Week of February 26, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### New faster sign-in frequency option (preview)<!--48439987-->

When single sign-on is enabled, selecting the **Conditional Access** > **Session** > **Sign-in frequency** > **Every time** option provides a faster reauthentication period of 5-10 minutes depending on the client used. For more information, see [Set Conditional Access policies](set-conditional-access-policies.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Boot

#### Shared and dedicated Windows 365 Boot device modes are now generally available<!--48742628-->

Windows 365 Boot shared and dedicated device modes have moved out of preview and into general availability.

For more information, see [What is Windows 365 Boot?](windows-365-boot-overview.md) and [Guided scenario - deploy Windows 365 Boot to shared physical devices](windows-365-boot-guide.md).

#### Windows 365 Boot sign-in page customization is now generally available<!--48742587-->

Windows 365 Boot support for sign-in page customization has moved out of preview and into general availability. For more information, see [Guided scenario - deploy Windows 365 Boot to shared physical devices](windows-365-boot-guide.md).

#### Windows 365 Boot fail fast notifications are now generally available<!--48742676-->

Windows 365 Boot detection and notification of network or application setup issues has moved out of preview and into general availability.

#### Manage local PC settings through Windows 365 Boot is now generally available<!--48742743-->

User management of local PC settings through their Windows 365 Boot Cloud PC has moved out of preview and into general availability.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Switch

#### Windows 365 Switch desktop identifiers are now generally available<!--48064527-->

Windows Task view identifiers for Cloud PC or local PC have moved out of preview and into general availability.

#### Windows 365 Switch improved disconnecting is now generally available<!--48743248-->

The ability for users to seamlessly disconnect from their Cloud PC without leaving their local desktop has moved out of preview and into general availability. For more information, see [Windows 365 Switch](https://support.microsoft.com/en-us/windows/windows-365-switch-4ea65cc3-05ff-4166-ac8b-389af27108f8).

#### Windows 365 Switch connection status now generally available<!--48743180-->

Connection status and timeout information on the connection screen for Windows 365 Switch with Windows 365 Frontline Cloud PCs has moved out of preview and into general availability.

<!-- ########################## -->
## Week of January 29, 2024 (Service release 2401)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### FQDN requirement changes<!--46731885-->

Many required FQDNs have been moved to the *.infra.windows365.microsoft.com wildcard FQDN. This move reduces the initial configuration requirements and the change rate of connectivity requirements. For Windows 365 Government, the FQDNs were moved to *.infra.windows365.microsoft.us. To avoid any issues when provisioning new Cloud PCs, you must make sure that *.infra.windows365.microsoft.com (*.infra.windows365.microsoft.us for Windows 365 Government) is an accessible endpoint in your network allow list.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### End users can restart their Windows Cloud PC using the keyboard<!--48453601-->

For newly created Cloud PCs, end users can now restart or shut down their Cloud PC by using the keyboard combination CTL+ALT+DEL. This doesn't apply to Cloud PCs created before 1/31/2024.

<!-- ########################## -->
## Week of January 15, 2024

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### Updated documentation article: Relative performance for different Cloud PC sizes<!--48521010-->

We’ve updated the article and added performance information for additional Cloud PC sizes. For more information, see [Relative performance for different Cloud PC sizes](../relative-cloud-pc-performance.md).

<!-- ########################## -->
## Week of January 8, 2024 (Service release 2312)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New alert rule: Cloud PCs that aren't available (preview)<!--47321010-->

A new alert rule is now available to notify you when Cloud PCs aren't available. For more information about alerts in general, see [Alerts in Windows 365](alerts.md).  For more information about the report, see [Cloud PCs that aren't available report](report-cloud-pcs-not-available.md). This feature is not yet available for Windows 365 Frontline.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Windows 365 now supports Italy North and Poland Central<!--41741396-->

Windows 365 Enterprise and Windows 365 Frontline Cloud PC now support the Italy North and Poland Central regions. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Boot

#### Manage local PC settings through Windows 365 Boot (preview)<!--48416631-->

Users can now access and manage local PC settings more easily from their Windows 365 Boot Cloud PC. These include sound, display, and other device specific settings of their local PC. Settings can be found by going to Start > **Settings** in the Cloud PC.

#### Windows 365 Boot sign-in page customization (preview)<!--48416441-->

Windows 365 Boot now supports customizing the Cloud PC sign-in page with company logo branding for Cloud PCs in shared PC mode. For more information, see [Guided scenario - deploy Windows 365 Boot to shared physical devices](windows-365-boot-guide.md).

#### Windows 365 Boot device modes - shared and dedicated (preview)<!--48065006-->

Windows 365 Boot now supports two modes of signing in to a Cloud PC from a physical device:

- Shared PC mode: Multiple users can use the same physical device to sign in to their own Cloud PCs through the Windows 11 sign-in screen.
- (New) Dedicated PC mode: The physical device is assigned to a specific user to sign in to their Cloud PC through the Windows 11 sign-in screen.

For more information, see [What is Windows 365 Boot?](windows-365-boot-overview.md) and [Guided scenario - deploy Windows 365 Boot to shared physical devices](windows-365-boot-guide.md).

#### Windows 365 Boot fail fast notifications (preview)<!--48416583-->

To speed up the sign-in process, Windows 365 Boot now detects network or application setup issues and notifies the users about them immediately during the sign-in process.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Switch

#### Windows 365 Switch improved disconnecting (preview)<!--48064527-->

Users can now seamlessly disconnect from their Cloud PC without leaving their local desktop. For more information, see [Windows 365 Switch](https://support.microsoft.com/en-us/windows/windows-365-switch-4ea65cc3-05ff-4166-ac8b-389af27108f8).

#### Windows 365 Switch desktop identifiers (preview)<!--48064527-->

When switching between desktops using Task view, each desktop is identified as a Cloud PC or Local PC.

#### Windows 365 Switch connection status (preview)<!--48064527-->

When using Windows 365 Switch with Windows 365 Frontline Cloud PCs, users now see connection status and timeout information on the connection screen. In case of an error, users can copy the correlation ID to help with resolving the issue.

<!-- ########################## -->
## Week of December 10, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Windows 365 support for Microsoft Purview Customer Key (preview)<!--46980464-->

Windows 365 now supports encrypting Cloud PCs by setting up Microsoft Purview Customer Key. For more information, see [Service encryption with Microsoft Purview Customer Key]( /purview/customer-key-overview).


<!-- ########################## -->
## Week of December 04, 2023 (Service release 2311)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Boot is now available for Windows 365 Government<!--46030732-->

Windows 365 Boot is now available for US Government Community Cloud (GCC) customers using Windows 365 Government. For more information, see [What is Windows 365 Boot?](windows-365-boot-overview.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### UI change in web client<!--46838016-->

The gear icon menu has been updated. For details on the new menu, see [Windows 365 web client](end-user-access-cloud-pc.md#windows-365-web-client).

#### New Microsoft Teams app is now generally available for Windows 365<!--47459639-->

The new Microsoft Teams app has moved out of preview and into general availability. It's been optimized for faster performance and more efficient resource use on Cloud PCs. For more information, see [Upgrade to new Teams for Virtualized Desktop Infrastructure]( /microsoftteams/new-teams-vdi-requirements-deploy).

The new Microsoft Teams app is not yet available in the Windows 365 gallery images.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New report: Action status (preview)<!--44871923-->

A new report is now available that lets you know which actions have been performed successfully on Cloud PCs. For failed actions, possible reasons will also be provided. For more information, see [Cloud PC actions report](report-cloud-pc-actions.md).

#### New filter option for the Connected Frontline Cloud PCs report<!--47323230-->

A new filter is available in the Connected Frontline Cloud PCs report. This new filter shows hourly data for various data periods. For more information, see [Connected Frontline Cloud PCs report (preview)](report-connected-frontline-cloud-pcs.md). 

<!-- ########################## -->
## Week of November 13, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Screen capture protection in Windows 365 settings catalog<!--46981580-->

You can now implement screen capture protection for your Cloud PCs by using the settings catalog. Alongside watermarking, screen capture is a deterrent to data leaks and data loss. For more information, see [Enable screen capture protection in Azure Virtual Desktop](/azure/virtual-desktop/screen-capture-protection) and [Configure the administrative template](/azure/virtual-desktop/administrative-template?tabs=intune#configure-the-administrative-template).

This feature isn’t supported on Android, iOS, or web clients. Enabling this feature blocks users from accessing their Cloud PCs when using these clients.

#### Watermarking support in Windows 365 settings catalog<!--45779621-->

You can now implement watermarking for your Cloud PCs by using the settings catalog. Alongside screen capture, watermarking is a deterrent to data leaks and data loss. For more information, see [Watermarking in Azure Virtual Desktop](/azure/virtual-desktop/watermarking) and [Configure the administrative template](/azure/virtual-desktop/administrative-template?tabs=intune#configure-the-administrative-template).

#### Customer Lockbox support (preview)<!--46807263-->

Windows 365 Enterprise and Frontline now support Microsoft Purview Customer Lockbox.

For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Single sign-on is now generally available<!--43836114-->

The following single sign-on updates have moved out of preview and are now generally available:

- Single sign-on for Microsoft Entra joined and Microsoft Entra hybrid joined Cloud PCs.
- You can turn on single sign-on separately for each provisioning policy to apply it to new Cloud PCs.
- You can apply single sign-on to existing Cloud PCs.
- A new Azure Network Connection check for Microsoft Entra hybrid joined provisioning policies to make sure that the domain is properly configured for single sign-on.

These updates are also available for Windows 365 Frontline.

#### New GPU offerings for Cloud PCs (preview)<!--46699074-->

Three new GPU offerings are now available for Window 365 Enterprise Cloud PCs. For more information, see [GPU Cloud PCs](gpu-cloud-pc.md)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows App now available in public preview<!--46667283-->

Windows App lets users securely connect to Windows devices and apps. Supported remote devices include:

- Azure Virtual Desktop
- Windows 365 Cloud PC
- Microsoft Dev Box
- Remote Desktop Services
- Remote PC

Windows App is available for Windows, macOS, iOS and iPadOS, and web browsers.

For more information, see [What is Windows App?](/windows-app/overview)

<!-- ########################## -->
## Week of October 30, 2023 (Service release 2310)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Permissions update for placing a Cloud PC under review<!--46608968-->

You now need an additional role, Storage Blob Data Contributor, to place a Cloud PC under review. For more information, see [Place a Windows 365 Enterprise Cloud PC under review](place-cloud-pc-under-review.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Two new sizes for Cloud PCs<!--46653331-->

Two new sizes are now available for Windows 365 Cloud PCs:

- 16vCPU/64GB RAM/512GB storage​
- 16vCPU/64GB RAM/1TB storage

These 16 vCPU licenses can be purchased and assigned in the same way that you purchase and assign other Windows 365 licenses.

#### New gallery images<!--47114436-->

Two new gallery images are now available for Windows 365 Cloud PCs:

- Windows 11 Preview + Microsoft 365 Apps 23H2
- Windows 11 Preview + OS Optimizations 23H2

You can choose the new gallery images when [creating a provisioning policy](create-provisioning-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### New Graph API for Windows 365 Frontline<!--46770829-->

A new graph API is now available for Windows 365 Frontline.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Audit logs supported in Azure Log Analytics<!--45693398-->

You can now send Windows 365 audit log data directly to Azure Log Analytics, Event Hub, or certain third-party solutions. For more information, see [Send Windows 365 audit logs to diagnostic settings in Azure Monitor](get-cloud-pc-audit-logs-using-powershell.md#send-windows-365-audit-logs-to-diagnostic-settings-in-azure-monitor).


<!-- ########################## -->
## Week of September 25, 2023 (Service release 2309)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### The resize action is now generally available<!--43950142-->

The resize action has moved out of preview and into general availability. This feature is also available for both Windows 365 Government and Windows 365 Government customers using Windows 365 Enterprise. The resize action isn't currently available for Windows 365 Frontline. For more information, see [Resize a Cloud PC](resize-cloud-pc.md).

#### Windows 365 Boot is now generally available<!--43305609-->

Windows 365 Boot has moved out of preview and into general availability. For more information, see [What is Windows 365 Boot?](windows-365-boot-overview.md) This feature isn't currently available for Windows 365 Government.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New filter options in the Cloud PC utilization report<!-- 43968518-->

Two new filter options are now available for the **Cloud PC utilization** report:

- **Date last connected** filter option: **No connection within the last 60 days**
- **Time connected** filter option: **None (0 hours)**

For more information, see [Cloud PC utilization report](report-cloud-pc-utilization.md).

#### New report: Cloud PCs that can't connect <!--45946128-->

A new report is now available that provides metrics that help admins evaluate tenant level device connection status and reliability.  For example, you can observe:

- devices that have unhealthy hosts.
- users' connections that consistently or frequently fail.
- systemic issues, like an Azure infrastructure issue, that is impacting the ability of a user to connect.

For more information, see [Cloud PCs that aren't available report](report-cloud-pcs-not-available.md).

#### Improvements to Cloud PC connection quality report<!--45946378-->

Improvements to the Cloud PC connection quality report include:

- A more comprehensive view of the overall performance of their Cloud PCs.
- A more detailed view of devices when they are in a state of poor performance due to high round trip times.
- Tenant level visibility to most recent/current for:
    - Round Trip Time.
    - Bandwidth.
    - Connection Time.
    - UDP Utilization.
- Connection specific detail on client IP and associated CPC Gateway.
- Filters for all columns.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Single sign-on updates<!--43751308-->

The following updates related to single sign-on are now available:

- [Public preview features](..\public-preview.md).
  - Single sign-on for Microsoft Entra hybrid join Cloud PCs.
  - You can turn on single sign-on separately for each provisioning policy.
  - A new Azure Network Connection check to make sure that the network is properly configured for single sign-on.
  - Apply single sign-on to existing Microsoft Entra joined and Microsoft Entra hybrid joined Cloud PCs.

For more information, see [Create provisioning policy](create-provisioning-policy.md) and [Edit provisioning policy](edit-provisioning-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows 365 Switch is now generally available<!--45933920-->

Windows 365 Switch has moved out of preview and into general availability. For more information, see [Windows 365 Switch](windows-365-switch-overview.md). This feature isn't currently available for Windows 365 Government.

<!-- ########################## -->
## Week of September 18, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### Windows 365 help documentation updated for Microsoft Entra ID<!--465015050-->

Windows 365 help documentation has been updated for the rebranding of Azure Active Directory to Microsoft Entra ID. For more information, see [New name for Azure Active Directory](/azure/active-directory/fundamentals/new-name). Some areas of the Microsoft Intune user interface haven't yet been updated to Microsoft Entra ID, so you might see  differences until those updates are made.

<!-- ########################## -->
## Week of August 28, 2023 (Service release 2308)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### System alerts and email notifications are now generally available<!--40932899 -->

System alerts and email notifications have moved out of preview and into general availability. For more information, see [Alerts](alerts.md).

#### New report: Connected Frontline Cloud PCs<!--45975938-->

The Connected Frontline Cloud PCs report is now available. For more information, see [Connected Frontline Cloud PCs report](report-connected-frontline-cloud-pcs.md).

#### Endpoint Analytics resource performance report now available to GCCH customers<!--45234123-->

The Endpoint Analytics resource performance report is now available to Government Community Cloud High (GCCH) customers. For more information, see [Resource performance report](report-resource-performance.md).

#### New Cloud PC overview report page<!--45976156-->

All Cloud PC reports can now be accessed from the **Cloud PC overview** section under **Device management**.

<!-- ########################## -->
## Week of August 21, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Partners

#### Use VMWare Horizon clients and the Blast protocol with Windows 365 Enterprise (public preview)<!--44716096-->

VMWare Horizon clients and the Blast protocol can be used with Windows 365 Enterprise Cloud PCs. This is a [public preview](..\public-preview.md). For more information, see [Set up VMware Horizon for Windows 365 Enterprise](set-up-vmware-horizon.md).

<!-- ########################## -->
## Week of August 7, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows 11 Task view support for Cloud PCs (preview)<!--44976396-->

Windows 365 Switch lets users connect to their Cloud PC by using the Windows 11 Task view. They can also use Task view to switch between their Cloud PC and their local device. For more information, see [Windows 365 Switch](windows-365-switch-overview.md)  and the [Windows 365 Switch end user help article](https://support.microsoft.com/windows/windows-365-switch-4ea65cc3-05ff-4166-ac8b-389af27108f8).

#### LG webOS 23 support on windows365.microsoft.com<!--45794301-->

The Windows 365 web site, windows365.microsoft.com, now supports LG webOS 23.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Security

#### Tamper protection support for Windows 365<!--45780208-->

Windows 365 now supports use of endpoint security Antivirus policy to manage Tamper protection for Windows 365 Cloud PCs. Support for Tamper protection requires devices to onboard to Microsoft Defender for Endpoint before the policy that enables Tamper protection is applied.

<!-- ########################## -->
## Week of July 31, 2023 (Service release 2307)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Move Cloud PC is now generally available<!--43667415-->

Move Cloud PC has moved out of preview and into general availability. For more information, see [Move Cloud PC](move-cloud-pc.md).

#### New setting to allow users to reprovision their own Cloud PC<!--45034196-->

You can now grant users permission to reset (reprovision) their own Cloud PC. For more information, see [Make a user a local admin](assign-users-as-local-admin.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Azure network connection (ANC) least privilege update<!--44876259-->

A new, more secure least privilege is now available. You must manually remove the old network contributor role from the resources where the ANC was created. For more information, see [Role-based access control](role-based-access.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### Provide feedback button for admins is now generally available<!--44506030-->

The **Provide feedback** button has moved out of preview and into general availability.

<!-- ########################## -->
## Week of July 17, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows 365 web client camera support (preview)<!--45017167-->

Users can now give their Cloud PC access to their local device's camera.

<!-- ########################## -->
## Week of July 3, 2023 (Service release 2306)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Frontline is now generally available<!--43582253 -->

Windows 365 Frontline has moved out of preview and into general availability. For more information, see [What is Windows 365 Frontline?](introduction-windows-365-frontline.md)

#### Group-based license support for Cloud PC resizing<!--41357690-->

Both single and bulk resizing now support Cloud PCs that were provisioned with group-based licenses.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows365.microsoft.com Open in browser button includes Windows 365 app and Open in Remote Desktop app<!--44467575-->

Users now have two options when they select the **Open in browser** drop-down button to open a Cloud PC user session from the windows365.microsoft.com page:

- **Open in Windows 365 app**
- **Open in Remote Desktop app**

#### Windows 365 app update notifications for users<!--45206957-->

Windows 365 app users will get a notification when an update is available. If users choose to update, the app closes and they'll get a Windows notification when the update is complete.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Resource performance report in Endpoint Analytics now available for Windows 365 Government<!--45052030-->

The resource performance report in Endpoint Analytics is now available for Windows 365 Government. For more information, see [Resource performance report](report-resource-performance.md).

#### Correlation IDs for Azure network connection notifications<!--45066996-->

The Azure network connection health check status in Microsoft Intune now includes a correlation ID. This ID helps the support team troubleshoot customer issues. Make sure to provide the ID number when you contact Microsoft support.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 app support for Windows 365 Government environments<!--43305226-->

The Windows 365 app now supports Windows 365 Government environments.

#### Windows 365 app pin Cloud PC to task bar now supports Windows 365 Government<!--43983776-->

Windows 365 Government users can now pin their Cloud PC to the task bar in the Windows 365 app for Windows 11 platforms.

<!-- ########################## -->
## Week of June 12, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Apps

#### Windows 365 Government support for virtualization-based workloads<!--45086869-->

Virtualization-based workloads are now supported in Windows 365 Government environments. For more information, see [Set up virtualization-based workloads on your Cloud PC](nested-virtualization.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: High-level architecture diagram<!--45049183-->

We’ve published a new help documentation article. For more information, see [High-level architecture diagram](high-level-architecture.md).

<!-- ########################## -->
## Week of June 5, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### Microsoft 365 admin center: Windows 365 cloud PC advanced deployment guide<!--44563663-->

The Advanced deployment guides page in the Microsoft 365 admin center has a new guide to help admins plan for, deploy, and scale Windows 365 Enterprise in their organization. This guide has a checklist of Cloud PC configuration tasks and includes best practices, tools, and recommendations based on the tenant's configuration.

#### Windows 365 Enterprise can now be purchased by government customers <!--44276738-->

Windows 365 Enterprise can now be purchased by customers with an existing Government Community Cloud (GCC) tenant. Such customers can use their Azure Commercial subscription if they want to use custom images and Azure network connections. (Previously, customers with a GCC tenant could only buy Windows 365 Government. An Azure Government subscription was required for custom images and Azure network connections.) Windows 365 Enterprise is a commercial product with commercial licensing terms and conditions.

Windows 365 Enterprise is FedRAMP compliant. Except for FedRAMP, Windows 365 Enterprise doesn't offer the same compliance as Windows 365 Government. CJIS and IRS 1075 aren't supported in Windows 365 Enterprise.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 Government setup tool<!--43461105-->

A new Windows 365 Government setup tool is now available. It replaces the PowerShell scripts that were used to set up tenant mapping and permissions. For more information, see [Set up tenants for Windows 365 Government](set-up-tenants-windows-365-gcc.md).

<!-- ########################## -->
## Week of May 29, 2023 (Service release 2305)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Cloud PC on-demand restore points and copy to Azure Storage account are now generally available<!--43450254-->

Cloud PC on-demand restore points and copy to  an Azure Storage account have moved out of preview and into general availability. For more information, see [Create on-demand manual restore points for Cloud PCs](create-manual-restore-point.md) and [Share Cloud PC restore points to an Azure Storage Account](share-restore-points-storage.md).

#### Shortpath for managed/private networks<!--44356711-->

Managed network RDP Shortpath is available for Windows 365. For more information about RDP Shortpath in Windows 365, see [Use RDP Shortpath for private networks with Windows 365 ](rdp-shortpath-private-networks.md).

#### Move Cloud PC<!--43450234-->

A new provisioning policy option lets you define a new region or ANC for the provisioning policy. When you initiate the move:

1. All Cloud PCs in the provisioning policy that no longer match the updated region or ANC will be shut down.
2. All such Cloud PCs will be moved to the new region or ANC.

It may take several hours for the moves to complete.

New Cloud PCs created by the provisioning policy will be created in the new region or ANC.

For more information, see [Move Cloud PC](move-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### Provide feedback button for admins (preview)<!--43853267-->

A **Provide feedback** button is now available in several Windows 365 admin pages in the Intune admin center.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Admin alert when a Cloud PC enters the grace period<!--44188012-->

Admins are now alerted when a Cloud PC enters the grace period. For more information about grace periods, see [Device management overview for Cloud PCs](device-management-overview.md). For information about how to view and customize alerts, see [Alerts in Windows 365](alerts.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 app

#### Windows 365 app supports dark mode<!--44828612-->

The Windows 365 app now supports dark mode. End users have the option to set the Windows 365 app to light or dark mode, or to match system settings.

#### Windows 365 app settings support for multiple monitors<!--44775534-->

Users can now change multiple monitor setting in the Windows 365 app.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 Government Azure Network Connection set up improvement<!--44237227-->

During Azure network connection (ANC) creation or editing, instead of copying and pasting details (like Subscription ID, and VNET name) for the ANC, you can now select options from a drop-down menu. For more information, see [Set up tenants for Windows 365 Government](set-up-tenants-windows-365-gcc.md).

<!-- ########################## -->
## Week of May 22, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Boot: users can sign in directly to their Cloud PC from their physical device (preview)<!--42936537-->

Windows 365 Boot lets admins configure Windows 11 physical devices so that users can:

- Avoid signing in to their physical device.
- Sign in directly to their Windows 365 Cloud PC on their physical device.

For more information, see [What is Windows 365 Boot?](windows-365-boot-overview.md)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Using Intune, install the Windows 365 app on physical devices

We’ve published a new help documentation article. For more information, see [Using Intune, install the Windows 365 app on physical devices](install-windows-365-app-intune.md).

<!-- ########################## -->
## Week of April 24, 2023 (Service release 2304)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Windows 365 web client keyboard shortcut redirection<!--43951825-->

Windows 365 web client users can now use keyboard shortcuts (like Alt + Tab) on their Cloud PC. These shortcuts would normally be intercepted by the host operating system and not sent to the Cloud PC. For more information about these keyboard shortcuts, see [Access a Cloud PC](../end-user-access-cloud-pc.md).

#### Windows 365 app: pin Cloud PC to task bar<!--43470782-->

End users can now pin their Cloud PC to the task bar in the Windows 365 app. This lets them launch the Cloud PC from the task bar icon without going into the connection center.

#### Windows365.microsoft.com dark mode<!--44269253-->

You now have the option to use dark mode on windows365.microsoft.com. For more information, see [Access a Cloud PC](../end-user-access-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Windows 365 now supports South Africa North and Sweden Central<!--44267264-->

Windows 365 Cloud PC now supports the South Africa North and Sweden Central regions. For more information, see [Supported Azure regions for Cloud PC provisioning](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 Government with custom images or Azure network connections<!--43667715-->

For Windows 365 Government customers, the **Custom images** and **Azure network connection**  pages have been updated to make it clear that:

- Before using custom images with Windows 365 Government, you must link your Azure Commercial tenant with your Azure Government tenant.
- Before using Azure network connections with Windows 365 Government, you must link your Azure Commercial tenant with your Azure Government tenant.

<!-- ########################## -->
## Week of April 10, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### End user experience

#### Location redirection<!--43953213-->

Users can now turn on Location redirection so that their Cloud PCs use their correct geographic location. For more information, see [Location redirection](../end-user-access-cloud-pc.md#location-preview).

<!-- ########################## -->
## Week of April 3, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Windows 365 Frontline<!-- 43452892-->

Windows 365 Frontline is a new version of Windows 365 that helps organizations save costs by providing a single license to provision three Cloud PC virtual machines. For each Windows 365 Frontline license that you buy, you can provision three different Cloud PCs that can’t be used concurrently. Instead, each user receives a unique Cloud PC that they can use when the other two users on the same license aren’t signed into their Cloud PCs. For more information, see [What is Windows 365 Frontline?](introduction-windows-365-frontline.md)

#### Convert Windows 365 licenses to higher level licenses<!--43204652-->

Customers with an active direct enterprise agreement can now convert lower-level Windows 365 licenses to higher-level licenses. Reach out to your field specialist to learn more.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Relative performance for different Cloud PC sizes

We’ve published a new help documentation article. For more information, see [Relative performance for different Cloud PC sizes](../relative-cloud-pc-performance.md).

<!-- ########################## -->
## Week of March 28, 2023 (Service release 2303)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Cloud PC custom name template<!--42947813-->

You can now create a template to automatically create unique names for new Cloud PCs. For more information, see [Create provisioning policies](create-provisioning-policy.md#continue-creating-a-provisioning-policy).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### FQDN tags <!--43488376-->

FQDN tags help customers simplify the creation and maintenance of the necessary rules for outbound network traffic through Azure firewalls. For more information, see [Use Azure Firewall to manage and secure Windows 365 environments](azure-firewall-windows-365.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Miscellaneous

#### Windows 365 and FedRAMP

Windows 365 Enterprise has been assessed by a FedRAMP authorized auditor to meet FedRAMP requirements at data centers within the Continental US.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--### Windows 365 app-->

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Windows 365 Government

#### Windows 365 Gov support for transferring files from your Cloud PC by using windows365.microsoft.com web client<!--43758020-->

You can use the windows365.microsoft.com web client to transfer files to and from your Windows 365 Gov Cloud PC. For more information, see [Transfer files to and from a Cloud PC](../end-user-access-cloud-pc.md#transfer-files-to-and-from-a-cloud-pc).

#### Higher Cloud PC screen resolution option for Windows 365 Gov<!--43758020-->

Windows 365 Gov Cloud PC users can now choose a higher screen resolution when they connect to their Cloud PC from [https://windows365.microsoft.com](https://windows365.microsoft.com).


<!-- ########################## -->
## Week of March 6, 2023

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Create on-demand Cloud PC restore points and copy them to an Azure Storage account<!--43450254-->

You can now create on-demand Cloud PC restore points and copy them to an Azure Storage account. For more information, see [Create on-demand manual restore points for Cloud PCs](create-manual-restore-point.md) and [Share Cloud PC restore points to an Azure Storage Account](share-restore-points-storage.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Permission changes for Azure network connection operations<!--43251193-->

The permissions required for the editing, creating, and deleting Azure network connection (ANC) and health check retry operations have changed: You must now have [Intune Administrator](/azure/active-directory/roles/permissions-reference#intune-administrator) or [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference) permissions. For more information, see [Azure network connections](azure-network-connections.md).

<!-- ########################## -->
## Week of February 27, 2023 (Service release 2302)

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

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Azure network connection domain credential life cycle

We’ve published a new help documentation article. For more information, see [Azure network connection domain credential life cycle](azure-network-connection-domain-credential.md).

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

- You can select a specific region to make sure that your Cloud PCs are only provisioned in that region.
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

Customers using Azure Active Directory (Azure AD) Join without bringing an Azure virtual network can now upload custom images directly on the image tab in Microsoft Intune. Previously, to upload an image, customers needed to create an ANC for the destination Azure subscription that provides the image.

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

The Windows 365 Administrator role is now available for admins by using role assignment in the Microsoft Intune admin center and Azure Active Directory (Azure AD) for Windows. With this role, admins can broadly manage Windows 365 Enterprise Cloud PCs, users, devices, and groups. This new role is in addition to the other existing roles that Windows 365 currently supports: Azure AD Global Admin, Intune Admin, and Cloud PC granular roles in Microsoft Intune. For more information, see [Role-based access control](role-based-access.md).

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

Windows 365 is a new service from Microsoft that automatically creates Cloud PCs for your end users. Cloud PCs are a new hybrid personal computing category that uses both the power of the cloud and the accessing device to provide a full and personalized Windows virtual machine. Admins can use Microsoft Intune to define the configurations and applications that are provisioned for each user’s Cloud PC. End users can access their Cloud PC from any device and any location. Windows 365 stores the end user’s Cloud PC and data in the cloud, not on the device, providing a secure experience.

For more information about Windows 365, see [Windows 365](https://www.microsoft.com/windows-365?rtc=1).

<!-- ########################## -->
## Next steps

For details about Windows 365 licensing, see [Windows 365 pricing](https://www.microsoft.com/windows-365/enterprise/compare-plans-pricing).
