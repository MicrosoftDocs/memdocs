---
# required metadata

title: Troubleshoot use of PKCS certificate profiles to provision certificates with Microsoft Intune | Microsoft Docs
description: Troubleshoot the use of PKCS profiles by devices to request certificates for use with Intune.  
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot PKCS certificate deployment in Microsoft Intune

The information in this article can help you resolve several common issues when deploying private and public key pair (PKCS) certificates in Microsoft Intune. Before troubleshooting, ensure you’ve completed the following tasks, which are documented in [Configure and use PKCS certificates with Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- Review the [requirements for using PKCS certificate profiles](../intune/protect/certficates-pfx-configure.md#requirements)
- Export the root certificate from the Enterprise Certification Authority (CA)
- Configure certificate templates on the certification authority
- Install and configure the Intune Certificate Connector
- Create and deploy a trusted certificate profile to deploy the root certificate
- Create and deploy a PKCS certificate profile 

The most common source of problems for PKCS certificate profiles has been with the configuration of the PKCS certificate profile. Review the profiles configuration and look for typos in server names or FQDNs, and confirm that the **Certificate Authority** and **Certificate Authority Name** are correct.

- **Certification Authority**: This is the internal FQDN of the Certificate Authority computer. For example, server1.domain.local.
- **Certification Authority Name**: This is the Certificate Authority Name as displayed in the certification authority MMC. Look under **Certification Authority (Local)**

To confirm the correct name for the Certification Authority and Certification Authority Name, run the following PowerShell cmdlet on the CA to confirm the CA and CA Name: `certutil -config - -ping`

## PKCS communication overview

The following graphic provides a basic overview of the PKCS certificate deployment process in Intune.

> [!div class="mx-imgBorder"]
> ![PKCS certificate profile flow](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. An Admin creates a PKCS certificate profile in Intune.
2. The Intune service requests that the on-premises Intune Certificate Connector create a new certificate for the user.
3. The Intune Certificate Connector sends a PFX Blob and Request to your Microsoft Certification Authority.
4. The Certification Authority issues and sends the PFX User Certificate back to the Intune Certificate Connector.
5. The Intune Certificate Connector uploads the encrypted PFX User Certificate to Intune.
6. Intune decrypts the PFX User Certificate and re-encrypts for the device using the Device Management Certificate.  Intune then sends the PFX User Certificate to the Device.
7. The device reports the certificate status to Intune.

## Data and Log files

To identify problems for the communication and certificate provisioning workflow, review log files from both the Server infrastructure, and from devices. Later sections for troubleshooting PKCS certificate profiles refer to log files referenced in this section.

- [Infrastructure and Server logs](#logs-for-on-premises-infrastructure)

Device logs depend on the device platform:  

- [iOS and iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### Logs for on-premises infrastructure
  
On-premises infrastructure that supports use of PKCS certificate profiles for certificate deployments includes the Microsoft Intune Certificate Connector, NDES that runs on a Windows Server, and the certification authority.

Log files for these roles include Windows Event Viewer, Certificate consoles, and various log files specific to the Intune Certificate Connector, NDES, or other role and operations that are part of the on-premises infrastructure.

- **NDESConnector_date_time.svclog**:

  This log shows communication from the Microsoft Intune Certificate Connector to the Intune cloud service. You can use the [Service Trace Viewer Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) to view this log file.

  Related registry key: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Location: On the server that hosts NDES at *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**:

  This log shows the NDES policy module receiving and verifying certificate requests. You can use the [Service Trace Viewer Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) to view this log file.

  Location: On the server that hosts NDES at *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**:

  This log shows the passing of certificate requests to the Certificate Registration Point, and the resulting verification of those requests.

  Location: On the server that hosts NDES at *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Windows Application log**:

  Location: On the server that hosts NDES: Run **eventvwr.msc** to open Windows Event Viewer

### Logs for Android devices

For devices that run Android, use the **Android Company Portal** app log file, **OMADM.log**. Before you collect and review logs, enable ensure [Verbose Logging](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) is enabled, and then reproduce the issue.

To collect the OMADM.logs from a device, see [Upload and email logs using a USB cable](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

You can also [Upload and email logs](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) to support.

### Logs for iOS and iPadOS devices

For devices that run iOS/iPadOS, you use debug logs and **Xcode** that runs on a Mac computer:

1. Connect the iOS/iPadOS device to Mac, and then go to **Applications** > **Utilities** to open the Console app. 

2. Under **Action**, select **Include Info Messages** and **Include Debug Messages**.

   ![Select log options](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Reproduce the problem, and then save the logs to a text file:
   1. Select **Edit** > **Select All** to select all the messages on the current screen, and then select **Edit** > **Copy** to copy the messages to the clipboard.
   2. Open the TextEdit application, paste the copied logs into a new text file, and then save the file.

The Company Portal log for iOS and iPadOS devices doesn't contain information about PKCS certificate profiles.

### Logs for Windows devices

For devices that run Windows, use the Windows Event logs to diagnose enrollment or device management issues for devices that you manage with Intune.

On the device, open **Event Viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Windows event logs](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## Common errors
The following common errors are each addressed in a following section:

- [The RPC server is unavailable 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [An enrollment policy server cannot be located 0x80094015](#)
- [The submission is pending](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [The parameter is incorrect 0x80070057](#the-submission-is-pending)
- [The submission failed: Denied by Policy Module](#the-submission-failed:-denied-by-policy-module)
- [Certificate profile stuck as Pending](#certificate-profile-stuck-as-pending)
- [Error “-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED”](#error-“-2146875374-certsrv_e_subject_email_required”)

### The RPC server is unavailable 0x800706ba

During PFX deployment, the trusted root certificate appears on the device but the PFX certificate doesn't appear on the device. The NDESConnector log file contains the string **The RPC server is unavailable. 0x800706ba**, as seen in the first line of the following example:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

**Cause 1: Incorrect configuration of the CA in Intune**  
This issue can occur when the PKCS certificate profile in Intune specifies the wrong server, or contains spelling errors for the name or FQDN of the CA. The CA is specified in the following properties of the profile:

- Certification authority
- Certification authority name

  **Resolution**:

  To fix the issue, make sure the following:
  1. The **Certification authority** property displays the internal fully qualified domain name (FQDN) of your CA server.
  2. The **Certification authority name** property displays the name of your CA.

**Cause 2: CA doesn’t support certificate renewal for requests signed by previous CA certificates**  
If the CA FQDN and name are correctly specified in the PKCS certificate profile, review the Windows Application log that’s on the certificate authority server. Look for an **Event ID 128** that resembles the following example:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

When the CA certificate renews, it must sign the Online Certificate Status Protocol (OCSP) Response Signing certificate. Signing enables the OCSP Response Signing certificate to validate other certificates by checking on their revocation status. This signing isn’t enabled by default.

  **Resolution**:
To fix this issue, manually force signing of the certificate:
  1. On the CA server, open an elevated Command Prompt and run the following command: **certutil -setreg ca\UseDefinedCACertInRequest 1**
  2. Restart the Certificate Services service.

After the Certificate Services service restarts, devices can receive certificates.

### An enrollment policy server cannot be located 0x80094015

