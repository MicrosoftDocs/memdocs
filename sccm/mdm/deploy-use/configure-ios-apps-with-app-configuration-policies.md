---
title: "Configure iOS apps with app configuration policies"
titleSuffix: "Configuration Manager"
description: "Help eliminate configuration problems on devices running iOS 8 or later by deploying app configuration policies to users before they run apps."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Apply settings to iOS apps with app configuration policies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


You can use app configuration policies in System Center Configuration Manager (Configuration Manager) to distribute settings that might be required when a user runs an app. For example, an app might require a user to specify these details:
- A custom port number
- Language settings
- Security settings
- Branding settings, like a company logo

If the user enters the settings incorrectly, the burden to fix them falls on your help desk, and app deployment is slow.
To help you prevent these problems, you can use app configuration policies to deploy required settings to users before they run the app. The settings are associated with a user automatically. The user doesn't need to take any action.
To use an app configuration policy in Configuration Manager, instead of deploying the configuration policies directly to users and devices, you associate a policy with a deployment type when you deploy the app. The policy settings are applied whenever the app checks for them (typically, the first time the app runs).

Currently, app configuration policies are available only on devices running iOS 8 and later, and for these application types:

- **app package for iOS (*.ipa file)**
- **app package for iOS from App Store**

For more information about app installation types, see the [introduction to application management](/sccm/apps/understand/introduction-to-application-management).

## Create an app configuration policy

1. In the Configuration Manager console, choose **Software Library** > **Application Management** > **App Configuration Policies**.
2. On the **Home** tab, in the **App Configuration Policies** group, choose **Create new Application Configuration Policy**.
3. In the Create App Configuration Policy Wizard, on the **General** page, set this policy information:
   - **Name**. Enter a unique name for the policy.
   - **Description**. (Optional) To make it easier to identify the policy, you can add a description.
   - **Assigned categories to improve searching and filtering**. (Optional) To create and assign categories to the policy, choose **Categories**. Categories make it easier for you to sort and find items in the Configuration Manager console.
4. On the **iOS Policy** page, choose how to set the configuration policy information:
   - **Specify name and value pairs**. You can use this option for property list files that do not use nesting.

      *To specify a name and value pair*
        1. To add a new pair, choose **New**.
        2. In the **Add Name/Value Pair** dialog box, specify the following:
            - **Type**. From the list, select the type of value that you want to specify.
            - **Name**. Enter the name of the property list key for which you want to specify a value.
            - **Value**. Enter the value that will be applied to the key you entered.

   - **Browse to a property list file**. Use this option if you already have an app configuration XML file, or for more complex files that use nesting.

     *To browse to a property list file*

     1. In the **App configuration policy** field, enter the property list information in the correct XML format.

        To find out more about XML property lists, see [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) in the iOS Developer Library.

The format of the XML property list varies depending on the app you are configuring. Contact the app supplier for details about the format to use.
Intune supports the following data types in a property list:
			
            ```
			<integer>
			<real>
			<string>
			<array>
			<dict>
			<true /> or <false />
            ```
For more information about data types, see [About Property Lists](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) in the iOS Developer Library.
Intune also supports the following token types in the property list:
			
            ```
			{{userprincipalname}} - (Example: John@contoso.com)
			{{mail}} - (Example: John@contoso.com)
			{{partialupn}} - (Example: John)
			{{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
			{{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
			{{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
			{{username}} - (Example: John Doe)
			{{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
			{{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

The {{ and }} characters are used by token types only and must not be used for other purposes.
			
5. To import an XML file that you created earlier, choose **Select file**.
6. Choose **Next**. If there are errors in the XML code, you'll have to correct them before you continue.
7. Finish the steps shown in the wizard.

The new app configuration policy is shown in the **Software Library** workspace, in the **App Configuration Policies** node.

## Associate an app configuration policy with a Configuration Manager application

To associate an app configuration policy with the deployment of an iOS app, deploy the application as you normally would by using the procedure in the [Deploy applications](/sccm/apps/deploy-use/deploy-applications) topic.

In the Deploy Software Wizard, on the **App Configuration Policies** page, choose **New**. In the **Select App Configuration Policy** dialog box, choose an application deployment type, and the app configuration policy that you want to associate it with.
When the deployment type is installed, the app configuration policy settings is automatically applied.

## Example format for the mobile app configuration XML file

When you create a mobile app configuration file, you can use this format to specify one or more of the following values:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```
