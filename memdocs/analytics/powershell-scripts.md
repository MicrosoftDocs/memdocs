---
title: PowerShell scripts for Proactive remediations
titleSuffix: Microsoft Endpoint Manager
description: PowerShell script reference for Proactive remediations in Endpoint analytics.
ms.date: 10/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: reference
author: smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---

# PowerShell scripts for Proactive remediations

Use the following information to create script packages for [Proactive remediations](proactive-remediations.md).


## <a name="bkmk_scripts"></a> Script descriptions

This table shows the script names, descriptions, detections, remediations, and configurable items. Script files whose names start with `Detect` are detection scripts. Remediation scripts start with `Remediate`. These scripts can be copied from the next section in this article.

|Script name|Description|
|---|---|
|**Check network certificates** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Detects certificates issued by a CA in either the Machine's or User's personal store that are expired, or near expiry. </br> Specify the CA by changing the value for `$strMatch` in the detection script. Specify 0 for `$expiringDays` to find expired certificates, or specify another number of days to find certificates near expiry.  </br></br>Remediates by raising a toast notification to the user. </br> Specify the `$Title` and `$msgText` values with the message title and text you want users to see. </br> </br> Notifies users of expired certificates that might need to be renewed. </br> </br> **Run the script using the logged-on credentials**: Yes|
|**Clear stale certificates** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Detects expired certificates issued by a CA in the current user's personal store. </br> Specify the CA by changing the value for `$certCN` in the detection script. </br> </br> Remediates by deleting expired certificates issued by a CA from the current user's personal store. </br> Specify the CA by changing the value for `$certCN` in the remediation script. </br> </br> Finds and deletes expired certificates issued by a CA from the current user's personal store. </br> </br> **Run the script using the logged-on credentials**: Yes|
|**Update stale Group Policies** (built-in) </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Detects if last Group Policy refresh is greater than `7 days` ago.  </br>This script package is included with Proactive remediations, but a copy is provided if you want to change the threshold. Customize the seven day threshold by changing the value for `$numDays` in the detection script. </br></br>Remediates by running `gpupdate /target:computer /force` and `gpupdate /target:user /force`  </br> </br>Can help reduce network connectivity-related support calls when certificates and configurations are delivered via Group Policy. </br> </br> **Run the script using the logged-on credentials**: Yes|

## <a name="bkmk_ps_scripts"></a> Check network certificates script package

This script package detects certificates issued by a CA in either the Machine's or User's personal store that are expired, or near expiry. The script remediates by raising a toast notification to the user.

### Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

## Clear stale certificates script package

This script package detects expired certificates issued by a CA in the current user's personal store. The script remediates by deleting expired certificates issued by a CA from the current user's personal store.

### Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## Update stale Group Policies script package

This script package is included with Proactive remediations, but a copy is provided if you want to change the threshold.

This script package detects if last Group Policy refresh is greater than `7 days` ago. The script remediates by running `gpupdate /target:computer /force` and `gpupdate /target:user /force`.

### Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $lastGPUpdateDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables

try {
    $gpResult = [datetime]::FromFileTime(([Int64] ((Get-ItemProperty -Path "Registry::HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Group Policy\State\Machine\Extension-List\{00000000-0000-0000-0000-000000000000}").startTimeHi) -shl 32) -bor ((Get-ItemProperty -Path "Registry::HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Group Policy\State\Machine\Extension-List\{00000000-0000-0000-0000-000000000000}").startTimeLo))
    $lastGPUpdateDate = Get-Date ($gpResult[0])
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        
    if ($lastGPUpdateDays -gt 7){
        #Exit 1 for Intune. We want it to be within the last 7 days "Match" to remediate in SCCM
        Write-Host "Match"
        exit 1
    }
    else {
        #Exit 0 for Intune and "No_Match" for SCCM, only remediate "Match"
        Write-Host "No_Match"
        exit 0
    }
}
catch {
    $errMsg = $_.Exception.Message
    return $errMsg
    exit 1
}

```

### Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try {
    $compGPUpd = gpupdate /force
    $gpResult = [datetime]::FromFileTime(([Int64] ((Get-ItemProperty -Path "Registry::HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Group Policy\State\Machine\Extension-List\{00000000-0000-0000-0000-000000000000}").startTimeHi) -shl 32) -bor ((Get-ItemProperty -Path "Registry::HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Group Policy\State\Machine\Extension-List\{00000000-0000-0000-0000-000000000000}").startTimeLo))
    $lastGPUpdateDate = Get-Date ($gpResult[0])
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days

    if ($lastGPUpdateDays -eq 0){
        Write-Host "gpupdate completed successfully"
        exit 0
    }
    else{
        Write-Host "gpupdate failed"
        }
}
catch{
    $errMsg = $_.Exception.Message
    return $errMsg
    exit 1
}
```

## Next steps
 
For information about deploying script packages, see [Proactive remediations](proactive-remediations.md).