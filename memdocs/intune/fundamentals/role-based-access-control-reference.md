---
# required metadata

title: Microsoft Intune built-in roles reference
description: Permissions reference for built-in roles for Microsoft Intune. 
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 06/14/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Built-in role permissions for Microsoft Intune

The following tables lists the built-in roles for Microsoft Intune. The tables also list the permissions that are associated with each role.

> [!NOTE]
> This article was partially created with the help of artificial intelligence. Before publishing, an author reviewed and revised the content as needed. See [Our principles for using AI-generated content in Microsoft Learn](https://aka.ms/ai-content-principles).


<!-- 
# Save the below .ps1 file, which can be used to generate the markdown when permissions change or new roles are added
# ISE tends to popup the authentication better for Connect-MSGraph cmdlet

## Start of script
# Import the required modules
Install-Module Microsoft.Graph.Intune -ErrorAction SilentlyContinue
Import-Module Microsoft.Graph.Intune -ErrorAction SilentlyContinue

# Connect to Microsoft Graph
$GraphCredentials = Connect-MSGraph

# Retrieve the role definitions and permissions
$RoleDefinitions = Get-DeviceManagement_RoleDefinitions
$ResourceOperations = Get-DeviceManagement_ResourceOperations

# Create an array to store the role details
$Roles = @()

# Iterate through each role definition
foreach ($RoleDefinition in $RoleDefinitions) {
    $RoleName = $RoleDefinition.displayName
    $RoleDescription = $RoleDefinition.description

    # Create an array to store the permission details for the role
    $RolePermissions = @()

    # Retrieve the permissions for the role
    $Permissions = $RoleDefinition.RolePermissions.resourceActions.allowedResourceActions

    # Iterate through each permission
    foreach ($Permission in $Permissions) {
        # Find the corresponding resource operation
        $ResourceOperation = $ResourceOperations | Where-Object { $_.id -eq $Permission }

        # Retrieve the permission and action details
        $PermissionName = $ResourceOperation.resourceName
        $Action = $ResourceOperation.actionName

        # Create the permission object
        $PermissionObject = [PSCustomObject]@{
            Permission = $PermissionName
            Action = $Action
        }

        $RolePermissions += $PermissionObject
    }

    # Create the role object with permissions
    $RoleObject = [PSCustomObject]@{
        Role = $RoleName
        Description = $RoleDescription
        Permissions = $RolePermissions | Sort-Object Permission
    }

    $Roles += $RoleObject
}

# Create the markdown file
$MarkdownFilePath = "C:\Temp\IntuneRolePermissions.md"

# Generate the markdown content
$MarkdownContent = @"
# Intune Role Permissions

This document lists the roles and associated permissions in Microsoft Intune.

## Roles

"@

foreach ($Role in $Roles) {
    $RoleName = $Role.Role
    $RoleDescription = $Role.Description

    $MarkdownContent += "## $RoleName`n"
    $MarkdownContent += "$RoleDescription`n"

    $MarkdownContent += "| Permission | Action |`n"
    $MarkdownContent += "| ---------- | ------ |`n"

    foreach ($Permission in $Role.Permissions) {
        $PermissionName = $Permission.Permission
        $Action = $Permission.Action

        $MarkdownContent += "| $PermissionName | $Action |`n"
    }

    $MarkdownContent += "`n"
}

# Save the markdown content to the file
$MarkdownContent | Out-File -FilePath $MarkdownFilePath

Write-Host "Markdown file has been generated at: $MarkdownFilePath"

## End of script

 -->

## Application Manager

Application Managers manage mobile and managed applications, can read device information and can view device configuration profiles.

| Permission | Action |
| ---------- | ------ |
| Android for work | Read |
| Android for work | Update app sync |
| Filters | Create |
| Filters | Delete |
| Filters | Read |
| Filters | Update |
| Certificate Connector | Read |
| Cloud attached devices | Take application actions |
| Cloud attached devices | View applications |
| Cloud attached devices | View client details |
| Cloud attached devices | View collections |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Customization | Read |
| Derived Credentials | Read |
| Device configurations | Read |
| Managed apps | Assign |
| Managed apps | Create |
| Managed apps | Delete |
| Managed apps | Read |
| Managed apps | Update |
| Managed apps | Wipe |
| Managed devices | Read |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile apps | Assign |
| Mobile apps | Create |
| Mobile apps | Delete |
| Mobile apps | Read |
| Mobile apps | Relate |
| Mobile apps | Update |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Assign |
| Policy Sets | Create |
| Policy Sets | Delete |
| Policy Sets | Read |
| Policy Sets | Update |
| Windows Enterprise Certificate | Read |

## Endpoint Security Manager

Manages security and compliance features such as security baselines, device compliance, Conditional Access, and Microsoft Defender ATP.

| Permission | Action |
| ---------- | ------ |
| Android FOTA | Read |
| Android for work | Read |
| App Control for Business | Assign - *(Added with the 2406 service release)* |
| App Control for Business | Create - *(Added with the 2406 service release)* |
| App Control for Business | Delete - *(Added with the 2406 service release)* |
| App Control for Business | Read - *(Added with the 2406 service release)* |
| App Control for Business | Update - *(Added with the 2406 service release)* |
| App Control for Business | View reports - *(Added with the 2406 service release)* |
| Attack surface reduction | Assign - *(Added with the 2406 service release)* |
| Attack surface reduction | Create - *(Added with the 2406 service release)* |
| Attack surface reduction | Delete - *(Added with the 2406 service release)* |
| Attack surface reduction | Read - *(Added with the 2406 service release)* |
| Attack surface reduction | Update - *(Added with the 2406 service release)* |
| Attack surface reduction | View reports - *(Added with the 2406 service release)* |
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | View client details |
| Cloud attached devices | Run CMPivot query |
| Cloud attached devices | View collections |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Corporate device identifiers | Read |
| Customization | Read |
| Derived Credentials | Read |
| Device compliance policies | Assign |
| Device compliance policies | Create |
| Device compliance policies | Delete |
| Device compliance policies | Read |
| Device compliance policies | Update |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint protection reports | Read |
| Enrollment programs | Read token |
| Endpoint detection and response | Assign - *(Added with the 2406 service release)*|
| Endpoint detection and response | Create - *(Added with the 2406 service release)*|
| Endpoint detection and response | Delete - *(Added with the 2406 service release)*|
| Endpoint detection and response | Read - *(Added with the 2406 service release)*|
| Endpoint detection and response | Update - *(Added with the 2406 service release)*|
| Endpoint detection and response | View reports - *(Added with the 2406 service release)*|
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View reports |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Filters | Read |
| Intune data warehouse | Read |
| Managed apps | Read |
| Managed devices | Delete |
| Managed devices | Read |
| Managed devices | Set primary user |
| Managed devices | Update |
| Managed devices | View reports |
| Managed devices | Query |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile apps | Read |
| Mobile Threat Defense | Modify |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Read |
| Remote assistance connectors | Read |
| Remote assistance connectors | View reports |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Get filevault key. |
| Remote tasks | Reboot now |
| Remote tasks | Remote lock |
| Remote tasks | Rotate BitLockerKeys (preview) |
| Remote tasks | Rotate filevault key. |
| Remote tasks | Shut down |
| Remote tasks | Sync devices. |
| Remote tasks | Windows defender |
| Roles | Read |
| Security baselines | Assign |
| Security baselines | Create |
| Security baselines | Delete |
| Security baselines | Read |
| Security baselines | Update |
| Security baselines | View reports |
| Security tasks | Read |
| Security tasks | Update |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |

## Endpoint Privilege Manager

Endpoint Privilege Managers can manage Endpoint Privilege Management (EPM) policies in the Intune console.

| Permission | Action |
| ---------- | ------ |
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View reports |
| Organization | Read |

## Read Only Operator

Read Only Operators view user, device, enrollment, configuration and application information and cannot make changes to Intune.

| Permission | Action |
| ---------- | ------ |
| Android FOTA | Read |
| Android for work | Read |
| App Control for Business | Read - *(Added with the 2406 service release)*|
| Attack surface reduction | Read - *(Added with the 2406 service release)*|
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | View applications |
| Cloud attached devices | View client details |
| Cloud attached devices | View collections |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Corporate device identifiers | Read |
| Customization | Read |
| Derived Credentials | Read |
| Device compliance policies | Read |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint detection and response | Read - *(Added with the 2406 service release)* |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View reports |
| Endpoint protection reports | Read |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Filters | Read |
| Managed apps | Read |
| Managed devices | Read |
| Managed devices | View reports |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile apps | Read |
| Mobile Threat Defense | Read |
| Organization | Read |
| Organizational Messages | Read |
| Partner Device Management | Read |
| Policy Sets | Read |
| Quiet Time policies | Read |
| Quiet Time policies | View reports |
| Remote assistance connectors | Read |
| Remote assistance connectors | View reports |
| Remote tasks | Get filevault key. |
| Intune data warehouse | Read |
| Roles | Read |
| Security baselines | Read |
| ServiceNow | View Incidents |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |


## Organizational Messages Manager

Organizational Messages Managers can manage organizational messages in Intune console.

| Permission | Action |
| ---------- | ------ |
| Organization | Read |
| Organizational Messages | Assign |
| Organizational Messages | Create |
| Organizational Messages | Delete |
| Organizational Messages | Read |
| Organizational Messages | Update |
| Organizational Messages | Update organizational message control |


## School Administrator

School Administrators can manage apps and settings for their groups. They can take remote actions on devices, including remotely locking them, restarting them, and retiring them from management.

| Permission | Action |
| ---------- | ------ |
| Audit data | Read |
| Certificate Connector | Modify |
| Certificate Connector | Read |
| Cloud attached devices | Take application actions |
| Cloud attached devices | View applications |
| Cloud attached devices | View client details |
| Cloud attached devices | Run CMPivot query |
| Cloud attached devices | View collections |
| Cloud attached devices | Enroll Now |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | Run script |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Customization | Assign |
| Customization | Create |
| Customization | Delete |
| Customization | Read |
| Customization | Update |
| Derived Credentials | Read |
| Device configurations | Assign |
| Device configurations | Create |
| Device configurations | Delete |
| Device configurations | Read |
| Device configurations | Update |
| Device enrollment managers | Read |
| Device enrollment managers | Update |
| Endpoint Analytics | Create |
| Endpoint Analytics | Delete |
| Endpoint Analytics | Read |
| Endpoint Analytics | Update |
| Enrollment programs | Assign profile |
| Enrollment programs | Create profile |
| Enrollment programs | Delete device |
| Enrollment programs | Delete profile |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Sync device |
| Enrollment programs | Update profile |
| Filters | Create |
| Filters | Delete |
| Filters | Read |
| Filters | Update |
| Enrollment programs | Create token |
| Enrollment programs | Delete token |
| Enrollment programs | Read token |
| Enrollment programs | Update token |
| Managed apps | Create |
| Managed apps | Delete |
| Managed apps | Read |
| Managed apps | Update |
| Managed devices | Delete |
| Managed devices | Read |
| Managed devices | Set primary user |
| Managed devices | Update |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Modify |
| Microsoft Store For Business | Read |
| Mobile apps | Assign |
| Mobile apps | Create |
| Mobile apps | Delete |
| Mobile apps | Read |
| Mobile apps | Relate |
| Mobile apps | Update |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Assign |
| Policy Sets | Create |
| Policy Sets | Delete |
| Policy Sets | Read |
| Policy Sets | Update |
| Remote assistance connectors | Read |
| Remote assistance connectors | Update |
| Remote assistance connectors | View reports |
| Remote Help app | Elevation |
| Remote Help app | Take full control |
| Remote Help app | View screen |
| Remote tasks | Update cellular data plan |
| Remote tasks | Clean PC |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Collect diagnostics |
| Remote tasks | Disable lost mode |
| Remote tasks | Enable lost mode |
| Remote tasks | Recover MDM Key |
| Remote tasks | Locate device |
| Remote tasks | Run Remediation |
| Remote tasks | Play sound to locate lost devices |
| Remote tasks | Reboot now |
| Remote tasks | Remote lock |
| Remote tasks | Offer remote assistance |
| Remote tasks | Reset passcode |
| Remote tasks | Retire |
| Remote tasks | Set device name |
| Remote tasks | Sync devices. |
| Remote tasks | Wipe |
| Intune data warehouse | Read |
| ServiceNow | View Incidents |
| Terms and conditions | Assign |
| Terms and conditions | Create |
| Terms and conditions | Delete |
| Terms and conditions | Read |
| Terms and conditions | Update |
| Windows Enterprise Certificate | Modify |
| Windows Enterprise Certificate | Read |


## Policy and Profile manager

Policy and Profile Managers manage compliance policy, configuration profiles, Apple enrollment and corporate device identifiers.

| Permission | Action |
| ---------- | ------ |
| Android FOTA | Read |
| Android for work | Read |
| Android for work | Update app sync |
| Android for work | Update onboarding |
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | View applications |
| Cloud attached devices | View client details |
| Cloud attached devices | View collections |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Corporate device identifiers | Create |
| Corporate device identifiers | Delete |
| Corporate device identifiers | Read |
| Corporate device identifiers | Update |
| Derived Credentials | Read |
| Device compliance policies | Assign |
| Device compliance policies | Create |
| Device compliance policies | Delete |
| Device compliance policies | Read |
| Device compliance policies | Update |
| Device compliance policies | View reports |
| Device configurations | Assign |
| Device configurations | Create |
| Device configurations | Delete |
| Device configurations | Read |
| Device configurations | Update |
| Device configurations | View reports |
| Enrollment programs | Assign profile |
| Enrollment programs | Create device |
| Enrollment programs | Create token |
| Enrollment programs | Create profile |
| Enrollment programs | Delete device |
| Enrollment programs | Delete profile |
| Enrollment programs | Delete token |
| Enrollment programs | Read device |
| Enrollment programs | Read token |
| Enrollment programs | Read profile |
| Enrollment programs | Sync device |
| Enrollment programs | Update token |
| Enrollment programs | Update profile 
| Filters | Create |
| Filters | Delete |
| Filters | Read |
| Filters | Update |
| Managed apps | Assign |
| Managed apps | Create |
| Managed apps | Delete |
| Managed apps | Read |
| Managed apps | Update |
| Microsoft Defender ATP | Read |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Assign |
| Policy Sets | Create |
| Policy Sets | Delete |
| Policy Sets | Read |
| Policy Sets | Update |
| Quiet Time policies | Assign |
| Quiet Time policies | Create |
| Quiet Time policies | Delete |
| Quiet Time policies | Read |
| Quiet Time policies | Update |
| Quiet Time policies | View reports |

## Help Desk Operator

Help Desk Operators perform remote tasks on users and devices and can assign applications or policies to users or devices.

| Permission | Action |
| ---------- | ------ |
| Android FOTA | Read |
| Android for work | Read |
| App Control for Business | Read - *(Added with the 2406 service release)* |
| Attack surface reduction | Read - *(Added with the 2406 service release)* |
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | Take application actions |
| Cloud attached devices | View applications |
| Cloud attached devices | View client details |
| Cloud attached devices | Run CMPivot query |
| Cloud attached devices | View collections |
| Cloud attached devices | Enroll Now |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | Run script |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Corporate device identifiers | Read |
| Customization | Read |
| Derived Credentials | Read |
| Device compliance policies | Read |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint detection and response | Read - *(Added with the 2406 service release)* |
| Endpoint protection reports | Read |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Filters | Read |
| Managed apps | Assign |
| Managed apps | Read |
| Managed apps | Wipe |
| Managed devices | Read |
| Managed devices | Set primary user |
| Managed devices | Update |
| Managed devices | View reports |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile apps | Assign |
| Mobile apps | Read |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Read |
| Remote assistance connectors | Read |
| Remote Help app | Elevation |
| Remote Help app | Take full control |
| Remote Help app | View screen |
| Remote tasks | Update cellular data plan |
| Remote tasks | Clean PC |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Send custom notifications |
| Remote tasks | Collect diagnostics |
| Remote tasks | Disable lost mode |
| Remote tasks | Enable lost mode |
| Remote tasks | Enable Windows IntuneAgent |
| Remote tasks | Get filevault key. |
| Remote tasks | Recover MDM Key |
| Remote tasks | Locate device |
| Remote tasks | Manage shared device users |
| Remote tasks | Run Remediation |
| Remote tasks | Play sound to locate lost devices |
| Remote tasks | Reboot now |
| Remote tasks | Remote lock |
| Remote tasks | Offer remote assistance |
| Remote tasks | Reset passcode |
| Remote tasks | Retire |
| Remote tasks | Revoke App Licenses |
| Remote tasks | Rotate BitLockerKeys (preview) |
| Remote tasks | Rotate filevault key. |
| Remote tasks | Set device name |
| Remote tasks | Shut down |
| Remote tasks | Sync devices. |
| Remote tasks | Update device account |
| Remote tasks | Windows defender |
| Remote tasks | Wipe |
| Roles | Read |
| Security baselines | Read |
| ServiceNow | View Incidents |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |


## Endpoint Privilege Reader

Organizational Messages Readers can view Endpoint Privilege Management (EPM) policies in the Intune console.

| Permission | Action |
| ---------- | ------ |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View reports |
| Organization | Read |


## Intune Role Administrator

Intune Role Administrators manage custom Intune roles and add assignments for built-in Intune roles. It is the only Intune role that can assign permissions to Administrators.

| Permission | Action |
| ---------- | ------ |
| Organization | Read |
| Roles | Assign |
| Roles | Create |
| Roles | Delete |
| Roles | Read |
| Roles | Update |

 
