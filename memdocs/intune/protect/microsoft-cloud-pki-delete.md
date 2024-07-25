---
title: Delete issued PKI certificates with Microsoft Intune
titleSuffix: Microsoft Intune 
description: Delete certificates issued via Microsoft Intune cloud PKI. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: wicale  
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

ms.collection:
- tier1
- M365-identity-device-management
- certificates
- IntuneSuite
---
# Delete certification authority 
Delete a certification authority (CA) from the Microsoft Cloud PKI service. 

This article describes how to delete certificate authorities in the Microsoft Intune admin center. 

## Prerequisites  
Review the following requirements to successfully delete a CA in the Microsoft Intune admin center.  

- All leaf certificates issued by the CA must be revoked. 
- A root CA cannot be deleted until all anchored issuing CAs are deleted. 
- A CA in a paused state can't issue leaf certificates.
- A CA in a paused or revoked state continues to respond to CRL requests and AIA requests.
- Once you revoke a CA, it can't be undone. 
- Once you delete a CA, it can't be undone.  

## Role based access control for deleting a CA
A Microsoft Entra Intune Administrator role has permission to view and disable/enable a CA, and revoke issued leaf certificates. Custom Intune roles with the following permissions can do the same thing:  
  - Read CAs  
  - Disable and reenable CAs  
  - Revoke issued leaf certificates  


## Delete issuing certificate  

1. Sign in to the Microsoft Intune admin center and go to **Tenant administration** > **Cloud PKI**. 
1. Select an Issuing CA from the list of CA’s
2. Select the “Pause” button. A confirmation dialog will appear, select the “Pause” button to continue
3. Go back to the CA list, be sure to “Refresh” the CA list. The Status column will show “Paused”

4. Select the “Paused” CA. Two options are now available, “Resume” or “Revoke”. The “Resume” button will make the CA active again. The “Revoke” button will revoke the Issuing CA certificate. All existing leaf certificates issued by this CA will stop being authenticated. The CA will no longer be trusted by relying parties performing a trust chain operation. The Certificate Revocation List (CRL) of the Root CA will show the issuing CA cert has been revoked. 

   >[!NOTE]
   > To successfully “Revoke” the CA, all active leaf certificates must first be revoked. To revoke leaf certificates, use the “View all certificates” button to revoke each active leaf certificate. Alternatively, refer to the sample PowerShell script to bulk revoke all leaf certificates <LINK>.

   A confirmation dialog will appear, select the “Revoke” button to continue.  

   >[!IMPORTANT]
   > This action cannot be undone.

5. After the CA is “Revoked”, the CA list “Status” column will show “Revoked” for the CA. If not, click on the “Refresh” button to update the CA list.

6. Click on the revoked CA in the list. The “Delete” button will now be active. Click on “Delete” button:

   A confirmation dialog will appear, click on the “Delete” button to remove the CA from Intune.


7. “Refresh” the CA list, the deleted Issuing CA will no longer appear.  

## Delete root CA  
In to the Microsoft Intune admin center, go to **Tenant administration** > **Cloud PKI**.  

1. Sign in to the Microsoft Intune admin center and go to **Tenant administration** > **Cloud PKI**. 
1. Select a Root CA from the list of CA’s  

2. Select the “Delete” button  

   A confirmation dialog will appear, click on the “Delete” button.  

3. Refresh the CA list, the deleted CA will no longer appear.  

   > [!div class="mx-imgBorder"]
   > ![Image of the admin center, highlighting delete action for a root CA.](./media/microsoft-cloud-pki/.png)  

## Bulk revoke leaf certificates 
You can use the following sample script to revoke more than one leaf certificate at a time from an issuing CA. 

 >[!CAUTION]
 > Use the script with caution. You can't undo the revoke action for any of the leaf certificates.  











## Monitor Cloud PKI issuing CA

Each Cloud PKI issuing CA has a monitoring dashboard. Select **View all certificates** to view all issued certificates. Certificate report details should be available within 24 hours of the certificate being successfully issued to the device.

   > [!div class="mx-imgBorder"]
   > ![Image of the certificate count for Microsoft Cloud PKI in admin center.](./media/microsoft-cloud-pki/intune-certificate-count-cloud-pki.png)  

From here, you can also manually revoke an issued leaf certificate.

 1. Select **View all certificates**.
 1. Select the **Subject name** of the certificate you want to revoke.  
 1. On the certificate's details page, select **Revoke**.  

> [!TIP]
> When you manually revoke a certificate from a user or device that has an active SCEP certificate profile assignment, then on the next device check-in a new certificate request is made by the device. A certificate is also issued.  If you don't want to reissue a certificate to the device, remove all SCEP policy assignments.  

## View SCEP certificate profile report

Go to **Devices** > **Manage devices** > **Configuration**. Select the SCEP profile, and then select **Certificates**.

   > [!div class="mx-imgBorder"]
   > ![Image of the SCEP certifiate profile report in the admin center.](./media/microsoft-cloud-pki/scep-certificate-profile.png)
