---
# required metadata

title: Configure ChromeOS connector for Microsoft Intune | Microsoft Intune  
description: Learn how to connect the Google Admin Console to Microsoft Intune so that you can view and take action on enrolled ChromeOS devices.  
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

# Configure Chrome Enterprise connector  

Set up the Chrome Enterprise connector with Microsoft Intune to view and take action on company and school-owned ChromeOS devices. This article describes how to create and monitor a connection between the Google Admin console and Microsoft Intune. After you establish a connection, you can: 

* Sync device information between the Google Admin console and Microsoft Intune.    
* View device information in your device inventory lists in the Microsoft Intune admin center.
* Apply remote actions, such as deprovision, restart, lost mode, and wipe in the admin center.   

One connection is allowed per tenant. 

Devices must be enrolled before you can see them in the admin center. Enrollment for ChromeOS devices is done in the Google Admin center. You can create the connection before or after you enroll devices. For more information, see [Enroll ChromeOS devices](https://support.google.com/chrome/a/answer/1360534) (opens Chrome Enterprise and Education Help).    

## Prerequisites  
To establish a connection, you must have:   

* Access to the Google Admin console  
* [Permission to manage ChromeOS Devices](https://support.google.com/a/answer/9807615)(opens Google Workspace Admin Help)  
* One of these roles: 
   * Intune Service Administrator 
   * Custom Intune role, with *Chrome Enterprise update connection settings* permission.  

## Create Chrome Enterprise connection  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant administration** > **Connectors and tokens**.
3. Select **Chrome Enterprise** > **Connect**. 
4. On the **Connect to Chrome Enterprise** page, select **Google Admin console**, and then:  
   1. Sign in to the Admin console. 
   2. Go to **Security** > **Access and data control** > **API Controls**.  
   3. Select **MANAGE DOMAIN WIDE DELEGATION**.   
   4. Select **Add new** to create the API client for your connection.        
   3. In the Microsoft Intune admin center, copy the Client ID and OAuth Scopes.  
   4. Return to the Google Admin console and paste each value in the **Client ID** and **OAutho scopes (comma-delimited)** spaces, respectively. Intune requires the following scopes:  
    `https://www.googleapis.com/auth/admin.directory.device.chromeos`  
    `https://www.googleapis.com/auth/admin.directory.user.readonly`  
    `https://www.googleapis.com/auth/admin.directory.orgunit.readonly`  
   5. Select **Authorize** to save all changes. 
5. Return to the Microsoft Intune admin center and select **Launch Google to connect now.**     
6. When prompted to authenticate with your organization's Google Enterprise domain, use your Google Admin account. The Google Admin account appears in Google Workspace audit logs for all actions applied to ChromeOS devices in the Intune admin center. Your account must have:  
   * Permission to manage ChromeOS devices, as described in [Prerequisites](chrome-enterprise-connector-configure.md#prerequisites).  
   * Access to Google Workspace Admin SDK Directory API.  

After you authenticate, the connection is established and your organization’s enrolled ChromeOS devices begin syncing from the Google Admin console. The status changes to **Active** when syncing is complete. 

   >[!NOTE]
   > Sync time varies and depends on the number of ChromeOS devices you have in the Google Admin console.  

## Monitor connection status  
Go to **Chrome Enterprise** in the Microsoft Intune admin center to check the overall health of your connection, and get details about the ongoing and completed syncs. ChromeOS devices should appear shortly after the initial connection. Devices will continue to sync periodically and receive updates.   

Available details include:  

* **Status**: **Syncing** is shown when devices are still being synced. The status changes to **Active** when syncing is complete.  
* **Last check-in**: Shows the last time new devices, device details, or remote actions were synced between Microsoft Intune and the Google Admin console.   
* **Chrome devices synced**: Shows the number of ChromeOS devices synced with Intune.  
* **Connected account**: Shows the Google Admin account that's connected to Microsoft Intune.    

## Delete connection   
These roles can delete the connection between Microsoft Intune and the Google Admin console:  
* Intune Service Administrator  
* Custom Intune role that has *Chrome Enterprise delete connection settings permission*  

Deleting your connection removes all ChromeOS devices and Chrome Enterprise connection settings from Intune and Microsoft Entra ID. After the existing connection is deleted, you'll have space in your tenant to create a new connection.  

To delete the connection in the Microsoft Intune admin center:  
1. Go to **Tenant administration** > **Connectors and tokens**.  
2. Select **Chrome Enterprise**.  
3. Select **Delete**.  

## Next steps  
* View ChromeOS devices and details synced between Google Admin console and the Microsoft Intune admin center. The information can be used to monitor connections or build reports. For more information, see [View ChromeOS device information in Intune](chrome-enterprise-device-details.md).   
*  Use the remote actions available for ChromeOS devices to deprovision, wipe, restart, or put devices in lost mode. For more information, see [Remote device actions for ChromeOS](chrome-enterprise-remote-actions.md).  
