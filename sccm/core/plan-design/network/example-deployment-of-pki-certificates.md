---
title: "Deployment PKI certificates | System Center Configuration Manager"
ms.custom: na
ms.date: 04/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigmanmanager: angrobe

---
# Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority
This step-by-step example deployment, which uses a Windows Server 2008 certification authority (CA), contains procedures to guide you through the process of creating and deploying the public key infrastructure (PKI) certificates that System Center Configuration Manager uses. These procedures use an enterprise certification authority (CA) and certificate templates. The steps are appropriate for a test network only, as a proof of concept.  

 Because there is no single method of deployment for the required certificates, you must consult your particular PKI deployment documentation for the required procedures and best practices to deploy the required certificates for a production environment. For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  The instructions in this topic can easily be adapted for operating systems other than the ones documented in the Test Network Requirements section. However, if you are running the issuing CA on Windows Server 2012, you are not prompted for the certificate template version. Instead, specify this on the **Compatibility** tab of the template properties, as follows:  
>   
>  -   **Certification Authority**: **Windows Server 2003**  
> -   **Certificate recipient**: **Windows XP / Server 2003**  

## In This Section  
 The following sections include example step-by-step instructions to create and deploy the following certificates that can be used with System Center Configuration Manager:  

 [Test Network Requirements](#BKMK_testnetworkenvironment)  

 [Overview of the Certificates](#BKMK_overview2008)  

 [Deploying the Web Server Certificate for Site Systems that Run IIS](#BKMK_webserver2008_cm2012)  

 [Deploying the Service Certificate for Cloud-Based Distribution Points](#BKMK_clouddp2008_cm2012)  

 [Deploying the Client Certificate for Windows Computers](#BKMK_client2008_cm2012)  

 [Deploying the Client Certificate for Distribution Points](#BKMK_clientdistributionpoint2008_cm2012)  

 [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012)  

 [Deploying the Certificates for AMT](#BKMK_AMT2008_cm2012)  

 [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a> Test Network Requirements  
 The step-by-step instructions have the following requirements:  

-   The test network is running Active Directory Domain Services with Windows Server 2008, and it is installed as a single domain, single forest.  

-   You have a member server running Windows Server 2008 Enterprise Edition, which has installed on it the Active Directory Certificate Services role, and it is configured as an enterprise root certification authority (CA).  

-   You have one computer that has Windows Server 2008 (Standard Edition or Enterprise Edition, R2 or later) installed on it and that is designated as a member server, and Internet Information Services (IIS) is installed on it. This computer will be the System Center Configuration Manager site system server that you will configure with an intranet FQDN (to support client connections on the intranet) and an Internet FQDN if you must support mobile devices that are enrolled by System Center Configuration Manager and clients on the Internet.  

-   You have one Windows Vista client with the latest service pack installed, and this computer is configured with a computer name that comprises ASCII characters and is joined to the domain. This computer will be a System Center Configuration Manager client computer.  

-   You can log in with a root domain administrator account or an enterprise domain administrator account and use this account for all procedures in this example deployment.  

##  <a name="BKMK_overview2008"></a> Overview of the Certificates  
 The following table lists the types of PKI certificates that might be required for System Center Configuration Manager and describes how they are used.  

|Certificate Requirement|Certificate Description|  
|-----------------------------|-----------------------------|  
|Web server certificate for site systems that run IIS|This certificate is used to encrypt data and authenticate the server to clients. It must be installed externally from System Center Configuration Manager on site systems servers that run IIS and that are configured in System Center Configuration Manager to use HTTPS.<br /><br /> For the steps to configure and install this certificate, see [Deploying the Web Server Certificate for Site Systems that Run IIS](#BKMK_webserver2008_cm2012) in this this topic.|  
|Service certificate for clients to connect to cloud-based distribution points|For the steps to configure and install this certificate, see [Deploying the Service Certificate for Cloud-Based Distribution Points](#BKMK_clouddp2008_cm2012) in this  topic.<br /><br /> **Important:** This certificate is used in conjunction with the Windows Azure management certificate. For more information about the management certificate, see [How to Create a Management Certificate](http://go.microsoft.com/fwlink/p/?LinkId=220281) and [How to Add a Management Certificate to a Windows Azure Subscription](http://go.microsoft.com/fwlink/?LinkId=241722) in the Windows Azure Platform section of the MSDN Library.|  
|Client certificate for Windows computers|This certificate is used to authenticate System Center Configuration Manager client computers to site systems that are configured to use HTTPS. It can also be used for management points and state migration points to monitor their operational status when they are configured to use HTTPS. It must be installed externally from System Center Configuration Manager on computers.<br /><br /> For the steps to configure and install this certificate, see [Deploying the Client Certificate for Windows Computers](#BKMK_client2008_cm2012) in this topic.|  
|Client certificate for distribution points|This certificate has two purposes:<br /><br /> The certificate is used to authenticate the distribution point to an HTTPS-enabled management point before the distribution point sends status messages.<br /><br /> When the **Enable PXE support for clients** distribution point option is selected, the certificate is sent to computers that PXE boot so that they can connect to a HTTPS-enabled management point during the deployment of the operating system.<br /><br /> For the steps to configure and install this certificate, see [Deploying the Client Certificate for Distribution Points](#BKMK_clientdistributionpoint2008_cm2012) in this topic.|  
|Enrollment certificate for mobile devices|This certificate is used to authenticate System Center Configuration Manager mobile device clients to site systems that are configured to use HTTPS. It must be installed as part of mobile device enrollment in System Center Configuration Manager and you select the configured certificate template as a mobile device client setting.<br /><br /> For the steps to configure this certificate, see [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) in this topic.|  
|Certificates for Intel AMT|There are three certificates that relate to out of band management for Intel AMT-based computers: An AMT provisioning certificate; an AMT web server certificate; and optionally, a client authentication certificate for 802.1X wired or wireless networks.<br /><br /> The AMT provisioning certificate must be installed externally from System Center Configuration Manager on the out of band service point computer, and then you select the installed certificate in the out of band service point properties. The AMT web server certificate and the client authentication certificate are installed during AMT provisioning and management, and you select the configured certificate templates in the out of band management component properties.<br /><br /> For the steps to configure these certificates, see [Deploying the Certificates for AMT](#BKMK_AMT2008_cm2012) in this topic.|  
|Client certificate for Mac computers|You can request and install this certificate from a Mac computer when you use System Center Configuration Manager enrollment and select the configured certificate template as a mobile device client setting.<br /><br /> For the steps to configure this certificate, see [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) in this topic.|  

##  <a name="BKMK_webserver2008_cm2012"></a> Deploying the Web Server Certificate for Site Systems that Run IIS  
 This certificate deployment has the following procedures:  

-   Creating and Issuing the Web Server Certificate Template on the Certification Authority  

-   Requesting the Web Server Certificate  

-   Configuring IIS to Use the Web Server Certificate  

###  <a name="BKMK_webserver22008"></a> Creating and Issuing the Web Server Certificate Template on the Certification Authority  
 This procedure creates a certificate template for System Center Configuration Manager site systems and adds it to the certification authority.  

##### To create and issue the web server certificate template on the certification authority  

1.  Create a security group named **ConfigMgr IIS Servers** that contains the member servers to install System Center Configuration Manager site systems that will run IIS.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates** and click **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that displays **Web Server** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the web certificates that will be used on Configuration Manager site systems, such as **ConfigMgr Web Server Certificate**.  

6.  Click the **Subject Name** tab, and make sure that **Supply in the request** is selected.  

7.  Click the **Security** tab, and remove the **Enroll** permission from the security groups **Domain Admins** and **Enterprise Admins**.  

8.  Click **Add**, enter **ConfigMgr IIS Servers** in the text box, and then click **OK**.  

9. Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Click **OK**, and close the **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Web Server Certificate**, and then click **OK**.  

13. If you do not need to create and issue any more certificate, close **Certification Authority**.  

###  <a name="BKMK_webserver32008"></a> Requesting the Web Server Certificate  
 This procedure allows you to specify the intranet and Internet FQDN values that will be configured in the site system server properties, and then installs the web server certificate on to the member server that runs IIS.  

##### To request the web server certificate  

1.  Restart the member server that runs IIS, to ensure that the computer can access the certificate template that you created, by using the **Read** and **Enroll** permissions that you configured.  

2.  Click **Start**, click **Run**, and type **mmc.exe.** In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

4.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

5.  In the **Select Computer** dialog box, ensure **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then click **Personal**.  

8.  Right-click **Certificates**, click **All Tasks**, and then click **Request New Certificate**.  

9. On the **Before You Begin** page, click **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, click **Next**.  

11. On the **Request Certificates** page, identify the **ConfigMgr Web Server Certificate** from the list of displayed certificates, and then click **More information is required to enroll for this certificate. Click here to configure settings**.  

12. In the **Certificate Properties** dialog box, in the **Subject** tab, do not make any changes to the **Subject name**. This means that the **Value** box for the **Subject name** section remains blank. Instead, from the **Alternative name** section, click the **Type** drop-down list, and then select **DNS**.  

13. In the **Value** box, specify the FQDN values that you will specify in the System Center Configuration Manager site system properties, and then click **OK** to close the **Certificate Properties** dialog box.  

     Examples:  

    -   If the site system will only accept client connections from the intranet, and the intranet FQDN of the site system server is **server1.internal.contoso.com**: Type **server1.internal.contoso.com**, and then click **Add**.  

    -   If the site system will accept client connections from the intranet and the Internet, and the intranet FQDN of the site system server is **server1.internal.contoso.com** and the Internet FQDN of the site system server is **server.contoso.com**:  

        1.  Type **server1.internal.contoso.com**, and then click **Add**.  

        2.  Type **server.contoso.com**, and then click **Add**.  

        > [!NOTE]  
        >  It does not matter in which order you specify the FQDNs for System Center Configuration Manager. However, check that all devices that will use the certificate, such as mobile devices and proxy web servers, can use a certificate SAN and multiple values in the SAN. If devices have limited support for SAN values in certificates, you might have to change the order of the FQDNs or use the Subject value instead.  

14. On the **Request Certificates** page, select **ConfigMgr Web Server Certificate** from the list of displayed certificates, and then click **Enroll**.  

15. On the **Certificates Installation Results** page, wait until the certificate is installed, and then click **Finish**.  

16. Close **Certificates (Local Computer)**.  

###  <a name="BKMK_webserver42008"></a> Configuring IIS to Use the Web Server Certificate  
 This procedure binds the installed certificate to the IIS **Default Web Site**.  

##### To configure IIS to use the web server certificate  

1.  On the member server that has IIS installed, click **Start**, click **Programs**, click **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.  

2.  Expand **Sites**, right-click **Default Web Site**, and then select **Edit Bindings**.  

3.  Click the **https** entry, and then click **Edit**.  

4.  In the **Edit Site Binding** dialog box, select the certificate that you requested by using the ConfigMgr Web Server Certificates template, and then click **OK**.  

    > [!NOTE]  
    >  If you are not sure which is the correct certificate, select one, and then click **View**. This allows you to compare the selected certificate details with the certificates that are displayed with the Certificates snap-in. For example, the Certificates snap-in displays the certificate template that was used to request the certificate. You can then compare the certificate thumbprint of the certificate that was requested with the ConfigMgr Web Server Certificates template with the certificate thumbprint of the certificate currently selected in the **Edit Site Binding** dialog box.  

5.  Click **OK** in the **Edit Site Binding** dialog box, and then click **Close**.  

6.  Close **Internet Information Services (IIS) Manager**.  

 The member server is now provisioned with a System Center Configuration Manager web server certificate.  

> [!IMPORTANT]  
>  When you install the System Center Configuration Manager site system server on this computer, make sure that you specify the same FQDNs in the site system properties as you specified when you requested the certificate.  

##  <a name="BKMK_clouddp2008_cm2012"></a> Deploying the Service Certificate for Cloud-Based Distribution Points  

> [!NOTE]  
>  The service certificate for cloud-based distribution points applies to System Center Configuration Manager SP1 and later.  

 This certificate deployment has the following procedures:  

-   [Creating and Issuing a Custom Web Server Certificate Template on the Certification Authority](#BKMK_clouddpcreating2008)  

-   [Requesting the Custom Web Server Certificate](#BKMK_clouddprequesting2008)  

-   [Exporting the Custom Web Server Certificate for Cloud-Based Distribution Points](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a> Creating and Issuing a Custom Web Server Certificate Template on the Certification Authority  
 This procedure creates a custom certificate template that is based on the Web Server certificate template. The certificate is for System Center Configuration Manager cloud-based distribution points and the private key must be exportable. After the certificate template is created, it is added to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the web server certificate template that you created for site systems that run IIS, because although both certificates require server authentication capability, the certificate for cloud-based distribution points requires you to enter a custom-defined value for the Subject Name and the private key must be exported. As a security best practice, do not configure certificate templates to allow the private key to be exported unless this configuration is required. The cloud-based distribution point requires this configuration because you must import the certificate as a file, rather than select it from the certificate store.  
>   
>  By creating a new certificate template for this certificate, you can restrict which computers request a certificate that allows the private key to be exported. On a production network, you might also consider adding the following modifications for this certificate:  
>   
>  -   Require approval to install the certificate, for additional security.  
> -   Increase the certificate validity period. Because you must export and import the certificate each time before it expires, increasing the validity period reduces how often you must repeat this procedure. However, when you increase the validity period, it decreases the security of the certificate because it provides more time for an attacker to decrypt the private key and steal the certificate.  
> -   Use a custom value in the certificate Subject Alternative Name (SAN) to help identify this certificate from standard web server certificates that you use with IIS.  

##### To create and issue the custom Web Server certificate template on the certification authority  

1.  Create a security group named **ConfigMgr Site Servers** that contains the member servers to install System Center Configuration Manager primary site servers that will manage cloud-based distribution points.  

2.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that displays **Web Server** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the web server certificate for cloud-based distribution points, such as **ConfigMgr Cloud-Based Distribution Point Certificate**.  

6.  Click the **Request Handling** tab, and select **Allow private key to be exported**.  

7.  Click the **Security** tab, and remove the **Enroll** permission from the **Enterprise Admins** security group.  

8.  Click **Add**, enter **ConfigMgr Site Servers** in the text box, and then click **OK**.  

9. Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Click **OK** and close **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Cloud-Based Distribution Point Certificate**, and then click **OK**.  

13. If you do not have to create and issue any more certificates, close **Certification Authority**.  

###  <a name="BKMK_clouddprequesting2008"></a> Requesting the Custom Web Server Certificate  
 This procedure requests and then installs the custom web server certificate on to the member server that will run the site server.  

##### To request the custom web server certificate  

1.  Restarted the member server after you created and configured the **ConfigMgr Site Servers** security group to ensure that the computer can access the certificate template that you created, by using the **Read** and **Enroll** permissions that you configured.  

2.  Click **Start**, click **Run**, and type **mmc.exe.** In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

4.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

5.  In the **Select Computer** dialog box, ensure **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then click **Personal**.  

8.  Right-click **Certificates**, click **All Tasks**, and then click **Request New Certificate**.  

9. On the **Before You Begin** page, click **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, click **Next**.  

11. On the **Request Certificates** page, identify the **ConfigMgr Cloud-Based Distribution Point Certificate** from the list of displayed certificates, and then click **More information is required to enroll for this certificate. Click here to configure settings**.  

12. In the **Certificate Properties** dialog box, in the **Subject** tab, for the **Subject name**, select **Common name** as the **Type**.  

13. In the **Value** box, specify your choice of service name and your domain name by using an FQDN format. For example: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  It does not matter what service name you specify, as long as it is unique in your namespace. You will use DNS to create an alias (CNAME record) to map this service name to an automatically generated identifier (GUID) and an IP address from Windows Azure.  

14. Click **Add**, and click **OK** to close the **Certificate Properties** dialog box.  

15. On the **Request Certificates** page, select **ConfigMgr Cloud-Based Distribution Point Certificate** from the list of displayed certificates, and then click **Enroll**.  

16. On the **Certificates Installation Results** page, wait until the certificate is installed, and then click **Finish**.  

17. Close **Certificates (Local Computer)**.  

###  <a name="BKMK_clouddpexporting2008"></a> Exporting the Custom Web Server Certificate for Cloud-Based Distribution Points  
 This procedure exports the custom web server certificate to a file, so that it can be imported when you create the cloud-based distribution point.  

##### To export the custom web server certificate for cloud-based distribution points  

1.  In the **Certificates (Local Computer)** console, right-click the certificate that you have just installed, select **All Tasks**, and then click **Export**.  

2.  In the Certificates Export Wizard, click **Next**.  

3.  On the **Export Private Key** page, select **Yes, export the private key**, and then click **Next**.  

    > [!NOTE]  
    >  If this option is not available, the certificate has been created without the option to export the private key. In this scenario, you cannot export the certificate in the required format. You must reconfigure the certificate template to allow the private key to be exported, and then request the certificate again.  

4.  On the **Export File Format** page, ensure that the option **Personal Information Exchange - PKCS #12 (.PFX)** is selected.  

5.  On the **Password** page, specify a strong password to protect the exported certificate with its private key, and then click **Next**.  

6.  On the **File to Export** page, specify the name of the file that you want to export, and then click **Next**.  

7.  To close the wizard, click **Finish** in the **Certificate Export Wizard** page, and click **OK** in the confirmation dialog box.  

8.  Close **Certificates (Local Computer)**.  

9. Store the file securely and ensure that you can access it from the System Center Configuration Manager console.  

 The certificate is now ready to be imported when you create a cloud-based distribution point.  

##  <a name="BKMK_client2008_cm2012"></a> Deploying the Client Certificate for Windows Computers  
 This certificate deployment has the following procedures:  

-   Creating and Issuing the Workstation Authentication Certificate Template on the Certification Authority  

-   Configuring Autoenrollment of the Workstation Authentication Template by Using Group Policy  

-   Automatically Enrolling the Workstation Authentication Certificate and Verifying Its Installation on Computers  

###  <a name="BKMK_client02008"></a> Creating and Issuing the Workstation Authentication Certificate Template on the Certification Authority  
 This procedure creates a certificate template for System Center Configuration Manager client computers and adds it to the certification authority.  

##### To create and issue the Workstation Authentication certificate template on the certification authority  

1.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the Certificate Templates management console.  

2.  In the results pane, right-click the entry that displays **Workstation Authentication** in the column **Template Display Name**, and then click **Duplicate Template**.  

3.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

4.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the client certificates that will be used on Configuration Manager client computers, such as **ConfigMgr Client Certificate**.  

5.  Click the **Security** tab, select the **Domain Computers** group, and select the additional permissions of **Read** and **Autoenroll**. Do not clear **Enroll**.  

6.  Click **OK** and close **Certificate Templates Console**.  

7.  In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

8.  In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Client Certificate**, and then click **OK**.  

9. If you do not need to create and issue any more certificate, close **Certification Authority**.  

###  <a name="BKMK_client12008"></a> Configuring Autoenrollment of the Workstation Authentication Template by Using Group Policy  
 This procedure configures Group Policy to autoenroll the client certificate on computers.  

##### To configure autoenrollment of the workstation authentication template by using Group Policy  

1.  On the domain controller, click **Start**, click **Administrative Tools**, and then click **Group Policy Management**.  

2.  Navigate to your domain, right-click the domain, and then select **Create a GPO in this domain, and Link it here**.  

    > [!NOTE]  
    >  This step uses the best practice of creating a new Group Policy for custom settings rather than editing the Default Domain Policy that is installed with Active Directory Domain Services. By assigning this Group Policy at the domain level, you will apply it to all computers in the domain. However, on a production environment, you can restrict the autoenrollment so that it enrolls on only selected computers by assigning the Group Policy at an organizational unit level, or you can filter the domain Group Policy with a security group so that it applies only to the computers in the group. If you restrict autoenrollment, remember to include the server that is configured as the management point.  

3.  In the **New GPO** dialog box, enter a name for the new Group Policy, such as **Autoenroll Certificates**, and click **OK**.  

4.  In the results pane, on the **Linked Group Policy Objects** tab, right-click the new Group Policy, and then click **Edit**.  

5.  In the **Group Policy Management Editor**, expand **Policies** under **Computer Configuration**, and then navigate to **Windows Settings** / **Security Settings** / **Public Key Policies**.  

6.  Right-click the object type named **Certificate Services Client - Auto-enrollment**, and then click **Properties**.  

7.  From the **Configuration Model** drop-down list, select **Enabled**, select **Renew expired certificates, update pending certificates, and remove revoked certificates**, select **Update certificates that use certificate templates**, and then click **OK**.  

8.  Close **Group Policy Management**.  

###  <a name="BKMK_client22008"></a> Automatically Enrolling the Workstation Authentication Certificate and Verifying Its Installation on Computers  
 This procedure installs the client certificate on computers and verifies the installation.  

##### To automatically enroll the workstation authentication certificate and verify its installation on the client computer  

1.  Restart the workstation computer, and wait a few minutes before logging on.  

    > [!NOTE]  
    >  Restarting a computer is the most reliable method of ensuring success with certificate autoenrollment.  

2.  Log on with an account that has administrative privileges.  

3.  In the search box, type **mmc.exe.**, and then press **Enter**.  

4.  In the empty management console, click **File**, and then click **Add/Remove Snap-in**.  

5.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

6.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

7.  In the **Select Computer** dialog box, ensure that **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

8.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

9. In the console, expand **Certificates (Local Computer)**, expand **Personal**, and then click **Certificates**.  

10. In the results pane, confirm that a certificate is displayed that has **Client Authentication** displayed in the **Intended Purpose** column, and that **ConfigMgr Client Certificate** is displayed in the **Certificate Template** column.  

11. Close **Certificates (Local Computer)**.  

12. Repeat steps 1 through 11 for the member server to verify that the server that will be configured as the management point also has a client certificate.  

 The computer is now provisioned with a System Center Configuration Manager client certificate.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a> Deploying the Client Certificate for Distribution Points  

> [!NOTE]  
>  This certificate can also be used for media images that do not use PXE boot, because the certificate requirements are the same.  

 This certificate deployment has the following procedures:  

-   Creating and Issuing a Custom Workstation Authentication Certificate Template on the Certification Authority  

-   Requesting the Custom Workstation Authentication Certificate  

-   Exporting the Client Certificate for Distribution Points  

###  <a name="BKMK_clientdistributionpoint02008"></a> Creating and Issuing a Custom Workstation Authentication Certificate Template on the Certification Authority  
 This procedure creates a custom certificate template for System Center Configuration Manager distribution points that allows the private key to be exported, and adds the certificate template to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the certificate template that you created for client computers, because although both certificates require client authentication capability, the certificate for distribution points requires that the private key is exported. As a security best practice, do not configure certificate templates to allow the private key to be exported unless this configuration is required. The distribution point requires this configuration because you must import the certificate as a file, rather than select it from the certificate store.  
>   
>  By creating a new certificate template for this certificate, you can restrict which computers request a certificate that allows the private key to be exported. In our example deployment, this will be the security group that you previously created for System Center Configuration Manager site system servers that run IIS. On a production network that distributes the IIS site system roles, consider creating a new security group for the servers that run distribution points so that you can restrict the certificate to just these site system servers. You might also consider adding the following modifications for this certificate:  
>   
>  -   Require approval to install the certificate, for additional security.  
> -   Increase the certificate validity period. Because you must export and import the certificate each time before it expires, increasing the validity period reduces how often you must repeat this procedure. However, when you increase the validity period, it decreases the security of the certificate because it provides more time for an attacker to decrypt the private key and steal the certificate.  
> -   Use a custom value in the certificate Subject field or Subject Alternative Name (SAN) to help identify this certificate from standard client certificates. This can be particularly helpful if you will use the same certificate for multiple distribution points.  

##### To create and issue the custom Workstation Authentication certificate template on the certification authority  

1.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the Certificate Templates management console.  

2.  In the results pane, right-click the entry that displays **Workstation Authentication** in the column **Template Display Name**, and then click **Duplicate Template**.  

3.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

4.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the client authentication certificate for distribution points, such as **ConfigMgr Client Distribution Point Certificate**.  

5.  Click the **Request Handling** tab, and select **Allow private key to be exported**.  

6.  Click the **Security** tab, and remove the **Enroll** permission from the **Enterprise Admins** security group.  

7.  Click **Add**, enter **ConfigMgr IIS Servers** in the text box, and then click **OK**.  

8.  Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

9. Click **OK** and close **Certificate Templates Console**.  

10. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

11. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Client Distribution Point Certificate**, and then click **OK**.  

12. If you do not have to create and issue any more certificates, close **Certification Authority**.  

###  <a name="BKMK_clientdistributionpoint12008"></a> Requesting the Custom Workstation Authentication Certificate  
 This procedure requests and then installs the custom client certificate on to the member server that runs IIS and that will be configured as a distribution point.  

##### To request the custom Workstation Authentication certificate  

1.  Click **Start**, click **Run**, and type **mmc.exe.** In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

2.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

3.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

4.  In the **Select Computer** dialog box, ensure **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

5.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

6.  In the console, expand **Certificates (Local Computer)**, and then click **Personal**.  

7.  Right-click **Certificates**, click **All Tasks**, and then click **Request New Certificate**.  

8.  On the **Before You Begin** page, click **Next**.  

9. If you see the **Select Certificate Enrollment Policy** page, click **Next**.  

10. On the **Request Certificates** page, select the **ConfigMgr Client Distribution Point Certificate** from the list of displayed certificates, and then click **Enroll**.  

11. On the **Certificates Installation Results** page, wait until the certificate is installed, and then click **Finish**.  

12. In the results pane, confirm that a certificate is displayed that has **Client Authentication** displayed in the **Intended Purpose** column, and that **ConfigMgr Client Distribution Point Certificate** is displayed in the **Certificate Template** column.  

13. Do not close **Certificates (Local Computer)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a> Exporting the Client Certificate for Distribution Points  
 This procedure exports the custom Workstation Authentication certificate to a file, so that it can be imported in the distribution point properties.  

##### To export the client certificate for distribution points  

1.  In the **Certificates (Local Computer)** console, right-click the certificate that you have just installed, select **All Tasks**, and then click **Export**.  

2.  In the Certificates Export Wizard, click **Next**.  

3.  On the **Export Private Key** page, select **Yes, export the private key**, and then click **Next**.  

    > [!NOTE]  
    >  If this option is not available, the certificate has been created without the option to export the private key. In this scenario, you cannot export the certificate in the required format. You must reconfigure the certificate template to allow the private key to be exported, and then request the certificate again.  

4.  On the **Export File Format** page, ensure that the option **Personal Information Exchange - PKCS #12 (.PFX)** is selected.  

5.  On the **Password** page, specify a strong password to protect the exported certificate with its private key, and then click **Next**.  

6.  On the **File to Export** page, specify the name of the file that you want to export, and then click **Next**.  

7.  To close the wizard, click **Finish** in the **Certificate Export Wizard** page, and click **OK** in the confirmation dialog box.  

8.  Close **Certificates (Local Computer)**.  

9. Store the file securely and ensure that you can access it from the System Center Configuration Manager console.  

 The certificate is now ready to be imported when you configure the distribution point.  

> [!TIP]  
>  You can use the same certificate file when you configure media images for an operating system deployment that does not use PXE boot, and the task sequence to install the image must contact a management point that requires HTTPS client connections.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a> Deploying the Enrollment Certificate for Mobile Devices  
 This certificate deployment has a single procedure to create and issue the enrollment certificate template on the certification authority.  

### Creating and Issuing the Enrollment Certificate Template on the Certification Authority  
 This procedure creates an enrollment certificate template for System Center Configuration Manager mobile devices and adds it to the certification authority.  

##### To create and issue the enrollment certificate template on the certification authority  

1.  Create a security group that contains users who will enroll mobile devices in System Center Configuration Manager.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that displays **Authenticated Session** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the enrollment certificates for the mobile devices to be managed by System Center Configuration Manager, such as **ConfigMgr Mobile Device Enrollment Certificate**.  

6.  Click the **Subject Name** tab, make sure that **Build from this Active Directory information** is selected, select **Common name** for the **Subject name format:** and clear **User principal name (UPN)** from **Include this information in alternate subject name**.  

7.  Click the **Security** tab, select the security group that contains users who have mobile devices to enroll, and select the additional permission of **Enroll**. Do not clear **Read**.  

8.  Click **OK** and close **Certificate Templates Console**.  

9. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

10. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Mobile Device Enrollment Certificate**, and then click **OK**.  

11. If you do not need to create and issue any more certificate, close the Certification Authority console.  

 The mobile device enrollment certificate template is now ready to be selected when you configure a mobile device enrollment profile in the client settings.  

##  <a name="BKMK_AMT2008_cm2012"></a> Deploying the Certificates for AMT  
 This certificate deployment has the following procedures:  

-   Creating, Issuing, and Installing the AMT provisioning certificate  

-   Creating and Issuing the Web Server Certificate for AMT-Based Computers  

-   Creating and Issuing the Client Authentication Certificates for 802.1X AMT-Based Computers  

###  <a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Create the provisioning certificate with your internal CA when the AMT-based computers are configured with the certificate thumbprint of your internal root CA. When this is not the case and you must use an external certification authority, use the instructions from the company issuing the AMT provisioning certificate, which will often involve requesting the certificate from the company's public Web site. You might also find detailed instructions for your chosen external CA on the Intel vPro Expert Center: Microsoft vPro Manageability Web site ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001)).  

> [!IMPORTANT]  
>  External CAs might not support the Intel AMT provisioning object identifier. When this is the case, use the alternative method of supplying the OU attribute of **Intel(R) Client Setup Certificate**.  

 When you request an AMT provisioning certificate from an external CA, install the certificate into the Computer Personal certificate store on the member server that will host the out of band service point.  

##### To request and issue the AMT provisioning certificate  

1.  Create a security group that contains the computer accounts of site system servers that will run the out of band service point.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that displays **Web Server** in the **Template Display Name** column, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name for the AMT provisioning certificate template, such as **ConfigMgr AMT Provisioning**.  

6.  Click the **Subject Name** tab, select **Build from this Active Directory information**, and then select **Common name**.  

7.  Click the **Extensions** tab, make sure **Application Policies** is selected, and then click **Edit**.  

8.  In the **Edit Application Policies Extension** dialog box, click **Add**.  

9. In the **Add Application Policy** dialog box, click **New**.  

10. In the **New Application Policy** dialog box, type **AMT Provisioning** in the **Name** field, and then type the following number for the **Object identifier**: **2.16.840.1.113741.1.2.3**.  

11. Click **OK**, and then click **OK** in the **Add Application Policy** dialog box.  

12. Click **OK** in the **Edit Application Policies Extension** dialog box.  

13. In the **Properties of New Template** dialog box, you should now see the following listed as the **Application Policies** description: **Server Authentication** and **AMT Provisioning**.  

14. Click the **Security** tab, and remove the **Enroll** permission from the security groups **Domain Admins** and **Enterprise Admins**.  

15. Click **Add**, enter the name of a security group that contains the computer account for the out of band service point site system role, and then click **OK**.  

16. Select the **Enroll** permission for this group, and do not clear the **Read** permission..  

17. Click **OK**, and close the **Certificate Templates** console.  

18. In **Certification Authority**, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

19. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr AMT Provisioning**, and then click **OK**.  

    > [!NOTE]  
    >  If you cannot complete steps 18 or 19, check that you are using the Enterprise Edition of Windows Server 2008. Although you can configure templates with Windows Server Standard Edition and Certificate Services, you cannot deploy certificates using modified certificate templates unless you are using the Enterprise Edition of Windows Server 2008.  

20. Do not close **Certification Authority**.  

 The AMT provisioning certificate from your internal CA is now ready to be installed on the band service point computer.  

##### To install the AMT provisioning certificate  

1.  Restart the member server that runs IIS, to ensure it can access the certificate template with the configured permission.  

2.  Click **Start**, click **Run**, and type **mmc.exe.** In the empty console, click **File**, and then click **Add/Remove Snap-in**.  

3.  In the **Add or Remove Snap-ins** dialog box, select **Certificates** from the list of **Available snap-ins**, and then click **Add**.  

4.  In the **Certificate snap-in** dialog box, select **Computer account**, and then click **Next**.  

5.  In the **Select Computer** dialog box, ensure **Local computer: (the computer this console is running on)** is selected, and then click **Finish**.  

6.  In the **Add or Remove Snap-ins** dialog box, click **OK**.  

7.  In the console, expand **Certificates (Local Computer)**, and then click **Personal**.  

8.  Right-click **Certificates**, click **All Tasks**, and then click **Request New Certificate**.  

9. On the **Before You Begin** page, click **Next**.  

10. If you see the **Select Certificate Enrollment Policy** page, click **Next**.  

11. On the **Request Certificates** page, select **AMT Provisioning** from the list of displayed certificates, and then click **Enroll**.  

12. On the **Certificates Installation Results** page, wait until the certificate is installed, and then click **Finish**.  

13. Close **Certificates (Local Computer)**.  

 The AMT provisioning certificate from your internal CA is now installed and is ready to be selected in the out of band service point properties.  

### Creating and Issuing the Web Server Certificate for AMT-Based Computers  
 Use the following procedure to prepare the web server certificates for AMT-based computers.  

##### To create and issue the Web server certificate template  

1.  Create an empty security group to contain the AMT computer accounts that System Center Configuration Manager creates during AMT provisioning.  

2.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the **Certificate Templates** console.  

3.  In the results pane, right-click the entry that displays **Web Server** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition.**  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the web certificates that will be used for out of band management on AMT computers, such as **ConfigMgr AMT Web Server Certificate**.  

6.  Click the **Subject Name** tab, click **Build from this Active Directory information**, select **Common name** for the **Subject name format**, and then clear **User principal name (UPN)** for the alternative subject name.  

7.  Click the **Security** tab, and remove the **Enroll** permission from the security groups **Domain Admins** and **Enterprise Admins**.  

8.  Click **Add** and enter the name of the security group that you created for AMT provisioning. Then click **OK**.  

9. Select the following **Allow** permissions for this security group: **Read** and **Enroll**.  

10. Click **OK**, and close the **Certificate Templates** console.  

11. In the **Certification Authority** console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr AMT Web Server Certificate**, and then click **OK**.  

13. If you do not have to create and issue any more certificates, close **Certification Authority**.  

 The AMT Web server template is now ready to provision AMT-based computers with web server certificates. Select this certificate template in the out of band management component properties.  

### Creating and Issuing the Client Authentication Certificates for 802.1X AMT-Based Computers  
 Use the following procedure if AMT-based computers will use client certificates for 802.1X authenticated wired or wireless networks.  

##### To create and issue the client authentication certificate template on the CA  

1.  On the member server that has Certificate Services installed, in the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the **Certificate Templates** console.  

2.  In the results pane, right-click the entry that displays **Workstation Authentication** in the column **Template Display Name**, and then click **Duplicate Template**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition.**  

3.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the client certificates that will be used for out of band management on AMT computers, such as **ConfigMgr AMT 802.1X Client Authentication Certificate**.  

4.  Click the **Subject Name** tab, click **Build from this Active Directory information** and select **Common name** for the **Subject name format**. Clear **DNS name** for the alternative subject name, and then select **User principal name (UPN)**.  

5.  Click the **Security** tab, and remove the **Enroll** permission from the security groups **Domain Admins** and **Enterprise Admins**.  

6.  Click **Add** and enter the name of the security group that you will specify in the out of band management component properties, to contain the computer accounts of the AMT-based computers. Then click **OK**.  

7.  Select the following **Allow** permissions for this security group: **Read** and **Enroll**.  

8.  Click **OK**, and close the **Certificate Templates** management console, **certtmpl - [Certificate Templates]**.  

9. In the **Certification Authority** management console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

10. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr AMT 802.1X Client Authentication Certificate**, and then click **OK**.  

11. If you do not need to create and issue any more certificate, close **Certification Authority**.  

 The client authentication certificate template is now ready to issue certificates to AMT-based computers that can be used for 802.1X client authentication. Select this certificate template in the out of band management component properties.  

##  <a name="BKMK_MacClient_SP1"></a> Deploying the Client Certificate for Mac Computers  

> [!NOTE]  
>  The client certificate for Mac computers applies to System Center Configuration Manager SP1 and later.  

 This certificate deployment has a single procedure to create and issue the enrollment certificate template on the certification authority.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a> Creating and Issuing a Mac Client Certificate Template on the Certification Authority  
 This procedure creates a custom certificate template for System Center Configuration Manager Mac computers and adds the certificate template to the certification authority.  

> [!NOTE]  
>  This procedure uses a different certificate template from the certificate template that you might have created for Windows client computers or for distribution points.  
>   
>  By creating a new certificate template for this certificate, you can restrict the certificate request to authorized users.  

##### To create and issue the Mac client certificate template on the certification authority  

1.  Create a security group that contains user accounts for administrative users who will enroll the certificate on the Mac computer by using System Center Configuration Manager.  

2.  On the member server that is running the Certification Authority console, right-click **Certificate Templates**, and then click **Manage** to load the Certificate Templates management console.  

3.  In the results pane, right-click the entry that displays **Authenticated Session** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**.  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the Mac client certificate, such as **ConfigMgr Mac Client Certificate**.  

6.  Click the **Subject Name** tab, make sure that **Build from this Active Directory information** is selected, select **Common name** for the **Subject name format:** and clear **User principal name (UPN)** from **Include this information in alternate subject name**.  

7.  Click the **Security** tab, and remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.  

8.  Click **Add**, specify the security group that you created in step one, and then click **OK**.  

9. Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Click **OK** and close **Certificate Templates Console**.  

11. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr Mac Client Certificate**, and then click **OK**.  

13. If you do not have to create and issue any more certificates, close **Certification Authority**.  

 The Mac client certificate template is now ready to be selected when you configure client settings for enrollment.
