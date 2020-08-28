---
title: Configure a software update point to use SSL with a PKI certificate tutorial
titleSuffix: "Configuration Manager"
description: "Tutorial - Configure WSUS servers and the software update points to use SSL with a PKI certificate."
author: mestew 
ms.author: mstewart
manager: dougeby
ms.date: 09/01/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
# Customer intent: As a Configuration Manager admin, I want to enable my WSUS servers and software update points to use SSL to further reduce the ability of a potential attacker to remotely compromise a client and elevate privileges.
---

# Tutorial: Configure a software update point to use SSL with a PKI certificate

*Applies to: Configuration Manager (current branch)*

<!--
> [!IMPORTANT]  
>  Before you install the software update point site system role (SUP), you must verify that the server meets the required dependencies and determines the software update point infrastructure on the site. For more information about how to plan for software updates and to determine your software update point infrastructure, see [Plan for software updates](../plan-design/plan-for-software-updates.md).  -->

Configuring Windows Server Update Services (WSUS) servers and their corresponding software update points (SUP) to use SSL may further reduce the ability of a potential attacker to remotely compromise a client and elevate privileges. To ensure that the best security protocols are in place, we recommend that you use the SSL/TLS protocol to help secure your software update infrastructure. WSUS uses SSL/TLS to authenticate client computers and downstream WSUS servers to the upstream WSUS server. WSUS also uses SSL/TLS to encrypt update metadata. This article walks you through the steps required to configure each of your WSUS servers and the software update point to use HTTPS.

In this tutorial, you will:
> [!div class="checklist"]
> * Obtain the PKI certificate, if needed
> * Bind the certificate in IIS
> * blah
> * blah
> * blah

## Prerequisites

- A WSUS server with the software update point role installed
- One of the two following options:
   - An appropriate PKI certificate already in the WSUS server's **Personal** certificate store.
   - The ability to request and enroll an appropriate PKI certificate for the WSUS server using an Active Directory Enrollment Policy. 
      - By default, most certificate templates including the WebServer certificate template will only issue to Domain Admins. If the logged in user isn't a domain admin, their user account will need to be granted the **Enroll** permission on the certificate template.

For more information about the certificate requirements, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements#BKMK_PKIcertificates_for_servers).

## <a name="bkmk_pki"></a> Obtain the certificate from the CA if needed
If you already have an appropriate PKI certificate in the WSUS server's **Personal** certificate store, skip this section and start with the [Bind the certificate](#bkmk_bind) section. If you need to send a certificate request to an enrollment server to install a new certificate, follow the instructions in this section.
 
1. From the WSUS server, open an administrative command prompt and run `certlm.msc`. Your user account needs to be a local administrator to manage certificates for the local computer.

   The Certificate Manager tool for the local device appears.

1. Expand **Personal**, then right-click on **Certificates**.
1. Select **All Tasks** then **Request New Certificate**. 
1. Choose **Next** to begin certificate enrollment. 

### Open the Certificate snap-in
1. From the WSUS server, open the Microsoft Management Console (mmc.exe).
1. Select **File** then **Add/Remove Sanp-in...**.
1. Select the **Certificates** snap-in, then **Add**.
1. Specify the following options for the snap-in:
   1. Choose the **Computer account** when prompted to select the account to manage the certificates for and select **Next**.
   1. In the **Select Computer** window, choose the **Local computer: (the computer this console is running on)** option and then **Finish**.
1. Select **OK** to load the **Certificates (Local Computer)** snap-in.
1. 


## <a name="bkmk_bind></a> Bind the certificate 