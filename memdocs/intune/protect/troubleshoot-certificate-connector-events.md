---
title: Troubleshoot the Microsoft Intune certificate connector and event IDs  | Microsoft Docs
titleSuffix: Microsoft Intune
description:  Troubleshoot the Microsoft Intune certificate connector by reviewing Event IDs and descriptions, and review diagnostic codes for the Intune connector service.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
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



# Intune Certificate Connector events and diagnostic codes

Starting with version 6.1806.x.x, the Intune Connector Service logs events in the **Event Viewer** (**Applications and Services Logs** > **Microsoft Intune Connector**). Use these events to help troubleshoot potential issues in the configuration of the Intune Connector. These events log successes and failures of an operation, and also contain diagnostic codes with messages to help the IT admin troubleshoot.

> [!TIP]  
> To troubleshoot issues and verify the Intune Connector setup, see [Certificate Authority script samples](https://aka.ms/intuneconnectorverificationscript).

## Event IDs and descriptions

| Event ID      | Event Name    | Event Description | Related Diagnostic Codes |
| ------------- | ------------- | -------------     | -------------            |
| 10010 | StartedConnectorService  | Connector service started | 0x00000000, 0x0FFFFFFF |
| 10020 | StoppedConnectorService  | Connector service stopped | 0x00000000, 0x0FFFFFFF |
| 10100 | CertificateRenewal_Success  | Connector enrollment certificate successfully renewed | 0x00000000, 0x0FFFFFFF |
| 10102 | CertificateRenewal_Failure  | Connector enrollment certificate failed to renew. Reinstall the connector. | 0x00000000, 0x00000405, 0x0FFFFFFF |
| 10302 | RetrieveCertificate_Error  | Failed to retrieve the connector enrollment certificate from the registry. Review event details for the certificate thumbprint related to this event. | 0x00000000, 0x00000404, 0x0FFFFFFF |
| 10301 | RetrieveCertificate_Warning  | Check diagnostic information in event details. | 0x00000000, 0x00000403, 0x0FFFFFFF |
| 20100 | PkcsCertIssue_Success  | Successfully issued a PKCS certificate. Review event details for the device ID, user ID, CA name, certificate template name, and certificate thumbprint related to this event. | 0x00000000, 0x0FFFFFFF |
| 20102 | PkcsCertIssue_Failure  | Failed to issue a PKCS certificate. Review event details for the device ID, user ID, CA name, certificate template name, and certificate thumbprint related to this event. | 0x00000000, 0x00000400, 0x00000401, 0x0FFFFFFF |
| 20200 | RevokeCert_Success  | Successfully revoked the certificate. Review event details for the device ID, user ID, CA name, and certificate serial number related to this event. | 0x00000000, 0x0FFFFFFF |
| 20202 | RevokeCert_Failure | Failed to revoke the certificate. Review event details for the device ID, user ID, CA name, and certificate serial number related to this event. For additional information, see the NDES SVC Logs.   | 0x00000000, 0x00000402, 0x0FFFFFFF |
| 20300 | Upload_Success | Successfully uploaded the certificate's request or revocation data. Review the event details for the upload details. | 0x00000000, 0x0FFFFFFF |
| 20302 | Upload_Failure | Failed to upload the certificate's request or revocation data. Review the event details > Upload State to determine the point of failure.| 0x00000000, 0x0FFFFFFF |
| 20400 | Download_Success | Successfully downloaded request to sign a certificate, download a client certificate, or revoke a certificate. Review the event details for the download details.  | 0x00000000, 0x0FFFFFFF |
| 20402 | Download_Failure | Failed to download request to sign a certificate, download client certificate, or revoke a certificate. Review the event details for the download details. | 0x00000000, 0x0FFFFFFF |
| 20500 | CRPVerifyMetric_Success  | Certificate Registration Point successfully verified a client challenge | 0x00000000, 0x0FFFFFFF |
| 20501 | CRPVerifyMetric_Warning  | Certificate Registration Point completed but rejected the request. See diagnostic code and message for more details. | 0x00000000, 0x00000411, 0x0FFFFFFF |
| 20502 | CRPVerifyMetric_Failure  | Certificate Registration Point failed to verify a client challenge. See diagnostic code and message for more details. See event message details for the Device ID corresponding to the challenge. | 0x00000000, 0x00000408, 0x00000409, 0x00000410, 0x0FFFFFFF |
| 20600 | CRPNotifyMetric_Success  | Certificate Registration Point successfully finished notify process and has sent the certificate to the client device. | 0x00000000, 0x0FFFFFFF |
| 20602 | CRPNotifyMetric_Failure  | Certificate Registration Point failed to finish notify process. See the event message details for information on the request. Verify connection between the NDES server and the CA. | 0x00000000, 0x0FFFFFFF |

## Diagnostic codes

| Diagnostic Code | Diagnostic Name | Diagnostic Message |
| -------------   | -------------   | -------------      |
| 0x00000000 | Success  | Success |
| 0x00000400 | PKCS_Issue_CA_Unavailable  | Certification authority is not valid or is unreachable. Verify that the certification authority is available, and that your server can communicate with it. |
| 0x00000401 | Symantec_ClientAuthCertNotFound  | Symantec Client Auth certificate was not found in the local cert store. See the article [Install the Symantec registration authorization certificate](certificates-digicert-configure.md#install-the-digicert-ra-certificate) for more information.  |
| 0x00000402 | RevokeCert_AccessDenied  | The specified account does not have permissions to revoke a certificate from CA. See CA Name field in the event message details to determine the issuing CA.  |
| 0x00000403 | CertThumbprint_NotFound  | Could not find a certificate that matched your input. Enroll the certificate connector and try again. |
| 0x00000404 | Certificate_NotFound  | Could not find a certificate that matched the input supplied. Re-enroll the certificate connector and try again. |
| 0x00000405 | Certificate_Expired  | A certificate expired. Re-enroll the certificate connector to renew the certificate and try again. |
| 0x00000408 | CRPSCEPCert_NotFound  | CRP Encryption certificate could not be found. Verify that NDES and the Intune Connector is setup correctly. |
| 0x00000409 | CRPSCEPSigningCert_NotFound  | Signing certificate could not be retrieved. Verify the Intune Connector Service is configured correctly, and the Intune Connector Service is running. Verify also that the certificate download events were successful. |
| 0x00000410 | CRPSCEPDeserialize_Failed  | Failed to deserialize SCEP challenge request. Verify the NDES and Intune Connector is setup correctly. |
| 0x00000411 | CRPSCEPChallenge_Expired  | Request denied due to expired certificate challenge. The client device can retry after obtaining a new challenge from the management server. |
| 0x0FFFFFFFF | Unknown_Error  | We are unable to complete your request because a server-side error occurred. Please try again. |


## Next steps
For additional assistance, use the [Troubleshooting SCEP certificate profile deployment in Microsoft Intune](https://support.microsoft.com/help/4457481/troubleshooting-scep-certificate-profile-deployment-in-intune) guide.
