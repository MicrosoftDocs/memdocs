---
title: "Deployment PKI certificates"
titleSuffix: "Configuration Manager"
description: "Follow a step-by-step example to learn how to create and deploy PKI certificates that System Center Configuration Manager uses."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: arob98
ms.author: angrobe
manager: angrobe

---
# Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 certification authority

*Applies to: System Center Configuration Manager (Current Branch)*

This step-by-step example deployment, which uses a Windows Server 2008 certification authority (CA), has procedures that show you how to create and deploy the public key infrastructure (PKI) certificates that System Center Configuration Manager uses. These procedures use an enterprise certification authority (CA) and certificate templates. The steps are appropriate for a test network only, as a proof of concept.  

 Because there is no single method of deployment for the required certificates, consult your particular PKI deployment documentation for the required procedures and best practices to deploy the required certificates for a production environment. For more about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  You can adapt the instructions in this topic for operating systems that are not documented in the Test Network Requirements section. However, if you are running the issuing CA on Windows Server 2012, you are not prompted for the certificate template version. Instead, specify this on the **Compatibility** tab of the template properties:  
>   
>  -   **Certification Authority**: **Windows Server 2003**  
> -   **Certificate recipient**: **Windows XP / Server 2003**  

## In this section  
 The following sections include example step-by-step instructions to create and deploy the following certificates that can be used with System Center Configuration Manager:  

 [Test network requirements](#BKMK_testnetworkenvironment)  

 [Overview of the certificates](#BKMK_overview2008)  

 [Deploy the web server certificate for site systems that run IIS](#BKMK_webserver2008_cm2012)  

 [Deploy the service certificate for cloud-based distribution points](#BKMK_clouddp2008_cm2012)  

 [Deploy the client certificate for Windows computers](#BKMK_client2008_cm2012)  

 [Deploy the client certificate for distribution points](#BKMK_clientdistributionpoint2008_cm2012)  

 [Deploy the enrollment certificate for mobile devices](#BKMK_mobiledevices2008_cm2012)  

 [Deploy the certificates for AMT](#BKMK_AMT2008_cm2012)  

 [Deploy the client Certificate for Mac computers](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a> Test network requirements  
 The step-by-step instructions have the following requirements:  

-   The test network is running Active Directory Domain Services with Windows Server 2008, and it is installed as a single domain, single forest.  

-   You have a member server running Windows Server 2008 Enterprise Edition, which has the Active Directory Certificate Services role installed on it, and it is set up as an enterprise root certification authority (CA).  

-   You have one computer that has Windows Server 2008 (Standard Edition or Enterprise Edition, R2 or later) installed on it, that computer is designated as a member server, and Internet Information Services (IIS) is installed on it. This computer will be the System Center Configuration Manager site system server that you will configure with an intranet fully qualified domain name (FQDN) to support client connections on the intranet and an Internet FQDN if you must support mobile devices that are enrolled by System Center Configuration Manager and clients on the Internet.  

-   You have one Windows Vista client that has the latest service pack installed, and this computer is set up with a computer name that comprises ASCII characters and is joined to the domain. This computer will be a System Center Configuration Manager client computer.  

-   You can sign in with a root domain administrator account or an enterprise domain administrator account and use this account for all procedures in this example deployment.  

##  <a name="BKMK_overview2008"></a> Overview of the certificates  
 The following table lists the types of PKI certificates that might be required for System Center Configuration Manager and describes how they are used.  

|Certificate Requirement|Certificate Description|  
|-----------------------------|-----------------------------|  
|Web server certificate for site systems that run IIS|This certificate is used to encrypt data and authenticate the server to clients. It must be installed externally from System Center Configuration Manager on site systems servers that run Internet Information Services (IIS) and that are set up in System Center Configuration Manager to use HTTPS.<br /><br /> For the steps to set up and install this certificate, see [Deploy the web server certificate for site systems that run IIS](#BKMK_webserver2008_cm2012) in this topic.|  
|Service certificate for clients to connect to cloud-based distribution points|For the steps to configure and install this certificate, see [Deploy the service certificate for cloud-based distribution points](#BKMK_clouddp2008_cm2012) in this topic.<br /><br /> **Important:** This certificate is used in conjunction with the Windows Azure management certificate. For more about the management certificate, see [How to Create a Management Certificate](http://go.microsoft.com/fwlink/p/?LinkId=220281) and [How to Add a Management Certificate to a Windows Azure Subscription](http://go.microsoft.com/fwlink/?LinkId=241722) in the Windows Azure Platform section of the MSDN Library.|  
|Client certificate for Windows computers|This certificate is used to authenticate System Center Configuration Manager client computers to site systems that are set up to use HTTPS. It can also be used for management points and state migration points to monitor their operational status when they are set up to use HTTPS. It must be installed externally from System Center Configuration Manager on computers.<br /><br /> For the steps to set up and install this certificate, see [Deploy the client certificate for Windows computers](#BKMK_client2008_cm2012) in this topic.|  
|Client certificate for distribution points|This certificate has two purposes:<br /><br /> The certificate is used to authenticate the distribution point to an HTTPS-enabled management point before the distribution point sends status messages.<br /><br /> When the **Enable PXE support for clients** distribution point option is selected, the certificate is sent to computers that PXE boot so that they can connect to a HTTPS-enabled management point during the deployment of the operating system.<br /><br /> For the steps to set up and install this certificate, see [Deploy the client certificate for distribution points](#BKMK_clientdistributionpoint2008_cm2012) in this topic.|  
|Enrollment certificate for mobile devices|This certificate is used to authenticate System Center Configuration Manager mobile device clients to site systems that are set up to use HTTPS. It must be installed as part of mobile device enrollment in System Center Configuration Manager, and you choose the configured certificate template as a mobile device client setting.<br /><br /> For the steps to set up this certificate, see [Deploy the enrollment certificate for mobile devices](#BKMK_mobiledevices2008_cm2012) in this topic.|  
|Certificates for Intel AMT|Three certificates relate to out-of-band management for Intel AMT-based computers:<ul><li>An  Active Management Technology (AMT) provisioning certificate</li><li>An AMT web server certificate</li><li>Optionally, a client authentication certificate for 802.1X wired or wireless networks</li></ul>The AMT provisioning certificate must be installed externally from System Center Configuration Manager on the out-of-band service point computer, and then you choose the installed certificate in the out-of-band service point properties. The AMT web server certificate and the client authentication certificate are installed during AMT provisioning and management, and you choose the configured certificate templates in the out-of-band management component properties.<br /><br /> For the steps to set up these certificates, see [Deploy the certificates for AMT](#BKMK_AMT2008_cm2012) in this topic.|  
|Client certificate for Mac computers|You can request and install this certificate from a Mac computer when you use System Center Configuration Manager enrollment and choose the configured certificate template as a mobile device client setting.<br /><br /> For the steps to set up this certificate, see [Deploy the client certificate for Mac computers](#BKMK_MacClient_SP1) in this topic.|  

##  <a name="BKMK_webserver2008_cm2012"></a> Deploy the web server certificate for site systems that run IIS  
 This certificate deployment has the following procedures:  

-   Create and issue the web server certificate template on the certification authority  

-   Request the web server certificate  

-   Configure IIS to use the web server certificate  

###  <a name="BKMK_webserver22008"></a> Create and issue the web server certificate template on the certification authority  
 This procedure creates a certificate template for System Center Configuration Manager site systems and adds it to the certification authority.  

##### To create and issue the web server certificate template on the certification authority  

1.  Create a security group named **ConfigMgr IIS Servers** that has the member servers to install System Center Configuration Manager site systems that will run IIS.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates** and then choose **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that has **Web Server** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Web Server Certificate**, to generate the web certificates that will be used on Configuration Manager site systems.  

6.  Choose the **Subject Name** tab, and make sure that **Supply in the request** is selected.  

7.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

8.  Choose **Add**, enter **ConfigMgr IIS Servers** in the text box, and then choose **OK**.  

9. Choose the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Choose **OK**, and then close the **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Web Server Certificate**, and then choose **OK**.  

13. If you do not need to create and issue more certificates, close **Certification Authority**.  

###  <a name="BKMK_webserver32008"></a> Request the web server certificate  
 This procedure lets you specify the intranet and Internet FQDN values that will be set up in the site system server properties and then installs the web server certificate on to the member server that runs IIS.  

##### To request the web server certificate  

1.  Restart the member server that runs IIS to ensure that the computer can access the certificate template that you created by using the **Read** and **Enroll** permissions that you configured.  

2.  Choose **Start**, choose **Run**, and then type **mmc.exe.** In the empty console, choose **File**, and then choose **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, choose **Certificates** from the list of **Available snap-ins**, and then choose **Add**.  

4.  In the **Certificate snap-in** dialog box, choose **Computer account**, and then choose **Next**.  

5.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then choose **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, choose **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then choose **Personal**.  

8.  Right-click **Certificates**, choose **All Tasks**, and then choose **Request New Certificate**.  

9. On the **Before You Begin** page, choose **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, choose **Next**.  

11. On the **Request Certificates** page, identify the **ConfigMgr Web Server Certificate** from the list of available certificates, and then choose **More information is required to enroll for this certificate. Click here to configure settings**.  

12. In the **Certificate Properties** dialog box, in the **Subject** tab, do not make any changes to **Subject name**. This means that the **Value** box for the **Subject name** section remains blank. Instead, from the **Alternative name** section, choose the **Type** drop-down list, and then choose **DNS**.  

13. In the **Value** box, specify the FQDN values that you will specify in the System Center Configuration Manager site system properties, and then choose **OK** to close the **Certificate Properties** dialog box.  

     Examples:  

    -   If the site system will only accept client connections from the intranet, and the intranet FQDN of the site system server is **server1.internal.contoso.com**, enter **server1.internal.contoso.com**, and then choose **Add**.  

    -   If the site system will accept client connections from the intranet and the Internet, and the intranet FQDN of the site system server is **server1.internal.contoso.com** and the Internet FQDN of the site system server is **server.contoso.com**:  

        1.  Enter **server1.internal.contoso.com**, and then choose **Add**.  

        2.  Enter **server.contoso.com**, and then choose **Add**.  

        > [!NOTE]  
        >  You can specify the FQDNs for System Center Configuration Manager in any order. However, check that all devices that will use the certificate, such as mobile devices and proxy web servers, can use a certificate subject alternative name (SAN) and multiple values in the SAN. If devices have limited support for SAN values in certificates, you might have to change the order of the FQDNs or use the Subject value instead.  

14. On the **Request Certificates** page, choose **ConfigMgr Web Server Certificate** from the list of available certificates, and then choose **Enroll**.  

15. On the **Certificates Installation Results** page, wait until the certificate is installed, and then choose **Finish**.  

16. Close **Certificates (Local Computer)**.  

###  <a name="BKMK_webserver42008"></a> Configure IIS to use the web server certificate  
 This procedure binds the installed certificate to the IIS **Default Web Site**.  

##### To set up IIS to use the web server certificate  

1.  On the member server that has IIS installed, choose **Start**, choose **Programs**, choose **Administrative Tools**, and then choose **Internet Information Services (IIS) Manager**.  

2.  Expand **Sites**, right-click **Default Web Site**, and then choose **Edit Bindings**.  

3.  Choose the **https** entry, and then choose **Edit**.  

4.  In the **Edit Site Binding** dialog box, select the certificate that you requested by using the ConfigMgr Web Server Certificates template, and then choose **OK**.  

    > [!NOTE]  
    >  If you are not sure which is the correct certificate, choose one, and then choose **View**. This lets you compare the selected certificate details to the certificates in the Certificates snap-in. For example, the Certificates snap-in shows the certificate template that was used to request the certificate. You can then compare the certificate thumbprint of the certificate that was requested by using the ConfigMgr Web Server Certificates template to the certificate thumbprint of the certificate currently selected in the **Edit Site Binding** dialog box.  

5.  Choose **OK** in the **Edit Site Binding** dialog box, and then choose **Close**.  

6.  Close **Internet Information Services (IIS) Manager**.  

 The member server is now set up with a System Center Configuration Manager web server certificate.  

> [!IMPORTANT]  
>  When you install the System Center Configuration Manager site system server on this computer, make sure that you specify the same FQDNs in the site system properties as you specified when you requested the certificate.  

##  <a name="BKMK_clouddp2008_cm2012"></a> Deploy the service certificate for cloud-based distribution points  

This certificate deployment has the following procedures:  

-   [Create and issue a custom web server certificate template on the certification authority](#BKMK_clouddpcreating2008)  

-   [Request the custom web server certificate](#BKMK_clouddprequesting2008)  

-   [Export the custom web server certificate for cloud-based distribution points](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a> Create and issue a custom web server certificate template on the certification authority  
 This procedure creates a custom certificate template that is based on the web server certificate template. The certificate is for System Center Configuration Manager cloud-based distribution points and the private key must be exportable. After the certificate template is created, it is added to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the web server certificate template that you created for site systems that run IIS. Although both certificates require server authentication capability, the certificate for cloud-based distribution points requires you to enter a custom-defined value for the Subject Name and the private key must be exported. As a security best practice, do not set up certificate templates so that the private key can be exported unless this configuration is required. The cloud-based distribution point requires this configuration because you must import the certificate as a file, rather than choose it from the certificate store.  
>   
>  When you create a new certificate template for this certificate, you can restrict the computers that can request a certificate whose private key can be exported. On a production network, you might also consider adding the following changes for this certificate:  
>   
>  -   Require approval to install the certificate for additional security.  
> -   Increase the certificate validity period. Because you must export and import the certificate each time before it expires, an increase of the validity period reduces how often you must repeat this procedure. However, an increase of the validity period also decreases the security of the certificate because it provides more time for an attacker to decrypt the private key and steal the certificate.  
> -   Use a custom value in the certificate Subject Alternative Name (SAN) to help identify this certificate from standard web server certificates that you use with IIS.  

##### To create and issue the custom web server certificate template on the certification authority  

1.  Create a security group named **ConfigMgr Site Servers** that has the member servers to install System Center Configuration Manager primary site servers that will manage cloud-based distribution points.  

2.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that has **Web Server** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Cloud-Based Distribution Point Certificate**, to generate the web server certificate for cloud-based distribution points.  

6.  Choose the **Request Handling** tab, and then choose **Allow private key to be exported**.  

7.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Enterprise Admins** security group.  

8.  Choose **Add**, enter **ConfigMgr Site Servers** in the text box, and then choose **OK**.  

9. Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Choose **OK**, and then close **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Cloud-Based Distribution Point Certificate**, and then choose **OK**.  

13. If you do not have to create and issue more certificates, close **Certification Authority**.  

###  <a name="BKMK_clouddprequesting2008"></a> Request the custom web server certificate  
 This procedure requests and then installs the custom web server certificate on the member server that will run the site server.  

##### To request the custom web server certificate  

1.  Restart the member server after you create and configure the **ConfigMgr Site Servers** security group to ensure that the computer can access the certificate template that you created by using the **Read** and **Enroll** permissions that you configured.  

2.  Choose **Start**, choose **Run**, and then enter **mmc.exe.** In the empty console, choose **File**, and then choose **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, choose **Certificates** from the list of **Available snap-ins**, and then choose **Add**.  

4.  In the **Certificate snap-in** dialog box, choose **Computer account**, and then choose **Next**.  

5.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then choose **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, choose **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then choose **Personal**.  

8.  Right-click **Certificates**, choose **All Tasks**, and then choose **Request New Certificate**.  

9. On the **Before You Begin** page, choose **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, choose **Next**.  

11. On the **Request Certificates** page, identify the **ConfigMgr Cloud-Based Distribution Point Certificate** from the list of available certificates, and then choose **More information is required to enroll for this certificate. choose here to configure settings**.  

12. In the **Certificate Properties** dialog box, in the **Subject** tab, for the **Subject name**, choose **Common name** as the **Type**.  

13. In the **Value** box, specify your choice of service name and your domain name by using an FQDN format. For example: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Make the service name unique in your namespace. You will use DNS to create an alias (CNAME record) to map this service name to an automatically generated identifier (GUID) and an IP address from Windows Azure.  

14. Choose **Add**, and then choose **OK** to close the **Certificate Properties** dialog box.  

15. On the **Request Certificates** page, choose **ConfigMgr Cloud-Based Distribution Point Certificate** from the list of available certificates, and then choose **Enroll**.  

16. On the **Certificates Installation Results** page, wait until the certificate is installed, and then choose **Finish**.  

17. Close **Certificates (Local Computer)**.  

###  <a name="BKMK_clouddpexporting2008"></a> Export the custom web server certificate for cloud-based distribution points  
 This procedure exports the custom web server certificate to a file, so that it can be imported when you create the cloud-based distribution point.  

##### To export the custom web server certificate for cloud-based distribution points  

1.  In the **Certificates (Local Computer)** console, right-click the certificate that you just installed, choose **All Tasks**, and then choose **Export**.  

2.  In the Certificates Export Wizard, choose **Next**.  

3.  On the **Export Private Key** page, choose **Yes, export the private key**, and then choose **Next**.  

    > [!NOTE]  
    >  If this option is not available, the certificate has been created without the option to export the private key. In this scenario, you cannot export the certificate in the required format. You must set up the certificate template so that the private key can be exported, and then request the certificate again.  

4.  On the **Export File Format** page, ensure that the **Personal Information Exchange - PKCS #12 (.PFX)** option is selected.  

5.  On the **Password** page, specify a strong password to protect the exported certificate with its private key, and then choose **Next**.  

6.  On the **File to Export** page, specify the name of the file that you want to export, and then choose **Next**.  

7.  To close the wizard, choose **Finish** in the **Certificate Export Wizard** page, and then choose **OK** in the confirmation dialog box.  

8.  Close **Certificates (Local Computer)**.  

9. Store the file securely and ensure that you can access it from the System Center Configuration Manager console.  

 The certificate is now ready to be imported when you create a cloud-based distribution point.  

##  <a name="BKMK_client2008_cm2012"></a> Deploy the client certificate for Windows computers  
 This certificate deployment has the following procedures:  

-   Create and issue the Workstation Authentication certificate template on the certification authority  

-   Configure autoenrollment of the Workstation Authentication template by using Group Policy  

-   Automatically enroll the Workstation Authentication certificate and verify its installation on computers  

###  <a name="BKMK_client02008"></a> Create and issue the Workstation Authentication certificate template on the certification authority  
 This procedure creates a certificate template for System Center Configuration Manager client computers and adds it to the certification authority.  

##### To create and issue the Workstation Authentication certificate template on the certification authority  

1.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the Certificate Templates management console.  

2.  In the results pane, right-click the entry that has **Workstation Authentication** in the **Template Display Name** column, and then choose **Duplicate Template**.  

3.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

4.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Client Certificate**, to generate the client certificates that will be used on Configuration Manager client computers.  

5.  Choose the **Security** tab, select the **Domain Computers** group, and then select the additional permissions of **Read** and **Autoenroll**. Do not clear **Enroll**.  

6.  Choose **OK**, and then close **Certificate Templates Console**.  

7.  In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

8.  In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Client Certificate**, and then choose **OK**.  

9. If you do not need to create and issue more certificates, close **Certification Authority**.  

###  <a name="BKMK_client12008"></a> Configure autoenrollment of the Workstation Authentication template by using Group Policy  
 This procedure sets up Group Policy to autoenroll the client certificate on computers.  

##### To set up autoenrollment of the Workstation Authentication template by using Group Policy  

1.  On the domain controller, choose **Start**, choose **Administrative Tools**, and then choose **Group Policy Management**.  

2.  Go to your domain, right-click the domain, and then choose **Create a GPO in this domain, and Link it here**.  

    > [!NOTE]  
    >  This step uses the best practice of creating a new Group Policy for custom settings rather than editing the Default Domain Policy that is installed with Active Directory Domain Services. When you assign this Group Policy at the domain level, you will apply it to all computers in the domain. In a production environment, you can restrict the autoenrollment so that it enrolls on only selected computers. You can assign the Group Policy at an organizational unit level, or you can filter the domain Group Policy with a security group so that it applies only to the computers in the group. If you restrict autoenrollment, remember to include the server that is set up as the management point.  

3.  In the **New GPO** dialog box, enter a name, like **Autoenroll Certificates**, for the new Group Policy, and then choose **OK**.  

4.  In the results pane, on the **Linked Group Policy Objects** tab, right-click the new Group Policy, and then choose **Edit**.  

5.  In the **Group Policy Management Editor**, expand **Policies** under **Computer Configuration**, and then go to **Windows Settings** / **Security Settings** / **Public Key Policies**.  

6.  Right-click the object type named **Certificate Services Client - Auto-enrollment**, and then choose **Properties**.  

7.  From the **Configuration Model** drop-down list, choose **Enabled**, choose **Renew expired certificates, update pending certificates, remove revoked certificates**, choose **Update certificates that use certificate templates**, and then choose **OK**.  

8.  Close **Group Policy Management**.  

###  <a name="BKMK_client22008"></a> Automatically enroll the Workstation Authentication certificate and verify its installation on computers  
 This procedure installs the client certificate on computers and verifies the installation.  

##### To automatically enroll the Workstation Authentication certificate and verify its installation on the client computer  

1.  Restart the workstation computer, and wait a few minutes before you sign in.  

    > [!NOTE]  
    >  Restarting a computer is the most reliable method of ensuring success with certificate autoenrollment.  

2.  Sign in with an account that has administrative privileges.  

3.  In the search box, enter **mmc.exe.**, and then press **Enter**.  

4.  In the empty management console, choose **File**, and then choose **Add/Remove Snap-in**.  

5.  In the **Add or Remove Snap-ins** dialog box, choose **Certificates** from the list of **Available snap-ins**, and then choose **Add**.  

6.  In the **Certificate snap-in** dialog box, choose **Computer account**, and then choose **Next**.  

7.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then choose **Finish**.  

8.  In the **Add or Remove Snap-ins** dialog box, choose **OK**.  

9. In the console, expand **Certificates (Local Computer)**, expand **Personal**, and then choose **Certificates**.  

10. In the results pane, confirm that a certificate has **Client Authentication** in the **Intended Purpose** column, and that **ConfigMgr Client Certificate** is in the **Certificate Template** column.  

11. Close **Certificates (Local Computer)**.  

12. Repeat steps 1 through 11 for the member server to verify that the server that will be set up as the management point also has a client certificate.  

 The computer is now set up with a System Center Configuration Manager client certificate.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a> Deploy the client certificate for distribution points  

> [!NOTE]  
>  This certificate can also be used for media images that do not use PXE boot, because the certificate requirements are the same.  

 This certificate deployment has the following procedures:  

-   Create and issue a custom Workstation Authentication certificate template on the certification authority  

-   Request the custom Workstation Authentication certificate  

-   Export the client certificate for distribution points  

###  <a name="BKMK_clientdistributionpoint02008"></a> Create and issue a custom Workstation Authentication certificate template on the certification authority  
 This procedure creates a custom certificate template for System Center Configuration Manager distribution points so that the private key can be exported and adds the certificate template to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the certificate template that you created for client computers. Although both certificates require client authentication capability, the certificate for distribution points requires that the private key is exported. As a security best practice, do not set up certificate templates so the private key can be exported unless this configuration is required. The distribution point requires this configuration because you must import the certificate as a file rather than choose it from the certificate store.  
>   
>  When you create a new certificate template for this certificate, you can restrict the computers that can request a certificate whose private key can be exported. In our example deployment, this will be the security group that you previously created for System Center Configuration Manager site system servers that run IIS. On a production network that distributes the IIS site system roles, consider creating a new security group for the servers that run distribution points so that you can restrict the certificate to just these site system servers. You might also consider adding the following modifications for this certificate:  
>   
>  -   Require approval to install the certificate for additional security.  
> -   Increase the certificate validity period. Because you must export and import the certificate each time before it expires, an increase of the validity period reduces how often you must repeat this procedure. However, an increase of the validity period also decreases the security of the certificate because it provides more time for an attacker to decrypt the private key and steal the certificate.  
> -   Use a custom value in the certificate Subject field or Subject Alternative Name (SAN) to help identify this certificate from standard client certificates. This can be particularly helpful if you will use the same certificate for multiple distribution points.  

##### To create and issue the custom Workstation Authentication certificate template on the certification authority  

1.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the Certificate Templates management console.  

2.  In the results pane, right-click the entry that has **Workstation Authentication** in the **Template Display Name** column, and then choose **Duplicate Template**.  

3.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

4.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Client Distribution Point Certificate**, to generate the client authentication certificate for distribution points.  

5.  Choose the **Request Handling** tab, and then choose **Allow private key to be exported**.  

6.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Enterprise Admins** security group.  

7.  Choose **Add**, enter **ConfigMgr IIS Servers** in the text box, and then choose **OK**.  

8.  Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

9. Choose **OK**, and then close **Certificate Templates Console**.  

10. In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

11. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Client Distribution Point Certificate**, and then choose **OK**.  

12. If you do not have to create and issue more certificates, close **Certification Authority**.  

###  <a name="BKMK_clientdistributionpoint12008"></a> Request the custom Workstation Authentication certificate  
 This procedure requests and then installs the custom client certificate on to the member server that runs IIS and that will be set up as a distribution point.  

##### To request the custom Workstation Authentication certificate  

1.  Choose **Start**, choose **Run**, and then enter **mmc.exe.** In the empty console, choose **File**, and then choose **Add/Remove Snap-in**.  

2.  In the **Add or Remove Snap-ins** dialog box, choose **Certificates** from the list of **Available snap-ins**, and then choose **Add**.  

3.  In the **Certificate snap-in** dialog box, choose **Computer account**, and then choose **Next**.  

4.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then choose **Finish**.  

5.  In the **Add or Remove Snap-ins** dialog box, choose **OK**.  

6.  In the console, expand **Certificates (Local Computer)**, and then choose **Personal**.  

7.  Right-click **Certificates**, choose **All Tasks**, and then choose **Request New Certificate**.  

8.  On the **Before You Begin** page, choose **Next**.  

9. If you see the **Select Certificate Enrollment Policy** page, choose **Next**.  

10. On the **Request Certificates** page, choose **ConfigMgr Client Distribution Point Certificate** from the list of available certificates, and then choose **Enroll**.  

11. On the **Certificates Installation Results** page, wait until the certificate is installed, and then choose **Finish**.  

12. In the results pane, confirm that a certificate has **Client Authentication** in the **Intended Purpose** column and that **ConfigMgr Client Distribution Point Certificate** is in the **Certificate Template** column.  

13. Do not close **Certificates (Local Computer)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a> Export the client certificate for distribution points  
 This procedure exports the custom Workstation Authentication certificate to a file so that it can be imported in the distribution point properties.  

##### To export the client certificate for distribution points  

1.  In the **Certificates (Local Computer)** console, right-click the certificate that you just installed, choose **All Tasks**, and then choose **Export**.  

2.  In the Certificates Export Wizard, choose **Next**.  

3.  On the **Export Private Key** page, choose **Yes, export the private key**, and then choose **Next**.  

    > [!NOTE]  
    >  If this option is not available, the certificate has been created without the option to export the private key. In this scenario, you cannot export the certificate in the required format. You must set up the certificate template so that the private key can be exported and then request the certificate again.  

4.  On the **Export File Format** page, ensure that the **Personal Information Exchange - PKCS #12 (.PFX)** option is selected.  

5.  On the **Password** page, specify a strong password to protect the exported certificate with its private key, and then choose **Next**.  

6.  On the **File to Export** page, specify the name of the file that you want to export, and then choose **Next**.  

7.  To close the wizard, choose **Finish** on the **Certificate Export Wizard** page, and choose **OK** in the confirmation dialog box.  

8.  Close **Certificates (Local Computer)**.  

9. Store the file securely and ensure that you can access it from the System Center Configuration Manager console.  

 The certificate is now ready to be imported when you set up the distribution point.  

> [!TIP]  
>  You can use the same certificate file when you set up media images for an operating system deployment that does not use PXE boot, and the task sequence to install the image must contact a management point that requires HTTPS client connections.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a> Deploy the enrollment certificate for mobile devices  
 This certificate deployment has a single procedure to create and issue the enrollment certificate template on the certification authority.  

### Create and issue the enrollment certificate template on the certification authority  
 This procedure creates an enrollment certificate template for System Center Configuration Manager mobile devices and adds it to the certification authority.  

##### To create and issue the enrollment certificate template on the certification authority  

1.  Create a security group that has users who will enroll mobile devices in System Center Configuration Manager.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that has **Authenticated Session** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Mobile Device Enrollment Certificate**, to generate the enrollment certificates for the mobile devices to be managed by System Center Configuration Manager.  

6.  Choose the **Subject Name** tab, make sure that **Build from this Active Directory information** is selected, select **Common name** for the **Subject name format:**, and then clear **User principal name (UPN)** from **Include this information in alternate subject name**.  

7.  Choose the **Security** tab, choose the security group that has users who have mobile devices to enroll, and then choose the additional permission of **Enroll**. Do not clear **Read**.  

8.  Choose **OK**, and then close **Certificate Templates Console**.  

9. In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

10. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Mobile Device Enrollment Certificate**, and then choose **OK**.  

11. If you do not need to create and issue more certificates, close the Certification Authority console.  

 The mobile device enrollment certificate template is now ready to be selected when you set up a mobile device enrollment profile in the client settings.  

##  <a name="BKMK_AMT2008_cm2012"></a> Deploy the certificates for AMT  
 This certificate deployment has the following procedures:  

-   Create, issue, and install the AMT provisioning certificate  

-   Create and issue the web server certificate for AMT-based computers  

-   Create and issue the client authentication certificates for 802.1X AMT-based computers  

###  <a name="BKMK_AMTprovisioning2008"></a> Create, issue, and install the AMT provisioning certificate  
 Create the provisioning certificate with your internal CA when the AMT-based computers are set up with the certificate thumbprint of your internal root CA. When this is not the case and you must use an external certification authority, use the instructions from the company that issued the AMT provisioning certificate, which will often involve requesting the certificate from the company's public web site. You might also find detailed instructions for your chosen external CA on the [Intel vPro Expert Center: Microsoft vPro Manageability web site](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  External CAs might not support the Intel AMT provisioning object identifier. When this is the case, supply the **Intel(R) Client Setup Certificate** OU attribute.  

 When you request an AMT provisioning certificate from an external CA, install the certificate into the Computer Personal certificate store on the member server that will host the out-of-band service point.  

##### To request and issue the AMT provisioning certificate  

1.  Create a security group that has the computer accounts of site system servers that will run the out-of-band service point.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that has **Web Server** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr AMT Provisioning**, for the AMT provisioning certificate template.  

6.  Choose the **Subject Name** tab, choose **Build from this Active Directory information**, and then choose **Common name**.  

7.  Choose the **Extensions** tab, make sure that **Application Policies** is selected, and then choose **Edit**.  

8.  In the **Edit Application Policies Extension** dialog box, choose **Add**.  

9. In the **Add Application Policy** dialog box, choose **New**.  

10. In the **New Application Policy** dialog box, enter **AMT Provisioning** in the **Name** field, and then enter the following number for the **Object identifier**: **2.16.840.1.113741.1.2.3**.  

11. Choose **OK**, and then choose **OK** in the **Add Application Policy** dialog box.  

12. Choose **OK** in the **Edit Application Policies Extension** dialog box.  

13. In the **Properties of New Template** dialog box, the following is listed as the **Application Policies** description: **Server Authentication** and **AMT Provisioning**.  

14. Choose the **Security** tab, and then remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

15. Choose **Add**, enter the name of a security group that has the computer account for the out-of-band service point site system role, and then choose **OK**.  

16. Choose the **Enroll** permission for this group, and do not clear the **Read** permission..  

17. Choose **OK**, and then close the **Certificate Templates** console.  

18. In **Certification Authority**, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

19. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr AMT Provisioning**, and then choose **OK**.  

    > [!NOTE]  
    >  If you cannot complete steps 18 or 19, check that you are using the Enterprise Edition of Windows Server 2008. Although you can set up templates with Windows Server Standard Edition and Certificate Services, you cannot deploy certificates by using modified certificate templates unless you are using the Enterprise Edition of Windows Server 2008.  

20. Do not close **Certification Authority**.  

 The AMT provisioning certificate from your internal CA is now ready to be installed on the out-of-band service point computer.  

##### To install the AMT provisioning certificate  

1.  Restart the member server that runs IIS to ensure that it can access the certificate template with the configured permission.  

2.  Choose **Start**, choose **Run**, and then enter **mmc.exe.** In the empty console, choose **File**, and then choose **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, choose **Certificates** from the list of **Available snap-ins**, and then choose **Add**.  

4.  In the **Certificate snap-in** dialog box, choose **Computer account**, and then choose **Next**.  

5.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then choose **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, choose **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then choose **Personal**.  

8.  Right-click **Certificates**, choose **All Tasks**, and then choose **Request New Certificate**.  

9. On the **Before You Begin** page, choose **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, choose **Next**.  

11. On the **Request Certificates** page, select **AMT Provisioning** from the list of available certificates, and then choose **Enroll**.  

12. On the **Certificates Installation Results** page, wait until the certificate is installed, and then choose **Finish**.  

13. Close **Certificates (Local Computer)**.  

 The AMT provisioning certificate from your internal CA is now installed and is ready to be selected in the out-of-band service point properties.  

### Create and issue the web server certificate for AMT-based computers  
 Use the following procedure to prepare the web server certificates for AMT-based computers.  

##### To create and issue the web server certificate template  

1.  Create an empty security group that has the AMT computer accounts that System Center Configuration Manager creates during AMT provisioning.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that has **Web Server** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition.**  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr AMT Web Server Certificate**, to generate the web certificates that will be used for out-of-band management on AMT computers.  

6.  Choose the **Subject Name** tab, choose **Build from this Active Directory information**, choose **Common name** for the **Subject name format**, and then clear **User principal name (UPN)** for the alternative subject name.  

7.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

8.  Choose **Add**, and enter the name of the security group that you created for AMT provisioning, and then choose **OK**.  

9. Choose the following **Allow** permissions for this security group: **Read** and **Enroll**.  

10. Choose **OK**, and then close the **Certificate Templates** console.  

11. In the **Certification Authority** console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr AMT Web Server Certificate**, and then choose **OK**.  

13. If you do not have to create and issue more certificates, close **Certification Authority**.  

 The AMT Web server template is now ready to set up AMT-based computers with web server certificates. Choose this certificate template in the out-of-band management component properties.  

### Create and issue the client authentication certificates for 802.1X AMT-based computers  
 Use the following procedure if AMT-based computers will use client certificates for 802.1X authenticated wired or wireless networks.  

##### To create and issue the client authentication certificate template on the CA  

1.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the **Certificate Templates** console.  

2.  In the results pane, right-click the entry that has **Workstation Authentication** in the **Template Display Name** column, and then choose **Duplicate Template**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition.**  

3.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr AMT 802.1X Client Authentication Certificate**, to generate the client certificates that will be used for out-of-band management on AMT computers.  

4.  Choose the **Subject Name** tab, choose **Build from this Active Directory information**, and then choose **Common name** for the **Subject name format**. Clear **DNS name** for the alternative subject name, and then choose **User principal name (UPN)**.  

5.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

6.  Choose **Add**, enter the name of the security group that you will specify in the out-of-band management component properties to contain the computer accounts of the AMT-based computers, and then choose **OK**.  

7.  Select the following **Allow** permissions for this security group: **Read** and **Enroll**.  

8.  Choose **OK**, and then close the **Certificate Templates** management console, **certtmpl - [Certificate Templates]**.  

9. In the **Certification Authority** management console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

10. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr AMT 802.1X Client Authentication Certificate**, and then choose **OK**.  

11. If you do not need to create and issue more certificates, close **Certification Authority**.  

 The client authentication certificate template is now ready to issue certificates to AMT-based computers that can be used for 802.1X client authentication. Choose this certificate template in the out-of-band management component properties.  

##  <a name="BKMK_MacClient_SP1"></a> Deploy the client certificate for Mac computers  

This certificate deployment has a single procedure to create and issue the enrollment certificate template on the certification authority.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a> Create and issue a Mac client certificate template on the certification authority  
 This procedure creates a custom certificate template for System Center Configuration Manager Mac computers and adds the certificate template to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the certificate template that you might have created for Windows client computers or for distribution points.  
>   
>  When you create a new certificate template for this certificate, you can restrict the certificate request to authorized users.  

##### To create and issue the Mac client certificate template on the certification authority  

1.  Create a security group that has user accounts for administrative users who will enroll the certificate on the Mac computer by using System Center Configuration Manager.  

2.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then choose **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that displays **Authenticated Session** in the **Template Display Name** column, and then choose **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then choose **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name, like **ConfigMgr Mac Client Certificate**, to generate the Mac client certificate.  

6.  Choose the **Subject Name** tab, make sure that **Build from this Active Directory information** is selected, choose **Common name** for the **Subject name format:**, and then clear **User principal name (UPN)** from **Include this information in alternate subject name**.  

7.  Choose the **Security** tab, and then remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

8.  Choose **Add**, specify the security group that you created in step one, and then choose **OK**.  

9. Choose the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Choose **OK**, and then close **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, choose **New**, and then choose **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, choose the new template that you just created, **ConfigMgr Mac Client Certificate**, and then choose **OK**.  

13. If you do not have to create and issue more certificates, close **Certification Authority**.  

 The Mac client certificate template is now ready to be selected when you set up client settings for enrollment.
