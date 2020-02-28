---
# required metadata

title: Troubleshoot use of SCEP certificate profiles to provision certificates with Microsoft Intune | Microsoft Docs
description: Troubleshoot the use of SCEP by devices to request certificates for use with Intune, including communication from devices to NDES, NDES to certification authorities, and from the Intune Certificate Connector to the Intune service.  
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Overview for troubleshooting SCEP certificate profiles with Microsoft Intune

Use of Simple Certificate Enrollment Protocol (SCEP) certificate profiles can be challenging to troubleshoot in Intune. This article is an overview that can help you resolve issues by:

- Explaining the architecture and the communication flow of the SCEP process
- Helping you to narrow down where a problem exists in that communication flow
- Identifying the key log files that are referenced in subsequent articles for troubleshooting certificate profiles

The information in this and the related SCEP certificate troubleshooting articles applies to using SCEP certificate profiles with Android, iOS/iPad, and Windows devices. Similar information for macOS is not available at this time.

To troubleshoot Network Device Enrollment Service (NDES), see the following articles from support.microsoft.com:

- [Verify NDES configuration on-premises for SCEP certificates in Intune](https://support.microsoft.com/help/4490130/ndes-configuration-on-premises-for-scep-certificates-in-intune)
- [Troubleshooting NDES configuration for use with Microsoft Intune certificate profiles]( https://support.microsoft.com/help/4459540/troubleshoot-ndes-configuration-for-use-with-intune)

Before proceeding, ensure you've meet the [prerequisites for using SCEP certificate profiles](certificates-scep-configure.md#prerequisites-for-using-scep-for-certificates), including the deployment of a root certificate through a trusted certificate profile.

## SCEP communication flow overview

The following graphic demonstrates a basic overview of the SCEP communication process in Intune.

![SCEP certificate profile flow](../protect/media/troubleshoot-scep-certificate-profiles/scep-certificate-profile-flow.png)

1. [Deploy a SCEP certificate profile](troubleshoot-scep-certificate-profile-deployment.md). Intune generates a challenge string, which requires a specific user, certificate purpose, and certificate type.

2. [Device to NDES server communication](troubleshoot-scep-certificate-device-to-ndes.md). The device uses the URI for NDES from the profile to contact the NDES server so it can present a challenge.

3. [NDES to policy module communication](troubleshoot-scep-certificate-ndes-policy-module.md). NDES forwards the challenge to the Intune Certificate Connector policy module on the server, which validates the request.

4. [NDES to certification authority](troubleshoot-scep-certificate-ndes-policy-module.md). NDES passes valid requests to issue a certificate to the Certification Authority (CA).

5. [Certificate delivery to the device](troubleshoot-scep-certificate-delivery.md). The certificate is delivered to the device.

6. [Reporting of deployment to Intune](troubleshoot-scep-certificate-reporting.md). The Intune Certificate Connector reports the certificate issuance event to Intune.

## Log files

To identify problems for the communication and certificate provisioning workflow, review log files from both the Server infrastructure, and from devices. Later sections for troubleshooting SCEP certificate profiles refer to log files referenced in this section.

- [Infrastructure and Server logs](#logs-for-on-premises-infrastructure)

Device logs depend on the device platform:  

- [iOS and iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### Logs for on-premises infrastructure
  
On-premises infrastructure that supports use of SCEP certificate profiles for certificate deployments includes the Microsoft Intune Certificate Connector, NDES that runs on a Windows Server, and the certification authority.

Log files for these roles include Windows Event Viewer, Certificate consoles, and various log files specific to the Intune Certificate Connector, NDES, or other role and operations that are part of the on-premises infrastructure.

The following list includes logs or consoles that are referenced in the subsequent SCEP troubleshooting articles. 

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

- **IIS logs**:

  IIS logs show the certificate requests from mobile devices entering NDES.

  Location: On the server that hosts NDES at *c:\inetpub\logs\LogFiles\W3SVC1*

- **Windows Application log**:

  This log is useful when investigating IIS issues, like the SCEP application pool.

  Location: On the server that hosts NDES: Run **eventvwr.msc** to open Windows Event Viewer




### Logs for Android devices

For devices that run Android, use the **Android Company Portal** app log file, **OMADM.log**. Before you collect and review logs, enable ensure [Verbose Logging](/intune-user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android) is enabled, and then reproduce the issue.

To collect the OMADM.logs from a device, see [Upload and email logs using a USB cable](/intune-user-help/send-logs-to-your-it-admin-using-cable-android).

You can also [Upload and email logs](/intune-user-help/send-logs-to-your-it-admin-by-email-android#upload-and-email-logs-from-microsoft-intune-app) to support.

### Logs for iOS and iPadOS devices

For devices that run iOS/iPadOS, you use debug logs and **Xcode** that runs on a Mac computer:

1. Connect the iOS/iPadOS device to Mac, and then go to **Applications** > **Utilities** to open the Console app. 

2. Under **Action**, select **Include Info Messages** and **Include Debug Messages**.

   ![Select log options](../protect/media/troubleshoot-scep-certificate-profiles/message-options.png)

3. Reproduce the problem, and then save the logs to a text file:
   1. Select **Edit** > **Select All** to select all the messages on the current screen, and then select **Edit** > **Copy** to copy the messages to the clipboard. 
   2. Open the TextEdit application, paste the copied logs into a new text file, and then save the file.


The Company Portal log for iOS and iPadOS devices doesn't contain information about SCEP certificate profiles.

### Logs for Windows devices

For devices that run Windows, use the Windows Event logs to diagnose enrollment or device management issues for devices that you manage with Intune.

On the device, open **Event Viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Windows event logs](../protect/media/troubleshoot-scep-certificate-profiles/windows-event-log.png)

## Next steps

Review [deployment of SCEP certificate profiles](troubleshoot-scep-certificate-profile-deployment.md) 
