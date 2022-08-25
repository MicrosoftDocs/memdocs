---
# required metadata

title: Require multifactor authentication for Intune device enrollment
titleSuffix: Microsoft Intune
description: How to require multifactor authentication in Azure AD for Intune device enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/25/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9

# optional metadata

ROBOTS:
#audience:

ms.reviewer: damionw
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---
# Require multifactor authentication for Intune device enrollments

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune can use Azure Active Directory (Azure AD) Conditional Access policies to require multifactor authentication (MFA) for device enrollment to help you secure your corporate resources.

MFA works by requiring any two or more of the following verification methods:

- Something you know (typically a password or PIN).
- Something you have (a trusted device that isn't easily duplicated, like a phone).
- Something you are (biometrics, like a fingerprint).

MFA is supported for iOS/iPadOS, macOS, Android, and Windows 8.1 or later devices.

When you enable MFA, end users need a second device, and must supply two forms of credentials to enroll a device.

## Configure Intune to require multifactor authentication at device enrollment

To require MFA when a device is enrolled, follow these steps:

> [!IMPORTANT]
> You must have an Azure Active Directory Premium P1 or above assigned to your users to implement this policy.

> [!IMPORTANT]
> Don't configure **Device based access rules** for Microsoft Intune enrollment.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Browse to **Devices** > **Conditional Access**. The Conditional Access node accessed from *Intune* is the same node as accessed from *Azure AD*.
1. Choose **New policy**.
1. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
1. Under **Assignments**, select **Users or workload identities**.
   1. Under **Include**, select **Select users or groups**, and check **Users and groups**. Then select the users and/or groups that will receive this policy
   1. Choose **Select**.
1. Under **Cloud apps or actions** > **Include**.
   1. Choose **Select apps** > **Microsoft Intune Enrollment**.
   1. Choose **Select**.
   > By choosing Microsoft Intune Enrollment, Conditional Access MFA is applied only to the enrollment of the device (one-time MFA prompt).

   > For Apple Automated Device Enrollments using **Setup assistant with modern authentication**, you have two options:
   >
   > | Cloud app | MFA prompt location | Automated Device Enrollment notes |
   > | --- | --- | --- |
   > | **Microsoft Intune** | Setup Assistant,<br>Company Portal app | With this option, MFA is required during enrollment and for each login to the Company Portal app/Company Portal website. Conditional Access MFA is applied only to the login of the Company Portal on the device. |
   > | **Microsoft Intune Enrollment** | Setup Assistant | With this option, MFA is applied only to the enrollment of the device (one-time MFA prompt). Conditional Access MFA is applied only to the login of the Company Portal on the device. |

1. Under **Conditions** you don't need to configure any settings for MFA.
1. Under **Access controls** > **Grant**
   1. Select **Require multifactor authentication** and **Require device to be marked as compliant**.
   1. Ensure **Require all the selected controls** is selected under **For multiple controls**.
   1. Choose **Select**.
1. Under **Session**.
   1. Select **Sign-in frequency**.
   1. Ensure **Every time** is selected.
   1. Select **Select**.
1. In **New policy**, choose **Enable policy** > **On**, and then choose **Create**.

> [!NOTE]
> A second device is required to complete the MFA challenge for corporate devices like the following:
>
> - Android Enterprise Fully Managed.
> - Android Enterprise Corporate Owned Work Profile.
> - iOS/iPadOS Automated Device Enrollment.
> - macOS Automated Device Enrollment.
>
> The second device is required because the primary device can't receive calls or text messages during the provisioning process.

## Next steps

When end users enroll their device, they now must authenticate with a second form of identification, like a PIN, a phone, or biometrics.
