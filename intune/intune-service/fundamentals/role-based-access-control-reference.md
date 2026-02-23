---
title: Microsoft Intune built-in roles reference
description: Permissions reference for built-in roles for Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 02/04/2026
ms.topic: reference

ms.collection:
- M365-identity-device-management
---

# Built-in role permissions for Microsoft Intune

The following tables list the built-in roles for Microsoft Intune. The tables also list the permissions that are associated with each role.

For a list of all available permission/actions combinations see [Custom role permissions](create-custom-role.md#custom-role-permissions) in *Create a custom role in Intune*.

> [!TIP]
> When your tenant includes a subscription to Windows 365 to support Cloud PCs, you might see additional Cloud PC roles in the Intune admin center. These roles aren't available by default and include permissions within Intune for tasks related to Cloud PCs. For more information about these roles, see [Cloud PC built-in roles](/windows-365/enterprise/role-based-access#cloud-pc-built-in-roles) in the Windows 365 documentation.

> [!TIP]
> For detailed descriptions of each permission and instructions for creating custom roles with specific permissions, see [Create a custom role in Intune](create-custom-role.md).

## Application Manager

Application Managers manage mobile and managed applications, can read device information and can view device configuration profiles.

| Permission | Action |
| ---------- | ------ |
| Admin tasks | Create |
| Admin tasks | Delete |
| Admin tasks | Read |
| Admin tasks | Update |
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
| Deployment Plans | Create |
| Deployment Plans | Delete |
| Deployment Plans | Read |
| Deployment Plans | Update |
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
| Admin tasks | Create |
| Admin tasks | Delete |
| Admin tasks | Read |
| Admin tasks | Update |
| Endpoint Privilege Management Elevation Requests | Modify elevation requests |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View Reports |
| Managed devices | Read |
| Organization | Read |

## Endpoint Privilege Reader

Endpoint Privilege Readers can view Endpoint Privilege Management (EPM) policies in the Intune console.

| Permission | Action |
| ---------- | ------ |
| Admin tasks | Read |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View Reports |
| Managed devices | Read |
| Organization | Read |

## Endpoint Security Manager

Manages security and compliance features such as security baselines, device compliance, conditional access, and Microsoft Defender ATP.

| Permission | Action |
| ---------- | ------ |
| Admin tasks | Create |
| Admin tasks | Delete |
| Admin tasks | Read |
| Admin tasks | Update |
| Android Enterprise | Read |
| Android FOTA | Read |
| App Control for Business | Assign |
| App Control for Business | Create |
| App Control for Business | Delete |
| App Control for Business | Read |
| App Control for Business | Update |
| App Control for Business | View Reports |
| Attack Surface Reduction | Assign |
| Attack Surface Reduction | Create |
| Attack Surface Reduction | Delete |
| Attack Surface Reduction | Read |
| Attack Surface Reduction | Update |
| Attack Surface Reduction | View Reports |
| Audit data | Read |
| Certificate Connector | Read |
| Cloud attached devices | Run CMPivot query |
| Cloud attached devices | View client details |
| Cloud attached devices | View collections |
| Cloud attached devices | View resource explorer |
| Cloud attached devices | View scripts |
| Cloud attached devices | View software updates |
| Cloud attached devices | View timeline |
| Corporate device identifiers | Read |
| Customization | Read |
| Deployment Plans | Create |
| Deployment Plans | Delete |
| Deployment Plans | Read |
| Deployment Plans | Update |
| Derived Credentials | Read |
| Device compliance policies | Assign |
| Device compliance policies | Create |
| Device compliance policies | Delete |
| Device compliance policies | Read |
| Device compliance policies | Update |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View Reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint Detection and Response | Assign |
| Endpoint Detection and Response | Create |
| Endpoint Detection and Response | Delete |
| Endpoint Detection and Response | Read |
| Endpoint Detection and Response | Update |
| Endpoint Detection and Response | View Reports |
| Endpoint Privilege Management Elevation Requests | Modify elevation requests |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Assign |
| Endpoint Privilege Management Policy Authoring | Create |
| Endpoint Privilege Management Policy Authoring | Delete |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | Update |
| Endpoint Privilege Management Policy Authoring | View Reports |
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
| Mobile apps | Read |
| Mobile Threat Defense | Modify |
| Mobile Threat Defense | Read |
| Organization | Read |
| Partner Device Management | Read |
| Policy Sets | Read |
| Remote assistance connectors | Read |
| Remote assistance connectors | View reports |
| Remote tasks | Get FileVault key. |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Reboot now |
| Remote tasks | Remote lock |
| Remote tasks | Rotate BitLockerKeys (preview) |
| Remote tasks | Rotate FileVault key. |
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
| Admin tasks | Read |
| Android Enterprise | Read |
| Android FOTA | Read |
| App Control for Business | Read |
| Attack Surface Reduction | Read |
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
| Deployment Plans | Read |
| Derived Credentials | Read |
| Device compliance policies | Read |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View Reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint Detection and Response | Read |
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
| Remote tasks | Change assignments |
| Remote tasks | Clean PC |
| Remote tasks | Collect diagnostics |
| Remote tasks | Disable lost mode |
| Remote tasks | Enable lost mode |
| Remote tasks | Enable Windows IntuneAgent |
| Remote tasks | Get FileVault key. |
| Remote tasks | Indicates remote device action to initiate Mobile Device Management (MDM) attestation if device is capable for it. |
| Remote tasks | Initiate Configuration Manager action |
| Remote tasks | Locate device |
| Remote tasks | Manage shared device users |
| Remote tasks | Offer remote assistance |
| Remote tasks | Play sound to locate lost devices |
| Remote tasks | Reboot now |
| Remote tasks | Recover MDM Key |
| Remote tasks | Remote lock |
| Remote tasks | Reset passcode |
| Remote tasks | Restore Managed Home Screen |
| Remote tasks | Retire |
| Remote tasks | Revoke App Licenses |
| Remote tasks | Rotate BitLockerKeys (preview) |
| Remote tasks | Rotate FileVault key. |
| Remote tasks | Run Remediation |
| Remote tasks | Send custom notifications |
| Remote tasks | Set device name |
| Remote tasks | Shut down |
| Remote tasks | Sync devices. |
| Remote tasks | Temporarily suspend Managed Home Screen |
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

Intune Role Administrators manage custom Intune roles and add assignments for built-in Intune roles. It is the only Intune role that can assign permissions to Administrators.

| Permission | Action |
| ---------- | ------ |
| Organization | Read |
| Roles | Assign |
| Roles | Create |
| Roles | Delete |
| Roles | Read |
| Roles | Update |

## Policy and Profile manager

Policy and Profile Managers manage compliance policy, configuration profiles, Apple enrollment, Android Enterprise enrollment profiles and corporate device identifiers.

| Permission | Action |
| ---------- | ------ |
| Admin tasks | Create |
| Admin tasks | Delete |
| Admin tasks | Read |
| Admin tasks | Update |
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
| Deployment Plans | Create |
| Deployment Plans | Delete |
| Deployment Plans | Read |
| Deployment Plans | Update |
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
| Device configurations | View Reports |
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
| Operating System Recovery Configurations | Assign Profiles |
| Operating System Recovery Configurations | Create Profiles |
| Operating System Recovery Configurations | Delete Profiles |
| Operating System Recovery Configurations | Read Profiles |
| Operating System Recovery Configurations | Update Profiles |
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
| Quiet Time policies | View Reports |

## Read Only Operator

Read Only Operators view user, device, enrollment, configuration and application information and cannot make changes to Intune.

| Permission | Action |
| ---------- | ------ |
| Admin tasks | Read |
| Android Enterprise | Read |
| Android FOTA | Read |
| App Control for Business | Read |
| Attack Surface Reduction | Read |
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
| Deployment Plans | Read |
| Derived Credentials | Read |
| Device compliance policies | Read |
| Device compliance policies | View reports |
| Device configurations | Read |
| Device configurations | View Reports |
| Device enrollment managers | Read |
| Endpoint Analytics | Read |
| Endpoint Detection and Response | Read |
| Endpoint Privilege Management Elevation Requests | View elevation requests |
| Endpoint Privilege Management Policy Authoring | Read |
| Endpoint Privilege Management Policy Authoring | View Reports |
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
| Quiet Time policies | View Reports |
| Remote assistance connectors | Read |
| Remote assistance connectors | View reports |
| Remote tasks | Get FileVault key. |
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
| Admin tasks | Create |
| Admin tasks | Delete |
| Admin tasks | Read |
| Admin tasks | Update |
| Audit data | Read |
| Certificate Connector | Modify |
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
| Customization | Assign |
| Customization | Create |
| Customization | Delete |
| Customization | Read |
| Customization | Update |
| Deployment Plans | Create |
| Deployment Plans | Delete |
| Deployment Plans | Read |
| Deployment Plans | Update |
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
| Remote tasks | Restore Managed Home Screen |
| Remote tasks | Retire |
| Remote tasks | Run Remediation |
| Remote tasks | Set device name |
| Remote tasks | Sync devices. |
| Remote tasks | Temporarily suspend Managed Home Screen |
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
