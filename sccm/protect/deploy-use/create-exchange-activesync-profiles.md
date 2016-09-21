---
title: "Create Exchange ActiveSync email profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15f0fd50-e196-44e5-b435-234d7ff6a5cd
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman

---
# How to create Exchange ActiveSync email profiles in System Center Configuration Manager
Create email profiles in System Center Configuration Manager to deploy email settings to users in your company. By deploying these settings, you reduce the end-user effort that is required to connect to corporate email on the company network for devices that use Exchange ActiveSync.  
  
## Steps to Create an Exchange ActiveSync Email Profile  
 Use the following required steps to create an email profile by using the **Create Exchange ActiveSync Email Profile Wizard**.  
  
|Step|Details|More information|  
|----------|-------------|----------------------|  
|**Step 1:** Start the **Create Exchange ActiveSync Email Profile Wizard**.|Start the wizard in the **Assets and Compliance** workspace in the **Compliance Settings** node.|See the [Step 1: Start the Create Exchange ActiveSync Email Profile Wizard.](#BKMK_Step1) section in this topic.|  
|**Step 2:** Provide general information about the Exchange ActiveSync email profile.|Provide a name and description for the Exchange ActiveSync email profile.|See the [Step 2: Provide General Information about the Exchange ActiveSync Email Profile.](#BKMK_Step2) section in this topic.|  
|**Step 3:** Configure Exchange ActiveSync settings for the Exchange ActiveSync email profile.|Configure settings that the device will use to connect to Exchange ActiveSync such as the host name and email account details.|See the [Step 3: Configure Exchange ActiveSync Settings for the Exchange ActiveSync Email Profile.](#BKMK_Step3) section in this topic.|  
|**Step 4:** Configure synchronization settings for the Exchange ActiveSync email profile.|Configure synchronization settings such as the number of days of email to synchronize and the content types that will be synchronized.|See the [Step 4: Configure Synchronization Settings for the Exchange ActiveSync Email Profile.](#BKMK_Step4) section in this topic.|  
|**Step 5:** Specify supported platforms for the Exchange ActiveSync email profile.|Supported platforms are the operating systems where you will install the Exchange ActiveSync email profile.|See the [Step 5: Specify Supported Platforms for the Exchange ActiveSync Email Profile.](#BKMK_Step5) section in this topic.|  
|**Step 6:** Complete the wizard.|Complete the wizard to create the new Exchange ActiveSync email profile.|See the [Step 6: Complete the Wizard.](#BKMK_Step6) section in this topic.|  
  
## Supplemental Procedures to Create a New Exchange ActiveSync Email Profile  
 Use the following information when the steps in the preceding table require supplemental procedures.  
  
###  <a name="BKMK_Step1"></a> Step 1: Start the Create Exchange ActiveSync Email Profile Wizard.  
 Use this procedure to start the Create Exchange ActiveSync Email Profile Wizard.  
  
##### To start the Create Exchange ActiveSync Email Profile Wizard  
  
1.  In the System Center Configuration Manager console, click **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Compliance Settings**, expand **Company Resource Access**, and then click **Email Profiles**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Exchange ActiveSync Profile**.  
  
###  <a name="BKMK_Step2"></a> Step 2: Provide General Information about the Exchange ActiveSync Email Profile.  
 Use this procedure to provide general information about the Exchange ActiveSync email profile.  
  
##### To provide general information about the Exchange ActiveSync email profile  
  
1.  On the **General** page of the Create Exchange ActiveSync Email Profile Wizard, specify the following information:  
  
    -   **Name:** Enter a unique name for the Exchange ActiveSync email profile. You can use a maximum of 256 characters.  
  
    -   **Description:** Provide a description that gives an overview of the Exchange ActiveSync email profile and other relevant information that helps to identify it in the System Center Configuration Manager console. You can use a maximum of 256 characters.  
  
###  <a name="BKMK_Step3"></a> Step 3: Configure Exchange ActiveSync Settings for the Exchange ActiveSync Email Profile.  
 Use this procedure to configure Exchange ActiveSync settings for the Exchange ActiveSync email profile.  
  
##### To configure Exchange ActiveSync settings for the Exchange ActiveSync email profile  
  
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
        >  Before you can select the identity certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
         This option is only available if you selected **Certificates** under **Authentication method**.  
  
    -   **Use S/MIME** Send outgoing email using S/MIME encryption. This option is applicable to iOS devices only.  
  
    -   **Encryption certificates:** Click **Select** and then select a certificate to use for encryption. This option is applicable to iOS devices only.  
  
        > [!NOTE]  
        >  Before you can select the encryption certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
         This option is only available if you selected **Use S/MIME**.  
  
    -   **Signing certificates:** Click **Select** and then select a certificate to use for signing. This option is applicable to iOS devices only.  
  
        > [!NOTE]  
        >  Before you can select the signing certificate, you must first configure it as a Simple Certificate Enrollment Protocol (SCEP) certificate profile. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
         This option is only available if you selected **Use S/MIME**.  
  
###  <a name="BKMK_Step4"></a> Step 4: Configure Synchronization Settings for the Exchange ActiveSync Email Profile.  
 Use this procedure to provide general information about the Exchange ActiveSync email profile.  
  
##### To configure synchronization settings for the Exchange ActiveSync email profile  
  
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
  
###  <a name="BKMK_Step5"></a> Step 5: Specify Supported Platforms for the Exchange ActiveSync Email Profile.  
 Use the following procedure to specify the supported platforms for the Exchange ActiveSync email profile.  
  
 Supported platforms are the operating systems on which the Exchange ActiveSync email profile will be installed.  
  
##### To specify supported platforms for the Exchange ActiveSync email profile  
  
1.  On the **Supported Platforms** page of the Create Exchange ActiveSync Email Profile Wizard, select the operating systems on which the email profile will be installed, or click **Select all** to install the email profile on all available operating systems.  
  
###  <a name="BKMK_Step6"></a> Step 6: Complete the Wizard.  
 On the **Summary** page of the wizard, review the actions to be taken, and then complete the wizard. The new Exchange ActiveSync email profile is displayed in the **Email Profiles** node in the **Assets and Compliance** workspace.  
  
 For information about how to deploy the Exchange ActiveSync email profiles, see [How to deploy email profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-email-profiles.md).  
  
## See Also  
 [Operations and maintenance for email profiles in System Center Configuration Manager](../Topic/Operations%20and%20maintenance%20for%20email%20profiles%20in%20System%20Center%20Configuration%20Manager.md)