---
title: "Create Exchange ActiveSync email profiles | Microsoft Docs"
description: "Learn how to create and configure email profiles in System Center Configuration Manager that work with Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---

# Exchange ActiveSync email profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Email profiles works with  Microsoft Intune to enable you to provision devices with email profiles and restrictions by using Exchange ActiveSync. This enables your users to access corporate email on their devices with minimal setup required on their part.  

 You can configure the following device types with email profiles:  

-   Devices that run Windows Phone 8  

-   Devices that run Windows Phone 8.1  

-   Devices that run Windows  10 Mobile  

-   IPhone devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

-   IPad devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

> [!IMPORTANT]  
>  To deploy profiles to iOS, Android Samsung KNOX Standard, Windows Phone, and Windows 8.1 or Windows 10 devices, these devices must be enrolled into Intune. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 In addition to configuring an email account on the device, you can also configure synchronization settings for contacts, calendars and tasks.  

 When you create an email profile, you can include a wide range of security settings, including certificates for identity, encryption and signing that have been provisioned by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](create-pfx-certificate-profiles.md).    


## Create a New Exchange ActiveSync Email Profile  

Start the Create Exchange ActiveSync Email Profile Wizard  

1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Email Profiles**.  

3.  On the **Home** tab, in the **Create** group, click **Create Exchange ActiveSync Profile**.

4.  Follow the wizard instructions   

### To configure Exchange ActiveSync settings for the Exchange ActiveSync email profile  

1.  On the **Exchange ActiveSync** page of the Create Exchange ActiveSync Email Profile Wizard, specify the following information:  

    -   **Exchange ActiveSync host:** Specify the hostname of your company Exchange Server that hosts Exchange ActiveSync services.  

    -   **Account name:** Specify the display name for the email account as it will be displayed to users on their devices.  

    -   **Account user name:** Select how the email account user name is configured on client devices. You can select one of the following options from the drop-down list:  

        -   **User Principal Name** Use the full user principal name to log onto Exchange.  

        -   **sAMAccountName** Use  

        -   **Primary SMTP Address** Use the users primary SMTP address to log onto Exchange.  

    -   **Email address:** Select how the email address for the user on each client device is generated. You can select one of the following options from the drop-down list:  

        -   **Primary SMTP Address** Use the users primary SMTP address to log onto Exchange.  

        -   **User Principal Name** Use the full user principal name as the email address.  

    -   **Account domain:** Choose one of the following options:  

        -   **Obtain from Active Directory**  

        -   **Custom**  

         This field is only applicable if **sAMAccountName** is selected in the **Account user name** drop-down list.  

    -   **Authentication method:** Choose one of the following authentication methods that will be used to authenticate the connection to Exchange ActiveSync:  

        -   **Certificates** An identity certificate will be used to authenticate the Exchange ActiveSync connection.  

        -   **Username and Password** The device user must supply a password to connect to Exchange ActiveSync (the user name is configured as part of the email profile).  

    -   **Identity certificate:** Click **Select** and then select a certificate to use for identity.  

        > [!NOTE]  
        >  Before you can select the identity certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](create-pfx-certificate-profiles.md).  

         This option is only available if you selected **Certificates** under **Authentication method**.  

    -   **Use S/MIME** Send outgoing email using S/MIME encryption. This option is applicable to iOS devices only.  

    -   **Encryption certificates:** Click **Select** and then select a certificate to use for encryption. This option is applicable to iOS devices only.  

        > [!NOTE]  
        >  Before you can select the encryption certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](create-pfx-certificate-profiles.md).  

         This option is only available if you selected **Use S/MIME**.  

    -   **Signing certificates:** Click **Select** and then select a certificate to use for signing. This option is applicable to iOS devices only.  

        > [!NOTE]  
        >  Before you can select the signing certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](create-pfx-certificate-profiles.md).  

         This option is only available if you selected **Use S/MIME**.  

###   Configure Synchronization Settings for the Exchange ActiveSync Email Profile.  

1.  On the **Configure synchronization settings** page of the Create Exchange ActiveSync Email Profile Wizard, specify the following information:  

    -   **Schedule:** Select the schedule by which devices will synchronize data from the Exchange Server. This option is applicable to Windows Phone devices only. Choose from:  

        -   **Not Configured** A synchronization schedule is not enforced. This allows users to configure their own synchronization schedule.  

        -   **As messages arrive** Data such as emails and calendar items will be automatically synchronized when they arrive.  

        -   **15 minutes** Data such as emails and calendar items will be automatically synchronized every 15 minutes.  

        -   **30 minutes** Data such as emails and calendar items will be automatically synchronized every 30 minutes.  

        -   **60 minutes** Data such as emails and calendar items will be automatically synchronized every 60 minutes.  

        -   **Manual** Synchronization must be initiated manually by the device user.  

    -   **Number of days of email to synchronize:** From the drop-down list, select the number of days of email that you want to synchronize. Choose one of the following values:  

        -   **Not Configured** The setting is not enforced. This allows users to configure how much email is downloaded to their device.  

        -   **Unlimited** Synchronize all available email.  

        -   **1 day**  

        -   **3 days**  

        -   **1 week**  

        -   **2 weeks**  

        -   **1 month**  

    -   **Allow messages to be moved to other email accounts** Select this option to allow users to move email messages between different accounts they have configured on their device. This option is applicable to iOS devices only.  

    -   **Allow email to be sent from third-party applications** Select this option to allow users to send email from certain non-default, third-party email applications. This option is applicable to iOS devices only.  

    -   **Synchronize recently used email addresses** Select this option to synchronize the list of email addresses that have been recently used on the device. This option is applicable to iOS devices only.  

    -   **Use SSL** Select this option to use Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange Server.  

    -   **Content type to synchronize:** Select the content types that you want to synchronize to devices. This option is applicable to Windows Phone devices only. Choose from:  

        -   **Email**  

        -   **Contacts**  

        -   **Calendar**  

        -   **Tasks**  

###  Specify Supported Platforms for the Exchange ActiveSync Email Profile.  

1.  On the **Supported Platforms** page of the Create Exchange ActiveSync Email Profile Wizard, select the operating systems on which the email profile will be installed, or click **Select all** to install the email profile on all available operating systems.  

2.  Complete the wizard.

For information about how to deploy the Exchange ActiveSync email profiles, see [How to deploy profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
