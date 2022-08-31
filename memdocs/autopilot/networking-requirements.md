---
title: Windows Autopilot networking requirements
description: Inform yourself about networking requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 08/23/2022
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---

# Windows Autopilot networking requirements

**Applies to**

- Windows 11
- Windows 10
- Windows Holographic, version 2004 or later

Windows Autopilot depends on a variety of internet-based services. Access to these services must be provided for Autopilot to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following conditions:

- Ensure Domain Name Services (DNS) name resolution for internet DNS names.
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP).

Additional configuration may be required to grant access to required services in environments that:

- Have more restrictive internet access.
- Require authentication before internet access can be obtained.

> [!NOTE]
> Smart card and certificate based authentication isn't supported during OOBE. For more information, see [Smartcards and certificate-based authentication](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

## Service requirements

For additional details about each of these services and their specific requirements, review these details.

### Windows Autopilot Deployment Service

After a network connection is in place, each Windows device will contact the Windows Autopilot Deployment Service. With Windows 10 version 1903 and above, the following URLs are used:

- `https://ztd.dds.microsoft.com`
- `https://cs.dds.microsoft.com`
- `https://login.live.com`

### Windows Activation

Windows Autopilot requires Windows Activation services. For more information about the URLs that need to be accessible for the activation services, see [Windows activation or validation fails with error code 0x8004FE33](https://support.microsoft.com/topic/windows-activation-or-validation-fails-with-error-code-0x8004fe33-a9afe65e-230b-c1ed-3414-39acd7fddf52).

### Azure Active Directory (Azure AD)

User credentials are validated by Azure AD, and the device can also be joined to Azure AD. For more information, see [Office 365 IP Address and URL Web service](/microsoft-365/enterprise/microsoft-365-ip-web-service).

### Microsoft Intune

Once authenticated, Azure AD will trigger enrollment of the device into the Intune mobile device management (MDM) service. For more information about Intune's network communication requirements, see the following articles:

- [Intune network configuration requirements and bandwidth](../intune/fundamentals/network-bandwidth-use.md)
- [Network endpoints for Microsoft Intune](../intune/fundamentals/intune-endpoints.md)

### Windows Update

During the OOBE process and after the Windows OS configuration, the Windows Update service retrieves needed updates. If there are problems connecting to Windows Update, see [Windows Update troubleshooting](/windows/deployment/update/windows-update-troubleshooting).

If Windows Update is inaccessible, the Autopilot process will still continue but critical updates won't be available.

### Delivery Optimization

Autopilot contacts the [Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) service when downloading the apps and updates. This contact establishes peer-to-peer sharing of content so that only a few devices need to download it from the internet.

- Windows Updates
- Microsoft Store apps and app updates
- Office Updates
- Intune Win32 Apps

If the Delivery Optimization Service is inaccessible, the Autopilot process will still continue with Delivery Optimization downloads from the cloud without peer-to-peer.

### Network Time Protocol (NTP) sync

When a Windows device starts up, it will talk to a network time server to ensure that the time on the device is correct. Ensure that UDP port **123** to `time.windows.com` is accessible.

### Domain Name Services (DNS)

To resolve DNS names for all services, the device communicates with a DNS server, typically provided via DHCP. This DNS server must be able to resolve internet names.

### Diagnostics data

Starting in Windows 10, version 1903, diagnostic data collection will be enabled by default. To disable Windows Analytics and related diagnostics capabilities, see [Manage enterprise diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data).

If the device can't send diagnostic data, the Autopilot process still continues. However, services that depend on diagnostic data, such as Desktop Analytics, won't work.

### Network Connection Status Indicator (NCSI)

Windows must be able to tell that the device can access the internet. For more information, see [Network Connection Status Indicator (NCSI)](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator).

`www.msftconnecttest.com` must be resolvable via DNS and accessible via HTTP.

### Windows Notification Services (WNS)

This service is used to enable Windows to receive notifications from apps and services. For more information, see [Microsoft Store](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store.

If the WNS services aren't available, the Autopilot process will still continue without notifications.

### Microsoft Store, Microsoft Store for Business & Education

Apps in the Microsoft Store can be pushed to the device, triggered via Intune (MDM). App updates and additional apps may also be needed when the user first logs in. For more information, see [Prerequisites for Microsoft Store for Business and Education](/microsoft-store/prerequisites-microsoft-store-for-business). (It also includes Azure AD and Windows Notification Services).

If the Microsoft Store isn't accessible, the Autopilot process will still continue without Microsoft Store apps.

### Microsoft 365

As part of the Intune device configuration, installation of Microsoft 365 Apps for enterprise may be required. For more information, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges). This article includes all Office services, DNS names, IP addresses. It also includes Azure AD and other services that may overlap with the services listed above.

### Certificate revocation lists (CRLs)

Some of these services will also need to check certificate revocation lists (CRLs) for certificates used in the services. For a full list, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges) and [Office 365 Certificate Chains](/microsoft-365/compliance/encryption-office-365-certificate-chains).

### Hybrid Azure AD join

The device can be hybrid Azure AD joined. The computer should be on the internal network for hybrid Azure AD join to work. For more information, see [Windows Autopilot user-driven mode](user-driven.md#user-driven-mode-for-hybrid-azure-ad-join).

### <a name="tpm"></a> Autopilot self-deploying mode and Autopilot pre-provisioning

The TPM attestation process requires access to a set of HTTPS URLs, which are unique for each TPM provider. Ensure access to this URL pattern: `*.microsoftaik.azure.net`.

Firmware TPM devices, which are only provided by Intel, AMD, or Qualcomm, don't include all needed certificates at boot time and must be able to retrieve them from the manufacturer on first use. Devices with discrete TPM chips come with these certificates preinstalled. These devices include ones from any other manufacturer. For more information, see [TPM recommendations](/windows/security/information-protection/tpm/tpm-recommendations).

For each firmware TPM provider, make sure that the appropriate URL is accessible so that certificates can be successfully requested. For example:

- Intel: `https://ekop.intel.com/ekcertservice`
- Qualcomm: `https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1`
- AMD: `https://ftpm.amd.com/pki/aia`

## Next steps

[Windows Autopilot licensing requirements](licensing-requirements.md)
