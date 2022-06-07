---
# required metadata

title: Configure Universal Print policy using settings catalog in Microsoft Intune
description: Use the settings catalog in Microsoft Intune and Endpoint Manager to create a Universal Print policy for Windows 10/11 client devices. The policy automatically installs printers on your managed devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/06/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create a Universal Print policy in Microsoft Intune

> [!NOTE]
> This feature will release over several days and won't be available to all tenants immediately.

Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution in Microsoft 365. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure.

When Universal Print is deployed with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. For a guided simulation, go to [Universal Print guided simulation](https://regale.cloud/Microsoft/viewer/1265/index.html#/0/0).

Using the settings catalog in Intune, you can create a printer policy, and deploy the policy to your managed users and devices. Then, on their devices, end users select the printer from a list of registered Universal Print printers to print.

This feature applies to:

- Windows 11

This article shows you how to create a Universal Print policy in Microsoft Intune. To learn more about Universal Print and onboarding, go to [What is Universal Print](/universal-print/fundamentals/universal-print-whatis) and [Set up Universal Print](/universal-print/fundamentals/universal-print-getting-started).

## Before you begin

- To use this feature, you need the following subscriptions:

  - **Universal Print**: For more specific information, go to [License Universal Print](/universal-print/fundamentals/universal-print-license).
  - **Microsoft Intune**: For more specific information, go to [Microsoft Intune licensing](../fundamentals/licenses.md).

- Every printer must be registered in the Universal Print service (UP), which uses Azure AD. To create the Intune policy, you need the device ID, printer shared ID, and printer shared name.

  For more specific information, go to [What is printer registration?](/universal-print/fundamentals/universal-print-printer-registration)

- Admin accounts need the following roles/licenses:

  - **Printer Administrator** or **Global Administrator** roles: Needed to add printers.

    For more information on these roles, go to [Azure AD built-in roles](/azure/active-directory/roles/permissions-reference).

  - **Intune Administrator** or **Global Administrator** roles: Needed to create and assign Intune policies.

    For more information on these roles, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)

  - An assigned Universal Print license.

- End user accounts need the following permissions/licenses:

  - An assigned Universal Print license
  - Have access rights to the printer service and the Universal Print service

  If the profile is assigned to an Azure AD user/user group that can't access the printers because of permissions, then Intune grants the assigned user/user group the permissions.

- These settings use the [UniversalPrint CSP](/windows/client-management/mdm/universalprint-csp).

## Create the policy

This policy includes your printer information. When you assign the policy, the printers are automatically installed. Then, on their devices, users select a printer that you added.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Settings catalog (preview)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Win11: Universal Print policy**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select **Printer Provisioning**, and select the settings you want to configure.

    :::image type="content" source="./media/settings-catalog-printer-provisioning/settings-picker-printer-provisioning.png" alt-text="In the Settings Catalog policy, select printer provisioning to create a universal print policy in Microsoft Intune and Endpoint Manager admin center.":::

    Close the settings picker.

8. Configure the settings:

    - **Action**: Select **Install** to install a printer. When users receive the policy, the printer will automatically install. Select **Uninstall** to uninstall a printer.
    - **Cloud Device ID**: Enter the printer ID. This ID is created when the printer is registered in Azure AD using the Universal Print service. To get the ID, use the [Universal Print portal](/universal-print/portal/navigate-up).
    - **Printer Shared ID**: Enter the Shared ID of the printer. To get the ID, use the [Universal Print portal](/universal-print/portal/navigate-up).
    - **Printer Shared Name**: Enter the Shared Name of the printer. To get the name, use the [Universal Print portal](/universal-print/portal/navigate-up).

    You can add more printers using the **Add** button:

    :::image type="content" source="./media/settings-catalog-printer-provisioning/add-printer.png" alt-text="In Settings Catalog, add more printers to the universal print policy in Microsoft Intune and Endpoint Manager admin center.":::

9. Select **Next**.

10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users that will receive your profile.

    These user accounts need access rights to the printer and the Universal Print service. If the profile is assigned to an Azure AD user/user group that can't access the printers because of permissions, then Intune grants the assigned user/user group the permissions.

    If users don't have permissions, then the following message is shown:

    ```log
    The selected groups may not have Universal Print permissions to selected printers. If this is the case, Intune will provide these groups with the correct permissions.
    ```

    For more information on assigning profiles in Intune, go to [Assign user and device profiles](device-profile-assign.md). For more information on user scope vs. device scope in the settings catalog, go to [Use the settings catalog to configure settings: Device scope vs. user scope settings](settings-catalog.md#device-scope-vs-user-scope-settings).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Failures and reporting

After you assign the profile, you can monitor its status. The Intune reports show if a profile successfully applied, failed, has conflicts, and more. For more specific information, go to [Monitor device configuration profiles in Microsoft Intune](device-profile-monitor.md).

If a printer is removed from the Universal Print service, unshared, or if permissions are removed, then the profile will fail.

For information on all the reporting data you can view, go to [Intune reports](../fundamentals/reports.md).

## Learn more

- [What is Universal Print](/universal-print/fundamentals/universal-print-whatis)
- [Use the settings catalog to configure settings on Windows and macOS devices](settings-catalog.md)
