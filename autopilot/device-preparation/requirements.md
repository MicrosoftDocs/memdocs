---
title: Windows Autopilot device preparation requirements
description: Software, Networking, Licensing, Configuration, and RBAC requirements for Windows Autopilot device preparation. # RSS subscription is based on this description so don't change. If the description needs to change, update RSS URL in the Tip in the article.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 01/24/2025
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier1
ms.topic: article
ms.custom:
  - CI 116757
  - CSSTroubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---


# Windows Autopilot device preparation requirements

> [!TIP]
>
> RSS can be used to notify when requirements are added or updated to this page. For example, the following RSS link includes this article:
>
> ``` url
> https://learn.microsoft.com/en-us/search/?terms=%22Software%2C%20Networking%2C%20Licensing%2C%20Configuration%2C%20and%20RBAC%20requirements%20for%20Windows%20Autopilot%20device%22
> ```
>
> This example includes the `&locale=en-us` variable. The `locale` variable is required, but it can be changed another supported locale. For example, `&locale=es-es`.
>
> For more information on using RSS for notifications, see [How to use the docs](/mem/use-docs#notifications) in the Intune documentation.

The list of requirements for Windows Autopilot device preparation is organized into five different categories:

- **Software** - OS requirements.
- **Networking** - networking requirements.
- **Licensing** - licensing requirements.
- **Configuration** - configurations required in Microsoft Entra ID and Microsoft Intune.
- **RBAC** - RBAC permissions required for a Windows Autopilot device preparation administrator.

Select the appropriate tab to see the relevant requirements:

## [:::image type="icon" source="../images/icons/software-18.svg"::: **Software**](#tab/software)

### Software requirements

Windows Autopilot device preparation depends on specific features available in Windows client, Microsoft Entra ID, and a mobile device management (MDM) service such as Microsoft Intune. To use Windows Autopilot device preparation and access these features, some software requirements must be met.

#### Windows 11

- Windows 11, version 24H2 or later
- Windows 11, version 23H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later - Windows installation media dated April 2024 or later has [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) included.
- Windows 11, version 22H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later - Windows installation media dated April 2024 or later has [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) included.

> [!IMPORTANT]
>
> - Verify with OEMs that devices shipped from the OEM have the minimum required update installed.
> - If installing Windows from installation media, verify that the media has the minimum required update installed. Updated Windows installation media with the latest cumulative update already installed is available at the [Volume Licensing Service Center (VLSC)](https://www.microsoft.com/licensing/ServiceCenter/Default.aspx).

The following editions are supported:

- Windows 11 Pro.
- Windows 11 Pro Education.
- Windows 11 Pro for Workstations.
- Windows 11 Enterprise.
- Windows 11 Education.
- [Windows 11 Enterprise LTSC](/windows/whats-new/ltsc/overview).

## [:::image type="icon" source="../images/icons/wifi-ethernet-18.svg"::: **Networking**](#tab/networking)

### Networking requirements

Windows Autopilot device preparation depends on various internet-based services. Access to these services must be provided for Windows Autopilot device preparation to function properly. In the simplest case, enabling proper functionality can be achieved by ensuring the following conditions:

- Ensure Domain Name Services (DNS) name resolution for internet DNS names.
- Allow access to all hosts via port 80 (HTTP), 443 (HTTPS), and 123 (UDP/NTP).

Additional configuration might be required to grant access to required services in environments that:

- Have more restrictive internet access.
- Require authentication before internet access can be obtained.

> [!NOTE]
>
> Smart card and certificate based authentication isn't supported during the out-of-box experience (OOBE). For more information, see [Smartcards and certificate-based authentication](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

#### Service requirements

Windows Autopilot device preparation relies on several different type of services to function properly. In order for these services to function properly, certain network configurations might need to be performed. These services and their required network configurations are as follows:

#### Windows Autopilot device preparation deployment service

After a network connection is in place, each Windows device will contact the Windows Autopilot device preparation deployment service. The following URLs are used:

- `https://ztd.dds.microsoft.com`
- `https://cs.dds.microsoft.com`
- `https://login.live.com`

#### Windows activation

Windows Autopilot device preparation requires Windows Activation services. For more information about the URLs that need to be accessible for the activation services, see [Windows activation or validation fails with error code 0x8004FE33](https://support.microsoft.com/topic/windows-activation-or-validation-fails-with-error-code-0x8004fe33-a9afe65e-230b-c1ed-3414-39acd7fddf52).

#### Microsoft Entra ID

Microsoft Entra ID validates user credentials. Additionally, the device is joined to Microsoft Entra ID during Windows Autopilot device preparation. For more information, see [Office 365 IP Address and URL Web service](/microsoft-365/enterprise/microsoft-365-ip-web-service).

#### Microsoft Intune

Once authenticated, Microsoft Entra ID triggers enrollment of the device into the Intune mobile device management (MDM) service. For more information about Intune's network communication requirements, see the following articles:

- [Intune network configuration requirements and bandwidth](/mem/intune-service/fundamentals/network-bandwidth-use).
- [Network endpoints for Microsoft Intune](/mem/intune-service/fundamentals/intune-endpoints).

#### Windows Autopilot device preparation automatic device diagnostics collection

For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` isn't blocked on the network. Diagnostics are available for 28 days before they're removed.

For more information, see [Collect diagnostics from a Windows device](/mem/intune-service/remote-actions/collect-diagnostics).

#### Windows Update

During the out-of-box experience (OOBE) process and after the Windows OS configuration, the Windows Update service retrieves needed updates. If there are problems connecting to Windows Update, see [Windows Update issues troubleshooting](/troubleshoot/windows-client/installing-updates-features-roles/windows-update-issues-troubleshooting).

If Windows Update is inaccessible, the Windows Autopilot device preparation process still continues but critical updates aren't available.

#### Delivery Optimization

Windows Autopilot device preparation contacts the [Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) service when downloading the applications and updates. This contact establishes peer-to-peer sharing of content so that only a few devices need to download it from the internet.

- Windows Updates.
- Microsoft Store applications and application updates.
- Office Updates.
- Intune Win32 Applications.

If the Delivery Optimization Service is inaccessible, the Autopilot process still continues with Delivery Optimization downloads from the cloud without peer-to-peer.

#### Network Time Protocol (NTP) sync

When a Windows device starts up, it talks to a network time server to ensure that the time on the device is correct. Ensure that UDP port **123** to `time.windows.com` is accessible.

#### Domain Name Services (DNS)

To resolve internet names for all services, the device communicates with a DNS server, typically provided via DHCP. This DNS server must be able to resolve internet names.

#### Diagnostics data

Diagnostic data collection is enabled by default. For more information, see [Manage enterprise diagnostic data](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-diagnostic-data-using-group-policy-and-mdm).

If the device can't send diagnostic data, the Windows Autopilot device preparation process still continues. However, services that depend on diagnostic data don't work.

#### Network Connection Status Indicator (NCSI)

Windows must be able to tell that the device can access the internet. For more information, see [Network Connection Status Indicator (NCSI)](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator).

`*.msftconnecttest.com` must be resolvable via DNS and accessible via HTTP.

#### Windows Notification Services (WNS)

This service is used to enable Windows to receive notifications from applications and services. For more information, see [Microsoft Store](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store).

If the WNS services aren't available, the Windows Autopilot device preparation process still continues without notifications.

#### Microsoft Store

Applications in the Microsoft Store can be pushed to the device by triggering them via Intune or other MDM service. App updates and additional applications might also be needed when the user first logs in. For more information, see [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-intune-integration-with-the-microsoft-store-on-windows/ba-p/3585077) and [FAQ: Supporting Microsoft Store experiences on managed devices](https://techcommunity.microsoft.com/t5/windows-management/faq-supporting-microsoft-store-experiences-on-managed-devices/m-p/3585286).

If the Microsoft Store isn't accessible, the Autopilot process still continues without Microsoft Store applications.

#### Microsoft 365

As part of the Intune device configuration, installation of Microsoft 365 Applications for enterprise might be required. For a list that includes all Office services, DNS names, IP addresses, including Microsoft Entra ID and other services that might overlap with the previously listed services, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges).

#### Certificate revocation lists (CRLs)

Some of these services also need to check certificate revocation lists (CRLs) for certificates used in the services. For a full list, see [Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges) and [Office 365 Certificate Chains](/microsoft-365/compliance/encryption-office-365-certificate-chains).

#### Proxy settings

Deploying proxy settings for Windows Autopilot device preparation should be configured on the proxy server itself. Implementing proxy settings via Intune policy isn't fully supported as it might cause issues and unexpected behavior with privileged access deployments.

## [:::image type="icon" source="../images/icons/license-18.svg"::: **Licensing**](#tab/licensing)

### Licensing requirements

Windows Autopilot device preparation depends on specific capabilities available in Windows client and Microsoft Entra ID. It also requires a mobile device management (MDM) service such as Microsoft Intune. These capabilities can be obtained through various editions and subscription programs.

To provide needed Microsoft Entra ID and MDM functionality, including automatic MDM enrollment and company branding features, one of the following subscriptions is required:

- [Microsoft 365 Business Premium subscription](https://www.microsoft.com/microsoft-365/business).
- [Microsoft 365 F1 or F3 subscription](https://www.microsoft.com/microsoft-365/enterprise/firstline).
- [Microsoft 365 Academic A1, A3, or A5 subscription](https://www.microsoft.com/education/products/microsoft-365).
- [Microsoft 365 Enterprise E3 or E5 subscription](https://www.microsoft.com/microsoft-365/enterprise), which include all Windows client, Microsoft 365, and EMS features (Microsoft Entra ID and Intune).
- [Enterprise Mobility + Security E3 or E5 subscription](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), which include all needed Microsoft Entra ID and Intune features.
- [Intune for Education subscription](/intune-education/what-is-intune-for-education), which include all needed Microsoft Entra ID and Intune features.
- [Microsoft Entra ID P1 or P2](https://azure.microsoft.com/services/active-directory/) and [Microsoft Intune subscription](https://www.microsoft.com/cloud-platform/microsoft-intune) or an alternative MDM service.

> [!NOTE]
>
> When a Microsoft 365 subscription is used, licenses still need to be assigned to users so they can enroll device in Intune. For more information, see [assign licenses to users so they can enroll devices in Intune](/mem/intune-service/fundamentals/licenses-assign).

Additionally, the following are also recommended, but not required:

- [Microsoft 365 Apps for enterprise](https://www.microsoft.com/microsoft-365/enterprise/microsoft-365-apps-for-enterprise-product) - Microsoft 365 Applications for enterprise can be deployed easily via Intune or other MDM service.
- [Windows Subscription Activation](/windows/deployment/windows-subscription-activation) - automatically step up devices from Windows Pro to Windows Enterprise edition.

## [:::image type="icon" source="../images/icons/configuration-18.svg"::: **Configuration**](#tab/configuration)

### Configuration requirements

Before Windows Autopilot device preparation can be used, some configuration tasks are required to support the common Autopilot scenarios.

- **Configure Microsoft Entra automatic enrollment**. For Microsoft Intune, see [Set up Windows automatic Intune enrollment](tutorial/user-driven/entra-join-automatic-enrollment.md) and [Enable Windows automatic enrollment](/mem/intune-service/enrollment/windows-enroll#enable-windows-automatic-enrollment) for details. If using a different mobile device management (MDM) service, contact the vendor for the specific URLs or configuration needed for those services.

- **The first user that signs in needs to have Microsoft Entra join permissions**. For more information, see [Allow users to join devices to Microsoft Entra ID](tutorial/user-driven/entra-join-allow-users-to-join.md).

The following configurations are optional but recommended. They aren't required:

- **Automatically step up from Windows Pro to Windows Enterprise**. For more information, see [Windows Subscription Activation](/windows/deployment/windows-subscription-activation).

There are no additional hardware requirements to use Autopilot, beyond the hardware requirements to run Windows. For more information, see:

- [Find Windows 11 specs, features, and computer requirements](https://www.microsoft.com/windows/windows-11-specifications).
- [Windows minimum hardware requirements](/windows-hardware/design/minimum/minimum-hardware-requirements-overview).
- [Windows 11 requirements](/windows/whats-new/windows-11-requirements).

## [:::image type="icon" source="../images/icons/permissions-18.svg"::: **RBAC**](#tab/rbac)

### Required RBAC permissions

The following role-based access control (RBAC) permissions are required in a role in Intune for a user to administer Windows Autopilot device preparation:

- **Device configurations**
  - Read
  - Delete
  - Assign
  - Create
  - Update

- **Enrollment programs**
  - Enrollment time device membership assignment

- **Managed apps**
  - Read

- **Mobile apps**
  - Read

- **Organization**
  - Read

To create a custom role with these permissions for use with Windows Autopilot device preparation:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Tenant administration** in the left hand pane.

1. In the **Tenant admin | Tenant status** screen, select **Roles**.

1. In the **Endpoint Manager roles | All roles** screen, make sure **All roles** is selected under **Manage**.

1. Select the **Create** drop down menu and then select **Intune role**. The **Add Custom Role** screen opens.

1. In the **Add Custom Role** screen:

   1. In the **Basics** page:

      1. **Name** - enter a name for the custom role, such as **Windows Autopilot device preparation administrator**.

      1. **Description** - enter a description for the custom role.

   1. Select **Next**.

   1. In the **Permissions** page, under **Select a category below to configure settings.**, scroll through the list to find the following settings. Once the setting is located, expand it, and then change to the following permissions:

      - **Device configurations**

         - **Read**: Yes
         - **Delete**: Yes
         - **Assign**: Yes
         - **Create**: Yes
         - **Update**: Yes

        **View Reports** can be left at the default of **No**.

      - **Enrollment programs**

         - **Enrollment time device membership assignment**: Yes

        All other permissions can be left at the default of **No**.

      - **Managed apps**

         - **Read**: Yes

        All other permissions can be left at the default of **No**.

      - **Mobile apps**

         - **Read**: Yes

        All other permissions can be left at the default of **No**.

      - **Organization**

         - **Read**: Yes

        All other permissions can be left at the default of **No**.

   1. Once all permissions are set correctly, select **Next**.

   1. In the **Scope tags** page, select **Next**.

        > [!NOTE]
        >
        > **Scope tags** are optional. If a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

   1. In the **Review + create** page, verify that all permissions are correct, and then select **Create**.

1. The new custom Windows Autopilot device preparation role can now be assigned to users who administer Windows Autopilot device preparation.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](/mem/intune-service/fundamentals/role-based-access-control).

---
