---
title: "Manage Internet access using managed browser policies | System Center Configuration Manager"
description: "Deploy the Intune Managed Browser to manage and restrict Internet access."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 735c45b8-a545-4805-84e5-46204fabd1a6
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft

---
# Manage Internet access using managed browser policies with System Center Configuration Manager
In System Center Configuration Manager, you can deploy the Intune Managed Browser, a web browsing application, and associate the application with a managed browser policy. The managed browser policy configures an allow list or a block list that restricts the web sites that users of the managed browser can visit.  

 Because this app is a managed app, you can also apply mobile application management policies to the app, such as controlling the use of cut, copy and paste, preventing screen captures, and also ensuring that links to content that users click only open in other managed apps. For details, see [Protect apps using mobile application management policies in System Center Configuration Manager](../../apps/deploy-use/protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  If users install the managed browser themselves, it will not be managed by any policies you specify. To ensure that the browser is managed by Configuration Manager, they must uninstall the app before you can deploy it to them as a managed app.  

 You can create managed browser policies for the following device types:  

-   Devices that run Android 4 and later  

-   Devices that run iOS 7 and later  

> [!NOTE]  
>  For more information about the Intune Managed Browser app, see [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) for iOS and [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) for Android.  

## Create a managed browser policy  

1.  In the Configuration Manager console, click **Software Library** > **Application Management** > **Application Management Policies**.  

3.  In the **Home** tab, in the **Create** group, click **Create Application Management Policy**.  

4.  On the **General** page, enter the name and description for the policy, and then click **Next**.  

5.  On the **Policy Type** page, select the platform, select **Managed Browser** for the policy type, and then click **Next**.  

     On the **Managed Browser** page, select one of the following options:  

    -   **Allow the managed browser to open only the URLs listed below** – Specify a list of URLs that the managed browser can open.  

    -   **Block the managed browser from opening the URLs listed below** – Specify a list of URLs that the managed browser will be blocked from opening.  

    > [!NOTE]  
    >  You cannot include both allowed and blocked URLs in the same managed browser policy.  

     For more information about the URL formats you can specify, see [URL format for allowed and blocked URLs](#BKMK_URLs) in this topic.  

    > [!NOTE]  
    >  The **General** policy type lets you modify the functionality of apps that you deploy to help bring them into line with your company compliance and security policies. For example, you can restrict cut, copy and paste operations within a restricted app. For more information about the General policy type, see [Protect apps using mobile application management policies in System Center Configuration Manager](../../apps/deploy-use/protect-apps-using-mam-policies.md).  

6.  Complete the wizard.  

 The new policy is displayed in the **Application Management Policies** node of the **Software Library** workspace.  

## Create a software deployment for the managed browser app  
 After you have created the managed browser policy, you can then create a software deployment type for the managed browser app. You must associate both a General and Managed Browser policy for the Managed Browser app.  

 For more information, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

## Security and privacy for the managed browser  

-   On iOS devices, web sites that users visit that have an expired or untrusted certificate cannot be opened.  

-   Settings that users make for the built-in browser on their devices are not used by the managed browser. This is because the managed browser does not have access to these settings.  

-   If you configure the options **Require simple PIN for access** or **Require corporate credentials for access** in a mobile application management policy associated with the managed browser and a user clicks the help link on the authentication page, they can then browse any Internet sites regardless of whether they were added to a block list in the managed browser policy.  

-   The managed browser can only block access to sites when they are accessed directly. It cannot block access when intermediate services (such as a translation service) are used to access the site.  

## Reference information  

###  <a name="BKMK_URLs"></a> URL format for allowed and blocked URLs  
 Use the following information to learn about the allowed formats and wildcards you can use when specifying URLs in the allowed and blocked lists.  

-   You can use the wildcard symbol ‘**\***’ according to the rules in the permitted patterns list below.  

-   Ensure that you prefix all URLs with **http** or **https** when entering them into the list.  

-   You can specify port numbers in the address. If you do not specify a port number, the values used will be:  

    -   Port 80 for http  

    -   Port 443 for https  

     Using wildcards for the port number is not supported, for example, **http://www.contoso.com:\*** and **http://www.contoso.com: /\***  

-   Use the following table to learn about the permitted patterns you can use when you specify URLs:  

    |URL|Matches|Does not match|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Matches a single page|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Matches a single page|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Matches all URLs beginning with www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Matches all sub-domains under contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Matches a single folder|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Matches a single page, using a port number|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Matches a single, secure page|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Matches a single folder and all subfolders|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   The following are examples of some of the inputs you cannot specify:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   IP addresses  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: /*  

> [!NOTE]  
>  *.microsoft.com is always allowed – it is always treated as allowed.  

### How conflicts between the allow and block list are resolved  
 If multiple managed browser policies are deployed to a device and the settings conflict, both the mode (allow or block) and the URL lists are evaluated for conflicts. In case of a conflict, the following behavior applies:  

-   If the modes in each policy are the same, but the URL lists are different, the URLs will not be enforced on the device.  

-   If the modes in each policy are different, but the URL lists are the same, the URLs will not be enforced on the device.  

-   If a device is receiving managed browser policies for the first time and two policies conflict, the URLs will not be enforced on the device. Use the **Policy Conflicts** node of the **Policy** workspace to view the conflicts.  

-   If a device has already received a managed browser policy and a second policy is deployed with conflicting settings, the original settings remain on the device. Use the **Policy Conflicts** node of the **Policy** workspace to view the conflicts.  
