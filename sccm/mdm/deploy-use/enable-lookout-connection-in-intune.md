---
title: "Enable Lookout MTP in Intune"
description: "Enable Lookout mobile threat protection in the Intune admin console."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision:
author: mtillman
ms.author: mtillman
manager: angrobe

---
# Enable Lookout MTP connection in the Intune admin console

*Applies to: System Center Configuration Manager (Current Branch)*

This topic shows you how to enable the Lookout MTP connection in Intune. You should have already configured the Intune Connector in the Lookout console before doing this step.  If you have not already done so, do the steps described in  [Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md).

To enable the Lookout MTP connection in Intune, on the **Administration** page in the [Microsoft Intune administrator console](https://manage.microsoft.com), choose **Third Party Service Integration**. Choose **Lookout status** and enable **Synchronization with MTP** using the toggle button.

![screenshot of the Lookout synchronization page with the enable toggle button highlighted](media/lookout-intune-synchronization.png)

This completes the setup of the Lookout and Intune integration in the Intune administrator console.  The next few steps to implement this solution involve deploying the [Lookout for Work apps](configure-and-deploy-lookout-for-work-apps.md) and setting up the [compliance](enable-device-threat-protection-rule-compliance-policy.md) policy.

>[!IMPORTANT]
> You **must** configure the Lookout for Work app before creating compliance policy rules and configuring conditional access. This ensures that the app is ready and available for end users to install before they can get access to email or other company resources.

## Next steps
[Configure Lookout for Work app ](configure-and-deploy-lookout-for-work-apps.md)
