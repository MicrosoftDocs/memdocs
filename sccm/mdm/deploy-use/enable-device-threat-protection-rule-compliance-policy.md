---
title: "Enable device protection rule in compliance policy"
titleSuffix: "Configuration Manager"
description: "Enable mobile threat protection rule in the device compliance policy."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision:
author: mtillman
ms.author: mtillman
manager: angrobe

---
# Enable device threat protection rule in the compliance policy

*Applies to: System Center Configuration Manager (Current Branch)*

Intune with Lookout mobile threat protection gives you the ability to detect mobile threats and make a risk assessment on the device. You can create an compliance policy rule in Configuration Manager  to include the risk assessment to determine if the device is compliant. You can then use the conditional access policy to allow or block access to Exchange, SharePoint, and other services based on device compliance.

To have Lookout device threat detection influence the compliance policy for the device:

* The  **Device Threat Protection** rule must be enabled on the compliance policy.

* The **Lookout Status** page in the **Intune administrator console** must show as **Active**. See the [Enable Lookout MTP connection in Intune](enable-lookout-connection-in-intune.md) topic for more details and instructions on how to activate Lookout integration.


Before creating the device threat protection rule in the compliancy policy, we recommend that you [set up your subscription with Lookout device threat protection](set-up-your-subscription-with-lookout.md), [enable the Lookout connection in Intune](enable-lookout-connection-in-intune.md),and [configure the Lookout for work app](configure-and-deploy-lookout-for-work-apps.md). The compliance rule enforced only after the setup is completed.

To enable the device threat protection rule, you can either use an existing compliance policy or create a new one.

As part of the Lookout device threat protection setup, in the [Lookout console](https://aad.lookout.com), you created a policy that classifies various threats into high, medium and low levels. In the Intune compliance policy you will use the threat level to set the maximum allowed threat level.

On the **Rules** page of the compliance policy wizard,  define a new rule with the following information:
  * Condition: Device threat protection maximum risk level.
  * Value: The value can be one of the following:
    * **None (secured)**: This is the most secure. This means that the device cannot have any threats. If any level of threats are found, the device is evaluated as non-compliant.
    * **Low**: The device is evaluated as compliant if only low level threats are present. Anything higher puts the device in a non-compliant status.
    * **Medium**: The device is evaluated as compliant if the threats found on the device are low or medium level. If high level threats are detected, the device is determined as non-compliant.
    * **High**: This is the least secure. Essentially, this allows all threat levels, and perhaps only useful if you are using this solution only for reporting purposes.

If you create conditional access policies for Office 365 and other services, the above compliance evaluation is taken into consideration and non-compliant devices are blocked from accessing company resources until the threat is resolved.

The device threat protection status is displayed on the **Security** node in the **Monitoring** workspace.
A summary of the status with various thread level is displayed in a visual chart. You can click on the individual sections of the chart to see more information like, the number of devices reporting as non-compliant by platform, and any errors that are reported.
You can also see the individual device status in the **Assets and compliance** workspace, under **Devices**.  You can add the **Device threat compliance** and the **Device threat level** columns to see the status.  These columns are not displayed by default.
