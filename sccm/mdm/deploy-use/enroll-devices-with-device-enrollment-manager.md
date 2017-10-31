---
title: "Enroll devices with device enrollment manager "
titleSuffix: "Configuration Manager"
description: "Enroll corporate-owned devices with the device enrollment manager account with System Center Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: 8
author: arob98
ms.author: angrobe
manager: angrobe

---
# Enroll devices with device enrollment manager with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Organizations can use Intune to manage large numbers of mobile devices with a single user account. The *device enrollment manager* (DEM) account is a special user account used to enroll devices. You add existing users to the DEM account to give them the special DEM capabilities. Each enrolled device uses a single license. We recommend that you use devices enrolled through this account as shared devices with no user affinity, rather than personal, dedicated devices.  

## Enroll corporate-owned devices with the device enrollment manager  
 You can assign a store manager or supervisor, for example, a device enrollment manager user account to allow her to do the following:  

-   Enroll up to 1000 devices for management  
-   Use the Company Portal app to install company apps  
-   Configure access to company data  

The following limitations apply to devices managed using a device enrollment manager account:

- The store manager cannot reset the device from the company portal.  
- Devices cannot be workplace joined or Azure Active Directory joined. This prevents these devices from using conditional access.
-  To deploy company apps to devices managed with the device enrollment manager, deploy Company Portal app as a **Required Install** to the device enrollment manager's user account. The device enrollment manager can then launch the Company Portal app to install additional apps.
- To improve performance, the Company Portal app only shows the local device. Remote management of other DEM devices can only be done from the Configuration Manager console by and administrator
- The Company Portal website is not available for device enrollment manager accounts. Use the Company Portal app.
- If you use DEM to enroll iOS devices, you can't use the Apple Configurator or Apple Device Enrollment Program (DEP) to enroll devices. (iOS only) 

 **Examples of device enrollment manager scenario:**   
A restaurant wants point-of-sale tablets for its wait staff and order-monitors for its kitchen staff. The employees never need access to company data or to log on as a user. The Intune administrator creates a device enrollment manager account and enrolls the company-owned devices using that account. Alternatively, the administrator could give the device enrollment manager credentials to a restaurant manager, allowing him or her to enroll and manage the devices.  

 The administrator or manager can deploy role-specific apps to the restaurant devices. An administrator can also select a device in the console and retire it from mobile device management.  

#### Add a device enrollment manager  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Cloud Services**, and click **Microsoft Intune Subscriptions**. Select the Microsoft Intune subscription to which you'll add a device enrollment manager, and then click **Properties**.  

3.  In the Microsoft Intune Subscription Properties dialog box, click the **Device Enrollment Manager** tab.  

4.  Click **Add/Remove**.  

5.  In the **Device Enrollment Manager** dialog, type the user name of the user you want to add as a device enrollment manager and then click **Search**. Select the user you'd like to add as a Device Enrollment Manager and click **Add**.  

6.  Confirm the user account that will be a device enrollment manager and click **Add/Remove**.  A subscription license is required for each user that accesses the service and the *device enrollment manager* cannot be an Intune administrator. Determine whether you need to add more licenses before you use this feature.  

7.  The device enrollment manager can now enroll mobile devices using the same procedure an end user uses for a bring-your-own-device (BYOD) scenario in the company portal.  

#### Delete a device enrollment manager from Intune  
Deleting a device enrollment manager does not affect enrolled devices. When a device enrollment manager is deleted:  
- No enrolled devices are unenrolled  
- Enrolled devices continue to be fully managed  
- The deleted device enrollment manager account credentials remain valid to log on to the company portal to access apps  
- The deleted device enrollment manager account credentials still cannot wipe or retire devices  
- The deleted device enrollment manager account’s relationship to enrolled devices remains but no additional devices can be enrolled

1.  In the Configuration Manager console, click **Administration**.  
2.  In the **Administration** workspace, expand **Cloud Services**, and click **Microsoft Intune Subscriptions**. Select the Microsoft Intune subscription to which you'll add a device enrollment manager, and then click **Properties**.  
3.  In the Microsoft Intune Subscription Properties dialog box, click the **Device Enrollment Manager** tab.  
4.  **Search** for the device enrollment manager you'd like to delete and click **Remove**, then **OK**.  
