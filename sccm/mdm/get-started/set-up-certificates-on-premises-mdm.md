---
title: "Set up certificates "
titleSuffix: "Configuration Manager"
description: "Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager On\-premises Mobile Device Management requires the enrollment point, enrollment proxy point, distribution point, and device management point  site system roles to be set up for trusted communications with managed devices. Any site system server hosting one or more of those roles must have a unique PKI certificate bound to the web server on that system. A certificate with the same  root as the certificate on the servers most also be stored on managed devices to establish trusted communication with them.  

 For domain-joined devices, Active Directory Certificate Services installs the needed certificate with the trusted root on all devices automatically. For non-domain-joined devices, you must obtain a valid certificate with a trusted root by some other means. If you use the site CA as your trusted root (which is the same one Active Directory uses for domain-joined devices), the site system servers for the enrollment point and enrollment proxy point must have a certificate issued by that CA bound to them.  

 Each device to be managed will also need to have a certificate with the same root installed on them to support trusted communications with the site system roles. For bulk-enrolled devices, you can include the certificate in the enrollment package that is added to the device for enrolling it when the device is started for the first time by a user. For user-enrolled devices, you need to add the certificate through email, web download, or some other method.  

 As an alternative for non-domain joined devices, you can use the root of a well-known public CA (like Verisign or GoDaddy) to issue the server certificate, which avoids having to manually install a certificate on the device, because most devices natively trust connections to servers using the same root of the public CA. This is a useful alternative for user-enrolled devices in which it is not feasible to install the certificates trusted through the site CA on each device.  

> [!IMPORTANT]  
>  There are many ways to set up the certificates for trusted communications between devices and the site system servers for On\-premises Mobile Device Management. The information provided in this article is given as an example of one way to do it. This method requires you to be running a server in your site with Active Directory Certificate Services role and the Certification Authority and Certification Authority Web Enrollment role services installed. See [Active Directory Certificate Services](http://go.microsoft.com/fwlink/p/?LinkId=115018) for more information and guidance on this Windows Server role.  

 To set up the Configuration Manager site for the SSL communications required for On\-premises Mobile Device Management, follow these high-level steps:  

-   [Configure the certification authority (CA) for CRL publishing](#bkmk_configCa)  

-   [Create the web server certificate template on the CA](#bkmk_certTempl)  

-   [Request the web server certificate for each site system role](#bkmk_requestCert)  

-   [Bind the certificate to the web server](#bkmk_bindCert)  

-   [Export the certificate with the same root as the web server certificate](#bkmk_exportCert)  

##  <a name="bkmk_configCa"></a> Configure the certification authority (CA) for CRL publishing  
 By default, the certification authority (CA) uses LDAP-based certificate revocation lists (CRLs) that allows connections for domain-joined devices. You must add HTTP-based CRLs to the CA to make it possible for non-domain-joined devices to be trusted with certificates issues from the CA. These certificates are required for SSL communications between the servers hosting the Configuration Manager site system roles and the devices enrolled for On\-premises Mobile Device Management.  

 Follow the steps below to configure the CA to autopublish CRL information for issuing certificates that allow trusted connections for domain-joined and non-domain-joined devices:  

1.  On the server running the certification authority for your site, click **Start** > **Administrative Tools** > **Certification Authority**.  

2.  In the Certification Authority console, right-click **CertificateAuthority**, and then click **Properties**.  

3.  In CertificateAuthority properties, click the **Extensions** tab, make sure that **Select extension** is set to **CRL Distribution Point (CDP)**  

4.  Select **http://<ServerDNSName\>/CertEnroll/<CAName\><CRLNameSuffix\><DeltaCRLAllowed\>.crl**. And the three options below:  

    -   **Include in CRLs. Clients use this to find Delta CRL locations.**  

    -   **Include in CDP extension of issued certificates.**  

    -   **Include in the IDP extension of issued CRLs**  

5.  Click the **Exit Module** tab, click **Properties...**, then select **Allow certificates to be published to the file system**.  

6.  Click **OK** when notified that Active Directory Certificate Services must restarted.  

7.  Right-click **Revoked Certificates**, click **All Tasks**, and then click **Publish**.  

8.  In Publish CRL dialog, select **Delta CRL only**, and then click **OK**.  

##  <a name="bkmk_certTempl"></a> Create the web server certificate template on the CA  
 After publishing the new CRL on the CA, the next step is to create a web server certificate template. This template is required for issuing certificates for the servers hosting the enrollment point, enrollment proxy point, distribution point, and  device management point site system roles. These servers will be SSL endpoints for trusted communications between the site system roles and  enrolled devices.    Follow the steps below to create the certificate template:  

1.  Create a security group named **ConfigMgr MDM Servers** that contains the servers running the site systems that require trusted communications with enrolled devices.  

2.  In the Certification Authority console, right-click **Certificate Templates** and click **Manage** to load the Certificate Templates console.  

3.  In the results pane, right-click the entry that displays **Web Server** in the column **Template Display Name**, and then click **Duplicate Template**.  

4.  In the **Duplicate Template** dialog box, ensure that **Windows 2003 Server, Enterprise Edition** is selected, and then click **OK**.  

    > [!IMPORTANT]  
    >  Do not select **Windows 2008 Server, Enterprise Edition**. Configuration Manager does not support Windows Server 2008 certificate templates for trusted communications using HTTPS.  

    > [!NOTE]  
    >  If the CA you are using is on Windows Server 2012, you are not prompted for the certificate template version when you click **Duplicate Template**. Instead, specify this on the **Compatibility** tab of the template properties, as follows:  
    >   
    >  **Certification Authority**: **Windows Server 2003**  
    >   
    >  **Certificate recipient**: **Windows XP / Server 2003**  

5.  In the **Properties of New Template** dialog box, on the **General** tab, enter a template name to generate the web certificates that will be used on Configuration Manager site systems, such as **ConfigMgr MDM Web Server**.  

6.  Click the **Subject Name** tab, select **Build from Active Directory information**, and for subject name format, specify **DNS name**. Clear the check box from alternate subject name, if **User Principal Name (UPN)** is selected.  

7.  Click the **Security** tab, and remove the **Enroll** permission from the security groups **Domain Admins** and **Enterprise Admins**.  

8.  Click **Add**, enter **ConfigMgr MDM Servers** in the text box, and then click **OK**.  

9. Select the **Enroll** permission for this group, and do not clear the **Read** permission.  

10. Click **OK**, and close the Certificate Templates  console.  

11. In the Certification Authority console, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.  

12. In the **Enable Certificate Templates** dialog box, select the new template that you have just created, **ConfigMgr MDM Web Server**, and then click **OK**.  

##  <a name="bkmk_requestCert"></a> Request the web server certificate for each site system role  
 Devices enrolled for On\-premises Mobile Device Management must trust SSL endpoints hosting the enrollment point, enrollment proxy point, distribution point, and  device management point.  The steps below describe how to request the web server certificate for IIS. You must do this for each server (SSL endpoint) hosting one of the required site system roles for On\-premises Mobile Device Management.  

1. On the primary site server, open command prompt with administrator permission, type **MMC** and press **Enter**.  

2. In the MMC, click **File** > **Add/Remove Snap-in**.  

3. In the Certificates snap-in, select **Certificates**, click **Add**, select **Computer account**, click **Next**, click **Finish**, and then click **OK** to exit the Add or Remove Snap-in window.  

4. Right-click **Personal**, and then click **All Tasks** > **Request New Certificate**.  

5. In the Certificate Enrollment wizard, click **Next**, select **Active Directory Enrollment Policy** and click **Next**.  

6. Select the checkbox next to the web server certificate (**ConfigMgr MDM Web Server**), and then click **Enroll**.  

7. Once certificate is enrolled, click **Finish**.  

   Because each server will need a unique web server certificate, you need to repeat this process for every server hosting one of the required site system roles for On\-premises Mobile Device Management.  If one server hosts all the site system roles, you just need to request one web server certificate.  

##  <a name="bkmk_bindCert"></a> Bind the certificate to the web server  
 The new certificate now needs to be bound to the web server of each site system server hosting the required site system roles for On\-premises Mobile Device Management. Follow the steps below for each server hosting the enrollment point and enrollment proxy point site system roles. If one server hosts all the site system roles, you only need to follow these steps once. You do not have to do this task for the distribution point and device management point site system roles since they automatically receive the required certificate during enrollment.  

1.  On the server hosting the enrollment point, enrollment proxy point, distribution point, or device management point, click **Start** > **Administrative Tools** > **IIS Manager**.  

2.  Under Connections, navigate to and right-click **Default Web Site**, and then  click **Edit Bindings...**  

3.  In Site Bindings dialog, click **https**, and then click **Edit...**  

4.  In the Edit Site Binding dialog, select the certificate you just enrolled for the **SSL certificate**, click **OK**, and then click **Close**.  

5.  In IIS Manager console, under Connections, select the web server, and then in the right Actions panel, click **Restart**.  

##  <a name="bkmk_exportCert"></a> Export the certificate with the same root as the web server certificate  
 Active Directory Certificate Services typically installs the required certificate from the CA on all domain-joined devices. But non-domain-joined devices will not be able to communicate with the site system roles without certificate from the root CA. To get the certificate required for devices to communicate with the site system roles, you can export it   from the certificate bound to the web server.  

 Follow these steps to export the root certificate of the web server's certificate.  

1.  In IIS Manager, click **Default Web Site**, and then in the right Action panel, click **Bindings...**  

2.  In the Site Bindings dialog, click **https**, and then click **Edit...**  

3.  Make sure the web server certificate is selected, and click **View...**  

4.  In properties of the web server certificate, click **Certification Path**, click the root at the top of the certification path, and click **View Certificate**.  

5.  In the properties of the root certificate, click **Details**, and then click **Copy to File...**  

6.  In the Certificate Export Wizard, click **Next**.  

7.  Make sure **DER encoded binary X.509 (.CER)** is selected for format, and click **Next**.  

8.  For the file name, click **Browse...**, choose a location to save the certificate file, name the file, and click **Save**.  

     Devices to be enrolled will need access to this file to import the root certificate, so you choose a common location that most computers and devices can access, or you can save it to a convenient location now (like the C drive) and move it to common location later.  

     Click **Next**.  

9. Review the settings, and click **Finish** .  
