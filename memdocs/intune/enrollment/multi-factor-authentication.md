---
# required metadata

title: Require multi-factor authentication for Intune device enrollment
titleSuffix: Microsoft Intune
description: How to require multi-factor authentication in Azure AD for Intune device enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/27/2021
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

# Require multi-factor authentication for Intune device enrollments

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune can use Azure Active Directory (AD) Conditional Access policies to require multi-factor authentication (MFA) for device enrollment to help you secure your corporate resources.

MFA works by requiring any two or more of the following verification methods:

- Something you know (typically a password or PIN).
- Something you have (a trusted device that isn't easily duplicated, like a phone).
- Something you are (biometrics, like a fingerprint).

MFA is supported for iOS/iPadOS, macOS, Android, and Windows 8.1 or later devices.

When you enable MFA, end users needs a second device and must supply two forms of credentials to enroll a device.

## Configure Intune to require multi-factor authentication at device enrollment

To require MFA when a device is enrolled, follow these steps:

>[!Important]
>You must have an Azure Active Directory Premium P1 or above assigned to your users to implement this policy.

>[!Important]
>Don't configure **Device based access rules** for Microsoft Intune enrollment.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Conditional Access**. The Conditional Access node accessed from *Intune* is the same node as accessed from *Azure AD*.
2. Choose **New policy**.
3. In **New** policy, type a descriptive name for the policy.
4. In the **Assignments** section, choose **Users and groups**. 
5. In **Users and groups**, choose **Select users or groups**, and check **Users and groups**. Then select the users and /or groups that will receive this policy, then choose **Done**.
6. In the **Assignments** section, choose **Cloud apps**.
7. On the **Include** tab of **Cloud apps**, choose **Select apps**, then choose **Select** > **Microsoft Intune Enrollment**, and then choose **Done**. By choosing Microsoft Intune Enrollment, conditional access MFA is applied only to the enrollment of the device (one-time MFA prompt).

    For Apple Automated Device Enrollments using **Setup assistant with modern authentication**, you have two options:

    | Cloud app | MFA prompt location | Automated Device Enrollment notes |
    | --- | --- | --- |
    | **Microsoft Intune** | Setup Assistant,<br>Company Portal app | With this option, MFA is required during enrollment and for each login to the Company Portal app/Company Portal website. Conditional access MFA is applied only to the login of the Company Portal on the device. |
    | **Microsoft Intune Enrollment** | Setup Assistant | With this option, MFA is applied only to the enrollment of the device (one-time MFA prompt). Conditional access MFA is applied only to the login of the Company Portal on the device. |

8. Choose **Done**.
9. In the **Assignments** section, for **Conditions** you don't need to configure any settings for MFA.
10. In the **Access controls** section, choose **Grant**.
11. In **Grant**, choose **Grant access**, and then select **Require multi-factor authentication** and **Require device to be marked as compliant**. Then choose **Select**.
12. In **New policy**, choose **Enable policy** > **On**, and then choose **Create**.

> [!NOTE]
> A second device is required to complete the MFA challenge for corporate devices like the following:
> - Android Enterprise Fully Managed.
> - Android Enterprise Corporate Owned Work Profile.
> - iOS/iPadOS Automated Device Enrollment.
> - macOS Automated Device Enrollment.
>
> The second device is required because the primary device can't receive calls or text messages during the provisioning process.


## Next steps

When end users enroll their device, they now must authenticate with a second form of identification, like a PIN, a phone, or biometrics.
