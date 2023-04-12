---
# required metadata

title: Common issues and resolutions with cloud-native endpoints
titleSuffix: Microsoft Intune
description: Learn more about the known and resolutions when using cloud-native endpoints. Use user-based authentication; don't use machine authentication. Existing group policy objects might not apply. Local Administrator Password Solution (LAPS) isn't supported.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 10/05/2022
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: ahamil, jasandys, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - intune-scenario
---

# Known issues and limitations with cloud-native endpoints

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../../includes/cloud-native-endpoints-definitions.md)]

When using or moving on-premises device management to cloud-native endpoints, there are some scenarios you need to know. This article lists and describes some changed behaviors, limitations, and resolutions.

Cloud-native endpoints are devices that are joined to Azure AD. In many cases, they don't require a direct connection to any on-premises resources for usability or management. For more specific information, go to [What are cloud-native endpoints](cloud-native-endpoints-overview.md).

This feature applies to:

- Windows cloud-native endpoints

In this article, **Computer accounts** and **machine accounts** are used interchangeably.

## Don't use machine authentication

When a Windows endpoint, like a Windows 10/11 device, joins an on-premises Active Directory (AD) domain, a computer account is automatically created. The computer/machine account can be used to authenticate.

Machine authentication happens when:

- On-premises resources, like file shares, printers, applications, and web sites, are accessed using on-premises AD computer accounts instead of user accounts.
- Administrators or application developers configure on-premises resource access using machine accounts instead of users or user groups.

Cloud-native endpoints are joined to Azure AD, and don't exist in on-premises AD. Cloud-native endpoints don't support on-premises AD machine authentication. Configuring access to on-premises file shares, applications, or services using only on-premises AD machine accounts will fail on cloud-native endpoints.

### Switch to user-based authentication

- When creating new projects, don't use machine authentication. It's not common or a recommended practice, but it's something you need to know and be aware. Instead, use user-based authentication.
- Review your environment and identify any applications and services that currently use machine authentication. Then, change the access to user-based authentication or service account-based authentication.

> [!IMPORTANT]
> The Azure AD Connect device writeback feature tracks devices that are registered in Azure AD. These devices are shown in on-premises AD as registered devices.
>
> Azure AD Connect device writeback doesn't create identical on-premises AD computer accounts in the on-premises AD domain. These writeback devices don't support on-premises machine authentication. 
>  
> For information on scenarios supported with device writeback, go to [Azure AD Connect: Enabling device writeback](/azure/active-directory/hybrid/how-to-connect-device-writeback).

### Common services that use machine accounts

The following list includes common features and services that might use machine accounts to authenticate. It also includes recommendations if your organization is using these features with machine authentication.

- **Network storage access** fails with machine accounts. Cloud-native endpoints can't access file shares secured using machine accounts. If ACL (access control list) permissions are assigned only to machine accounts, or assigned to groups that include only machine accounts, then drive mapping with file shares or network-attached storage (NAS) shares will fail.

  **Recommendation**:

  - **Server and workstation file shares**: Update permissions to use user account-based security. When you do, use [Azure AD single sign-on (SSO)](/azure/active-directory/devices/azuread-join-sso) to access resources that use Windows integrated authentication.

    Move file share content to SharePoint Online or OneDrive. For more specific information, go to [Migrate file shares to SharePoint and OneDrive](/sharepointmigration/fileshare-to-odsp-migration-guide).

  - **Network File System (NFS) root access**: Direct users to access specific folders, not the root. If you can, move content from an NFS to SharePoint Online or OneDrive.

- **Win32 apps** on Azure AD joined Windows endpoints:

  - Won't work if the apps use machine account authentication.
  - Won't work if the apps access resources that are secured with groups that include only machine accounts.

  **Recommendation**: 
  - If your Win32 apps use machine authentication, then update the app to use Azure AD authentication. For more information, go to [Migrate application authentication to Azure AD](/azure/active-directory/manage-apps/migrate-application-authentication-to-azure-active-directory).
  - Check the authentication and identities of your applications and kiosk devices. Update the authentication and identities to use user account-based security.

  For more information, go to [Authentication and Win32 apps](/windows/win32/secauthn/authentication-portal).

- **IIS web server** deployments that restrict site access using ACL permissions with only computer accounts, or groups of computer accounts, will fail. Authentication strategies that limit access to only computer accounts or groups of computer accounts will also fail.

  **Recommendation**:
  - On your web sites, enable Negotiate authentication.
  - Update your web server apps to use Azure AD authentication. For more information, go to [Migrate application authentication to Azure AD](/azure/active-directory/manage-apps/migrate-application-authentication-to-azure-active-directory).
  
  More resources:

  - [IIS Authentication `<windowsAuthentication>`](/iis/configuration/system.webserver/security/authentication/windowsauthentication/)
  - [IIS Security Authorization `<authorization>`](/iis/configuration/system.webserver/security/authorization/)

- Standard **print management and discovery** depends on machine authentication. On Azure AD joined Windows endpoints, users can't print using standard print.

  **Recommendation**: Use Universal Print. For more specific information, go to [What is Universal Print](/universal-print/fundamentals/universal-print-whatis).

- **Windows scheduled tasks** that run in the machine-context on cloud-native endpoints can't access resources on remote servers and workstations. The cloud-native endpoint doesn't have an account in on-premises AD, and therefore can't authenticate.

  **Recommendation**: Configure your scheduled tasks to use **logged in user**, or another form of account-based authentication.

- **Active Directory login scripts** are assigned in the on-premises AD user's properties or deployed using a Group Policy Object (GPO). These scripts aren't available for cloud-native endpoints.  

  **Recommendation**: Review your scripts. If there's a modern equivalent, then use it instead. For example, if your script sets the user's home drive, then you can move a user's home drive to OneDrive instead. If your script stores shared folder content, then migrate the shared folder content to SharePoint Online instead.

  If there isn't a modern equivalent, then you can deploy Windows PowerShell scripts using Microsoft Intune.

  For more information, go to:

  - [Add PowerShell scripts to Windows 10/11 devices in Microsoft Intune](../../intune/apps/intune-management-extension.md)
  - [Introduction to OneDrive in Microsoft 365](/training/modules/m365-onedrive-collaboration-use/)

## Group policy objects might not apply

It's possible some of your older policies aren't available, or don't apply to cloud-native endpoints.

**Resolution**:

- Using [Group Policy Analytics](../../intune/configuration/group-policy-analytics.md) in Intune, you can evaluate your existing group policy objects (GPO). The analysis shows the policies that are available, and policies that aren't available.
- In endpoint management, policies are deployed to users and groups. They aren't applied in LSDOU order. This behavior is a mind shift, so make sure your users and groups are in order.

  For more specific information and guidance on policy assignment in Microsoft Intune, go to [Assign user and device profiles in Microsoft Intune](../../intune/configuration/device-profile-assign.md).

- Inventory your policies, and determine what they do. You may find categories or groupings, such as policies that focus on security, policies that focus on the OS, and so on.

  You can create an Intune policy that includes the settings from your categories or groupings. The [Settings Catalog](../../intune/configuration/settings-catalog.md) is a good resource.

- Be prepared to create new policies. The built-in features of modern endpoint management, like Microsoft Intune, may have better options to create and deploy policies.

  The [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md#move-from-group-policy-objects-gpos) is a good resource.

- Don't migrate all your policies. Remember, your old policies might not make sense with cloud-native endpoints.

  Instead of doing what you've always done, focus on what you actually want to achieve.

## Local Administrator Password Solution (LAPS) aren't supported

Currently, cloud-native endpoints don't support the [Microsoft Local Administrator Password Solution (LAPS)](/defender-for-identity/cas-isp-laps) (opens another Microsoft website).

LAPS manages local administrator account passwords for domain-joined devices. Passwords are randomized and stored in on-premises AD, and protected by ACLs. So, only eligible users can read the password or request a password reset.

Microsoft will release an update to provide LAPS for Azure AD joined devices (no ETA). When it's released, you can use it to manage local administrator account passwords on cloud-native endpoints.

**Resolution**: 

Azure AD joined devices use Azure AD to configure users and groups that will have local administrator privileges. For more information and guidance, go to [How to manage local administrators on Azure AD joined devices](/azure/active-directory/devices/assign-local-admin).

## Synchronized user accounts can't complete first sign-in

Synchronized user accounts are on-premises AD domain users that are synchronized to Azure AD using Azure AD Connect.

Currently, synchronized user accounts with passwords that have **User must change password at next logon** configured can't complete a first-time sign-in to a cloud-native endpoint.

**Resolution**: 

Use Password Hash Sync and Azure AD connect, which forces the **force password change at logon** attribute to sync.

For more specific information, go to [Implement password hash synchronization with Azure AD Connect sync](/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#synchronizing-temporary-passwords-and-force-password-change-on-next-logon).

## Follow the cloud-native endpoints guidance

1. [Overview: What are cloud-native endpoints?](cloud-native-endpoints-overview.md)
2. [Tutorial: Get started with cloud-native Windows endpoints](cloud-native-windows-endpoints.md)
3. [Concept: Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
4. [Concept: Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. 🡺 **Known issues and important information** (*You are here*)
