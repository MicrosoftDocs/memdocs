---
title: "Configure Android for Work apps with app configuration policies | Microsoft Docs"
description: "Help eliminate configuration problems on devices running Android for Work by deploying app configuration policies to users before they run apps."
ms.custom: na
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
caps.latest.revision: 0
caps.handback.revision: 0
author: NathBarn
ms.author: NathBarn
manager: angrobe
---
# Apply settings to Android for Work apps with app configuration policies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can use app configuration policies in System Center Configuration Manager to distribute settings that might be required when a user runs an app. For example, an app might require a user to specify these details:
- A custom port number
- Language settings
- Security settings
- Branding settings, like a company logo

If the user enters the settings incorrectly, the burden to fix them falls on your help desk, and app deployment is slow. To help you prevent these problems, you can use app configuration policies to deploy required settings to users before they run the app. The settings are associated with a user automatically. The user doesn't need to take any action.
To use an app configuration policy in Configuration Manager, instead of deploying the configuration policies directly to users and devices, you associate a policy with a deployment type when you deploy the app. The policy settings are applied whenever the app checks for them, typically the first time the app runs.

Android app configuration policies are available only on devices running Android for Work and apply to approved apps from the Play for Work store. For details about Android volume-purchased apps, see [How to deploy apps to Android for Work devices](https://docs.microsoft.com/en-us/intune/deploy-use/android-for-work-apps).

For more information about app installation types, see the [introduction to application management](/sccm/apps/understand/introduction-to-application-management).

## Create an app configuration policy

1. In the Configuration Manager console, choose **Software Library** > **Application Management** > **App Configuration Policies**.
2. On the **Home** tab, in the **App Configuration Policies** group, choose **Create App Configuration Policy**.
3. In the Create App Configuration Policy Wizard, on the **General** page, set this policy information:
  - **Name**. Enter a unique name for the policy.
  - **Description**. (Optional) To make it easier to identify the policy, you can add a description.
  -  **Select a configuration policy type**. Specify the platform targeted by the app configuration policy: **Configuration policy for Android for Work apps**.
  -  **Assigned categories to improve searching and filtering**. (Optional) To create and assign categories to the policy, choose **Categories**. Categories make it easier for you to sort and find items in the Configuration Manager console.
4. On the **Android for Work Policy** page, choose how to set the configuration policy information:
  - **Specify name and value pairs**. You can use this option for property list files that do not use nesting. To specify a name and value pair:
        1. To add a new JSON pair, choose **New**.
        2. In the **Add Name/Value Pair** dialog box, specify the following:
            - **Type**. From the list, select the type of value that you want to specify.
            - **Name**. Enter the name of the property list key for which you want to specify a value.
            - **Value**. Enter the value that will be applied to the key you entered.

  - **Browse to a property list JSON file**. Use this option if you already have an app configuration JSON file, or for more complex files that use nesting. In the **App configuration policy** field, enter the property list information in the correct JSON format.
5. To import a JSON file that you created earlier, choose **Select file**.
6. Choose **Next**. If there are errors in the JSON code, you'll have to correct them before you continue.
7. Finish the steps shown in the wizard.

The new app configuration policy is shown in the **Software Library** workspace, in the **App Configuration Policies** node.

## Associate an app configuration policy with a Configuration Manager application

To associate an app configuration policy with the deployment of an Android for Work app, deploy the application as you normally would by using the procedure in the [Deploy applications](/sccm/apps/deploy-use/deploy-applications) topic.

In the Deploy Software Wizard, on the **App Configuration Policies** page, choose **New**. In the **Select App Configuration Policy** dialog box, choose an application deployment type, and the app configuration policy that you want to associate it with.
When the deployment type is installed, the app configuration policy settings is automatically applied.
