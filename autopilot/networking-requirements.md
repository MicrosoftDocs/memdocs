---
title: Windows Autopilot networking requirements
description: Inform yourself about networking requirements for Windows Autopilot deployment.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 12/08/2023
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
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a> 
---

# Windows Autopilot networking requirements

Windows Autopilot depends on various internet-based services. Access to these services must be provided for Autopilot to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following conditions:

- Ensure Domain Name Services (DNS) name resolution for internet DNS names.
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP).

Additional configuration might be required to grant access to required services in environments that:

- Have more restrictive internet access.
- Require authentication before internet access can be obtained.

> [!NOTE]
>
> Smart card and certificate based authentication isn't supported during OOBE. For more information, see [Smartcards and certificate-based authentication](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

## Service requirements

For additional details about each of these services and their specific requirements, review these details.

### Windows Autopilot Deployment Service

After a network connection is in place, each Windows device will contact the Windows Autopilot Deployment Service. The following URLs are used:

- `https://ztd.dds.microsoft.com`
- `https://cs.dds.microsoft.com`
- `https://login.live.com`

### Windows Activation

Windows Autopilot requires Windows Activation services. For more information about the URLs that need to be accessible for the activation services, see [Windows activation or validation fails with error code 0x8004FE33](https://support.microsoft.com/topic/windows-activation-or-validation-fails-with-error-code-0x8004fe33-a9afe65e-230b-c1ed-3414-39acd7fddf52).

<a name='azure-active-directory-azure-ad'></a>

### Microsoft Entra ID

Microsoft Entra ID validates user credentials, and the device can also be joined to Microsoft Entra ID. For more information, see [Office 365 IP Address and URL Web service](/microsoft-365/enterprise/microsoft-365-ip-web-service).

### Microsoft Intune

Once authenticated, Microsoft Entra ID triggers enrollment of the device into the Intune mobile device management (MDM) service. For more information about Intune's network communication requirements, see the following articles:

- [Intune network configuration requirements and bandwidth](/mem/intune/fundamentals/network-bandwidth-use).
- [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints).

### Autopilot automatic device diagnostics collection

For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` isn't blocked on the network. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

### Windows Update

During the OOBE process and after the Windows OS configuration, the Windows Update service retrieves needed updates. If there are problems connecting to Windows Update, see [Windows Update troubleshooting](/windows/deployment/update/windows-update-troubleshooting).

If Windows Update is inaccessible, the Autopilot process still continues but critical updates aren't available.

### Delivery Optimization

Autopilot contacts the [Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) service when downloading the apps and updates. This contact establishes peer-to-peer sharing of content so that only a few devices need to download it from the internet.

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

If the device can't send diagnostic data, the Autopilot process still continues. However, services that depend on diagnostic data, such as Desktop Analytics, doesn't work.

### Network Connection Status Indicator (NCSI)

Windows must be able to tell that the device can access the internet. For more information, see [Network Connection Status Indicator (NCSI)](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator).

`*.msftconnecttest.com` must be resolvable via DNS and accessible via HTTP.

### Windows Notification Services (WNS)

This service is used to enable Windows to receive notifications from apps and services. For more information, see [Microsoft Store](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store).

If the WNS services aren't available, the Autopilot process still continues without notifications.

### Microsoft Store, Microsoft Store for Business & Education

Apps in the Microsoft Store can be pushed to the device by triggering them via Intune (MDM). App updates and additional apps might also be needed when the user first logs in. For more information, see [Prerequisites for Microsoft Store for Business and Education](/microsoft-store/prerequisites-microsoft-store-for-business). (It also includes Microsoft Entra ID and Windows Notification Services).

If the Microsoft Store isn't accessible, the Autopilot process still continues without Microsoft Store apps.

### Microsoft 365

As part of the Intune device configuration, installation of Microsoft 365 Apps for enterprise might be required. For more information, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges). This article includes all Office services, DNS names, IP addresses. It also includes Microsoft Entra ID and other services that might overlap with the previously listed services listed.

### Certificate revocation lists (CRLs)

Some of these services also need to check certificate revocation lists (CRLs) for certificates used in the services. For a full list, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges) and [Office 365 Certificate Chains](/microsoft-365/compliance/encryption-office-365-certificate-chains).

<a name='hybrid-azure-ad-join'></a>

### Microsoft Entra hybrid join

> [!IMPORTANT]
>
> Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Autopilot. For more information, see [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints: Which option is right for your organization](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined#which-option-is-right-for-your-organization).

The device can be Microsoft Entra hybrid joined. The computer should be on the internal network for Microsoft Entra hybrid join to work. For more information, see [Windows Autopilot user-driven mode](user-driven.md#user-driven-mode-for-hybrid-azure-ad-join).

### <a name="tpm"></a> Autopilot self-deploying mode and Autopilot pre-provisioning

The TPM attestation process requires access to a set of HTTPS URLs, which are unique for each TPM provider. Ensure access to this URL pattern: `*.microsoftaik.azure.net`.

Firmware TPM devices, which are only provided by Intel, AMD, or Qualcomm, don't include all needed certificates at boot time and must be able to retrieve them from the manufacturer on first use. Devices with discrete TPM chips come with these certificates preinstalled. These devices include ones from any other manufacturer. For more information, see [TPM recommendations](/windows/security/information-protection/tpm/tpm-recommendations).

For each firmware TPM provider, make sure that the appropriate URL is accessible so that certificates can be successfully requested. For example:

- Intel: `https://ekop.intel.com/ekcertservice`
- Qualcomm: `https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1`
- AMD: `https://ftpm.amd.com/pki/aia`

### Proxy settings

Deploying proxy settings for Windows Autopilot should be configured on the proxy server itself. Implementing proxy settings via Intune policy isn't fully supported as it might cause issues and unexpected behavior with privileged access deployments.

## Next steps

- [Windows Autopilot licensing requirements](licensing-requirements.md).
