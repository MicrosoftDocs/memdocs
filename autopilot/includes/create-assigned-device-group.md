---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 11/18/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

device-preparation/tutorial/user-driven/entra-join-device group.md

Headings are driven by article context. -->

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

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

       1. Scroll through the list of objects and select the service principal **Intune Provisioning Client** with AppId of **f1346770-5b25-470b-88bd-d5744ab7952c**. Alternatively, use the **Search** bar to search for and select **Intune Provisioning Client**.

           > [!NOTE]
           >
           > - In some tenants, the service principal might have the name of **Intune Autopilot ConfidentialClient** instead of **Intune Provisioning Client**. As long as the AppID of the service principal is **f1346770-5b25-470b-88bd-d5744ab7952c**, it's the correct service principal.
           >
           > - If the **Intune Provisioning Client** or **Intune Autopilot ConfidentialClient** service principal with AppId of **f1346770-5b25-470b-88bd-d5744ab7952c** isn't available either in the list of objects or when searching, see [Adding the Intune Provisioning Client service principal](#adding-the-intune-provisioning-client-service-principal).

       1. Once **Intune Provisioning Client** is selected as the owner, select **Select**.

    1. Select **Create** to finish creating the assigned device group.

    > [!IMPORTANT]
    >
    > Don't manually add any devices to the device group created in this step by selecting the **No members selected** link under **Members**. Devices are automatically added to this device group during the Windows Autopilot device preparation deployment.

### Adding the Intune Provisioning Client service principal

If the **Intune Provisioning Client** service principal with AppId **f1346770-5b25-470b-88bd-d5744ab7952c** isn't available when selecting the owner of the device group, then follow these steps to add the service principal:

1. On a device where Microsoft Intune or Microsoft Entra ID is normally administered, open a **Windows PowerShell** command prompt.

1. In the **Windows PowerShell** command prompt window:

   1. Install the **Microsoft.Graph.Authentication** module by entering the following command:

        ```powershell
        Install-Module Microsoft.Graph.Authentication
        ```

        If prompted to do so, select **Yes** to agree to install from the **PSGallery** untrusted repository. For more information, see [Microsoft.Graph.Authentication](/powershell/module/microsoft.graph.authentication/) and [Set-PSRepository -InstallationPolicy](/powershell/module/powershellget/set-psrepository#-installationpolicy).
    
    1. Install the **Microsoft.Graph.Applications** module by entering the following command:

        ```powershell
        Install-Module Microsoft.Graph.Applications
        ```

        If prompted to do so, select **Yes** to agree to install from the **PSGallery** untrusted repository. For more information, see [Microsoft.Graph.Applications](/powershell/module/microsoft.graph.applications/) and [Set-PSRepository -InstallationPolicy](/powershell/module/powershellget/set-psrepository#-installationpolicy).

   1. Once the **Microsoft.Graph.Authentication** and **Microsoft.Graph.Applications** modules are installed, connect to Microsoft Entra ID by entering the following command:

        ```powershell
        Connect-MgGraph
        ```

        For more information, see [Connect-MgGraph](/powershell/module/microsoft.graph.authentication/connect-mggraph).

   1. If not already authenticated to Microsoft Entra ID, the **Sign in to your account** window appears. Enter the credentials of a Microsoft Entra ID administrator that has permissions to add service principals.

   1. Once authenticated to Microsoft Entra ID, add the **Intune Provisioning Client** service principal by entering the following command:

        ```powershell
        New-MgServicePrincipal -BodyParameter f1346770-5b25-470b-88bd-d5744ab7952c
        ```

        For more information, see [New-MgServicePrincipal](/powershell/module/microsoft.graph.applications/new-mgserviceprincipal).
