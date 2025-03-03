---
title: Certificates for on-premises MDM
titleSuffix: Configuration Manager
description: Set up certificates for trusted communications with on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: install-set-up-deploy
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Set up certificates for trusted communications with on-premises MDM

*Applies to: Configuration Manager (current branch)*

Configuration Manager on-premises mobile device management (MDM) requires that you configure the site system roles for trusted communications with managed devices. You need two types of certificates:

- A **web server certificate** in IIS on the servers hosting the required site system roles. If one server hosts multiple site system roles, then you only need one certificate for that server. If each role is on a separate server, each server needs a separate certificate.

- The **trusted root certificate** of the certificate authority (CA) that issues the web server certificates. Install this root certificate on all devices that need to connect to the site system roles.

For domain-joined devices, if you use Active Directory Certificate Services, it can automatically install these certificates on all devices. For non-domain-joined devices, install the trusted root certificate by some other means.

For bulk-enrolled devices, you can include the certificate in the enrollment package. For user-enrolled devices, you need to add the certificate through email, web download, or some other method.

If you use a public and globally trusted certificate provider to issue the server certificates, you can avoid having to manually install the trusted root certificate on each device. Most devices natively trust these public authorities. This method is a useful alternative for user-enrolled devices, instead of installing the certificate through other means.

> [!IMPORTANT]  
> There are many ways to set up the certificates for trusted communications between devices and the site system servers for on-premises MDM. The information in this article is an example of one way to do it. This method requires Active Directory Certificate Services, with a certification authority and the certification authority web enrollment role. For more information, see [Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="bkmk_configCa"></a> Publish the CRL

By default, the Active Directory certification authority (CA) uses LDAP-based certificate revocation lists (CRLs). It allows connections to the CRL for domain-joined devices. To allow non-domain-joined devices to trust certificates issued from the CA, add an HTTP-based CRL.

1. On the server running the certification authority for your site, go to the **Start** menu, select **Administrative Tools**, and choose **Certification Authority**.

1. In the Certification Authority console, right-click **CertificateAuthority**, and then select **Properties**.

1. In CertificateAuthority properties, switch to the **Extensions** tab. Make sure that **Select extension** is set to **CRL Distribution Point (CDP)**.

1. Select `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Then select the following options:

    - **Include in CRLs. Clients use this to find Delta CRL locations.**

    - **Include in CDP extension of issued certificates.**

    - **Include in the IDP extension of issued CRLs**

1. Switch to the **Exit Module** tab. Select **Properties**, then select **Allow certificates to be published to the file system**. You'll see a notice to restart Active Directory Certificate Services.

1. Right-click **Revoked Certificates**, select **All Tasks**, and then choose **Publish**.

1. In the Publish CRL window, select **Delta CRL only**, and then select **OK** to close the window.

## <a name="bkmk_certTempl"></a> Create the certificate template

The CA uses the web server certificate template to issue certificates for the servers hosting the site system roles. These servers will be SSL endpoints for trusted communications between the site system roles and enrolled devices.

1. Create a domain security group named **ConfigMgr MDM servers**. Add to the group the computer accounts of the site system servers.

1. In the Certification Authority console, right-click **Certificate Templates**, and choose **Manage**. This action loads the Certificate Templates console.

1. In the results pane, right-click the entry that displays **Web Server** in the **Template Display Name** column, and then select **Duplicate Template**.

1. In the **Duplicate Template** window, select **Windows 2003 Server, Enterprise Edition** or **Windows 2008 Server, Enterprise Edition**, and then select **OK**.

    > [!TIP]
    > Configuration Manager supports Windows 2008 Server certificate templates, also known as V3 or Cryptography: Next Generation (CNG) certificates. For more information, see [CNG v3 certificates overview](../../core/plan-design/network/cng-certificates-overview.md).

    If your CA runs on Windows Server 2012 or later, this window doesn't show the option for certificate template version. After you duplicate the template, select the version on the **Compatibility** tab of the template properties.

1. In the **Properties of New Template** window, on the **General** tab, enter a template name. The CA uses this name to generate the web certificates that will be used on Configuration Manager site systems. For example, type **ConfigMgr MDM web server**.

1. Switch to the **Subject Name** tab, and select **Build from Active Directory information**. For the subject name format, specify **DNS name**. If **User Principal Name (UPN)** is selected, disable the option for alternate subject name.

1. Switch to the **Security** tab.

    1. Remove the **Enroll** permission from the **Domain Admins** and **Enterprise Admins** security groups.

    1. Select **Add**, and enter the name of your security group. For example, **ConfigMgr MDM servers**. Select **OK** to close the window.

    1. Select the **Enroll** permission for this group. Don't remove the **Read** permission.

1. Select **OK** to save your changes, and close the Certificate Templates console.

1. In the Certification Authority console, right-click **Certificate Templates**, select **New**, and then choose **Certificate Template to Issue**.

1. In the **Enable Certificate Templates** window, select the new template. For example, **ConfigMgr MDM web server**. Then select **OK** to save and close the window.

## <a name="bkmk_requestCert"></a> Request the certificate

This process describes how to request the web server certificate for IIS. Do this process for each site system server that hosts one of the roles for on-premises MDM.

1. On the site system server that hosts one of the roles, open a command prompt as an administrator. Enter `mmc` to open an empty Microsoft Management Console.

1. In the console window, go to the **File** menu, and select **Add/Remove Snap-in**.

    1. Choose **Certificates** from the list of available snap-ins and select **Add**.

    1. In the Certificates snap-in window, choose **Computer account**. Select **Next**, and then select **Finish** to manage the local computer.

    1. Select **OK** to exit the Add or Remove Snap-in window.

1. Expand **Certificates (Local Computer)**, and select the **Personal** store. Go to the **Action** menu, select **All Tasks**, and choose **Request New Certificate**. This action communicates with Active Directory Certificate Services to create a new certificate using the template you previously created.

    1. In the Certificate Enrollment wizard, on the Before You Begin page, select **Next**.

    1. On the Select Certificate Enrollment Policy page, select **Active Directory Enrollment Policy**, and then select **Next**.

    1. Select your web server certificate template (**ConfigMgr MDM Web Server**), and then select **Enroll**.

    1. After it requests the certificate, select **Finish**.

Each server needs a unique web server certificate. Repeat this process for every server that hosts one of the required site system roles. If one server hosts all the site system roles, you just need to request one web server certificate.

## <a name="bkmk_bindCert"></a> Bind the certificate

The next step is to bind the new certificate to the web server. Follow this process for each server that hosts the *enrollment point* and *enrollment proxy point* site system roles. If one server hosts all the site system roles, you only need to do this process once.

> [!NOTE]
> You don't have to do this process for the distribution point and device management point site system roles. They automatically receive the required certificate during enrollment.

1. On the server hosting the enrollment point or enrollment proxy point, go to the **Start** menu, select **Administrative Tools**, and choose **IIS Manager**.

1. In the list of Connections, select the **Default Web Site**, and then select **Edit Bindings**.

    1. In Site Bindings window, select **https**, and then select **Edit**.

    1. In the Edit Site Binding window, select the newly enrolled certificate for the **SSL certificate**. Select **OK** to save, and then select **Close**.

1. In the IIS Manager console, in the list of Connections, select the web server. In the Action panel on the right side, select **Restart**. This action restarts the web server service.

## <a name="bkmk_exportCert"></a> Export the trusted root certificate

Active Directory Certificate Services automatically installs the required certificate from the CA on all domain-joined devices. To get the certificate that's required for non-domain-joined devices to communicate with the site system roles, export it from the certificate bound to the web server.

1. In IIS Manager, select the **Default Web Site**. In the Action panel on the right side, select **Bindings**.

1. In the Site Bindings window, select **https**, and then select **Edit**.

1. Select the web server certificate, and select **View**.

1. In properties of the web server certificate, switch to the **Certification Path** tab. Select the root of the certification path, and select **View Certificate**.

1. In the properties of the root certificate, switch to the **Details** tab, and then select **Copy to File**.

1. In the Certificate Export Wizard, on the Welcome page, select **Next**.

1. Select **DER encoded binary X.509 (.CER)** as the format, and select **Next**.

1. Enter a path and file name to identify this trusted root certificate. For the file name, click **Browse...**, choose a location to save the certificate file, name the file, and select **Next**.

1. Review the settings, and select **Finish** to export the certificate to file.

Depending upon your certificate authority design, you may need to export additional subordinate CA root certificates. Repeat this process to export the other certificates in the web server certificate's certification path.

## Next step

> [!div class="nextstepaction"]
> [Set up device enrollment](set-up-device-enrollment-on-premises-mdm.md)