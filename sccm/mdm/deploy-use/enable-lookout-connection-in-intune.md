---
title: Enable Lookout MTD in Intune
titleSuffix: Configuration Manager
description: Enable Lookout mobile threat defense (MTD) in the Microsoft Intune portal.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Enable Lookout MTD connection in the Intune admin console

*Applies to: System Center Configuration Manager (Current Branch)*

This article shows you how to enable the Lookout mobile threat defense (MTD) connection in Microsoft Intune. You should have already configured the Intune Connector in the Lookout console before doing this step. If you haven't already done so, do the steps described in [Set up your subscription with Lookout mobile threat defense](set-up-your-subscription-with-lookout.md).



## Enable the Lookout MTD connector

1. Go to the [Azure portal](https://portal.azure.com), and sign in with your Intune credentials. After you've successfully signed in, you see the **Azure Dashboard**.  

2. On the **Azure Dashboard**, choose **All services** from the left menu, then type **Intune** in the text box filter.  

3. Choose **Intune**; the **Intune Dashboard** opens.  

4. On the **Intune Dashboard**, choose **Device compliance**, then choose **Mobile Threat Defense** under the **Setup** section.  

5. On the **Mobile Threat Defense** pane, choose **Add**.  

6. Choose **Lookout** as the **Mobile Threat Defense connector to setup** from the drop-down list.  

7. Enable the toggle options according to your organization's requirements.  



## MTD toggle options

You can decide which MTD toggle options you need to enable according to your organization's requirements. Here are more details:

- **Connect Android 4.1+ devices to Lookout for Work MTD**: When you enable this option, you can have Android 4.1+ devices reporting security risk back to Intune.  
	- **Mark as noncompliant if no data is received**: If Intune doesn't receive data about a device on this platform from Lookout, consider the device noncompliant.  

- **Connect iOS 8.0+ devices to Lookout for Work MTD**: When you enable this option, you can have Android 4.1+ devices reporting security risk back to Intune.
	- **Mark as noncompliant if no data is received**: If Intune doesn't receive data about a device on this platform from Lookout, consider the device noncompliant.  

> [!TIP]  
> You can see the **Connection status** and the **Last synchronized** time between Intune and Lookout from the Mobile Threat Defense pane.



## Next steps
This completes the setup of the Lookout and Intune integration. The next few steps to implement this solution involve deploying the [Lookout for Work apps](configure-and-deploy-lookout-for-work-apps.md) and setting up the [compliance](enable-device-threat-protection-rule-compliance-policy.md) policy.

>[!IMPORTANT]
> You *must* configure the Lookout for Work app before creating compliance policy rules and configuring conditional access. This action ensures that the app is ready and available for end users to install before they can get access to email or other company resources.

[Configure Lookout for Work app](configure-and-deploy-lookout-for-work-apps.md)
