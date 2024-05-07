---
title: Windows Autopilot device preparation requirements
description: Requirements for Windows Autopilot device preparation.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/26/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: conceptual
ms.custom:
  - CI 116757
  - CSSTroubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---


# Windows Autopilot device preparation requirement

## Windows Autopilot device preparation software requirements

Windows Autopilot device preparation depends on specific features available in Windows client, Microsoft Entra ID, and MDM services, such as Microsoft Intune. To use Windows Autopilot device preparation and access these features, some software requirements must be met.

> [!NOTE]
>
> For a list of OEMs that currently support Windows Autopilot device preparation, see the Participant device manufacturers section at [Windows Autopilot device preparation](https://www.microsoft.com/microsoft-365/windows/windows-autopilot).

### Windows 11

A [supported version](/windows/release-health/) of Windows 11 General Availability Channel is required.

The following editions are supported:

- Windows 11 Pro
- Windows 11 Pro Education
- Windows 11 Pro for Workstations
- Windows 11 Enterprise
- Windows 11 Education

## Windows Autopilot device preparation networking requirements

Windows Autopilot device preparation depends on various internet-based services. Access to these services must be provided for Windows Autopilot device preparation to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following conditions:

- Ensure Domain Name Services (DNS) name resolution for internet DNS names.
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP).

Additional configuration might be required to grant access to required services in environments that:

- Have more restrictive internet access.
- Require authentication before internet access can be obtained.

> [!NOTE]
>
> Smart card and certificate based authentication isn't supported during OOBE. For more information, see [Smartcards and certificate-based authentication](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

### Windows Autopilot device preparation deployment service

After a network connection is in place, each Windows device will contact the Windows Autopilot device preparation Deployment Service. The following URLs are used:

- `https://ztd.dds.microsoft.com`
- `https://cs.dds.microsoft.com`
- `https://login.live.com`

### Windows activation

Windows Autopilot device preparation requires Windows Activation services. For more information about the URLs that need to be accessible for the activation services, see [Windows activation or validation fails with error code 0x8004FE33](https://support.microsoft.com/topic/windows-activation-or-validation-fails-with-error-code-0x8004fe33-a9afe65e-230b-c1ed-3414-39acd7fddf52).

### Microsoft Entra ID

Microsoft Entra ID validates user credentials, and the device can also be joined to Microsoft Entra ID. For more information, see [Office 365 IP Address and URL Web service](/microsoft-365/enterprise/microsoft-365-ip-web-service).

### Microsoft Intune

Once authenticated, Microsoft Entra ID triggers enrollment of the device into the Intune mobile device management (MDM) service. For more information about Intune's network communication requirements, see the following articles:

- [Intune network configuration requirements and bandwidth](/mem/intune/fundamentals/network-bandwidth-use).
- [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints).

### Windows Autopilot device preparation automatic device diagnostics collection

For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` isn't blocked on the network. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

### Windows Update

During the OOBE process and after the Windows OS configuration, the Windows Update service retrieves needed updates. If there are problems connecting to Windows Update, see [Windows Update troubleshooting](/windows/deployment/update/windows-update-troubleshooting).

If Windows Update is inaccessible, the Autopilot process still continues but critical updates aren't available.

### Delivery Optimization

Windows Autopilot device preparation contacts the [Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) service when downloading the apps and updates. This contact establishes peer-to-peer sharing of content so that only a few devices need to download it from the internet.

- Windows Updates.
- Microsoft Store apps and app updates.
- Office Updates.
- Intune Win32 Apps.

If the Delivery Optimization Service is inaccessible, the Autopilot process still continues with Delivery Optimization downloads from the cloud without peer-to-peer.

### Network Time Protocol (NTP) sync

When a Windows device starts up, it talks to a network time server to ensure that the time on the device is correct. Ensure that UDP port **123** to `time.windows.com` is accessible.

### Domain Name Services (DNS)

To resolve DNS names for all services, the device communicates with a DNS server, typically provided via DHCP. This DNS server must be able to resolve internet names.

### Diagnostics data

Diagnostic data collection is enabled by default. To disable Windows Analytics and related diagnostics capabilities, see [Manage enterprise diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data).

If the device can't send diagnostic data, the Windows Autopilot device preparation process still continues. However, services that depend on diagnostic data, such as Desktop Analytics, doesn't work.

### Network Connection Status Indicator (NCSI)

Windows must be able to tell that the device can access the internet. For more information, see [Network Connection Status Indicator (NCSI)](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator).

`*.msftconnecttest.com` must be resolvable via DNS and accessible via HTTP.

### Windows Notification Services (WNS)

This service is used to enable Windows to receive notifications from apps and services. For more information, see [Microsoft Store](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store).

If the WNS services aren't available, the Windows Autopilot device preparation process still continues without notifications.

### Microsoft Store, Microsoft Store for Business & Education

Apps in the Microsoft Store can be pushed to the device by triggering them via Intune (MDM). App updates and additional apps might also be needed when the user first logs in. For more information, see [Prerequisites for Microsoft Store for Business and Education](/microsoft-store/prerequisites-microsoft-store-for-business). (It also includes Microsoft Entra ID and Windows Notification Services).

If the Microsoft Store isn't accessible, the Autopilot process still continues without Microsoft Store apps.

### Microsoft 365

As part of the Intune device configuration, installation of Microsoft 365 Apps for enterprise might be required. For more information, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges). This article includes all Office services, DNS names, IP addresses. It also includes Microsoft Entra ID and other services that might overlap with the previously listed services listed.

### Certificate revocation lists (CRLs)

Some of these services also need to check certificate revocation lists (CRLs) for certificates used in the services. For a full list, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges) and [Office 365 Certificate Chains](/microsoft-365/compliance/encryption-office-365-certificate-chains).

### Proxy settings

Deploying proxy settings for Windows Autopilot device preparation should be configured on the proxy server itself. Implementing proxy settings via Intune policy isn't fully supported as it might cause issues and unexpected behavior with privileged access deployments.

## Windows Autopilot device preparation licensing requirements

Windows Autopilot device preparation depends on specific capabilities available in Windows client and Microsoft Entra ID. It also requires an MDM service such as Microsoft Intune. These capabilities can be obtained through various editions and subscription programs:

To provide needed Microsoft Entra ID (automatic MDM enrollment and company branding features) and MDM functionality, one of the following subscriptions is required:

- [Microsoft 365 Business Premium subscription](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 or F3 subscription](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic A1, A3, or A5 subscription](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 or E5 subscription](https://www.microsoft.com/microsoft-365/enterprise), which include all Windows client, Microsoft 365, and EMS features (Microsoft Entra ID and Intune).
- [Enterprise Mobility + Security E3 or E5 subscription](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), which include all needed Microsoft Entra ID and Intune features.
- [Intune for Education subscription](/intune-education/what-is-intune-for-education), which include all needed Microsoft Entra ID and Intune features.
- [Microsoft Entra ID P1 or P2](https://azure.microsoft.com/services/active-directory/) and [Microsoft Intune subscription](https://www.microsoft.com/cloud-platform/microsoft-intune) (or an alternative MDM service).

> [!NOTE]
>
> Even when using Microsoft 365 subscriptions, you still need to [assign Intune licenses to the users](/intune/fundamentals/licenses-assign).

Additionally, the following are also recommended (but not required):

- [Microsoft 365 Apps for enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), which can be deployed easily via Intune (or other MDM services).
- [Windows Subscription Activation](/windows/deployment/windows-10-enterprise-subscription-activation), to automatically step up devices from Windows Pro to Windows Enterprise edition.


## Related content

