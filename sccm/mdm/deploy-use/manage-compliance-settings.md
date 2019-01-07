---
title: "Managing compliance on devices managed with Intune"
titleSuffix: "Configuration Manager"
description: "Learn about System Center Configuration Manager compliance settings by working through some common scenarios."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Managing compliance on devices managed with Intune

*Applies to: System Center Configuration Manager (Current Branch)*

These scenarios give you an introduction to using System Center Configuration Manager compliance settings by working through some common scenarios you might encounter.  

 If you are already familiar with compliance settings, detailed documentation about all the features you use can be found in the [Configuration items for devices managed with Intune](#configuration-items-for-devices-managed-with-intune) section.  

 [Get started with compliance settings](../../compliance/get-started/get-started-with-compliance-settings.md) provides the basics about compliance settings and [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) will help you implement any necessary prerequisites.  

## General information for each scenario  
 In each scenario, you'll create a configuration item that performs a specific task. open the Create Configuration Item Wizard, use the following steps:  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Items**.  

3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  

4.  On the **General** tab of the Create Configuration Item Wizard as shown below, specify a name and description for the configuration item, then choose the appropriate configuration item type for each scenario in this topic.  

     ![Shows general page of the create configuration item wizard.](media/Compliance-Settings-Wizard---1.png)  

## Scenarios for Windows 8.1 and Windows 10 devices managed with Intune  

### Scenario: Restrict access to the app store on all Windows PCs  
 In this scenario, you are the IT admin for a company that deals with highly sensitive information. Because of this, you restrict the apps that users can install. You want to stop users of all Windows 10 PCs from downloading apps from the Windows Store, so you take the following actions.  

1. On the **General** page of the Create Configuration Item wizard, select the **Windows 8.1 and Windows 10** configuration item type, then click **Next**.  

2. On the **Supported Platforms** page, select all of the Windows 10 platforms.  

3. On the **Device Settings** page, select **Store**, then click **Next**.  

4. On the **Store** page, select **Prohibited** as the value for **Application store**.  

5. Select **Remediate noncompliant settings** to ensure the change is applied to all PCs.  

6. Complete the wizard to create the configuration item.  

   You can now use the information in the [Common tasks for creating and deploying configuration baselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  

## Scenarios for Windows Phone devices managed with Intune  

### Scenario: Disable the use of screen capture on a Windows Phone  
 In this scenario, you use Windows Phone 8.1 devices in your company. These devices run a sales app that contains sensitive information. To protect your company, you want to disable the use of screen capture on the device which could potentially be used to transmit sensitive information outside of your company.  

1. On the **General** page of the Create Configuration Item wizard, select the **Windows Phone** configuration item type, then click **Next**.  

2. On the **Supported Platforms** page, select **All Windows Phone 8.1** platforms.  

3. On the **Device Settings** page, select **Device**, then click **Next**.  

4. On the **Device** page, select **Disabled** as the value for **Screen capture**.  

5. Select **Remediate noncompliant settings** to ensure the change is applied to all Windows Phone 8.1 devices.  

6. Complete the wizard to create the configuration item.  

   You can now use the information in the [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  

## Scenarios for iOS and Mac OS X devices managed with Intune  

### Scenario: Disable the camera on iOS devices  
 In this scenario, your company produces blueprints for new product designs. These contain sensitive information that must not be leaked. As your company issues iPhones or iPads to all employees, you want to disable the use of the camera on these devices to prevent them being used to photograph the blueprints.  

1. On the **General** page of the Create Configuration Item wizard, select the **iOS and Mac OS X** configuration item type, then click **Next**.  

2. On the **Supported Platforms** page, select all iPhone and all iPad device platforms.  

3. On the **Device Settings** page, select **Security**, then click **Next**.  

4. On the **Security** page, select **Prohibited** as the value for **Camera**.  

5. Select **Remediate noncompliant settings** to ensure the change is applied to all iOS devices.  

6. Complete the wizard to create the configuration item.  

   You can now use the information in the [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  

## Scenarios for Android and Samsung KNOX Standard devices managed with Intune  

### Scenario: Require a password on all Android 5 devices  
 In this scenario, you'll create a configuration item for Android 5 devices only that requires users to configure a password of at least 6 characters on their devices. Additionally, if a user enters an incorrect password 5 times, then the device will be wiped.  

1. On the **General** page of the Create Configuration Item wizard, select the **Android and Samsung KNOX** configuration item type, then click **Next**.  

2. On the **Supported Platforms** page, select only **Android 5** (to ensure that the settings only get applied to that platform).  

3. On the **Device Settings** page, select **Password**, then click **Next**.  

4. On the **Password** page, configure the following settings:  

   -   **Require password settings on devices** > **Required**  

   -   **Minimum password length (characters)** > **6**  

   -   **Number of failed logon attempts before device is wiped** > **5**  

5. Complete the wizard to create the configuration item.  

   You can now use the information in the [Common tasks for creating and deploying configuration baselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  

## Configuration items for devices managed with Intune

The following System Center Configuration Manager configuration item types are available for devices that are not managed by the Configuration Manager client, for example, devices that are enrolled with Microsoft Intune.  

 -   [How to create configuration items for Windows 8.1 and Windows 10 devices managed with Intune](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [How to create configuration items for Windows Phone devices managed with Intune](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [How to create configuration items for iOS and Mac OS X devices managed with Intune](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [How to create configuration items for Android and Samsung KNOX Standard devices managed with Intune](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
