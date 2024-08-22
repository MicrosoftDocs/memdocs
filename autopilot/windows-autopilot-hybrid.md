---
title: Enrollment for Microsoft Entra hybrid joined devices
titleSuffix: Windows Autopilot
description: Use Windows Autopilot to enroll Microsoft Entra hybrid joined devices in Microsoft Intune.
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: jubaptis
ms.date: 08/22/2024
ms.topic: how-to
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
ms.collection:
  - M365-identity-device-management
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot

> [!IMPORTANT]
>
> Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Autopilot. For more information, see [Microsoft Entra joined vs. Microsoft Entra hybrid joined in cloud-native endpoints: Which option is right for your organization](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined#which-option-is-right-for-your-organization).

Intune and Windows Autopilot can be used to set up Microsoft Entra hybrid joined devices. To do so, follow the steps in this article. For more information about Microsoft Entra hybrid join, see [Understanding Microsoft Entra hybrid join and co-management](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201).

## Prerequisites

- Successfully configured the [Microsoft Entra hybrid joined devices](/azure/active-directory/devices/hybrid-azuread-join-plan). Be sure to [verify the device registration](/azure/active-directory/devices/howto-hybrid-join-verify) by using the [Get-MgDevice](/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice) cmdlet.
- If [Domain and OU-based filtering](/azure/active-directory/hybrid/how-to-connect-install-custom#domain-and-ou-filtering) is configured as part of Microsoft Entra Connect, ensure that the default organizational unit (OU) or container intended for the Autopilot devices is included in the sync scope.

### Device enrollment prerequisites

The device to be enrolled must follow these requirements:

- Use a currently supported version of Windows.
- Have access to the internet [following Windows Autopilot network requirements](./requirements.md?tabs=networking).
- Have access to an Active Directory domain controller.
- Successfully ping the domain controller of the domain being joined.
- If using Proxy, Web Proxy Auto-Discovery Protocol (WPAD) Proxy settings option must be enabled and configured.
- Undergo the out-of-box experience (OOBE).
- Use an authorization type that Microsoft Entra ID supports in OOBE.

Although not required, configuring Microsoft Entra hybrid join for Active Directory Federated Services (ADFS) enables a faster Windows Autopilot Microsoft Entra registration process during deployments. Federated customers that aren't supporting the use of passwords and using AD FS need to follow the steps in the article [Active Directory Federation Services prompt=login parameter support](/windows-server/identity/ad-fs/operations/ad-fs-prompt-login) to properly configure the authentication experience.

### Intune connector server prerequisites

- The Intune Connector for Active Directory must be installed on a computer that's running Windows Server 2016 or later with .NET Framework version 4.7.2 or later.

- The server hosting the Intune Connector must have access to the Internet and Active Directory.

    > [!NOTE]
    >
    > The Intune Connector server requires standard domain client access to domain controllers, which includes the RPC port requirements it needs to communicate with Active Directory. For more information, see the following articles:
    >
    > - [Service overview and network port requirements for Windows](/troubleshoot/windows-server/networking/service-overview-and-network-port-requirements)
    > - [How to configure a firewall for Active Directory domains and trusts](/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts)
    > - [Hybrid Identity Required Ports and Protocols](/azure/active-directory/hybrid/reference-connect-ports)

- To increase scale and availability, multiple connectors can be installed in the environment. We recommend installing the Connector on a server that's not running any other Intune connectors. Each connector must be able to create computer objects in any domain that needs to be supported.

<!-- MAXADO-8594181 -->

- If the organization has multiple domains and multiple Intune Connectors are installed, a domain service account that can create computer objects in all domains must be used. This requirement is true even if Microsoft Entra hybrid join is only implemented for a specific domain. If these domains are untrusted domains, the connectors must be uninstalled from domains where Windows Autopilot isn't used. Otherwise, with multiple connectors across multiple domains, all connectors must be able to create computer objects in all domains.

  This connector service account must have the following permissions:

  - [**Log on as a service**](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service).
  - Must be part of the **Domain user** group.
  - Must be a member of the local **Administrators** group on the Windows server that hosts the connector.

  > [!IMPORTANT]
  >
  > Managed service accounts aren't supported for the service account. The service account must be a domain account.

- The Intune Connector requires the [same endpoints as Intune](/mem/intune/fundamentals/intune-endpoints).

## Set up Windows automatic MDM enrollment

1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Microsoft Entra ID**.

1. In the left hand pane, select **Manage** | **Mobility (MDM and WIP)** > **Microsoft Intune**.

1. Make sure users who deploy Microsoft Entra joined devices by using Intune and Windows are members of a group included in **MDM User scope**.

1. Use the default values in the **MDM Terms of use URL**, **MDM Discovery URL**, and **MDM Compliance URL** boxes, and then select **Save**.

## Increase the computer account limit in the Organizational Unit

The Intune Connector for Active Directory creates autopilot-enrolled computers in the on-premises Active Directory domain. The computer that hosts the Intune Connector must have the rights to create the computer objects within the domain.

In some domains, computers aren't granted the rights to create computers. Additionally, domains have a built-in limit (default of 10) that applies to all users and computers that aren't delegated rights to create computer objects. The rights must be delegated to computers that host the Intune Connector on the organizational unit where Microsoft Entra hybrid joined devices are created.

The organizational unit that has the rights to create computers must match:

- The organizational unit entered in the Domain Join profile.
- If no profile is selected, the computer's domain name for the organization's domain.

1. Open **Active Directory Users and Computers (DSA.msc)**.

1. Right-click the organizational unit to use to create Microsoft Entra hybrid joined computers > **Delegate Control**.

    :::image type="content" source="./media/windows-autopilot-hybrid/delegate-control.png" alt-text="Screenshot of the Delegate Control command.":::

1. In the **Delegation of Control** wizard, select **Next** > **Add** > **Object Types**.

1. In the **Object Types** pane, select the **Computers** > **OK**.

    :::image type="content" source="./media/windows-autopilot-hybrid/object-types-computers.png" alt-text="Screenshot of the Object Types pane.":::

1. In the **Select Users, Computers, or Groups** pane, in the **Enter the object names to select** box, enter the name of the computer where the Connector is installed.

    :::image type="content" source="./media/windows-autopilot-hybrid/enter-object-names.png" alt-text="Screenshot of the Select Users, Computers, or Groups pane.":::

1. Select **Check Names** to validate the entry > **OK** > **Next**.

1. Select **Create a custom task to delegate** > **Next**.

1. Select **Only the following objects in the folder** > **Computer objects**.

1. Select **Create selected objects in this folder** and **Delete selected objects in this folder**.

    :::image type="content" source="./media/windows-autopilot-hybrid/only-following-objects.png" alt-text="Screenshot of the Active Directory Object Type pane.":::

1. Select **Next**.

1. Under **Permissions**, select the **Full Control** check box. This action selects all the other options.

    :::image type="content" source="./media/windows-autopilot-hybrid/full-control.png" alt-text="Screenshot of the Permissions pane.":::

1. Select **Next** > **Finish**.

## Install the Intune Connector

Before beginning the installation, make sure that all of the [Intune connector server prerequisites](#intune-connector-server-prerequisites) are met.

### Install steps

1. By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends to turn off Internet Explorer Enhanced Security Configuration.  To turn off Internet Explorer Enhanced Security Configuration:

   1. On the server where the Intune Connector is being installed, open **Server Manager**.

   1. In the left pane of Server Manager, select **Local Server**.

   1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

   1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** screen, select **Add**.

1. Follow the instructions to download the Connector.

1. Open the downloaded Connector setup file, *ODJConnectorBootstrapper.exe*, to install the Connector.

1. At the end of the setup, select **Configure Now**.

1. Select **Sign In**.

1. Enter the credentials of an Intune administrator role. The user account must have an assigned Intune license.

> [!NOTE]
>
> The Intune administrator role is a temporary requirement at the time of installation.

After authenticating, the Intune Connector for Active Directory finishes installing. Once it finishes installing, verify that it is active in Intune by following these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. Confirm that the connection status in the **Status** column is **Active**.

> [!NOTE]
>
> - After signing into the Connector, it can take several minutes to appear in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). It appears only if it can successfully communicate with the Intune service.
>
> - Inactive Intune connectors still appear in the Intune Connectors page and will automatically be cleaned up after 30 days.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

> [!NOTE]
>
> The Intune Connector originally logged in the **Event Viewer** directly under **Applications and Services Logs** in a log called **ODJ Connector Service**. However, logging for the Intune Connector has since moved to the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. If the **ODJ Connector Service** log at the original location is empty or not updating, check the new path location instead.

### Configure web proxy settings

If there is a web proxy in the networking environment, ensure that the Intune Connector for Active Directory works properly by referring to [Work with existing on-premises proxy servers](/mem/intune/enrollment/autopilot-hybrid-connector-proxy).

## Create a device group

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New group**.

1. In the **Group** pane, select the following options:

    1. For **Group type**, select **Security**.

    1. Enter a **Group name** and **Group description**.

    1. Select a **Membership type**.

1. If **Dynamic Devices** is selected for the membership type, in the **Group** pane, select **Dynamic device members**.

1. Select **Edit** in the **Rule syntax** box and enter one of the following code lines:

    - To create a group that includes all Autopilot devices, enter:

      `(device.devicePhysicalIDs -any _ -startsWith "[ZTDId]")`

    - Intune's Group Tag field maps to the OrderID attribute on Microsoft Entra devices. To create a group that includes all of Autopilot devices with a specific Group Tag (OrderID), enter:

      `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`

    - To create a group that includes all Autopilot devices with a specific Purchase Order ID, enter:

      `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`

1. Select **Save** > **Create**.

## Register Autopilot devices

Select one of the following ways to enroll Autopilot devices.

### Register Autopilot devices that are already enrolled

1. Create an Autopilot deployment profile with the setting **Convert all targeted devices to Autopilot** set to **Yes**.

1. Assign the profile to a group that contains the members that need to be automatically registered with Autopilot.

For more information, see [Create an Autopilot deployment profile](profiles.md).

### Register Autopilot devices that aren't enrolled

Devices that aren't yet enrolled into Windows Autopilot can be manually registered. For more information, see [Manual registration](manual-registration.md).

### Register devices from an OEM

If purchasing new devices, some OEMs can register the devices on behalf of the organization. For more information, see [OEM registration](oem-registration.md).

### Display registered Autopilot device

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

A device object is pre-created in Microsoft Entra ID once a device is registered in Autopilot. When a device goes through a hybrid Microsoft Entra deployment, by design, another device object is created resulting in duplicate entries.

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

## Create and assign an Autopilot deployment profile

Autopilot deployment profiles are used to configure the Autopilot devices.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Deployment Profiles**.

1. In the **Windows Autopilot deployment profiles** screen, select the **Create Profile** drop down menu and then select **Windows PC**.

1. In the **Create profile** screen, on the **Basics** page, enter a **Name** and optional **Description**.

1. If all devices in the assigned groups should automatically register to Windows Autopilot, set **Convert all targeted devices to Autopilot** to **Yes**. All corporate owned, non-Autopilot devices in assigned groups register with the Autopilot deployment service. Personally owned devices aren't registered to Autopilot. Allow 48 hours for the registration to be processed. When the device is unenrolled and reset, Autopilot enrolls it again. After a device is registered in this way, disabling this setting or removing the profile assignment won't remove the device from the Autopilot deployment service. Instead the devices need to be directly deleted. For more information, see [Delete Autopilot devices](add-devices.md#delete-autopilot-devices).

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
> Intune periodically checks for new devices in the assigned groups, and then begin the process of assigning profiles to those devices. Due to several different factors involved in the process of Autopilot profile assignment, an estimated time for the assignment can vary from scenario to scenario. These factors can include Microsoft Entra groups, membership rules, hash of a device, Intune and Autopilot service, and internet connection. The assignment time varies depending on all the factors and variables involved in a specific scenario.

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

    - Provide an OU in which control is delegated to the Windows device that is running the Intune Connector.
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

## Uninstall the ODJ Connector

The ODJ connector is installed locally on a computer via an executable file. If the ODJ connector needs to be uninstalled from a computer, it needs to also be done locally on the computer. The ODJ connector can't be removed through the Intune portal or through a graph API call.

To uninstall the ODJ Connector from the computer, follow these steps:

1. Sign into the computer hosting the ODJ connector.
1. Right-click on the **Start** menu and select **Settings**.
1. In the **Windows Settings** window, select **Apps**.
1. Under **Apps & features**, find and select **Intune Connector for Active Directory**.
1. Under **Intune Connector for Active Directory**, select the **Uninstall** button, and then select the **Uninstall** button again.
1. The ODJ connector proceeds to uninstall.

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
