---
title: "Certificate profile security and privacy"
titleSuffix: "Configuration Manager"
description: "Learn about the security best practices for managing certificate profiles for users and devices in Configuration Manager."
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby


---
# Security and privacy for certificate profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

##  Security Best Practices for Certificate Profiles  
 Use the following security best practices when you manage certificate profiles for users and devices.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Identify and follow any security best practices for the Network Device Enrollment Service, which includes configuring the Network Device Enrollment Service website in Internet Information Services (IIS) to require SSL and ignore client certificates.|For more information, see [Network Device Enrollment Service Guidance](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).|  
|When you configure SCEP certificate profiles, choose the most secure options that devices and your infrastructure can support.|Identify, implement, and follow any security best practices that have been recommended for your devices and infrastructure.|  
|Manually specify user device affinity instead of allowing users to identify their primary device. In addition, do not enable usage-based configuration.|If you click the **Allow certificate enrollment only on the users primary device** option in a SCEP certificate profile, do not consider the information that is collected from users or from the device to be authoritative. If you deploy SCEP certificate profiles with this configuration and a trusted administrative user does not specify user device affinity, unauthorized users might receive elevated privileges and be granted certificates for authentication.<br /><br /> **Note:** If you do enable usage-based configuration, this information is collected by using state messages that are not secured by Configuration Manager. To help mitigate this threat, use SMB signing or IPsec between client computers and the management point.|  
|Do not add Read and Enroll permissions for users to the certificate templates, or configure the certificate registration point to skip the certificate template check.|Although Configuration Manager supports the additional check if you add the security permissions of Read and Enroll for users, and you can configure the certificate registration point to skip this check if authentication is not possible, neither configuration is a security best practice. For more information, see [Planning for certificate template permissions for certificate profiles](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## Privacy Information for Certificate Profiles  
 You can use certificate profiles to deploy root certification authority (CA) and client certificates, and then evaluate whether those devices become compliant after the profiles are applied. The management point sends compliance information to the site server, and Configuration Manager stores that information in the site database. Compliance information includes certificate properties such as subject name and thumbprint. The information is encrypted when devices send it to the management point, but it is not stored in encrypted format in the site database. The database retains the information until the site maintenance task **Delete Aged Configuration Management Data** deletes it after the default interval of 90 days. You can configure the deletion interval. Compliance information is not sent to Microsoft.  

 Certificate profiles use information that Configuration Manager collects using discovery. For more information about privacy information for discovery, see the **Privacy Information for Discovery** section in [Security and privacy for Configuration Manager](../../security/index.yml).  

> [!NOTE]  
>  Certificates that are issued to users or devices might allow access to confidential information.  

 By default, devices do not evaluate certificate profiles. In addition, you must configure the certificate profiles, and then deploy them to users or devices.  

 Before you configure certificate profiles, consider your privacy requirements.