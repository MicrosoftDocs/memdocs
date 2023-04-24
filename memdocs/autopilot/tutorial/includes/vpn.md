---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/24/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md
user-driven/hybrid-azure-ad-join-autopilot-profile.md

Headings are driven by article context. -->

Windows Autopilot for pre-provisioned hybrid Azure AD join supports off-premises/Internet scenarios where direct connectivity to Active directory and domain controllers isn't available. However, an off-premises/Internet scenario doesn't eliminate the need for connectivity to Active Directory and a domain controller during the domain join. In an off-premises/Internet scenario, connectivity to Active Directory and a domain controller can be established via a VPN connection during the Autopilot process.

For off-premises/Internet scenarios requiring VPN connectivity, the only change in the Autopilot profile would be in the setting **Skip AD connectivity check**. In the [Create and assign pre-provisioned hybrid Azure AD join Autopilot profile](#create-and-assign-a-pre-provisioned-hybrid-azure-ad-join-autopilot-profile) section, the **Skip AD connectivity check** setting should be set to **Yes** instead of to **No**. Setting this option to **Yes** prevents the deployment from failing since there's no direct connectivity to Active Directory and domain controllers until the VPN connection is established.

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