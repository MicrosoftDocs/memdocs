---
title: "Protect apps using mobile application management policies"
titleSuffix: "Configuration Manager"
description: "Modify the functionality of apps that you deploy so they will meet your company compliance and security policies."
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Protect apps using mobile application management policies in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager application management policies let you modify the functionality of apps that you deploy to help bring them in line with your company compliance and security policies. For example, you can restrict cut, copy, and paste operations within a restricted app, or configure an app to open all URLs inside a managed browser. App management policies support:  

-   Devices that run Android 4 and later  

-   Devices that run iOS 9 and later  

You can also use mobile app management policies to protect apps on devices that are not managed by Intune. Using this new capability, you can apply mobile app management policies to apps that connect to Office 365 services. This is not supported for apps that connect to on-premises Exchange or SharePoint.  

To use this new capability, you need to use the Azure preview portal. The following topics can help you get started:  
- [Get started with mobile app management policies in the Azure portal](https://technet.microsoft.com/library/mt627830.aspx)  
- [Create and deploy mobile app management policies with Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

  You don't deploy an application management policy directly as you do with configuration items and baselines in Configuration Manager. Instead, you associate the policy with the application deployment type that you want to restrict. When the app deployment type is deployed and installed on devices, the settings you specify take effect.  

To apply restrictions to an app, the app must incorporate the Microsoft Intune App Software Development Kit (SDK). There are two methods of obtaining this type of app:  

-   **Use a policy managed app** (Android and iOS): These apps have the App SDK built in. To add this type of app, you specify a link to the app from an app store such as the iTunes store or Google Play. No further processing is required for this type of app. For a list of the policy managed apps that are available for iOS and Android devices, see [Managed apps for Microsoft Intune mobile application management policies](https://technet.microsoft.com/library/dn708489.aspx).  

-   **Use a "wrapped" app** (Android and iOS): These apps are repackaged to include the App SDK by using the **Microsoft Intune App Wrapping Tool**. This tool is typically used to process company apps that were created in-house. It cannot be used to process apps that were downloaded from the app store. See the following articles for more information:
    - [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/dn878028.aspx)

    - [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/mt147413.aspx)  

## Create and deploy an app with a mobile application management policy  

##  Step 1: Obtain the link to a policy managed app or create a wrapped app  

-   **To obtain a link to a policy managed app**: From the app store, find, and note the URL of the policy managed app you want to deploy.  

     For example, the URL of the Microsoft Word for iPad app is **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **To create a wrapped app**: Use the information in the topics [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/dn878028.aspx) and [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/mt147413.aspx) to create a wrapped app.  

     The tool creates a processed app and an associated manifest file. You use these files when you create a Configuration Manager application that contains the app.  

##  Step 2: Create a Configuration Manager application that contains an app  
 The procedure to create the Configuration Manager application differs depending on whether you are using a policy managed app (external link), or an app that was created by using the Microsoft Intune App Wrapping Tool for iOS (App package for iOS). Use one of the following procedures to create the Configuration Manager application.  

1. In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

2. In the **Home** tab, in the **Create** group, choose **Create Application** to open the **Create Application** Wizard.  

3. On the **General** page, select **Automatically detect information about this application from installation files**.  

4. In the **Type** drop-down list, select **App package for iOS (\*.ipa file)**.  

5. Choose **Browse** to select the app package you want to import, and then choose **Next**.  

6. On the **General Information** page, enter the descriptive text and category information that you want users to see in the company portal.  

7. Complete the wizard.  

   The new application is displayed in the **Applications** node of the **Software Library** workspace.  

### Create an application that contains a link to a policy managed app  

1. In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

2. In the **Home** tab, in the **Create** group, choose **Create Application** to open the **Create Application** Wizard.  

3. On the **General** page, select **Automatically detect information about this application from installation files**.  

4. In the **Type** drop-down, select one of the following:  

   -   For iOS: **App Package for iOS from App Store**  

   -   For Android: **App Package for Android on Google Play**  

5. Enter the URL for the app (from step 1), and then choose **Next**.  

6. On the **General Information** page, enter the descriptive text and category information that you want users to see in the company portal.  

7. Complete the wizard.  

   The new application is displayed in the **Applications** node of the **Software Library** workspace.  

##  Step 3: Create an application management policy  
 Next, create an application management policy that you associate with the application. You can create a general or managed browser policy.  

1)  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Application Management Policies**.  

2)  In the **Home** tab, in the **Create** group, choose **Create Application Management Policy**.  

3)  On the **General** page, enter the name and description for the policy, and then choose **Next**.  

4)  On the **Policy Type** page, select the platform and the policy type for this policy, and then choose **Next**. The following policy types are available:  

-   **General**: The General policy type lets you modify the functionality of apps that you deploy to help bring them in line with your company compliance and security policies. For example, you can restrict cut, copy, and paste operations within a restricted app.  

-   **Managed Browser**: The Managed Browser policy lets you decide whether to allow or block the managed browser from opening a list of URLs. The Managed Browser policy type lets you modify the functionality of the Intune Managed Browser app. This is a web browser that lets you manage the actions that users can perform, including the sites they can visit, and how links to content within the browser are opened. Learn more about the  [Intune Managed Browser app for iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [the Intune Managed Browser app for Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  On the **iOS Policy** or **Android Policy** page, configure the following values as required, and then choose **Next**. The options might differ depending on the device type for which you are configuring the policy.  

|Value|More information|  
|-----------|----------------------|  
|**Restrict web content to display in a corporate managed browser**|Enables all links in the app to open in the Managed Browser. You must have deployed this app to devices in order for this option to work.|  
|**Prevent Android backups** or **Prevent iTunes and iCloud backups**|Disables the backup of any information from the app.|  
|**Allow app to transfer data to other apps**|Specifies the apps that this app can send data to. You can choose to not allow data transfer to any app, to only allow transfer to other restricted apps, or to allow transfer to any app.<br /><br /> For iOS devices, to prevent document transfer between managed and unmanaged apps, you must also configure and deploy a mobile device security policy that disables the setting **Allow managed documents in other unmanaged apps**.<br /><br /> If you select to only allow transfer to other restricted apps, the Intune PDF and image viewers (if deployed) are used to open content of the respective types.|  
|**Allow app to receive data from other apps**|Specifies the apps that this app can receive data from. You can choose to not allow data transfer from any app, to only allow transfer from other restricted apps, or to allow transfer from any app.|  
|**Prevent “Save As”**|Disables the use of the **Save As** option in any app that uses this policy.|  
|**Restrict cut, copy and paste with other apps**|Specifies how cut, copy, and paste operations can be used with the app. Choose from:<br /><br /> **Blocked** – Doesn't allow cut, copy, and paste operations between this app and other apps.<br /><br /> **Policy Managed Apps** – Allows cut, copy, and paste operations between only this app and other restricted apps.<br /><br /> **Policy Managed Apps with Paste In** – Allows data that's cut or copied from this app only to be pasted into other restricted apps. Allows data that is cut or copied from any app to be pasted into this app.<br /><br /> **Any App** – No restrictions to cut, copy, and paste operations to or from this app.|  
|**Require simple PIN for access**|Requires the user to enter a PIN that they specify to use this app. The user is asked to set this up the first time they run the app.|  
|**Number of attempts before PIN reset**|Specifies the number of PIN entry attempts that can be made before the user must reset the PIN.|  
|**Require corporate credentials for access**|Requires that the user must enter their corporate sign-in information before they can access the app.|  
|**Require device compliance with corporate policy for access**|Allows the app to be used only when the device is not jailbroken or rooted.|  
|**Recheck the access requirements after (minutes)**|Specifies the time period before the access requirements for the app are rechecked after the app is launched (in the **Timeout** field).<br /><br /> In the **Offline grace period** field, if the device is offline, specifies the time period before the access requirements for the app are rechecked.|  
|**Encrypt app data**|Specifies that all data that is associated with this app is encrypted, including data that's stored externally, such as data stored on SD cards.<br /><br /> **Encryption for iOS**<br /><br /> For apps that are associated with a Configuration Manager mobile application management policy, data is encrypted at rest using device-level encryption that's provided by the OS. This is enabled through a device PIN policy that must be set by the IT admin. When a PIN is required, the data is encrypted per the settings in the mobile application management policy. As stated in Apple documentation, [the modules that are used by iOS 7 are FIPS 140-2 certified](http://support.apple.com/en-us/HT202739).<br /><br /> **Encryption for Android**<br /><br /> For apps that are associated with a Configuration Manager mobile application management policy, encryption is provided by Microsoft. Data is encrypted synchronously during file I/O operations according to the setting in the mobile application management policy. Managed apps on Android use AES-128 encryption in CBC mode utilizing the platform cryptography libraries. The encryption method is not FIPS 140-2 certified. Content on the device storage is always encrypted.|  
    |**Block screen capture** (Android devices only)|Specifies that the screen capture capabilities of the device are blocked when using this app.|  
    |**Disable contact sync**| Beginning with version 1710, this option prevents the app from saving data to the native Contacts app on the device. If you choose No, the app can save data to the native Contacts app on the device.|  
    |**Disable printing**| Beginning with version 1710, this option prevents the app from printing work or school data. |  

6)  On the **Managed Browser** page, select whether the managed browser is allowed to open only URLs in the list or to block the managed browser from opening the URLs in the list, and then choose **Next**.  
For more information, see [Manage Internet access using managed browser policies](manage-internet-access-using-managed-browser-policies.md).  

7)  Complete the wizard.  

 The new policy is displayed in the **Application Management Policies** node of the **Software Library** workspace.  

##  Step 4: Associate the application management policy with a deployment type  

 When a deployment type is created for an app that requires an application management policy, Configuration Manager recognizes this and prompts you to associate an app management policy. For the Managed Browser, you are required to associate both a General and Managed Browser policy. For more information, see [Create applications](create-applications.md).  

> [!IMPORTANT]  
>  If the application is already deployed, then the deployment for the new deployment type fails until this association is made. You can make the association in **Properties** for the application, on the **Application Management** tab.  

> [!IMPORTANT]  
>  For devices that run operating systems earlier than iOS 7.1, associated policies aren't removed when the app is uninstalled.  
>   
>  If the device is unenrolled from Configuration Manager, polices are not removed from the apps. Apps that had policies applied  retain the policy settings even after the app is uninstalled and reinstalled.  

##  Step 5: Monitor the app deployment  
 Once you have created and deployed an app that's associated with a mobile application management policy, you can monitor the app and resolve any policy conflicts.  

1. In the Configuration Manager console, choose **Software Library** > **Overview** > **Deployments**.  

2. Select the deployment that you created. Then, on the **Home** tab, choose **Properties**.  

3. In the details pane for the deployment, under **Related Objects**, choose **Application Management Policies**.  

   For more information about monitoring applications, see [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  Learn how policy conflicts are resolved  
 When there is a mobile application management policy conflict on the first deployment to the user or device, the specific setting value that's in conflict is removed from the policy that's deployed to the app. Then the app uses a built-in conflict value.  

 When there is a mobile app management policy conflict on later deployments to the app or user, the specific setting value that's in conflict is not  updated on the mobile app management policy that's deployed to the app, and the app uses the existing value for that setting.  

 In cases where the device or user receives two conflicting policies, the following behavior applies:  

-   If a policy has yet been deployed to the device, the existing policy settings are not overwritten.  

-   If no policy has already been deployed to the device, and two conflicting settings are deployed, the default setting that's built into the device is used.  

##  See a list of available policy managed apps  
 For a list of the policy managed apps that are available for iOS and Android devices, see [Microsoft Intune application partners](https://www.microsoft.com/cloud-platform/microsoft-intune-partners).  
