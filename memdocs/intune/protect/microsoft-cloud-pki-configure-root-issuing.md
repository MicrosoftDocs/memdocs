---
title: Configure Microsoft Cloud PKI root and issuing CA for Microsoft Intune  
description: Configure a root and issuing CA for the Microsoft Cloud PKI service.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 02/26/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier3
- M365-identity-device-management
- certificates
---
# Configure Intune root CA and issuing CA for Microsoft Cloud PKI      

This article describes how to create and deploy a Microsoft Cloud PKI root CA and issuing CA in Microsoft Intune. An intermediate/issuing CA issues certificate to devices based on the certificate profiles you create. 
     
## Prerequisites  
For more information about how to prepare your tenant for Microsoft Cloud PKI, including key concepts and requirements, see: 
* [Overview of Microsoft Cloud PKI for Intune](microsoft-cloud-pki-overview.md): Review for architecture, tenant requirements, a feature summary, and known issues and limitations.    
* [Deployment models](microsoft-cloud-pki-deployment): Review for an explanation of Microsoft Cloud PKI deployment options.  
* [Fundamentals](microsoft-cloud-pki-fundamentals): Review for PKI fundamentals and concepts that are important to know prior to configuration and deployment.  

## Role based access control    
The account you use to sign into the Microsoft Intune admin center must have permission to create CAs. The roles with built-in permissions include Microsoft Entra Global administrator and Intune service administrator account. Alternatively, you can assign Cloud PKI CA permissions to an admin user.  

## Step 1: Create root CA in admin center    
Before you can start to issue certificates to managed devices, you need to create a Root Certification Authority in your tenant to act as the trust anchor. This section describes how to create the Root CA. At least one Root CA must be created before an Issuing CA can be created.  

1. Sign in to the Microsoft Intune admin center. 
1. Go to **Tenant administration** > **Cloud PKI**, and then select **Create**.   

   > [!div class="mx-imgBorder"]
   > ![Image of the Microsoft Intune admin center Cloud PKI page, highlighting the path to create a Cloud PKI.](./media/microsoft-cloud-pki/create-microsoft-cloud-pki.png)  

1. Enter a **Name** and optional **Description** for the Intune object you're creating so you can distinguish it from other Cloud PKIs in your tenant.  

   > [!div class="mx-imgBorder"]
   > ![Image of the Cloud PKI Basics tab in the admin center.](./media/microsoft-cloud-pki/create-cloud-pki-basics.png)  

1. Select **Next** to continue to **Configuration settings**.    
1. Configure the following settings for the root CA:  
     1. **CA type**: Select **Root CA**. 
     1. **Validity period**: Select 5, 10, 15, 20, 25, or 30 years. To create a Root CA with a custom validity period, use [Microsoft Graph API]() to create the CAs. 
1. For **Extended Key Usages**, select how you intend to use the CA. To prevent potential security risks, CAs are limited to specific types of use.   
     1. Under **Type**, select the purpose of the CA. Optionally, you can set a custom EKU. The **Any Purpose (2.5.29.37.0)** EKU isn't for use, because it's overly permissive and a potential security risk.  
     1. Enter the **Name** and **Object Identifier**.  

   > [!div class="mx-imgBorder"]
   > ![Image of the Configuration settings tab, showing the Extended Key Usages section for Cloud PKI.](./media/microsoft-cloud-pki/cloud-pki-extended-usage.png)  

 > [!NOTE]
 > Keep in mind that Root CA EKU/OID constraints are a superset of the Issuing CA. This means that when you create an Issuing CA, you can only select the EKUs defined for the Root CA.  If you don't define the EKU in the Root CA, it won't show up as an EKU option for the Issuing CA.   

1. Under **Subject attributes** enter a **Common name (CN)** for the Root CA. 

    Optional attributes include:    
     - Organization (O)  
     - Organizational unit (OU)
     - Country (C)  
     - State or province (ST)
     - Locality (L)  

     To adhere to PKI standards, Intune enforces a two-character limit for country/region.   

1. Under **Encryption**, enter the **Key size and algorithm**. Your options:  
     - **RSA-2048 and SHA-256**
     - **RSA-3096 and SHA-384**
     - **RSA-4096 and SHA-512**  

   This setting enforces the upper bound key size and hash algorithm that can be used when configuring a device configuration SCEP certificate profile in Intune. It enables you to select any key size and hash up to what is set on the Cloud PKI Issuing CA. Keep in mind a 1024 key size and SHA-1 hash isn't supported with Cloud PKI.   
1. Select **Next** to continue to **Scope tags**.    
1. Optionally, you can add scope tags to control visibility and access control.  
1. Select **Next** to continue to **Review + create**.    
1. Review the summary provided. You won't be able to edit these properties after you create the CA. If needed, select **Back** to edit the settings and ensure they're correct and satisfy your PKI requirements. If later you need to add another EKU, you must create a new CA.  

1. When you're ready to finalize everything, select **Create**.   
1. Return to the Cloud PKI CA list in the admin center. Select **Refresh** to see your new CA.  

      > [!div class="mx-imgBorder"]
      > ![Image of the Microsoft Cloud PKI list showing the new Root CA.](./media/microsoft-cloud-pki/microsoft-intune-cloud-pki-list.png)  

## Step 2: Create issuing CA in admin center    
An Issuing Certification Authority is required to issue certificates for Intune-managed devices. Cloud PKI automatically provides a SCEP service that acts as a Certificate Registration Authority. It requests certificates from the Issuing CA on behalf of Intune-managed devices using a SCEP profile.   

> [!NOTE]
> With Microsoft Cloud PKI, you don't need to:  
> - Install and configure an NDES server.    
> - Install and configure the Intune certificate connector.   
> - Configure a proxy service to enable access to the NDES server URL.  

1.Return to ***Tenant administration** > **Cloud PKI**.  
1. Enter a **Name** and optional **Description** for so you can distinguish this CA from others in your tenant.  
1. Select **Next** to continue to **Configuration settings**.    
1. Configure the following settings for the issuing CA:  
     1. **CA type**: Select **Issuing CA**. Then choose:   
       1. **Root CA source**: Select **Intune**. This setting determines the root CA source anchoring the issuing CA. 
       1. **Root CA**: Select one of the root CAs you created in Intune to anchor against. 
     1. **Validity period**: Select 2, 4, 6, 8, or 10 years. The validity period of the issuing CA can't be longer than the Root CA. To create an issuing CA with a custom validity period, use [Microsoft Graph API]() to create the CAs. 
1. For **Extended Key Usages**, select how you intend to use the CA. To prevent potential security risks, CAs are limited to specific types of use.  
     * For **Type**, select the purpose of the CA. The **Any Purpose (2.5.29.37.0)** EKU isn't for use, because it's overly permissive and a potential security risk.  
     *  Alternatively, to create a custom EKU, enter the **Name** and **Object Identifier**.  

       > [!NOTE]
       > You can only select from EKUs defined in the Root CA.  If you didn't define an EKU in the Root CA, it won't show up as an EKU option here.   

1. Under **Subject attributes** enter a **Common name (CN)** for the issuing CA. 

    Optional attributes include:    
     - Organization (O)  
     - Organizational unit (OU)
     - Country (C)  
     - State/province (ST)
     - Locality (L)  

     To adhere to PKI standards, Intune enforces a two-character limit for country/region.   

1. Select **Next** to continue to **Scope tags**.  
1. Optionally, you can add scope tags to control visibility and access control.   
1. Select **Next** to continue to **Review + create**.    
1. Review the summary provided. 

   > [!TIP]
   > You won't be able to edit these properties after you create the CA. If needed, select **Back** to edit the settings and ensure they are correct and satisfy your PKI requirements. If later you require additional EKUs, you must create a new CA.

   When you're ready to finalize everything, select **Create**.   
1. Return to the Cloud PKI CA list in the admin center. Select **Refresh** to see your new issuing CA.  

Go to **Properties** to view the properties of root CAs and issuing CAs in your tenant. Available properties include: 

- Certificate Revocation List (CRL) distribution point URI 
- Authority Information Access (AIA) URI 
- SCEP URI (*issuing CA only*)  

Take note of these endpoint locations so you have them for later. Relying parties need network visibility to these endpoints. For example, you need to know the SCEP URI endpoint when you create SCEP profiles.    

>[!NOTE]
> The CRL is valid for 7 days, and is refreshed and republished in the admin center every 3.5 days. A refresh also happens every time an end-entity certificate is revoked.    

When you create the trusted certificate profile required for Cloud PKI, you must have the public keys for the root CA certificates and issuing CA certificates. The public keys establish a chain of trust between Intune managed devices and Cloud PKI when requesting a certificate using SCEP certificate profiles. Select **Download** to download the public keys for these certificates. Repeat this step for every CA you have. The Root and Issuing CA certificates are also required to be installed on any relying parties, or authentication endpoints, supporting certificate-based authentication.  

## Step 3: Create certificate profiles   
To issue certificates, you must create a trusted certificate profile for your root and issuing CAs. The trusted certificate profile establishes trust with the Cloud PKI certificate registration authority supporting the SCEP protocol. A trusted certificate profile required for each platform (Windows, Android, iOS/iPad, macOS) that's issuing Cloud PKI SCEP certificates. 

This step requires you to: 

* Create a trusted certificate profile for the Cloud PKI root CA.    
* Create a trusted certificate profile for a Cloud PKI issuing CA.   
* Create an SCEP certificate profile for a Cloud PKI issuing CA.  


### Create trusted certificate profile  
>[!Note]
> The file names are based on the Common Names specified in the CA.  Some browsers, like Edge, show a warning if you download a file with a .cer or other well-known certificate extension. If you receive this warning, select **Keep**.  

 In the admin center, [create a trusted certificate profile](certificates-trusted-root.md#to-create-a-trusted-certificate-profile) for each OS platform you're targeting. Create one trusted certificate profile for the root CA certificate and one for the issuing CA. 

When prompted to, enter the public keys for the root CA and issuing CA. Complete the following steps to download the public keys for your CAs.  

For the root CA:  

1. Sign in to the Microsoft Intune admin center. 
1. Go to **Tenant administration** > **Cloud PKI**.
1. Select a CA that has a root type.  
1. Go to **Properties**. 
1. Select **Download**. Wait while the public key downloads. 

For the issuing CA:  

1. Return to your **Cloud PKI** list.  
1. Select a CA that has an issuing type.  
1. Go to **Properties**. 
1. Select **Download**. Wait while the public key downloads. 

The Cloud PKI Root CA and Issuing CA you download must be installed on all relying parties. For more information about deployment models, see [Microsoft Cloud PKI deployment](microsoft-cloud-pki-deployment).  


### Create SCEP certificate profile  
>[!NOTE]
> Only Cloud PKI Issuing CAs (including BYOCA Issuing CA) can be used to issue SCEP certificates to Intune managed devices.  

Just like you did for the trusted certificate profiles, create an SCEP certificate profile for each OS platform you're targeting. The SCEP certificate profile is used to request a leaf *Client Authentication* certificate from the Issuing CA. This type of certificate is used in certificate based authentication scenarios, for things like Wi-Fi and VPN access. 

1. Return to **Tenant administration** > **Cloud PKI**.
1. Select a CA that has an *issuing* type.  
1. Go to **Properties**. 
1. Next to the SCEP URI property, select **Copy to clipboard**.  
1. In the admin center, [create a SCEP certificate profile](certificates-profile-scep.md#create-a-scep-certificate-profile) for each OS platform you're targeting.   
1. In the profile, under **Root Certificate**, link the trusted certificate profile. The trusted certificate you select must be the Root CA certificate that the Issuing CA is anchored to in the CA hierarchy.  
    
      > [!div class="mx-imgBorder"]
      > ![Screenshot of available root certificate you can select.](./media/microsoft-cloud-pki/.png)  

1. For **SCEP Server URLS**, paste the SCEP URI. 
1. Configure the remaining settings, following these best practices:  
    1. **Subject name format**: Ensure the variables specified are available on the user or device object in Microsoft Entra ID. For example, if the target user of this profile doesn't have an email address attribute but the email address in this profile is filled in, the certificate won't be issued. An error also appears in the SCEP certificate profile report.  
    1. **Extended Key Usage**: Microsoft Cloud PKI doesn't support the **Any Purpose** option.   
    1. **SCEP Server URLs**: Don't combine NDES/SCEP URLs with Microsoft Cloud PKI Issuing CA SCEP URLs.  
1. Assign and review the profile. When you're ready to finalize everything, select **Create**.  