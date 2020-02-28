---
# required metadata

title: Troubleshoot the reporting of successful certificate deployment to devices when you use SCEP with Microsoft Intune | Microsoft Docs
description: Troubleshoot the reporting by NDES and the connector to Intune about a successful deployment of certificates that were provisioned with SCEP certificate profiles. 
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

# Troubleshoot NDES reporting of certificate deployments in Microsoft Intune

Use the following information to confirm that NDES and the Microsoft Intune Certificate Connector successfully report to Intune that the certificate was delivered to a device. Reporting to Intune is the last phase for using SCEP certificate profiles to provision Windows devices with a certificate.

This article applies to the step 6 of the [SCEP communication workflow](troubleshoot-scep-certificate-profiles.md).

## Review for signs of successful reporting

If reporting was successful, you'll find entries that resemble the following examples on the NDES server:

- **IIS log**:

  `fe80::f53d:89b8:c3e8:5fec%13 POST /CertificateRegistrationSvc/Certificate/Notify - 443 - fe80::f53d:89b8:c3e8:5fec%13 NDES_Plugin - 204 0 0 277 62`

- **NDESPlugin.log**:

  ```
  Calling Notifyrequest ...
  Sending request to certificate registration point.
  Exiting Notify with 0x0
  ```

- **CertificateRegistrationPoint.svclog**:

  ![Intune Certificate Connector log](../protect/media/troubleshoot-scep-certificate-reporting/certificate-registration-point-log.png)

- **NDESConnector.svclog**:

  ![Intune Certificate Connector log](../protect/media/troubleshoot-scep-certificate-reporting/ndesconnector-log.png)

- **CertificateRequestStatus**:

  Go to the *%ProgramFiles%\Microsoft Intune\CertificateRequestStatus* folder where you'll see the **Failed**, **Processing**, and **Succeed** folders that contain certificate request status files.

  If the certificate request is successfully processed, you'll see new files in the **Succeed** folder. You can use *Notepad.exe* to open the files and view the data that's uploaded to the Intune Service by the Intune Certificate Connector. Data that uploaded includes details like **CertificateSerialNumber**, **UserID**, **DeviceID**, and **Thumbprint**.

### Troubleshoot stuck files

If you don’t see any new files being created in the *Succeed* folder, check whether there are any files stuck in the *Processing* folder.

Verify that the Intune Connector Service is started on the NDES server, and there are no errors in Ndesconnector.svclog.

## Next steps

[How to get support for Microsoft Intune](../fundamentals/get-support.md)
