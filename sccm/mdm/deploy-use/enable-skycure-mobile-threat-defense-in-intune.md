---
title: "Enable Skycure Mobile Threat Defense in Intune | Microsoft Docs"
description: "Enable Skycure Mobile Threat Defense in Intune"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7a3525d-02de-4c13-a411-677ca5327667
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# Enable Skycure Mobile Threat Defense in Intune

*Applies to: System Center Configuration Manager (Current Branch)*

To enable the Skycure mobile threat defense (MTD) connection in Intune, you should have already configured the [Intune Connector in the Skycure console](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-the-skycure-integration-with-Intune).

## To enable the Skycure MTD connection in Intune

1.  Go to the [Intune classic console](https://manage.microsoft.com/) then enter your credentials.

2.  Choose **Admin** &gt; **Third Party Service Integration**, then choose **Skycure Status** and enable **Synchronization with MTD** using the toggle button.

	![Enable Skycure toggle in Intune classic console](../media/mtp/enable-skycure-1.png)

> [!IMPORTANT] 
> You must configure the Skycure apps before creating compliance policy rules and configuring conditional access. This ensures that the app is ready and available for end users to install before they can get access to email or other company resources.

This completes the setup of the Skycure and Intune integration in the Intune administrator console. The next few steps to implement this solution involve deploying the Skycure for Work apps and setting up the compliance policy.

## Next steps

[Create Skycure Mobile Threat Defense compliance policy](https://docs.microsoft.com/sccm/mdm/deploy-use/create-skycure-mobile-threat-defense-compliance-policy)
