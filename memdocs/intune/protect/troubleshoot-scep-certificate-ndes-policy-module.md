---
# required metadata

title: Troubleshoot the Microsoft Intune Certificate Connector policy module | Microsoft Docs
description: Troubleshoot the operation of the NDES policy module when the module processes a certificate request when you use SCEP certificate profiles to deploy certificates with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/30/2020
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

# Troubleshoot the NDES policy module in Microsoft Intune

The information in this article can help you validate operation of the Network Device Enrollment Service (NDES) policy module that installs with the Microsoft Intune Certificate Connector. When NDES receives a request for a certificate, it forwards the request to the policy module, which validates the request as valid for the device. After the validation, NDES contacts the certificate authority (CA) to request the certificate on behalf of the device.

This article applies to both step 3 and step 4 of [SCEP communication workflow](troubleshoot-scep-certificate-profiles.md).

## NDES communication to the policy module

After receiving the certificate request from a device, NDES validates that request with Intune through the policy module that installs with the Microsoft Intune Certificate Connector. These entries refer to the *certificate registration point*.

**Log entries that indicate success**:

To confirm the validation request is submitted to the module, look for an entry that resembles the following examples in logs on the NDES server:

- **IIS logs**:

  ```
  fe80::f53d:89b8:c3e8:5fec%13 POST /CertificateRegistrationSvc/Certificate/VerifyRequest - 443 - 
  fe80::f53d:89b8:c3e8:5fec%13 NDES_Plugin - 201 0 0 341 875
  ```

- **NDESPlugin log**:

  ```
  Calling VerifyRequest ...  
  Sending request to certificate registration point.
  ```

  The following example indicates a successful validation of the devices challenge request and that NDES can now contact the CA:

  ```
  Verify challenge returns true
  Exiting VerifyRequest with 0x0
  ```

- **CertificateRegistrationPoint.svclog**:

  `Validation Phase 1 finished with status True.`  
  `Validation Phase 3 finished with status True.`  
  `VerifyRequest Finished with status True`


**When success indicators aren't present**:

If you don't find these entries, start by reviewing the troubleshooting guidance for [device to NDES server communication](troubleshoot-scep-certificate-device-to-ndes.md#troubleshoot-common-errors).

If the information in that article doesn't help you resolve the issue, the following are additional entries that can indicate problems.

### NDESPlugin.log contains an error 12175

When the log contains an error 12175 that's similar to the following, there might be a problem with the SSL certificate:

```
WINHTTP_CALLBACK_STATUS_FLAG_CERT_CN_INVALID
Failed to send http request /CertificateRegistrationSvc/Certificate/VerifyRequest. Error 12175
```

Modern browsers and browsers on mobile devices ignore the *Common Name* on an SSL certificate if there are *Subject Alternative Names* present.

**Resolution**:  Issue the web server SSL certificate with the following attributes for *Common Name* and *Subject Alternative Name*, and then bind it to port 443 in IIS:

  - **Subject name**  
    CN = external server name
  - **Subject Alternative Name**  
     Name = external server name  
     DNS Name = internal server name

### NDESPlugin.log contains an error 403 – Forbidden: Access is denied"

When the following logs contain an error 403 that's similar to the following, the client certificate might be untrusted or invalid:

**NDESPlugin.log**:

```
Sending request to certificate registration point.
Verify challenge returns <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> <html xmlns="http://www.w3.org/1999/xhtml"> <head><meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"/>
<title>403 - Forbidden: Access is denied.</title>
```

**IIS log**:

```
POST /CertificateRegistrationSvc/Certificate/VerifyRequest - 443 -<IP_address>
NDES_Plugin - 403 16 2148204809 453  
```

This issue occurs if there are intermediate CA certificates in the NDES server's Trusted Root Certification Authorities certificate store.

If a certificate has the same *Issued to* and *Issued by* values, it's a root certificate. Otherwise, it's an intermediate certificate.

**Resolution**: To fix the issue, identify and remove the intermediate CA certificates from the Trusted Root Certification Authorities certificate store.

### NDESPlugin.log indicates the challenge returns false

When the result of the challenge returns **false**, check the *CertificateRegistrationPoint.svclog* for errors. For example, you might see a "Signing certificate could not be retrieved" error that resembles the following entry:

```
Signing certificate could not be retrieved. System.Security.Cryptography.CryptographicException: m_safeCertContext is an invalid handle. at System.Security.Cryptography.X509Certificates.X509Certificate.ThrowIfContextInvalid() at System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString() at Microsoft.ConfigurationManager.CertRegPoint.CRPCertificate.RetrieveSigningCert(String certThumbprint
```

**Resolution**: On the server where the connector is installed, open the Registry Editor, locate the `HKLM\SOFTWARE\Microsoft\MicrosoftIntune\NDESConnector` registry key, and then check whether the SigningCertificate value exists.

If this value doesn't exist, restart the Intune Connector Service in services.msc, and then check whether the value appears in registry. If the value is still missing, it's often because of network connectivity issues between the server that NDES and the Intune service.

## NDES passes the request to issue the certificate

After a successful validation by the certificate registration point (the policy module), NDES passes the certificate request to the CA on behalf of the device.

**Log entries that indicate success**:

- **NDESPlugin log**:

  ```
  Verify challenge returns true
  Exiting VerifyRequest with 0x0
  ```

- **IIS logs**:

  ```
  fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe ... 80 - 
  fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 2713 1296
  ```

- **CertificateRegistrationPoint.svclog**:

  `Validation Phase 1 finished with status True.`  
  `Validation Phase 3 finished with status True.`  
  `VerifyRequest Finished with status True`

**When success indicators aren't present**:

If you don't see the entries that indicate success, follow these steps:

1. Look for problems that are logged in *CertificateRegistrationPoint.svclog* when the certificate registration point verifies the challenge. Look for the entries between the following lines:

   - VerifyRequest Started.
   - VerifyRequest Finished with status False

2. Open the Certification Authority MMC on the CA, and select **Failed Requests** to look for errors that help identify a problem. The following image is an example:

   ![Example of a failed request](../protect/media/troubleshoot-scep-certificate-ndes-policy-module/failed-requests.png)

3. Review the application event log on the CA for errors. Usually you can see errors that match what you see in the **Failed Requests** from the previous step. The following image is an example:

   ![Review the application log](../protect/media/troubleshoot-scep-certificate-ndes-policy-module/application-log-errors.png)

## Next steps

If the NDES policy module validates the request and the request is forwarded to the certificate authority, the next step is to review the [certificate delivery to the device](troubleshoot-scep-certificate-delivery.md).
