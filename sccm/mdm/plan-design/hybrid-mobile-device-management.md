---
title: "Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune"
description: "Walk through how to configure System Center Configuration Manager to manage mobile devices with Microsoft Intune."
ms.custom: na
ms.date: 05/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarnms.author: nathbarnmanager: angrobe

---
# Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune
This walkthrough shows you how to configure System Center Configuration Manager to manage iOS, Android (including Samsung KNOX), Windows Phone, and Windows devices with the Microsoft Intune online service over the Internet. Although you use the Intune service, management tasks are done using the service connection point site system role in the Configuration Manager console.  

 You can configure Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned mobile devices and giving them access to company data. When you use Configuration Manager with Intune, you have the following management capabilities on devices:  

-   Retire and wipe devices  

-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication  

-   Deploy line of business apps to devices  

-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play  

-   Collect hardware inventory  

-   Collect software inventory by using built-in reports  

 To read about what new features are available for hybrid MDM, see [What's new in hybrid mobile device management with System Center Configuration Manager and Microsoft Intune](../../mdm/understand/whats-new-in-hybrid-mobile-device-management.md).  

 This document assumes that you are using Configuration Manager to manage computers, and that you are interested in extending the Configuration Manager console with Intune to manage mobile devices. To understand the differences between  Intune and hybrid mobile device management, see [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager](../../mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management.md).  

 After extending Configuration Manager with Intune, you can give users permission to enroll their personal devices or enroll and manage corporate-owned devices. You can also manage company-owned devices with Intune using Configuration Manager. See [Enroll company-owned devices for hybrid deployments with Configuration Manager](../../mdm/deploy-use/enroll-company-owned-devices.md).  

 Use the following sections to help you manage mobile devices.  

##  <a name="bkmk_preq"></a> Prerequisites  
 Use the following information to determine the prerequisites for managing mobile devices.  

###  <a name="BKMK_ADmin"></a> Dependencies external to Configuration Manager  
 If necessary, take the following steps to satisfy any dependencies external to Configuration Manager:  

1.  Make sure that you have a publicly registered domain name and each user has a public domain UPN  that can be verified by Intune. GoDaddy or Symantec are typical examples of companies that provide domain names.  

     Before synchronizing the Active Directory user account, you must verify that user accounts have a public domain UPN. For more information, see [Add User Principal Name Suffixes](http://go.microsoft.com/fwlink/?LinkID=271122) in the Active Directory documentation library.  

     You can create a Configuration Manager custom report to verify that the UPN of the users who are discovered is consistent with the Intune Account Portal by using the following SQL query:  

    ```  
    SELECT UserPrincipalName,   
    COUNT(*) AS NumOfOccurances FROM (SELECT RIGHT(User_Principal_Name0,   
    LEN(User_Principal_Name0)-PATINDEX('%@%',   
    User_Principal_Name0)) AS UserPrincipalName FROM CM_EC1.dbo.v_R_User)   
    AS sub GROUP BY UserPrincipalName  
    ```  

2.  Optional, but strongly recommended: Deploy and configure Active Directory Federated Services (AD FS).  

     When you set up single sign-on, your users can sign in with their corporate credentials to access the services in Intune.  

     For more information, see the following topics:  

    -   [Prepare for single sign-on](http://go.microsoft.com/fwlink/?LinkID=271124)  

    -   [Plan for and deploy AD FS 2.0 for use with single sign-on](http://go.microsoft.com/fwlink/?LinkID=271125)  

3.  Deploy and configure directory synchronization.  

     Directory synchronization lets you populate Intune with synchronized user accounts. The synchronized user accounts and security groups are added to Intune. Failure to enable Directory Synchronization is a common cause of devices not being able to enroll when setting up Configuration Manager MDM with Microsoft Intune.  

     For more information, see [Directory integration](http://go.microsoft.com/fwlink/?LinkID=271120) in the Active Directory documentation library.  

4.  Optional, not recommended: If you are not using Active Directory Federation Services, reset users' Microsoft Online passwords.  

     If you are not using AD FS, you must set a Microsoft Online password for each user.  

##  <a name="bkmk_witsub"></a> Configuring the Microsoft Intune subscription  
 The Intune subscription lets you specify your configuration settings for the Intune service. This includes specifying which users can enroll their devices and defining which mobile device platforms to manage. When you have created your subscription, you can then install the service connection point site system role that lets you connect to the Intune service. This site system role will push settings and applications to the Intune service. The Intune subscription does the following:  

-   Retrieves the certificate that the service connection point requires to connect to the Intune service  

-   Defines the user collection that enables users to enroll mobile devices  

-   Defines and configures the mobile platforms that you want to support  

> [!IMPORTANT]  
>  Creating a subscription for Microsoft Intune in Configuration Manager will put your site's service connection point in "online mode." See [About the service connection point in System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).  

###  <a name="bkmk_subscription"></a> To create the Microsoft Intune subscription  

1.  If you haven't already, sign up for a Microsoft Intune account at [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=271123).  

     For guidance, see  [Get started with Microsoft Intune](https://docs.microsoft.com/en-us/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune).  

2.  In the Configuration Manager console, click **Administration**.  

3.  In the **Administration** workspace, expand **Cloud Services**, and click **Microsoft Intune Subscriptions**. On the **Home** tab, click **Add Microsoft Intune Subscription**.  

4.  On the **Introduction** page of the Create Microsoft Intune Subscription Wizard, review the text and click **Next**.  

5.  On the **Subscription** page, click **Sign in** and sign in by using your work or school account. In the **Set the Mobile Device Management Authority** dialog, select the check box to only manage mobile devices by using Configuration Manager through the Configuration Manager console. To continue with your subscription, you must select this option.  

    > [!IMPORTANT]  
    >  Once you select Configuration Manager as your management authority, you cannot change the management authority to Microsoft Intune in the future.  

6.  Click the privacy links to review them, and then click **Next**.  

7.  On the **General** page, specify the following options, and then click **Next**.  

    -   **Collection**: Specify a user collection that contains users who will enroll their mobile devices.  

        > [!NOTE]  
        >  If a user is removed from the collection, the user's device will continue to be managed for up to 24 hours when the user record is removed from the user database.  

    -   **Company name**: Specify your company name.  

    -   **URL to company privacy documentation**: If you publish your company privacy information to a link that is accessible from the Internet, provide a link that users can access from the company portal, for example http://www.contoso.com/CP_privacy.html. Privacy information can clarify what information users are sharing with your company.  

    -   **Color scheme for company portal**: Optionally, change the default color of blue for the company portals.  

    -   **Configuration Manager site code**: Specify a site code for a primary site to manage the mobile devices.  

        > [!NOTE]  
        >  Changing the site code affects only new enrollments and does not affect existing enrolled devices.  

    -   Specify the **Device enrollment limit**. Each licensed user can have up to 5 devices enrolled. Users receive an error message if they attempt to enroll more than the specified number of devices.  

8.  On the **Company Contact Information** page, specify the company contact information that is displayed in the company portal, and then click **Next**.  

9. On the **Company Logo** page, choose whether to display a logo in the company portal, and then click **Next**.  

10. Complete the wizard.  

 Once you've configured Intune management for mobile devices, you can create **Terms and Conditions**. Use terms and conditions to explain to users what happens when they enroll their devices. Users must accept the terms and conditions before they can enroll a device. See [Terms and Conditions in System Center Configuration Manager](../../mdm/deploy-use/terms-and-conditions.md).  

##  <a name="bkmk_WITconn"></a> The service connection point site system role  
 The service connection point sends settings and software deployment information to Configuration Manager and retrieves status and inventory messages from mobile devices. The Configuration Manager service acts as a gateway that communicates with mobile devices and stores settings.  

> [!NOTE]  
>  The service connection point site system role may only be installed on a central administration site or stand-alone primary site. The service connection point must have Internet access.  

###  <a name="bkm_connector"></a> To configure the service connection point role  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.  

3.  Add the **Service connection point** role to a new or existing site system server by using the associated step:  

    -   New site system server: On the **Home** tab, in the **Create** group, click **Create Site System Server** to start the Create Site System Server Wizard.  

    -   Existing site system server: Click the server on which you want to install the service connection point role. Then, on the **Home** tab, in the **Server** group, click **Add Site System Roles** to start the Add Site system Roles Wizard.  

4.  On the **System Role Selection** page, select **Service connection point**, and click **Next**.  

5.  Complete the wizard.  

### How does the service connection point authenticate with the Microsoft Intune service?  
 The service connection point extends Configuration Manager by establishing a connection to the cloud-based Intune service that manages mobile devices over the Internet. The service connection point authenticates with the Intune service as follows:  

1.  When you create an Intune subscription in the Configuration Manager console, the Configuration Manager admin is authenticated by connecting to Azure Active Directory, which redirects to the respective ADFS server to prompt for user name and password. Then, Intune issues a certificate to the tenant.  

2.  The certificate from step 1 is installed on the service connection point site role and is used to authenticate and authorize all further communication with the Microsoft Intune service.  

## Enable mobile device enrollment  
 Before devices can be enrolled, you must establish a trust relationship between the management solution and the managed mobile devices. This relationship is platform-specific so if, for example, you want to manage iOS devices, you must enable enrollment through Apple's servers with an Apple Push Notification service (APNs) certificate.  The following topics explain how to enable MDM for each set of devices:  

-   [Set up iOS hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md)  

-   [Set up Android hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-android-hybrid-device-management.md)  

-   [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-windows-phone-hybrid-enrollment.md)  

-   [Set up Windows hybrid device management with System Center Configuration Manager and Microsoft Intune](../../mdm/deploy-use/set-up-windows-hybrid-device-management.md)  

### Verify mobile device management configuration  
 You can verify certain device management components by checking the following log files:  

-   Check the Cloudusersync.log to verify that user accounts are successfully synchronized.  

-   Check the Sitecomp.log to verify that the service connection point was created successfully.  

## Managing Intune subscriptions associated with Configuration Manager  
 If you add a Microsoft Intune (either a trial subscription or paid subscription) to Configuration Manager, and then need to switch to a different Intune subscription, you must delete both the  **Microsoft Intune Subscription** and the **Service connection point** from the Configuration Manager console before you can add a new subscription.  

#### How to delete an Intune subscription from Configuration Manager  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Overview**, go to **Cloud Services**, and click **Microsoft Intune Subscriptions**.  

3.  Right-click **Microsoft Intune Subscription** and then click **Delete**. The **Microsoft Intune Subscription**.  

    > [!IMPORTANT]  
    >  All content including user enrollments, policies, and app deployments configured for the Intune evaluation subscription will be lost.  

4.  In the **Administration** workspace, expand **Overview**, go to **Site Configuration**, and select **Servers and Site System Roles**.  

5.  Select the server that hosts the **Service connection point** role.  

6.  In the **Site System Roles** list, select **Service connection point** and then click **Remove Role** in the ribbon. Confirm you want to remove the role. The service connection point is deleted.  

7.  You can now create a new service connection point, add a new Intune subscription to Configuration Manager, and set Configuration Manager as the MDM Authority.  
