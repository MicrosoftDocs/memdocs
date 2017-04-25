---
title: "Download Skycure iOS app configuration policy | Microsoft Docs"
description: "Download Skycure iOS app configuration policy"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 542369dd-b95b-4dd9-8681-5139fe8b53ae
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# Download Skycure iOS app configuration policy

*Applies to: System Center Configuration Manager (Current Branch)*

##Before you begin

You need to log in to the Skycure Management Console to perform the next steps.

> [!TIP] 
> If using Microsoft Internet explorer 11 or Edge, you might need to open the Skycure Management console using In-Private mode.

## To download the iOS app configuration policy

1.  Go to [Skycure Management Console](https://aad.skycure.com).

2.  Enter your **Skycure admin credentials**, then click **Continue**.

	![Skycure Management console login](../media/mtp/skycure-ios-app-1.png)

	> [!IMPORTANT] 
	> The Skycure admin username is an e-mail account that must be a valid user account in the Azure Active Directory, otherwise the login will fail. Skycure uses Azure Active Directory to authenticate its admin username using Single Sign On (SSO).

3.  Go to **Settings** &gt; **Device Management Integrations** &gt; **EMM Integration Selection**, choose **Microsoft Intune**, then save your selection.

2.  Click on the **Integration setup files** link and save the generated \*.zip file. The .zip file contains the **skycure\_configuration.plist** file, which will be used to create the iOS app configuration policy in the Intune classic console.

![Skycure Integration setup files](../media/mtp/skycure-ios-app-2.png)

## Next steps

[Add Skycure apps, Microsoft Authenticator app and the iOS configuration policy](https://docs.microsoft.com/sccm/mdm/deploy-use/add-skycure-apps-microsoft-authenticator-and-ios-app-configuration-policy)
