---
title: Device compliance policies
titleSuffix: "Configuration Manager"
description: "Learn how to manage compliance policies in System Center Configuration Manager to make devices compliant with conditional access polices."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: 18
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
---
# Device compliance policies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

**Compliance policies** in System Center Configuration Manager define the rules and settings that a device must comply with in order to be considered compliant by conditional access polices. You can also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access.  


> [!IMPORTANT]  
>  This article describes the compliance policies for devices managed by Microsoft Intune.    The compliance policies for PCs managed by System Center Configuration Manager is described in [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

 These rules include requirements like:  

-   PIN and passwords to access a device

-   Encryption of data stored on the device

-   Whether the device is jailbroken or rooted  

-   Whether email on the device is managed by an Intune policy, or if the device is reported as unhealthy by the Windows device health attestation service.
-   Apps that cannot be installed on the device.


 You deploy compliance policies to user collections. When a compliance policy is deployed to a user, then all of the users devices are checked for compliance.  

 The following table lists the device types supported by compliance policies and how noncompliant settings are managed when the policy is used with a conditional access policy.  

|Rule|Windows 8.1 and later|Windows Phone 8.1 and later|iOS 6.0 and later|Android 4.0 and later Samsung KNOX Standard 4.0 and later, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN or password configuration**|Remediated|Remediated|Remediated|Quarantined|  
|**Device encryption**|N/A|Remediated|Remediated (by setting PIN)|Quarantined<br>(Android for Work always encrypted)|  
|**Jailbroken or rooted device**|N/A|N/A|Quarantined (not a setting)|Quarantined (not a setting)|  
|**Email profile**|N/A|N/A|Quarantined|N/A|  
|**Minimum OS version**|Quarantined|Quarantined|Quarantined|Quarantined|  
|**Maximum OS version**|Quarantined|Quarantined|Quarantined|Quarantined|  
|**Device Health Attestation (1602 update)**|Setting is not applicable to Windows 8.1<br /><br /> Windows 10 and Windows 10 Mobile are Quarantined.|N/A|N/A|N/A|  
|**Apps that cannot be installed**|N/A|N/A|Quarantined|Quarantined|

 **Remediated** = Compliance is enforced by the device operating system (for example, the user is forced to set a PIN).  There is never a case when the setting will be noncompliant.  

 **Quarantined** = The device operating system does not enforce compliance (for example, Android devices do not force the user to encrypt the device).  In this case:  

-   The device will be blocked if the user is targeted by a conditional access policy.  

-   The company portal or web portal will notify the user about any compliance issues.  


### Next Steps  
[Create and deploy a device compliance policy](create-compliance-policy.md)
### See also  
 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
