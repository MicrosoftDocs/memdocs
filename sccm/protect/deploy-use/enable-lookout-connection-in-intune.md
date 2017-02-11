---
title: "Enable Lookout MTP in Intune | System Center Configuration Manager"
description: "Enable Lookout mobile threat protection in the Intune admin console."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9536efdd-0f29-47a8-8283-0edea7714319
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---
# Enable Lookout MTP connection in the Intune admin console

*Applies to: System Center Configuration Manager (Current Branch)*

This topic shows you how to enable the Lookout MTP connection in Intune. You should have already configured the Intune Connector in the Lookout console before doing this step.  If you have not already done so, do the steps described in  [Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md).

To enable the Lookout MTP connection in Intune, on the **Administration** page in the [Microsoft Intune administrator console](https://manage.microsoft.com), choose **Third Party Service Integration**. Choose **Lookout status** and enable **Synchronization with MTP** using the toggle button.

![screenshot of the Lookout synchronization page with the enable toggle button highlighted](../media/lookout-intune-synchronization.png)

This completes the setup of the Lookout and Intune integration in the Intune administrator console.  The next few steps to implement this solution involve deploying the [Lookout for Work apps](configure-and-deploy-lookout-for-work-apps.md) and setting up the [compliance](enable-device-threat-protection-rule-compliance-policy.md) policy.

>[!IMPORTANT]
> You **must** configure the Lookout for Work app before creating compliance policy rules and configuring conditional access. This ensures that the app is ready and available for end users to install before they can get access to email or other company resources.

## Next steps
[Configure Lookout for Work app ](configure-and-deploy-lookout-for-work-apps.md)
