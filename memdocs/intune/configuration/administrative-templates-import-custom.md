---
# required metadata

title: Import custom and third party ADMX templates in Microsoft Intune
description: You can upload or import custom and third party partner ADMX and ADML files in Microsoft Intune and Endpoint Manager.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: 
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management

---

# Import custom ADMX and ADML administrative templates into Endpoint Manager

You can import custom and third party/partner ADMX and ADML templates into the Endpoint Manager admin center. Once imported, you can create a device configuration policy using these settings, and then assign the policy to your managed devices.

This feature applies to:

- Windows 11
- Windows 10

This article shows you how to import custom ADMX and ADML files in the Endpoint Manager admin center. For more information on administrative templates in Endpoint Manager, go to [Use ADMX templates to configure policy settings in Microsoft Intune](administrative-templates-windows.md).

## What you need to know

- This feature is in [public preview](public-preview.md).

- There are some limits:

  - A maximum of 10 packages can be uploaded. Each package file must be 1 MB or smaller.
  - For each ADMX file, only one ADML file can be uploaded.
  - Each ADMX package supports one language.

- Currently, only `en-us` ADML files are supported.

- If you upload an ADMX that already exists in the Endpoint Manager admin center, then the upload will fail. For example, the upload will fail if you try to upload a newer version of the same ADMX file.

  To replace an existing ADMX file:

  1. Delete any profiles using the existing ADMX settings.
  2. Delete the original ADMX file you imported.
  3. Import the new ADMX and ADML files.

- Some ADMX packages may have dependency prerequisites. You must import any dependency ADMX files first. For example, to import Mozilla Firefox ADMX and ADML files:

  1. Import the `mozilla.admx` and `mozilla.adml` files. Make sure the status shows **Available**.
  2. Import the `firefox.admx` and `firefox.adml` files.

  If you upload `firefox.admx` before `mozilla.adml`, then the import will fail.

  To remove a dependency prerequisite, delete the associated ADMX package first. Then, delete the dependency prerequisite. In our Mozilla Firefox example, delete `firefox.admx` and then delete `mozilla.admx`.

- ADMX files with unsupported setting types will fail to upload. For example, combo box settings won't upload.

  **QUESTION**: Do we have a list of unsupported settings types? If yes, we should include this info.

- New settings can be added to an existing namespace if the new settings are added as a new file with the already uploaded setting removed from the file.

  **QUESTION**: This sentence is confusing. I assume the namespace is in the ADMX file. Would this namespace also exist in a different ADMX file? If yes, how is that a "different" ADMX file? I assume the ADMX would fail to import as it would already exist. What about renaming the admx file (from filename1.admx to filename2.admx)? I suggest we have a call about this bullet.

## Download the ADMX templates

Download the ADMX templates you want to import. Save these files to an easily accessible folder, like `C:\ADMXTemplates`. Some common ADMX template downloads include:

- Adobe Reader
- Mozilla Firefox
- Zoom

## Add the ADMX and ADML files

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Custom administrative templates**:

    :::image type="content" source="./media/administrative-templates-import-custom/custom-administrative-templates.png" alt-text="To add or import custom ADMX and ADML, go to Devices > Configuration profiles > Custom administrative templates in Microsoft Intune and Endpoint Manager admin center.":::

3. Select **Import** and upload your files:

    - **ADMX file**: Select the ADMX file you want to upload.
    - **ADML file for the default language**: Select the ADMX file you want to upload. Remember, you can add only one language file for each ADMX file you upload. For any other limitations, go to [What you need to know](#what-you-need-to-know) (in this article).
    - **Specify the language of the ADML file**: Shows the ADML language of the file you uploaded.

4. Select **Next**.
5. In **Review + Create**, review your changes. Select **Create** to import the files.

When the import completes, the template is shown in the list. You can also:

- Select **Refresh** to see the updated state.
- See the upload **Status**.
- **Delete** an imported template.

:::image type="content" source="./media/administrative-templates-import-custom/imported-templates-refresh-delete.png" alt-text="You can refresh and delete imported custom ADMX and ADML administrative templates in Microsoft Intune and Endpoint Manager admin center.":::

## Create a profile using your imported files

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Imported Administrative templates (Preview)**:

      :::image type="content" source="./media/administrative-templates-import-custom/select-imported-administrative-templates.png" alt-text="Select imported administrative templates to create a device configuration profile using the imported ADMX settings in Microsoft Intune and Endpoint Manager admin center.":::

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

## Next steps

[Overview: Use ADMX templates to configure policy settings in Microsoft Intune](administrative-templates-windows.md)
