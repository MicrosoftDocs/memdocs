---
# required metadata

title: Use Intune to manage Microsoft Defender settings on devices that aren't enrolled with Intune
description: Learn how to use Intune policy to manage Microsoft Defender security settings on devices that aren't enrolled with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/25/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: laarrizz

---

# Use Intune endpoint security policies to manage Microsoft Defender for Endpoint on devices not enrolled with Intune

When you integrate Microsoft Intune with Microsoft Defender for Endpoint, you can use Intune endpoint security policies to manage the Defender security settings on devices that aren't enrolled with Intune. This capability is known as *Defender for Endpoint security settings management*.

When you manage devices through security settings management:

- You can use the *Microsoft Intune admin center* or the *Microsoft 365 Defender portal* to manage Intune endpoint security policies for Defender for Endpoint and assign those policies to Microsoft Entra ID groups. The Defender portal includes the user interface for device views, policy management, and reports for security settings management.

  To manage policies from within the Defender portal, see [Manage endpoint security policies in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/manage-security-policies?toc=/mem/intune/toc.json&bc=/mem/breadcrumb/toc.json) in the Defender content.

- Devices get their assigned policies based on their Microsoft Entra ID device object. A device that isn't already registered in Microsoft Entra is joined as part of this solution.

- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the device's status. The device's status is available in the Microsoft Intune admin center and the Microsoft Defender portal.

This scenario extends the Microsoft Intune Endpoint Security surface to devices that aren't capable of enrolling in Intune. When a device is managed by Intune (enrolled to Intune) the device doesn't process policies for Defender for Endpoint security settings management. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

Applies to:

- Windows 10 and Windows 11
- Windows Server (2012 R2 and up)
- Linux
- macOS

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview-2.png" alt-text="Conceptual presentation of the Microsoft Defender for Endpoint-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview-2.png":::

## Prerequisites

Review the following sections for requirements for the Defender for Endpoint security settings management Scenario.

### Environment

When a supported device onboards to Microsoft Defender for Endpoint:

- The device is surveyed for an existing Microsoft Intune presence, which is a mobile device management (MDM) enrollment to Intune.
- Devices without an Intune presence enable the security settings management feature.
- For devices that aren't fully Microsoft Entra registered, a synthetic device identity is created in Microsoft Entra ID that allows the device to retrieve policies. Fully registered devices use their current registration.
- Policies retrieved from Microsoft Intune are enforced on the device by Microsoft Defender for Endpoint.

Security settings management isn't yet supported with Government clouds. For more information, see [Feature parity with commercial](/microsoft-365/security/defender-endpoint/gov#feature-parity-with-commercial) in *Microsoft Defender for Endpoint for US Government customers*.

### Connectivity requirements

Devices must have access to the following endpoint:

- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

### Supported platforms

Policies for Microsoft Defender for Endpoint security management are supported for the following device platforms:

**Linux**:

With [Microsoft Defender for Endpoint for Linux](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-linux#system-requirements) agent version **101.23052.0009** or later, security settings management supports the following Linux distributions:

- Red Hat Enterprise Linux 7.2 or higher  
- CentOS 7.2 or higher  
- Ubuntu 16.04 LTS or higher LTS  
- Debian 9 or higher  
- SUSE Linux Enterprise Server 12 or higher  
- Oracle Linux 7.2 or higher  
- Amazon Linux 2  
- Fedora 33 or higher

To confirm the version of the Defender agent, in the Defender portal go to the devices page, and on the devices *Inventories* tab, search for *Defender for Linux*. For guidance on updating the agent version, see [Deploy updates for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-updates).

*Known issue*: With the Defender agent version **101.23052.0009**, Linux devices fail to enroll when they're missing the following filepath: `/sys/class/dmi/id/board_vendor`.

*Known issue*: When a Linux device performs synthetic registration the Device Entra ID (formerly known as Device AAD ID) will not be visible in the Defender portal. This information can be viewed from the Intune or Entra portals. Administrators will still be able to manage devices with policies in this manner. 


**macOS**:

With [Microsoft Defender for Endpoint for macOS](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-mac#system-requirements) agent version **101.23052.0004** or later, security settings management supports the following macOS versions:

- macOS 14 (Sonoma)
- macOS 13 (Ventura)
- macOS 12 (Monterey)
- macOS 11 (Big Sur)

To confirm the version of the Defender agent, in the Defender portal go to the devices page, and on the devices *Inventories* tab, search for *Defender for macOS*. For guidance on updating the agent version, see [Deploy updates for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-updates).

*Known issue*: With the Defender agent version **101.23052.0004**, macOS devices that are registered in Microsoft Entra ID before enrolling with security settings management receive a duplicate Device ID in Microsoft Entra ID, which is a synthetic registration. When you create a Microsoft Entra group for targeting policy, you must use the synthetic Device ID created by security settings management. In Microsoft Entra ID, the *Join Type* column for the synthetic Device ID  is blank.

*Known issue*: When a macOS device performs synthetic registration the Device Entra ID (formerly known as Device AAD ID) will not be visible in the Defender portal. This information can be viewed from the Intune or Entra portals. Administrators will still be able to manage devices with policies in this manner. 

**Windows**:

- Windows 10 Professional/Enterprise (with [KB5023773](https://support.microsoft.com/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23))
- Windows 11 Professional/Enterprise (with [KB5023778](https://support.microsoft.com/topic/march-28-2023-kb5023778-os-build-22621-1485-preview-d490bb51-492e-410c-871f-50ad01b0f765))
- Windows Server 2012 R2 with [Microsoft Defender for Down-Level Devices](/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2016 with [Microsoft Defender for Down-Level Devices](/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2019 (with [KB5025229](https://support.microsoft.com/topic/april-11-2023-kb5025229-os-build-17763-4252-e8ead788-2cd3-4c9b-8c77-d677e2d8744f))
- Windows Server 2022 (with [KB5025230](https://support.microsoft.com/topic/april-11-2023-security-update-kb5025230-5048ddfb-7bf3-4e6c-b29a-7b44b789d282))
- Domain controllers (preview). See important information in [Use of security settings management on domain controllers](#use-of-security-settings-management-on-domain-controllers) (in this article).

Security settings management doesn't work on and isn't supported with the following devices:

- Non-persistent desktops, like Virtual Desktop Infrastructure (VDI) clients
- Azure Virtual Desktop (AVD and formerly Windows Virtual Desktop, WVD)
- 32-bit versions of Windows

### Licensing and subscriptions

To use security settings management, you need:

- A subscription that grants licenses for Microsoft Defender for Endpoint, like Microsoft 365, or a standalone license for only Microsoft Defender for Endpoint. A subscription that grants Microsoft Defender for Endpoint licenses also grants your tenant access to the Endpoint security node of the Microsoft Intune admin center.

  > [!NOTE]
  >
  > **Exception**: If you have access to Microsoft Defender for Endpoint *only* through Microsoft Defender for servers (part of Microsoft Defender for Cloud, formerly Azure Security Center), the security settings management functionality isn't available. You will need to have at least one Microsoft Defender for Endpoint (user) subscription license active.

  The Endpoint security node is where you configure and deploy policies to manage Microsoft Defender for Endpoint for your devices and monitor device status.

  For current information about options, see [Minimum requirements for Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/minimum-requirements?view=o365-worldwide&preserve-view=true).

### Role-based access controls (RBAC)

For guidance on assigning the right level of permissions and rights to administrators who manage Intune endpoint security policies from within the Intune admin center, see [Assign-role-based-access-controls-for-endpoint-security-policy](endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy).

## Architecture

The following diagram is a conceptual representation of the Microsoft Defender for Endpoint security configuration management solution.

:::image type="content" alt-text="Conceptual diagram of the Microsoft Defender for Endpoint security configuration management solution" source="./media/mde-security-integration/mde-architecture-2.png" lightbox="./media/mde-security-integration/mde-architecture-2.png":::

1. Devices onboard to Microsoft Defender for Endpoint.
2. Devices communicate with Intune. This communication enables Microsoft Intune to distribute policies that are targeted to the devices when they check in.
3. A registration is established for each device in Microsoft Entra ID:
   - If a device previously was fully registered, like a Hybrid Join device, the existing registration is used.
   - For devices that aren't registered, a synthetic device identity is created in Microsoft Entra ID to enable the device to retrieve policies. When a device with a synthetic registration has a full Microsoft Entra registration created for it, the synthetic registration is removed and the devices management continues on uninterrupted by using the full registration.
4. Defender for Endpoint reports the status of the policy back to Microsoft Intune.

> [!IMPORTANT]
>
> Security settings management uses a synthetic registration for devices that don't fully register in Microsoft Entra ID, and drops the Microsoft Entra hybrid join prerequisite. With this change, Windows devices that previously had enrollment errors will begin onboarding to Defender and then receive and process the security settings management policies.
>
> To filter for devices that were unable to enroll due to failing to meet the Microsoft Entra hybrid join prerequisite, navigate to the **Devices** list in the Microsoft Defender portal, and filter by enrollment status. Because these devices are not fully registered, their device attributes show **MDM** = **Intune** and **Join Type** = **Blank**. These devices will now enroll with security settings management using the synthetic registration.
>
> After enrolling these devices appear in the device lists for Microsoft Defender, Microsoft Intune, and Microsoft Entra portals. While the devices won't be fully registered with Microsoft Entra, their synthetic registration counts as one device object.

<a name='what-to-expect-in-the-microsoft-365-defender-portal'></a>

### What to expect in the Microsoft Defender portal

You can use the Microsoft Defender for Endpoint *Device inventory* to confirm a device is using the security settings management capability in Defender for Endpoint, by reviewing the devices status in the **Managed by** column. The *Managed by* information is also available on the devices side-panel or device page. *Managed by* should consistently indicate that its managed by **MDE**.  

You can also confirm a device is enrolled in *security settings management* successfully by confirming that the device-side panel or device page display **MDE Enrollment status** as **Success**.

:::image type="content" source="./media/mde-security-integration/defender-enrollment-validation.png" alt-text="A screenshot of a devices security settings management enrollment status on the device page in the Microsoft Defender portal." lightbox="./media/mde-security-integration/defender-enrollment-validation.png":::

If the **MDE Enrollment** status doesn't display **Success**, make sure you're looking at a device that was updated and is in scope for security settings management. (You configure the scope on the Enforcement scope page while configuring security settings management.)

### What to expect in the Microsoft Intune admin center

In the Microsoft Intune admin center, go to the All Devices page. Devices enrolled with security settings management appear here as in the Defender portal. In the admin center, the devices Managed by field should display MDE.

:::image type="content" source="./media/mde-security-integration/intune-enrollment-validation.png" alt-text="A screenshot of the device page in the Intune admin center with the Managed by status of the device highlighted." lightbox="./media/mde-security-integration/intune-enrollment-validation.png" :::

> [!TIP]
>
> In June 2023, security settings management began using synthetic registration for devices that don't fully register in Microsoft Entra. With this change, devices that previously had enrollment errors will begin onboarding  to Defender and then receive and process the security settings management policies.

### What to expect in the Microsoft Azure portal

On the *All devices* page In the Microsoft Azure portal, you can view device details.

:::image type="content" source="./media/mde-security-integration/azure-enrollment-validation.png" alt-text="A screenshot of the All device page in the Microsoft Azure portal with an example device highlighted." lightbox="./media/mde-security-integration/azure-enrollment-validation.png":::

To ensure that all devices enrolled in Defender for Endpoint security settings management receive policies, we recommend creating a [dynamic Microsoft Entra group](../fundamentals/groups-add.md) based on the devices' OS Type. With a dynamic group, devices that are managed by Defender for Endpoint are automatically added to the group without requiring admins to perform other tasks, like creating a new policy.

> [!IMPORTANT]
>
> From July 2023 to September 25, 2023, security settings management ran an opt-in public preview that introduced new behavior for devices that were managed and enrolled to the scenario. Starting on September 25, 2023, the public preview behavior became generally available and now applies to all tenants that use security settings management.
>
> If you used security settings management prior to September 25, 2023, and did not join the opt-in public preview that ran from July 2023 to September 25, 2023, review your Microsoft Entra groups that rely on system labels to make changes that will identify new devices you manage with security settings management. This is because prior to September 25, 2023, devices not managed through the opt-in public preview would use the following system labels (tags) of *MDEManaged* and *MDEJoined* to identify managed devices. These two system labels are no longer supported and are no longer added to devices that enroll.

Use the following guidance for your Dynamic groups:

- (Recommended) When targeting policy, use dynamic groups based on the device platform by using the *deviceOSType* attribute (Windows, Windows Server, macOS, Linux) to ensure policy continues to be delivered for devices that change management types, for example during MDM enrollment.

- If necessary, dynamic groups containing exclusively devices that are managed by Defender for Endpoint can be targeted by defining a dynamic group using the *managementType* attribute **MicrosoftSense**. Use of this attribute targets all devices that are managed by Defender for Endpoint via the security settings management functionality, and devices remain in this group only while managed by Defender for Endpoint.

Also, when configuring security settings management, if you intend to manage entire OS platform fleets using Microsoft Defender for Endpoint, by selecting **all devices** instead of **tagged devices** in the Microsoft Defender for Endpoint Enforcement Scope page, understand that any synthetic registrations are counted against Microsoft Entra ID quotas the same as full registrations.

## Which solution should I use?

Microsoft Intune includes several methods and policy types to manage the configuration of Defender for Endpoint on devices. The following table identifies the Intune policies and profiles that support deployment to devices managed by Defender for Endpoint security settings management and can help you identify if this solution is right for your needs.

When you deploy an endpoint security policy that's supported for both *Defender for Endpoint security settings management* and *Microsoft Intune*, a single instance of that policy can be processed by:

- Devices supported through security settings management (Microsoft Defender)
- Devices that are managed by either Intune or Configuration Manager.

Profiles for the *Windows 10 and later platform* aren't supported for devices managed by security settings management.

Following profiles are supported for each device type:

### Linux

The following policy types support the *Linux* platform.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus                            | Microsoft Defender Antivirus | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus                            | Microsoft Defender Antivirus exclusions | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Endpoint detection and response | Endpoint detection and response | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |

### macOS

The following policy types support the *macOS* platform.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus                            | Microsoft Defender Antivirus            | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus                            | Microsoft Defender Antivirus exclusions | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Endpoint detection and response | Endpoint detection and response |  ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |

### Windows

To support use with Microsoft Defender security settings management, your policies for Windows devices must use the *Windows* platform. Each profile for the *Windows* platform can apply to devices that are managed by Intune and to devices that are managed by security settings management.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus              | Defender Update controls               | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus              | Microsoft Defender Antivirus           | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus              | Microsoft Defender Antivirus exclusions| ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus              | Windows Security Experience            | *Note 1*                                                       | ![Supported](./media/mde-security-integration/green-check.png) |
| Attack Surface Reduction | Attack Surface Reduction Rules       | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
|Attack Surface Reduction|Device Control                          | *Note 1*                                                       | ![Supported](./media/mde-security-integration/green-check.png) |
| Endpoint detection and response | Endpoint detection and response | ![Supported](./media/mde-security-integration/green-check.png)| ![Supported](./media/mde-security-integration/green-check.png)|
| Firewall               | Firewall                               | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Firewall               | Firewall Rules                         | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |

***1*** - This profile is visible in the Defender portal but isn't supported for devices managed only by Microsoft Defender through the Microsoft Defender security settings management scenario. This profile is supported only for devices managed by Intune.

**Each Intune endpoint security profile** is a discrete group of settings intended for use by security admins who focus on protecting devices in your organization. The following are descriptions of the profiles that are supported by the security settings management scenario:

- **[Antivirus](endpoint-security-antivirus-policy.md)** policies manage the security configurations found in Microsoft Defender for Endpoint.

  > [!NOTE]
  >
  > While endpoints do not require a restart in order to apply modified settings or new policies, we are aware of an issue where the *AllowOnAccessProtection* and *DisableLocalAdminMerge* settings might at times require end users to restart their devices for these settings to update. We are currently investigating this issue in order to provide a resolution.

- **[Attack surface reduction (ASR)](endpoint-security-asr-policy.md)** policies focus on minimizing the places where your organization is vulnerable to cyberthreats and attacks. With security settings management, ASR rules apply to devices that run *Windows 10*, *Windows 11*, and *Windows Server*.

  For current guidance about which settings apply to the different platforms and versions, see [ASR rules supported operating systems](/microsoft-365/security/defender-endpoint/attack-surface-reduction-rules-reference#asr-rules-supported-operating-systems) in the Windows Threat protection documentation.

  > [!TIP]
  >
  > To help keep supported endpoints up to date, consider using the [modern unified solution](/microsoft-365/security/defender-endpoint/configure-server-endpoints#onboarding-steps-summary) for Windows Server 2012 R2 and 2016.

  Also see:
  - [Overview of attack surface reduction](/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation.

- **[Endpoint detection and response (EDR)](endpoint-security-edr-policy.md)** policies manage the Defender for Endpoint capabilities that provide advanced attack detections that are near real-time and actionable. Based on EDR configurations, security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

- **[Firewall](endpoint-security-firewall-policy.md)** policies focus on the Defender firewall on your devices.

- **Firewall Rules** are a type of profile for [Firewall](endpoint-security-firewall-policy.md) policy that are comprised of are granular rules for Firewalls, including specific ports, protocols, applications, and networks.

## Configure your tenant to support Defender for Endpoint security settings management

To support security settings management through the Microsoft Intune admin center, you must enable communication between them from within each console.

The following sections guide you through that process.

### Configure Microsoft Defender for Endpoint

In the Microsoft Defender portal, as a security administrator:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope** and enable the platforms for security settings management.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-defender.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft Defender portal." lightbox="./media/mde-security-integration/enable-mde-settings-management-defender.png#lightbox":::

   > [!NOTE]
   >
   > If you have the *Manage security settings in Security Center* permission in the Microsoft Defender portal, and are simultaneously enabled to view devices from all Device Groups (no [role-based access control](/microsoft-365/security/defender-endpoint/rbac) limits on your user permissions), you can also perform this action.

2. Initially, we recommend testing the feature for each platform by selecting the platforms option for **On tagged devices**, and then tagging the devices with the `MDE-Management` tag.

   > [!IMPORTANT]
   >
   > Use of [*Microsoft Defender for Endpoint's Dynamic tag capability*](/microsoft-365/security/defender/configure-asset-rules?view=o365-worldwide&preserve-view=true) to tag devices with *MDE-Management* isn't currently supported with security settings management. Devices tagged through this capability won't successfully enroll. This issue remains under investigation.

   > [!TIP]
   >
   > Use the proper device tags to test and validate your rollout on a small number of devices.
   >
   > When deploying to the *All devices* group, any device that falls into the scope configured will automatically be enrolled.
   >
   > While most devices complete enrollment and apply assigned policy within a few minutes, a device can sometimes take up to 24 hours to complete enrollment.

3. Configure the feature for Microsoft Defender for Cloud onboarded devices and Configuration Manager authority settings to fit your organization's needs:

   :::image type="content" source="./media/mde-security-integration/pilot-CMAuthority-mde-settings-management-defender.png" alt-text="Configure Pilot mode for Endpoint settings management in the Microsoft Defender portal." lightbox="./media/mde-security-integration/pilot-CMAuthority-mde-settings-management-defender.png" :::

   > [!TIP]
   >
   > To ensure your Microsoft Defender portal users have consistent permissions across portals, if not already provided, request that your IT administrator grant them the Microsoft Intune **Endpoint Security Manager** [built-in RBAC role](../fundamentals/role-based-access-control.md).

### Configure Intune

In the Microsoft Intune admin center, your account needs permissions equal to Endpoint Security Manager built-in Role based access control (RBAC) role.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-mem.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft Intune admin center." lightbox="./media/mde-security-integration/enable-mde-settings-management-mem.png" :::

   When you set this option to *On*, all devices in the platform scope for Microsoft Defender for Endpoint that aren't managed by Microsoft Intune qualify to onboard to Microsoft Defender for Endpoint.

## Onboard devices to Microsoft Defender for Endpoint

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboard to Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/onboarding) in the Defender for Endpoint documentation.

## Coexistence with Microsoft Configuration Manager

In some environments it might be desired to use security settings management with devices managed by Configuration Manager. If you use both, you need to control policy through a single channel. Use of more than one channel creates the opportunity for conflicts and undesired results.

To support this, configure the *Manage Security settings using Configuration Manager* toggle to *Off*. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope**:

:::image type="content" source="./media/mde-security-integration/disable-configuration-manager-toggle.png" alt-text="Screen shot of the Defender portal showing the Manage Security settings using Configuration Manager toggle set to Off." lightbox="./media/mde-security-integration/disable-configuration-manager-toggle.png" :::

## Create Microsoft Entra Groups

After devices onboard to Defender for Endpoint, you'll need to create device groups to support deployment of policy for Microsoft Defender for Endpoint. To identify devices that have enrolled with Microsoft Defender for Endpoint but aren't managed by Intune or Configuration Manager:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **All devices**, and then select the column **Managed by** to sort the view of devices. 

   Devices that onboard to Microsoft Defender for Endpoint and have registered but aren't managed by Intune display **Microsoft Defender for Endpoint** in the *Managed by* column. These are the devices that can receive policy for security management for Microsoft Defender for Endpoint.

   Starting on September 25, 2023, devices that use security management for Microsoft Defender for Endpoint can no longer be identified by using the following system labels:

   - **MDEJoined** - A now deprecated tag that was previously added to devices that were joined to the directory as part of this scenario.
   - **MDEManaged** - A now deprecated tag that was previously added to devices that actively used the security management scenario. This tag is removed from the device if Defender for Endpoint stops managing the security configuration.

   Instead of using system labels, you can use the management type attribute, and configure it to **MicrosoftSense**.

You can create groups for these devices [in Microsoft Entra](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) or [from within the Microsoft Intune admin center](../fundamentals/groups-add.md). When creating groups, you can use the **OS** value for a device if you're deploying policies to devices running Windows Server vs devices that run a client version of Windows:  

- **Windows 10 and Windows 11** - The deviceOSType or OS displays as *Windows*
- **Windows Server** - The deviceOSType or OS displays as *Windows Server*
- **Linux Device** - The deviceOSType or OS displays as *Linux*

### Sample Intune Dynamic Groups with Rule Syntax

**Windows Workstations**:

:::image type="content" source="./media/mde-security-integration/windowworkstation.jpg" alt-text="A screenshot of the Intune Dynamic Group for Windows Workstations." lightbox="./media/mde-security-integration/windowworkstation.jpg":::

**Windows Servers**:

:::image type="content" source="./media/mde-security-integration/windowsserver.jpg" alt-text="A screenshot of the Intune Dynamic Group for Windows Servers." lightbox="./media/mde-security-integration/windowsserver.jpg":::

**Linux Devices**:

:::image type="content" source="./media/mde-security-integration/linuxdevices.jpg" alt-text="A screenshot of the Intune Dynamic Group for Windows Linux." lightbox="./media/mde-security-integration/linuxdevices.jpg":::

> [!IMPORTANT]
> In May 2023, *deviceOSType* updated to distinguish between *Windows clients* and *Windows Servers*.
>
> Custom scripts and [Microsoft Entra dynamic device groups](/azure/active-directory/enterprise-users/groups-dynamic-membership) created before this change that specify rules that reference only *Windows* might exclude *Windows Servers* when used with the Security Management for Microsoft Defender for Endpoint solution. For example:
>
> - If you have a rule that uses the `equals` or `not equals` operator to identify *Windows*, this change will affect your rule. That is because previously both *Windows* and *Windows Server* were reported as *Windows*. To continue to include both, you must update the rule to also reference *Windows Server*.
> - If you have a rule that use the `contains` or `like` operator to specify *Windows*, then the rule won't be affected by this change. These operators can find both *Windows* and *Windows Server*.

> [!TIP]
>
> Users that are delegated the ability to manage endpoint security settings may not have the ability to implement tenant-wide configurations in Microsoft Intune.  Check with your Intune administrator for more information on roles and permissions in your organization.

## Deploy policy

After creating one or more Microsoft Entra groups that contain devices managed by Microsoft Defender for Endpoint, you can create and deploy the following policies for security settings management to those groups. The policies and profiles available vary by platform.

For the list of policy and profile combinations supported for security settings management, see the chart in [Which solution should I use](#which-solution-should-i-use), found in this article.

> [!TIP]
> Avoid deploying multiple policies that manage the same setting to a device.
>
> Microsoft Intune supports deploying multiple instances of each endpoint security policy type to the same device, with each policy instance being received by the device separately. Therefore, a device might receive separate configurations for the same setting from different policies, which results in a conflict. Some settings (like Antivirus Exclusions) will merge on the client and apply successfully.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Endpoint security**, select the type of policy you want to configure, and then select **Create Policy**.

3. For the policy, select the Platform and the Profile that you want to deploy. For a list of the Platforms and Profiles that support security settings management, see the chart in [Which solution should I use?](#which-solution-should-i-use) earlier in this article.

   > [!NOTE]
   >
   > The supported profiles apply to devices that communicate through Mobile Device Management (MDM) with Microsoft Intune and devices that communicate using the Microsoft Defender for Endpoint client.
   >
   > Ensure you review your targeting and groups as necessary.

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, select the settings you want to manage with this profile.

   To learn more about a setting, expand its *information* dialog and select the **Learn more** link to view the on-line Configuration Service Provider (CSP) documentation or related details, for that setting.

   When you're done configuring settings, select **Next**.

7. On the **Assignments** page, select the Microsoft Entra groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next** to continue.

   > [!TIP]
   >
   > - Assignment filters are not supported for devices managed by security settings management.
   > - Only *Device Objects* are applicable for Microsoft Defender for Endpoint management. Targeting users is not supported.
   > - Policies configured will apply to both Microsoft Intune and Microsoft Defender for Endpoint clients.

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. You can validate that settings were applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples) command utility.

## Monitor status

Status and reports for policies that target devices in this channel are available from the policy node under Endpoint security in the Microsoft Intune admin center.

Drill in to the policy type and then select the policy to view its status. You can view the list of platforms, policy types, and profiles that support security settings management in the table in [Which solution should I use](#which-solution-should-i-use), earlier in this article.

When you select a policy, you can view information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Frequently asked questions and considerations

### Device check-in frequency

Devices managed by this capability check-in with Microsoft Intune every 90 minutes to update policy.

You can manually sync a device on-demand from the [Microsoft Defender portal](https://security.microsoft.com/). Sign-in to the portal and go to **Devices**. Select a device that is managed by Microsoft Defender for Endpoint, and then select the **Policy sync** button:  

:::image type="content" source="./media/mde-security-integration/policy-sync-from-mde.png" alt-text="Manually sync devices managed by Microsoft Defender for Endpoint." lightbox="./media/mde-security-integration/policy-sync-from-mde.png"  :::

The Policy sync button only appears for devices that are successfully managed by Microsoft Defender for Endpoint.

### Devices protected by tamper protection

If a device has tamper protection turned on, it isn't possible to edit the values of [Tamper-protected settings](/microsoft-365/security/defender-endpoint/prevent-changes-to-security-settings-with-tamper-protection#what-happens-when-tamper-protection-is-turned-on) without disabling Tamper Protection first.

### Assignment Filters and security settings management

Assignment filters aren't supported for devices communicating through the Microsoft Defender for Endpoint channel. While assignment filters can be added to a policy that could target these devices, the devices ignore assignment filters. For assignment filter support, the device must be enrolled in to Microsoft Intune.

### Deleting and removing devices

You can delete devices that use this flow using one of two methods:

- From within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **All devices**, select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column, and then select **Delete**.
- You can also remove devices from the scope of Configuration Management in the Security Center.

Once a device is removed from either location, that change propagates to the other service.

### Unable to enable the Security Management for Microsoft Defender for Endpoint workload in Endpoint Security

While initial provisioning flows can be completed by an Administrator with permissions in both services, the following roles are sufficient to complete configurations in each separate service:

- For Microsoft Defender, use the Security Administrator role.
- For Microsoft Intune, use the Endpoint Security Manager role.

### Microsoft Entra joined devices

Devices that are joined to Active Directory use their **existing infrastructure** to complete the Microsoft Entra hybrid join process.

### Unsupported security settings

The following security settings are pending deprecation. The Defender for Endpoint security settings management flow doesn't support these settings:

- Expedite telemetry reporting frequency (under **Endpoint Detection and Response**)
- AllowIntrusionPreventionSystem (under **Antivirus**)
- Tamper Protection (under **Windows Security Experience**). This setting isn't pending deprecation, but is currently not supported.

### Use of security settings management on domain controllers

Currently in preview, security settings management is now supported on domain controllers. To manage security settings on domain controllers, you must enable it in the enforcement scope page (go to **Settings** > **Endpoints** **Enforcement scope**). Windows Server devices must be enabled before you can enable configuration of domain controllers. Additionally, if the *on tagged devices* option is selected for Windows Servers, configuration of domain controllers is limited to tagged devices, too. 

> [!CAUTION]
> - Misconfiguration of domain controllers could have a negative impact on both your security posture and operational continuity.
> - If configuration of domain controllers is enabled in your tenant, make sure to review all Windows policies to make sure you're not unintentionally targeting Microsoft Entra device groups that contain domain controllers. To minimize risk to productivity, firewall policies aren't supported on domain controllers. 
> - We recommend reviewing all policies targeted to domain controllers before unenrolling those devices. Make any required configurations first, and then unenroll your domain controllers. Defender for Endpoint configuration is maintained on each device after the device is unenrolled.


### Server Core installation

Security settings management doesn't support Server core installations due to Server core platform limitations.

### PowerShell restrict mode

PowerShell needs to be enabled.

Security settings management doesn't work for a device that has PowerShell *LanguageMode* configured with *ConstrainedLanguage* mode `enabled`. For more information, see [about_Language_Modes](/powershell/module/microsoft.powershell.core/about/about_language_modes) in the PowerShell documentation.

### Managing security through MDE if you were previously using a third party security tool

If you previously had a third-party security tool on the machine and are now managing it with MDE, you might see some impact on MDE's capability to manage Security settings in rare cases. In such cases, as a troubleshooting measure, uninstall and reinstall the latest version of MDE on your machine.

## Next steps

- [Monitor Defender for Endpoint in Intune](advanced-threat-protection-monitor.md)
- [Manage endpoint security policies in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/manage-security-policies) in the Defender documentation.
