---
# required metadata

title: Configure Universal Print policy using settings catalog in Microsoft Intune
description: Use the settings catalog in Microsoft Intune to create a Universal Print policy for Windows 10/11 client devices. The policy automatically installs printers on your managed devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/11/2023
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Create a Universal Print policy in Microsoft Intune

Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution in Microsoft 365. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure.

When Universal Print is deployed with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. For a guided simulation, go to [Universal Print guided simulation](https://regale.cloud/Microsoft/viewer/1265/index.html#/0/0).

Using the settings catalog in Intune, you can create a printer policy, and deploy the policy to your managed users and devices. Then, on their devices, end users select the printer from a list of registered Universal Print printers to print.

This feature applies to:

- Windows 11
- Windows 10 21H2 with [July 2022 update](https://support.microsoft.com/topic/july-12-2022-kb5015807-os-builds-19042-1826-19043-1826-and-19044-1826-8c8ea8fe-ec83-467d-86fb-a2f48a85eb41) and later

This article shows you how to create a Universal Print policy in Microsoft Intune. To learn more about Universal Print and onboarding, go to [What is Universal Print](/universal-print/fundamentals/universal-print-whatis) and [Set up Universal Print](/universal-print/fundamentals/universal-print-getting-started).

> [!TIP]
> The __PrintProvisioning__ tool and the __printers.csv__ file process is deprecated. Be sure to use the steps in this article to install universal printers.

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

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Win11: Universal Print policy**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select **Add settings**. In the settings picker, select **Printer Provisioning**, and select the settings you want to configure.

    :::image type="content" source="./media/settings-catalog-printer-provisioning/settings-picker-printer-provisioning.png" alt-text="Screenshot that shows how to select printer provisioning in the settings catalog to create a universal print policy in Microsoft Intune and Intune admin center.":::

    Close the settings picker.

8. Configure the settings:

    - **Action**: Select **Install** to install a printer. When users receive the policy, the printer will automatically install. Select **Uninstall** to uninstall a printer.
    - **Cloud Device ID**: Enter the printer ID. This ID is created when the printer is registered in Azure AD using the Universal Print service. To get the ID, use the [Universal Print portal](/universal-print/portal/navigate-up).
    - **Printer Shared ID**: Enter the Shared ID of the printer. To get the ID, use the [Universal Print portal](/universal-print/portal/navigate-up).
    - **Printer Shared Name**: Enter the Shared Name of the printer. To get the name, use the [Universal Print portal](/universal-print/portal/navigate-up).

    You can add more printers using the **Add** button:

    :::image type="content" source="./media/settings-catalog-printer-provisioning/add-printer.png" alt-text="Screenshot that shows how to add more printers to the universal print policy in the settings catalog in Microsoft Intune and Intune admin center.":::

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

For information on all the reporting data you can view, go to [Intune reports](../fundamentals/reports.md).

### Common issues

- When you deploy the printer policy, you might get a `Error 0x8007007f (ERROR_PROC_NOT_FOUND)` message.

  The `ERROR_PROC_NOT_FOUND` is a very common error, and is usually associated with the `DelayLoaded` DLLs missing or missing APIs.

  To resolve this error, make sure your Windows OS client version is supported. The supported versions are listed at the top of this article.

- If a printer is removed from the Universal Print service, unshared, or if permissions are removed, then the Intune policy will fail to install the printer.

- Make sure the printer is discoverable on the device. If users can't discover or install the printer manually, then the Intune policy will also fail to install the printer.

  For more information and possible steps, go to [Unable to discover printers on the client](https://supportability.visualstudio.com/WindowsUserExperience/_wiki/wikis/WindowsUserExperience/725155/Unable-to-discover-printers-on-the-client).  

- Make sure the **SharedID** and **PrinterID** are entered correctly in the Intune policy.

  In some cases, the PrinterID and SharedID are reversed, which prevents the printer from being discovered. For more information on these settings, go to [Create the policy](#create-the-policy) (in this article).

- The Application event log may shows errors related to Universal Print.

### Enable tracing

THIS SECTION IS STILL IN DRAFT

The following steps must be completed in an Administrator session on the session host to trace a user logging onto the session host and when trying to print to Universal Print.

1. On the client device, install Fiddler. For the specific steps, go to [Universal Print troubleshooting guide](/universal-print/fundamentals/universal-print-troubleshooting-support-howto).
2. On the client device, open a command prompt as administrator, and run `PrintTrace.cmd`.

    1. Gather [Fiddler trace](/universal-print/fundamentals/universal-print-troubleshooting-support-howto) and [Printtrace.cmd](https://supportability.visualstudio.com/WindowsUserExperience/_wiki/wikis/WindowsUserExperience?wikiVersion=GBmaster&pagePath=/UEX%20Wiki/Universal%20Print/Common%20Steps/How%20to%20run%20PrintTrace.cmd) of the client resyncing the Microsoft Intune package.

3. Make sure the the required CSP binaries are installed.

    1. On the device, open a command prompt as administrator, and go to the `System32` directory, which is usually `c:\windows\system32`.
    2. The `UPPrinterInstaller.exe` and `UPPrinterInstallsCSP.dll` files should be there. If they're not there, then NEED SOMETHING.

    2. Manually run the `UPPrinterInstaller.exe` file with your parameters and trace with __Fiddler__ and __PrintTrace.cmd.__ 

      For example, enter:
      
      `UPPritnerInstaller.exe -install -printersharedid E7CBB880-A194-450A-ACC7-86AEE809B971 -omadmaccountid 8A917C42-BE97-49EA-AD77-6EF9FE143E04 -correlationid 8A7E7CDE-D0EE-4C45-86FB-3570C3D5F81F")`

## Learn more

- [What is Universal Print](/universal-print/fundamentals/universal-print-whatis)
- [Use the settings catalog to configure settings on Windows and macOS devices](settings-catalog.md)
