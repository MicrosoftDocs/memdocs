---
title: Configure a software update point to use TLS/SSL with a PKI certificate tutorial
titleSuffix: "Configuration Manager"
description: "Tutorial - Configure Windows Server Update Services (WSUS) servers and the software update points to use TLS/SSL with a PKI certificate."
author: mestew 
ms.author: mstewart
manager: dougeby
ms.date: 09/01/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
# Customer intent: As a Configuration Manager admin, I want to enable my WSUS servers and software update points to use TLS/SSL to reduce the ability of a potential attacker to remotely compromise a client and elevate privileges.
---

# Tutorial: Configure a software update point to use TLS/SSL with a PKI certificate

*Applies to: Configuration Manager (current branch)*

Configuring Windows Server Update Services (WSUS) servers and their corresponding software update points (SUP) to use TLS/SSL may reduce the ability of a potential attacker to remotely compromise a client and elevate privileges. To ensure that the best security protocols are in place, we recommend that you use the TLS/SSL protocol to help secure your software update infrastructure. This article walks you through the steps required to configure each of your WSUS servers and the software update point to use HTTPS.

In this tutorial, you will:
> [!div class="checklist"]
> * Obtain a PKI certificate, if needed
> * Bind the certificate to the WSUS Administration website
> * Configure the WSUS web services to require SSL
> * Configure the WSUS application to use SSL
> * Configure the Configuration Manager software update point to require SSL communication to the WSUS server
> * Verify functionality

## Considerations and limitations

WSUS uses TLS/SSL to authenticate client computers and downstream WSUS servers to the upstream WSUS server. WSUS also uses TLS/SSL to encrypt update metadata. WSUS doesn't use TLS/SSL for an update's content files. The content files are signed and the hash of the file is included in the update's metadata. Before the files are downloaded and installed by the client, both the digital signature and hash are checked. If either check fails, the update won't be installed.

Consider the following limitations when you use TLS/SSL to secure a WSUS deployment:

- Using TLS/SSL increases the server workload. You should expect a small performance loss from encrypting all the metadata that is sent over the network.
- If you use WSUS with a remote SQL Server database, the connection between the WSUS server and the database server isn't secured by TLS/SSL. If the database connection must be secured, consider the following recommendations:
   - Move the WSUS database to the WSUS server.
   - Move the remote database server and the WSUS server to a private network.
   - Deploy Internet Protocol security (IPsec) to help secure network traffic.

When configuring WSUS servers and their software update points to use TLS/SSL, you may want to phase in the configuration changes for large Configuration Manager hierarchies. If you choose to phase in these changes, start at the bottom of the hierarchy and move upwards ending with the central administration site.  

## Prerequisites

This tutorial covers the most common method to obtain a certificate for use with IIS. Whichever method your organization uses, ensure that the certificate meets the [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md) for a Configuration Manager software update point. As with any certificate, the certificate authority must be trusted by devices communicating with the WSUS server. 

- A WSUS server with the software update point role installed
- One of the two following options:
   - An appropriate PKI certificate already in the WSUS server's **Personal** certificate store.
   - The ability to request and obtain an appropriate PKI certificate for the WSUS server from your Enterprise root certificate authority (CA).
      - By default, most certificate templates including the WebServer certificate template will only issue to Domain Admins. If the logged in user isn't a domain admin, their user account will need to be granted the **Enroll** permission on the certificate template.

## <a name="bkmk_pki"></a> Obtain the certificate from the CA if needed

If you already have an appropriate certificate in the WSUS server's **Personal** certificate store, skip this section and start with the [Bind the certificate](#bkmk_bind) section. To send a certificate request to your internal CA to install a new certificate, follow the instructions in this section.
 
1. From the WSUS server, open an administrative command prompt and run `certlm.msc`. Your user account needs to be a local administrator to manage certificates for the local computer.

   The Certificate Manager tool for the local device appears.

1. Expand **Personal**, then right-click on **Certificates**.
1. Select **All Tasks** then **Request New Certificate**.
1. Choose **Next** to begin certificate enrollment.
1. Choose the type of certificate to enroll. You may be prompted for additional information to enroll the certificate. Typically, you'll specify the following information at minimum:
   - **Common name:** Found on the **Subject** tab, set the value to the WSUS server's FQDN.
   - **Friendly name:** Found on the **General** tab, set the value to a descriptive name to help you identify the certificate later.
:::image type="content" source="media/certificate-properties.png" alt-text="Certificate properties window to specify more information for enrollment":::
1. Select **Enroll** then **Finish** to complete the enrollment.
1. Open the certificate if you want to see details about it such as the certificate's thumbprint.

## <a name="bkmk_bind"></a> Bind the certificate to the WSUS Administration site

Once you have the certificate in the WSUS server's personal certificate store, bind it to the WSUS Administration site in IIS.

1. On the WSUS server, open Internet Information Services (IIS) Manager.
1. Go to **Sites** > **WSUS Administration**.
1. Select **Bindings** from either the action menu or by right clicking on the site.
1. In the **Site Bindings** window, select the line for **https**, then select **Edit...**. Note the **Port** numbers for the WSUS Administration site.
   - Don't remove the HTTP site binding. WSUS uses HTTP for the update content files.
1. Under the **SSL certificate** option, choose the certificate to bind to the WSUS Administration site. The certificate's friendly name is shown in the drop down menu. If a friendly name wasn't specified, then the certificate's `IssuedTo` field is shown. If you're not sure which certificate to use, select **View** and verify the thumbprint matches the one you obtained.  
   :::image type="content" source="media/edit-site-binding.png" alt-text="Edit Site Binding window with SSL certificate selection":::
1. Select **OK** when you're done, then **Close** to exit the site bindings. Keep Internet Information Services (IIS) Manager open for the next steps.



## <a name="bkmk_webserv"></a> Configure the WSUS web services to require SSL

1. In IIS Manager on the WSUS server, go to **Sites** > **WSUS Administration**.
1. Expand the WSUS Administration site so you see the list of web services and virtual directories for WSUS.
1. For each of the below WSUS web services:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Make the following changes:

      1. Select **SSL Settings**.
      1. Enable the **Require SSL** option.
      1. Verify the **Client certificates** is set to **Ignore**.
      1. Select **Apply**.

Don't set the SSL settings at the top-level WSUS Administration site. 
