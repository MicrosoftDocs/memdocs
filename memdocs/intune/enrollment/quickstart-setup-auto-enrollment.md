---
# required metadata

title: Set up automatic enrollment in Intune
description: Enable Intune automatic enrollment of Windows 10/11 devices that join or register with your Microsoft Entra ID. 
services: microsoft-intune
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 4/11/2024

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Step 4: Set up automatic enrollment for Windows 10/11 devices  

**Applies to**:

- Windows 10  
- Windows 11  

In this task, you'll set up Microsoft Intune to automatically enroll corporate-owned devices, and user-owned devices for bring-your-own-device (BYOD) deployments. You can scope automatic enrollment to some Microsoft Entra users, all users, or none.  

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md) to try out this tutorial. 

## Prerequisites 

- Microsoft Intune subscription - [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
- To complete this step, you must:
  - [Create a user](quickstart-create-user.md).
  - [Create a group](../fundamentals/quickstart-create-group.md).
  - Sign up for the Microsoft Entra ID Free Premium trial.

Automatic MDM enrollment is a premium Microsoft Entra feature. To sign up for a Microsoft Entra ID Premium trial subscription:  

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).  
2. Go to **Identity** > **Settings** > **Mobility**.  
3. Select **Get a free Premium trial to use this feature**. This option gets you the Microsoft Entra ID Free Premium trial.  
4. Choose the **Enterprise Mobility + Security E5** free trial option.  
5. Select **Free trial** > **Activate**. It can take a few minutes to activate.## Sign in to the Microsoft Intune admin center

## Sign in to the Microsoft Intune admin center

Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a [Global administrator or an Intune Service administrator](users-add.md#types-of-administrators). If you've created an Intune Trial subscription, the account you created the subscription with is the Global administrator.  

## Set up automatic enrollment  

For this example, you'll configure Microsoft Intune mobile device management (MDM) and mobile application management (MAM) enrollment settings so that corporate-owned and personal devices automatically enroll in Microsoft Intune. The MDM and MAM user scopes determine how devices and apps are managed in Intune. *MDM user scope* enables automatic enrollment for Microsoft Intune device management. *MAM user scope* enables automatic enrollment for Microsoft Intune mobile application management (MAM). 

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).  
2. Go to **Identity** > **Settings** > **Mobility**.  
4. Select Microsoft Intune.   
5. Configure the MDM and MAM user scope.   
   1. For **MDM user scope** select **All**. Or you can select **Some** and choose a user group. Make sure users aren't members of a group targeted by the MAM user scope.     
   2. For **MAM user scope**, select **None**. Or you can select **Some** and choose a user group. Make sure users aren't members of a group targeted by the MDM user scope.  

>[!IMPORTANT]
> If you configure both user scope types for the same user:
> - The MDM user scope takes precedence if they're on a corporate-owned device. The device automatically enrolls in Microsoft Intune when they set it up for work.  
> - The MAM user scope takes precedence if they bring their own device. The device doesn't enroll in Microsoft Intune for device management. Microsoft Purview Information Protection policies are applied if you configured them. 

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **All services** > **M365 Microsoft Entra ID** > **All services** > **Microsoft Entra ID** > **Mobility (MDM and MAM)**.  
2. Select **Get a free Premium trial to use this feature**. Selecting this option will allow auto enrollment using the Microsoft Entra ID Free Premium trial.  
3. Choose the **Enterprise Mobility + Security E5** free trial option.  
4. Select **Free trial** > **Activate**. It can take a minute to activate.  
5. Select **Microsoft Intune** to configure Intune.  
6. Select **Some** from the **MDM user scope** to use MDM auto-enrollment to manage enterprise data on your employees' Windows devices. MDM auto-enrollment will be configured for Microsoft Entra joined devices and bring-your-own-device scenarios.  
7. Choose **Select groups** > **Contoso Testers** > **Select** as the assigned group.  
8. For **MAM User scope**, select **None**.  
9. Use the default values for the remaining configuration values on the page.    
10. Choose **Save**.  

## Clean up resources

To reconfigure Intune automatic enrollment, check out [Set up enrollment for Windows devices](windows-enroll.md).  

## Next steps

In this task, you learned how to set up auto-enrollment for devices running Windows 10/11. For more information about device enrollment, see [Device enrollment overview](../fundamentals/deployment-guide-enrollment.md).  

To continue to evaluate Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 5 - Enroll your Windows 10/11 device](quickstart-enroll-windows-device.md)
