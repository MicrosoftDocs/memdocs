---
# required metadata

title: Walk through new Devices experience in Microsoft Intune
description: Walkthrough the new Devices workload, now in public preview, in the Microsoft Intune admin center.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 3/20/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: 
ms.localizationpriority: med

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Try new Devices experience in Microsoft Intune        

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Enroll devices, manage profiles and policies, and access monitoring and reports all in one place in the **Devices** area in Microsoft Intune. From the **Devices** area, you can:  

* Get at-a-glance actionable information and key metrics about your devices.  
* Access workloads for device onboarding, management, and monitoring.      
* View, monitor, and drill down into active issues on the Overview page. 
* Manage devices by OS platform. 
* Access, apply, and view filters at the top of every list view.  

This article describes how to opt in to the public preview, and also describes these updated areas: 

* Devices > Overview
* Devices > All devices  
* Devices > Configuration
* Devices > Compliance 
* Devices > Windows 10 and later updates  
* Devices > Apple updates  
* Devices > Enrollment  

## Opt in to public preview   
You can switch back and forth between the current UI and public preview without impacting other admins in your tenant.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices**. 
3. On the **Overview** page, select the **Devices preview** notification: **Preview upcoming changes to Devices and provide feedback**. 
4. The **Devices preview** page opens. Select **Try it now** to opt in.   

You remain in public preview until you switch it back, even if you close the browser.To exit public preview and return to the current version of the admin center:  

1. Go to **Overview**. 
2. Flip the **Use Devices preview** switch. Wait while Intune refreshes the UI.  
3. Optionally, when prompted, provide feedback about your experience with the Devices public preview. Select **x** to return to the admin center without giving feedback.      

## Overview         
Go to **Devices** > **Overview** to access workloads by OS platform, view key metrics about assigned policies, and access associated reports.  

Overview contains:  

* **Manage devices by platform**: Select an OS platform to pivot between management workloads by platform.
* Key metrics: Get at-a-glance metrics such as configuration profile status, device compliance status, and Windows 10 update ring status.  
* **Additional monitoring reports**: Access reports associated with your key metrics.  
* **Other devices**: Access other device workloads, such as configuration for the Chrome OS enterprise connector.  

## All devices  
Select **Devices** > **All devices** to view a list of all Intune-managed devices in your tenant. Within this area, you can select a device to see more details and access remote actions. Use the **Export** feature to create a .zip list of all the devices, in increments of 10,000 (Internet Explorer) or 30,000 (Microsoft Edge, Chrome).  

Select a device to view more details about it, such as:  
* Hardware details  
* Installed apps  
* Assigned policies  
* Available remote actions  

For more information about device details, see [See device details in Intune](../remote-actions/device-inventory.md).   

## Device onboarding  
Under **Device onboarding**, you can access these onboarding options for Microsoft Intune (workloads with UI changes are marked as *New*):

* **Windows 365**  
* **Enrollment** - *New* 

Within Enrollment, you can access the following subworkloads: 

* **Monitor**: Access reports and list views associated with enrollment profiles, policies, and Windows Autopilot deployment. 
* **Windows**: Set up enrollment for devices running Windows 10 or Windows 11.    
* **Apple**: Set up enrollment for iOS/iPadOS and Mac devices.  
* **Android**: Set up enrollment for supported Android devices.     
* **Corporate device identifiers**: 
* **Device enrollment manager**: Add and manage device enrollment managers that oversee or help with enrolling devices.            

For more information about device enrollment, see [Enrollment guide: Microsoft Intune enrollment](../fundamentals/deployment-guide-enrollment.md).  

## Manage devices    
Under **Manage devices**, you can access your most essential management workloads. Monitored data and relevant reports are now located in the same place as your management tasks to help you find and act on issues quickly. The following workloads are available in public preview (workloads with UI changes are marked as *New*):         

* **Windows 365 provisioning**     
* **Configuration** - *New* 
* **Compliance** - *New* 
* **Conditional access**
* **Scripts**
* **Windows 10 and later updates** - *New*   
* **Apple updates** - *New*  
* **Group Policy analytics (preview)**  
* **eSIM cellular profiles (preview)**  
* **Policy sets**  
* **Device clean-up rules**  
* **Device categories**  
* **Partner portals**   

This section describes the public preview experience for all updated workloads.  

### Configuration 
Select **Devices** > **Configuration** to monitor and manage device configuration policies in Microsoft Intune. Within Configuration, you can access the following subworkloads: 

* **Monitor**: Access reports and list views associated with device configuration profiles.          
* **Policies**: Create, view and edit device configuration policies.      
* **Import ADMX**: Import custom and partner ADMX and ADML templates that you can create device configuration policies from.   

For more information about device configuration, see [Apply features settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md). 

### Compliance  
Select **Devices** > **Compliance** to monitor and manage device compliance policies in Microsoft Intune. This workload is made up of the following subworkloads:

* **Monitor**: Access reports and list views associated with device compliance.          
* **Policies**: Create, view and edit device compliance policies.
* **Notifications**: Create and send custom notifications to device users on managed iOS/iPadOS and Android devices.  
* **Retire noncompliant devies**: Remove all company data from a device and remove the device from Intune management. 
* **Compliance settings**: Configure compliance policy settings such as enhanced jailbreak detection and compliance status validity period.      
* **Scripts**: Add and manage scripts used for custom compliance settings.   

For more information about device compliance, see [Compliance overview](../protect/device-compliance-get-started.md). 

## Next steps  

For more information about this public preview feature, see:

* [What's New in Microsoft Intune](../fundamentals/whats-new.md#week-of-march-20-2023)  
* [Support blog for new Microsoft Intune Devices experience]() 
