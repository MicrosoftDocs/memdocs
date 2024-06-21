---
# required metadata

title: Troubleshoot Windows 10/11 device access for school or work | Microsoft Intune
description: Resolve access or account connection issues for an enrolled Windows device. 
keywords:
author: lenewsad

ms.author: lanewsad
manager: dougeby
ms.date: 04/30/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
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
- tier2
---



# Troubleshoot Windows device access  

**Applies to**  
- Windows 10  
- Windows 11

This article describes how to resolve access issues for an enrolled Windows 10/11 device. 

## Check Wi-Fi connection  

A connection to Wi-Fi is required to access work or school resources. Verify that you're connected to Wi-Fi and then try accessing the resources again.  

## Add work or school account in Settings app  
If your account isn't appearing in the **Settings** app, go through the setup steps in the Settings app again.  

1. Open the **Settings** app. 
2. Select **Accounts**.
3. Identify the version of Windows you're using and then:   
    * Windows 10 (version 1607 and later) and Windows 11: Select **Access work or school**.
    * Windows 10, version 1511 and earlier: Select **Work access**.  
4. Check for your account. If it's not listed, select **Connect** to add it. 
5. Sign in with your work or school account, and then follow the onscreen prompts to finish connecting.  

When complete, your account appears as a connection, and you have access to any resources your organization makes available.   

## Contact IT support for access problems   
If you see your work or school account listed in the Settings app, then your device and account are already connected. Contact your IT support person for further help. They may have put restrictions or requirements in place that prevent you from accessing certain resources. Sign in the Company Portal app or [website](https://go.microsoft.com/fwlink/?linkid=2010980) for your organization's helpdesk details.  

## Error messages  

### We couldn't auto-discover a management endpoint matching the username entered. Please check your username and try again. If you know the URL to your management endpoint, please enter it.

**Cause**: Your account couldn't be verified alongside the provided URL (also referred to as the management endpoint).  

#### Resolution
1. Re-enter your username and password. 
2. If it still doesn't work, contact your IT support person to get the correct URL (example: <code>www.yourcompany.onmicrosoft.com</code>). 
3. When prompted to, enter the provided URL. 

### It looks like you're not connected. Make sure you're connected to the network.

**Cause**: Your device isn't connected to Wi-Fi and a connection is required to add a work or school account.     

#### Resolution
Connect to a Wi-Fi network and then try adding your account again.  

### Your device is already being managed by an organization.  

**Cause**: Your device has already been enrolled in Intune or another mobile device management (MDM) provider.    

#### Resolution  
Contact your IT support person to find out how they want you to proceed.    


