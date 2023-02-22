---
# required metadata

title: Quickstart - Set up automatic enrollment in Intune
description: Quickstart - Set up automatic enrollment for Windows 10/11 devices in Intune.
services: microsoft-intune
author: Lenewsad
ms.author: lanewsad
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 09/22/2020

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Quickstart: Set up automatic enrollment for Windows 10/11 devices

In this quickstart, you'll set up Microsoft Intune to automatically enroll devices when specific users sign in to Windows 10/11 devices.

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

- Microsoft Intune subscription - [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
- To complete this quickstart, you must first [create a user](../fundamentals/quickstart-create-user.md) and [create a group](../fundamentals/quickstart-create-group.md).

## Sign in to Intune in the Microsoft Endpoint Manager

Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator. If you've already created an Intune Trial subscription, the account you created the subscription with is a Global Administrator.

## Set up Windows 10/11 automatic enrollment

For this example, you'll use MDM enrollment so that both corporate and bring-your-own-devices can be automatically enrolled. You will sign up for a free Azure Active Directory Premium subscription.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **All services** > **M365 Azure Active Directory** > **Azure Active Directory** > **Mobility (MDM and MAM)**.
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

6. For **MAM User scope**, select **None**.  
7. Choose **Select groups** > **Contoso Testers** > **Select** as the assigned group. 
8. Use the default values for the remaining configuration values on the page.    
9. Choose **Save**.

> [!IMPORTANT]
> For Windows BYOD devices, the MAM user scope takes precedence if both the MAM user scope and the MDM user scope (automatic MDM enrollment) are enabled for all users (or the same groups of users). The device will not be MDM enrolled, and Windows Information Protection (WIP) policies will be applied if you have configured them.

If your intent is to enable automatic enrollment for Windows BYOD devices to an MDM, configure the MDM user scope to All (or Some, and specify a group) and configure the MAM user scope to None (or Some, and specify a group–ensuring that users are not members of a group targeted by both MDM and MAM user scopes).

For corporate devices, the MDM user scope takes precedence if both MDM and MAM user scopes are enabled. The device will get automatically enrolled in the configured MDM.

## Clean up resources

To reconfigure Intune automatic enrollment, check out [Set up enrollment for Windows devices](windows-enroll.md).  

## Next steps

In this quickstart, you learned how to set up auto-enrollment for devices running Windows 10/11. For more information about device enrollment, see [What is device enrollment?](device-enrollment.md)

To follow this series of Intune quickstarts, continue to the next quickstart.

> [!div class="nextstepaction"]
> [Quickstart: Enroll your Windows 10/11 device](quickstart-enroll-windows-device.md)
