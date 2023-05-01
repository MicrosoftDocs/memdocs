---
# required metadata

title: Use Intune to manage Microsoft Defender for Endpoint Security on devices not enrolled with Microsoft Intune 
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/30/2023
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
ms.reviewer: mattcall

---

# Manage Microsoft Defender for Endpoint on devices with Microsoft Intune

With Microsoft Defender for Endpoint (MDE), you can now deploy security configurations from Microsoft Intune directly to your onboarded devices without requiring a full Microsoft Intune device enrollment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this capability, devices that aren’t managed by a Microsoft Intune service can receive security configurations for Microsoft Defender for Endpoint directly from Intune.

When devices are managed through this capability:

- You use the Microsoft Intune admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups
- Devices get the policies based on their Azure Active Directory device object. A device that isn’t already present in Azure Active Directory is joined as part of this solution
- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the device's status. The device's status is available in the Microsoft Intune admin center

This scenario extends the Microsoft Intune Endpoint Security surface to devices that aren't capable of enrolling in Intune. When a device is managed by Intune (enrolled to Intune) the device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

## Prerequisites

Review the following sections for requirements for the Security Management for Microsoft Defender for Endpoint Scenario.

### Environment

When a device onboards to Microsoft Defender for Endpoint:

- The device is surveyed for an existing Microsoft Intune presence, which is a mobile device management (MDM) enrollment to Intune
- Devices without an Intune presence enable the Security Management feature
- A trust is created with Azure Active Directory if one doesn't already exist
- Azure Active Directory trust is used to communicate with Intune and retrieve policies
- Policies retrieved from Microsoft Intune is enforced on the device by Microsoft Defender for Endpoint

Security Management for Microsoft Defender for Endpoint is not yet supported with Government clouds. For more information, see [Feature parity with commercial](/microsoft-365/security/defender-endpoint/gov#feature-parity-with-commercial) in *Microsoft Defender for Endpoint for US Government customers*.

### Active Directory requirements

When a device that is domain joined creates a trust with Azure Active Directory, this scenario is referred to as a *Hybrid Azure Active Directory Join* scenario. The Security Management for Microsoft Defender for Endpoint fully supports this scenario with the following requirements:

- Azure Active Directory Connect (AAD Connect) must be synchronized to the tenant that is used from Microsoft Defender for Endpoint
- Hybrid Azure Active Directory Join must be configured in your environment (either through Federation or AAD Connect Sync)
- AAD Connect Sync must include the device objects *in scope* for synchronization with Azure Active Directory (when needed for join)
- AAD Connect rules for sync [must be modified for Server 2012 R2](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt#instructions-for-applying-computer-join-rule-in-aad-connect) (when support for Server 2012 R2 is needed)
- All devices must register in the Azure Active Directory of the tenant that hosts Microsoft Defender for Endpoint. Cross-tenant scenarios are not supported.


### Connectivity requirements

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` - For Azure AD registration.
- `login.microsoftonline.com` - For Azure AD registration.
- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

> [!Note]
>  You need to configure endpoint system-wide proxy in the Internet-disconnected environment. It is not enough to use only the EDR static proxy configuration.
>
>  If your organization uses Secure Socket Layer (SSL) inspection, the endpoints should be excluded from inspection.

### Supported platforms

Policies for Microsoft Defender for Endpoint security management are supported for the following device platforms:

- Windows 10 Professional/Enterprise (with [KB5006738](https://support.microsoft.com/topic/october-26-2021-kb5006738-os-builds-19041-1320-19042-1320-and-19043-1320-preview-ccbce6bf-ae00-4e66-9789-ce8e7ea35541))
- Windows 11 Professional/Enterprise
- Windows Server 2012 R2 with [Microsoft Defender for Down-Level Devices](/microsoft-365/security/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2016 with [Microsoft Defender for Down-Level Devices](/microsoft-365/security/defender-endpoint/configure-server-endpoints#new-functionality-in-the-modern-unified-solution-for-windows-server-2012-r2-and-2016-preview)
- Windows Server 2019 (with [KB5006744](https://support.microsoft.com/topic/october-19-2021-kb5006744-os-build-17763-2268-preview-e043a8a3-901b-4190-bb6b-f5a4137411c0))
- Windows Server 2022 (with [KB5006745](https://support.microsoft.com/topic/october-26-2021-kb5006745-os-build-20348-320-preview-8ff9319a-19e7-40c7-bbd1-cd70fcca066c))

Security management for Microsoft Defender for Endpoint will not work on non-persistent desktops, like Virtual Desktop Infrastructure (VDI) clients or Azure Virtual Desktops.

### Licensing and subscriptions

To use security management for Microsoft Defender for Endpoint, you need:

- A subscription that grants licenses for Microsoft Defender for Endpoint, like Microsoft 365, or a standalone license for only Microsoft Defender for Endpoint. A subscription that grants Microsoft Defender for Endpoint licenses also grants your tenant access to the Endpoint security node of the Microsoft Intune admin center.

  > [!NOTE]  
  > **Exception**: If you have access to Microsoft Defender for Endpoint *only* through Microsoft Defender for servers (part of Microsoft Defender for Cloud, formerly Azure Security Center), the Security Management for Microsoft Defender for Endpoint functionality is not available. You will need to have at least one Microsoft Defender for Endpoint (user) subscription license active.

  The Endpoint security node is where you'll configure and deploy policies to manage Microsoft Defender for Endpoint for your devices and monitor device status.

  For current information about options, see [Minimum requirements for Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/minimum-requirements?view=o365-worldwide&preserve-view=true).

## Architecture

The following diagram is a conceptual representation of the Microsoft Defender for Endpoint security configuration management solution.

:::image type="content" alt-text="Conceptual representation of the Microsoft Defender for Endpoint security configuration management solution" source="./media/mde-security-integration/mde-architecture.png":::

1. Devices onboard to Microsoft Defender for Endpoint.
2. A trust is established between each device and Azure AD. When a device has an existing trust, that is used. When devices haven't registered, a new trust is created.
3. Devices use their Azure AD Identity to communicate with Intune. This identity enables Microsoft Intune to distribute policies that are targeted to the devices when they check in.
4. Defender for Endpoint reports the status of the policy back to Microsoft Intune.

## Which solution should I use?

Microsoft Intune includes several methods and policy types to manage the configuration of Defender for Endpoint on devices.

When your device protection needs extend beyond managing Defender for Endpoint, see [Device protection overview](/mem/intune/protect/device-protect) to learn about additional capabilities provided by Microsoft Intune to help protect devices, including *device compliance*, *managed apps*, *app protection policies*, and integration with third-party compliance and *mobile threat defense* partners.

The following table can help you understand which policies that can configure MDE settings are supported by devices that are managed by the different scenarios. When you deploy a policy that’s supported for both *MDE security configuration* and *Microsoft Intune*, a single instance of that policy can be processed by devices that run MDE only and devices that are managed by either Intune or Configuration Manager.

| Microsoft Intune  | Workload | Policy | MDE Security configuration  |  Microsoft Intune |
|----------------|----------------|----------------|-------------------|------------|
| Endpoint security  | Antivirus  | Antivirus                    | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                    | Antivirus   | Antivirus Exclusions        | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                    | Antivirus   | Windows Security Experience |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                    | Disk Encryption | All                     |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                    | Firewall    | Firewall                    | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                    | Firewall    | Firewall Rules              | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     | Endpoint detection and response | Endpoint detection and response | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     |Attack Surface Reduction | All            |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     |Attack Surface Reduction | Attack Surface Reduction Rules *(In public preview)* | ![Supported](./media/mde-security-integration/green-check.png) | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     |Account Protection  | All                 |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     | Device Compliance  | All                 |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     | Conditional Access | All                 |  | ![Supported](./media/mde-security-integration/green-check.png)  |
|                     | Security baselines | All                 |  | ![Supported](./media/mde-security-integration/green-check.png)  |

**Endpoint security policies** are discrete groups of settings intended for use by security admins who focus on protecting devices in your organization.

- **Antivirus** policies manage the security configurations found in Microsoft Defender for Endpoint. See  [antivirus](/mem/intune/protect/endpoint-security-antivirus-policy) policy for endpoint security.
- **Attack surface reduction** policies focus on minimizing the places where your organization is vulnerable to cyberthreats and attacks. For more information, see [Overview of attack surface reduction](/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation, and [attack surface reduction](/mem/intune/protect/endpoint-security-asr-policy) policy for endpoint security.
- **Endpoint detection and response** (EDR) policies manage the Defender for Endpoint capabilities that provide advanced attack detections that are near real-time and actionable. Based on EDR configurations, security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. See [endpoint detection and response](/mem/intune/protect/endpoint-security-edr-policy) policy for endpoint security.
- **Firewall** policies focus on the Defender firewall on your devices. See [firewall](/mem/intune/protect/endpoint-security-firewall-policy) policy for endpoint security.
- **Firewall Rules** configure granular rules for Firewalls, including specific ports, protocols, applications, and networks. See [firewall](/mem/intune/protect/endpoint-security-firewall-policy) policy for endpoint security.
- **Security baselines** include preconfigured security settings that define the Microsoft recommended security posture for different products like Defender for Endpoint, Edge, or Windows. The default recommendations are from the relevant product teams and enable you to quickly deploy that recommended secure configuration to devices. While settings are preconfigured in each baseline, you can create customized instances of them to establish your organization’s security expectations. See [security baselines](/mem/intune/protect/security-baselines) for Intune.

## Configure your tenant to support Microsoft Defender for Endpoint Security Configuration Management

To support Microsoft Defender for Endpoint security configuration management through the Microsoft Intune admin center, you must enable communication between them from within each console.

1. Sign in to [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope** and enable the platforms for security settings management:
   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-defender.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft 365 Defender portal." lightbox="./media/mde-security-integration/enable-mde-settings-management-defender.png#lightbox":::
1. In order to test the feature only on a specific set of devices, select **On tagged devices** for the respective platform, and tag the devices with the `MDE-Management` tag
1. Configure the feature for Microsoft Defender for Cloud onboarded devices and Configuration Manager authority settings to fit your organization's needs:  
   :::image type="content" source="./media/mde-security-integration/pilot-CMAuthority-mde-settings-management-defender.png" alt-text="Configure Pilot mode for Endpoint settings management in the Microsoft 365 Defender portal.":::
   > [!TIP]
   > Use pilot mode and the proper device tags to test and validate your rollout on a small number of devices. Without using pilot mode, any device that falls into the scope configured will automatically be enrolled.

1. Make sure the relevant users have permissions to manage endpoint security settings in Microsoft Intune. If not already provided, request for your IT administrator to grant applicable users the Microsoft Intune's **Endpoint Security Manager** [built-in RBAC role](/mem/intune/fundamentals/role-based-access-control).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-mem.png" alt-text="Enable Microsoft Defender for Endpoint settings management in the Microsoft Intune admin center.":::
   
   When you set this option to *On*, all devices in the platform scope in Microsoft Defender for Endpoint that aren't managed by Microsoft Intune will qualify to onboard to Microsoft Defender for Endpoint.

> [!TIP]
> Users that are delegated the ability to manage endpoint security settings may not have the ability to implement tenant-wide configurations in Microsoft Intune.  Check with your Intune administrator for more information on roles and permissions in your organization.

## Onboard devices to Microsoft Defender for Endpoint

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboard devices and configure Microsoft Defender for Endpoint capabilities](/microsoft-365/security/defender-endpoint/onboard-configure) in the Defender for Endpoint documentation.

## Co-existence with Microsoft Configuration Manager

In some environments it might be desired to use Security Management for Microsoft Defender for Endpoint with [Configuration Manager tenant attach](/mem/configmgr/tenant-attach/endpoint-security-get-started). If you use both, you’ll need to control policy through a single channel, as using more than one channel creates the opportunity for conflicts and undesired results.

To support this, configure the *Manage Security settings using Configuration Manager* toggle to *Off*.  Sign in to the [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope**:

:::image type="content" source="./media/mde-security-integration/disable-configuration-manager-toggle.png" alt-text="Screen shot of the Defender portal showing the Manage Security settings using Configuration Manager toggle set to Off.":::

## Create Azure AD Groups

After devices onboard to Defender for Endpoint, you'll need to create device groups to support deployment of policy for Microsoft Defender for Endpoint.
To identify devices that have enrolled with Microsoft Defender for Endpoint but aren't managed by Intune or Configuration Manager:

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **All devices**, and then select the column **Managed by** to sort the view of devices.

   Devices that onboard to Microsoft Defender for Endpoint and have registered but aren't managed by Intune display **Microsoft Defender for Endpoint** in the *Managed by* column. These are the devices that can receive policy for security management for Microsoft Defender for Endpoint.

   You'll also find two labels for devices that are using security management for Microsoft Defender for Endpoint:
   - **MDEJoined** - Added to devices that are joined to the directory as part of this scenario.
   - **MDEManaged** - Added to devices that are actively using the security management scenario. This tag is removed from the device if Defender for Endpoint stops managing the security configuration.

You can create groups for these devices [in Azure AD](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) or [from within the Microsoft Intune admin center](/mem/intune/fundamentals/groups-add). When creating groups, you can use the **OS** value for a device if you are deploying policies to devices running Windows Server vs devices that run a client version of Windows:  

- **Windows 10 and Windows 11** - The deviceType or OS displays as *Windows*
- **Windows Server** - The deviceType or OS displays as *Windows Server*

> [!IMPORTANT]
> In May 2023, *deviceType* updated to distinguish between *Windows clients* and *Windows Servers*.
>
> Custom scripts and [Azure AD dynamic device groups](/azure/active-directory/enterprise-users/groups-dynamic-membership) created before this change that specify rules that reference only *Windows* will now exclude Windows Servers when used with the Security Management for Microsoft Defender for Endpoint solution. For example, if you have rules that use the `equals` or `not equals` operator, then you must explicitly update the rule to reference **Windows Server**. If you have rules that use the `contains` or `like` operator, then the rule won’t be affected by this change.

## Deploy policy

After creating one or more Azure AD groups that contain devices managed by Microsoft Defender for Endpoint, you can create and deploy the following policies for Security Management for Microsoft Defender for Endpoint to those groups:

- Antivirus
- Firewall
- Firewall Rules
- Endpoint Detection and Response
- Attack Surface Reduction

> [!TIP]
> Avoid deploying multiple policies that manage the same setting to a device.
>
> Microsoft Intune supports deploying multiple instances of each endpoint security policy type to the same device, with each policy instance being received by the device separately. Therefore, a device might receive separate configurations for the same setting from different policies, which results in a conflict. Some settings (like Antivirus Exclusions) will merge on the client and apply successfully.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Endpoint security** and then select the type of policy you want to configure, either Antivirus or Firewall, and then select **Create Policy**.
3. Enter the following properties or the policy type you selected:
   - For Antivirus policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Microsoft Defender Antivirus**
   - For Firewall policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Microsoft Defender Firewall**
   - For Firewall rules policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Microsoft Defender Firewall Rules**
   - For Endpoint detection and response policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Endpoint detection and response**
   - For Attack surface reduction policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Attack surface reduction rules**

   >[!Note]
   > These profiles apply to both devices communicating through Mobile Device Management (MDM) with Microsoft Intune as well as devices that are communicating using the Microsoft Defender for Endpoint client.
   >
   > Ensure you review your targeting and groups as necessary.

4. Select **Create**.
5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.
6. On the **Configuration settings** page, select the settings you want to manage with this profile. To learn more about a setting, expand its information dialog and select the *Learn more* link to view the CSP information for the setting in the on-line documentation.

   When you're done configuring settings, select **Next**.

7. On the **Assignments** page, select the Azure AD groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](/mem/intune/configuration/device-profile-assign).

   Select **Next** to continue.

   > [!TIP]
   >
   > - Assignment filters are not supported for devices leveraging the Security Management for Microsoft Defender for Endpoint feature.
   > - Only *Device Objects* are applicable for Microsoft Defender for Endpoint management. Targeting users is not supported.
   > - Policies configured will apply to both Microsoft Intune and Microsoft Defender for Endpoint clients

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. You can validate that settings have applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples) command utility.

## Monitor status

Status and reports for policies that target devices in this channel are available from the policy node under Endpoint security in the Microsoft Intune admin center.

Drill in to the policy type and then select the policy to view its status. The following policy types support MDE security configuration:

- Antivirus > *Microsoft Defender Antivirus*
- Firewall > *Microsoft Defender Firewall* or *Microsoft Defender Firewall Rules*
- Endpoint detection and response > *Endpoint detection and response*

When you select a policy, you'll see information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Frequently asked questions and considerations

### Device check-in frequency

Devices managed by this capability check-in with Microsoft Intune every 90 minutes to update policy.

You can manually sync a device on-demand from the [Microsoft 365 Defender portal](https://security.microsoft.com/). Sign-in to the portal and go to **Devices**. Select a device that is managed by MDE, and then select the **Policy sync** button:  

:::image type="content" source="./media/mde-security-integration/policy-sync-from-mde.png" alt-text="Manually sync devices managed by MDE." lightbox="./media/mde-security-integration/policy-sync-from-mde.png":::

The Policy sync button only appears for devices that are successfully managed by MDE. 

### Devices protected by Tamper Protection

If a device has Tamper Protection turned on, it will not be possible to edit its settings without turning off Tamper Protection. 

### Assignment Filters and Security Management for Microsoft Defender for Endpoint

Assignment filters aren't supported for devices communicating through the Microsoft Defender for Endpoint channel. While assignment filters can be added to a policy that could be targeted at these devices, the device will ignore assignment filters. For assignment filter support, the device must be enrolled in to Microsoft Intune.

### Deleting and removing devices

You can delete devices that use this flow using one of two methods:

- From within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **All devices**, select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column, and then select **Delete**.
- You can also remove devices from the scope of Configuration Management in the Security Center.

Once a device is removed from either location, that change will propagate to the other service.

### Unable to enable the Security Management for Microsoft Defender for Endpoint workload in Endpoint Security

Most initial provisioning flows are typically completed by an Administrator of both services (such as a Global Administrator). There are some scenarios where Role-based Administration is used to customize the permissions of administrators. Today, individuals who are delegated the *Endpoint Security Manager* role might not have the necessary permissions to enable this feature.

### Active Directory joined devices

Devices that are joined to Active Directory will use their **existing infrastructure** to complete the Hybrid Azure Active Directory join process. While the Defender for Endpoint component will start this process, the join action uses your Federation provider or Azure Active Directory Connect (Azure AD Connect) to complete the join. Review [Plan your hybrid Azure Active Directory join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) to learn more about configuring your environment.

To troubleshoot Azure Active Directory onboarding issues, see  [Troubleshoot Security Configuration Management Azure Active Directory onboarding issues](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt).

### Unsupported security settings

The following security settings are pending deprecation. The Security Management for Microsoft Defender for Endpoint flow doesn't support these settings:

- Expedite telemetry reporting frequency (under **Endpoint Detection and Response**)
- AllowIntrusionPreventionSystem (under **Antivirus**)

### Managing security configurations on domain controllers

Currently, devices aren't supported to complete a Hybrid Join to Azure Active Directory. Since an Azure Active Directory trust is required, domain controllers aren't currently supported. We're looking at ways to add this support.

### Server Core installation

Due to the platform limitations of Server core installations, these aren't supported by Security Management for Microsoft Defender for Endpoint.

### PowerShell restrict mode

Security Management for Microsoft Defender for Endpoint won't work for a device that has PowerShell *LanguageMode* configured with *ConstrainedLanguage* mode ‘enabled’. For more information, see [about_Language_Modes](/powershell/module/microsoft.powershell.core/about/about_language_modes) in the PowerShell documentation.

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)
