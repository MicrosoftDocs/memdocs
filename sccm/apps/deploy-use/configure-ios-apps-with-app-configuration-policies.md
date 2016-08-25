---
title: "Configure iOS apps with app configuration policies in System Center Configuration Manager"
ms.custom: na
ms.date: 2016-04-03
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Configure iOS apps with app configuration policies in System Center Configuration Manager
||  
|-|  
|This article contains information about [new functionality introduced in version 1602](https://technet.microsoft.com/library/mt622084.aspx) of System Center Configuration Manager \(current branch\). To use the new functionality, you must [install the 1602 update](https://technet.microsoft.com/library/mt607046.aspx). If you have not updated to the most recent version of Configuration Manager, you can [download the documentation for the version you use](https://gallery.technet.microsoft.com/Documentation-for-System-ea90eaf1) from the TechNet Gallery.|  
  
 Use app configuration policies in System Center Configuration Manager to supply settings that might be required when the user runs an app. For example, an app might require the user to specify:  
  
-   A custom port number  
  
-   Language settings  
  
-   Security settings  
  
-   Branding settings such as a company logo  
  
 If these settings are incorrectly entered by the user, this can increase the burden on your help desk, and also slow the adoption of new apps.  
  
 App configuration policies can help you eliminate these problems by letting you deploy these settings to users in a policy before they run the app. The settings are then supplied automatically, and the user needs to take no action.  
  
 You do not deploy these policies directly to users and devices. Instead, you associate the policy with a deployment type when you  deploy the application. The policy settings will be used whenever the app checks for them (typically, the first time it is run).  
  
> [!TIP]  
>  App configuration policies are  currently available only on devices running iOS 7.1 and later and support the following application types:  
>   
>  -   **App Package for iOS (\*.ipa file)**  
> -   **App Package for iOS from App Store**  
>   
>  For more information about app installation types, see [Get started with application management in System Center Configuration Manager](../../apps/understand/get-started-with-application-management.md).  
  
## Create an app configuration policy  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **App Configuration Policies**.  
  
3.  On the **Home** tab, in the **App Configuration Policies** group, click **Create new Application Configuration Policy**.  
  
4.  On the **General** page of the **Create App Configuration Policy Wizard**, specify the following information:  
  
    -   **Name:** Specify a unique name for the policy.  
  
    -   **Description:** Optionally, specify a description for the policy that helps you to identify it.  
  
    -   **Assigned categories to improve searching and filtering:** Optionally, click **Categories** to create and assign categories to the policy. This makes it easier for you to sort and find items in the Configuration Manager console.  
  
5.  On the **iOS Policy** page of the wizard, choose how you will specify the configuration policy information:  
  
    -   **Specify name and value pairs**: You can use this option for property list files that do not use nesting.  
  
        ###### To specify name and value pairs  
  
        1.  To add a new pair, click **New**.  
  
        2.  In the **Add Name/Value Pair** dialog box, specify the following:  
  
            -   **Type:** From the list, choose the type of value you want to specify.  
  
            -   **Name:** Enter the name of the property list key for which you want to specify a value.  
  
            -   **Value:** Enter the value that will be applied to the key you entered.  
  
    -   **Browse to a property list file:** Use this option if you already have an app configuration XML file, or for more complex files that use nesting.  
  
        ###### To browse to a property list file  
  
        1.  In the **App configuration policy** field, enter the property list information in the correct XML format.  
  
            > [!TIP]  
            >  To find out more about XML property lists, see [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) in the iOS Developer Library.  
            >   
            >  The format of the XML property list will vary depending on the app you are configuring. Contact the supplier of the app for details about the exact format to use.  
            >   
            >  Intune supports the following data types in a property list:  
            >   
            >  -   <integer\>  
            > -   <real\>  
            > -   <string\>  
            > -   <array\>  
            > -   <dict\>  
            > -   <true /\> or <false /\>  
            >   
            >  For more information about data types, see [About Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) in the iOS Developer Library.  
            >   
            >  Additionally, Intune supports the following token types in the property list:  
            >   
            >  -   {{userprincipalname}} - (Example: **John@contoso.com**)  
            > -   {{mail}} - (Example: **John@contoso.com**)  
            > -   {{partialupn}} - (Example: **John**)  
            > -   {{accountid}} - (Example: **fc0dc142-71d8-4b12-bbea-bae2a8514c81**)  
            > -   {{deviceid}} - (Example: **b9841cd9-9843-405f-be28-b2265c59ef97**)  
            > -   {{userid}} - (Example: **3ec2c00f-b125-4519-acf0-302ac3761822**)  
            > -   {{username}} - (Example: **John Doe**)  
            > -   {{serialnumber}} - (Example: **F4KN99ZUG5V2**) for iOS devices  
            > -   {{serialnumberlast4digits}} - (Example: **G5V2**) for iOS devices  
            >   
            >  The {{ and }} characters are used by token types only and must not be used for other purposes.  
  
             You can also click **Select file** to import an XML file you have previously created.  
  
        2.  Click **Next**. If there are errors in the XML code, you will have to correct these before you continue.  
  
6.  Complete the wizard.  
  
 The new app configuration policy is displayed in the **App Configuration Policies** node of the **Software Library** workspace.  
  
## Associate an app configuration policy with a Configuration Manager application  
 To associate an app configuration policy with the deployment of an iOS app, you deploy the application as you normally would using the procedure in the [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) topic.  
  
 On the **App Configuration Policies** page of the **Deploy Software Wizard**, click **New**. Then, in the **Select App Configuration Policy** dialog box, choose an application deployment type and an app configuration policy you want to associate it with.  
  
 When the deployment type is installed the app configuration policy settings will be automatically applied.  
  
## Example format for the mobile app configuration XML file  
 When you create a mobile app configuration file, you can specify one or more of the following values using this format:  
  
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
  
## See Also  
 [Manage and protect apps with System Center Configuration Manager](../Topic/Manage%20and%20protect%20apps%20with%20System%20Center%20Configuration%20Manager.md)