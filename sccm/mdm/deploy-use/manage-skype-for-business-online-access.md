---
title: "Manage Skype for Business Online access"
description: "Learn how to use conditional access policy to manage access to Skype for Business Online."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: 6
author: andredm7
ms.author: andredm
manager: angrobe

---
# Manage Skype for Business Online access

*Applies to: System Center Configuration Manager (Current Branch)*


Use conditional access policy for  **Skype for Business Online** to manage access to Skype for Business Online, based on conditions you specify.  


 When a targeted user attempts to use Skype for Business Online on their device, the following evaluation occurs:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## Prerequisites  

-   Enable modern authentication for Skype for Business Online. Fill this [connect form](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) to be enrolled in the modern authentication program.  

-   All your end-users must be using Skype for Business Online. If you have a deployment with both Skype for Business Online and Skype for Business on-premises, conditional access policy will not be applied to end-users.  

-   The device that needs access to Skype for Business Online must:  

    -   Be an Android or iOS device.  

    -   Be enrolled with Intune.  

    -   Be compliant with any deployed Intune compliance policies.  

 The device state is stored in Azure Active Directory which grants or blocks access, based on the conditions you specify.  
If a condition is not met, the user is presented with one of the following messages when they log in:  

-   If the device is not enrolled with Intune, or is not registered in Azure Active Directory, a message is displayed with instructions about how to install the company portal app and enroll.  

-   If the device is not compliant, a message is displayed that directs the user to the Intune Company Portal website or Company Portal app where they can find information about the problem, and how to remediate it.  

## Configure conditional access for Skype for Business Online  

### Step 1: Configure Active Directory security groups  
 Before you start, configure Azure Active Directory security groups for the conditional access policy. You can configure these groups in the Office 365 admin center. These groups contain the users that will be targeted, or exempt from the policy. When a user is targeted by a policy, each device they use must be compliant in order to access resources.  

 You can specify two group types to use for the Skype for Business policy:  

-   Targeted groups â€“ Contains groups of users to which the policy will apply  

-   Exempted groups â€“ Contains groups of users that are exempt from the policy (optional)  
    If a user is in both groups, they will be exempt from the policy.  

### Step 2: Configure and deploy a compliance policy  
 Ensure that you create and deploy a compliance policy to all devices that the Skype for Business Online policy will be targeted to.  

 For details about how to configure the compliance policy, see [Manage device compliance policies in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  If you have not deployed a compliance policy and then enable the Skype for Business Online policy, all targeted devices will be allowed access if they are enrolled in Intune.  

 When you are ready, continue to Step 3.  

### Step 3: Configure the Skype for Business Online policy  
 Next, configure the policy to require that only managed and compliant devices can access Skype for Business Online. This policy will be will be stored in Azure Active Directory.  

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com), click **Policy** > **Conditional Access** > **Skype for Business Online Policy**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Select **Enable conditional access policy**.  

3.  Under **Application access**, you can choose to apply conditional access policy to:  

    -   iOS  

    -   Android  

4.  Under **Targeted Groups**, click **Modify** to select the Azure Active Directory security groups to which the policy will apply. You can choose to target this to all users or just a select group of users.  

5.  Under **Exempted Groups**, optionally, click **Modify** to select the Azure Active Directory security groups that are exempt from this policy.  

6.  When you are done, click **Save**.  

 You have now configured conditional access for Skype for Business Online. You do not have to deploy the conditional access policy, it takes effect immediately.  

## Monitor the compliance and conditional access policies  
 In the Groups workspace, you can view the conditional access status of your devices.  

 Select any mobile device group and then, on the **Devices** tab, select one of the following **Filters**:  

-   **Devices that are not registered with AAD** â€“ These devices are blocked from Skype for Business Online.  

-   **Devices that are not compliant** â€“ These devices are blocked from Skype for Business Online.  

-   **Devices that are registered with AAD and compliant** â€“ These devices can access Skype for Business Online.  

### See also  

 [Manage device compliance policies in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
