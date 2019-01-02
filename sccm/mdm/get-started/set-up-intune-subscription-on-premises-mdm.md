---
title: "Set up Intune subscription "
titleSuffix: "Configuration Manager"
description: "Set up an Intune subscription to track licensing for On-premises Mobile Device Management in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Set up a Microsoft Intune subscription for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager On\-premises Mobile Device Management requires a Microsoft Intune subscription to track licensing. The Intune service is not used to manage the devices or to store management information. For On\-premises Mobile Device Management, all device management is handled by the Configuration Manager infrastructure.  

> [!NOTE]  
> Beginning in version 1610, Configuration Manager supports using both Microsoft Intune and on-premises Configuration Manager infrastructure to manage mobile devices at the same time.   

> [!TIP]  
>  We recommend that you set up the Intune subscription for On\-premises Mobile Device Management before you install the required site system roles to minimize the time required for the newly installed site system roles to become functional.  

##  Sign up for Microsoft Intune  
 Intune is required to make On\-premises Mobile Device Management functional. Simply [sign up](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) for a trial or paid subscription and go to the next step to add the subscription to Configuration Manager.  

##  Add the Intune subscription to Configuration Manager  
 To add the subscription to Configuration Manager, you follow the same basic steps as you would when adding the subscription for mobile device management with  Intune. Read the notes below for specific differences, and then use the instructions in [Configure your Intune subscription](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]
>  When adding the Intune subscription, keep the following in mind:  
> 
> - The collection specified in the Add Microsoft Intune Subscription Wizard is not used for On\-premises Mobile Device Management user right delegation. It is only used for mobile device management with Intune. However, you are required to specify a collection for the wizard to proceed.  
>   -   The site code setting specified in the wizard is ignored for On\-premises Mobile Device Management. The site code that is used is the one you specify in the enrollment profile that grants users permission to enroll devices.  
>   -   Do not enable multi factor authentication. It is not supported in On\-premises Mobile Device Management.  

##  Configure the Intune subscription for On-premises Mobile Device Management  

1. In the Configuration Manager console, right-click  the **Microsoft Intune Subscription**, and click **Properties**.  

2. In the On Premises Mobile Device Management box, choose one of the following:

   - If you plan to only have devices managed on-premises, click the check box next to **Only manage devices on-premises**, and click **OK**.  

     > [!NOTE]  
     >  By clicking this check box, you configure the Intune subscription to keep all management information on-premises and not replicate data to the cloud.  

   - If you plan to have devices managed by both Intune and Configuration Manager on-premises, leave the box unchecked.

3. If you plan to manage Windows 10 Mobile devices, right-click the **Microsoft Intune Subscription**, click **Configure Platforms**, and then click  **Windows Phone**.  

4. Click the check box next to **Windows Phone 8.1 and Windows 10 Mobile**, and then click **OK**.  

5. If you plan to manage Windows 10 desktop computers, right-click the **Microsoft Intune Subscription**, click **Configure Platforms**, and then click **Enable Windows Enrollment**.  

6. Click the check box next to **Enable Windows enrollment**, and then click **OK**.  
