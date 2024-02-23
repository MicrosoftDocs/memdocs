---
title: Troubleshoot Microsoft Intune cloud PKI  
titleSuffix: Microsoft Intune 
description: Troubleshoot Microsoft Intune cloud PKI in Intune.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/26/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: wicale  
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier1
- M365-identity-device-management
- certificates
---
# Troubleshooting for Microsoft Cloud PKI  
This article gives troubleshooting guidance for common issues that occur when deploying the Microsoft Cloud PKI service in Microsoft Intune. 

## Check SCEP certificate profile is using the correct root CA trusted certificate profile   
Troubleshoot a device that's not receiving a SCEP certificate.  
1. Go to **Devices** > **All devices**.
1. Select the device not getting the certificate. 
1. Go to **Monitor** > **Device configuration**.
1. Find the the assigned SCEP profile with the error and then: 
    * Make sure the SCEP profile is using the Trusted certificate that has the root certificate of the trust chain for the Issuing CA.  For more information , see [Create a SCEP certificate profile]().  
    * Make sure the trusted certificate profile linked in the SCEP profile is assigned to the same Microsoft Entra group as the SCEP profile.  

1. The file type appears on Windows machines as a *PKCS #7 Certificate*. Open the file.  You will see 3 certificates: the Cloud PKI Root CA certificate, the Cloud PKI Issuing CA certificate, and the SCEP Registration Authority certificate. 
1. Check that the SCEP URI is available and active, and responding to the `GetCACaps` and `GetCACaps` SCEP protocol commands.     

## Confirm Intune managed device has network access to the SCEP URI  
Confirm a device has network access to the SCEP URI endpoint.  The following steps must be done in a web browser, on the device targeted to receive a SCEP profile.  

1. Open any browser on the managed device and go to the SCEP URI for the Cloud PKI issuing CA the SCEP certificate profile is using.

1. If a test device requires the use of an outbound proxy to reach the internet, provide this information. Ensure the test device can access the SCEP URI in the SCEP profile.  

1. Enter the SCEP profile URI in a web browser. Append the protocol command `“?operation=GetCACaps` to the end of the SCEP profile URI, as shown in the following example:     

    `https://fef.msua04.manage.microsoft.com/CloudPki/CloudPkiFEService/Scep/b3db7b19-f980-44f3-8a65-d3f64ae5941a/f09b0fe8-c7b9-45f2-8491-19edc5b13cb6?operation=GetCACaps`






