---
# required metadata
title: Export Cloud PC names for Windows 365
titleSuffix:
description: Learn how to export Cloud PC names for Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/09/2021
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: naramkri
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Export Cloud PC names

You can export the Cloud PC name of every Cloud PC on your tenant.  

1. Sign in to a Cloud PC with a user who is assigned the Azure Active Directory (Azure AD) Global Administrator role.
2. Open PowerShell and type ```Install-Module Microsoft.Graph -Scope CurrentUser```.
3. Enter **Y** in all confirmation dialogs.
4. Wait for the installation to finish then close PowerShell.
5. Open a text editor like Visual Studio Code.
6. In a new file paste the following script:
```
param(
    [Parameter(Mandatory)]
    [string]$Output
)

Select-MgProfile -Name "beta"
Connect-MgGraph -Scopes "CloudPC.Read.All"
$CloudPCs = Get-MgDeviceManagementVirtualEndpointCloudPC -Property "DisplayName"
$DisplayNames = $CloudPCs | Select -ExpandProperty DisplayName
Write-Output $DisplayNames

$Outarray = @()

foreach ( $Name in $DisplayNames )
{
    $Outarray += New-Object PsObject -property @{
    'DisplayName' = $Name
     }
}
$Outarray | Export-Csv -Path $Output -NoTypeInformation
Disconnect-MgGraph
```

7. Save the file as “GetCloudPCNames.ps1” in a location of your choice.
8. In the file explorer, navigate to your file location.
9. Right-click on the file and select **Run with PowerShell**.
10. A PowerShell window will pop up. In the window, type “CloudPCNames.csv” and then press enter.
11. When the authentication Window pops up, sign in with the same account you used to access the Cloud PC.

When the PowerShell window closes, the script has finished running. Go back to the location of your script and there will be a file called “CloudPCNames.csv”. This file includes the list of all Cloud PC names on your tenant.
