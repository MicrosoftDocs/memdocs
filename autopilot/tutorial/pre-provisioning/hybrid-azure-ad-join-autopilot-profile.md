---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 7 of 11 - Create and assign pre-provisioned Microsoft Entra hybrid join Autopilot profile
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join - Step 7 of 11 - Create and assign hybrid pre-provisioned Microsoft Entra join Autopilot profile.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Microsoft Entra hybrid join: Create and assign a pre-provisioned Microsoft Entra hybrid join Autopilot profile

Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join steps:

- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)

> [!div class="checklist"]
>
> - **Step 7: Create and assign Microsoft Entra hybrid join Autopilot profile**

- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join overview](hybrid-azure-ad-join-workflow.md#workflow).

## Create and assign a pre-provisioned Microsoft Entra hybrid join Autopilot profile

The Autopilot profile specifies how the device is configured during Windows Setup and what is shown during the out-of-box experience (OOBE).

The difference between a Microsoft Entra join and a Microsoft Entra hybrid join is that the Microsoft Entra hybrid join scenario joins both an on-premises domain and Microsoft Entra ID during Autopilot. The pre-provisioned Microsoft Entra join scenario only joins Microsoft Entra ID during Autopilot.

> [!TIP]
>
> For Configuration Manager admins, the Autopilot profile is similar to some of the configuration that takes place during a task sequence via an `unattend.xml` file. The unattend.xml file is configured during the **Apply Windows Settings** and **Apply Network Settings** steps. Note however that Autopilot doesn't use `unattend.xml` files.

To create a pre-provisioned Microsoft Entra hybrid join Autopilot profile, follow these steps:

[!INCLUDE [Autopilot profiles before steps](../includes/autopilot-profile-steps-before.md)]

8. In the **Out-of-box experience (OOBE)** page:

      - For **Deployment mode**, select **User-driven**.

      - For **Join to Microsoft Entra ID as**, select **Microsoft Entra hybrid joined**. After this option is selected, several the options underneath this option will change.

      - For **Skip AD connectivity check**, select **No**. This section of the tutorial assumes that the device undergoing Autopilot is an on-premises internal client and that has direct connectivity to the on-premises domain and domain controllers. For off-premise/Internet scenarios where VPN connectivity is required, see [Off-premises/Internet scenarios and VPN connectivity](#off-premisesinternet-scenarios-and-vpn-connectivity).

      - For **Microsoft Software License Terms**, select **Hide** to skip the EULA page.

      - For **Privacy settings**, select **Hide** to skip the privacy settings.

      - For **Hide change account options**, select **Hide**.

      - For **User account type**, select the desired account type for the user (**Administrator** or **Standard** user). If **Administrator** is chosen, the user is added to the local Admin group.

      - For **Allow pre-provisioned deployment**, select **Yes**.

      - For **Language (Region)**, select **Operating system default** to use the default language for the operating system being configured. If another language is desired, select the desired language from the drop-down list.

      - For **Automatically configure keyboard**, select **Yes** to skip the keyboard selection page.

      - The **Apply device name template** is greyed out for Microsoft Entra hybrid join scenarios. Although not as robust, device names can be specified during the [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md) step.

      > [!NOTE]
      >
      > The above settings are selected to minimize needed user interaction during device setup. However, some of the settings that are hidden can instead be shown as desired. For example, some regions might require that **Privacy settings** always be shown.

      > [!NOTE]
      >
      > If the language/region and keyboard screens are set to hidden, they might still be displayed if there's no network connectivity at the start of the Autopilot deployment. When there's no network connectivity at the start of the deployment, the Autopilot profile, where the settings to hide these screens is defined, hasn't downloaded yet. Once network connectivity is established, the Autopilot profile is downloaded and any additional screen settings should work as expected.

[!INCLUDE [Autopilot profiles after steps](../includes/autopilot-profile-steps-after.md)]

## Verify device has an Autopilot profile assigned to it

[!INCLUDE [How to verify a device has an Autopilot profile assigned to it in Intune](../includes/verify-autopilot-profile-assignment.md)]

## Off-premises/Internet scenarios and VPN connectivity

Windows Autopilot for pre-provisioned Microsoft Entra hybrid join supports off-premises/Internet scenarios where direct connectivity to Active directory and domain controllers isn't available. However, an off-premises/Internet scenario doesn't eliminate the need for connectivity to Active Directory and a domain controller during the domain join. In an off-premises/Internet scenario, connectivity to Active Directory and a domain controller can be established via a VPN connection during the Autopilot process.

For off-premises/Internet scenarios requiring VPN connectivity, the only change in the Autopilot profile would be in the setting **Skip AD connectivity check**. In the [Create and assign pre-provisioned Microsoft Entra hybrid join Autopilot profile](#create-and-assign-a-pre-provisioned-microsoft-entra-hybrid-join-autopilot-profile) section, the **Skip AD connectivity check** setting should be set to **Yes** instead of to **No**. Setting this option to **Yes** prevents the deployment from failing since there's no direct connectivity to Active Directory and domain controllers until the VPN connection is established.

In addition to changing the **Skip AD connectivity check** setting to **Yes** in the Autopilot profile, VPN support also relies on the following prerequisites:

- The VPN solution can be deployed and installed with Intune.
- The VPN solution needs to support one of the following options:
  - Lets the user manually establish a VPN connection from the Windows sign-in screen.
  - Automatically establishes a VPN connection as needed.

The VPN solution would need to be installed and configured via Intune during the Autopilot process. Configuration would need to include deploying any required device certificates if needed by the VPN solution. Once the VPN solution is installed and configured on the device, the VPN connection can be established, either automatically or manually by the user, at which point the domain join can occur. For more information and support on VPN solutions during Autopilot, consult the respective VPN vendor.

> [!NOTE]
>
> Some VPN configurations aren't supported because the connection isn't initiated until the user signs into Windows. Unsupported VPN configurations include:
>
> - VPN solutions that use user certificates
> - Non-Microsoft UWP VPN plug-ins from the Windows Store

## Next step: Configure and assign domain join profile

> [!div class="nextstepaction"]
> [Step 8: Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)

## Related content

[!INCLUDE [More information Autopilot profile](../includes/more-info-autopilot-profile.md)]
- [User-driven mode for Microsoft Entra hybrid join with VPN support](../../user-driven.md#user-driven-mode-for-microsoft-entra-hybrid-join-with-vpn-support).
- [VPNs](../../windows-autopilot-hybrid.md#vpns).
