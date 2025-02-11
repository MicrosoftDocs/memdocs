---
title: Enrollment for Microsoft Entra hybrid joined devices
titleSuffix: Windows Autopilot
description: Use Windows Autopilot to enroll Microsoft Entra hybrid joined devices in Microsoft Intune.
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: madakeva
ms.date: 02/11/2025
ms.topic: how-to
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
ms.collection:
  - M365-identity-device-management
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2025</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2022</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2019</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2016</a>
---

# Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot

> [!IMPORTANT]
>
> Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Windows Autopilot. For more information, see [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints: Which option is right for your organization](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined#which-option-is-right-for-your-organization).

Intune and Windows Autopilot can be used to set up Microsoft Entra hybrid joined devices. To do so, follow the steps in this article. For more information about Microsoft Entra hybrid join, see [Understanding Microsoft Entra hybrid join and co-management](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201).

## Requirements

The list of requirements for performing Microsoft Entra hybrid join during Windows Autopilot is organized into three different categories:

- **General** - general requirements.
- **Device enrollment** - device enrollment requirements.
- **Intune connector** - Intune Connector for Active Directory requirements.

Select the appropriate tab to see the relevant requirements:

### [:::image type="icon" source="images/icons/software-18.svg"::: **General**](#tab/general-requirements)

- Successfully configured the [Microsoft Entra hybrid joined devices](/azure/active-directory/devices/hybrid-azuread-join-plan). Be sure to [verify the device registration](/azure/active-directory/devices/howto-hybrid-join-verify) by using the [Get-MgDevice](/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice) cmdlet.
- If [Domain and OU-based filtering](/azure/active-directory/hybrid/how-to-connect-install-custom#domain-and-ou-filtering) is configured as part of Microsoft Entra Connect, ensure that the default organizational unit (OU) or container intended for the Autopilot devices is included in the sync scope.

### [:::image type="icon" source="images/icons/software-18.svg"::: **Device enrollment**](#tab/device-enrollemnt-requirements)

<!-- ### Device enrollment requirements -->

The device to be enrolled must follow these requirements:

- Use a currently supported version of Windows.
- Have access to the internet [following Windows Autopilot network requirements](./requirements.md?tabs=networking).
- Have access to an Active Directory domain controller.
- Successfully ping the domain controller of the domain being joined.
- If using Proxy, Web Proxy Auto-Discovery Protocol (WPAD) Proxy settings option must be enabled and configured.
- Undergo the out-of-box experience (OOBE).
- Use an authorization type that Microsoft Entra ID supports in OOBE.

Although not required, configuring Microsoft Entra hybrid join for Active Directory Federated Services (ADFS) enables a faster Windows Autopilot Microsoft Entra registration process during deployments. Federated customers that aren't supporting the use of passwords and using ADFS need to follow the steps in the article [Active Directory Federation Services prompt=login parameter support](/windows-server/identity/ad-fs/operations/ad-fs-prompt-login) to properly configure the authentication experience.

### [:::image type="icon" source="images/icons/software-18.svg"::: **Intune connector**](#tab/intune-connector-requirements)

<!-- ### Intune connector server requirements -->

- The Intune Connector for Active Directory, also known as the Offline Domain Join (ODJ) connector, must be installed on a computer that's running Windows Server 2016 or later with .NET Framework version 4.7.2 or later.

- The server hosting the Intune Connector for Active Directory must have access to the Internet and Active Directory.

    > [!NOTE]
    >
    > The Intune Connector for Active Directory server requires standard domain client access to domain controllers, which includes the RPC port requirements it needs to communicate with Active Directory. For more information, see the following articles:
    >
    > - [Service overview and network port requirements for Windows](/troubleshoot/windows-server/networking/service-overview-and-network-port-requirements)
    > - [How to configure a firewall for Active Directory domains and trusts](/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts)
    > - [Hybrid Identity Required Ports and Protocols](/azure/active-directory/hybrid/reference-connect-ports)

- To increase scale and availability, multiple connectors can be installed in a domain. Each connector must be able to create computer objects in the domain that it supports.

- The administrator installing the Intune Connector for Active Directory must be a local administrator on the server where the Intune Connector for Active Directory is being installed.

- For the updated Intune Connector for Active Directory, installation needs to be done with an account that has the following domain rights:

  - **Required** - Create **msDs-ManagedServiceAccount** objects in the Managed Service Accounts container
  - **Optional** - Modify permissions in OUs in Active Directory - if the administrator installing the updated Intune Connector for Active Directory doesn't have this right, additional configuration steps are required by an administrator who has these rights. For more information, see the section [Increase the computer account limit in the Organizational Unit](#increase-the-computer-account-limit-in-the-organizational-unit) in this article.

    These rights allow the Intune Connector for Active Directory install to properly create Managed Service Accounts (MSAs) and set permissions correctly for the OUs that the MSA is adding computers to.

<!-- MAXADO-8594181
Multi-domain support section removed
-->

- The Intune Connector for Active Directory requires the [same endpoints as Intune](/mem/intune/fundamentals/intune-endpoints).

---

## Set up Windows automatic MDM enrollment

1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Microsoft Entra ID**.

1. In the left hand pane, select **Manage** | **Mobility (MDM and WIP)** > **Microsoft Intune**.

1. Make sure users who deploy Microsoft Entra joined devices by using Intune and Windows are members of a group included in **MDM User scope**.

1. Use the default values in the **MDM Terms of use URL**, **MDM Discovery URL**, and **MDM Compliance URL** boxes, and then select **Save**.

## Install the Intune Connector for Active Directory

[!INCLUDE [Install the Intune Connector for Active Directory](includes/intune-connector.md)]

### Configure web proxy settings

If there's a web proxy in the networking environment, ensure that the Intune Connector for Active Directory works properly by referring to [Work with existing on-premises proxy servers](/mem/intune/enrollment/autopilot-hybrid-connector-proxy).

## Increase the computer account limit in the Organizational Unit

[!INCLUDE [Increase the computer account limit in the Organizational Unit](includes/computer-account-limit.md)]

## Create a device group

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New group**.

1. In the **Group** pane, select the following options:

    1. For **Group type**, select **Security**.

    1. Enter a **Group name** and **Group description**.

    1. Select a **Membership type**.

1. If **Dynamic Devices** is selected for the membership type, in the **Group** pane, select **Dynamic device members**.

1. Select **Edit** in the **Rule syntax** box and enter one of the following code lines:

    - To create a group that includes all Windows Autopilot devices, enter:

      `(device.devicePhysicalIDs -any _ -startsWith "[ZTDId]")`

    - Intune's Group Tag field maps to the OrderID attribute on Microsoft Entra devices. To create a group that includes all of Windows Autopilot devices with a specific Group Tag (OrderID), enter:

      `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`

    - To create a group that includes all Windows Autopilot devices with a specific Purchase Order ID, enter:

      `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`

1. Select **Save** > **Create**.

## Register Windows Autopilot devices

Select one of the following ways to enroll Windows Autopilot devices.

### Register Windows Autopilot devices that are already enrolled

1. Create a Windows Autopilot deployment profile with the setting **Convert all targeted devices to Autopilot** set to **Yes**.

1. Assign the profile to a group that contains the members that need to be automatically registered with Windows Autopilot.

For more information, see [Create an Autopilot deployment profile](profiles.md).

### Register Windows Autopilot devices that aren't enrolled

Devices that aren't yet enrolled into Windows Autopilot can be manually registered. For more information, see [Manual registration](manual-registration.md).

### Register devices from an OEM

If purchasing new devices, some OEMs can register the devices on behalf of the organization. For more information, see [OEM registration](oem-registration.md).

### Display registered Windows Autopilot device

Before devices enroll in Intune, *registered* Windows Autopilot devices are displayed in three places (with names set to their serial numbers):

- The **Windows Autopilot Devices** pane in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **By platform | Windows** > **Device onboarding | Enrollment**. Under **Windows Autopilot**, select **Devices**.
- The **Devices | All devices** pane in the [Azure portal](https://portal.azure.com). Select **Devices** > **All Devices**.
- The **Autopilot** pane in [Microsoft 365 admin center](https://admin.microsoft.com/). Select **Devices** > **Autopilot**.

After the Windows Autopilot devices are *enrolled*, the devices are displayed in four places:

- The **Devices | All Devices** pane in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **All devices**.
- The **Windows | Windows devices** pane in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **By platform | Windows**.
- The **Devices | All devices** pane in the [Azure portal](https://portal.azure.com). Select **Devices** > **All Devices**.
- The **Active devices** pane in [Microsoft 365 admin center](https://admin.microsoft.com/). Select **Devices** > **Active devices**.

> [!NOTE]
>
> After devices are enrolled, the devices are still displayed in the **Windows Autopilot Devices** pane in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and in the **Autopilot** pane in [Microsoft 365 admin center](https://admin.microsoft.com/), but those objects are the Windows Autopilot registered objects.

A device object is pre-created in Microsoft Entra ID once a device is registered in Windows Autopilot. When a device goes through a hybrid Microsoft Entra deployment, by design, another device object is created resulting in duplicate entries.

## VPNs

The following VPN clients are tested and validated:

- In-box Windows VPN client
- Cisco AnyConnect (Win32 client)
- Pulse Secure (Win32 client)
- GlobalProtect (Win32 client)
- Checkpoint (Win32 client)
- Citrix NetScaler (Win32 client)
- SonicWall (Win32 client)
- FortiClient VPN (Win32 client)

When using VPNs, select **Yes** for the **Skip AD connectivity check** option in the Windows Autopilot deployment profile. Always-On VPNs shouldn't require this option since it connects automatically.

> [!NOTE]
>
> This list of VPN clients isn't a comprehensive list of all VPN clients that work with Windows Autopilot. Contact the respective VPN vendor regarding compatibility and supportability with Windows Autopilot or regarding any issues with using a VPN solution with Windows Autopilot.

### Unsupported VPN clients

The following VPN solutions are **known** not to work with Windows Autopilot and therefore aren't supported for use with Windows Autopilot:

- UWP-based VPN plug-ins
- Anything that requires a user cert
- DirectAccess

> [!NOTE]
>
> Omission of a specific VPN client from this list doesn't automatically mean it's supported or that it works with Windows Autopilot. This list only lists the VPN clients that are **known** not to work with Windows Autopilot.

## Create and assign a Windows Autopilot deployment profile

Windows Autopilot deployment profiles are used to configure the Windows Autopilot devices.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment Profiles**.

1. In the **Windows Autopilot deployment profiles** screen, select the **Create Profile** drop down menu and then select **Windows PC**.

1. In the **Create profile** screen, on the **Basics** page, enter a **Name** and optional **Description**.

1. If all devices in the assigned groups should automatically register to Windows Autopilot, set **Convert all targeted devices to Autopilot** to **Yes**. All corporate owned, non-Windows Autopilot devices in assigned groups register with the Windows Autopilot deployment service. Personally owned devices aren't registered to Windows Autopilot. Allow 48 hours for the registration to be processed. When the device is unenrolled and reset, Windows Autopilot enrolls it again. After a device is registered in this way, disabling this setting or removing the profile assignment won't remove the device from the Windows Autopilot deployment service. Instead the devices need to be directly deleted. For more information, see [Delete Autopilot devices](add-devices.md#delete-autopilot-devices).

1. Select **Next**.

1. On the **Out-of-box experience (OOBE)** page, for **Deployment mode**, select **User-driven**.

1. In the **Join to Microsoft Entra ID as** box, select **Microsoft Entra hybrid joined**.

1. If deploying devices off of the organization's network using VPN support, set the **Skip Domain Connectivity Check** option to **Yes**. For more information, see [User-driven mode for Microsoft Entra hybrid join with VPN support](user-driven.md#user-driven-mode-for-microsoft-entra-hybrid-join-with-vpn-support).

1. Configure the remaining options on the **Out-of-box experience (OOBE)** page as needed.

1. Select **Next**.

1. On the **Scope tags** page, select [scope tags](/mem/intune/fundamentals/scope-tags) for this profile.

1. Select **Next**.

1. On the **Assignments** page, select **Select groups to include** > search for and select the device group > **Select**.

1. Select **Next** > **Create**.

> [!NOTE]
>
> Intune periodically checks for new devices in the assigned groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Windows Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Microsoft Entra groups, membership rules, hash of a device, Intune and Windows Autopilot service, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.

## (Optional) Turn on the enrollment status page

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Enrollment Status Page**.

1. In the **Enrollment Status Page** pane, select **Default** > **Settings**.

1. In the **Show app and profile installation progress** box, select **Yes**.

1. Configure the other options as needed.

1. Select **Save**.

## Create and assign a Domain Join profile

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices | Configuration** > **Policies** >**Create** > **New Policy**.

1. In the **create a profile** window that opens, enter the following properties:
    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile.
    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates**, select the template name **Domain Join**, and select **Create**.

1. Enter the **Name** and **Description** and select **Next**.

1. Provide a **Computer name prefix** and **Domain name**.

1. (Optional) Provide an **Organizational unit** (OU) in [DN format](/windows/desktop/ad/object-names-and-identities#distinguished-name). The options include:

    - Provide an OU in which control is delegated to the Windows device that is running the Intune Connector for Active Directory.
    - Provide an OU in which control is delegated to the root computers in organization's on-premises Active Directory.
    - If this field is left blank, the computer object is created in the Active Directory default container. The default container is normally the `CN=Computers` container. For more information, see [Redirect the users and computers containers in Active Directory domains](/troubleshoot/windows-server/identity/redirect-users-computers-containers).

    Valid examples:

      - `OU=SubOU,OU=TopLevelOU,DC=contoso,DC=com`
      - `OU=Mine,DC=contoso,DC=com`

    Invalid examples:

      - `CN=Computers,DC=contoso,DC=com` - a container can't be specified. Instead, leave the value blank to use the default for the domain.
      - `OU=Mine` - the domain must be specified via the `DC=` attributes.

    Make sure not to use quotation marks around the value in **Organizational unit**.

1. Select **OK** > **Create**. The profile is created and displayed in the list.

1. [Assign a device profile](/mem/intune/configuration/device-profile-assign#assign-a-policy-to-users-or-groups) to the same group used at the step [Create a device group](windows-autopilot-hybrid.md#create-a-device-group). Different groups can be used if there's a need to join devices to different domains or OUs.

> [!NOTE]
>
> The naming capability for Windows Autopilot for Microsoft Entra hybrid join doesn't support variables such as **%SERIAL%**. It only supports prefixes for the computer name.

## Uninstall the Intune Connector for Active Directory

The Intune Connector for Active Directory is installed locally on a computer via an executable file. If the Intune Connector for Active Directory needs to be uninstalled from a computer, it needs to also be done locally on the computer. The Intune Connector for Active Directory can't be removed through the Intune portal or through a graph API call.

To uninstall the Intune Connector for Active Directory from the server, select the appropriate tab for the version of the Windows Server OS and then follow the steps:

### [:::image type="icon" source="images/icons/software-18.svg"::: **Windows Server 2025**](#tab/windows-server-2025)

1. Sign into the computer hosting the Intune Connector for Active Directory.

1. Right-click on the **Start** menu and then select **Settings** > **Apps** > **Installed apps**.

    Or

    Select the following **Apps > Installed apps** shortcut:

    > [!div class="nextstepaction"]
    > [Open Apps > Installed apps](ms-settings:appsfeatures-app)

1. In the **Apps > Installed apps** window, find **Intune Connector for Active Directory**.

1. Next to **Intune Connector for Active Directory**, select **...** > **Uninstall**, and then select the **Uninstall** button.

1. The Intune Connector for Active Directory proceeds to uninstall.

1. In some cases, the Intune Connector for Active Directory might not fully uninstall until the original Intune Connector for Active Directory installer `ODJConnectorBootstrapper.exe` is run again. To verify that the Intune Connector for Active Directory is fully uninstalled, run the `ODJConnectorBootstrapper.exe` installer again. If it prompts to **Uninstall**, select to uninstall it. Otherwise, close the `ODJConnectorBootstrapper.exe` installer.

    > [!NOTE]
    >
    > The legacy **Intune Connector for Active Directory** installer can be downloaded from the [Intune Connector for Active Directory](https://www.microsoft.com/download/details.aspx?id=105392&msockid=3cb707200c316b2c119712450d8b6a5d) and should only be used for uninstalls. For new installs, use the [updated Intune Connector for Active Directory](windows-autopilot-hybrid.md?tabs=updated-connector#install-the-intune-connector-for-active-directory-on-the-server).

### [:::image type="icon" source="images/icons/software-18.svg"::: **Windows Server 2019/2022**](#tab/windows-server-2019-2022)

1. Sign into the computer hosting the Intune Connector for Active Directory.

1. Right-click the **Start** menu and then select **Settings** > **Apps**.

    Or

    Select the following **Apps** shortcut:

    > [!div class="nextstepaction"]
    > [Open Apps](ms-settings:appsfeatures)

1. Under **Apps & features**, find and select **Intune Connector for Active Directory**.

1. Under **Intune Connector for Active Directory**, select the **Uninstall** button, and then select the **Uninstall** button again.

1. The Intune Connector for Active Directory proceeds to uninstall.

1. In some cases, the Intune Connector for Active Directory might not fully uninstall until the original Intune Connector for Active Directory installer `ODJConnectorBootstrapper.exe` is run again. To verify that the Intune Connector for Active Directory is fully uninstalled, run the `ODJConnectorBootstrapper.exe` installer again. If it prompts to **Uninstall**, select to uninstall it. Otherwise, close the `ODJConnectorBootstrapper.exe` installer.

    > [!NOTE]
    >
    > The legacy **Intune Connector for Active Directory** installer can be downloaded from the [Intune Connector for Active Directory](https://www.microsoft.com/download/details.aspx?id=105392&msockid=3cb707200c316b2c119712450d8b6a5d) and should only be used for uninstalls. For new installs, use the [updated Intune Connector for Active Directory](windows-autopilot-hybrid.md?tabs=updated-connector#install-the-intune-connector-for-active-directory-on-the-server).

### [:::image type="icon" source="images/icons/software-18.svg"::: **Windows Server 2016**](#tab/windows-server-2016)

1. Sign into the computer hosting the Intune Connector for Active Directory.

1. Right-click the **Start** menu and then select **Settings** > **System** > **Apps & features**.

    Or

    Select the following **Apps** shortcut:

    > [!div class="nextstepaction"]
    > [Open Apps](ms-settings:appsfeatures)

1. Under **Apps & features**, find and select **Intune Connector for Active Directory**.

1. Under **Intune Connector for Active Directory**, select the **Uninstall** button, and then select the **Uninstall** button again.

1. The Intune Connector for Active Directory proceeds to uninstall.

1. In some cases, the Intune Connector for Active Directory might not fully uninstall until the original Intune Connector for Active Directory installer `ODJConnectorBootstrapper.exe` is run again. To verify that the Intune Connector for Active Directory is fully uninstalled, run the `ODJConnectorBootstrapper.exe` installer again. If it prompts to **Uninstall**, select to uninstall it. Otherwise, close the `ODJConnectorBootstrapper.exe` installer.

    > [!NOTE]
    >
    > The legacy **Intune Connector for Active Directory** installer can be downloaded from the [Intune Connector for Active Directory](https://www.microsoft.com/download/details.aspx?id=105392&msockid=3cb707200c316b2c119712450d8b6a5d) and should only be used for uninstalls. For new installs, use the [updated Intune Connector for Active Directory](windows-autopilot-hybrid.md?tabs=updated-connector#install-the-intune-connector-for-active-directory-on-the-server).

---

## Next steps

After Windows Autopilot is configured, learn how to manage those devices. For more information, see [What is Microsoft Intune device management?](/mem/intune/remote-actions/device-management).

## Related content

<!-- Intune 12378279 -->

- [What is a device identity?](/azure/active-directory/devices/overview).
- [Learn more about cloud-native endpoints](/mem/solutions/cloud-native-endpoints/cloud-native-endpoints-overview).
- [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined).
- [Tutorial: Set up and configure a cloud-native Windows endpoint with Microsoft Intune](/mem/solutions/cloud-native-endpoints/cloud-native-windows-endpoints).
- [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/device-join-plan).
- [A framework for Windows endpoint management transformation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/a-framework-for-windows-endpoint-management-transformation/ba-p/2460684).
- [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201).
- [Success with remote Windows Autopilot and hybrid Azure Active Directory join](https://techcommunity.microsoft.com/t5/intune-customer-success/success-with-remote-windows-autopilot-and-hybrid-azure-active/ba-p/2749353).
