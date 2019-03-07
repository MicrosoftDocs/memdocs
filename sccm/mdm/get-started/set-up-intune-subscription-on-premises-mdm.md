---
title: Set up Intune subscription
titleSuffix: Configuration Manager
description: Set up an Intune subscription to track licensing for on-premises mobile device management in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Set up a Microsoft Intune subscription for on-premises MDM in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager on-premises mobile device management (MDM) requires a Microsoft Intune subscription to track licensing. The Intune service isn't used to manage the devices or to store management information. For on-premises MDM, all device management is handled by the Configuration Manager infrastructure.  

Before you install the required site system roles for on-premises MDM, set up the Intune subscription. This action minimizes the time required for the newly installed site system roles to become functional.  

> [!Note]  
> Starting in version 1810, an Intune connection is no longer required for new on-premises MDM deployments.<!--3607730, fka 1359124--> Your organization still requires Intune licenses to use this feature. You can't currently remove the Intune connection from existing on-premises MDM deployments. For more information, see the [Intune support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  Sign up for Microsoft Intune  

Intune is required to make on-premises MDM functional. [Sign up](https://docs.microsoft.com/intune/free-trial-sign-up) for a trial or paid subscription. Then go to the next step to add the subscription to Configuration Manager.  



##  Add the Intune subscription to Configuration Manager  

To add the subscription to Configuration Manager, you follow the same basic steps as you would when adding the subscription for hybrid MDM with Intune. Read the notes below for specific differences, and then use the instructions in [Configure your Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  When adding the Intune subscription, keep the following notes in mind:  
> 
> - The collection specified in the Add Microsoft Intune Subscription Wizard isn't used for on-premises MDM user right delegation. It's only used for mobile device management with Intune. However, you're required to specify a collection for the wizard to proceed.  
> 
> - The site code that you specify in the wizard is ignored for on-premises MDM. It uses the site code that you specify in the enrollment profile that grants users permission to enroll devices.  
> 
> - Don't enable multi-factor authentication. It's not supported in on-premises MDM.  



##  Configure the Intune subscription for on-premises MDM  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Microsoft Intune Subscriptions** node. Select your subscription, and then choose **Properties** in the ribbon.   

    1. In the On Premises Mobile Device Management section at the bottom of the **General** page, choose one of the following options:

        - If you plan to only have devices managed on-premises, select the option to **Only manage devices on-premises**.  

            > [!NOTE]  
            > When you enable this option, you configure the Intune subscription to keep all management information on-premises. No device management data is replicated to the cloud.  

        - If you plan to have devices managed by both Intune and Configuration Manager on-premises, don't configure this option.  

    Select **OK** to close the subscription properties.

2. If you plan to manage Windows 10 Mobile devices, select your subscription in the list, select **Configure Platforms** in the ribbon, and then select **Windows Phone**.  

    1. Select the option for **Windows Phone 8.1 and Windows 10 Mobile**, and then select **OK**.  

3. If you plan to manage Windows 10 desktop computers, select your subscription in the list, select **Configure Platforms** in the ribbon, and then select **Windows**.  

    1. Select the option to **Enable Windows enrollment**, and then select **OK**.  

