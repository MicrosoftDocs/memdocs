---
title: Windows Autopilot networking requirements
ms.reviewer: 
manager: laurawi
description: Inform yourself about networking requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: 
- CI 116757
- CSSTroubleshooting
---


# Windows Autopilot networking requirements

**Applies to: Windows 10**

Windows Autopilot depends on a variety of internet-based services. Access to these services must be provided for Autopilot to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following:

- Ensure DNS name resolution for internet DNS names
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP)

In environments that have more restrictive Internet access, or for those that require authentication before internet access can be obtained, additional configuration may be required to whitelist access to the required services. 

> [!NOTE]
> Smart card and certificate based authentication is not supported during OOBE. For more information, see [Smartcards and certificate-based authentication](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

For additional details about each of these services and their specific requirements, review the following details:

<table><th>Service<th>Information
<tr><td><b>Windows Autopilot Deployment Service<b><td>After a network connection is in place, each Windows 10 device will contact the Windows Autopilot Deployment Service.  With Windows 10 version 1903 and above, the following URLs are used: https://ztd.dds.microsoft.com, https://cs.dds.microsoft.com. <br>

<tr><td><b>Windows Activation<b><td>Windows Autopilot also requires Windows Activation services. See <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows activation or validation fails with error code 0x8004FE33</a> for details about the URLs that need to be accessible for the activation services.<br>

<tr><td><b>Azure Active Directory<b><td>User credentials are validated by Azure Active Directory, and the device can also be joined to Azure Active Directory. See <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">Office 365 IP Address and URL Web service</a> for more information.
<tr><td><b>Intune<b><td>Once authenticated, Azure Active Directory will trigger enrollment of the device into the Intune MDM service. See the following link for details about network communication requirements: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">Intune network configuration requirements and bandwidth</a>.
<tr><td><b>Windows Update<b><td>During the OOBE process, as well as after the Windows 10 OS is fully configured, the Windows Update service is leveraged to retrieve needed updates. If there are problems connecting to Windows Update, see <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">How to solve connection problems concerning Windows Update or Microsoft Update</a>.<br>

If Windows Update is inaccessible, the Autopilot process will still continue but critical updates will not be available.

<tr><td><b>Delivery Optimization<b><td>When downloading Windows Updates, Microsoft Store apps and app updates, Office Updates and Intune Win32 Apps, the <a href="https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization">Delivery Optimization</a> service is contacted to enable peer-to-peer sharing of content so that only a few devices need to download it from the internet.<br>

If the Delivery Optimization Service is inaccessible, the Autopilot process will still continue with Delivery Optimization downloads from the cloud (without peer-to-peer).

<tr><td><b>Network Time Protocol (NTP) Sync<b><td>When a Windows device starts up, it will talk to a network time server to ensure that the time on the device is accurate. Ensure that UDP port 123 to time.windows.com is accessible.
<tr><td><b>Domain Name Services (DNS)<b><td>To resolve DNS names for all services, the device communicates with a DNS server, typically provided via DHCP.  This DNS server must be able to resolve internet names.
<tr><td><b>Diagnostics data<b><td>Starting in Windows 10, 1903, diagnostic data collection will be enabled by default. To disable Windows Analytics and related diagnostics capabilities, see <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Manage enterprise diagnostic data level</a>.<br>

If diagnostic data cannot be sent, the Autopilot process will still continue, but services that depend on diagnostic data, such as Windows Analytics, will not work.
<tr><td><b>Network Connection Status Indicator (NCSI)<b><td>Windows must be able to tell that the device is able to access the internet. For more information, see <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">Network Connection Status Indicator (NCSI)</a>.

<a href="http://www.msftconnecttest.com">www.msftconnecttest.com</a> must be resolvable via DNS and accessible via HTTP.
<tr><td><b>Windows Notification Services (WNS)<b><td>This service is used to enable Windows to receive notifications from apps and services. See <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> for more information.<br>

If the WNS services are not available, the Autopilot process will still continue without notifications.
<tr><td><b>Microsoft Store, Microsoft Store for Business<b><td>Apps in the Microsoft Store can be pushed to the device, triggered via Intune (MDM).  App updates and additional apps may also be needed when the user first logs in. For more information, see <a href="https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business">Prerequisites for Microsoft Store for Business and Education</a> (also includes Azure AD and Windows Notification Services).<br>

If the Microsoft Store is not accessible, the Autopilot process will still continue without Microsoft Store apps.

<tr><td><b>Office 365<b><td>As part of the Intune device configuration, installation of Microsoft 365 Apps for enterprise may be required. For more information, see <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">Office 365 URLs and IP address ranges</a> (includes all Office services, DNS names, IP addresses; includes Azure AD and other services that may overlap with those listed above).
<tr><td><b>Certificate revocation lists (CRLs)<b><td>Some of these services will also need to check certificate revocation lists (CRLs) for certificates used in the services.  A full list of these is documented at <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">Office 365 URLs and IP address ranges</a> and <a href="https://aka.ms/o365chains">Office 365 Certificate Chains</a>.
<tr><td><b>Hybrid AAD join<b><td>The device can be hybrid AAD joined. The computer should be on corporate network for hybrid AAD join to work. See details at <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">Windows Autopilot user-driven mode</a>
<tr><td><b>Autopilot Self-Deploying mode and Autopilot White Glove<b><td>Firmware TPM devices, which are only provided by Intel, AMD, or Qualcomm, do not include all needed certificates at boot time and must be able to retrieve them from the manufacturer on first use. Devices with discrete TPM chips (including devices from any other manufacturer) come with these certificates preinstalled. See <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">TPM recommendations</a> for more details. Make sure that these URLs are accessible for each firmware TPM provider so that certificates can be successfully requested: 

  <br>Intel- https://ekop.intel.com/ekcertservice 
  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1
  <br>AMD- https://ftpm.amd.com/pki/aia

</table>

## Next steps

[Windows Autopilot licensing requirements](licensing-requirements.md)

