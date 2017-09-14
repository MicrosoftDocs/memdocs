---
title: "Common compliance management tasks for client-managed devices - Configuration Manager | Microsoft Docs"
description: "Learn about System Center Configuration Manager compliance settings by working through some common scenarios."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: 8
author: andredm7ms.author: andredmmanager: angrobe

---
# Common tasks for managing compliance on devices with the System Center Configuration Manager client*Applies to: System Center Configuration Manager (Current Branch)*
The scenarios in this topic give you an introduction to using System Center Configuration Manager compliance settings by working through some common scenarios you might encounter.  

 If you are already familiar with compliance settings, detailed documentation about all the features you use can be found in the [Configuration items for devices managed with the System Center Configuration Manager client](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md) section.  

 Before you start, read [Get started with compliance settings](../../compliance/get-started/get-started-with-compliance-settings.md) to learn some basics about compliance settings, and also read [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) to implement any necessary prerequisites.  

## General information for each scenario  
 In each scenario, you'll create a configuration item that performs a specific task. open the Create Configuration Item Wizard, use the following steps:  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Items**.  

3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  

4.  On the **General** tab of the Create Configuration Item Wizard as shown below, specify a name and description for the configuration item, then choose the appropriate configuration item type for each scenario in this topic.  

     ![Shows general page of the create configuration item wizard.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## Scenarios for Windows 10 devices managed with the Configuration Manager client  

### Scenario: Disable the use of Bluetooth on Windows 10 devices  
 In this scenario, your security department have identified the Bluetooth capability on devices as a means that could be used to transmit sensitive corporate information outside the company. You have recently upgraded all of your PCs to Windows 10 and decide to disable the Bluetooth capability on these devices.  

1.  On the **General** page of the Create Configuration Item wizard, select the **Windows 10** configuration item type, then click **Next**.  

2.  On the **Supported Platforms** page of the wizard, select all Windows 10 platforms.  

3.  On the **Device Settings** page, select **Device**, then click **Next**.  

4.  On the **Device** page, select **Prohibited** as the value for **Bluetooth**.  

5.  Select **Remediate noncompliant settings** to ensure the change is applied to all Windows 10 devices.  

6.  Complete the wizard to create the configuration item.  

 You can now use the information in the [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  

## Scenarios for Windows desktop and server computers managed with the Configuration Manager client  
 On Mac computers running the Configuration Manager client, you have two options for assessing compliance:  

-   Evaluate a Mac OS X preferences (plist) file.  

-   Use a custom script and evaluate the results returned by the script.  

 For more information, see [How to create configuration items for Mac OS X devices managed with the System Center Configuration Manager client](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### Scenario: Remediate an incorrect registry value on Windows desktop computers  
 In this scenario, you discover that an important line of business app is not running correctly on some computers you manage that run Windows 8.1. After investigation, you discover that this is because a registry key named **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** is set to a value of **0** on some computers. For the line of business app to run successfully, this value must be set to **1**.  

 In this procedure, you'll create a configuration item that monitors for, and automatically remediates any incorrect registry key values found.  

1.  On the **General** page of the Create Configuration Item wizard, select the **Windows Desktops and Servers (custom)** configuration item type, then click **Next**.  

2.  On the **Supported Platforms** page of the wizard, select **Windows 8.1** (to ensure the configuration item only applies to affected computers).  

3.  On the **Settings** page, click **New** to create a new setting.  

4.  On the **General** tab of the **Create Setting** dialog box, configure the following:  

    -   **Name** > **Example setting**  

    -   **Setting type** > **Registry value**  

    -   **Data type** > **Integer** (as the value contains a number only)  

    -   **Hive** > **HKEY_LOCAL_MACHINE**  

    -   **Key** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **Value** > **1** (the required value)  

5.  On the **Compliance Rules** tab of the **Create Setting** dialog box, click **New**, then in the **Create Rule** dialog box, configure the following:  

    -   **Name** > **Example Rule**  

    -   **Selected setting** – Verify that the selected setting is **Example setting**.  

    -   **Rule type** > **Value**  

    -   **The setting must comply with the following rule** – Verify that the setting name is correct and configure the option to specify that the setting value must equal **1**.  

    -   **Remediate noncompliant rules when supported** – Check this box to ensure that Configuration Manager will reset the registry key value to the correct value if it is incorrect.  

6.  Complete the wizard to create the configuration item.  

 You can now use the information in the [Common tasks for creating and deploying configuration baselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) topic to help you deploy the configuration you have created to devices.  
