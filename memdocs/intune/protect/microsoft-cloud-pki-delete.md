---
title: Delete issued PKI certificates with Microsoft Intune
titleSuffix: Microsoft Intune 
description: Delete certificates issued via Microsoft Intune cloud PKI. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/29/2024
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
Delete an issuing CA and root CA from the Microsoft Cloud PKI service in Microsoft Intune. You can take the following actions in the Microsoft Intune admin center to delete a CA:    

1. Pause CA: Pause the CA to stop the initial use of it. 
2. Revoke CA: Revoke the CA and its active leaf certificates.   
3. Delete CA: Delete and remove the CA from Microsoft Intune.  

All actions are required. If you change your mind, you can resume use of a paused CA anytime and return to normal use. However, deleting or revoking a CA is permanent and can't be undone.    


## You should know 

|Microsoft Cloud PKI action| You should know|
| --- | --- |
|Pause| When you pause an issuing CA: <br> - It's can't issue leaf certificates. <br> - It continues to respond to certificate revocation list (CRL) requests and AIA requests.  |
| Revoke | When you revoke an issuing CA: <br> - It continues to respond to certificate revocation list (CRL) requests and AIA requests. <br> - It's no longer trusted to the relying parties performing a trust chain operation. <br> - The CRL of the root CA shows that the issuing CA cert has been revoked. <br> - All existing leaf certificates issued by the CA stop being authenticated.   |
| Delete| A root CA can't be deleted until all anchored issuing CAs are deleted.  | 


## Role based access control for deleting a CA  

The following roles can delete CAs:

- Intune Administrator, a built-in Microsoft Entra role  
- Custom Intune role assigned the following permissions: 
  - Read CAs  
  - Disable and reenable CAs  
  - Revoke issued leaf certificates  

## Delete issuing CA 
Permanently remove an issuing certificate from Microsoft Intune. 

> [!TIP]
> Want to delete a root CA? Complete these steps first to delete the issuing CA anchored to it. 

1. Go to **Tenant administration** > **Cloud PKI**.  
1. Select an active issuing CA from the list of available CAs. Selecting a CA opens its available actions. 
1. Choose **Pause**, and then select **Pause** again when prompted to confirm. 
1. Go back to your list of CAs and choose **Refresh**. Then look under the **Status** column to confirm that the issuing CA is paused. 
1. Select the paused CA to open all available options again. Two new options appear: 
   - **Resume**: This option unpauses the CA and makes it active again. 
   - **Revoke**: This option revokes the issuing CA certificate, and is required to eventually delete the CA.
1. Select **Revoke**, and then select **Revoke** again when prompted to confirm.  

    >[!IMPORTANT]
    > This action cannot be undone.

    Remember, for the revoke action to work, all active leaf certificates must first be revoked. For more information and steps, see [Revoke active leaf certificates](#revoke-active-leaf-certificates) in this article.    

1. Go back to your list of CAs and choose **Refresh**. Then look under the **Status** column to confirm that the issuing CA is revoked. 

1. Select the revoked CA to open all available options again. The delete option should be available now.  
1. Select **Delete** to remove the CA from Microsoft Intune. Then select **Delete** again when prompted to confirm.  

    >[!IMPORTANT]
    > This action cannot be undone.

1. Go back to your list of CAs and choose **Refresh**. Confirm that the issuing CA no longer appears in the list. 

## Delete root CA  
Permanently remove a root CA from Microsoft Intune.  

1. Go to **Tenant administration** > **Cloud PKI**.  
1. Select a root CA from the list of available CAs. Selecting a CA opens its available actions.    
1. Select **Delete** to remove the CA from Microsoft Intune. Then select **Delete** again when prompted to confirm.    
1. Go back to your list of CAs and choose **Refresh**. Confirm that the root CA no longer appears in the list. 

   > [!div class="mx-imgBorder"]
   > ![Image of the admin center, highlighting delete action for a root CA.](./media/microsoft-cloud-pki/.png)  

## Revoke active leaf certificates  

When trying to revoke an issuing CA, it's important to revoke all of its active leaf certificates first. You can revoke one leaf certificate at a time from an issuing CA, or you can bulk revoke leaf certificates.  

### Revoke a leaf certificate  

1. In the Microsoft Intune admin center, go to **Tenant administration** > **Cloud PKI**.  
1. Select an issuing CA. 
1. Choose **View all certificates**. 
1. Select an active leaf certificate, and then choose **Revoke**. Repeat this step until every active leaf certificate has been revoked. 

### Revoke all leaf certificates 

<!-- alternate if no repo
You can use the following Powershell script to revoke all leaf certificates belonging to a CA.  --->

You can use the RevokeAllLeafCerts.ps1 PowerShell script to remove all leaf certificates belonging to a CA.  

 >[!CAUTION]
 > Use this script with caution. You can't undo the revoke action for any of the leaf certificates.  

1. Download the **RevokeAllLeafCerts.ps1** PowerShell script from [download.microsoft.com]( https://aka.ms/intune_WDAC/CatCleanAll). 

2. Run this script on devices that have ---. 

For information about how to run PowerShell scripts on devices using Intune, see [Add PowerShell scripts to Windows 10/11 devices in Microsoft Intune](../apps/intune-management-extension.md).  


<!-- powershell script sample  -----------------------------------------------------

 ``powershell
 param (
	[string]$caId = $(Read-Host "Input CaId")
	)

Install-Module Microsoft.Graph

Connect-MgGraph -Scopes "DeviceManagementConfiguration.ReadWrite.All"

Start-Transcript -Path ".\RevokeAllLeafCerts_$($caId)_$(Get-Date -f 'yyyyMMdd-HHmmss').txt"

### Get all leaf certs
$leafCerts = Invoke-MgGraphRequest -Method GET -Uri "https://graph.microsoft.com/beta/devicemanagement/cloudCertificationAuthority/$caId/cloudCertificationAuthorityLeafCertificate"

# Prompt user to confirm data cleanup
$confirmAllDelete = $(Write-Host "Are you 100% sure you want to revoke all $($leafCerts.value.count) certificates for CA $($caId)?" -ForegroundColor Yellow; Write-Host '[Y] Yes' -NoNewline; Write-Host ' [N] No' -ForegroundColor Yellow -NoNewline;
Read-Host " ")

if ($confirmAllDelete.ToLower() -ne "y" -and $confirmAllDelete.ToLower() -ne "yes") {
	Write-Host "Aborted"
	Stop-Transcript
	exit
}

# Iterate on retrieved leaf certs and revoke
foreach ($leafCert in $leafCerts.value)
{
	Write-Host ""
	if ($leafCert.certificateStatus.ToLower() -eq "revoked") {
	 	Write-Host "LeafCert id: $($leafCert.id), thumbprint: $($leafCert.thumbprint) is already revoked. Skipping" 
	 	continue
	}
	
    Write-Host "Revoking leafCert id: $($leafCert.id), thumbprint: $($leafCert.thumbprint)" 
	
	# Uncomment next five lines to prompt for each cert
	# $confirmCertDelete = $(Write-Host "Are you sure you want to revoke leafCert id: $($leafCert.id), thumbprint: $($leafCert.thumbprint), $($leafCert.certificateStatus)?" -ForegroundColor Yellow; Write-Host '[Y] Yes' -NoNewline; Write-Host ' [N] No' -ForegroundColor Yellow -NoNewline; Read-Host " ")
	# if ($confirmCertDelete.ToLower() -ne "y" -and $confirmCertDelete.ToLower() -ne "yes") {
	# 	Write-Host "Skipping"
	# 	continue
	# }
	
	$currentCertId = $($leafCert.id)
	$revokeParams = @{ "leafCertificateId" = $($leafCert.id) }

	Invoke-MgGraphRequest -Method POST -Uri "https://graph.microsoft.com/beta/devicemanagement/cloudCertificationAuthority/$caId/revokeLeafCertificate" -Body ($revokeParams|ConvertTo-Json) -ContentType "application/json"
}

 ```powershell  ----------- >