---
# required metadata

title: Use Microsoft Defender for Endpoint Security Configuration Management in Microsoft Endpoint manager
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/02/2021
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
ms.collection: M365-identity-device-management
ms.reviewer: mattcall

---

# Manage Microsoft Defender for Endpoint on devices with Microsoft Endpoint Manager

With Microsoft Defender for Endpoint (MDE), you can now deploy security configurations from Microsoft Endpoint Manager directly to your onboarded devices without requiring a full Microsoft Endpoint Manager device enrollment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this capability, devices that aren’t managed by a Microsoft Endpoint Manager, either Microsoft Intune or Microsoft Endpoint Configuration Manager, can receive security configurations for Microsoft Defender directly from Endpoint Manager.

When devices are managed through this capability:

- You use the Microsoft Endpoint Manager admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups
- Devices get the policies based on their Azure Active Directory device object. A device that isn’t already present in Azure Active Directory is joined as part of this solution
- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the devices status. The device's status is available in the Microsoft Endpoint Manager admin center

This scenario extends the Microsoft Endpoint Manager Endpoint Security surface to devices that aren't capable of enrolling in Endpoint Manager. When a device is managed by Endpoint Manager, either through Intune or Configuration Manager), the device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune or Configuration Manager to deploy policy for Defender to your devices.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

## Prerequisites

Review the following sections for requirements for the Security Management for Microsoft Defender for Endpoint Scenario:

### Environment

When a device onboards to Microsoft Defender for Endpoint:

- The device is surveyed for an existing Endpoint Manager presence, either Configuration Manager or Intune
- Devices without an Endpoint Manager presence enable the Security Management feature
- A trust is created with Azure Active Directory if one doesn't already exist
- Azure Active Directory trust is used to communicate with Endpoint Manager (Intune) and retrieve policies
- Policy retrieve from Endpoint Manager is enforced on the device by Microsoft Defender for Endpoint

### Active Directory Requirements

When a device that is domain joined creates a trust with Azure Active Directory, this scenario is referred to as a *Hybrid Azure Active Directory Join* scenario. The Security Management for MDE fully supports this scenario with the following requirements:

- Azure Active Directory Connect (AAD Connect) must be synchronized to the tenant that is used from Microsoft Defender for Endpoint
- Hybrid Azure Active Directory Join must be configured in your environment (either through Federation or AAD Connect Sync)
- AAD Connect Sync must include the device objects *in scope* for synchronization with Azure Active Directory (when needed for join)
- AAD Connect rules for sync must be modified for Server 2012 R2 (when support for Server 2012 R2 is needed)

### Connectivity Requirements

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` – For Azure AD registration.
- `login.microsoftonline.com` – For Azure AD registration.
- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

### Supported platforms

Policies for MDE security management are supported for the following device platforms:

- Windows 10 Professional/Enterprise (With KB5006738)
- Windows 11 Professional/Enterprise (With KB5007262)
- Windows Server 2012 R2 with Microsoft Defender for Down-Level Devices
- Windows Server 2019 with Microsoft Defender for Down-Level Devices
- Windows Server 2022 (with KB5006745)

### Licensing and subscriptions

To use security management for MDE, you need:

- A subscription that grants licenses for Microsoft Defender for Endpoint, like Microsoft 365, or a standalone license for only Microsoft Defender for Endpoint. For current information about options, see [Minimum requirements for Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/minimum-requirements?view=o365-worldwide).

  *Any subscription* that grants MDE licenses also grants your tenant access to the Endpoint security node of the Microsoft Endpoint Manager admin center. The Endpoint security node is where you’ll configure and deploy policies to manage MDE for your devices and monitor device status.

## Architecture

The following diagram is a conceptual representation of the MDE security configuration management solution.

:::image type="content" source="./media/mde-security-integration/mde-architecture.png" alt-text="Conceptual representation of the MDE security configuration management solution.":::

1. Devices onboard to MDE.

2. A trust is established between each device and Azure AD. When a device has an existing trust, that is used. When devices haven't registered, a new trust is created.

3. Devices use their Azure AD Identity to communicate with Endpoint Manager. This identity enables Microsoft Endpoint Manager to distribute policies that are targeted to the devices when they check in.

4. Defender for Endpoint reports the status of the policy back to Endpoint Manager.

## Which solution should I use?

Microsoft Endpoint Manager includes several methods and policy types to manage the configuration of Defender for Endpoint on devices.

The following table can help you understand which policies that can configure MDE settings are supported by devices that are managed by the different scenario. When you deploy a policy that’s supported for both *MDE security configuration* and *Microsoft Endpoint Manager*, a single instance of that policy can be processed by devices that run MDE only and devices that are managed by either Intune or Configuration Manager.

| Microsoft Endpoint Manager  | Policy options  | MDE Security configuration  |  Microsoft Endpoint Manager (Intune and Configuration Manager)  |
|----------------|----------------|-------------------|------------|
| Endpoint security    | Antivirus                   | ![Supported](./media/certificates-configure/green-check.png)  | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Attack surface reduction    |           | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Endpoint detection and response        | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Firewall                | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Firewall rules          | ![Supported](./media/certificates-configure/green-check.png) | ![Supported](./media/certificates-configure/green-check.png)  |
|         | Security baselines  |       | ![Supported](./media/certificates-configure/green-check.png)  |
| Device configuration | Device restriction (template)   |    | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Endpoint Protection (template)  |    | ![Supported](./media/certificates-configure/green-check.png)  |
|                      | Settings catalog                |    | ![Supported](./media/certificates-configure/green-check.png)  |

**Endpoint security policies** are discrete groups of settings intended for use by security admins who focus on protecting devices in your organization.

- **Antivirus** policies manage the security configurations found in Microsoft Defender for Endpoint. See  [antivirus](../protect/endpoint-security-antivirus-policy.md) policy for endpoint security.
- **Attack surface reduction** policies focus on minimizing the places where your organization is vulnerable to cyberthreats and attacks. For more information, see [Overview of attack surface reduction](/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation, and [attack surface reduction](../protect/endpoint-security-asr-policy.md) policy for endpoint security.
- **Endpoint detection and response** (EDR) policies manage the Defender for Endpoint capabilities that provide advanced attack detections that are near real-time and actionable. Based on EDR configurations, security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats. See [endpoint detection and response](../protect/endpoint-security-edr-policy.md) policy for endpoint security.
- **Firewall** policies focus on the Defender firewall on your devices. See [firewall](../protect/endpoint-security-firewall-policy.md) policy for endpoint security. 
- **Firewall Rules** configure granular rules for Firewalls, including specific ports, protocols, applications, and networks. See [firewall](../protect/endpoint-security-firewall-policy.md) policy for endpoint security.
- **Security baselines** include preconfigured security settings that define the Microsoft recommended security posture for different products like Defender, Edge, or Windows. The default recommendations are from the relevant product teams and enable you to quickly deploy that recommended secure configuration to devices. While settings are preconfigured in each baseline, you can create customized instances of them to establish your organization’s security expectations. See [security baselines](../protect/security-baselines.md) for Intune.

**Device configuration policies** are intended for use by Administrators who manage a broad range of device settings and can often extend beyond a device security focus.

- **Device restriction** policies use a template that include a logical grouping of device settings that manage how users share data, which apps are allowed or prohibited, and similar concepts. See configure [device restriction](../configuration/device-restrictions-configure.md) settings.
- **Endpoint protection** policies use a template that  include a range of settings from disk encryption, BitLocker, and Antivirus settings. See configure [endpoint Protection](../protect/endpoint-protection-configure.md) settings.
- **Settings catalog** policies don’t use templates of related settings. Instead, you select each setting you want the policy to manage. This type of policy has no predetermined focus as do templates for device configuration or endpoint security policies. See [settings catalog](../configuration/settings-catalog.md) to configure settings on devices.

## Configure your Tenant to support MDE Security Configuration Management

To support MDE security configuration management through the Microsoft Endpoint Manager admin center, you must enable communication between them from within each console.

1. Sign in to [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Configuration Management** > **Enforcement Scope** and enable the platforms for security settings management:

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-defender.png" alt-text="Enable MDE settings management in the Defender console.":::

2. Make sure the relevant users have permissions to manage endpoint security settings in Microsoft Endpoint Manager or grant those permissions by configuring a role in the Defender portal. Go to **Settings** > **Roles** > **Add item**:

   :::image type="content" source="./media/mde-security-integration/add-role-in-mde.png" alt-text="Create a new role in the Defender portal.":::

   > [!TIP]
   > You can modify existing roles and add the necessary permissions versus creating additional roles in Microsoft Defender for Endpoint

3. When configuring the role, add users and be sure to select **Manage endpoint security settings in Microsoft Endpoint Manager**:

   :::image type="content" source="./media/mde-security-integration/add-role.png" alt-text="Grant users permissions to manage settings.":::

4. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations (Preview)** to **On**.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-mem.png" alt-text="Enable MDE settings management in the Microsoft Endpoint Manager admin center.":::

   When you set this option to *On*, all devices in the platform scope in Microsoft Defender for Endpoint that aren't managed by Microsoft Endpoint Manager will qualify to onboard to Microsoft Defender for Endpoint.

## Onboard devices to Microsoft Defender for Endpoint

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboarding tools and methods for Windows devices](/microsoft-365/security/defender-endpoint/security-config-management?view=o365-worldwide) in the Defender for Endpoint documentation.

Devices that you manage with Intune or Configuration Manager are not supported for this scenario.

## Create Azure AD Groups

After devices onboard to Defender for Endpoint, you'll need to create device groups to support deployment of policy for MDE.

To identify devices that have enrolled with MDE but aren't managed by Intune or Configuration Manager:

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Devices** > **All devices**, and then select the column **Managed by** to sort the view of devices.

   Devices that onboard to MDE and have registered but aren't managed by Intune or Configuration Manager display **MDE** in the *Managed by* column. These are the devices that can receive policy for security management for Microsoft Defender for Endpoint.

You can create groups for these devices [in Azure AD](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) or [from within the Microsoft Endpoint Manager admin center](../fundamentals/groups-add.md).

## Deploy policy

After creating one or more Azure AD groups that contain devices managed by MDE, you can create and deploy the following policies for Security Management for Microsoft Defender for Endpoint to those groups:

- Antivirus
- Firewall
- Firewall Rules
- Endpoint Detection and Response

> [!TIP]
> Avoid deploying multiple policies that manage the same setting to a device.
>
> Microsoft Endpoint Manager supports deploying multiple instances of each endpoint security policy type to the same device, with each policy instance being received by the device separately. Therefore, a device might receive separate configurations for the same setting from different policies, which results in a conflict. Some settings (like Antivirus Exclusions) will merge on the client and apply successfully.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Endpoint security** and then select the type of policy you want to configure, either Antivirus or Firewall, and then select **Create Policy**.

3. Enter the following properties or the policy type you selected:

   - For Antivirus policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Microsoft Defender Antivirus (Preview)**

   - For Firewall policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Microsoft Defender Firewall (Preview)**

   - For Firewall Rules policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Microsoft Defender Firewall Rules (Preview)**

   - For Endpoint Detection and Response policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Endpoint detection and response (Preview)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, select the settings you want to manage with this profile. To learn more about a setting, expand its information dialog and select the *Learn more* link to view the CSP information for the setting in the on-line documentation.

   When your done configuring settings, select **Next**.

7. On the **Assignments** page, select the Azure AD groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next** to continue.

   > [!TIP]
   >
   > - Assignment filters are not supported for Security Configuration Management profiles.
   > - Only *Device Objects* are applicable for Microsoft Defender for Endpoint management. User targeting is not supported.
   > - Policies configured will apply to both Microsoft Intune and Microsoft Defender for Endpoint clients

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. You can validate that settings are applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples?view=windowsserver2019-psreserve-view=true) command utility.

## Monitor status

Status and reports for MDE policies are available from the policy node under Endpoint security in the Microsoft Endpoint Manager admin center.

Drill in to the policy type, Antivirus or Firewall, and then select the policy to view its status. Policies for MDE have a *Policy type* of either *Microsoft Defender Antivirus (Preview)* or *Microsoft Defender Firewall (Preview)*.

When you select a policy, you'll see information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)  
[Troubleshoot security configuration management onboarding issues](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt?view=o365-21vianet&branch=security-config)