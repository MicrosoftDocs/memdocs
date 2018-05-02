---
title: "Deploy Mac clients"
titleSuffix: "Configuration Manager"
description: "Learn how to deploy clients to Mac computers in System Center Configuration Manager."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to deploy clients to Macs

*Applies to: System Center Configuration Manager (Current Branch)*

This topic describes how to deploy and maintain the Configuration Manager client on Mac computers. To learn about what you have to configure before deploying clients to Mac computers, see [Prepare to deploy client software to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

When you install a new client for Mac computers, you might have to also install Configuration Manager updates to reflect the new client information in the Configuration Manager console.

In these procedures, you have two options for installing client certificates. Read more about client certificates for Macs in [Prepare to deploy client software to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Use Configuration Manager enrollment by using the [CMEnroll tool](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). The enrollment process does not support automatic certificate renewal so you must re-enroll Mac computers before the installed certificate expires.    

-   [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  To deploy the client to devices running macOS Sierra, the Subject name of the management point certificate must be configured correctly, for example, by using the FQDN of the management point server.


## Configure client settings for enrollment  
 You must use the [default client settings](../../../core/clients/deploy/about-client-settings.md) to configure enrollment for Mac computers; you cannot use custom client settings.  

 This is required for Configuration Manager to request and install the certificate on the Mac.  

### To configure the default client settings for Configuration Manager to enroll certificates for Macs  

1.  In the Configuration Manager console, choose **Administration** >  **Client Settings** > **Default Client Settings**.  

4.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

5.  Select the **Enrollment** section, and then configure these settings:  

    1.  **Allow users to enroll mobile devices and Mac computers:Yes**  

    2.  **Enrollment profile:** Choose **Set Profile**.  

6.  In the **Mobile Device Enrollment Profile** dialog box, choose **Create**.  

7.  In the **Create Enrollment Profile** dialog box, enter a name for this enrollment profile, and then configure the **Management site code**. Select the Configuration Manager primary site that contains the management points that will manage the Mac computers.  

    > [!NOTE]  
    >  If you cannot select the site, check that at least one management point in the site is configured to support mobile devices.  

8.  Choose **Add**.  

9. In the **Add Certification Authority for Mobile Devices** dialog box, select the certification authority (CA) server that will issue certificates to Mac computers.  

10. In the **Create Enrollment Profile** dialog box, select the Mac computer certificate template that you created in Step 3.  

11. Click **OK** to close the **Enrollment Profile** dialog box, and then  the **Default Client Settings** dialog box.  

    > [!TIP]  
    >  If you want to change the client policy interval, use **Client policy polling interval** in the **Client Policy** client setting group.  

 All users will be configured with these settings the next time that they download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 In addition to the enrollment client settings, ensure that you have configured the following client device settings:  

-   **Hardware inventory**: Enable and configure this if you want to collect hardware inventory from Mac and Windows client computers. For more information, see [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Compliance settings**: Enable and configure this  if you want to evaluate and remediate settings on Mac and Windows client computers. For more information, see [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  For more information about Configuration Manager client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

## Download the client source files for Macs  

1.  Download the Mac OS X client file package, **ConfigmgrMacClient.msi**, and save it to a computer that runs Windows.  

     This file is not supplied on the Configuration Manager installation media. You can download this file from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  On the Windows computer, run  **ConfigmgrMacClient.msi** to extract the Mac client package, Macclient.dmg to a folder on the local disk (by default **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copy the Macclient.dmg file to a folder on the Mac computer.  

4.  On the Mac computer, run the Macclient.dmg file to extract the files to a folder on the local disk.  

5.  In the folder, ensure that the files Ccmsetup and CMClient.pkg are extracted and that a folder named Tools is created that contains the CMDiagnostics,  CMUninstall, CMAppUtil and CMEnroll tools.

	-  **Ccmsetup**: Installs the Configuration Manager client on your Mac computers.  

	-   **CMDiagnostics**: Collects diagnostic information related to the Configuration Manager client on your Mac computers.  

	-   **CMUninstall**: Uninstalls the client from your Mac computers.  

	-   **CMAppUtil**: Converts Apple application packages into a format that can be deployed as a Configuration Manager application.  

	-   **CMEnroll**: Requests and installs the client certificate for a Mac computer so that you can then install the Configuration Manager client.   

## Install the client and then enroll the client certificate on the Mac  

You can enroll individual clients with the [Mac Computer Enrollment wizard](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

For automation that enables enrollment of many clients, use the [CMEnroll tool](#client-and-certificate-automation-with-cmenroll).   


###  Enroll the client with the Mac Computer Enrollment Wizard  

1.  After you have finished installing the client, the Computer Enrollment wizard opens. If the wizard does not open, or if you accidentally close it, click **Enroll** from the **Configuration Manager** preference page to open it.  

2.  On the second page of the wizard, provide:  

    -   **User name** - The user name can be in the following formats:  

        -   'domain\name'. For example: 'contoso\mnorth'  

        -   'user@domain'. For example: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  When you use an email address to populate the **User name** field, Configuration Manager automatically uses the domain name of the email address and the default name of the enrollment proxy point server to populate the **Server name** field. If this domain name and server name do not match the name of the enrollment proxy point server, tell your users the correct name  to use when enrolling their Mac computers.  

         The user name and corresponding password must match an Active Directory user account that is granted Read and Enroll permissions on the Mac client certificate template.  

    -   **Password** - Enter a corresponding password for the user name specified.  

    -   **Server name** - Enter the name of the enrollment proxy point server.  


### Client and certificate automation with CMEnroll  

Use this procedure for automation of client installation and requesting and enrollment of client certificates with the CMEnroll tool. To run the tool you must have an Active Directory user account.

1.  On the Mac computer, navigate to the folder where you extracted the contents of the Macclient.dmg file.  

2.  Enter the following command-line: **sudo ./ccmsetup**  

3.  Wait until you see the **Completed installation** message. Although the installer displays a message that you must restart now, do not restart, and continue to the next step.  

4.  From the Tools folder on the Mac computer, type the following: **sudo ./CMEnroll -s &lt;enrollment_proxy_server_name> -ignorecertchainvalidation -u &lt;user name'>**  

	After the client installs, the Mac Computer Enrollment wizard opens to help you enroll the Mac computer. To enroll the client by this method, see [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) in this topic.  

5. Type the password for the Active Directory user account.  When you enter this command, you are asked for two passwords: The first prompt is for the super user account to run the command. The second prompt is for the Active Directory user account. The prompts look identical, so make sure that you specify them in the correct sequence.  

	The user name can be in the following formats:  

    -   'domain\name'. For example: 'contoso\mnorth'  

    -   'user@domain'. For example: 'mnorth@contoso.com'  

     The user name and corresponding password must match an Active Directory user account that is granted Read and Enroll permissions on the Mac client certificate template.  

     Example: If the enrollment proxy point server is named **server02.contoso.com**, and a user name of **contoso\mnorth** has been granted permissions for the Mac client certificate template, type the following: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  If the username contains any of the characters **&lt;>"+=,** enrollment will fail. Obtain an out-of-band certificate with a username that does not contain these characters.  
	>  
    >  For a more seamless user experience, you can script the installation steps and commands so that users only have to supply their user name and password.  

5.  Wait until you see the **Successfully enrolled** message.  

6.  To limit the enrolled certificate to Configuration Manager, on the Mac computer, open a terminal window and make the following changes:  

    a.  Enter the command **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  In the **Keychain Access** dialog box, in the **Keychains** section, choose **System**, and then, in the **Category** section, choose **Keys**.  

    c.  Expand the keys to view the client certificates. When you have identified the certificate with a private key that you have just installed, double-click the key.  

    d.  On the **Access Control** tab, choose **Confirm before allowing access**.  

    e.  Browse to **/Library/Application Support/Microsoft/CCM**, select **CCMClient**, and then choose **Add**.  

    f.  Choose **Save Changes** and close the **Keychain Access** dialog box.  

7.  Restart the Mac computer.  

 Verify that the client installation is successful by opening the **Configuration Manager** item in **System Preferences** on the Mac computer. You can also update and view the **All Systems** collection to confirm that the Mac computer now appears in this collection as a managed client.  

> [!TIP]  
>  To help troubleshoot the Mac client, you can use the CMDiagnostics program that is included with the Mac OS X client package to collect the following diagnostic information:  
>   
>  -   A list of running processes  
> -   The Mac OS X operating system version  
> -   Mac OS X crash reports relating to the Configuration Manager client including **CCM\*.crash** and **System Preference.crash**.  
> -   The Bill of Materials (BOM) file and property list (.plist) file created by the Configuration Manager client installation.  
> -   The contents of the folder /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  The information collected by CmDiagnostics is added to a zip file that is saved to the desktop of the computer and is named `cmdiag-*<hostname\>***-***&gt;date and time\>*.zip`


##  Use a certificate request and installation method that is independent from Configuration Manager  

First, perform these specific tasks from [Prepare to deploy client software to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients):

1. [Deploy a web server certificate to site system servers](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Deploy a client authentication certificate to site system servers](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configure the management point and distribution point](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Optional: Install the reporting services point](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Then, perform these tasks:

5. [Download the client source files for Macs](#download-the-client-source-files-for-macs) .  
6. Use the instructions that accompany your chosen certificate deployment method to request and install the client certificate on the Mac computer.  
7.  Navigate to the folder where you extracted the contents of the macclient.dmg file that you downloaded from the Microsoft Download Center.  

3.  Enter the following command-line: **sudo ./ccmsetup -MP <management point Internet FQDN\> -SubjectName <certificate subject value\>**.  The certificate subject value is case-sensitive, so type it exactly as it appears in the certificate details.  

     Example: If the Internet FQDN in the site system properties is **server03.contoso.com** and the Mac client certificate has the FQDN of **mac12.contoso.com** as a common name in the certificate subject, type: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Wait until you see the **Completed installation** message and then restart the Mac computer.  

5.  To make sure that this certificate is accessible to Configuration Manager, on the Mac computer, open a terminal window and make these changes:  

    a.  Enter the command **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  In the **Keychain Access** dialog box, in the **Keychains** section, choose **System**, and then, in the **Category** section, choose **Keys**.  

    c.  Expand the keys to view the client certificates. When you have identified the certificate with a private key that you have just installed, double-click the key.  

    d.  On the **Access Control** tab, choose **Confirm before allowing access**.  

    e.  Browse to **/Library/Application Support/Microsoft/CCM**, select **CCMClient**, and then choose **Add**.  

    f.  Choose **Save Changes** and close the **Keychain Access** dialog box.  

6.  If you have more than one certificate that contains the same subject value, you must specify the certificate serial number to identify the certificate that you want to use for the Configuration Manager client. To do this, use the following command: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number\>"**.  

     For example: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Verify that the client installation is successful by opening the **Configuration Manager** item in **System Preferences** on the Mac. You can also update and view the **All Systems** collection to confirm that the Mac appears in this collection as a managed client.  

## Renewing the Mac client certificate  
 Use the following procedure before you renew the computer certificate on Mac computers.  

 This procedure removes the SMSID, which is required for the client to use a new or renewed certificate on the Mac computer.  

> [!IMPORTANT]  
>  When you remove and replace the client SMSID, any stored client history such as inventory is deleted after you delete the client from the Configuration Manager console.  

### To renew the Mac client certificate  

1.  Create and populate a device collection for the Mac computers that must renew the computer certificates.  

2.  In the **Assets and Compliance** workspace, start the **Create Configuration Item Wizard**.  

3.  On the **General** page of the wizard, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Type:Mac OS X**  

4.  On the **Supported Platforms** page of the wizard, ensure that all Mac OS X versions are selected.  

5.  On the **Settings** page of the wizard, click **New** and then, in the **Create Setting** dialog box, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Setting type:Script**  

    -   **Data type:String**  

6.  In the **Create Setting** dialog box, for **Discovery script**, click **Add script** to specify a script that discovers Mac computers with an SMSID configured.  

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

12. On the **Compliance Rules** page of the wizard, choose **New**, and then in the **Create Rule** dialog box, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Selected setting:** Choose **Browse** and then select the discovery script that you specified previously.  

    -   In **the following values** field, enter **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Enable the option **Run the specified remediation script when this setting is noncompliant**.  

13. Complete the Create Configuration Item Wizard.  

14. Create a configuration baseline that contains the configuration item that you have just created and deploy this to the device collection that you created in step 1.  

     For more information about how to create and deploy configuration baselines, see [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. After you have installed a new certificate on Mac computers that have the SMSID removed, run the following command to configure the client to use the new certificate:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. If you have more than one certificate that contains the same subject value, you must then specify the certificate serial number to identify the certificate that you want to use for the Configuration Manager client. To do this, use the following command: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number\>"**.  

     For example: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Restart.  


## See also

[Maintain Mac clients](/sccm/core/clients/manage/maintain-mac-clients)
