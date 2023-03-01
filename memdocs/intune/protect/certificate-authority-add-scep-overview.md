---
title: Use third-party certification authorities (CA) with SCEP in Microsoft Intune
description: In Microsoft Intune, you can add a vendor or third-party certificate authority (CA) to issue certificates to mobile devices using the SCEP protocol. In this overview, an Azure Active Directory (Azure AD) application gives Microsoft Intune permissions to validate certificates. Then, use the application ID, authentication key, and tenant ID of the AAD application in the setup of your SCEP server to issue certificates. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Add partner certification authority in Intune using SCEP

Use third-party certification authorities (CA) with Intune. Third-party CAs can provision mobile devices with new or renewed certificates by using the Simple Certificate Enrollment Protocol (SCEP), and can support Windows, iOS/iPadOS, Android, and macOS devices.

There are two parts to using this feature: open-source API, and the Intune administrator tasks.

**Part 1 - Use an open-source API**  
Microsoft created an API to integrate with Intune. Through the API you can validate certificates, send success or failure notifications, and use SSL, specifically SSL socket factory, to communicate with Intune.

The API is available on the [Intune SCEP API public GitHub repository](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation) for you to download, and use in your solutions. Use this API with third-party SCEP servers to run custom challenge validation against Intune before SCEP provisions a certificate to a device.

[Integrate with Intune SCEP management solution](scep-libraries-apis.md) provides more details on using the API, its methods, and testing the solution you build.

**Part 2 - Create the application and profile**  
Using an Azure Active Directory (Azure AD) application, you can delegate rights to Intune to handle SCEP requests coming from devices. The Azure AD application includes application ID and authentication key values that are used within the API solution the developer creates. Administrators then create and deploy SCEP certificates profiles using Intune and can view reports on the deployment status on the devices.

This article provides an overview of this feature from an Administrator-perspective, including creating the Azure AD application.

## Overview

The following steps provide an overview of using SCEP for certificates in Intune:

1. In Intune, an administrator creates a SCEP certificate profile, and then targets the profile to users or devices.
2. The device checks in to Intune.
3. Intune creates a unique SCEP challenge. It also adds additional integrity-check information, such as what the expected subject and SAN should be.
4. Intune encrypts and signs both the challenge and integrity-check information, and then sends this information to the device with the SCEP request.
5. The device generates a certificate signing request (CSR) and public/private key pair on the device based on the SCEP certificate profile that's pushed from Intune.
6. The CSR and encrypted/signed challenge are sent to the third-party SCEP server endpoint.
7. The SCEP server sends the CSR and the challenge to Intune. Intune then validates the signature, decrypts the payload, and compares the CSR to the integrity-check information.
8. Intune sends back a response to the SCEP server, and states whether the challenge validation is successful or not.  
9. If the challenge is successfully verified, then the SCEP server issues the certificate to the device.

The following diagram shows a detailed flow of third-party SCEP integration with Intune:

> [!div class="mx-imgBorder"]
> ![How third-party certification authority SCEP integrates with Microsoft Intune](./media/certificate-authority-add-scep-overview/scep-certificate-vendor-integration.png)

## Set up third-party CA integration

### Validate third-party certification authority

Before integrating third-party certification authorities with Intune, confirm that the CA you're using supports Intune. [Third-party CA partners](#third-party-certification-authority-partners) (in this article) includes a list. You can also check your certification authority's guidance for more information. The CA may include setup instructions specific to their implementation.

> [!NOTE]
> To support the following devices, the CA must support the use of an HTTPS URL when you configure  you must configure an HTTPS URL when you configure *SCEP Server URLs* for the [SCEP certificate profile](certificates-profile-scep.md):
> - Android device administrator
> - Android Enterprise device owner
> - Android Enterprise corporate-owned work profile
> - Android Enterprise personally-owned work profile

### Authorize communication between CA and Intune

To allow a third-party SCEP server to run custom challenge validation with Intune, create an app in Azure AD. This app gives delegated rights to Intune to validate SCEP requests.

Be sure you have the required permissions to register an Azure AD app. See [Required permissions](/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions), in the Azure AD documentation.

#### Create an application in Azure Active Directory  

1. In the [Azure portal](https://portal.azure.com), go to **Azure Active Directory** > **App Registrations**, and then select **New registration**.

2. On the **Register an application** page, specify the following details:  
   - In the **Name** section, enter a meaningful application name.
   - For the **Supported account types** section, select **Accounts in any organizational directory**.  
   - For **Redirect URI**, leave the default of Web, and then specify the sign-on URL for the third-party SCEP server.

3. Select **Register** to create the application and to open the Overview page for the new app.

4. On the app **Overview** page, copy the **Application (client) ID** value and record it for later use. You'll need this value later.  

5. In the navigation pane for the app, go to **Certificates & secrets** under **Manage**. Select the **New client secret** button. Enter a value in Description, select any option for **Expires**, and then and choose **Add** to generate a *value* for the client secret.

   > [!IMPORTANT]  
   > Before you leave this page, copy the value for the client secret and record it for later use with your third-party CA implementation. This value is not shown again. Be sure to review the guidance for your third-party CA on how they want the Application ID, Authentication Key, and Tenant ID configured.  

6. Record your **Tenant ID**. The Tenant ID is the domain text after the @ sign in your account. For example, if your account is *admin@name.onmicrosoft.com*, then your tenant ID is **name.onmicrosoft.com**.  

7. In the navigation pane for the app, go to **API permissions**, which are under **Manage**. You're going to add two separate application permissions:

   1. Select **Add a permission**:
      1. On the *Request API permissions* page, select **Intune** and then select **Application permissions**.
      2. Select the checkbox for **scep_challenge_provider** (SCEP challenge validation).
      3. Select **Add permissions** to save this configuration.

   1. Select **Add a permission** again.
      1. On the *Request API permissions* page, select **Microsoft Graph** > **Application permissions**.
      2. Expand **Application** and select the checkbox for **Application.Read.All** (Read all applications).
      3. Select **Add permissions** to save this configuration.

8. Remain on the **API permissions** page, and select **Grant admin consent for** ***\<your tenant>***, and then select **Yes**.  

   The app registration process in Azure AD is complete.

### Configure and deploy a SCEP certificate profile

As the administrator, create a SCEP certificate profile to target to users or devices. Then, assign the profile.

- [Create a SCEP certificate profile](certificates-profile-scep.md#create-a-scep-certificate-profile)

- [Assign the certificate profile](certificates-profile-scep.md#assign-the-certificate-profile)

## Removing certificates

When you unenroll or wipe the device, the certificates are removed. The certificates aren't revoked.

## Third-party certification authority partners

The following third-party certification authorities support Intune:

- [DigiCert](https://knowledge.digicert.com/tutorials/microsoft-intune.html)
- [EJBCA](https://doc.primekey.com/ejbca/ejbca-integration/integrating-with-third-party-applications/microsoft-intune-device-certificate-enrollment)
- [Entrust](https://go.entrustdatacard.com/pki/intune/)
- [EverTrust](https://evertrust.fr/en/products/)
- [GlobalSign](https://downloads.globalsign.com/acton/attachment/2674/f-6903f60b-9111-432d-b283-77823cc65500/1/-/-/-/-/globalsign-aeg-microsoft-intune-integration-guide.pdf)
- [HID Global](https://help.hydrantid.com/HydrantID_Intune_Integration.pdf)
- [IDnomic](https://www.idnomic.com/)
- [KeyTalk](https://keytalk.com/our-services)
- [Nexus Certificate Manager](https://doc.nexusgroup.com/display/PUB/Example%3A+SCEP+Intune+configuration+in+Protocol+Gateway)
- [SCEPman](https://azuremarketplace.microsoft.com/marketplace/apps/glueckkanja-gabag.scepman)
- [Sectigo](https://sectigo.com/products)
- [SecureW2](https://www.securew2.com/solutions/managed-devices/scep-ca-integration-with-microsoft-intune)
- [Venafi](https://www.venafi.com/platform/enterprise-mobility)

If you're a third-party CA interested in integrating your product with Intune, review the API guidance:

- [Intune SCEP API GitHub repository](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Intune SCEP API guidance for third party CAs](scep-libraries-apis.md)

## See also

- [Configure certificate profiles](certificates-scep-configure.md)
- [Intune SCEP API GitHub repository](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Intune SCEP API guidance for third party CAs](scep-libraries-apis.md)
