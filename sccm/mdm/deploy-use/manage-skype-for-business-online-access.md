---
title: "Manage Skype for Business Online access"
titleSuffix: "Configuration Manager"
description: "Learn how to use conditional access policy to manage access to Skype for Business Online."
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Manage Skype for Business Online access

*Applies to: System Center Configuration Manager (Current Branch)*


Use conditional access policy for Skype for Business Online to manage access to Skype for Business Online, based on conditions you specify.  


 When a targeted user attempts to use Skype for Business Online on their device, the following evaluation occurs:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## Prerequisites  

-   Enable [modern authentication](https://aka.ms/SkypeModernAuth) for Skype for Business Online.   

-   All of your users must use Skype for Business Online. If you have a deployment with both Skype for Business Online and Skype for Business on-premises, conditional access policy does not apply to on-premises users.  

-   The device that needs access to Skype for Business Online must:  

    -   Be an Android or iOS device

    -   Be enrolled with Microsoft Intune

    -   Be compliant with any deployed Microsoft Intune compliance policies

 Azure Active Directory stores the device state, which grants or blocks access based on the conditions you specify.  
If a condition is not met, the user sees one of the following messages when they log in:  

-   If the device is not enrolled with Microsoft Intune, or is not registered in Azure Active Directory, the user sees instructions about how to install the Company Portal app and enroll.  

-   If the device is not compliant, the user sees a message that directs them to the Company Portal website or Company Portal app. The Company Portal has information about the problem and how to remediate it.  

## Configure conditional access for Skype for Business Online  

### Step 1: Configure Active Directory security groups  
 Before you start, configure Azure Active Directory security groups for the conditional access policy. Configure these groups in the Office 365 admin center. These groups contain the users to target with or exclude from the policy. When a user is targeted by a policy, each device they use must be compliant in order to access resources.  

 You can specify two group types to use for the Skype for Business policy:  

-   **Targeted groups** contain users to which the policy applies  

-   **Exempted groups** contain users to exclude from the policy  
    If a user is in both groups, they are exempt.  

### Step 2: Configure and deploy a compliance policy  
 Create and deploy a compliance policy to all devices to which the Skype for Business Online policy is targeted.  

 For details about how to configure the compliance policy, see [Manage device compliance policies](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  If you have not deployed a compliance policy and then enable the Skype for Business Online policy, all targeted devices are allowed access if they are enrolled in Microsoft Intune.  


### Step 3: Configure the Skype for Business Online policy  
 Configure the policy to require that only managed and compliant devices can access Skype for Business Online. This policy is stored in Azure Active Directory.  

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com), click **Policy** > **Conditional Access** > **Skype for Business Online Policy**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Select **Enable conditional access policy**.  

3.  Under **Application access**, you can choose to apply conditional access policy to:  

    -   iOS  

    -   Android  

4.  Under **Targeted Groups**, click **Modify** to select the Azure Active Directory security groups to which the policy applies. You can choose to target this policy to all users or just a select group of users.  

5.  Under **Exempted Groups**, optionally, click **Modify** to select the Azure Active Directory security groups that are exempt from this policy.  

6.  When you are done, click **Save**.  

 You have now configured conditional access for Skype for Business Online. You do not have to deploy the conditional access policy, it takes effect immediately.  

## Monitor the compliance and conditional access policies  
 In the Groups workspace, you can view the conditional access status of your devices.  

 Select any mobile device group and then, on the **Devices** tab, select one of the following **Filters**:  

-   **Devices that are not registered with AAD** are blocked from Skype for Business Online

-   **Devices that are not compliant** are blocked from Skype for Business Online  

-   **Devices that are registered with AAD and compliant** can access Skype for Business Online  

### See also  

 [Manage device compliance policies in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
