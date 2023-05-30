---
# required metadata

title: Import custom and third party partner ADMX templates in Microsoft Intune
description: You can add, upload, or import custom and third party partner ADMX and ADML files in Microsoft Intune. When they're imported, create a device configuration profile and assign the profile to your Windows 10/11 devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/05/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano, kabalu
ms.suite: ems
search.appverid: 
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management

---

# Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)

You can import custom and third party/partner ADMX and ADML templates into the Intune admin center. Once imported, you can create a device configuration policy using these settings, and then assign the policy to your managed devices.

This feature applies to:

- Windows 11
- Windows 10

This article shows you how to import custom ADMX and ADML files in the Intune admin center. For more information on administrative templates in Intune, go to [Use ADMX templates to configure policy settings in Microsoft Intune](administrative-templates-windows.md).

> [!TIP]
> The settings catalog has many settings natively built-in to Intune, including Google Chrome. For more information, go to:
>
> - [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](settings-catalog.md)
> - [Common tasks you can complete using the Settings Catalog](settings-catalog-common-features.md)

## What you need to know

- This feature is in [public preview](../fundamentals/public-preview.md).

- There are some limits:

  - A maximum of 10 ADMX files can be uploaded. Each file must be 1 MB or smaller.
  - For each ADMX file, only one ADML file can be uploaded.
  - Each ADMX file supports one language.

- Currently, only `en-us` ADML files are supported.

- Some ADMX files have dependency prerequisites. Import any dependency ADMX files first. If you upload an ADMX file without the dependency, an error message will list the missing namespace.

  For example, to import Mozilla Firefox ADMX and ADML files, you:

  1. Import the `mozilla.admx` and `mozilla.adml` files. Make sure the status shows **Available**.
  2. Import the `firefox.admx` and `firefox.adml` files.

  If you upload `firefox.admx` before `mozilla.adml`, then the import will fail.
  
  To see if your ADMX has a dependency, open the ADMX file in a text editor and look for `using prefix` in the `policyNamespaces` node. Any dependencies will be listed. 
  
  In the following example, the`kerberos.admx` file requires the `Windows.admx` file:
  
```xml
 <policyNamespaces>
    <target prefix="kerberos" namespace="Microsoft.Policies.Kerberos" />
    <using prefix="windows" namespace="Microsoft.Policies.Windows" />
  </policyNamespaces>
```

  To remove a dependency prerequisite, delete the associated ADMX file first. Then, delete the dependency prerequisite. In our Mozilla Firefox example, delete `firefox.admx` and then delete `mozilla.admx`.

- Some files may require `Windows.admx` as a prerequisite. This file must be uploaded first. In a future release (no ETA), this namespace will be automatically included and eventually not be required.

- Currently, the combo box setting type isn't supported. ADMX files with the combo box setting type will fail to import. All other setting types are supported.

- Not all areas of the registry can be set using custom ADMX. For more information on the registry locations that can be used, go to [Win32 and Desktop Bridge app ADMX policy Ingestion Overview](/windows/client-management/win32-and-centennial-app-policy-configuration#overview).

- ADMX settings that are built into Windows (located in the `C:\Windows\PolicyDefinitions` folder) are enabled through configuration service providers (CSPs). 

  - Don't import these built-in settings if your intent is to configure them. Instead, use the [settings catalog](settings-catalog.md) or a [custom profile](custom-settings-configure.md).
  - Do import these built-in settings if they're a required parent namespace of another file. 

  For a list of the ADMX backed CSP settings, go to [ADMX-backed policies in Policy CSP](/windows/client-management/mdm/policies-in-policy-csp-admx-backed).

## Download the ADMX templates

Download the ADMX templates you want to import. Save these files to an easily accessible folder, like `C:\ADMXTemplates`. Some common ADMX template downloads include:

- Adobe Reader
- Mozilla Firefox
- Zoom

## Add the ADMX and ADML files

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Windows** > **Configuration profiles** > **Import ADMX** > **Import**:

    :::image type="content" source="./media/administrative-templates-import-custom/import-admx.png" alt-text="Screenshot that shows how to add or import custom ADMX and ADML. Go to Devices > Configuration profiles > Import ADMX in Microsoft Intune and Intune admin center.":::

3. Upload your files:

    - **ADMX file**: Select the ADMX file you want to upload.
    - **ADML file for the default language**: Select the ADML file you want to upload. Remember, you can add only one language file for each ADMX file you upload. For any other limitations, go to [What you need to know](#what-you-need-to-know) (in this article).
    - **Specify the language of the ADML file**: Shows the ADML language of the file you uploaded.

4. Select **Next**.
5. In **Review + Create**, review your changes. Select **Create** to import the files.

When the import completes, your ADMX templates are shown in the list. You can also:

- Select **Refresh** to see the updated state.
- See the upload **Status**.
- **Delete** an imported template.

:::image type="content" source="./media/administrative-templates-import-custom/imported-templates-refresh-delete.png" alt-text="Screenshot that shows how to refresh and delete imported custom ADMX and ADML administrative templates in Microsoft Intune and Intune admin center.":::

## Create a profile using your imported files

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Imported Administrative templates (Preview)**:

      :::image type="content" source="./media/administrative-templates-import-custom/select-imported-administrative-templates.png" alt-text="Screenshot that shows how to select imported administrative templates to create a device configuration profile using the imported ADMX settings in Microsoft Intune and Intune admin center.":::

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **ADMX: Mozilla Firefox for Windows 10/11 devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, select and configure the settings you want in your policy. When finished, select **Next**.
8. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

9. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles in Intune](device-profile-assign.md).

    If the profile is assigned to user groups, then configured ADMX settings apply to any device that the user enrolls, and signs in to. If the profile is assigned to device groups, then configured ADMX settings apply to any user that signs into that device. This assignment happens if the ADMX setting is a computer configuration (`HKEY_LOCAL_MACHINE`), or a user configuration (`HKEY_CURRENT_USER`). With some settings, a computer setting assigned to a user may also impact the experience of other users on that device.

    For more information, see [User groups vs. device groups when assigning policies](device-profile-assign.md#user-groups-vs-device-groups).

    Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Replace existing ADMX files

If you upload an ADMX file with settings that are already imported, then the upload will fail.

For example, if you upload a different version of an ADMX file that has the same settings as the original ADMX file, then the upload will fail with a namespace error.

To update existing ADMX files that are imported, you have the following options:

- **Option 1: Replace the existing ADMX file**

  To replace an existing ADMX file with the same settings, you can use the following steps:

  1. Delete any profiles using the existing ADMX settings.
  2. Delete the original ADMX file you imported.
  3. Import the new ADMX and ADML files.

- **Option 2: Create a new ADMX file**

  1. Create another version of the ADMX file with the same namespace as the original ADMX file.
  2. Add the new and different settings to this ADMX file.
  3. Import the new ADMX and ADML files.

## Next steps

[Overview: Use ADMX templates to configure policy settings in Microsoft Intune](administrative-templates-windows.md)
