---
# required metadata

title: Use Intune to manage Microsoft Defender security settings management on devices not enrolled with Microsoft Intune 
description: Use Intune profiles to manage security settings management for Microsoft Defender for Endpoint on devices supported by Defender that don't enroll with Microsoft Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

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
ms.reviewer: laarrizz

zone_pivot_groups: mde-attach-preview

---

<!--  PIVOTS in use:
    - id: mdssc-ga
      title: Generally Available
    - id: mdssc-preview
      title: Opt-in Public Preview
-->
# Manage Microsoft Defender for Endpoint on devices with Microsoft Intune

When you use Microsoft Defender for Endpoint, you can  deploy policies from Microsoft Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. This capability is known as *Defender for Endpoint security settings management*.

::: zone pivot="mdssc-ga"
**The following describes behavior that is generally available.**
::: zone-end

::: zone pivot="mdssc-preview"
**The following describes behavior for the opt-in public preview.**
::: zone-end

>[!NOTE]
>
> Beginning in July of 2023, an opt-in public preview for security settings management is available. To view content that reflects the capabilities of the opt-in public preview, select the **Opt-in Public Preview** option.
>
> You can opt-in to the public preview by enabling the use of **Preview features** from within the [Microsoft 365 Defender portal](https://sip.security.microsoft.com/homepage). For more information on this, see [Microsoft Defender for Endpoint preview features](/microsoft-365/security/defender-endpoint/preview) in the Defender documentation.

::: zone pivot="mdssc-ga"

When you manage devices through security settings management without participation in the public preview:

- You use the Microsoft Intune admin center to configure endpoint security policies for Defender for Endpoint and assign those policies to Azure AD groups
- Devices get the policies based on their Azure Active Directory device object. A device that isn’t already present in Azure Active Directory is joined as part of this solution
- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the device's status. The device's status is available in the Microsoft Intune admin center

This scenario extends the Microsoft Intune Endpoint Security surface to devices that aren't capable of enrolling in Intune. When a device is managed by Intune (enrolled to Intune) the device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

Applies to:

- Windows 10
- Windows 11

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the Microsoft Defender for Endpoint-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

::: zone-end
::: zone pivot="mdssc-preview"

*The information in this article describes behavior for the opt-in public preview. If you use security settings management but haven't opted in to the public preview, select **Generally Available** at the top of this article to view content that describes the behaviors your tenant supports*

When you manage devices through security settings management as part of the public preview:

- You can use the Microsoft Intune admin center or the Microsoft 365 Defender portal to configure endpoint security policies for Defender for Endpoint and assign those policies to Azure Active Directory (Azure AD) groups. The Defender portal includes the user interface for device views, policy management, and reports for security settings management.

  To view guidance on managing the Intune endpoint security policies from within the Defender portal, see [Manage endpoint security policies in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/manage-security-policies) in the Defender content.

- Devices get their assigned policies based on their Azure AD device object. A device that isn’t already registered in Azure Active Directory is joined as part of this solution.

- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the device's status. The device's status is available in the Microsoft Intune admin center and the Microsoft 365 Defender portal.

This scenario extends the Microsoft Intune Endpoint Security surface to devices that aren't capable of enrolling in Intune. When a device is managed by Intune (enrolled to Intune) the device doesn't process policies for Defender for Endpoint security settings management. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

Applies to:

- Linux
- macOS
- Windows 10
- Windows 11

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview-2.png" alt-text="Conceptual presentation of the Microsoft Defender for Endpoint-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview-2.png":::

::: zone-end

## Prerequisites

Review the following sections for requirements for the Defender for Endpoint security settings management Scenario.

### Environment

When a supported device onboards to Microsoft Defender for Endpoint:

::: zone pivot="mdssc-ga"

- The device is surveyed for an existing Microsoft Intune presence, which is a mobile device management (MDM) enrollment to Intune.
- Devices without an Intune presence enable the security settings management feature.
- A trust is created with Azure Active Directory if one doesn't already exist.
- Policies retrieved from Microsoft Intune are enforced on the device by Microsoft Defender for Endpoint.

Security settings management isn't yet supported with Government clouds. For more information, see [Feature parity with commercial](/microsoft-365/security/defender-endpoint/gov#feature-parity-with-commercial) in *Microsoft Defender for Endpoint for US Government customers*.

::: zone-end
::: zone pivot="mdssc-preview"

- The device is surveyed for an existing Microsoft Intune presence, which is a mobile device management (MDM) enrollment to Intune.
- Devices without an Intune presence enable the security settings management feature.
- For devices that aren't fully Azure AD registered, a synthetic device identity is created in Azure AD that allows the device to retrieve policies. Fully registered devices use their current registration.
- Policies retrieved from Microsoft Intune are enforced on the device by Microsoft Defender for Endpoint.

Security settings management isn't yet supported with Government clouds. For more information, see [Feature parity with commercial](/microsoft-365/security/defender-endpoint/gov#feature-parity-with-commercial) in *Microsoft Defender for Endpoint for US Government customers*.
::: zone-end

### Active Directory requirements

When a device that is domain joined creates a trust with Azure Active Directory, this scenario is referred to as a *Hybrid Azure Active Directory Join* scenario. Security settings management fully supports this scenario with the following requirements:

- Azure Active Directory Connect (Azure AD Connect) must be synchronized to the tenant that is used from Microsoft Defender for Endpoint.
- Hybrid Azure Active Directory Join must be configured in your environment (either through Federation or Azure AD Connect Sync).
- Azure AD Connect Sync must include the device objects *in scope* for synchronization with Azure Active Directory (when needed for join).
- Azure AD Connect rules for sync [must be modified for Server 2012 R2](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt#instructions-for-applying-computer-join-rule-in-aad-connect) (when support for Server 2012 R2 is needed).
- All devices must register in the Azure Active Directory of the tenant that hosts Microsoft Defender for Endpoint. Cross-tenant scenarios aren't supported.

> [!NOTE]
>
> If a device is deleted (from either Azure AD or the on-premises Active Directory), or the device is shifted to a different organizational unit (OU) that isn’t synchronized by Azure AD Connect, the device's record is removed from Azure AD and the group membership is also removed. As a result, Intune policies no longer target the device.
>
> If the device was part of a dynamic Azure AD group, the policy targeting the device will be resolved within a minimum of 48 hours. However, if the device was targeted as part of a static Azure AD group, administrators will need to go back and retarget the device.
>
> This is a known issue with Azure AD.

### Connectivity requirements

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` - For Azure AD registration.
- `login.microsoftonline.com` - For Azure AD registration.
- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

> [!NOTE]
> You need to configure an endpoint system-wide proxy in an environment that is not connected to the internet. Use of only the EDR static proxy configuration is not sufficient.
>
> If your organization uses Secure Socket Layer (SSL) inspection, the endpoints should be excluded from inspection.

### Supported platforms

Policies for Microsoft Defender for Endpoint security management are supported for the following device platforms:

::: zone pivot="mdssc-preview"

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


**macOS**:

With [Microsoft Defender for Endpoint for macOS](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-mac#system-requirements) agent version **101.23052.0004** or later, security settings management supports the following macOS versions:

- macOS 13 (Ventura)
- macOS 12 (Monterey)
- macOS 11 (Big Sur)

To confirm the version of the Defender agent, in the Defender portal go to the devices page, and on the devices *Inventories* tab, search for *Defender for macOS*. For guidance on updating the agent version, see [Deploy updates for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-updates).

*Known issue*: With the Defender agent version **101.23052.0004**, macOS devices that are registered in Azure AD before enrolling with security settings management receive a duplicate Device ID in Azure AD, which is a synthetic registration.  When you create an Azure AD group for targeting policy, you must use the synthetic Device ID created by security settings management. In Azure AD, the Join Type column for the synthetic Device ID  is blank.

::: zone-end

**Windows**:

- Windows 10 Professional/Enterprise (with [KB5006738](https://support.microsoft.com/topic/october-26-2021-kb5006738-os-builds-19041-1320-19042-1320-and-19043-1320-preview-ccbce6bf-ae00-4e66-9789-ce8e7ea35541))
- Windows 11 Professional/Enterprise
- Windows Server 2012 R2 with [Microsoft Defender for Down-Level Devices](/microsoft-365/security/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2016 with [Microsoft Defender for Down-Level Devices](/microsoft-365/security/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2019 (with [KB5006744](https://support.microsoft.com/topic/october-19-2021-kb5006744-os-build-17763-2268-preview-e043a8a3-901b-4190-bb6b-f5a4137411c0))
- Windows Server 2022 (with [KB5006745](https://support.microsoft.com/topic/october-26-2021-kb5006745-os-build-20348-320-preview-8ff9319a-19e7-40c7-bbd1-cd70fcca066c))

Security settings management doesn't work on and is not supported with the following:

- Non-persistent desktops, like Virtual Desktop Infrastructure (VDI) clients or Azure Virtual Desktops.
- Domain Controllers

> [!IMPORTANT]
>
> In some cases, Domain Controllers that are run a down level server Operating system (2012 R2 or 2016) can unintentionally be managed by Microsoft Defender for Endpoint. In order to ensure that this doesn’t happen in your environment, we recommend making sure your domain controllers are neither tagged “MDE-Management” or managed by MDE.

### Licensing and subscriptions

To use security settings management, you need:

- A subscription that grants licenses for Microsoft Defender for Endpoint, like Microsoft 365, or a standalone license for only Microsoft Defender for Endpoint. A subscription that grants Microsoft Defender for Endpoint licenses also grants your tenant access to the Endpoint security node of the Microsoft Intune admin center.

  > [!NOTE]
  >
  > **Exception**: If you have access to Microsoft Defender for Endpoint *only* through Microsoft Defender for servers (part of Microsoft Defender for Cloud, formerly Azure Security Center), the security settings management functionality isn't available. You will need to have at least one Microsoft Defender for Endpoint (user) subscription license active.

  The Endpoint security node is where you configure and deploy policies to manage Microsoft Defender for Endpoint for your devices and monitor device status.

  For current information about options, see [Minimum requirements for Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/minimum-requirements?view=o365-worldwide&preserve-view=true).

## Architecture

The following diagram is a conceptual representation of the Microsoft Defender for Endpoint security configuration management solution.

::: zone pivot="mdssc-ga"

:::image type="content" alt-text="Conceptual representation of the Microsoft Defender for Endpoint security configuration management solution" source="./media/mde-security-integration/mde-architecture.png" lightbox="./media/mde-security-integration/mde-architecture.png":::

1. Devices onboard to Microsoft Defender for Endpoint.
2. A trust is established between each device and Azure AD. When a device has an existing trust, it uses that trust. When devices haven't registered, a new trust is created.
3. Devices use their Azure AD Identity to communicate with Intune. This identity enables Microsoft Intune to distribute policies that are targeted to the devices when they check in.
4. Defender for Endpoint reports the status of the policy back to Microsoft Intune.

::: zone-end
::: zone pivot="mdssc-preview"

:::image type="content" alt-text="Conceptual diagram of the Microsoft Defender for Endpoint security configuration management solution" source="./media/mde-security-integration/mde-architecture-2.png" lightbox="./media/mde-security-integration/mde-architecture-2.png":::

1. Devices onboard to Microsoft Defender for Endpoint.
2. Devices communicate with Intune. This enables Microsoft Intune to distribute policies that are targeted to the devices when they check in.
3. A registration is established for each device in Azure AD:
   - If a device was previously fully registered, like a Hybrid Join device, the existing registration is used.
   - For devices that haven't been registered, a synthetic device identity is created in Azure AD to enable the device to retrieve policies. When a device with a synthetic registration has a full Azure AD registration created for it, the synthetic registration is removed and the devices management continues on uninterrupted by using the full registration.
4. Defender for Endpoint reports the status of the policy back to Microsoft Intune.

> [!IMPORTANT]
> With the public preview, security settings management uses a synthetic registration for devices that don’t fully register in Azure AD, and drops the Hybrid Azure AD Join prerequisite. With this change, Windows devices that previously had enrollment errors will begin onboarding to Defender and then receive and process the security settings management policies.
>
> To filter for devices that were unable to enroll due to failing to meet the Hybrid Azure AD Join prerequisite, navigate to the **Devices** list in the Microsoft 365 Defender portal, and filter by enrollment status. Because these devices are not fully registered, their device attributes show **MDM** = **Intune** and **Join Type** = **Blank**. These devices will now enroll with security settings management using the synthetic registration.
>
> After enrolling these devices appear in the device lists for Microsoft 365 Defender, Microsoft Intune, and Azure AD portals. While the devices won’t be fully registered with Azure AD, their synthetic registration counts as one device object.

### What to expect in the Microsoft 365 Defender portal

You can use the Microsoft 365 Defender *Device inventory* to confirm a device is using the security settings management capability in Defender for Endpoint, by reviewing the devices status in the **Managed by** column. The *Managed by* information is also available on the devices side-panel or device page. *Managed by* should consistently indicate that its managed by **MDE**.  

You can also confirm a device has enrolled in *security settings management* successfully by confirming that the device-side panel or device page display **MDE Enrollment status** as **Success**.

:::image type="content" source="./media/mde-security-integration/defender-enrollment-validation.png" alt-text="A screenshot of a devices security settings management enrollment status on the device page in the Microsoft 365 Defender portal." lightbox="./media/mde-security-integration/defender-enrollment-validation.png":::

If the **MDE Enrollment** status doesn’t display **Success**, make sure you’re looking at a device that was updated and is in scope for security settings management. (You configure the scope on the Enforcement scope page while configuring security settings management.)

### What to expect in the Microsoft Intune admin center

In the Microsoft Intune admin center, go to the All Devices page. Devices enrolled with security settings management appear here as in the Defender portal. In the admin center, the devices Managed by field should display MDE.

:::image type="content" source="./media/mde-security-integration/intune-enrollment-validation.png" alt-text="A screenshot of the device page in the Intune admin center with the Managed by status of the device highlighted." lightbox="./media/mde-security-integration/intune-enrollment-validation.png" :::

> [!TIP]
>
> In June 2023, security settings management began using synthetic registration for devices that don’t fully register in Azure AD. With this change, devices that previously had enrollment errors will begin onboarding  to Defender and then receive and process the security settings management policies.

### What to expect in the Microsoft Azure portal

On the *All devices* page In the Microsoft Azure portal, you can view device details.

:::image type="content" source="./media/mde-security-integration/azure-enrollment-validation.png" alt-text="A screenshot of the All device page in the Microsoft Azure portal with an example device highlighted." lightbox="./media/mde-security-integration/azure-enrollment-validation.png":::

To ensure that all devices enrolled in Defender for Endpoint security settings management receive policies, we recommend creating a [dynamic Azure AD group](../fundamentals/groups-add.md) based on the devices’ OS Type. With a dynamic group, devices that are managed by Defender for Endpoint are automatically added to the group without requiring admins to perform other tasks, like creating a new policy.

> [!IMPORTANT]
>
> If you used security settings management prior to joining the public preview, review your Azure AD groups that rely on system labels and make changes that will identify the devices added after joining the public preview. Prior to the new opt-in public preview, enrolled devices would use the following system labels (tags) of *MDEManaged* and *MDEJoined* to identify managed devices. With the changes introduced with the opt-in public preview, these system labels are no longer supported and added to devices that enroll.

With the behavior that is introduced with the public preview in July of 2023, use the following guidance for your Dynamic groups:

- (Recommended) When targeting policy, use dynamic groups based on the device platform by using the *deviceType* attribute (Windows, WindowsServer, macOS, Linux) to ensure policy continues to be delivered for devices that change management types, for example during MDM enrollment.

- If necessary, dynamic groups containing exclusively devices managed by Defender for Endpoint can be targeted by defining a dynamic group using the *managementType* attribute **MicrosoftSense**. Use of this attribute targets all devices managed by Defender for Endpoint via the security settings management functionality, and devices will only remain in this group while being managed by Defender for Endpoint.

Also, when configuring security settings management, if you intend to manage entire OS platform fleets using Microsoft Defender for Endpoint, by selecting **all devices** instead of **tagged devices** in the Microsoft Defender for Endpoint Enforcement Scope page, understand that any synthetic registrations are counted against Azure AD quotas the same as full registrations.


::: zone-end

## Which solution should I use?

Microsoft Intune includes several methods and policy types to manage the configuration of Defender for Endpoint on devices. The following table identifies the Intune policies and profiles that support deployment to devices managed by Defender for Endpoint security settings management and can help you identify if this solution is right for your needs.

When you deploy an endpoint security policy that’s supported for both *Defender for Endpoint security settings management* and *Microsoft Intune*, a single instance of that policy can be processed by devices supported through security settings management (Microsoft Defender), and by devices that are managed by either Intune or Configuration Manager.

Profiles for the *Windows 10 and later platform* aren't supported for devices managed by security settings management.

::: zone pivot="mdssc-ga"

| Endpoint security policy | Platform  | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|-----------|--------------------------|---------|--------------------------------------------------------|-------------------|
| Windows 10, Windows 11, and Windows Server | Antivirus  | Antivirus                   | ![Supported](./media/mde-security-integration/green-check.png)  | ![Supported](./media/mde-security-integration/green-check.png)  |
| Windows 10, Windows 11, and Windows Server | Antivirus           | Antivirus Exclusions        | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Windows 10, Windows 11, and Windows Server| Attack Surface Reduction  | Attack Surface Reduction Rules  | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Windows 10, Windows 11, and Windows Server| Endpoint detection and response  | Endpoint detection and response | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Windows 10, Windows 11, and Windows Server| Firewall     | Firewall                    | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Windows 10, Windows 11, and Windows Server | Firewall   | Firewall Rules  | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |

::: zone-end

::: zone pivot="mdssc-preview"

Following profiles are supported for each device type:

### Linux

The following policy types support the *Linux* platform.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus                            | Microsoft Defender Antivirus | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus                            | Microsoft Defender Antivirus exclusions | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |

### macOS

The following policy types support the *macOS* platform.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus                            | Microsoft Defender Antivirus            | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus                            | Microsoft Defender Antivirus exclusions | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |

### Windows 10, Windows 11, and Windows Server

To support use with Microsoft Defender security settings management, your policies for Windows devices must use the *Windows 10, Windows 11, and Windows Server* platform. Each profile for the *Windows 10, Windows 11, and Windows Server* platform can apply to devices that are managed by Intune and to devices that are managed by security settings management.

| Endpoint security policy | Profile | Defender for Endpoint security settings management  |  Microsoft Intune |
|---------|----------|-----------|----------|
| Antivirus              | Microsoft Defender Antivirus           | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus              | Microsoft Defender Antivirus exclusions| ![Supported](./media/mde-security-integration/green-check.png)  | ![Supported](./media/mde-security-integration/green-check.png) |
| Antivirus              | Windows Security Experience            | *Note 1*         | ![Supported](./media/mde-security-integration/green-check.png) |
|Attack Surface Reduction |Attack Surface Reduction Rules          | ![Supported](./media/mde-security-integration/green-check.png)  | ![Supported](./media/mde-security-integration/green-check.png)  |
| Endpoint detection and response | Endpoint detection and response | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Firewall  | Firewall            | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
| Firewall  | Firewall Rules      | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |

***1*** - The *Windows Security Experience* profile is available in the Defender portal but only applies to devices managed by Intune. It isn't supported for devices managed by Microsoft Defender security settings management.

::: zone-end

**Endpoint security policies** are discrete groups of settings intended for use by security admins who focus on protecting devices in your organization. The following are descriptions of the policies that support security settings management:

- **Antivirus** policies manage the security configurations found in Microsoft Defender for Endpoint. See  [antivirus](/mem/intune/protect/endpoint-security-antivirus-policy) policy for endpoint security.
- **Attack surface reduction** (ASR) policies focus on minimizing the places where your organization is vulnerable to cyberthreats and attacks. With security settings management, ASR rules apply to devices that run Windows 10, Windows 11, and Windows Server. For more information, see:
  - [Overview of attack surface reduction](/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation.
  - [ASR rules supported operating systems](/microsoft-365/security/defender-endpoint/attack-surface-reduction-rules-reference#asr-rules-supported-operating-systems) in the Windows Threat protection documentation.
  - [Attack surface reduction](/mem/intune/protect/endpoint-security-asr-policy) policy for endpoint security, in the Intune documentation.
  
- **Endpoint detection and response** (EDR) policies manage the Defender for Endpoint capabilities that provide advanced attack detections that are near real-time and actionable. Based on EDR configurations, security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. See [endpoint detection and response](/mem/intune/protect/endpoint-security-edr-policy) policy for endpoint security.
- **Firewall** policies focus on the Defender firewall on your devices. See [firewall](/mem/intune/protect/endpoint-security-firewall-policy) policy for endpoint security.
- **Firewall Rules** configure granular rules for Firewalls, including specific ports, protocols, applications, and networks. See [firewall](/mem/intune/protect/endpoint-security-firewall-policy) policy for endpoint security.

## Configure your tenant to support Defender for Endpoint security settings management

To support security settings management through the Microsoft Intune admin center, you must enable communication between them from within each console.

The following sections guide you through that process.

### Configure Microsoft Defender for Endpoint

In Microsoft Defender for Endpoint portal, as a security admin, your account needs at minimum permissions to view and edit security settings (Manage security settings in Security Center).

1. Sign in to [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope** and enable the platforms for security settings management.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-defender.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft 365 Defender portal." lightbox="./media/mde-security-integration/enable-mde-settings-management-defender.png#lightbox":::

2. Initially, we recommend testing the feature for each platform by selecting the platforms option for **On tagged devices**, and then tagging the devices with the `MDE-Management` tag.

3. Configure the feature for Microsoft Defender for Cloud onboarded devices and Configuration Manager authority settings to fit your organization's needs:

   :::image type="content" source="./media/mde-security-integration/pilot-CMAuthority-mde-settings-management-defender.png" alt-text="Configure Pilot mode for Endpoint settings management in the Microsoft 365 Defender portal." lightbox="./media/mde-security-integration/pilot-CMAuthority-mde-settings-management-defender.png" :::

   > [!TIP]
   >
   > Use the proper device tags to test and validate your rollout on a small number of devices. Without using pilot mode, any device that falls into the scope configured will automatically be enrolled.

4. Make sure the relevant users have permissions to manage endpoint security settings in Microsoft Intune. If not already provided, request for your IT administrator to grant applicable users the Microsoft Intune's **Endpoint Security Manager** [built-in RBAC role](/mem/intune/fundamentals/role-based-access-control).

### Configure Intune

In the Microsoft Intune admin center, your account need permissions equal to Endpoint Security Manager built-in Role based access control (RBAC) role.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-mem.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft Intune admin center." lightbox="./media/mde-security-integration/enable-mde-settings-management-mem.png" :::

   When you set this option to *On*, all devices in the platform scope for Microsoft Defender for Endpoint that aren't managed by Microsoft Intune qualify to onboard to Microsoft Defender for Endpoint.

## Onboard devices to Microsoft Defender for Endpoint

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboard devices and configure Microsoft Defender for Endpoint capabilities](/microsoft-365/security/defender-endpoint/onboard-configure) in the Defender for Endpoint documentation.

## Coexistence with Microsoft Configuration Manager

In some environments it might be desired to use security settings management with devices managed by Configuration Manager. If you use both, you’ll need to control policy through a single channel, as using more than one channel creates the opportunity for conflicts and undesired results.

To support this, configure the *Manage Security settings using Configuration Manager* toggle to *Off*. Sign in to the [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope**:

:::image type="content" source="./media/mde-security-integration/disable-configuration-manager-toggle.png" alt-text="Screen shot of the Defender portal showing the Manage Security settings using Configuration Manager toggle set to Off." lightbox="./media/mde-security-integration/disable-configuration-manager-toggle.png" :::

## Create Azure AD Groups

After devices onboard to Defender for Endpoint, you'll need to create device groups to support deployment of policy for Microsoft Defender for Endpoint. To identify devices that have enrolled with Microsoft Defender for Endpoint but aren't managed by Intune or Configuration Manager:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **All devices**, and then select the column **Managed by** to sort the view of devices. Devices that onboard to Microsoft Defender for Endpoint but aren't managed by Intune display **Microsoft Defender for Endpoint** in the *Managed by* column. These are the devices that can receive policies for security settings management.

   Devices that onboard to Microsoft Defender for Endpoint and have registered but aren't managed by Intune display **Microsoft Defender for Endpoint** in the *Managed by* column. These are the devices that can receive policy for security management for Microsoft Defender for Endpoint.

   ::: zone pivot="mdssc-ga"

   You can also find two labels for devices that are using security management for Microsoft Defender for Endpoint:
   - **MDEJoined** - Added to devices that are joined to the directory as part of this scenario.
   - **MDEManaged** - Added to devices that are actively using the security management scenario. This tag is removed from the device if Defender for Endpoint stops managing the security configuration.

   ::: zone-end
   ::: zone pivot="mdssc-preview"

   With behavior introduced with the opt-in public preview, devices that used security management for Microsoft Defender for Endpoint can no longer be identified by using the following system labels:

   - **MDEJoined** - Added to devices that are joined to the directory as part of this scenario.
   - **MDEManaged** - Added to devices that are actively using the security management scenario. This tag is removed from the device if Defender for Endpoint stops managing the security configuration.

   Instead of using system labels, you can use the management type attribute, and configure it to **MicrosoftSense**.

   ::: zone-end

You can create groups for these devices [in Azure AD](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) or [from within the Microsoft Intune admin center](/mem/intune/fundamentals/groups-add). When creating groups, you can use the **OS** value for a device if you're deploying policies to devices running Windows Server vs devices that run a client version of Windows:  

- **Windows 10 and Windows 11** - The deviceType or OS displays as *Windows*
- **Windows Server** - The deviceType or OS displays as *Windows Server*

> [!IMPORTANT]
> In May 2023, *deviceType* updated to distinguish between *Windows clients* and *Windows Servers*.
>
> Custom scripts and [Azure AD dynamic device groups](/azure/active-directory/enterprise-users/groups-dynamic-membership) created before this change that specify rules that reference only *Windows* might exclude *Windows Servers* when used with the Security Management for Microsoft Defender for Endpoint solution. For example:
>
> - If you have a rule that uses the `equals` or `not equals` operator to identify *Windows*, this change will affect your rule. That is because previously both *Windows* and *Windows Server* were reported as *Windows*. To continue to include both, you must update the rule to also reference *Windows Server*.
> - If you have a rule that use the `contains` or `like` operator to specify *Windows*, then the rule won’t be affected by this change. These operators can find both *Windows* and *Windows Server*.

> [!TIP]
>
> Users that are delegated the ability to manage endpoint security settings may not have the ability to implement tenant-wide configurations in Microsoft Intune.  Check with your Intune administrator for more information on roles and permissions in your organization.

## Deploy policy

After creating one or more Azure AD groups that contain devices managed by Microsoft Defender for Endpoint, you can create and deploy the following policies for security settings management to those groups. The policies and profiles available vary by platform.

For the list of policy and profile combinations supported for security settings management, see the chart in [Which solution should I use?](#which-solution-should-i-use) earlier in this article.

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

7. On the **Assignments** page, select the Azure AD groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](/mem/intune/configuration/device-profile-assign).

   Select **Next** to continue.

   > [!TIP]
   >
   > - Assignment filters are not supported for devices managed by security settings management.
   > - Only *Device Objects* are applicable for Microsoft Defender for Endpoint management. Targeting users is not supported.
   > - Policies configured will apply to both Microsoft Intune and Microsoft Defender for Endpoint clients.

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. You can validate that settings have applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples) command utility.

## Monitor status

Status and reports for policies that target devices in this channel are available from the policy node under Endpoint security in the Microsoft Intune admin center.

Drill in to the policy type and then select the policy to view its status. You can view the list of platforms, policy types, and profiles that support security settings management in the table in [Which solution should I use](#which-solution-should-i-use), earlier in this article.

When you select a policy, you can view information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Frequently asked questions and considerations

### Device check-in frequency

Devices managed by this capability check-in with Microsoft Intune every 90 minutes to update policy.

You can manually sync a device on-demand from the [Microsoft 365 Defender portal](https://security.microsoft.com/). Sign-in to the portal and go to **Devices**. Select a device that is managed by Microsoft Defender for Endpoint, and then select the **Policy sync** button:  

:::image type="content" source="./media/mde-security-integration/policy-sync-from-mde.png" alt-text="Manually sync devices managed by Microsoft Defender for Endpoint." lightbox="./media/mde-security-integration/policy-sync-from-mde.png"  :::

The Policy sync button only appears for devices that are successfully managed by Microsoft Defender for Endpoint.

### Devices protected by Tamper Protection

If a device has Tamper Protection turned on, it isn't possible to edit the values of [Tamper Protected settings](/microsoft-365/security/defender-endpoint/prevent-changes-to-security-settings-with-tamper-protection#what-happens-when-tamper-protection-is-turned-on) without disabling Tamper Protection first.

### Assignment Filters and security settings management

Assignment filters aren't supported for devices communicating through the Microsoft Defender for Endpoint channel. While assignment filters can be added to a policy that could target these devices, the devices ignore assignment filters. For assignment filter support, the device must be enrolled in to Microsoft Intune.

### Deleting and removing devices

You can delete devices that use this flow using one of two methods:

- From within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **All devices**, select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column, and then select **Delete**.
- You can also remove devices from the scope of Configuration Management in the Security Center.

Once a device is removed from either location, that change propagates to the other service.

### Unable to enable the Security Management for Microsoft Defender for Endpoint workload in Endpoint Security

Most initial provisioning flows are typically completed by an Administrator of both services (such as a Global Administrator). There are some scenarios where Role-based Administration is used to customize the permissions of administrators. Today, individuals who are delegated the *Endpoint Security Manager* role might not have the necessary permissions to enable this feature.

### Active Directory joined devices

::: zone pivot="mdssc-ga"

Devices that are joined to Active Directory use their **existing infrastructure** to complete the Hybrid Azure Active Directory join process. While the Defender for Endpoint component starts this process, the join action uses your Federation provider or Azure Active Directory Connect (Azure AD Connect) to complete the join. Review [Plan your hybrid Azure Active Directory join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) to learn more about configuring your environment.

To troubleshoot Azure Active Directory onboarding issues, see  [Troubleshoot Security Configuration Management Azure Active Directory onboarding issues](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt).

::: zone-end
::: zone pivot="mdssc-preview"

Devices that are joined to Active Directory use their **existing infrastructure** to complete the Hybrid Azure Active Directory join process.

::: zone-end

### Unsupported security settings

The following security settings are pending deprecation. The Defender for Endpoint security settings management flow doesn't support these settings:

- Expedite telemetry reporting frequency (under **Endpoint Detection and Response**)
- AllowIntrusionPreventionSystem (under **Antivirus**)

### Use of security settings management on domain controllers

Because an Azure Active Directory trust is required, domain controllers aren't currently supported. We're looking at ways to add this support.

> [!IMPORTANT]
>
> In some cases, Domain Controllers that are run a down level server Operating system (2012 R2 or 2016) can unintentionally be managed by Microsoft Defender for Endpoint. In order to ensure that this doesn’t happen in your environment, we recommend making sure your domain controllers are neither tagged “MDE-Management” or managed by MDE.

### Server Core installation

Due to the platform limitations of Server core installations, these aren't supported by security settings management.

### PowerShell restrict mode

Security settings management won't work for a device that has PowerShell *LanguageMode* configured with *ConstrainedLanguage* mode `enabled`. For more information, see [about_Language_Modes](/powershell/module/microsoft.powershell.core/about/about_language_modes) in the PowerShell documentation.

## Next steps

- [Monitor Defender for Endpoint in Intune](../protect/advanced-threat-protection-monitor.md)

::: zone pivot="mdssc-preview"

- [Manage endpoint security policies in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/manage-security-policies) in the Defender documentation.

::: zone-end
