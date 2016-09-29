 ---
title: "Configuring certificate infrastructure | System Center Configuration Manager"
description: "Learn how to configure certificate enrollment in System Center Configuration Manager."
ms.custom: na
ms.date: 04/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigmanmanager: angrobe

---
# Certificate infrastructure

 Use the following table for the steps, details, and more information about how to configure certificate enrollment in System Center Configuration Manager. Before you start, check for any prerequisites that are listed in [Prerequisites for certificate profiles in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

 After you complete these steps and verify the installation, you can configure and deploy certificate profiles. For more information, see [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

|Steps|Details|More information|  
|-----------|-------------|----------------------|  
|**Step 1:** Install and configure the Network Device Enrollment Service and dependencies|The Network Device Enrollment Service role service for Active Directory Certificate Services (AD CS) must be running on the Windows Server 2012 R2 operating system.<br /><br /> **Important:** You must complete additional configuration steps before you can use the Network Device Enrollment Service with System Center Configuration Manager.|See [Step 1: Install and Configure the Network Device Enrollment Service and Dependencies](#BKMK_Step1) in this topic.|  
|**Step 2:** Install and configure the certificate registration point|You must install at least one certificate registration point. This registration point can be in a central administration site or a primary site.|See [Step 2: Install and Configure the Certificate Registration Point](#BKMK_Step2) in this topic.|  
|**Step 3:** Install the System Center Configuration Manager Policy Module|Install the Policy Module on the server that is running the Network Device Enrollment Service.|See [Step 3: Install the Configuration Manager Policy Module](#BKMK_Step3) in this topic.|  

## Supplemental Procedures to Configure Certificate Enrollment in Configuration Manager  
 Use the following information when the steps in the preceding table require supplemental procedures.  

###  <a name="BKMK_Step1"></a> Step 1: Install and Configure the Network Device Enrollment Service and Dependencies  
 You must install and configure the Network Device Enrollment Service role service for Active Directory Certificate Services (AD CS), change the security permissions on the certificate templates, deploy a public key infrastructure (PKI) client authentication certificate, and edit the registry to increase the Internet Information Services (IIS) default URL size limit. If necessary, you must also configure the issuing certification authority (CA) to allow a custom validity period.  

> [!IMPORTANT]  
>  Before you configure System Center Configuration Manager to work with the Network Device Enrollment Service, verify the installation and configuration of the Network Device Enrollment Service. If these dependencies are not working correctly, you will have difficulty troubleshooting certificate enrollment by using System Center Configuration Manager.  

##### To install and configure the Network Device Enrollment Service and dependencies  

1.  On a server that is running Windows Server 2012 R2, install and configure the Network Device Enrollment Service role service for the Active Directory Certificate Services server role. For more information, see [Network Device Enrollment Service Guidance](http://go.microsoft.com/fwlink/p/?LinkId=309016) in the Active Directory Certificate Services library on TechNet.  

2.  Check, and if necessary, modify the security permissions for the certificate templates that the Network Device Enrollment Service is using:  

    -   For the account that runs the System Center Configuration Manager console: **Read** permission.  

         This permission is required so that when you run the Create Certificate Profile Wizard, you can browse to select the certificate template that you want to use when you create a SCEP settings profile. Selecting a certificate template means that some settings in the wizard are automatically populated, so there is less for you to configure and there is less risk of selecting settings that are not compatible with the certificate templates that the Network Device Enrollment Service is using.  

    -   For the SCEP Service account that the Network Device Enrollment Service application pool uses: **Read** and **Enroll** permissions.  

         This requirement is not specific to System Center Configuration Manager but is part of configuring the Network Device Enrollment Service. For more information, see [Network Device Enrollment Service Guidance](http://go.microsoft.com/fwlink/p/?LinkId=309016) in the Active Directory Certificate Services library on TechNet.  

    > [!TIP]  
    >  To identify which certificate templates the Network Device Enrollment Service is using, view the following registry key on the server that is running the Network Device Enrollment Service: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

    > [!NOTE]  
    >  These are the default security permissions that will be appropriate for most environments. However, you can use an alternative security configuration. For more information, see [Planning for certificate template permissions for certificate profiles in System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3.  Deploy to this server a PKI certificate that supports client authentication. You might already have a suitable certificate installed on the computer that you can use, or you might have to (or prefer to) deploy a certificate specifically for this purpose. For more information about the requirements for this certificate, refer to the details for â€œServers running the Configuration Manager Policy Module with the Network Device Enrollment Service role serviceâ€ in the [PKI Certificates for Servers](../../core/plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers) section in the [PKI certificate requirements for System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) topic.  

    > [!TIP]  
    >  If you need help deploying this certificate, you can use the instructions for [Deploying the Client Certificate for Distribution Points](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_clientdistributionpoint2008_cm2012) in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic, because the certificate requirements are the same with one exception:  
    >   
    >  -   Do not select the **Allow private key to be exported** check box on the **Request Handling** tab of the properties for the certificate template.  
    >   
    >  You do not have to export this certificate with the private key because you will be able to browse to the local Computer store and select it when you configure the System Center Configuration Manager Policy Module.  

4.  Locate the root certificate that the client authentication certificate chains to. Then, export this root CA certificate to a certificate (.cer) file. Save this file to a secured location that you can securely access when you later install and configure the site system server for the certificate registration point.  

5.  On the same server, use the registry editor to increase the IIS default URL size limit by setting the following registry key DWORD values in HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

    -   Set the **MaxFieldLength** key to **65534**.  

    -   Set the **MaxRequestBytes** key to **16777216**.  

     For more information, see article [820129: Http.sys registry settings for Windows](http://go.microsoft.com/fwlink/?LinkId=309013) in the Microsoft Knowledge Base.  

6.  On the same server, in Internet Information Services (IIS) Manager, modify the request-filtering settings for the /certsrv/mscep application, and then restart the server. In the **Edit Request Filtering Settings** dialog box, the **Request Limits** settings should be as follows:  

    -   **Maximum allowed content length (Bytes)**: **30000000**  

    -   **Maximum URL length (Bytes)**: **65534**  

    -   **Maximum query string (Bytes)**: **65534**  

     For more information about these settings and how to configure them, see [Requests Limits](http://go.microsoft.com/fwlink/?LinkId=309014) in the IIS Reference Library.  

7.  If you want to be able to request a certificate that has a lower validity period than the certificate template that you are using: This configuration is disabled by default for an enterprise CA. To enable this option on an enterprise CA, use the Certutil command-line tool, and then stop and restart the certificate service by using the following commands:  

    1.  **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     For more information, see [Certificate Services Tools and Settings](http://go.microsoft.com/fwlink/p/?LinkId=309015) in the PKI Technologies library on TechNet.  

8.  Verify that the Network Device Enrollment Service is working by using the following link as an example: **https://server.contoso.com/certsrv/mscep/mscep.dll**. You should see the built-in Network Device Enrollment Service webpage. This webpage explains what the service is and explains that network devices use the URL to submit certificate requests.  

 Now that the Network Device Enrollment Service and dependencies are configured, you are ready to install and configure the certificate registration point.  

###  <a name="BKMK_Step2"></a> Step 2: Install and Configure the Certificate Registration Point  
 You must install and configure at least one certificate registration point in the System Center Configuration Manager hierarchy, and you can install this site system role in the central administration site or in a primary site.  

> [!IMPORTANT]  
>  Before you install the certificate registration point, see the **Site System Requirements** section in the [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) topic for operating system requirements and dependencies for the certificate registration point.  

##### To install and configure the certificate registration point  

1.  In the System Center Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, click **Servers and Site System Roles**, and then select the server that you want to use for the certificate registration point.  

3.  On the **Home** tab, in the **Server** group, click **Add Site System Roles**.  

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.  

5.  On the **Proxy** page, click **Next**. The certificate registration point does not use Internet proxy settings.  

6.  On the **System Role Selection** page, select **Certificate registration point** from the list of available roles, and then click **Next**.  

7.  On the **Certificate Registration Point** page, accept or change the default settings, and then click **Add**.  

8.  In the **Add URL and Root CA Certificate** dialog box, specify the following, and then click **OK**:  

    1.  **URL for the Network Device Enrollment Service**: Specify the URL in the following format: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. For example, if the FQDN of your server that is running the Network Device Enrollment Service is server1.contoso.com, type **https://server1.contoso.com/certsrv/mscep/mscep.dll**.  

    2.  **Root CA Certificate**: Browse to and select the certificate (.cer) file that you created and saved in **Step 1: Install and configure the Network Device Enrollment Service and dependencies**. This root CA certificate allows the certificate registration point to validate the client authentication certificate that the System Center Configuration Manager Policy Module will use.  

    > [!NOTE]  
    >  If you are using more than one server that is running the Network Device Enrollment Service, click **Add** to specify the details for the other servers.  

9. Click **Next** and complete the wizard.  

10. Wait a few minutes to let the installation finish, and then verify that the certificate registration point was installed successfully by using any of the following methods:  

    -   In the **Monitoring** workspace, expand **System Status**, click **Component Status**, and look for status messages from the **SMS_CERTIFICATE_REGISTRATION_POINT** component.  

    -   On the site system server, use the *<ConfigMgr Installation Path\>*\Logs\crpsetup.log file and *<ConfigMgr Installation Path\>*\Logs\crpmsi.log file. A successful installation will return an exit code of 0.  

    -   By using a browser, verify that you can connect to the URL of the certificate registration pointâ€”for example, https://server1.contoso.com/CMCertificateRegistration. You should see a **Server Error** page for the application name, with an HTTP 404 description.  

11. Locate the exported certificate file for the root CA that the certificate registration point automatically created in the following folder on the primary site server computer: *<ConfigMgr Installation Path\>*\inboxes\certmgr.box. Save this file to a secured location that you can securely access when you later install the System Center Configuration Manager Policy Module on the server that is running the Network Device Enrollment Service.  

    > [!TIP]  
    >  This certificate is not immediately available in this folder. You might need to wait awhile (for example, half an hour) before System Center Configuration Manager copies the file to this location.  

 Now that the certificate registration point is installed and configured, you are ready to install the System Center Configuration Manager Policy Module for the Network Device Enrollment Service.  

###  <a name="BKMK_Step3"></a> Step 3: Install the Configuration Manager Policy Module  
 You must install and configure the System Center Configuration Manager Policy Module on each server that you specified in **Step 2: Install and configure the certificate registration point** as **URL for the Network Device Enrollment Service** in the properties for the certificate registration point.  

##### To install the Policy Module  

1.  On the server that runs the Network Device Enrollment Service, log on as a domain administrator and copy the following files from the <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 folder on the System Center Configuration Manager installation media to a temporary folder:  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

     In addition, if you have a LanguagePack folder on the installation media, copy this folder and its contents.  

2.  From the temporary folder, run PolicyModuleSetup.exe to start the System Center Configuration Manager Policy Module Setup wizard.  

3.  On the initial page of the wizard, click **Next**, accept the license terms, and then click **Next**.  

4.  On the **Installation Folder** page, accept the default installation folder for the policy module or specify an alternative folder, and then click **Next**.  

5.  On the **Certificate Registration Point** page, specify the URL of the certificate registration point by using the FQDN of the site system server and the virtual application name that is specified in the properties for the certificate registration point. The default virtual application name is CMCertificateRegistration. For example, if the site system server has an FQDN of server1.contoso.com and you used the default virtual application name, specify **https://server1.contoso.com/CMCertificateRegistration**.  

6.  Accept the default port of **443** or specify the alternative port number that the certificate registration point is using, and then click **Next**.  

7.  On the **Client Certificate for the Policy Module**page, browse to and specify the client authentication certificate that you deployed in **Step 1: Install and configure the Network Device Enrollment Service and dependencies**, and then click **Next**.  

8.  On the **Certificate Registration Point Certificate** page, click **Browse** to select the exported certificate file for the root CA that you located and saved at the end of **Step 2: Install and configure the certificate registration point**.  

    > [!NOTE]  
    >  If you did not previously save this certificate file, it is located in the <ConfigMgr Installation Path\>\inboxes\certmgr.box on the site server computer.  

9. Click **Next** and complete the wizard.  

 Now that you have completed the configuration steps to install the Network Device Enrollment Service and dependencies, the certificate registration point, and the System Center Configuration Manager Policy Module, you are ready to deploy certificates to users and devices by creating and deploying certificate profiles. For more information about how to create certificate profiles, see [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

 If you want to uninstall the System Center Configuration Manager Policy Module, use **Programs and Features** in Control Panel.  

### See also  

 [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md)
