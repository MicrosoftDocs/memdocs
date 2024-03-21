---
# required metadata
title: Configure single sign-on for Windows 365 Business
titleSuffix:
description: How to configure single sign-on for Windows 365 Business
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/21/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidbel
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Configure single sign-on for Windows 365 Business using Microsoft Entra authentication

This article explains the process of configuring single sign-on (SSO) for Windows 365 by using Microsoft Entra authentication. When you enable SSO, users can use passwordless authentication and third-party Identity Providers that federate with Microsoft Entra ID to sign in to their Cloud PC. When enabled, this feature provides a SSO experience both when authenticating to the Cloud PC and inside the session when accessing Microsoft Entra ID-based apps and websites.

To enable SSO using Microsoft Entra ID authentication, there are four tasks you must complete:

1. [Enable Microsoft Entra authentication for Remote Desktop Protocol (RDP)](#enable-microsoft-entra-authentication-for-rdp).

1. Configure the target device groups.

1. Review your conditional access policies.

1. Configure your organizational settings to enable single sign-on.

## Before enabling single sign-on

Before you enable single sign-on, review the following information for using it in your environment.

### Disconnection when the session is locked

When single sign-on is enabled, users sign in to Windows using a Microsoft Entra ID authentication token, which provides support for passwordless authentication to Windows. The Windows lock screen in the remote session doesn't support Microsoft Entra ID authentication tokens or passwordless authentication methods, like FIDO keys, which means:

- Users can't unlock their screens in a remote session.
- When someone tries to lock a remote session, either through user action or system policy, the session is instead disconnected and the service sends a message to the user explaining they were disconnected.

Disconnecting the session also ensures that when the connection is relaunched after a period of inactivity, Microsoft Entra ID reevaluates any applicable conditional access policies.

## Prerequisites

Before you can enable single sign-on, you must meet the following prerequisites:

- To configure your Microsoft Entra tenant, you must be assigned one of the following [Microsoft Entra built-in roles](/entra/identity/role-based-access-control/manage-roles-portal):
  - [Application Administrator](/entra/identity/role-based-access-control/permissions-reference#application-administrator)
  - [Cloud Application Administrator](/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
  - [Global Administrator](/entra/identity/role-based-access-control/permissions-reference#global-administrator)

- The Cloud PCs must be running one of the following operating systems with the relevant cumulative update installed:
  - Windows 11 Enterprise with the [2022-10 Cumulative Updates for Windows 11 (KB5018418)](https://support.microsoft.com/kb/KB5018418) or later installed.
  - Windows 10 Enterprise with the [2022-10 Cumulative Updates for Windows 10 (KB5018410)](https://support.microsoft.com/kb/KB5018410) or later installed.

- [Install the Microsoft Graph PowerShell SDK](/powershell/microsoftgraph/installation) version 2.9.0 or later on your local device or in [Azure Cloud Shell](/azure/cloud-shell/overview).

## Enable Microsoft Entra authentication for RDP

You must first allow Microsoft Entra authentication for Windows in your Microsoft Entra tenant, which enables issuing RDP access tokens allowing users to sign in to their Cloud PCs. You must set the `isRemoteDesktopProtocolEnabled` property to true on the service principal's `remoteDesktopSecurityConfiguration` object for the following Microsoft Entra applications:

| Application Name | Application ID |
|--|--|
| Microsoft Remote Desktop | a4a365df-50f1-4397-bc59-1a1564b8bb9c |
| Windows Cloud Login | 270efc09-cd0d-444b-a71f-39af4910ec45 |

> [!IMPORTANT]
> As part of an upcoming change, we're transitioning from Microsoft Remote Desktop to Windows Cloud Login, beginning in 2024. Configuring both applications now ensures you're ready for the change.

To configure the service principal, use the [Microsoft Graph PowerShell SDK](/powershell/microsoftgraph/overview) to create a new [remoteDesktopSecurityConfiguration object](/graph/api/serviceprincipal-post-remotedesktopsecurityconfiguration) on the service principal and set the property `isRemoteDesktopProtocolEnabled` to `true`. You can also use the [Microsoft Graph API](/graph/use-the-api) with a tool such as [Graph Explorer](/graph/use-the-api#graph-explorer).

1. Launch the Azure Cloud Shell in the Azure portal with the PowerShell terminal type, or run PowerShell on your local device.

    1. If you're using Cloud Shell, make sure your Azure context is set to the subscription you want to use.

    1. If you're using PowerShell locally, first Sign in with Azure PowerShell, then make sure your Azure context is set to the subscription you want to use.

1. Make sure you installed the [Microsoft Graph PowerShell SDK](/powershell/microsoftgraph/installation) from the [prerequisites](#prerequisites). Then, import the *Authentication* and *Applications* Microsoft Graph modules and connect to Microsoft Graph with the `Application.Read.All` and `Application-RemoteDesktopConfig.ReadWrite.All` scopes by running the following commands:

   ```powershell
   Import-Module Microsoft.Graph.Authentication
   Import-Module Microsoft.Graph.Applications

   Connect-MgGraph -Scopes "Application.Read.All","Application-RemoteDesktopConfig.ReadWrite.All"
   ```

1. Get the object ID for each service principal and store them in variables by running the following commands:

   ```powershell
   $MSRDspId = (Get-MgServicePrincipal -Filter "AppId eq 'a4a365df-50f1-4397-bc59-1a1564b8bb9c'").Id
   $WCLspId = (Get-MgServicePrincipal -Filter "AppId eq '270efc09-cd0d-444b-a71f-39af4910ec45'").Id
   ```

1. Set the property `isRemoteDesktopProtocolEnabled` to `true` by running the following commands. There's no output from these commands.

   ```powershell
   If ((Get-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $MSRDspId) -ne $true) {
       Update-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $MSRDspId -IsRemoteDesktopProtocolEnabled
   }

   If ((Get-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $WCLspId) -ne $true) {
       Update-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $WCLspId -IsRemoteDesktopProtocolEnabled
   }
   ```

1. Confirm the property `isRemoteDesktopProtocolEnabled` is set to `true` by running the following commands:

   ```powershell
   Get-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $MSRDspId
   Get-MgServicePrincipalRemoteDesktopSecurityConfiguration -ServicePrincipalId $WCLspId
   ```

   The output should be:

   ```output
   Id IsRemoteDesktopProtocolEnabled
   -- ------------------------------
   id True
   ```

## Configure the target device groups

After you enable Microsoft Entra authentication for RDP, you must configure the target device groups. By default when enabling single sign-on, users are prompted to authenticate to Microsoft Entra ID and allow the Remote Desktop connection when launching a connection to a new session host. Microsoft Entra remembers up to 15 hosts for 30 days before prompting again. If you see a dialogue to allow the Remote Desktop connection, select **Yes** to connect.

You can hide this dialog and provide single sign-on for connections to all your session hosts by configuring a list of trusted devices. You need to create one or more groups in Microsoft Entra ID that contains your session hosts, then set a property on the service principals for the same *Microsoft Remote Desktop* and *Windows Cloud Login* applications, as used in the previous section, for the group.

> [!TIP]
> We recommend you use a dynamic group and configure the dynamic membership rules to includes all your Cloud PCs. You can use the device names in this group, but for a more secure option, you can set and use [device extension attributes](/graph/extensibility-overview) using [Microsoft Graph API](/graph/api/resources/device). While dynamic groups normally update within 5-10 minutes, large tenants can take up to 24 hours.
>
> Dynamic groups requires the Microsoft Entra ID P1 license or Intune for Education license. For more information, see [Dynamic membership rules for groups](/entra/identity/users/groups-dynamic-membership).

To configure the service principal, use the [Microsoft Graph PowerShell SDK](/powershell/microsoftgraph/overview) to create a new [targetDeviceGroup object](/graph/api/remotedesktopsecurityconfiguration-post-targetdevicegroups) on the service principal with the dynamic group's object ID and display name. You can also use the [Microsoft Graph API](/graph/use-the-api) with a tool such as [Graph Explorer](/graph/use-the-api#graph-explorer).

1. [Create a dynamic group](/entra/identity/users/groups-create-rule) in Microsoft Entra ID containing the Cloud PCs for which you want to hide the dialog. Make a note of the object ID of the group for the next step.

1. In the same PowerShell session, create a `targetDeviceGroup` object by running the following commands, replacing the `<placeholders>` with your own values:

   ```powershell
   $tdg = New-Object -TypeName Microsoft.Graph.PowerShell.Models.MicrosoftGraphTargetDeviceGroup
   $tdg.Id = "<Group object ID>"
   $tdg.DisplayName = "<Group display name>"
   ```

1. Add the group to the `targetDeviceGroup` object by running the following commands:

   ```powershell
   New-MgServicePrincipalRemoteDesktopSecurityConfigurationTargetDeviceGroup -ServicePrincipalId $MSRDspId -BodyParameter $tdg
   New-MgServicePrincipalRemoteDesktopSecurityConfigurationTargetDeviceGroup -ServicePrincipalId $WCLspId -BodyParameter $tdg
   ```

   The output should be similar:

   ```output
   Id                                   DisplayName
   --                                   -----------
   12345678-abcd-1234-abcd-1234567890ab Contoso-session-hosts
   ```

   Repeat steps 2 and 3 for each group you want to add to the `targetDeviceGroup` object, up to a maximum of 10 groups.

1. If you later need to remove a device group from the `targetDeviceGroup` object, run the following commands, replacing the `<placeholders>` with your own values:

   ```powershell
   Remove-MgServicePrincipalRemoteDesktopSecurityConfigurationTargetDeviceGroup -ServicePrincipalId $MSRDspId -TargetDeviceGroupId "<Group object ID>"
   Remove-MgServicePrincipalRemoteDesktopSecurityConfigurationTargetDeviceGroup -ServicePrincipalId $WCLspId -TargetDeviceGroupId "<Group object ID>"
   ```

## Review your conditional access policies

When single sign-on is enabled, a new Microsoft Entra ID app is introduced to authenticate users to the session host. If you have conditional access policies that apply when accessing Windows 365, review the recommendations to [set conditional access policies](set-conditional-access-policies.md) for Windows 365 to ensure users have the desired experience and to secure your environment.

## Configure your organizational settings to enable single sign-on

SSO can be enabled using the **Single sign-on** option under the **Cloud PC settings** group in your [organizational settings](change-organization-default-settings.md). When enabled, the setting applies to all your Cloud PCs.
