---
title: Microsoft Intune built-in roles reference
description: Permissions reference for built-in roles for Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 06/14/2025
ms.topic: reference

ms.collection:
- M365-identity-device-management
---

# Built-in role permissions for Microsoft Intune

The following tables list the built-in roles for Microsoft Intune. The tables also list the permissions that are associated with each role.

For a list of all available permission/actions combinations see [Custom role permissions](create-custom-role.md#custom-role-permissions) in *Create a custom role in Intune*.

> [!TIP]
> When your tenant includes a subscription to Windows 365 to support Cloud PCs, you'll also find the following Cloud PC roles in the Intune admin center. These roles aren't available by default and include permissions within Intune for tasks related to Cloud PCs. For more information about these roles, see [Cloud PC built-in roles](/windows-365/enterprise/role-based-access#cloud-pc-built-in-roles) in the Windows 365 documentation.


> [!TIP]
> For detailed descriptions of each permission and instructions for creating custom roles with specific permissions, see [Create a custom role in Intune](create-custom-role.md).

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
| Android Enterprise | Read |
| Android Enterprise | Update app sync |
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
| Filters | Create |
| Filters | Delete |
| Filters | Read |
| Filters | Update |
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

## Endpoint Privilege Manager

Endpoint Privilege Managers can manage Endpoint Privilege Management (EPM) policies in the Intune console.

| Permission | Action |
| ---------- | ------ |
| Endpoint Privilege Management Elevation Requests | Modify elevation requests |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View reports |
| Managed devices | Read |
| Organization | Read |


## Endpoint Privilege Reader

Organizational Messages Readers can view Endpoint Privilege Management (EPM) policies in the Intune console.

| Permission | Action |
| ---------- | ------ |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View reports |
| Managed devices | Read |
| Organization | Read |

## Endpoint Security Manager

Manages security and compliance features such as security baselines, device compliance, Conditional Access, and Microsoft Defender ATP.

| Permission | Action |
| ---------- | ------ |
| Android Enterprise | Read |
| Android FOTA | Read |
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
| Endpoint Detection and Response | Assign - *(Added with the 2406 service release)*|
| Endpoint Detection and Response | Create - *(Added with the 2406 service release)*|
| Endpoint Detection and Response | Delete - *(Added with the 2406 service release)*|
| Endpoint Detection and Response | Read - *(Added with the 2406 service release)*|
| Endpoint Detection and Response | Update - *(Added with the 2406 service release)*|
| Endpoint Detection and Response | View reports - *(Added with the 2406 service release)*|
| Endpoint Privilege Management Elevation Requests | Modify elevation requests |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View reports |
| Endpoint protection reports | Read |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Filters | Read |
| Intune data warehouse | Read |
| Managed apps | Read |
| Managed devices | Delete |
| Managed devices | Read |
| Managed devices | Set primary user |
| Managed devices | Update |
| Managed devices | View reports |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile Threat Defense | Modify |
| Mobile Threat Defense | Read |
| Mobile apps | Read |
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
| Security tasks | Read |
| Security tasks | Update |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |

## Help Desk Operator

Help Desk Operators perform remote tasks on users and devices and can assign applications or policies to users or devices.

| Permission | Action |
| ---------- | ------ |
| Android Enterprise | Read |
| Android FOTA | Read |
| App Control for Business | Read - *(Added with the 2406 service release)* |
| Attack surface reduction | Read - *(Added with the 2406 service release)* |
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | Enroll Now |
| Cloud attached devices | Run CMPivot query |
| Cloud attached devices | Run script |
| Cloud attached devices | Take application actions |
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
| Remote Help app | Unattended control |
| Remote Help app | View screen |
| Remote tasks | Change \assignments |
| Remote tasks | Clean PC |
| Remote tasks | Collect diagnostics |
| Remote tasks | Disable lost mode |
| Remote tasks | Enable lost mode |
| Remote tasks | Indicates remote device action to initiate Mobile Device Management (MDM) attestation if device is capable for it. |
| Remote tasks | Enable Windows IntuneAgent |
| Remote tasks | Get filevault key. |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Locate device |
| Remote tasks | Manage shared device users |
| Remote tasks | Offer remote assistance |
| Remote tasks | Play sound to locate lost devices |
| Remote tasks | Reboot now |
| Remote tasks | Recover MDM Key |
| Remote tasks | Remote lock |
| Remote tasks | Reset passcode |
| Remote tasks | Retire |
| Remote tasks | Revoke App Licenses |
| Remote tasks | Rotate BitLockerKeys (preview) |
| Remote tasks | Rotate filevault key. |
| Remote tasks | Run Remediation |
| Remote tasks | Send custom notifications |
| Remote tasks | Set device name |
| Remote tasks | Shut down |
| Remote tasks | Sync devices. |
| Remote tasks | Update cellular data plan |
| Remote tasks | Update device account |
| Remote tasks | Windows defender |
| Remote tasks | Wipe |
| Roles | Read |
| Security baselines | Read |
| ServiceNow | View Incidents |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |

## Intune Role Administrator

Intune Role Administrators manage custom Intune roles and add assignments for built-in Intune roles. It's the only Intune role that can assign permissions to Administrators.

| Permission | Action |
| ---------- | ------ |
| Organization | Read |
| Roles | Assign |
| Roles | Create |
| Roles | Delete |
| Roles | Read |
| Roles | Update |


## Policy and Profile manager

Policy and Profile Managers manage compliance policy, configuration profiles, Apple enrollment, and corporate device identifiers.

| Permission | Action |
| ---------- | ------ |
| Android Enterprise | Read |
| Android Enterprise | Update app sync |
| Android Enterprise | Update enrollment profiles |
| Android Enterprise | Update onboarding |
| Android FOTA | Read |
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
| Enrollment programs | Create profile |
| Enrollment programs | Create token |
| Enrollment programs | Delete device |
| Enrollment programs | Delete profile |
| Enrollment programs | Delete token |
| Enrollment programs | Enrollment time device membership assignment |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Enrollment programs | Sync device |
| Enrollment programs | Update profile |
| Enrollment programs | Update token |
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
| Operating System Recovery Configurations| Assign Profiles |
| Operating System Recovery Configurations| Create Profiles |
| Operating System Recovery Configurations| Delete  Profiles |
| Operating System Recovery Configurations| Read Profiles |
| Operating System Recovery Configurations| Update Profiles |
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

## Read Only Operator

Read Only Operators view user, device, enrollment, configuration, application information, and can't make changes to Intune.

| Permission | Action |
| ---------- | ------ |
| Android Enterprise | Read |
| Android FOTA | Read |
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
| Endpoint Detection and Response | Read - *(Added with the 2406 service release)* |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View reports |
| Endpoint protection reports | Read |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Filters | Read |
| Intune data warehouse | Read |
| Managed apps | Read |
| Managed devices | Read |
| Managed devices | View reports |
| Microsoft Defender ATP | Read |
| Microsoft Store For Business | Read |
| Mobile apps | Read |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Read |
| Quiet Time policies | Read |
| Quiet Time policies | View reports |
| Remote assistance connectors | Read |
| Remote assistance connectors | View reports |
| Remote tasks | Get filevault key. |
| Roles | Read |
| Security baselines | Read |
| ServiceNow | View Incidents |
| Telecom expenses | Read |
| Terms and conditions | Read |
| Windows Enterprise Certificate | Read |

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
| Enrollment programs | Create token |
| Enrollment programs | Delete device |
| Enrollment programs | Delete profile |
| Enrollment programs | Delete token |
| Enrollment programs | Enrollment time device membership assignment |
| Enrollment programs | Read device |
| Enrollment programs | Read profile |
| Enrollment programs | Read token |
| Enrollment programs | Sync device |
| Enrollment programs | Update profile |
| Enrollment programs | Update token |
| Filters | Create |
| Filters | Delete |
| Filters | Read |
| Filters | Update |
| Intune data warehouse | Read |
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
| Remote tasks | Change assignments |
| Remote tasks | Clean PC |
| Remote tasks | Collect diagnostics |
| Remote tasks | Disable lost mode |
| Remote tasks | Enable lost mode |
| Remote tasks | Indicates remote device action to initiate Mobile Device Management (MDM) attestation if device is capable for it. |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Locate device |
| Remote tasks | Offer remote assistance |
| Remote tasks | Play sound to locate lost devices |
| Remote tasks | Reboot now |
| Remote tasks | Recover MDM Key |
| Remote tasks | Remote lock |
| Remote tasks | Reset passcode |
| Remote tasks | Retire |
| Remote tasks | Run Remediation
| Remote tasks | Set device name |
| Remote tasks | Sync devices. |
| Remote tasks | Update cellular data plan |
| Remote tasks | Wipe |
| ServiceNow | View Incidents |
| Terms and conditions | Assign |
| Terms and conditions | Create |
| Terms and conditions | Delete |
| Terms and conditions | Read |
| Terms and conditions | Update |
| Windows Enterprise Certificate | Modify |
| Windows Enterprise Certificate | Read |
