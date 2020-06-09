---
# required metadata

title: Resolving threats found by SandBlast Mobile Protect for Android | Microsoft Docs
description: Learn how to fix a threat found by SandBlast Mobile Protect for Android.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/28/2018
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 449c34ec-2d94-4c7f-8691-a5200efee3cb
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

#ms.reviewer: heenamac
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Resolve a threat found by SandBlast Mobile Protect

SandBlast Mobile Protect is a Mobile Threat Defender service that identifies potential threats on your Android devices. It reports threats that you can then view from the Company Portal app. Threats appear to you in the app as unresolved, noncompliant issues. As long as these threats are present, you might not be able to:   

* Connect to corporate e-mail
* Connect to corporate Wi-Fi
* Connect to SharePoint Online
* Sync corporate files with OneDrive
* Access company apps

This article describes how to recognize Sandblast Mobile Protect threat alerts and what to do to resolve them.  

## Troubleshoot virus or security threat  
If a virus or security threat is detected, SandBlast Mobile Protect app will act according to your organization's access policies. You company's access policies could prevent you from accessing your work's network, apps, and email.  

![Example screenshot of a SEP Mobile app alert message.](./media/skycure-list-of-potential-issues-android.png)  

However, SandBlast Mobile Protect will also prompt you to take action to regain the access you've lost. Select the threat and follow the instructions within the app to resolve it.

Because the app is integrated with your company's MDM provider, you'll also see a warning about restricted access in the Company portal app. The warning instructs you to open Sandblast Mobile Protect to fix the virus or security threat.

  ![Example screenshot of the Company Portal device page, showing the SandBlast Mobile Protect warning.](./media/CP-lookout-virus-banner-1808.png)  

## Troubleshoot an app threat  

If you install an app that's seen as a threat to your device, you'll receive a notification within SandBlast Mobile Protect. If the affected app remains on your device, you'll be unable to access company resources.  

To resolve, select the app from the list of threats in SandBlast Mobile Protect. Then follow the instructions to remove and uninstall the app.     

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
