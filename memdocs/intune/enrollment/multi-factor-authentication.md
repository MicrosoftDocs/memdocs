---
# required metadata

title: Require multifactor authentication for Intune device enrollment
titleSuffix: Microsoft Intune
description: How to require multifactor authentication in Microsoft Entra ID for Intune device enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/19/2024
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
 * Windows 10
 * Windows 11  


You can use Intune together with Microsoft Entra Conditional Access policies to require multifactor authentication (MFA) during device enrollment. If you require MFA, employees and students wanting to enroll devices must first authenticate with a second device and two forms of credentials. MFA requires them to authenticate using two or more of these verification methods:  

- Something they know, such as a password or PIN.  
- Something they have that can't be duplicated, such as a trusted device or phone.        
- Something they are, such as a fingerprint.

If a device isn't compliant, the device user is prompted to make the device compliant before enrolling in Microsoft Intune. 

## Prerequisites  
To implement this policy, you must assign Microsoft Entra ID P1 or later to users.   

## Configure Intune to require multifactor authentication at device enrollment

Complete these steps to enable multifactor authentication during Microsoft Intune enrollment. 

> [!IMPORTANT]
> Don't configure **Device based access rules** for Microsoft Intune enrollment.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
1. Go to **Devices**.
1. Expand **Manage devices**, and then select **Conditional access**. This conditional access area is the same as the conditional access area available in the Microsoft Entra admin center. For more information about the available settings, see [Building a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies).  
1. Choose **Create new policy**.  
1. Name your policy.      
1. Select the **Users** category.
   1. Under the **Include** tab, choose **Select users or groups**.
   2. Additional options appear. Select **Users and groups**. A list of users and groups opens. 
   3. Browse and select the Microsoft Entra users or groups you want to include in the policy. Then choose **Select**.    
   4. To exclude users or groups from the policy, select the **Exclude** tab and add those users or groups like you did in the previous step.    
1. Select the next category, **Target resources**. In this step, you select the resources that the policy applies to. In this case, we want the policy to apply to events where users or groups try to access the Microsoft Intune Enrollment app.   
   1. Under **Select what this policy applies to**, choose **Resources (formerly cloud apps)**.  
   2. Select the **Include** tab.  
   3. Choose **Select resources**. Additional options appear.     
   4. Under **Select**, choose **None**. A list of resources open.  
   5. Search for **Microsoft Intune Enrollment**. Then choose **Select** to add the app.  
     
     For Apple automated device enrollments using Setup Assistant with modern authentication, you have two options to choose from. The following table describes the difference between the *Microsoft Intune* option and *Microsoft Intune Enrollment* option.      
    
     | Cloud app | MFA prompt location | Automated Device Enrollment notes |
     | --- | --- | --- |
     | **Microsoft Intune** | Setup Assistant,<br>Company Portal app | With this option, MFA is required during enrollment and each time the user signs into the Company Portal app or website. The MFA prompts appear on the Company Portal sign-in page. |  
     | **Microsoft Intune Enrollment** | Setup Assistant | With this option, MFA is required during device enrollment and appears as a one-time MFA prompt on the Company Portal sign-in page. |

     > [!NOTE]
     > The Microsoft Intune Enrollment cloud app isn't created automatically for new tenants. To add the app for new tenants, a Microsoft Entra administrator must create a service principal object, with app ID d4ebce55-015a-49b5-a083-c84d1797ae8c, in PowerShell or Microsoft Graph.  

1. Select the **Grant** category. In this step, you grant or block access to the Microsoft Intune Enrollment app.       
   1. Choose **Grant access**.  
   1. Select **Require multifactor authentication**. 
   1. Select **Require device to be marked as compliant**.  
   1. Under **For multiple controls**, select **Require all the selected controls**.  
   1. Choose **Select**.
1. Select the **Session** category. In this step, you can make use of session controls to enable limited experiences within the Microsoft Intune Enrollment app. 
   1. Select **Sign-in frequency**. Additional options appear.
   1. Choose **Every time**.  
   1. Choose **Select**.  
1. For **Enable policy**, select **On**.
1. Select **Create** to save and create your policy.  

After you apply and deploy this policy, device users enrolling their devices see a one-time MFA prompt.  

> [!NOTE]
> A second device or a Temporary Access Pass is required to complete the MFA challenge for these types of corporate-owned devices:  
>
> - Android Enterprise fully managed devices  
> - Android Enterprise corporate-owned devices with a work profile  
> - iOS/iPadOS devices enrolled via Apple automated device enrollment  
> - macOS devices enrolled via Apple automated device enrollment  
>
> The second device is required because the primary device can't receive calls or text messages during the provisioning process.  
