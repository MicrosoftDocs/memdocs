---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-domain-join-profile.md
user-driven/hybrid-azure-ad-join-domain-join-profile.md

Headings are driven by article context. -->

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **Manage devices**, select **Configuration**.

1. In the **Devices | Configuration** screen:

   1. At the top, make sure **Policies** is selected.

   1. Select the **Create** drop down menu and then select **New Policy**.

1. In the **Create a profile** window that opens:

   1. Under **Platform**, select **Windows 10 and later**.

   1. Under **Profile type**, select **Templates**.

   1. When the templates appear, under **Template name**, select **Domain join**. If **Domain join** isn't visible, scroll through the **Template name** list until **Domain join** is visible or search for **Domain join** in the **Search by profile name** box.

   1. Select **Create** to close the **Create a profile** window.

1. The **Domain Join** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the domain join profile.

   1. Next to **Description**, enter a description for the domain join profile.

   1. Select **Next**.

1. In the **Configuration settings** page:

   1. Next to **computer name prefix**, enter a prefix for computer names. This field is required. This prefix is used on all computer names. The rest of the computer name after the prefix is randomly generated up to 15 characters.

        > [!NOTE]
        >
        > This field doesn't support the **%SERIAL%** or **%RAND:x%** variables that can be used with the **Apply device name template** in the Microsoft Entra join scenario.

   1. Next to **Domain name**, enter the FQDN of the domain that devices should join. This field is required. Make sure to specify the FQDN of the domain and not the NETBIOS name of the domain. For example, enter in **contoso.com** and not just **CONTOSO**.

   1. Next to **Organizational unit**, enter the full path to the Organizational Unit (OU) in the domain that the computer accounts should be created in. For example, **OU=OU-Name,DC=contoso,DC=com**. This field is optional. If the OU isn't specified, the computer accounts are created in the **Computer** container.

        > [!NOTE]
        >
        > The OU specified in this step should be the same OU that permissions were set for and computer account limits increased in the step **Increase the computer account limit in the Organizational Unit (OU)**. Make sure that the step **Increase the computer account limit in the Organizational Unit (OU)** is followed for the OU specified in this field. Skipping the step that sets permissions correctly on the OU results in computers failing to join the domain.

        > [!IMPORTANT]
        >
        > If computers are joining the **Computers** container, leave this field blank. Don't specify the **Computers** container in this field via **CN=Computers,DC=contoso,DC=com**. The **Computers** container is a container and not an OU. When no OU is specified in this field and the field is left blank, devices automatically join the **Computers** container. If the **Computers** container is specified, it causes domain joins to fail.

   1. Once the settings in the **Configuration settings** page are complete, select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, select **Add all devices**.

        > [!NOTE]
        >
        > - Microsoft recommends selecting and assigning to **Add all devices** instead of selecting and assigning to the device group created in the **Create device group** step. Assigning to all devices ensures that the domain join profile works when using:
        >
        >   - [Windows Autopilot deployment for existing devices](../existing-devices/existing-devices-workflow.md) scenario.
        >   - A Windows Autopilot deployment that utilizes Microsoft Entra hybrid join and runs after the Windows Autopilot deployment for existing devices deployment.
        >
        > - Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** results in those devices being excluded and they don't receive the configuration profile.

   1. Under **Included groups** > **Groups**, ensure that **All devices** is selected, and then select **Next**.

1. In the **Applicability Rules** page, select **Next**. For this tutorial, applicability rules are being skipped. However if applicability rules are needed, do so at this screen. For more information about scope tags, see [Applicability rules](/mem/intune-service/configuration/device-profile-create#applicability-rules).

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then select **Create** to create the domain join profile.
