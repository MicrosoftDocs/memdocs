---
title: "Configure Universal Print Policy Using Settings Catalog"
description: Learn how to configure a Universal Print policy using the settings catalog in Microsoft Intune to automatically install printers on managed Windows devices.
ms.date: 05/13/2026
ms.topic: how-to
ms.reviewer: laarrizz, mayurjadhav
ms.collection:
- M365-identity-device-management
---

# Create a Universal Print policy in Microsoft Intune

Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution in Microsoft 365. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure.

When you deploy Universal Print with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. For a guided simulation, see [Universal Print guided simulation](https://regale.cloud/Microsoft/viewer/1265/index.html#/0/0).

By using the settings catalog in Intune, you can create a printer policy and deploy the policy to your managed users and devices. Then, on their devices, end users select the printer from a list of registered Universal Print printers to print. These settings use the [UniversalPrint CSP](/windows/client-management/mdm/universalprint-csp).

This feature applies to:

- Windows

This article shows you how to create a Universal Print policy in Microsoft Intune. To learn more about Universal Print and onboarding, see [What is Universal Print](/universal-print/fundamentals/universal-print-whatis) and [Set up Universal Print](/universal-print/fundamentals/universal-print-getting-started).

> [!TIP]
> The __PrintProvisioning__ tool and the __printers.csv__ file process are deprecated. Be sure to use the steps in this article to install universal printers.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> To use this feature, you need the following subscriptions:
> - **Universal Print**: For more specific information, go to [License Universal Print](/universal-print/fundamentals/universal-print-license).
> - **Microsoft Intune**: For more specific information, go to [Microsoft Intune licensing](../../fundamentals/licensing/index.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> - Every printer must be registered in the Universal Print service (UP), which uses Microsoft Entra ID. For more information, go to [What is printer registration?](/universal-print/fundamentals/universal-print-printer-registration).
> - To create the Intune policy, you need the following printer information. Get this information from the Printer Administrator in your organization:
>
>   - Device ID
>   - Printer shared ID
>   - Printer shared name
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> **Admins** need the following roles/licenses:
> - **Policy and Profile Manager** role: Needed to create and assign Intune policies. For information on this role, go to [Role-based access control (RBAC) with Microsoft Intune](../../fundamentals/role-based-access-control/overview.md)
> - An assigned Universal Print license.
>
> **End users** need the following permissions/licenses:
> - An assigned Universal Print license
> - Access rights to the printer service and the Universal Print service
>
> If you assign the profile to a Microsoft Entra user or user group that can't access the printers because of permissions, Intune grants the assigned user or user group the permissions.
:::column-end:::
:::row-end:::

## Create the policy

This policy includes your printer information. When you assign the policy, the printers are automatically installed. Then, on their devices, users select a printer that you added.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Win11: Universal Print policy**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select **Printer Provisioning**, and select the settings you want to configure.

    :::image type="content" source="./media/configure-universal-print/settings-picker-printer-provisioning.png" alt-text="Screenshot that shows how to select printer provisioning in the settings catalog to create a universal print policy in Microsoft Intune and Intune admin center.":::

    Close the settings picker.

8. Configure the settings:

    - **Action**: Select **Install** to install a printer. When users receive the policy, the printer automatically installs.
    - **Cloud Device ID**: Enter the printer ID. This ID is created when the printer is registered in Microsoft Entra ID using the Universal Print service. To get the ID, use the [Universal Print portal](/universal-print/reference/portal/navigate-azure-portal).
    - **Printer Shared ID**: Enter the Shared ID of the printer. To get the ID, use the [Universal Print portal](/universal-print/reference/portal/navigate-azure-portal).
    - **Printer Shared Name**: Enter the Shared Name of the printer. To get the name, use the [Universal Print portal](/universal-print/reference/portal/navigate-azure-portal).

    You can add more printers using the **Add** button:

    :::image type="content" source="./media/configure-universal-print/add-printer.png" alt-text="Screenshot that shows how to add more printers to the universal print policy in the settings catalog in Microsoft Intune and Intune admin center.":::

9. Select **Next**.

10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../../fundamentals/role-based-access-control/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users that will receive your profile.

    These user accounts need access rights to the printer and the Universal Print service. If the profile is assigned to a Microsoft Entra user or user group that can't access the printers because of permissions, Intune grants the assigned user or user group the permissions.

    If users don't have permissions, the following message is shown:

    `The selected groups may not have Universal Print permissions to selected printers. If this is the case, Intune will provide these groups with the correct permissions.`

    For more information on assigning profiles in Intune, go to [Assign user and device profiles](../../device-configuration/assign-device-profile.md). For more information on user scope vs. device scope in the settings catalog, go to [Use the settings catalog to configure settings: Device scope vs. user scope settings](index.md#device-scope-vs-user-scope-settings).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Failures and reporting

After you assign the profile, you can monitor its status. The Intune reports show if a profile is successfully applied, failed, has conflicts, and more. For more specific information, see [Monitor device configuration profiles in Microsoft Intune](../../device-configuration/monitor-device-profile.md).

For information on the reporting data you can view, see [Intune reports](../../device-management/reports/overview.md).

### Common issues

- When you deploy the printer policy, you might get a `Error 0x8007007f (ERROR_PROC_NOT_FOUND)` message.

  The `ERROR_PROC_NOT_FOUND` error is common, and is typically associated with missing `DelayLoaded` DLLs or missing APIs.

  To resolve this error, make sure your Windows OS client version is supported. The supported versions are listed at the top of this article.

- If you remove a printer from the Universal Print service, unshare it, or remove permissions, the Intune policy fails to install the printer.

- Make sure the printer is discoverable on the device. If users can't discover or install the printer manually, the Intune policy also fails to install the printer.

- Make sure you enter the **SharedID** and **PrinterID** correctly in the Intune policy.

  In some cases, the PrinterID and SharedID are reversed, which prevents the printer from being discovered. For more information on these settings, see [Create the policy](#create-the-policy) (in this article).

- The Application event log can show errors related to Universal Print.

### Enable tracing for Universal Print issues

If the [common issues](#common-issues) (in this article) don't resolve your issue, you can use TSS (Troubleshooting Script for Support) together with `UPPrinterInstaller.exe` to capture client-side traces for the Intune installation of the universal printer. You can review these logs for possible issues. You can also work with the Intune support team to review and analyze these logs.

For more information and specific steps, see [Universal Print troubleshooting guide - Use TSS and UPPrinterInstaller](/universal-print/fundamentals/universal-print-troubleshooting-support-howto#use-tss-and-upprinterinstaller).

## Related articles

- [What is Universal Print](/universal-print/fundamentals/universal-print-whatis)
- [Use the settings catalog to configure settings on Windows and macOS devices](index.md)
