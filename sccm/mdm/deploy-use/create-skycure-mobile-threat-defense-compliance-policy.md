---
# required metadata

title: Create Skycure Mobile Threat Defense compliance policy | Microsoft Docs
description: Create Skycure Mobile Threat Defense compliance policy in the Intune classic console.
keywords:
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 56ff1728-1119-4e8a-aae6-ed5c7fafa052

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: heenamac
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-classic

---

# Create Skycure Mobile Threat Defense compliance policy

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Intune with Skycure Mobile Threat Defense lets you detect threats on mobile devices and assess risk on those devices. You can create an Intune compliance policy rule that assesses risk to determine if the device is compliant. You can then use conditional access policy to block access to services based on device compliance.

## Before you begin

Prerequisites for compliance policy with Skycure device threat protection:

-   [Setup Skycure integration with Intune](https://docs.microsoft.com/intune/deploy-use/setup-the-skycure-integration-with-Intune)

-   [Enable the Skycure connection in Intune](https://docs.microsoft.com/intune/deploy-use/enable-skycure-mobile-threat-defense-in-intune)

As part of the Skycure Mobile Threat Defense setup, in the Skycure console, you created a policy that classifies various threats as high, medium and low. You now need to set the maximum allowed threat level in the Intune compliance policy.

## To create Skycure compliance policy

1.  Go to the [Intune classic console](https://manage.microsoft.com/) then enter your credentials.

2.  Choose **Policy** &gt; **Compliance Policies**. You can either use an existing compliance policy or create a new one.

3.  Choose **Add** &gt; **Device Health**, then enable **Device Threat Protection**.

4.  Select the **Maximum allowed threat level**:

    a.  **None (Secured)**: This is the most secure. The device cannot have any threats present and still access company resources. If any threats are found, the device is evaluated as non-compliant.

    b.  **Low**: The device is compliant if only low level threats are present. Anything higher puts the device in a non-compliant status.

    c.  **Medium**: The device is compliant if the threats found on the device are low or medium level. If high level threats are detected, the device is determined as non-compliant.

    d.  **High**: This is the least secure. This allows all threat levels, and uses Skycure mobile threat defense for reporting purposes only.

> [!IMPORTANT] 
> If you create conditional access policies for Office 365 or other services, this compliance evaluation is assessed and non-compliant devices are blocked from accessing those services until the threat is resolved.

## <span id="monitor-device-threats" class="anchor"><span id="next-steps" class="anchor"><span id="_Toc477360344" class="anchor"></span></span></span>Next steps

-   Create a conditional access policy for:

	-   [Exchange Online](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
	-   [Exchange On-premises](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-onpremises-with-microsoft-intune)
	-   [SharePoint Online](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)
	-   [Skype for Business Online](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)
	-   [Dynamics CRM](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)
