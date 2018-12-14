---
title: Deploy Mac clients
titleSuffix: Configuration Manager
description: Learn how to deploy clients to Mac computers in Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to deploy clients to Macs

*Applies to: System Center Configuration Manager (Current Branch)*

This article describes how to deploy and maintain the Configuration Manager client on Mac computers. To learn about what you have to configure before deploying clients to Mac computers, see [Prepare to deploy client software to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

When you install a new client for Mac computers, you might have to also install Configuration Manager updates to reflect the new client information in the Configuration Manager console.

In these procedures, you have two options for installing client certificates. Read more about client certificates for Macs in [Prepare to deploy client software to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

- Use Configuration Manager enrollment by using the [CMEnroll tool](#bkmk_enroll). The enrollment process doesn't support automatic certificate renewal. Re-enroll the Mac computer before the installed certificate expires.    

- [Use a certificate request and installation method that is independent from Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> To deploy the client to devices running macOS Sierra, correctly configure the **Subject name** of the management point certificate. For example, use the FQDN of the management point server.



## Configure client settings  

Use the [default client settings](/sccm/core/clients/deploy/about-client-settings) to configure enrollment for Mac computers. You can't use custom client settings. To request and install the certificate, the Configuration Manager client for Mac requires the default client settings.  

1. In the Configuration Manager console, go to the **Administration** workspace. Select the **Client Settings** node, and then select **Default Client Settings**.  

2. On the **Home** tab of the ribbon, in the **Properties** group, choose **Properties**.  

3. Select the **Enrollment** section, and then configure the following settings:  

    1. **Allow users to enroll mobile devices and Mac computers**: **Yes**  

    2. **Enrollment profile:** Choose **Set Profile**.  

4. In the **Mobile Device Enrollment Profile** dialog box, choose **Create**.  

5. In the **Create Enrollment Profile** dialog box, enter a name for this enrollment profile. Then configure the **Management site code**. Select the Configuration Manager primary site that contains the management points for these Mac computers.  

    > [!NOTE]  
    >  If you can't select the site, make sure that you configure at least one management point in the site to support mobile devices.  

6. Choose **Add**.  

7. In the **Add Certification Authority for Mobile Devices** window, select the certification authority server that issues certificates to Mac computers.  

8. In the **Create Enrollment Profile** dialog box, select the Mac computer certificate template that you previously created.  

9. Select **OK** to close the **Enrollment Profile** dialog box, and then  the **Default Client Settings** dialog box.  

    > [!TIP]  
    > If you want to change the client policy interval, use **Client policy polling interval** in the **Client Policy** client setting group.  

The next time the devices download client policy, Configuration Manager applies these settings for all users. To initiate policy retrieval for a single client, see [Initiate policy retrieval for a Configuration Manager client](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

In addition to the enrollment client settings, make sure that you have configured the following client device settings:  

- **Hardware inventory**: Enable and configure this feature if you want to collect hardware inventory from Mac and Windows client computers. For more information, see [How to extend hardware inventory](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

- **Compliance settings**: Enable and configure this feature if you want to evaluate and remediate settings on Mac and Windows client computers. For more information, see [Plan for and configure compliance settings](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

For more information, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).  



## <a name="bkmk_download"></a> Download the Mac client  

1. Download the Mac OS X client file package from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Save **ConfigmgrMacClient.msi** to a computer that runs Windows. This file isn't on the Configuration Manager installation media.  

2. Run the installer on the Windows computer. Extract the Mac client package, **Macclient.dmg**, to a folder on the local disk. The default path is `C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client`.  

3. Copy the **Macclient.dmg** file to a folder on the Mac computer.  

4. On the Mac computer, run **Macclient.dmg** to extract the files to a folder on the local disk.  

5. In the folder, make sure that it contains the following files: 

	- **Ccmsetup**: Installs the Configuration Manager client on your Mac computers using **CMClient.pkg**  

	- **CMDiagnostics**: Collects diagnostic information related to the Configuration Manager client on your Mac computers  

	- **CMUninstall**: Uninstalls the client from your Mac computers  

	- **CMAppUtil**: Converts Apple application packages into a format that you can deploy as a Configuration Manager application  

	- **CMEnroll**: Requests and installs the client certificate for a Mac computer so that you can then install the Configuration Manager client  



## <a name="bkmk_enroll"></a> Enroll the Mac client  

Enroll individual clients with the [Mac computer enrollment wizard](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

To automate enrollment for many clients, use the [CMEnroll tool](#client-and-certificate-automation-with-cmenroll).   


### Enroll the client with the Mac computer enrollment wizard  

1. After you install the client, the Computer Enrollment wizard opens. To manually start the wizard, select **Enroll** from the **Configuration Manager** preference page.  

2. On the second page of the wizard, provide the following information:  

   - **User name**: The user name can be in the following formats:  

     - `domain\name`. For example: `contoso\mnorth`  

     - `user@domain`. For example: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  When you use an email address to populate the **User name** field, Configuration Manager automatically populates the **Server name** field. It uses the default name of the enrollment proxy point server and the domain name of the email address. If these names don't match the name of the enrollment proxy point server, fix the **Server name** during enrollment.  

       The user name and corresponding password must match an Active Directory user account that has **Read** and **Enroll** permissions on the Mac client certificate template.  

   - **Server name**: The name of the enrollment proxy point server.  


### Client and certificate automation with CMEnroll  

Use this procedure for automation of client installation and requesting and enrollment of client certificates with the CMEnroll tool. To run the tool, you must have an Active Directory user account.

1. On the Mac computer, navigate to the folder where you extracted the contents of the **Macclient.dmg** file.  

2. Enter the following command: `sudo ./ccmsetup`  

3. Wait until you see the **Completed installation** message. Although the installer displays a message that you must restart now, don't restart, and continue to the next step.  

4. From the **Tools** folder on the Mac computer, type the following command: `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

	After the client installs, the Mac Computer Enrollment wizard opens to help you enroll the Mac computer. For more information, see [Enroll the client by using the Mac computer enrollment wizard](#bkmk_enroll).  

     Example: If the enrollment proxy point server is named **server02.contoso.com**, and you grant **contoso\mnorth** permissions for the Mac client certificate template, type the following command: `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > If the user name includes any of the following characters, enrollment fails: `<>"+=,`. Use an out-of-band certificate with a user name that doesn't include these characters.  
    >  
    > For a more seamless user experience, script the installation steps. Then users only have to supply their user name and password.  

5. Type the password for the Active Directory user account. When you enter this command, it prompts for two passwords. The first password is for the super user account to run the command. The second prompt is for the Active Directory user account. The prompts look identical, so make sure that you specify them in the correct sequence.  

6. Wait until you see the **Successfully enrolled** message.  

7. To limit the enrolled certificate to Configuration Manager, on the Mac computer, open a terminal window and make the following changes:  

    1. Enter the command `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. In the **Keychain Access** window, in the **Keychains** section, choose **System**. Then in the **Category** section, choose **Keys**.  

    3. Expand the keys to view the client certificates. Find the certificate with a private key that you installed, and open the key.  

    4. On the **Access Control** tab, choose **Confirm before allowing access**.  

    5. Browse to **/Library/Application Support/Microsoft/CCM**, select **CCMClient**, and then choose **Add**.  

    6. Choose **Save Changes** and close the **Keychain Access** dialog box.  

8. Restart the Mac computer.  

To verify that the client installation is successful, open the **Configuration Manager** item in **System Preferences** on the Mac computer. Also update and view the **All Systems** collection in the Configuration Manager console. Confirm that the Mac computer appears in this collection as a managed client.  

> [!TIP]  
> To help troubleshoot the Mac client, use the **CMDiagnostics** tool included with the Mac client package. Use it to collect the following diagnostic information:  
>   
> - A list of running processes  
> - The Mac OS X operating system version  
> - Mac OS X crash reports relating to the Configuration Manager client including **CCM\*.crash** and **System Preference.crash**.  
> - The Bill of Materials (BOM) file and property list (.plist) file created by the Configuration Manager client installation.  
> - The contents of the folder **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> The information collected by CmDiagnostics is added to a zip file that is saved to the desktop of the computer and is named `cmdiag-<hostname>-<datetime>.zip`



## <a name="bkmk_external"></a> Manage certificates external to Configuration Manager

You can use a certificate request and installation method independent from Configuration Manager. Use the same general process, but include the following additional steps: 

- When you install the Configuration Manager client, use the **MP** and **SubjectName** command-line options. Enter the following command: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. The certificate subject name is case-sensitive, so type it exactly as it appears in the certificate details.  

     Example: The management point's internet FQDN is **server03.contoso.com**. The Mac client certificate has the FQDN of **mac12.contoso.com** as a common name in the certificate subject. Use the following command: `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- If you have more than one certificate that contains the same subject value, specify the certificate serial number to use for the Configuration Manager client. Use the following command: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     For example: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## Renew the Mac client certificate  

This procedure removes the SMSID. The Configuration Manager client for Mac requires a new ID to use a new or renewed certificate.  

> [!IMPORTANT]  
> After you replace the client SMSID, when you delete the old resource in the Configuration Manager console, you also delete any stored client history. For example, hardware inventory history for that client.  


1. Create and populate a device collection for the Mac computers that must renew the computer certificates.  

2. In the **Assets and Compliance** workspace, start the **Create Configuration Item Wizard**.  

3. On the **General** page of the wizard, specify the following information:  

    - **Name**: **Remove SMSID for Mac**  

    - **Type**: **Mac OS X**  

4. On the **Supported Platforms** page, select all Mac OS X versions.  

5. On the **Settings** page, select **New**. In the **Create Setting** window, specify the following information:  

    - **Name**: **Remove SMSID for Mac**  

    - **Setting type**: **Script**  

    - **Data type**: **String**  

6. In the **Create Setting** window, for **Discovery script**, select **Add script**. This action specifies a script to discover Mac computers configured with an SMSID.  

7. In the **Edit Discovery Script** window, enter the following shell script:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Choose **OK** to close the **Edit Discovery Script** window.  

9. In the **Create Setting** window, for **Remediation script (optional)**, choose **Add script**. This action specifies a script to remove the SMSID when it's found on Mac computers.  

10. In the **Create Remediation Script** window, enter the following shell script:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choose **OK** to close the **Create Remediation Script** window.  

12. On the **Compliance Rules** page, choose **New**. Then in the **Create Rule** window, specify the following information:  

    - **Name**: **Remove SMSID for Mac**  

    - **Selected setting**: Choose **Browse** and then select the discovery script that you previously specified.  

    - In **the following values** field: **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    - Enable the option to **Run the specified remediation script when this setting is noncompliant**.  

13. Complete the wizard.  

14. Create a configuration baseline that contains this configuration item. Deploy the baseline to the target collection.  

     For more information, see [How to create configuration baselines](/sccm/compliance/deploy-use/create-configuration-baselines).  

15. After you install a new certificate on Mac computers that have the SMSID removed, run the following command to configure the client to use the new certificate:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## See also

[Prepare to deploy clients to Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)

[Maintain Mac clients](/sccm/core/clients/manage/maintain-mac-clients)
