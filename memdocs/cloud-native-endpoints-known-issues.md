---
# required metadata

title: Common issues and resolutions with cloud native endpoints
titleSuffix: Microsoft Endpoint Manager
description: Learn more about the known and resolutions when using cloud native endpoints. Use user-based authentication; don't use machine authentication. Existing group policy objects might not apply. Local Administrator Password Solution (LAPS) aren't supported.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 03/29/2022
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
---

# Known issues and limitations with cloud native endpoints

When using or moving on-premises device management to cloud native endpoints, there are some scenarios you need to know. This article lists and describes some changed behaviors, limitations, and resolutions.

Cloud native endpoints are devices that are joined to Azure AD. In many cases, they don't require a direct connection to any on-premises resources for usability or management. For more specific information, see [Cloud native endpoint overview](cloud-native-endpoints-overview.md).

In this article, **Azure AD joined** and **cloud native endpoints** are used interchangeably.

## Don't use machine authentication

When a Windows endpoint, like a Windows 10/11 device joins an Active Directory Domain, a computer account is automatically created.

Machine authentication occurs when on-premises resources, like file shares, printers, applications, and web sites are accessed using Active Directory computer accounts instead of users.  Machine authentication happens when administrators or application developers configure on-premises resource access using machine accounts instead of users or user groups.

Cloud native endpoints are joined to Azure AD, and don't exist in Active Directory. So, cloud native endpoints don't support Active Directory machine authentication. Strictly configuring access to on-premises file shares, applications, or services using only Active Directory machine accounts will fail on cloud native endpoints.


### Switch to user-based authentication

- Don't use machine authentication for any new projects in your organization. It's not common or a recommended practice, but it's something you need to know and be aware.
- Review your environment and identify any applications and services that use machine authentication. Then, change the access to user-based authentication or service account-based authentication.

> [!IMPORTANT]
> The Azure AD Connect device writeback feature does not create equivalent AD computer accounts in the on-premises AD domain. The devices created in Active Directory because of device writeback do not support on-premises machine authentication. 
>  
> For information on scenarios supported with Device Writeback refer to - [Azure AD Connect: Enabling device writeback](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-device-writeback).

### Common services that use machine accounts

The following list includes common features and services that might use machine accounts to authenticate. It also includes recommendations if your organization is using these features with machine authentication.

- **Network storage access** fails with machine accounts. Cloud native endpoints can't access file shares secured using machine accounts. If ACL (access control list) permissions are assigned only to machine accounts, or assigned to groups that include only machine accounts, then drive mapping with file shares or network-attached storage (NAS) shares will fail.

  **Recommendation**:

  - **Server and workstation file shares**: Update permissions to use user account-based security. When you do, use [Azure AD single sign-on (SSO)](/azure/active-directory/devices/azuread-join-sso) to access resources that use Windows integrated authentication.

    Move file share content to SharePoint Online or OneDrive for Business. For more specific information, see [Migrate file shares to SharePoint and OneDrive](/sharepointmigration/fileshare-to-odsp-migration-guide).

  - **Network File System (NFS) root access**: Direct users to access specific folders, not the root. If you can, move content from a NFS to SharePoint Online or OneDrive for Business.

- On Azure AD joined Windows endpoints, **Win32 apps**:

  - Won't work if the apps use machine account authentication.
  - Won't work if the apps access resources that are secured with groups that include only machine accounts.

  **Recommendation**: 
  - If machine authentication is present in Win32 apps, consider migrating application authentication to Azure Active Directory.  For more information see [Migrate application authentication to Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/migrate-application-authentication-to-azure-active-directory).
  - Check the authentication and identities of your applications and kiosk devices. Update the authentication and identities to use user account-based security.
  - Update Win32 apps to move away from the use of Active Directory machine account authentication.
  - Reference: [Authentication - Win32 apps](https://docs.microsoft.com/en-us/windows/win32/secauthn/authentication-portal).

- **IIS web server** deployments that restrict site access using ACL permissions with only computer accounts, or groups of computer accounts, will fail. Authentication strategies that limit access to only computer accounts or groups of computer accounts will also fail.

  **Recommendation**: 
  - Consider using Kerberos authentication or [migrating on premises web infrastructure - IIS authentiation to Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/migrate-application-authentication-to-azure-active-directory). 
  
  Additional resources:

  - [IIS Authentication `<windowsAuthentication>`](/iis/configuration/system.webserver/security/authentication/windowsauthentication/)
  - [IIS Security Authorization `<authorization>`](/iis/configuration/system.webserver/security/authorization/)

- Standard **print management and discovery** depends on machine authentication. On Azure AD joined Windows endpoints, users can't print using standard print.

  **Recommendation**: Use Universal Print. For more specific information, see [What is Universal Print](/universal-print/fundamentals/universal-print-whatis).

- **Windows scheduled tasks** that run in the machine-context on cloud native endpoints can't access resources on remote servers and workstations. The cloud native endpoint doesn't have an account in Active Directory, and therefore can't authenticate.

  **Recommendation**: Configure your scheduled tasks to use **logged in user**, or another form of account-based authentication.

- **Login scripts** Active Directory logon scripts assigned as part of an Active Directory users’ properties or delivered via a Group Policy Object (GPO) are not available for cloud native endpoints.  

  **Recommendation**: As an alternative consider using consider using Intune PowerShell scripts feature for Windows.  In addition, consider the use of OneDrive and SharePoint Online.
  Reference: 
  - [Add PowerShell scripts to Windows 10/11 devices in Microsoft Intune](https://docs.microsoft.com/en-us/mem/intune/apps/intune-management-extension)
  - [Introduction to OneDrive in Microsoft 365](https://docs.microsoft.com/en-us/learn/modules/m365-onedrive-collaboration-use/)

## Group policy objects might not apply

It's possible some of your older policies aren't available, or don't apply to cloud native endpoints.

**Resolution**:

- Using [Group Policy Analytics](/mem/intune/configuration/group-policy-analytics) in Endpoint Manager, you can evaluate your existing group policy objects (GPO). The analysis shows the policies that are available, and policies that aren't available.
- In endpoint management, policies are deployed to users and groups. They aren't applied in LSDOU order. This is a mind shift, so make sure your users and groups are in order.

  For more specific information and guidance on policy assignment in Microsoft Intune, see [Assign user and device profiles in Microsoft Intune](/mem/intune/configuration/device-profile-assign).

- Inventory your policies, and determine what they do. You may find categories or groupings, such as policies that focus on security, policies that focus on the OS, and so on.

  You can create an Intune policy that includes the settings from your categories or groupings. The [Settings Catalog](/mem/intune/configuration/settings-catalog) is a good resource.

- Be prepared to create new policies. The built-in features of modern endpoint management, like Microsoft Intune, may have better options to create and deploy policies.

  The [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md#move-from-group-policy-objects-gpos) is a good resource.

- Don't migrate all your policies. Remember, your old policies might not make any sense with cloud native endpoints.

  Instead of doing what you've always done, focus on the what you actually want to achieve.

## Local Administrator Password Solution (LAPS) aren't supported

Currently, cloud native endpoints don't support the [Microsoft Local Administrator Password Solution (LAPS)](/defender-for-identity/cas-isp-laps) (opens another Microsoft website).

LAPS manages local administrator account passwords for domain-joined devices. Passwords are randomized and stored in Active Directory (AD), and protected by ACLs. So, only eligible users can read the password or request a password reset.

Microsoft will release an update to provide LAPS for Azure AD joined devices. When it's released, you can use it to manage local administrator account passwords on cloud native endpoints.

**Resolution**: 

Azure AD joined devices use Azure AD to configure users and groups that will have local administrator privileges. For more information and guidance, see [How to manage local administrators on Azure AD joined devices](/azure/active-directory/devices/assign-local-admin).

## Synchronized user accounts can't complete first sign-in

Synchronized user accounts are on-premises AD domain users that are synchronized to Azure AD using Azure AD Connect.

Currently, synchronized user accounts with passwords that have **User must change password at next logon** configured can't complete a first-time sign in to a cloud native endpoint.

**Resolution**: 

Use Password Hash Sync and Azure AD connect, which forces the **force password change at logon** attribute to sync.

For more specific information, see [Implement password hash synchronization with Azure AD Connect sync](/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#synchronizing-temporary-passwords-and-force-password-change-on-next-logon).

## Next steps

- [What are cloud native endpoints?](cloud-native-endpoints-overview.md)
- [Tutorial: Get started with cloud native Windows endpoints with Microsoft Endpoint Manager](cloud-native-windows-endpoints.md)
- [Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
- [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md)
