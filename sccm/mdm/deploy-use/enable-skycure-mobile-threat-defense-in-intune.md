---
# required metadata

title: Enable Skycure Mobile Threat Defense in Intune | Microsoft Docs
description: Enable Skycure Mobile Threat Defense in the Intune classic console.
keywords:
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 0cc4e59d-819a-47a2-a26f-4f8d0f8df7bf

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: heenamac
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-classic

---

# Enable Skycure Mobile Threat Defense in Intune

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

To enable the Skycure mobile threat defense (MTD) connection in Intune, you should have already configured the [Intune Connector in the Skycure console](https://docs.microsoft.com/intune/deploy-use/setup-the-skycure-integration-with-Intune).

## To enable the Skycure MTD connection in Intune

1.  Go to the [Intune classic console](https://manage.microsoft.com/) then enter your credentials.

2.  Choose **Admin** &gt; **Third Party Service Integration**, then choose **Skycure Status** and enable **Synchronization with MTD** using the toggle button.

	![Enable Skycure toggle in Intune classic console](../media/mtp/enable-skycure-1.png)

> [!IMPORTANT] 
> You must configure the Skycure apps before creating compliance policy rules and configuring conditional access. This ensures that the app is ready and available for end users to install before they can get access to email or other company resources.

This completes the setup of the Skycure and Intune integration in the Intune administrator console. The next few steps to implement this solution involve deploying the Skycure for Work apps and setting up the compliance policy.

## Next steps

[Create Skycure Mobile Threat Defense compliance policy](https://docs.microsoft.com/intune/deploy-use/create-skycure-mobile-threat-defense-compliance-policy)
