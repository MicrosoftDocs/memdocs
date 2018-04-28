---
title: "Maintain Mac clients"
titleSuffix: "Configuration Manager"
description: Maintenance tasks for Configuration Manager Mac clients.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Maintain Mac clients
*Applies to: System Center Configuration Manager (Current Branch)*

Here are procedures for uninstalling Mac clients and for renewing their certificates.

##  Uninstalling the Mac client  

1.  On a Mac computer, open a terminal window and navigate to the folder containing **macclient.dmg**.  

2.  Navigate to the Tools folder and enter the following command-line:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  The **-c** property instructs the client uninstall to also remove  client crash logs and log files. We recommend this to avoid confusion if you later reinstall the client.  

3.  If required, manually remove the client authentication certificate that Configuration Manager was using, or revoke it. CMUnistall does not remove or revoke this certificate.  

##  Renewing the Mac client certificate  
 Use one of the following methods to renew the Mac client certificate:  

-   [Renew certificate wizard](#renew-certificate-wizard)  

-   [Renew certificate manually](#renew-certificate-manually)  

###  Renew certificate wizard  

1.  Configure the following values as *strings* in the ccmclient.plist file that controls when the Renew Certificate Wizard opens:  

 -   **RenewalPeriod1** - Specifies, in seconds, the first renewal period in which users can renew the certificate. The default value is 3,888,000 seconds (45 days). Don't configure a value less than 300, as the period will revert to the default. 

 -   **RenewalPeriod2** - Specifies, in seconds, the second renewal period in which users can renew the certificate. The default value is 259,200 seconds (3 days). If this value is configured and is greater than or equal to 300 seconds and is less than or equal to **RenewalPeriod1**, the value will be used. If **RenewalPeriod1** is greater than 3 days, a value of 3 days will be used for **RenewalPeriod2**.  If **RenewalPeriod1** is less than 3 days, then **RenewalPeriod2** is set to the same value as **RenewalPeriod1**.  

 -   **RenewalReminderInterval1** - Specifies, in seconds, the frequency at which the Renew Certificate Wizard will be displayed to users during the first renewal period. The default value is 86,400 seconds (1 day). If **RenewalReminderInterval1** is greater than 300 seconds and less than the value configured for **RenewalPeriod1**, then the configured value will be used. Otherwise, the default value of 1 day will be used.  

 -   **RenewalReminderInterval2** - Specifies, in seconds the frequency at which the Renew Certificate Wizard will be displayed to users during the second renewal period. The default value is 28,800 seconds (8 hours). If **RenewalReminderInterval2** is greater than 300 seconds, less   than or equal to **RenewalReminderInterval1** and less than or equal to **RenewalPeriod2**, then the configured value will be used. Otherwise, a value of 8 hours will be used.  

     **Example:** If the values are left as their defaults, 45 days before the certificate expires, the wizard will open every 24 hours.  Within 3 days of the certificate expiring, the wizard will open every 8 hours.  

     **Example:** Use the following command line, or a script, to set the first renewal period to 20 days.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  When the Renew Certificate Wizard opens, the **User name** and **Server name** fields will typically be pre-populated and the user can just enter a password to renew the certificate.  

    > [!NOTE]  
    >  If the wizard does not open, or if you accidentally close the wizard, click **Renew** from the **Configuration Manager** preference page to open the wizard.  

###  Renew certificate manually  
 A typical validity period for the Mac client certificate is 1 year. Configuration Manager does not automatically renew the user certificate that it requests during enrollment, so you must use the following procedure to renew the certificate manually.  

> [!IMPORTANT]  
>  If the certificate expires, you must uninstall, reinstall and then re-enroll the Mac client.  

 This procedure removes the SMSID, which is required to request a new certificate for the same Mac computer. When you remove and replace the client SMSID, any stored client history such as inventory is deleted after you delete the client from the Configuration Manager console.  

1.  Create and populate a device collection for the Mac computers that must renew the user certificates.  

    > [!WARNING]  
    >  Configuration Manager does not monitor the validity period of the certificate that it enrolls for Mac computers. You must monitor this independently from Configuration Manager to identify the Mac computers to add to this collection.  

2.  In the **Assets and Compliance** workspace, start the **Create Configuration Item Wizard**.  

3.  On the **General** page, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Type:Mac OS X**  

4.  On the **Supported Platforms** page, ensure that all Mac OS X versions are selected.  

5.  On the **Settings** page, choose **New** and then, in the **Create Setting** dialog box, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Setting type:Script**  

    -   **Data type:String**  

6.  In the **Create Setting** dialog box, for **Discovery script**, choose **Add script** to specify a script that discovers Mac computers with an SMSID configured.  

7.  In the **Edit Discovery Script** dialog box, enter the following Shell Script:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Choose **OK** to close the **Edit Discovery Script** dialog box.  

9. In the **Create Setting** dialog box, for **Remediation script (optional)**, choose **Add script** to specify a script that removes the SMSID when it is found on Mac computers.  

10. In the **Create Remediation Script** dialog box, enter the following Shell Script:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choose **OK** to close the **Create Remediation Script** dialog box.  

12. On the **Compliance Rules** page of the wizard, click **New**, and then in the **Create Rule** dialog box, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Selected setting:** Choose **Browse** and then select the discovery script that you specified previously.  

    -   In **the following values** field, enter **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Enable the option **Run the specified remediation script when this setting is noncompliant**.  

13. Complete the Create Configuration Item Wizard.  

14. Create a configuration baseline that contains the configuration item that you have just created and deploy it to the device collection that you created in step 1.  

     For more information about how to create and deploy configuration baselines, see [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) and [How to deploy configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. On Mac computers that have the SMSID removed, run the following command to install a new certificate:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     When prompted, provide the password for the super user account to run the command and then the password for the Active Directory user account.  

16. To limit the enrolled certificate to Configuration Manager, on the Mac computer, open a terminal window and make the following changes:  

    a.  Enter the command **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  In the **Keychain Access** dialog, in the **Keychains** section, choose **System**, and then, in the **Category** section, choose **Keys**.  

    c.  Expand the keys to view the client certificates. When you have identified the certificate with a private key that you have just installed, double-click the key.  

    d.  On the **Access Control** tab, choose **Confirm before allowing access**.  

    e.  Browse to **/Library/Application Support/Microsoft/CCM**, select **CCMClient**, and then choose **Add**.  

    f.  Choose **Save Changes** and close the **Keychain Access** dialog box.  

17. Restart the Mac computer.  

