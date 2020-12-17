---
title: Windows Autopilot networking requirements
ms.reviewer: 
manager: laurawi
description: Inform yourself about networking requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot networking requirements

**Applies to**

- Windows 10
- Windows Holographic, version 2004 or later

Windows Autopilot depends on a variety of internet-based services. Access to these services must be provided for Autopilot to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following conditions:

- Ensure Domain Name Services (DNS) name resolution for internet DNS names
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP)

Additional configuration may be required to grant access to required services in environments that:
- have more restrictive Internet access.
- require authentication before internet access can be obtained. 

> [!NOTE]
> Smart card and certificate based authentication isn't supported during OOBE. For more information, see [Smartcards and certificate-based authentication](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

For additional details about each of these services and their specific requirements, review the following details:

<table><th>Service<th>Information
<tr><td><b>Windows Autopilot Deployment Service<b><td>After a network connection is in place, each Windows 10 device will contact the Windows Autopilot Deployment Service. With Windows 10 version 1903 and above, the following URLs are used: https://ztd.dds.microsoft.com, https://cs.dds.microsoft.com, and https://login.live.com.<br>

<tr><td><b>Windows Activation<b><td>Windows Autopilot requires Windows Activation services. For details about the URLs that need to be accessible for the activation services, see <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows activation or validation fails with error code 0x8004FE33</a>.<br>

<tr><td><b>Azure Active Directory<b><td>User credentials are validated by Azure Active Directory, and the device can also be joined to Azure Active Directory. For more information, see <a href="/office365/enterprise/office-365-ip-web-service">Office 365 IP Address and URL Web service</a>.
<tr><td><b>Intune<b><td>Once authenticated, Azure Active Directory will trigger enrollment of the device into the Intune mobile device management (MDM) service. See the following link for details about network communication requirements: <a href="/intune/network-bandwidth-use#network-communication-requirements">Intune network configuration requirements and bandwidth</a>.
<tr><td><b>Windows Update<b><td>During the OOBE process and after the Windows 10 OS configuration, the Windows Update service retrieves needed updates. If there are problems connecting to Windows Update, see <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">How to solve connection problems concerning Windows Update or Microsoft Update</a>.<br>

If Windows Update is inaccessible, the Autopilot process will still continue but critical updates won't be available.

<tr><td><b>Delivery Optimization<b><td>Autopilot contacts the <a href="/windows/deployment/update/waas-delivery-optimization">Delivery Optimization</a> service when downloading the apps and updates. This contact establishes peer-to-peer sharing of content so that only a few devices need to download it from the Internet.
- Windows Updates
- Microsoft Store apps and app updates
- Office Updates
- Intune Win32 Apps<br>

If the Delivery Optimization Service is inaccessible, the Autopilot process will still continue with Delivery Optimization downloads from the cloud (without peer-to-peer).

<tr><td><b>Network Time Protocol (NTP) Sync<b><td>When a Windows device starts up, it will talk to a network time server to ensure that the time on the device is correct. Ensure that UDP port 123 to time.windows.com is accessible.
<tr><td><b>Domain Name Services (DNS)<b><td>To resolve DNS names for all services, the device communicates with a DNS server, typically provided via DHCP. This DNS server must be able to resolve internet names.
<tr><td><b>Diagnostics data<b><td>Starting in Windows 10, 1903, diagnostic data collection will be enabled by default. To disable Windows Analytics and related diagnostics capabilities, see <a href="/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Manage enterprise diagnostic data level</a>.<br>

If diagnostic data can't be sent, the Autopilot process still continues. However, services that depend on diagnostic data, such as Windows Analytics, won't work.
<tr><td><b>Network Connection Status Indicator (NCSI)<b><td>Windows must be able to tell that the device can access the internet. For more information, see <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">Network Connection Status Indicator (NCSI)</a>.

<code>www.msftconnecttest.com</code> must be resolvable via DNS and accessible via HTTP.
<tr><td><b>Windows Notification Services (WNS)<b><td>This service is used to enable Windows to receive notifications from apps and services. For more information, see <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>.<br>

If the WNS services aren't available, the Autopilot process will still continue without notifications.
<tr><td><b>Microsoft Store, Microsoft Store for Business<b><td>Apps in the Microsoft Store can be pushed to the device, triggered via Intune (MDM).  App updates and additional apps may also be needed when the user first logs in. For more information, see <a href="/microsoft-store/prerequisites-microsoft-store-for-business">Prerequisites for Microsoft Store for Business and Education</a> (also includes Azure AD and Windows Notification Services).<br>

If the Microsoft Store isn't accessible, the Autopilot process will still continue without Microsoft Store apps.

<tr><td><b>Microsoft 365<b><td>As part of the Intune device configuration, installation of Microsoft 365 Apps for enterprise may be required. For more information, see <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">Office 365 URLs and IP address ranges</a>. This article includes all Office services, DNS names, IP addresses. It also includes Azure AD and other services that may overlap with the services listed above.
<tr><td><b>Certificate revocation lists (CRLs)<b><td>Some of these services will also need to check certificate revocation lists (CRLs) for certificates used in the services.  For a full list, see <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">Office 365 URLs and IP address ranges</a> and <a href="/microsoft-365/compliance/encryption-office-365-certificate-chains">Office 365 Certificate Chains</a>.
<tr><td><b>Hybrid Azure AD join<b><td>The device can be hybrid Azure AD joined. The computer should be on corporate network for hybrid Azure AD join to work. See details at <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">Windows Autopilot user-driven mode</a>
<tr><td><a href="" id="tpm"></a><b>Autopilot self-Deploying mode and Autopilot pre-provisioning<b><td>
The TPM attestation process requires access to a set of HTTPS URLs (unique for each TPM provider).  Ensure access to this URL pattern: *.microsoftaik.azure.net.<br><br>
 
Firmware TPM devices, which are only provided by Intel, AMD, or Qualcomm, don't include all needed certificates at boot time and must be able to retrieve them from the manufacturer on first use. Devices with discrete TPM chips (including devices from any other manufacturer) come with these certificates preinstalled. For more information, see <a href="/windows/security/information-protection/tpm/tpm-recommendations">TPM recommendations</a>. 

For each firmware TPM provider, make sure that the appropriate URL is accessible so that certificates can be successfully requested. For example:

 Intel- <code>https://ekop.intel.com/ekcertservice</code>
 <br>Qualcomm- <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>AMD- <code>https://ftpm.amd.com/pki/aia</code>

</table>

**Next steps**

[Windows Autopilot licensing requirements](licensing-requirements.md)