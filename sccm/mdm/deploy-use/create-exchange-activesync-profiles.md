---
title: "Create Exchange ActiveSync email profiles"
titleSuffix: "Configuration Manager"
description: "Learn how to create and configure email profiles in System Center Configuration Manager that work with Microsoft Intune."
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Exchange ActiveSync email profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

By using Microsoft Intune and Exchange ActiveSync, you can set up devices with email profiles and restrictions. This lets your users access corporate email on their devices with minimal setup required on their part.  

 You can configure the following device types with email profiles:  

- Windows 10
- Windows Phone 8.1
- iPhones running iOS 9 and later 
- iPads running iOS 9 and later 
- Samsung KNOX Standard (4 and later)
- Android for Work

To deploy email profiles to devices, you must enroll the devices in Intune. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).

> [!NOTE]
> Intune provides two Android for Work email profiles, one each for the Gmail email app and the Nine Work email app. These apps are available in the Google Play Store, and they support connections to Exchange. To enable the email connectivity, deploy one of these email apps to your users' devices, and then create and deploy the appropriate profile. Email apps like Nine Work might not be free. Review the app’s licensing details or contact the app company with any questions.

 In addition to configuring an email account on the device, you can configure synchronization settings for contacts, calendars, and tasks.  

 When you create an email profile, you can include a wide range of security settings. These settings include certificates for identity, encryption, and signing that have been set up by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## Create an Exchange ActiveSync email profile  

To create a profile, you use the Create Exchange ActiveSync Email Profile Wizard. 

1. In the Configuration Manager console, choose **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then choose **Email Profiles**.  

3. On the **Home** tab, in the **Create** group, choose **Create Exchange ActiveSync Email Profile** to start the wizard.

4. On the **General** page of the wizard, configure the following:

   - **Name**. Provide a descriptive name for the email profile.

   - **Description**. Optionally, provide a description for the email profile that will help you identify it in the Configuration Manager console.

   - **This email profile is for Android for Work**. Choose this option if you will deploy this email profile to only Android for Work devices. If you check this box, the **Supported Platforms** wizard page is not shown. Only Android for Work email profiles are configured.

5. On the **Exchange ActiveSync** page of the wizard, specify the following information:  

   - **Exchange ActiveSync host**. Specify the host name of your company Exchange server that hosts Exchange ActiveSync services.  

   - **Account name**. Specify the display name for the email account as it will be shown to users on their devices.  

   - **Account user name**. Choose how the email account username is configured on client devices. You can choose one of the following options from the drop-down list:  

     -   **User Principal Name**. Use the full user principal name to sign in to Exchange.  

     -   **AccountName**. Use the full user account name from Active Directory.

     -   **Primary SMTP Address**. Use the user's primary SMTP address to sign in to Exchange.  

   - **Email address**. Choose how the email address for the user on each client device is generated. You can choose one of the following options from the drop-down list:  

     -   **Primary SMTP Address**. Use the user's primary SMTP address to sign in to Exchange.  

     -   **User Principal Name**. Use the full user principal name as the email address.  

   - **Account domain**. Choose one of the following options:  

     - **Obtain from Active Directory**  

     - **Custom**  

       This field is applicable only if **sAMAccountName** is selected in the **Account user name** drop-down list.  

   - **Authentication method**. Choose one of the following authentication methods that will be used to authenticate the connection to Exchange ActiveSync:  

     -   **Certificates**. An identity certificate will be used to authenticate the Exchange ActiveSync connection.  

     -   **Username and Password**. The device user must supply a password to connect to Exchange ActiveSync. (The username is configured as part of the email profile.)  

   - **Identity certificate**. Choose **Select** and then choose a certificate to use for identity.  

      Identity certificates must be SCEP certificates; you cannot use a PFX certificate.  To learn more, see [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

      This option is available only if you chose **Certificates** under **Authentication method**.  

   - **Use S/MIME**. Send outgoing email by using S/MIME encryption. This option is applicable to iOS devices only. Choose from the following options:

     - **Signing certificates**.  Choose **Select** and then choose a certificate profile to use for encryption.  

       The profile can be either a SCEP or PFX certificate.  However, if both signing and encryption are used, you must select PFX certificate profiles for *both* signing and encryption.

     - **Encryption certificates**. Choose **Select** and then choose a certificate to use for encryption. You can choose only a PFX certificate to use as an encryption certificate.

     - To encrypt all mail messages on iOS devices, enable the **Require encryption** checkbox.    

       You must create certiciate profiles before you can choose them here.  To learn more, see [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## Configure synchronization settings for the Exchange ActiveSync email profile  

On the **Configure synchronization settings** page of the Create Exchange ActiveSync Email Profile Wizard, specify the following information:  

-   **Schedule**. Choose the schedule by which devices will sync data from the Exchange server. This option is applicable to Windows Phone devices only. Choose from:  

    -   **Not Configured**. A synchronization schedule is not enforced. This lets users configure their own synchronization schedule.  

    -   **As messages arrive**. Data like emails and calendar items will be automatically synced when they arrive.  

    -   **15 minutes**. Data like emails and calendar items will be automatically synced every 15 minutes.  

    -   **30 minutes**. Data like emails and calendar items will be automatically synced every 30 minutes.  

    -   **60 minutes**. Data like emails and calendar items will be automatically synced every 60 minutes.  

    -   **Manual**. The device user must initiate synchronization manually.  

-   **Number of days of email to synchronize**. From the drop-down list, choose the number of days of email that you want to sync. Choose one of the following values:  

    -   **Not Configured**. The setting is not enforced. It lets users configure how much email is downloaded to their device.  

    -   **Unlimited**. Sync all available email.  

    -   **1 day**  

    -   **3 days**  

    -   **1 week**  

    -   **2 weeks**  

    -   **1 month**  

-   **Allow messages to be moved to other email accounts**. Choose this option to let users move email messages between different accounts that they have configured on their device. This option is applicable to iOS devices only.  

-   **Allow email to be sent from third-party applications**. Choose this option to let users send email from certain non-default, third-party email applications. This option is applicable to iOS devices only.  

-   **Synchronize recently used email addresses**. Choose this option to sync the list of email addresses that have been recently used on the device. This option is applicable to iOS devices only.  

-   **Use SSL**. Choose this option to use Secure Sockets Layer (SSL) communication for sending emails, receiving emails, and communicating with the Exchange server.  

-   **Content type to synchronize**. Choose the content types that you want to sync to devices. This option is applicable to Windows Phone devices only. Choose from:  

    -   **Email**  

    -   **Contacts**  

    -   **Calendar**  

    -   **Tasks**  

## Specify supported platforms for the Exchange ActiveSync email profile  

1.  On the **Supported Platforms** page of the Create Exchange ActiveSync Email Profile Wizard, choose the operating systems on which the email profile will be installed. Or choose **Select all** to install the email profile on all available operating systems.  

2.  Finish the wizard.

For information about how to deploy the Exchange ActiveSync email profiles, see [How to deploy profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
