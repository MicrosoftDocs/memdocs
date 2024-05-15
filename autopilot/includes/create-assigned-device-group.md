---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 05/27/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

device-preparation/tutorial/user-driven/entra-join-device group.md

Headings are driven by article context. -->

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Groups** in the left hand pane.

1. In the **Groups | All groups** screen, make sure **All groups** is selected, and then select **New group**.

1. In the **New Group** screen that opens:

    1. For **Group type**, select **Security**.

    1. For **Group name**, enter a name for the device group, such as **Windows Autopilot device preparation device group**.

    1. For **Group description**, enter a description for the device group.

    1. For **Microsoft Entra roles can be assigned to the group**, select **No**.

    1. For **Membership type**, select **Assigned**.

    1. For **Owners**, select the **No owners selected** link.

    1. In the **Add owners** screen that opens:

       1. Scroll through the list of objects and select **Intune Provisioning Client**. Alternatively, use the **Search** bar to search for and select **Intune Provisioning Client**.

           > [!NOTE]
           >
           > If the **Intune Provisioning Client** object isn't available either in the list of objects or when searching, see [Adding the Intune Provisioning Client object](#adding-the-intune-provisioning-client-object).

       1. Once **Intune Provisioning Client** is selected as the owner, select the **Select** button.



    1. Select the **Create** button to finish creating the assigned device group.

    > [!IMPORTANT]
    >
    > Don't manually add any devices to the device group created in this step by selecting the **No members selected** link under **Members**. Devices will be automatically added to this device group during the Windows Autopilot device preparation deployment.

### Adding the Intune Provisioning Client object

If the **Intune Provisioning Client** object isn't available when selecting the owner of the device group, then follow these steps to add the object:

1. On a device that where Microsoft Intune or Microsoft Entra ID is normally administered, open a **Windows PowerShell** command prompt.

1. In the **Windows Powershell** command prompt window:

   1. Install the **azuread** module by entering the following command:

        ```powershell
        install-module azuread
        ```

    If prompted to do so, agree to install **NuGet** and to install **azuread** module from **PSGallery**.

   1. Once the **azuread** module is installed, connect to Microsoft Entra ID by entering the following command:

        ```powershell
        Connect-AzureAD
        ```

   1. If not already authenticated to Microsoft Entra ID, the **Sign in to your account** window appears. Enter the credentials of a Microsoft Entra ID administrator that has permissions to add objects.

   1. Once authenticated to Microsoft Entra ID, add the **Intune Provisioning Client** object by entering the following command:

        ```powershell
        New-AzureADServicePrincipal -AppId f1346770-5b25-470b-88bd-d5744ab7952c
        ```
