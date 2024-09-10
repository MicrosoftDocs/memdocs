---
# required metadata

title: Require multifactor authentication for Intune device enrollment
titleSuffix: Microsoft Intune
description: How to require multifactor authentication in Microsoft Entra ID for Intune device enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9

# optional metadata

ROBOTS:
#audience:

ms.reviewer: damionw
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---
# Require multifactor authentication for Intune device enrollments  

*Applies to*: 
 * Android
 * iOS/iPadOS
 * macOS
 * Windows 8.1
 * Windows 10
 * Windows 11  


You can use Intune together with Microsoft Entra Conditional Access policies to require multifactor authentication (MFA) during device enrollment. If you require MFA, employees and students wanting to enroll devices must first authenticate with a second device and two forms of credentials.  MFA requires them to authenticate using two or more of these verification methods:  

- Something they know, such as a password or PIN.  
- Something they have that can't be duplicated, such as a trusted device or phone.        
- Something they are, such as a fingerprint.  

## Prerequisites  
To implement this policy, you must assign Microsoft Entra ID P1 or later to users.   

## Configure Intune to require multifactor authentication at device enrollment

Complete these steps to enable multi-factor authentication during Microsoft Intune enrollment. 

> [!IMPORTANT]
> Don't configure **Device based access rules** for Microsoft Intune enrollment.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
1. Go to **Devices** > **Conditional Access**. This area is the same as the Conditional Access area available in the Microsoft Entra admin center. For more information about the available settings, see [Building a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies).  
1. Choose **Create new policy**.  
1. Name your policy.      
1. Select the **Users** category.
   1. Under the **Include** tab, choose **Select users or groups**.
   2. Additional options appear. Select **Users and groups**. A list of users and groups opens. 
   3. Add the users or groups you're assigning the policy to, and then choose **Select**.    
   4. To exclude users or groups from the policy, select the **Exclude** tab and add those users or groups like you did in the previous step.    
1. Select the next category, **Target resources**.  
   1. Select the **Include** tab.  
   2. Choose **Select apps** > **Select**.   
   3. Choose **Microsoft Intune Enrollment** > **Select** to add the app. Use the search bar in the app picker to find the app.   
     
     For Apple automated device enrollments using Setup Assistant with modern authentication, you have two options to choose from. The following table describes the difference between the *Microsoft Intune* option and *Microsoft Intune Enrollment* option.      
    
     | Cloud app | MFA prompt location | Automated Device Enrollment notes |
     | --- | --- | --- |
     | **Microsoft Intune** | Setup Assistant,<br>Company Portal app | With this option, MFA is required during enrollment and each time the user signs into the Company Portal app or website. The MFA prompts appear on the Company Portal sign-in page. |  
     | **Microsoft Intune Enrollment** | Setup Assistant | With this option, MFA is required during device enrollment and appears as a one-time MFA prompt on the Company Portal sign-in page. |

1. Select the **Grant** category.  
   1. Select **Require multifactor authentication** and **Require device to be marked as compliant**.
   1. Under **For multiple controls**, select **Require all the selected controls**.  
   1. Choose **Select**.
1. Select the **Session** category.  
   1. Select **Sign-in frequency** and choose **Every time**.  
   1. Choose **Select**.  
1. For **Enable policy**, select **On**.
1. Select **Create** to save and create your policy.  

After you apply and deploy this policy, users will see a one-time MFA prompt when they enroll their device. 

> [!NOTE]
> A second device or a Temporary Access Pass is required to complete the MFA challenge for these types of corporate-owned devices:  
>
> - Android Enterprise fully managed devices  
> - Android Enterprise corporate-owned devices with a work profile  
> - iOS/iPadOS devices enrolled via Apple automated device enrollment  
> - macOS devices enrolled via Apple automated device enrollment  
>
> The second device is required because the primary device can't receive calls or text messages during the provisioning process.  
