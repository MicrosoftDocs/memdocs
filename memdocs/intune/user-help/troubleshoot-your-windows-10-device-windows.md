---
# required metadata

title: Troubleshoot Windows 10/11 device access for school or work | Microsoft Intune
description: Resolve access or account connection issues for an enrolled Windows device. 
keywords:
author: lenewsad

ms.author: lanewsad
manager: dougeby
ms.date: 10/04/2021
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: amanh
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---



# Troubleshoot Windows device access  

**Applies to**  
- Windows 10  
- Windows 11

This article describes how to resolve access issues for an enrolled Windows 10/11 device. 

## Check Wi-Fi connection  

A connection to Wi-Fi is required to access work or school resources. Verify that you're connected to Wi-Fi and then try accessing the resources again.  

## Add work or school account in Settings app  
These steps are the same you'd use to enroll your device. However, if your account isn't appearing in the **Settings** app, you may need to run through these steps again.  

1. Open the **Settings** app. 
2. Select **Accounts**.
3. This next step varies depending on the version of Windows you're using. 
    * Windows 10 (version 1607 and later) and Windows 11: Select **Access work or school**.
    * Windows 10, version 1511 and earlier: Select **Work access**.  
4. Check for your account. If it's not listed, select the **Connect** plus sign button to add it. 
5. Sign in with your work or school credentials. 
6. Follow the onscreen prompts to finish connecting.  
7. When complete, your account will be added as a connection. You'll have access to any resources your organization makes available.   

## Contact IT support for access requirements  
If you see your work or school account listed in the Settings app, your device and account are already connected. Contact your IT support person for further help with access problems. They may have restrictions or requirements in place that are preventing you from accessing certain resources.  

## Error messages  

### We couldn't auto-discover a management endpoint matching the username entered. Please check your username and try again. If you know the URL to your management endpoint, please enter it.

**Cause**: Your account couldn't be verified alongside the provided URL (also referred to as the management endpoint).  

#### Resolution
1. Re-enter your username and password. 
2. If it still doesn't work, contact your IT support person to get the correct URL (example: <code>www.yourcompany.onmicrosoft.com</code>). 
3. When prompted, enter the provided URL. 

### It looks like you're not connected. Make sure you're connected to the network.

**Cause**: Your device isn't connected to Wi-Fi and a connection is required to add a work or school account.     

#### Resolution
1. From your device toolbar or settings, select the **Network status** globe icon.
2. Select a Wi-Fi network > **Connect**.  
3. Try to connect your account again.  

### Your device is already being managed by an organization.  

**Cause**: Your device has already been enrolled in Intune or another mobile device management (MDM) provider.    

#### Resolution  
Contact your IT support person to find out how they want you to proceed.    


## Next steps  

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
