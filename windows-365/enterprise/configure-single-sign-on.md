---
# required metadata
title: Configure single sign-on for Windows 365
titleSuffix:
description: How to configure single sign-on for Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/10/2023
ms.topic: overview
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

# Configure single sign-on for Windows 365 using Microsoft Entra authentication

>[!Important]
>Single sign-on is in [public preview](../public-preview.md) for Microsoft Entra joined and Microsoft Entra hybrid joined Cloud PCs.

This article walks you through the process of configuring single sign-on (SSO) using Microsoft Entra authentication for Windows 365. When you enable SSO, you can use passwordless authentication and third-party Identity Providers that federate with Microsoft Entra ID to sign in to your Cloud PC. When enabled, this feature provides a single sign-on experience both when authenticating to the Cloud PC and inside the session when accessing Microsoft Entra ID-based apps and websites.

For information on using passwordless authentication within the session, see [In-session passwordless authentication (Preview)](identity-authentication.md#in-session-passwordless-authentication-preview).

## Prerequisites

Single sign-on is available on Cloud PCs using the following operating systems:

- Windows 11 Enterprise with the [2022-10 Cumulative Updates for Windows 11 (KB5018418)](https://support.microsoft.com/kb/KB5018418) or later installed.
- Windows 10 Enterprise, versions 20H2 or later with the [2022-10 Cumulative Updates for Windows 10 (KB5018410)](https://support.microsoft.com/kb/KB5018410) or later installed.

Cloud PCs must be Microsoft Entra joined or [Microsoft Entra hybrid joined](/entra/identity/devices/hybrid-join-plan).

## Things to know before enabling single sign-on

Before enabling single sign-on, review the following information for using SSO in your environment.

### Disconnection when the session is locked

When SSO is enabled, you sign in to Windows using a Microsoft Entra authentication token, which provides support for passwordless authentication to Windows. The Windows lock screen in the remote session doesn't support Microsoft Entra authentication tokens or passwordless authentication methods like FIDO keys. The lack of support for these authentication methods means that passwordless users can't unlock their screens in a remote session. When you try to lock a remote session, either through user action or system policy, the session is instead disconnected and the service sends a message to the user explaining they've been disconnected.

Disconnecting the session also ensures that when the connection is relaunched after a period of inactivity, Microsoft Entra ID reevaluates the applicable conditional access policies.

### Using an Active Directory domain admin account with single sign-on

In environments with an Active Directory (AD) and hybrid user accounts, the default Password Replication Policy on Read-only Domain Controllers denies password replication for members of Domain Admins and Administrators security groups. This will prevent these admin accounts from signing in to Microsoft Entra hybrid joined hosts and might keep prompting them to enter their credentials. It will also prevent admin accounts from accessing on-premises resources that leverage Kerberos authentication from Microsoft Entra joined hosts.

To allow these admin accounts to connect when single sign-on is enabled:

1. On a device that you use to manage your Active Directory domain, open the **Active Directory Users and Computers** console.
1. Open the **Domain Controllers** folder for your tenant.
1. Find the **AzureADKerberos** object, then right-click it and select **Properties**.
1. Select the **Password Replication Policy** tab.
1. Change the policy for **Domain Admins** from *Deny* to *Allow*.
1. Delete the policy for **Administrators**. The Domain Admins group is a member of the Administrators group, so denying replication for administrators also denies it for domain admins.
1. Select **OK** to save your changes.

## Enable single sign-on

To enable single sign-on in your environment, you must:

1. Enable Microsoft Entra authentication for Remote Desktop Protocol (RDP).
1. Configure the target device groups.
1. Create a Kerberos Server object.
1. Review your conditional access policies.
1. Configure your provisioning policy to enable single sign-on.

### Enable Microsoft Entra authentication for RDP

> [!IMPORTANT]
> Due to an upcoming change, the steps below should be completed for the following Microsoft Entra Apps:
>
> - Microsoft Remote Desktop (App ID a4a365df-50f1-4397-bc59-1a1564b8bb9c).
> - Windows Cloud Login (App ID 270efc09-cd0d-444b-a71f-39af4910ec45)

Before enabling the single sign-on feature, you must first allow Microsoft Entra authentication for Windows in your Microsoft Entra tenant. This will enable issuing RDP access tokens, allowing users to sign in to Cloud PCs. This is done by enabling the isRemoteDesktopProtocolEnabled property on the service principal's remoteDesktopSecurityConfiguration object for the apps listed above.

Use the [Microsoft Graph API](/graph/use-the-api) to [create remoteDesktopSecurityConfiguration](/graph/api/serviceprincipal-post-remotedesktopsecurityconfiguration) and set the property **isRemoteDesktopProtocolEnabled** to **true** to enable Microsoft Entra authentication.

### Configure the target device groups

> [!IMPORTANT]
> Due to an upcoming change, the steps below should be completed for the following Microsoft Entra Apps:
>
> - Microsoft Remote Desktop (App ID a4a365df-50f1-4397-bc59-1a1564b8bb9c).
> - Windows Cloud Login (App ID 270efc09-cd0d-444b-a71f-39af4910ec45)

By default when enabling single sign-on, users are prompted to authenticate to Microsoft Entra ID and allow the Remote Desktop connection when launching a connection to a new Cloud PC. Microsoft Entra remembers up to 15 hosts for 30 days before prompting again. If you see this dialogue, select **Yes** to connect.

To provide single sign-on for all connections, you can hide this dialog by configuring a list of trusted Cloud PCs. This is done by adding one or more Device Groups containing Cloud PCs to a property on the service principals for the apps listed above in your Microsoft Entra tenant.

Follow these steps to hide the dialog:

1. [Create a Dynamic Device Group](/entra/identity/users/groups-create-rule) in Microsoft Entra containing the devices to hide the dialog for. Remember the device group ID for the next step.
    > [!TIP]
    > It's recommended to use a dynamic device group and configure the dynamic membership rules to includes all your Cloud PCs. This can be done using the device names or for a more secure option, you can set and use [device extension attributes](/graph/extensibility-overview) using [Microsoft Graph API](/graph/api/resources/device).
1. Use the [Microsoft Graph API](/graph/use-the-api) to [create a new targetDeviceGroup object](/graph/api/remotedesktopsecurityconfiguration-post-targetdevicegroups) to suppress the prompt for these Cloud PCs.

### Create a Kerberos Server object

You must [Create a Kerberos Server object](/entra/identity/authentication/howto-authentication-passwordless-security-key-on-premises#create-a-kerberos-server-object) if your Cloud PC meets the following criteria:

- Your Cloud PC is Microsoft Entra hybrid joined. You must have a Kerberos Server object to complete authentication to the domain controller.
- Your Cloud PC is Microsoft Entra joined and your environment contains Active Directory Domain Controllers. You must have a Kerberos Server object for users to access on-premises resources, such as SMB shares, and Windows-integrated authentication to websites.

If the Kerberos Server object isn't present for Microsoft Entra hybrid joined provisioning policies, you'll also see an error in your Azure Network Connection (ANC) health check regarding single sign-on.

> [!IMPORTANT]
> If you enable SSO on your Microsoft Entra hybrid joined Cloud PCs before you create a Kerberos server object, one of the following things can happen:
>
> - You receive an error message saying the specific session doesn't exist.
> - SSO will be skipped and you'll see a standard authentication dialog for the session host.
>
> You'll also see an error in your Azure Network Connection (ANC) health check regarding single sign-on.
>
> To resolve these issues, create the Kerberos server object before trying to connect again.

### Review your conditional access policies

When single sign-on is enabled, a new Microsoft Entra ID app is introduced to authenticate users to the Cloud PC. If you have conditional access policies that apply when accessing Windows 365, review the recommendations to [set conditional access policies](set-conditional-access-policies.md) to ensure users have the desired experience.

### Configure provisioning policy

SSO can be enabled on any provisioning policies. You can find the **Use Microsoft Entra single sign-on (preview)** option under the Join type on the General page. This can be done when [creating a new provisioning policy](create-provisioning-policy.md#continue-creating-a-provisioning-policy) or when [editing an existing provisioning policy](edit-provisioning-policy.md), with an option to apply SSO to existing Cloud PCs.

## Next steps

- Check out [In-session passwordless authentication (Preview)](identity-authentication.md#in-session-passwordless-authentication-preview) to learn how to enable passwordless authentication.
