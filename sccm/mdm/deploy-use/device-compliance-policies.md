---
title: Device compliance policies
titleSuffix: Configuration Manager
description: Learn how to manage compliance policies in Configuration Manager to make devices compliant with conditional access polices.
ms.date: 07/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Device compliance policies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Compliance policies in Configuration Manager define the rules and settings that a device must comply with in order to be considered compliant by conditional access policies. You can also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access.  


> [!IMPORTANT]  
>  This article describes the compliance policies for devices managed by Microsoft Intune. The compliance policies for devices managed by the Configuration Manager client is described in [Manage access to O365 services for devices managed by Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 These rules include requirements like:  

-   PIN and passwords to access a device  

-   Encryption of data stored on the device  

-   Whether the device is jailbroken or rooted  

-   Whether email on the device is managed by an Intune policy, or if the device is reported as unhealthy by the Windows device health attestation service.  

-   Apps that can't be installed on the device.  


 You deploy compliance policies to user collections. When a compliance policy is deployed to a user, then all of the users devices are checked for compliance.  



## Supported device types

 The following table lists the device types supported by compliance policies and how non-compliant settings are managed when the policy is used with a conditional access policy.  

|Rule|Windows 8.1 and later|Windows Phone 8.1 and later|iOS 6.0 and later|Android 4.0 and later Samsung KNOX Standard 4.0 and later, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN or password configuration**|Remediated|Remediated|Remediated|Quarantined|  
|**Device encryption**|N/A|Remediated|Remediated (by setting PIN)|Quarantined<br>(Android for Work always encrypted)|  
|**Jailbroken or rooted device**|N/A|N/A|Quarantined (not a setting)|Quarantined (not a setting)|  
|**Email profile**|N/A|N/A|Quarantined|N/A|  
|**Minimum OS version**|Quarantined|Quarantined|Quarantined|Quarantined|  
|**Maximum OS version**|Quarantined|Quarantined|Quarantined|Quarantined|  
|**Device Health Attestation (1602 update)**|Setting isn't applicable to Windows 8.1<br /><br /> Windows 10 and Windows 10 Mobile are Quarantined.|N/A|N/A|N/A|  
|**Apps that cannot be installed**|N/A|N/A|Quarantined|Quarantined|

 **Remediated** = Compliance is enforced by the device OS. For example, the user is forced to set a PIN. There's never a case when the setting is non-compliant.  

 **Quarantined** = The device OS doesn't enforce compliance. For example, Android devices don't force the user to encrypt the device. In this case:  

-   If the user is targeted by a conditional access policy, the device is blocked.  

-   The company portal or web portal notifies the user about any compliance issues.  



## Devices without any assigned compliance policy
<!--2520152-->
Starting in July 2018, configure whether all devices that have no assigned compliance policy are considered compliant or non-compliant. By default, devices with no assigned compliance policy are considered compliant. Use the following steps to change this setting in the Azure portal:

1. Sign in to the [Intune on Azure portal](https://aka.ms/intuneportal).  

2. Select **Device compliance**, and then select **Compliance policy settings** in the Setup group.  

3. For the setting **Mark devices with no compliance policy assigned as**, select one of the following options:  

     - **Compliant** (default) - Devices with no assigned compliance policy are considered compliant with policy. If conditional access is enabled, these devices have access to internal resources.  

     - **Not Compliant** - Devices with no assigned compliance policy are considered not compliant with policy. If conditional access is enabled, these devices are blocked from internal resources, per the conditions in the conditional access policy.  

4. Click Save.  

We strongly recommend that you deploy at least one compliance policy for each platform to all users in your environment. Then configure this setting to **Not Compliant** in order to ensure the security of your internal resources. For more information, see the [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) blog post.



## Next Steps  
[Create and deploy a device compliance policy](/sccm/mdm/deploy-use/create-compliance-policy)

### See also  
 [Manage access to services in Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)