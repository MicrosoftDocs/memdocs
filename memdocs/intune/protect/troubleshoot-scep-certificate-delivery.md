---
# required metadata

title: Troubleshoot delivery of certificates to devices when you use SCEP with Microsoft Intune | Microsoft Docs
description: Troubleshoot the delivery of a certificate to a device from the CA when using SCEP certificate profiles with Intune to deploy certificates.
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

# Troubleshoot the delivery of certificates provisioned by SCEP to devices in Microsoft Intune

Use the information in this article to help you investigate delivery of certificates to devices when you use Simple Certificate Enrollment Protocol (SCEP) to provision certificates in Intune. After the Network Device Enrollment Service (NDES) server receives the requested certificate for a device from the certification authority (CA), it passes that certificate back to the device.

This article applies to the step 5 of the [SCEP communication workflow](troubleshoot-scep-certificate-profiles.md); delivery of the certificate to the device that submitted the certificate request.

## Review the certification authority

When the CA has issued the certificate, you'll see an entry similar to the following example on the CA:

![Example of issued certificates](../intune/protect/media/troubleshoot-scep-certificate-delivery/certificate-authority.png)

## Review the device

### Android

For device administrator enrolled devices, you'll see a notification similar to the following image, which prompts you to install the certificate:

![Android notification](../intune/protect/media/troubleshoot-scep-certificate-delivery/android-notification.png)

For Android Enterprise or Samsung Knox, the certificate installation is automatic, and silent.

To view an installed certificate on Android, use a 3rd party certificate viewing app.

You can also review the [devices OMADM log](troubleshoot-scep-certificate-profiles.md#logs-for-android-devices). Look for entries that resemble the following, which are logged when certificates install:

**Root certificate**:

```
2018-02-27T04:50:52.1890000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595        9    Root cert '17…' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALL_REQUESTED
2018-02-27T04:53:31.1300000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595        0    Root cert '17…' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALLING
2018-02-27T04:53:32.0390000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595       14    Root cert '17…' state changed from CERT_INSTALLING to CERT_INSTALL_SUCCESS
```

**Certificate provisioned through SCEP**

```
2018-02-27T05:16:08.2500000    VERB    Event     com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager    18327       10    There are 1 requests
2018-02-27T05:16:08.2500000    VERB    Event     com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager    18327       10    Trying to enroll certificate request: ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787
2018-02-27T05:16:20.6150000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Sending GetCACert(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=ca
2018-02-27T05:16:20.6530000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Received '200 OK' when sending GetCACert(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=ca
2018-02-27T05:16:21.7460000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Sending GetCACaps(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:21.7890000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Received '200 OK' when sending GetCACaps(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:28.0340000    VERB    Event     org.jscep.transaction.EnrollmentTransaction    18327       10    Response: org.jscep.message.CertRep@3150777b[failInfo=<null>,pkiStatus=SUCCESS,recipientNonce=Nonce [GUID],messageData=org.spongycastle.cms.CMSSignedData@27cc8998,messageType=CERT_REP,senderNonce=Nonce [GUID],transId=TRANSID]
2018-02-27T05:16:28.2440000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       10    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_ENROLLED to CERT_INSTALL_REQUESTED
2018-02-27T05:18:44.9820000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327        0    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALLING
2018-02-27T05:18:45.3460000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       14    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_INSTALLING to CERT_ACCESS_REQUESTED
2018-02-27T05:20:15.3520000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       21    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_ACCESS_REQUESTED to CERT_ACCESS_GRANTED
```

### iOS/iPadOS

On the iOS/iPadOS or iPadOS device, you can view the certificate under the Device Management Profile. Drill-in to see details for installed certificates.

![iOS certificate](../intune/protect/media/troubleshoot-scep-certificate-delivery/ios-certificate.png)

You can also find entries that resemble the following in the [iOS debug log](troubleshoot-scep-certificate-profiles.md#logs-for-ios-and-ipados-devices):

```
Debug 18:30:53.691033 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=SCEP%20Authority\  
Debug 18:30:54.640644 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=SCEP%20Authority\ 
Debug 18:30:55.487908 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=PKIOperation&message=MIAGCSqGSIb3DQEHAqCAMIACAQExDzANBglghkgBZQMEAgMFADCABgkqhkiG9w0BBwGggCSABIIZfzCABgkqhkiG9w0BBwOggDCAAgEAMYIBgjCCAX4CAQAwZjBPMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxHDAaBgoJkiaJk/IsZAEZFgxmb3VydGhjb2ZmZWUxGDAWBgNVBAMTD0ZvdXJ0aENvZmZlZSBDQQITaAAAAAmaneVjEPlcTwAAAAAACTANBgkqhkiG9w0BAQEFAASCAQCqfsOYpuBToerQLkw/tl4tH9E+97TBTjGQN9NCjSgb78fF6edY0pNDU+PH4RB356wv3rfZi5IiNrVu5Od4k6uK4w0582ZM2n8NJFRY7KWSNHsmTIWlo/Vcr4laAtq5rw+CygaYcefptcaamkjdLj07e/Uk4KsetGo7ztPVjSEFwfRIfKv474dLDmPqp0ZwEWRQG 
Debug 18:30:57.285730 -0500 profiled Adding dependent Microsoft.Profiles.MDM to parent www.windowsintune.com.SCEP.ModelName=AC_51bad41f.../LogicalName_1892fe4c...;Hash=-912418295 in domain ManagedProfileToManagingProfile to system\ 
Default 18:30:57.320616 -0500 profiled Profile \'93www.windowsintune.com.SCEP.ModelName=AC_51bad41f.../LogicalName_1892fe4c...;Hash=-912418295\'94 installed.\ 
```

### Windows

On the Windows device, verify the certificate was delivered:

- Run **eventvwr.msc** to open Event Viewer. Go to **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Admin** and look for **Event 39**. This Event should have a general description of: **SCEP: Certificate installed successfully.**

   ![Event 39 in the Windows Application log](../intune/protect/media/troubleshoot-scep-certificate-delivery/device-app-log.png)

To view the certificate on the device, run **certmgr.msc** to open the Certificates MMC and verify that the root and SCEP certificates are installed correctly on the device in the personal store:

   1. Go to **Certificates (local Computer)** > **Trusted Root Certification Authorities** > **Certificates**, and verify that the root certificate from your CA is present. The values for *Issued To* and *Issued By* will be the same.
   2. In the Certificates MMC, go to **Certificates – Current User** > **Personal** > **Certificates**, and verify the requested certificate is present, with *Issued By* equal to the name of the CA.

## Troubleshoot failures

### Android

To troubleshoot this step, review errors that are logged in the OMA DM log.

### iOS/iPadOS

To troubleshoot this step, review errors that are logged in the devices debug log.

### Windows

To troubleshoot issues with the certificate not being installed on the device, look in the Windows Event log for errors that suggest problems:

- On the device, run **eventvwr.msc** to open Event Viewer, and then go to **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **Admin**.

Errors with delivery and installation of the certificate to the device are typically related to Windows operations, and not to Intune.

## Next steps

When the certificate successfully deploys to the device, but Intune doesn't report success, see [NDES reporting to Intune](troubleshoot-scep-certificate-reporting.md) to troubleshoot reporting.
