---
# required metadata

title: Set up automatic enrollment in Intune
description: Set up automatic enrollment for Windows 10/11 devices in Intune.
services: microsoft-intune
author: Lenewsad
ms.author: lanewsad
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/30/2023

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Tutorial: Enable automatic enrollment for Windows 10/11 devices
*Applies to Windows 10, Windows 11*

In this tutorial, you'll set up Microsoft Intune so that it can automatically enroll corporate owned or user owned devices. The feature is called *MDM automatic enrollment* and is enabled by adjusting the MDM user scope in your Azure Active Directory (Azure AD). You can scope automatic enrollment to some users, all users, or none.

We recommend using automatic enrollment for these scenarios:

* Corporate-owned devices joining to Azure AD: Automatic enrollment works with new and existing devices, when enrolling a few devices or in bulk, and when provisioning devices with Windows Autopilot. You can enroll these devices as user-associated or user-less. Enrollment is triggered when the device joins to your Azure AD.     
* User-owned devices in BYOD scenarios: Automatic enrollment works with personal devices that employee or students want to use for work. Devices are enrolled as user-associated, meaning that the device is associated with their Azure AD account (also known as *work or school account*). Enrollment is triggered when the device user registers with Azure AD. They can trigger registration by signing into the Intune Company Portal app or Settings app with their work or school account.  

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md) to try out this tutorial.

## Prerequisites
To try out this feature, you must: 

1. Sign up for Microsoft Intune subscription or trial subscription.  
2. [Create a user](../fundamentals/quickstart-create-user.md) 
3. [Create a group](../fundamentals/quickstart-create-group.md).
4. Get Azure AD Premium (this tutorial describes how to sign up for Azure AD Premium free trial).   

## Sign in to Microsoft Endpoint Manager admin center

Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator to access Microsoft Intune. If you've already created an Intune Trial subscription, the account you created the subscription with is a Global Administrator.

## Set up automatic enrollment

During this short tutorial, you will configure your MDM enrollment settings so that both corporate and bring-your-own-devices can be automatically enrolled in Intune.   

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **All services** > **M365 Azure Active Directory** > **Azure Active Directory** > **Mobility (MDM and MAM)**.
2. Select **Get a free Premium trial to use this feature**. Selecting this option will allow auto enrollment using the Azure Active Directory free Premium trial. 

    ![Screenshot highlighting the Premium trial banner for the Azure Active Directory free Premium trial in the Azure AD admin center.](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-01.png)

3. Choose the **Enterprise Mobility + Security E5** free trial option. 
4. Select **Free trial** > **Activate**. It can take a minute to activate. 

3. Select **Microsoft Intune** to configure Intune. 

    ![Screenshot highlighting the Microsoft Itnune option in the list in Azure AD.](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-03.png)

4. Select **Some** from the **MDM user scope** to use MDM auto-enrollment to manage enterprise data on your employees' Windows devices. MDM auto-enrollment will be configured for Azure AD joined devices and bring-your-own-device scenarios.

    ![Screenshot highlighting the "Some" configuration option next to the "MDM user scope" setting.](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-04.png)

5. Choose **Select groups** > **Contoso Testers** > **Select** as the assigned group.

    ![Screenshot of the "Select groups" assignment pane, highlighting the Contoso Testers example group.](./media/quickstart-setup-auto-enrollment/quickstart-setup-auto-enrollment-05.png)

6. For **MAM User scope**, select **Some** to manage data on your workforce's devices.  

7. Choose **Select groups** > **Contoso Testers** > **Select** as the assigned group. 
8. Use the default values for the remaining configuration values on the page.    
9. Choose **Save**.  
