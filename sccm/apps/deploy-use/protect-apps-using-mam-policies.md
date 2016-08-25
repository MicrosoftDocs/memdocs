---
title: "Protect apps using mobile application management policies in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
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
# Protect apps using mobile application management policies in System Center Configuration Manager
System Center Configuration Manager application management policies let you modify the functionality of apps that you deploy to help bring them into line with your company compliance and security policies. For example, you can restrict cut, copy, and paste operations within a restricted app, or configure an app to open all web links inside a managed browser. App management policies support:  
  
-   Devices that run Android 4 and later.  
  
-   Devices that run iOS 7 and later.  
  
> [!TIP]  
>  In addition to managed devices, you can use mobile app management policies to protect apps on devices that are not managed by Intune. Using this new capability, you can apply mobile app management policies for apps connecting to Office 365 services. This is not supported for apps connecting to on-premises Exchange or SharePoint.  
>   
>  To use this new capability, you must use the Azure preview portal. The following topics can help you get started:  
>   
>  -   [Get started with mobile app management policies in the Azure portal](https://technet.microsoft.com/library/mt627830.aspx)  
> -   [Create and deploy mobile app management policies with Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  
  
 Unlike configuration items and baselines in Configuration Manager, you do not deploy an application management policy directly. Instead, you associate the policy with the application deployment type that you want to restrict. When the app deployment type is deployed and installed on devices, the settings you specify will take effect.  
  
 To apply restrictions to an app, the app must incorporate the Microsoft Intune App Software Development Kit (SDK). There are two methods of obtaining this type of app:  
  
-   **Use a policy managed app** (Android and iOS): Has the App SDK built-in. To add this type of app, you specify a link to the app from an app store such as the iTunes store or Google Play. No further processing is required for this type of app. For a list of the policy managed apps that are available for iOS and Android devices, see [Managed apps for Microsoft Intune mobile application management policies](https://technet.microsoft.com/en-us/library/dn708489.aspx).  
  
-   **Use a ‘wrapped’ app** – (Android and iOS): Apps that are repackaged to include the App SDK by using the **Microsoft Intune App Wrapping Tool**. This tool is typically used to process company apps that were created in-house. It cannot be used to process apps that were downloaded from the app store. See [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) and [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx).  
  
## Create and deploy an app with a mobile application management policy  
  
-   [Step 1: Obtain the link to a policy managed app, or create a wrapped app](#BKMK_Step1)  
  
-   [Step 2: Create a Configuration Manager application that contains an app](#BKMK_Step2)  
  
-   [Step 3: Create an application management policy](#bkmk_step3)  
  
-   [Step 4: Associate the application management policy with a deployment type](#BKMK_Step4)  
  
-   [Step 5: Monitor the app deployment](#BKMK_Step5)  
  
##  <a name="BKMK_Step1"></a> Step 1: Obtain the link to a policy managed app, or create a wrapped app  
  
-   **To obtain a link to a policy managed app** - From the app store, find, and note the URL of the policy managed app you want to deploy.  
  
     For example, the URL of the Microsoft Word for iPad app is **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  
  
-   **To create a wrapped app** - Use the information in the topics [Prepare iOS apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) and [Prepare Android apps for mobile application management with the Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx) to create a wrapped app.  
  
     The tool creates a processed app and an associated manifest file. You will use these files when you create a Configuration Manager application containing the app.  
  
##  <a name="BKMK_Step2"></a> Step 2: Create a Configuration Manager application that contains an app  
 The procedure to create the Configuration Manager application differs depending on whether you are using a policy managed app (external link), or an app that was created by using the Microsoft Intune App Wrapping Tool for iOS (App package for iOS). Use one of the following procedures to create the Configuration Manager application.  
  
#### To create an application for an app wrapping tool for iOS app  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **Applications**.  
  
3.  In the **Home** tab, in the **Create** group, click **Create Application** to open the Create Application Wizard.  
  
4.  On the **General** page, select **Automatically detect information about this application from installation files**.  
  
5.  In the **Type** drop-down list, select **App package for iOS (\*.ipa file)**.  
  
6.  Click **Browse** to select the app package you want to import, and then click **Next**.  
  
7.  On the **General Information** page, enter the descriptive text and category information that you want users to see in the company portal.  
  
8.  Complete the wizard.  
  
 The new application is displayed in the **Applications** node of the **Software Library** workspace.  
  
#### To create an application containing a link to a policy managed app  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **Applications**.  
  
3.  In the **Home** tab, in the **Create** group, click **Create Application** to open the Create Application Wizard.  
  
4.  On the **General** page, select **Automatically detect information about this application from installation files**.  
  
5.  In the **Type** drop-down, select one of the following:  
  
    -   For iOS: **App Package for iOS from App Store**  
  
    -   For Android: **App Package for Android on Google Play**  
  
6.  Enter the URL for the app (from step 1), and then click **Next**.  
  
7.  On the **General Information** page, enter the descriptive text and category information that you want users to see in the company portal.  
  
8.  Complete the wizard.  
  
 The new application is displayed in the **Applications** node of the **Software Library** workspace.  
  
##  <a name="bkmk_step3"></a> Step 3: Create an application management policy  
 Next, you create an application management policy that you will associate with the application. You can create a general or managed browser policy.  
  
#### To create an application management policy  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **Application Management Policies**.  
  
3.  In the **Home** tab, in the **Create** group, click **Create Application Management Policy**.  
  
4.  On the **General** page, enter the name and description for the policy, and then click **Next**.  
  
5.  On the **Policy Type** page, select the platform and the policy type for this policy, and then click **Next**. The following policy types are available:  
  
    -   **General**: The General policy type lets you modify the functionality of apps that you deploy to help bring them into line with your company compliance and security policies. For example, you can restrict cut, copy, and paste operations within a restricted app.  
  
    -   **Managed Browser**: Configure whether to allow or block the managed browser from opening a list of URLs. The Managed Browser policy type lets you modify the functionality of the Intune Managed Browser app. This is a web browser that lets you manage the actions that users can perform, including the sites they can visit, and how links to content within the browser are opened. Learn more about the  [Intune Managed Browser app for iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [the Intune Managed Browser app for Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).  
  
6.  On the **iOS Policy** or **Android Policy** page, configure the following values as required, and then click **Next**. The options might differ depending on the device type for which you are configuring the policy.  
  
    |Value|More information|  
    |-----------|----------------------|  
    |**Restrict web content to display in a corporate managed browser**|When this setting is enabled, any links in the app will be opened in the Managed Browser. You must have deployed this app to devices in order for this option to work.|  
    |**Prevent Android backups** or **Prevent iTunes and iCloud backups**|Disables the backup of any information from the app.|  
    |**Allow app to transfer data to other apps**|Specifies the apps that this app can send data to. You can choose to not allow data transfer to any app, only allow transfer to other restricted apps, or to allow transfer to any app.<br /><br /> For iOS devices, to prevent document transfer between managed and unmanaged apps, you must also configure and deploy a mobile device security policy that disables the setting **Allow managed documents in other unmanaged apps**.<br /><br /> If you select to only allow transfer to other restricted apps, the Intune PDF and image viewers (if deployed) will be used to open content of the respective types.|  
    |**Allow app to receive data from other apps**|Specifies the apps that this app can receive data from. You can choose to not allow data transfer from any app, only allow transfer from other restricted apps, or allow transfer from any app.|  
    |**Prevent “Save As”**|Disables use of the **Save As** option in any app that uses this policy.|  
    |**Restrict cut, copy and paste with other apps**|Specifies how cut, copy, and paste operations can be used with the app. Choose from:<br /><br /> **Blocked** – Do not allow cut, copy, and paste operations between this app and other apps.<br /><br /> **Policy Managed Apps** – Only allow cut, copy, and paste operations between this app and other restricted apps.<br /><br /> **Policy Managed Apps with Paste In** – Allow data cut or copied from this app only to be pasted into other restricted apps. Allow data cut or copied from any app to be pasted into this app.<br /><br /> **Any App** – No restrictions to cut, copy, and paste operations to, or from this app.|  
    |**Require simple PIN for access**|Requires the user to enter a PIN number which they specify to use this app. The user will be asked to set this up the first time they run the app.|  
    |**Number of attempts before PIN reset**|Specify the number of PIN entry attempts which can be made before the user must reset the PIN.|  
    |**Require corporate credentials for access**|Requires that the user must enter their corporate logon information before they can access the app.|  
    |**Require device compliance with corporate policy for access**|Only allows the app to be used when the device is not jailbroken or rooted.|  
    |**Recheck the access requirements after (minutes)**|In the **Timeout** field, specify the time period before the access requirements for the app are rechecked after the app is launched.<br /><br /> In the **Offline grace period** field, if the device is offline, specify the time period before the access requirements for the app are rechecked.|  
    |**Encrypt app data**|Specifies that all data associated with this app will be encrypted, including data stored externally, such as SD cards.<br /><br /> **Encryption for iOS**<br /><br /> For apps that are associated with a Configuration Manager mobile application management policy, data is encrypted at rest using device level encryption provided by the OS. This is enabled through device PIN policy that must be set by the IT admin. When a PIN is required, the data will be encrypted per the settings in the mobile application management policy. As stated in Apple documentation, [the modules used by iOS 7 are FIPS 140-2 certified](http://support.apple.com/en-us/HT202739).<br /><br /> **Encryption for Android**<br /><br /> For apps that are associated with a Configuration Manager mobile application management policy, encryption is provided by Microsoft. Data is encrypted synchronously during file I/O operations according to the setting in the mobile application management policy. Managed apps on Android use AES-128 encryption in CBC mode utilizing the platform cryptography libraries. The encryption method is not FIPS 140-2 certified. Content on the device storage will always be encrypted.|  
    |**Block screen capture** (Android devices only)|Specifies that the screen capture capabilities of the device are blocked when using this app.|  
  
7.  On the **Managed Browser** page, select whether the managed browser is allowed to open only URLs in the list or to block the managed browser from opening the URLs in the list, manage the URLs in the list, and then click **Next**.  
  
    > [!WARNING]  
    >  For more information, see [Manage Internet access using managed browser policies with System Center Configuration Manager](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  
  
8.  Complete the wizard.  
  
 The new policy is displayed in the **Application Management Policies** node of the **Software Library** workspace.  
  
##  <a name="BKMK_Step4"></a> Step 4: Associate the application management policy with a deployment type  
 When a deployment type is created for an app that requires an application management policy, Configuration Manager will recognize that an app management policy must be linked to this deployment type when the associated app gets deployed and prompt you to associate an app management policy. For the Managed Browser, you will be required to associate both a General and Managed Browser policy. For more information, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  If the application is already deployed, then the deployment for the new deployment type will fail until this association is made. You can make the association in **Properties** for the application, on the **Application Management** tab.  
  
> [!IMPORTANT]  
>  For devices that run operating systems earlier than iOS 7.1, associated policies will not be removed when the app is uninstalled.  
>   
>  If the device is unenrolled from Configuration Manager, polices are not removed from the apps. Apps that had policies applied will retain the policy settings even after the app is uninstalled and reinstalled.  
  
##  <a name="BKMK_Step5"></a> Step 5: Monitor the app deployment  
 Once you have created and deployed an app associated with a mobile application management policy, you can monitor the app and resolve any policy conflicts.  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Monitoring** workspace, expand **Overview**, and then click **Deployments**.  
  
3.  Select the deployment and on the **Home** tab, click **Properties**.  
  
4.  In the details pane for the deployment, click **Application Management Policies** under **Related Objects**.  
  
 For more information about monitoring applications, see [Monitor applications with System Center Configuration Manager](../Topic/Monitor%20applications%20with%20System%20Center%20Configuration%20Manager.md).  
  
###  <a name="BKMK_Conf"></a> How policy conflicts are resolved  
 When there is a mobile application management policy conflict on the first deployment to the user or device, the specific setting value in conflict will be removed from the policy deployed to the app, and the app will use a built-in conflict value.  
  
 When there is a mobile app management policy conflict on later deployments to the app or user, the specific setting value in conflict will not be updated on the mobile app management policy deployed to the app, and the app will use the existing value for that setting.  
  
 In cases where the device or user receives two conflicting policies, the following behavior applies:  
  
-   If a policy has already been deployed to the device, the existing policy settings are not overwritten.  
  
-   If no policy has already been deployed to the device, and two conflicting settings are deployed, the default setting built into the device is used.  
  
###  <a name="BKMK_Availapps"></a> Available policy managed apps  
 For a list of the policy managed apps that are available for iOS and Android devices, see [Managed apps for Microsoft Intune mobile application management policies](https://technet.microsoft.com/en-us/library/dn708489.aspx).  
  
## See Also  
 [Manage and protect apps with System Center Configuration Manager](../Topic/Manage%20and%20protect%20apps%20with%20System%20Center%20Configuration%20Manager.md)