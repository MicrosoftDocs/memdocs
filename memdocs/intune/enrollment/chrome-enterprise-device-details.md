---
# required metadata

title: View Chrome OS device information | Microsoft Intune  
description: View Chrome OS devices and details synced with the Chrome Enterprise connector.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/26/2022  
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shsivak
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# View Chrome OS device information in Intune    

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).   

View details about your Chrome Enterprise connector and Chrome OS devices in the Microsoft Intune admin center. Information becomes available after:  

* You establish the connection between Google Admin console and Microsoft Intune.
* The initial device sync finishes. 
* The status in the admin center shows as **Active**.   

You can view synced devices in the **Devices** > **All devices** list and throughout the admin center where Intune-managed devices are shown. This article describes the information available, which you can use for monitoring or reporting, and where to find it in the admin center.  

## Prerequisites  

To view Chrome OS devices and device details, you must be assigned a role that has read permission for *Chrome Enterprise (preview)*.  

Devices must be enrolled before you can see them in the admin center. Enrollment for Chrome OS devices is done in the Google Admin center. You can create the connection before or after you enroll devices. For more information, see [Enroll ChromeOS devices](https://support.google.com/chrome/a/answer/1360534) (opens Chrome Enterprise and Education Help).

## View Chrome OS devices  
Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Devices** > **All devices** to view an aggregated list of all devices in Intune, including those running Chrome OS.  The following information is shown for Chrome OS devices: 

* **Device name**: Device names for Chrome OS devices appear as `Chrome- {serialNumber}`. 
* **Managed by**: Chrome OS devices are managed by **Intune**. 
* **Ownership**: Chrome OS devices are always marked as **Corporate**.  
* **Compliance**: Compliance policies are not supported with Chrome OS devices in Intune so they'll appear in this column as **Not evaluated**.  

Select **Filter** to filter the device list by platform. You can also go to the navigation menu and select **Chrome OS (preview)** for an exclusive view of Chrome OS devices.    

## View Chrome OS device details  
Directly select a device to view more details about it. The device's **Overview** page shows the device name, and lists key properties of the device, such as ownership, serial number, primary user, and device model. 

You can also view properties and system info for a device, as described in the following sections.  

### Properties  
Select **Properties** to view management information about the device. 

The following properties sync back to the Google Admin console:. Any changes made to these properties in Intune also show up in the Google Admin console.  

* Management name, known in Google Admin as the *asset ID*      
* User  
* Location  
* Notes  
### System info  
Select **System info** to see a real-time snapshot of the information available from the Google Admin console.  

## Next steps  
Use the remote actions available for Chrome OS devices to deprovision, wipe, restart, or put devices in lost mode. For more information, see [Remote actions for Chrome OS](chrome-enterprise-remote-actions.md).  