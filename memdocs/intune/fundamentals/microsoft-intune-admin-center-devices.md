---
# required metadata

title: Try new Devices experience in Microsoft Intune 
description: Walkthrough the new Devices workload, now in public preview in the Microsoft Intune admin center.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 3/20/2023
ms.topic: how-to
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

Enroll devices, manage profiles and policies, and access monitoring and reports all in one place in Microsoft Intune. Now in public preview, you can go to the **Devices** area in the Microsoft Intune admin center to:   

* Get at-a-glance actionable information and key metrics about your devices.  
* Access workloads for device onboarding, management, and monitoring.      
* View, monitor, and drill down into active issues on the Overview page. 
* Manage devices by OS platform. 
* Access, apply, and view filters at the top of every list view.  

This article describes how to opt in to the public preview and access updated workloads, including:    

* **Devices** > **Overview**
* **Devices** > **All devices**  
* **Devices** > **Configuration**
* **Devices** > **Compliance** 
* **Devices** > **Windows 10 and later updates**  
* **Devices** > **Apple updates**  
* **Devices** > **Enrollment**  

## Opt in to public preview   
You can switch back and forth between the current UI and public preview without impacting other admins in your tenant.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices**. 
3. On the **Overview** page, select the notification banner that says **Preview upcoming changes to Devices and provide feedback**.  
4. The **Devices preview** page opens. Select **Try it now** to opt in.   

You remain in public preview until you switch it back, even if you close the browser. To exit public preview and return to the current version of the admin center:  

1. Go to **Overview**. 
2. Flip the switch next to **Use Devices preview**. Wait while Intune refreshes the UI.  
3. Optionally, when prompted, provide feedback about your experience with the Devices public preview. Select **x** to return to the admin center without giving feedback.       

## Overview         
Go to **Devices** > **Overview** to access workloads by OS platform, view key metrics about assigned policies, and access associated reports.  *Overview* contains at-a-glance metrics that highlight active issues, such as enrollment failures and Windows 365 provisioning failures, happening across devices. Select a metric for more information about an active issue.   

* **Manage devices by platform**: Select an OS platform to pivot between management workloads by platform.  
* **Additional monitoring reports**: Access reports associated with your key metrics.  
* **Other devices**: Access other device workloads, such as configuration for the Chrome OS enterprise connector.  

You can also get 

## All devices  
Select **Devices** > **All devices** to view a list of all Intune-managed devices in your tenant. Select a device to get more granular information about it, such as:   

* Hardware details  
* Installed apps  
* Assigned policies  
* Available remote actions  

You can use the **Export** feature to create a .zip list of all the devices, in increments of 10,000 (Internet Explorer) or 30,000 (Microsoft Edge, Chrome). For more information about device details, see [See device details in Intune](../remote-actions/device-inventory.md).   

## Device onboarding  
Under **Device onboarding**, you can access these onboarding options (workloads with UI changes are marked as *New*):   

* **Cloud PC creation**  
* **Enrollment** - *New*  

Select **Enrollment** to access these subworkloads:  

* **Monitor**: Access reports and list views associated with enrollment profiles, policies, and Windows Autopilot deployment. 
* **Windows**: Set up enrollment for devices running Windows 10 or Windows 11.    
* **Apple**: Set up enrollment for iOS/iPadOS and Mac devices.  
* **Android**: Set up enrollment for supported Android devices.     
* **Corporate device identifiers**: Add and manage corporate identifiers for devices that should have corporate-owned status.  
* **Device enrollment manager**: Add and manage device enrollment managers that oversee or help with enrolling devices.            

For more information about corporate identifiers, see [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md).  

## Manage devices    
Under **Manage devices**, you can access your most essential management workloads, including (workloads with UI changes are marked as *New*):           

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

Monitored data and relevant reports are located in the same place as your management tasks to help you find and act on issues quickly. This section describes the public preview experience for all updated workloads.  

### Configuration workload  
Select **Devices** > **Configuration** to monitor and manage device configuration policies in Microsoft Intune. Within Configuration, you can access the following subworkloads: 

* **Monitor**: Access reports and list views associated with device configuration profiles.          
* **Policies**: Create, view and edit device configuration policies.      
* **Import ADMX**: Import custom and partner ADMX and ADML templates that you can create device configuration policies from.   

For more information about device configuration, see [Apply features settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).  

### Compliance workload   
Select **Devices** > **Compliance** to monitor and manage device compliance policies in Microsoft Intune. This workload is made up of the following subworkloads:  

* **Monitor**: Access key metrics, reports, and list views associated with device compliance.          
* **Policies**: Create, view and edit device compliance policies.
* **Notifications**: Create and send custom notifications to device users on managed iOS/iPadOS and Android devices.  
* **Retire noncompliant devies**: Remove all company data from a device and remove the device from Intune management. 
* **Compliance settings**: Configure compliance policy settings such as enhanced jailbreak detection and compliance status validity period.      
* **Scripts**: Add and manage scripts used for custom compliance settings.   

For more information about device compliance, see [Compliance overview](../protect/device-compliance-get-started.md).  

### Windows 10 and later updates
Select **Devices** > **Windows 10 and later updates** to monitor and manage software update policies for devices running Windows 10 or Windows 11. This workload is made up of the following subworkloads:

* **Monitor**: Access key metrics and active issues associated with Windows software update policies.             
* **Update rings**: Create and manage update ring policies for Windows 10 and Windows 11.    
* **Feature updates**: Create and manage policies for Windows 10 and Windows 11 feature updates.   
* **Quality updates**: Create and manage policies for Windows 10 and Windows 11 quality updates.  
* **Driver updates**: Create and manage policies for Windows 10 and Windows 11 driver updates.    

For more information about Windows updates, see [Manage Windows 10 and Windows 11 software updates in Intune](../protect/windows-update-for-business-configure.md).   


### Apple updates   
Select **Devices** > **Apple updates** to monitor and manage software update policies for Apple devices. This workload is made up of the following subworkloads:

* **Monitor**: Access key metrics and active issues associated with Apple update policies.            
* **iOS/iPadOS updates**: Create and manage policies for iOS/iPadOS updates.      
* **macOS updates**: Create and manage policies for macOS updates.   

For more information about Windows updates, see [Manage Windows 10 and Windows 11 software updates in Intune](../protect/windows-update-for-business-configure.md).   

## Next steps  

For an overview of new features and features that are ready to try in public preview, see [What's New in Microsoft Intune](../fundamentals/whats-new.md).    
