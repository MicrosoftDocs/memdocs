---
title: Manage Windows LAPS with Microsoft Intune policies
description: Use Microsoft Intune application protection policy to manage the local administrator accounts on Windows devices. Through the Windows LAPS CSP, back up accounts and passwords to Microsoft Entra ID, define password requirements, and protect account passwords through scheduled password rotations and manual rotations at need.

keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/13/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- sub-secure-endpoints
---

# Microsoft Intune support for Windows LAPS

Every Windows machine has a built-in local administrator account that can’t be deleted, and which has full permissions to the device. Securing this account is an important step in securing your organization. Windows devices include *Windows Local Administrator Password Solution* ([LAPS](/windows-server/identity/laps/laps-overview)), a built-in solution to help manage local admin accounts.

You can use Microsoft Intune endpoint security policies for [account protection](../protect/endpoint-security-account-protection-policy.md) to manage LAPS on devices that have enrolled with Intune. Intune policies can:

- Enforce password requirements for local admin accounts
- Back up a local admin account from devices to your Active Directory (AD) or Microsoft Entra
- Schedule rotation of those account passwords to help keep them safe.

You can also view details about the managed local admin accounts in the Intune Admin center, and manually rotate their account passwords outside of a scheduled rotation.

Use of Intune LAPS policies helps you protect Windows devices from attacks that are aimed at exploiting local user accounts like pass-the-hash or lateral-traversal attacks. Managing LAPS with Intune can also help improve security for remote help desk scenarios and recover devices that are otherwise inaccessible.

Intune LAPS policy manages the settings available from the Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp). Intune's use of the CSP replaces the use of [Legacy Microsoft LAPS](https://www.microsoft.com/download/details.aspx?id=46899) or other LAPS management solutions, with CSP based [taking precedence](/windows-server/identity/laps/laps-management-policy-settings#supported-policy-roots) over other LAPS management sources.

Intune support for Windows LAPS includes the following capabilities:

- **Set password requirements** – Define password requirements including complexity and length for the local administrator account on a device.
- **Rotate passwords** – With policy you can have devices automatically rotate the local admin account passwords on a schedule. You can also use the Intune admin center to manually rotate the password for a device as a device action.
- **Backup accounts and passwords** – You can choose to have devices back up their account and password in either Microsoft Entra ID in the cloud, or your on-premises Active Directory. Passwords are stored using strong encryption.
- **Configure post authenticating actions** – Define actions that a device takes when its local admin account password expires. Actions range from resetting the managed account to use a new secure password, logging off the account, or doing both and then powering down the device. You can also manage how long the device waits after the password expires before taking these actions.
- **View account details** – Intune administrators with sufficient role-based administrative control (RBAC) permissions can view information about a devices local admin account and its current password. You can also see when that password was last rotated (reset) and when it's next scheduled to rotate.
- **View reports** – Intune provides reports on password rotation including details about past manual and scheduled password rotation.

To learn about Windows LAPS in more detail, start with the following articles in the Windows documentation:

- [What is Windows LAPS?](/windows-server/identity/laps/laps-overview) – Introduction to Windows LAPS and the Windows LAPS documentation set.
- Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp) – View the full details for LAPS settings and options. Intune policy for LAPS uses these settings to configure the LAPS CSP on devices.

Applies to:

- Windows 10
- Windows 11

## Prerequisites

The following are requirements for Intune to support Windows LAPS in your tenant:

### Licensing requirements

- **Intune subscription** - *Microsoft Intune Plan 1*, which is the basic Intune subscription. You can also use Windows LAPS with a free trial subscription for Intune.

- **Microsoft Entra ID** – *Microsoft Entra ID Free*, which is the free version of Microsoft Entra ID that’s included when you subscribe to Intune. With Microsoft Entra ID Free, you can use all the features of LAPS.
  
### Active Directory support

Intune policy for Windows LAPS can configure a device to back up a local administrator account and password to one of the following Directory types:

  > [!NOTE]  
  > Devices that are workplace-joined (WPJ) are not supported by Intune for LAPS.

- **Cloud** – Cloud supports backup to your Microsoft Entra ID for the following scenarios:

  - Microsoft Entra hybrid join
  - Microsoft Entra join

    Support for *Microsoft Entra join* requires you to enable LAPS in your Microsoft Entra ID. The following steps can help you complete this configuration. For the larger context, view these steps in the Microsoft Entra documentation at [Enabling Windows LAPS with Microsoft Entra ID](/azure/active-directory/devices/howto-manage-local-admin-passwords#enabling-windows-laps-with-azure-ad). *Microsoft Entra hybrid join* does not require LAPS to be enabled in Microsoft Entra.

    **Enable LAPS in Microsoft Entra**:  
    1. Sign in to the [**Microsoft Entra admin center**](https://entra.microsoft.com/) as a [Cloud Device Administrator](/entra/identity/role-based-access-control/permissions-reference#cloud-device-administrator).
    2. Browse to **Identity** > **Devices** > **Overview** > **Device settings**.
    3. Select **Yes** for the *Enable Local Administrator Password Solution (LAPS)* setting and select **Save**. You may also use the Microsoft Graph API [Update deviceRegistrationPolicy](/graph/api/deviceregistrationpolicy-update?view=graph-rest-beta&preserve-view=true).

    For more information, see [Windows Local Administrator Password Solution in Microsoft Entra ID](/entra/identity/devices/howto-manage-local-admin-passwords) in the Microsoft Entra documentation.

- **On-premises** – On-premises supports back up to Windows Server Active Directory (on-premises Active Directory).

  > [!IMPORTANT]  
  > LAPS on Windows devices can be configured to use one directory type or the other, but not both. Also consider, the backup directory must be supported by the devices join type – if you set the directory to an on-premises Active Directory and the device is not domain joined, it will accept the policy settings from Intune, but LAPS cannot successfully use that configuration.

### Device Edition and Platform

Devices can have any [Windows edition that Intune supports](../fundamentals/supported-devices-browsers.md#microsoft), but must run of one of the following versions to support the Windows LAPS CSP:

- Windows 10, version 22H2 (19045.2846 or later) with [KB5025221 ](https://support.microsoft.com/topic/april-11-2023-kb5025221-os-builds-19042-2846-19044-2846-and-19045-2846-b00c3356-baac-4a41-8342-7f97ec83445a)
- Windows 10, version 21H2 (19044.2846 or later) with [KB5025221 ](https://support.microsoft.com/topic/april-11-2023-kb5025221-os-builds-19042-2846-19044-2846-and-19045-2846-b00c3356-baac-4a41-8342-7f97ec83445a)
- Windows 10, version 20H2 (19042.2846 or later) with [KB5025221 ](https://support.microsoft.com/topic/april-11-2023-kb5025221-os-builds-19042-2846-19044-2846-and-19045-2846-b00c3356-baac-4a41-8342-7f97ec83445a)
- Windows 11, version 22H2 (22621.1555 or later) with [KB5025239](https://support.microsoft.com/en-us/topic/april-11-2023-kb5025239-os-build-22621-1555-5eaaaf42-bc4d-4881-8d38-97e0082a6982)
- Windows 11, version 21H2 (22000.1817 or later) with [KB5025224](https://support.microsoft.com/en-us/topic/april-11-2023-kb5025224-os-build-22000-1817-ebc75372-608d-4a77-a6e0-cb1e15f117fc)

### GCC High support

Intune policy for Windows LAPS is supported for GCC High environments.

## Role based access controls for LAPS

To manage LAPS, an account must have sufficient role-based access control (RBAC) permissions to complete a desired task. The following are the available tasks with their required permissions:

- **Create and access LAPS policy** – To work with and view LAPS policies, your account must be assigned sufficient permissions from the Intune RBAC category for **Security baselines**. By default, these are included in the built-in role **Endpoint Security Manager**.  To use custom roles, ensure the custom role includes the rights from the *Security baselines* category.

- **Rotate local Administrator password** – To use the Intune admin center to view or rotate a devices local admin account password, your account must be assigned the following Intune permissions:

  - Managed devices: **Read**
  - Organization: **Read**
  - Remote tasks:  **Rotate Local Admin Password**

- **Retrieve local Administrator password** – To view password details, your account must have one of the following Microsoft Entra permissions:

  - `microsoft.directory/deviceLocalCredentials/password/read` to read LAPS metadata and passwords.
  - `microsoft.directory/deviceLocalCredentials/standard/read` to read LAPS metadata excluding passwords.

  To create custom roles that can grant these permissions, see [Create and assign a custom role in Microsoft Entra ID](/azure/active-directory/roles/custom-create) in the Microsoft Entra documentation.
  
- **View Microsoft Entra audit logs and events** – To view details about LAPS policies and recent device actions such as password rotation events, your account must permissions equivalent to the built-in Intune role **Read Only Operator**.

For more information, see [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

## LAPS Architecture

For information about Windows LAPS architecture, see [Windows LAPS architecture](/windows-server/identity/laps/laps-concepts-overview#windows-laps-architecture) in the Windows documentation.

## Frequently Asked Questions

### Can I use Intune LAPS policy to manage any local admin account on a device?

Yes. Intune LAPS policy can be used to manage any local administrator account on a device. However, LAPS supports only one account per device:

- When a policy doesn’t specify an account name, Intune manages the default built-in administrator account regardless of its current name on the device.
- You can change the account that Intune manages for a device by changing the device’s assigned policy or editing its current policy to specify a different account.
- If two separate policies are assigned to a device that both specify a different account, a conflict occurs that must be resolved before the device’s account can be managed.

### What if I deploy LAPS policy with Intune to a device that already has LAPS configurations from a different source?

The CSP-based policy from Intune overrides all other sources of LAPS policy, such as from GPOs or a configuration from [Legacy Microsoft LAPS](https://www.microsoft.com/download/details.aspx?id=46899). For more information, see [Supported Policy roots](/windows-server/identity/laps/laps-management-policy-settings#supported-policy-roots) in the Windows LAPS documentation.

### Can Windows LAPS create local admin accounts based on the administrator account name that’s configured using LAPS policy?

No. Windows LAPS can only manage accounts that already exist on the device. If a policy specifies an account by name that doesn't exist on the device, the policy applies and doesn’t report an error. However, no account is backed up.

### Does Windows LAPS rotate and backup the password for a device that is disabled in Microsoft Entra?

No. Windows LAPS requires the device to be in an enabled state before password rotation and backup operations can apply.

### What happens when a device is deleted in Microsoft Entra?

When a device is deleted in Microsoft Entra, the LAPS credential that was tied to that device is lost and the password that is stored in Microsoft Entra ID is lost. Unless you have a custom workflow to retrieve LAPS passwords and store them externally, there's no method in Microsoft Entra ID to recover the LAPS managed password for a deleted device.

### What roles are needed to recover LAPS passwords?

The following [built-in Microsoft Entra roles](/entra/identity/role-based-access-control/permissions-reference) have permission to recover LAPS passwords: *Cloud Device Administrator*, and *Intune Administrator*.

### What roles are needed to read LAPS metadata?

The following [built-in Microsoft Entra roles](/entra/identity/role-based-access-control/permissions-reference) roles are supported to view metadata about LAPS including the device name, last password rotation, and next password rotation:

- *Security Reader*

You can also use following roles:

- *Cloud Device Administrator*
- *Intune Administrator*
- *Helpdesk Administrator*
- *Security Administrator*

### Why is the Local admin password button greyed out and inaccessible?
Currently, access to this area requires the Rotate local Administrator password Intune permission. See [Role-based access control for Microsoft Intune](../fundamentals/role-based-access-control.md).

### What happens when the account specified by policy is changed?

Because Windows LAPS can only manage one local admin account on a device at a time, the original account is no longer managed by LAPS policy. If policy has the device back up that account, the new account is backed up and details about the previous account are no longer available from within the Intune admin center or from the Directory that is specified to store the account information.

## Next steps

- [Create policy for LAPS](../protect/windows-laps-policy.md)
- [View reports for LAPS](../protect/windows-laps-reports.md)
- [Account protection policy for endpoint security in Intune](../protect/endpoint-security-account-protection-policy.md)
