---
title: "Enable device protection rule in compliance policy | System Center Configuration Manager"
description: "Enable mobile threat protection rule in the device compliance policy."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---
# Create a Lookout device threat protection rule

*Applies to: System Center Configuration Manager (Current Branch)*

## Before you begin

Intune with Lookout mobile threat protection gives you the ability to detect mobile threats and make a risk assessment on the device. You can create an compliance policy rule in Configuration Manager to include the risk assessment to determine if the device is compliant. You can then use the conditional access policy to allow or block access to Exchange, SharePoint, and other services based on device compliance.

To have Lookout device threat detection influence the compliance policy for the device:

-   The **Device Threat Protection** rule must be enabled on the compliance policy.

-   The **Lookout Status** page in the **Intune administrator console** must show as **Active**. See the [Enable Lookout MTP connection in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune) topic for more details and instructions on how to activate Lookout integration.

Before creating the device threat protection rule in the compliancy policy, we recommend that you do the following:

1.  [Set up your subscription with Lookout device threat protection](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Enable the Lookout connection in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Configure the Lookout for work app](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>The compliance rule gets enforced only after the setup is completed.

## To create a device threat protection rule

As part of the Lookout device threat protection setup, in the [Lookout console](https://aad.lookout.com), you created a policy that classifies various threats into high, medium and low levels. In the Intune compliance policy, you’ll use the threat level to set the maximum allowed threat level.

To create a Lookout device threat protection rule:

1.  In the Configuration Manager console, click on **Assets and Compliance** workspace.

2.  In the **Assets and Compliance**, expand **Compliance Policies.**

3.  Right-click on **Compliance Policies**, and then select **Create Compliance Policy**.

4.  Enter the compliance policy name, and then select **Compliance rules for devices managed without the Configuration Manager client**.

5.  Select the OS platforms that will be provisioned with the compliance policy (Android 4.1 and later, and/or iOS 8 and later).

6.  On the **Rules** page, click **New** to specify the rules for a compliant device.

7.  On the **Add Rule** page, define a new rule with the following information:
	1.  Condition: Device threat protection maximum risk level.
	
	2.  Value: The value can be one of the following:
		1.  **None (secured)**: This is the most secure. This means that the device cannot have any threats. If any level of threats is found, the device is evaluated as non-compliant.
		2.  **Low**: The device is evaluated as compliant if only low level threats are present. Anything higher puts the device in a non-compliant status.
		3.  **Medium**: The device is evaluated as compliant if the threats found on the device are low or medium level. If high level threats are detected, the device is determined as non-compliant.
		4.  **High**: This is the least secure. Essentially, this allows all threat levels, and perhaps only useful if you are using this solution only for reporting purposes.

>[!IMPORTANT]
>If you create conditional access policies for Office 365 and other services, the above compliance evaluation is taken into consideration and non-compliant devices are blocked from accessing company resources until the threat is resolved.