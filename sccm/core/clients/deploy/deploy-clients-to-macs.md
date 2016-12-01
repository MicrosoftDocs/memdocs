---
title: "Deploy Mac clients | Microsoft Docs"
description: "Learn how to deploy clients to Mac computers in System Center Configuration Manager."
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigmanms.author: nbigmanmanager: angrobe

---
# How to deploy clients to Macs in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
This topic describes how to install the Configuration Manager client on Mac computers.

## Prerequisites and preparatory steps

### Mac prerequisites

Before you install the client make sure that the Mac computers meet the prerequisites, as described in [Supported operating systems for Macs](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

### Certificate requirements
Client installation and management for Mac computers requires public key infrastructure (PKI) certificates. PKI certificates secure the communication between the Mac computers and the Configuration Manager site by using mutual authentication and encrypted data transfers. Configuration Manager can request and install a user client certificate by using Microsoft Certificate Services with an enterprise certification authority (CA) and the Configuration Manager enrollment point and enrollment proxy point site system roles. Or, you can request and install a computer certificate independently from Configuration Manager if the certificate meets the requirements for Configuration Manager.   
  
Configuration Manager Mac clients always perform certificate revocation checking; unlike Configuration Manager clients that run on Windows, you cannot disable this certificate revocation list (CRL) checking function.  
  
If Mac clients cannot confirm the certificate revocation status for a server certificate because they cannot locate the CRL, they will not be able to successfully connect to Configuration Manager site systems, such as management points and distribution points. Especially for Mac clients in a different forest to the issuing certification authority, check your CRL design to ensure that Mac clients can locate and connect to a CRL distribution point (CDP) for connecting site system servers.  

Before you install the Configuration Manager client on a Mac computer, decide how to install the client certificate:  

-   Use Configuration Manager enrollment by using the CMEnroll tool and follow the steps in the next section of this topic. The enrollment process does not support automatic certificate renewal so you must re-enroll Mac computers before the installed certificate expires.  

-   Use a certificate request and installation method that is independent from Configuration Manager. For this installation method, see the [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) section in this topic.  

For more information about the Mac client certificate requirement and other PKI certificates that are required to support Mac computers, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Mac clients are automatically assigned to the Configuration Manager site that manages them. Mac clients install as Internet-only clients, even if communication is restricted to the intranet. This client configuration means that they will communicate with the site system roles (management points and distribution points) in their assigned site when you configure these site system roles to allow client connections from the Internet. Mac computers do not communicate with site system roles outside their assigned site.  

> [!IMPORTANT]  
>  The Configuration Manager Mac client cannot be used to connect to a management point that is configured to use a [database replica](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


### Deploy a web server certificate to site system servers  
If these site systems don't have it, deploy a web server certificate to the computers that have these site system roles:  

-   Management point  

-   Distribution point  

-   Enrollment point  

-   Enrollment proxy point  

The web server certificate must contain the Internet FQDN that is specified in the site system properties. The server doesn't have to be accessible from the Internet to support Mac computers. If you do not require Internet-based client management, you can specify the intranet FQDN value for the Internet FQDN.  

Specify the site system's Internet FQDN value in the web server certificate for the management point, the distribution point, and the enrollment proxy point. 

For an example deployment that creates and installs this web server certificate, see the [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

 

### Deploy a client authentication certificate to site system servers  
 If these site systems don't have it, deploy a client authentication certificate to the following computers that hold the following site system roles:  

-   Management point  

-   Distribution point  

 For an example deployment that creates and installs the client certificate for management points, see the [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 For an example deployment that creates and installs the client certificate for distribution points, see the [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### Prepare the client certificate template for Macs  

> [!NOTE]  
>  To run the Configuration Manager enrollment tool, you must have an Active Directory user account.  

 The certificate template must have **Read** and **Enroll** permissions for the user account that will enroll the certificate on the Mac computer.  

 See [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

### Configure the management point and distribution point  
 Configure management points for the following options:  

-   HTTPS  

-   Allow client connections from the Internet. This configuration value is required to manage Mac computers. However, it does not mean that site system servers must be accessible from the Internet.  

-   Allow mobile devices and Mac computers to use this management point  

 Although distribution points are not required to install the client, you must configure distribution points to allow client connections from the Internet if you want to deploy software to these computers after the client is installed.  

 
##### To configure management points and distribution points to support Macs  

Before you start this procedure, make sure that the site system server that runs the management point and distribution point is configured with an Internet FQDN. If these servers won't support Internet-based client management, you can specify the intranet FQDN as the Internet FQDN value. 

The site system roles must be in a primary site.  


1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Servers and Site System Roles**, and then choose the server that has the right site system roles.  

3.  In the details pane, right-click **Management point**, choose **Role Properties**, and in the **Management Point Properties** dialog box, configure these options:  

    1.  Choose **HTTPS**.  

    2.  Choose **Allow Internet-only client connections** or **Allow intranet and Internet client connections**. These options require an Internet or intranet FQDN.  

    3.  Choose **Allow mobile devices and Mac computers to use this management point**.  

4.  In the details pane, right-click **Distribution point**, choose **Role Properties**, and in the **Distribution Point Properties** dialog box, configure these options:  

    -   Choose **HTTPS**.  

    -   Choose **Allow Internet-only client connections** or **Allow intranet and Internet client connections**. These options require an Internet or intranet FQDN.  

    -   Choose **Import certificate**, browse to the exported client distribution point certificate file, and then specify the password.  

5.  Repeat steps 2 through 4 for all management points and distribution points in primary sites that you will use with Macs.  

### Configure the enrollment proxy point and the enrollment point  
 You must install both these site system roles in the same site but you do not have to install them on the same site system server, or in the same Active Directory forest.  

 For more information about site system role placement and considerations, see  [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) in [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 These procedures configure the site system roles to support Mac computers. Choose one of these procedures, depending on whether you will install a new site system server to support Mac computers or use an existing site system server:  

-   [New site system server](#new-site-system-server)  

-   [Existing site system server](#existing-site-system-server)  

####  New site system server  

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Servers and Site System Roles**  

3.  On the **Home** tab, in the **Create** group, choose **Create Site System Server**.  

4.  On the **General** page, specify the general settings for the site system.  Make sure that you specify a value for the Internet FQDN. If the server won't be accessible from the Internet, use the intranet FQDN.  

5.  On the **System Role Selection** page, select **Enrollment proxy point** and **Enrollment point** from the list of available roles.  

6.  On the **Enrollment Proxy Point** page, review the settings and make any necessary changes.  

7.  On the **Enrollment Point Settings** page, review the settings and make any necessary changes. Then, complete the wizard.  

#### Existing site system server  

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Servers and Site System Roles**, and then choose the server that you want to use to support Macs.  

3.  On the **Home** tab, in the **Create** group, choose **Add Site System Roles**.  

4.  On the **General** page, specify the general settings for the site system, and then click **Next**. Make sure that you specify a value for the Internet FQDN. If the server won't be accessible from the Internet, use the intranet FQDN.   

5.  On the **System Role Selection** page, choose **Enrollment proxy point** and **Enrollment point** from the list of available roles.  

6.  On the **Enrollment Proxy Point** page, review the settings and make any necessary changes.  

7.  On the **Enrollment Point Settings** page, review the settings and make any necessary changes. Then, complete the wizard.  

### Optional: Install the reporting services point  
 Install the reporting services point if you want to run reports for Macs.  

 For more information about how to install and configure the reporting services point, see [Configuring reporting in System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).  


##  Install and configure the client for Macs  


### Configure client settings for enrollment  
 You must use the default client settings to configure enrollment for Mac computers; you cannot use custom client settings.  

 For more information about client settings, see [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 This is required for Configuration Manager to request and install the certificate on the Mac.  

#### To configure the default client settings for Configuration Manager to enroll certificates for Macs  

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
    >  If you want to change the client policy interval, use the **Client policy polling interval** client setting in the **Client Policy** client setting group.  

 All users will be configured with these settings the next time that they download client policy. To initiate policy retrieval for a single client, see [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 In addition to the enrollment client settings, ensure that you have configured the following Configuration Manager client device settings:  

-   **Hardware inventory**: Enable and configure this if you want to collect hardware inventory from Mac and Windows client computers. For more information, see [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Compliance settings**: Enable and configure this  if you want to evaluate and remediate settings on Mac and Windows client computers. For more information, see [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  For more information about Configuration Manager client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

### Download the client source files for Macs  
 You must download and install the following programs before you can install and manage the Configuration Manager client on Macs:  

-   **Ccmsetup**: Use this application to install the Configuration Manager client on your Mac computers.  

-   **CMDiagnostics**: Use this tool to collect diagnostic information related to the Configuration Manager client on your Mac computers.  

-   **CMUninstall**: Use this tool to uninstall the Configuration Manager client from your Mac computers.  

-   **CMAppUtil**: Use this tool to convert Apple application packages into a format that can be deployed as a Configuration Manager application.  

-   **CMEnroll**: Use this tool to request and install the client certificate for a Mac computer so that you can then install the Configuration Manager client.  

> [!IMPORTANT]  
>  When you install a new client for Mac computers, you might have to also install Configuration Manager updates to reflect the new client information in the Configuration Manager console.  

##### To download and install the Mac OS X client files  

1.  Download the Mac OS X client file package, **ConfigmgrMacClient.msi**, and save it to a computer that runs Windows.  

     This file is not supplied on the Configuration Manager installation media. You can download this file from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  On the Windows computer, run the **ConfigmgrMacClient.msi** file that you just downloaded to extract the Mac client package, Macclient.dmg to a folder on the local disk (by default **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copy the Macclient.dmg file to a folder on the Mac computer.  

4.  On the Mac computer, run the Macclient.dmg file to extract the files to a folder on the local disk.  

5.  In the folder, ensure that the files Ccmsetup and CMClient.pkg are extracted and that a folder named Tools is created that contains the CMDiagnostics,  CMUninstall, CMAppUtil and CMEnroll tools.  

### Install the client and then enroll the client certificate on the Mac  
 This procedure installs the client and then uses the CMEnroll tool to request and install the client certificate for a Mac computer so that you can then manage this computer by using Configuration Manager.  

 You can enroll the client by using the Mac Computer Enrollment wizard without having to use the CMEnroll tool, as described in [Enroll the client by using the Mac Computer Enrollment Wizard](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard)  

#### To install the client and enroll the certificate by using the CMEnroll tool  

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
    >  If the username contains any of the characters **&lt;>"+=,** then enrollment will fail. To fix this problem, obtain an out-of-band certificate with a username that does not contain these characters.  
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
>  To help troubleshoot any problems with the Mac client, you can use the CMDiagnostics program that is included with the Mac OS X client package to collect the following diagnostic information:  
>   
>  -   A list of running processes  
> -   The Mac OS X operating system version  
> -   Mac OS X crash reports relating to the Configuration Manager client including **CCM\*.crash** and **System Preference.crash**.  
> -   The Bill of Materials (BOM) file and property list (.plist) file created by the Configuration Manager client installation.  
> -   The contents of the folder /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  The information collected by CmDiagnostics is added to a zip file that is saved to the desktop of the computer and is named cmdiag-*<hostname\>***-***<date and time\>*.zip.  

####  Enroll the client by using the Mac Computer Enrollment Wizard  

1.  After you have finished installing the client, the Computer Enrollment wizard opens. If the wizard does not open, or if you accidentally close the wizard, click **Enroll** from the **Configuration Manager** preference page to open the wizard.  

2.  On the second page of the wizard, specify the following information:  

    -   **User name** - The user name can be in the following formats:  

        -   'domain\name'. For example: 'contoso\mnorth'  

        -   'user@domain'. For example: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  When you use an email address to populate the **User name** field, Configuration Manager automatically uses the domain name of the email address and the default name of the enrollment proxy point server to populate the **Server name** field. If this domain name and server name do not match the name of the enrollment proxy point server, you must advise your users of the correct name to use, so that they can enter this when enrolling their Mac computers.  

         The user name and corresponding password must match an Active Directory user account that is granted Read and Enroll permissions on the Mac client certificate template.  

    -   **Password** - Enter a corresponding password for the user name specified.  

    -   **Server name** - Enter the name of the enrollment proxy point server.  

3.  Click **Next** to continue, and then complete the wizard.  

## Maintenance tasks for Mac clients

###  Uninstalling the Mac client  

1.  On a Mac computer, open a terminal window and navigate to the folder where you extracted the contents of the macclient.dmg file that you downloaded.  

2.  Navigate to the Tools folder and enter the following command-line:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  The **-c** property instructs the client uninstall to also remove and client crash logs and log files. This is optional, but a best practice to help avoid confusion if you later reinstall the client.  

3.  If required, manually remove the client authentication certificate that Configuration Manager was using, or revoke it. CMUnistall does not remove or revoke this certificate.  

###  Renewing the Mac client certificate  
 Use one of the following methods to renew the Mac client certificate:  

-   [Renew certificate wizard](#renew-certificate-wizard)  

-   [Renew certificate manually](#renew-certificate-manually)  

####  Renew certificate wizard  

1.  Configure the following values as *strings* in the ccmclient.plist file that controls when the Renew Certificate Wizard opens:  

    -   **RenewalPeriod1** - Specifies, in seconds, the first renewal period in which users can renew the certificate. The default value is 3,888,000 seconds (45 days). Don't configure a value less than 300, as the period will revert to the default. 


    -   **RenewalPeriod2** - Specifies, in seconds, the second renewal period in which users can renew the certificate. The default value is 259,200 seconds (3 days). If this value is configured and is greater than or equal to 300 seconds and is less than or equal to **RenewalPeriod1**, the value will be used. If **RenewalPeriod1** is greater than 3 days, a value of 3 days will be used for **RenewalPeriod2**.  If **RenewalPeriod1** is less than 3 days, then **RenewalPeriod2** is set to the same value as **RenewalPeriod1**.  

    -   **RenewalReminderInterval1** - Specifies, in seconds, the frequency at which the Renew Certificate Wizard will be displayed to users during the first renewal period. The default value is 86,400 seconds (1 day). If **RenewalReminderInterval1** is greater than 300 seconds and less than the value configured for **RenewalPeriod1**, then the configured value will be used. Otherwise, the default value of 1 day will be used.  

    -   **RenewalReminderInterval2** - Specifies, in seconds the frequency at which the Renew Certificate Wizard will be displayed to users during the second renewal period. The default value is 28,800 seconds (8 hours). If **RenewalReminderInterval2** is greater than 300 seconds, less   than or equal to **RenewalReminderInterval1** and less than or equal to **RenewalPeriod2**, then the configured value will be used. Otherwise, a value of 8 hours will be used.  

     **Example:** If the values are left as their defaults, 45 days before the certificate expires, the wizard will open every 24 hours.  Within 3 days of the certificate expiring, the wizard will open every 8 hours.  

     **Example:** Use the following command line, or a script, to set the first renewal period to 20 days.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  When the Renew Certificate Wizard opens, the **User name** and **Server name** fields will typically be pre-populated and the user will only need to enter a password to renew the certificate.  

    > [!NOTE]  
    >  If the wizard does not open, or if you accidentally close the wizard, click **Renew** from the **Configuration Manager** preference page to open the wizard.  

####  Renewing the Mac client certificate manually  
 A typical validity period for the Mac client certificate is 1 year. Configuration Manager does not automatically renew the user certificate that it requests during enrollment, so you must use the following procedure to renew the certificate manually.  

> [!IMPORTANT]  
>  If the certificate expires, you must uninstall, reinstall and then re-enroll the Mac client.  

 This procedure removes the SMSID, which is required to request a new certificate for the same Mac computer. When you remove and replace the client SMSID, any stored client history such as inventory is deleted after you delete the client from the Configuration Manager console.  

1.  Create and populate a device collection for the Mac computers that must renew the user certificates.  

    > [!WARNING]  
    >  Configuration Manager does not monitor the validity period of the certificate that it enrolls for Mac computers. You must monitor this independently from Configuration Manager to identify the Mac computers to add to this collection.  

2.  In the **Assets and Compliance** workspace, start the **Create Configuration Item Wizard**.  

3.  On the **General** page of the wizard, specify the following information:  

    -   **Name:Remove SMSID for Mac**  

    -   **Type:Mac OS X**  

4.  On the **Supported Platforms** page of the wizard, ensure that all Mac OS X versions are selected.  

5.  On the **Settings** page of the wizard, choose **New** and then, in the **Create Setting** dialog box, specify the following information:  

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

##  Use a certificate request and installation method that is independent from Configuration Manager  
 When you do not use Configuration Manager enrollment but instead, request and install the client certificate independently from Configuration Manager, the configuration steps are slightly different

Beging by performing *only* these steps:

a. [Deploy a web server certificate to site system servers](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Deploy a client authentication certificate to site system servers](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Configure the management point and distribution point](#configure-the-management-point-and-distribution-point)

d. [Optional: Install the reporting services point](#optional:-install-the-reporting-services-point)

e. [Download the client source files for Macs](#download-the-client-source-files-forMacs) .  
  

#### To install the client certificate independently from Configuration Manager and install the client  

1.  To install the client certificate independently from Configuration Manager, use the instructions that accompany your chosen certificate deployment method to request and install the client certificate on the Mac computer.  

2.  Navigate to the folder where you extracted the contents of the macclient.dmg file that you downloaded from the Microsoft Download Center.  

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

### Renewing the Mac client certificate  
 Use the following procedure before you renew the computer certificate on Mac computers.  

 This procedure removes the SMSID, which is required for the client to use a new or renewed certificate on the Mac computer.  

> [!IMPORTANT]  
>  When you remove and replace the client SMSID, any stored client history such as inventory is deleted after you delete the client from the Configuration Manager console.  

#### To renew the Mac client certificate  

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

17. Restart the Mac.  
