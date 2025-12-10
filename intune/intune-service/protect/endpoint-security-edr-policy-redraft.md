---
title: Deploy endpoint detection and response policy with Intune
description: Use Microsoft Intune endpoint security policies to configure and deploy Microsoft Defender for Endpoint EDR capabilities to Windows, macOS, and Linux devices.
author: brenduns
ms.author: brenduns
ms.date: 12/09/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: laarrizz

---

# Deploy endpoint detection and response policy with Intune

When you integrate Microsoft Defender for Endpoint with Intune, you can use endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

Intune policies for EDR include platform-specific profiles that manage the onboarding (installation) of Microsoft Defender for Endpoint. Use of onboarding packages is how devices are configured to work with Microsoft Defender for Endpoint. Onboarding to Defender through Intune EDR policies configures devices to send security telemetry to Microsoft Defender for Endpoint, enabling advanced threat detection, investigation, and response capabilities.

This article covers EDR deployment scenarios, from automatic connector-based deployment to manual configuration for specialized environments.

> [!TIP]
> In addition to EDR policy, you can use [device configuration](../protect/microsoft-defender-integrate.md) policy to onboard devices to Microsoft Defender for Endpoint. However, device configuration policies don't support tenant attached devices.
>
> When using multiple policies or policy types like *device configuration* policy and *endpoint detection and response* policy to manage the same device settings (such as onboarding to Defender for Endpoint), you can create policy conflicts for devices. To learn more about conflicts, see [Manage policy conflicts](../protect/endpoint-security-policy.md#manage-policy-conflicts).

## Understanding EDR onboarding

EDR onboarding configures devices so they can send security telemetry to your Defender for Endpoint tenant. The onboarding package is a platform-specific configuration file containing:

- **Tenant configuration**: Identifies your specific Defender for Endpoint organization.
- **Service endpoints**: URLs for communicating with Defender services.
- **Authentication material**: Certificates and tokens for secure device-to-service communication.
- **Basic configuration**: Device registration settings and initial communication parameters.

**Key concepts:**
- Devices appear in the Defender portal shortly after successful onboarding and initial telemetry submission.
- Onboarding enables telemetry flow, but doesn't configure advanced settings such as attack surface reduction, firewall, or antivirus policies.
- EDR policies don't manage threat hunting rules, custom detection logic, response automation, or investigation workflows.

For technical details, see [Onboard devices to Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/onboard-configure).

Applies to:

- Linux
- macOS
- Windows
- Windows Server 2012 R2 and later is supported when devices are managed through one of the following:
  - Configuration Manager (tenant attach)
  - Microsoft Defender for Endpoint security settings management

> [!IMPORTANT]
> On October 14, 2025, Windows 10 reached end of support and won't receive quality and feature updates. Windows 10 is an allowed version in Intune. Devices running this version can still enroll in Intune and use eligible features, but functionality isn't guaranteed and can vary.

## Prerequisites

Before you deploy EDR policies, confirm that your organization meets the licensing and permission requirements.

### License

- Microsoft Intune Plan 1


You need licenses for Microsoft Defender:  
- Defender for Endpoint Plan 1 license per user
- Microsoft 365 E5/A5/G5 (includes Defender for Endpoint Plan 2)
- Microsoft Defender XDR (standalone)

For detailed licensing information, see:
- [Microsoft Intune licensing](/mem/intune/fundamentals/licenses)
- [Microsoft Defender for Endpoint licensing](/microsoft-365/security/defender-endpoint/minimum-requirements#licensing-requirements)

### Role-based access control

To configure EDR policy, your account must be assigned an Intune role with sufficient role-based access control (RBAC) permissions:

- **Endpoint Security Manager**: The Endpoint Security Manager role includes permissions to create and manage endpoint security policies.
- **Custom role**: At minimum, *Create*/*Read*/*Update*/*Delete* permissions for *Endpoint security*.

You also need permissions in Microsoft Defender for Endpoint to establish the service connection:
- **[Security Administrator](/entra/identity/role-based-access-control/permissions-reference#security-administrator)** role in Microsoft Entra ID, or
- **Custom role** with equivalent permissions: *microsoft.directory/applications/create*, *microsoft.directory/applications/delete*, *microsoft.directory/servicePrincipals/create*

For detailed permission guidance, see [Role-based access control for endpoint security](../protect/endpoint-security-policy.md#role-based-access-control-for-endpoint-security).

## Supported platforms and profiles

**Windows:**

- **Profile**: *Endpoint detection and response*  
  - **Sample sharing**: Choose how devices send file samples to Defender for Endpoint.
  - **Onboarding options**: *Auto from connector* (available when the service connection is configured) or manually add an *Onboard* or *Offboard* package.
    - Auto from connector (recommended when the service-to-service connection is configured).
    - Manual onboarding using an *Onboard* or *Offboard* package from the Defender portal.
  - **Management**: Intune-enrolled devices, or unenrolled devices through [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

**macOS:**

- **Profile**: *Endpoint detection and response*
  - **Device tags**: Device tags include a *name* and *value* pair used to organize devices in Defender for Endpoint.
  - **Management methods**:
    - Intune-enrolled
    - [Defender for Endpoint security settings management](../protect/mde-security-integration.md)

**Linux:**

- **Profiles**:
  - *Endpoint detection and response*
    - **Device tags**: Device tags include a *name* and *value* pair used to organize devices in Defender for Endpoint.
    - **Management methods**:
      - Intune-enrolled
      - [Defender for Endpoint security settings management](../protect/mde-security-integration.md)
  - *Microsoft Defender Global Exclusions (AV+EDR)* - See [Linus global exclusions profile](#create-a-linux-global-exclusions-policy) later in this article.
  
**Windows Server 2012 R2+:**

- **Profile**: *Endpoint detection and response (ConfigMgr)*
  - **Management**:
    - Configuration Manager tenant attach
    - [Defender for Endpoint security settings management](../protect/mde-security-integration.md).
  - **Collection targeting**: Assign to Configuration Manager collections instead of Entra ID groups.
  - **Requirements**:
    - KB4563473 hotfix
    - Collections synchronized to Intune for assignments
    - Assignments are applied to Configuration Manager collections, not Entra ID groups

## Configure the Intune–Defender for Endpoint connection

Intune requires a connection to Microsoft Defender for Endpoint to automatically retrieve onboarding packages and support EDR policy deployment.

When the connection is enabled:

- Intune retrieves the latest onboarding package from Defender for Endpoint.
- Policy creation uses the most recent onboarding configuration.
- You can use **Auto from connector** in EDR profiles.

**To configure the connection:**

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Connectors and tokens** > **Microsoft Defender for Endpoint**.
2. Select **Connect Microsoft Defender for Endpoint to Intune**.
3. Enable the connection and configure data sharing preferences.
4. Verify the connection status shows **Connected**.

> [!TIP]
> Connection verification can take up to 15 minutes. If the connection fails, confirm that your account has Security Administrator permissions in both Intune and Defender for Endpoint.

For detailed setup instructions, see [Connect Microsoft Defender for Endpoint to Intune](../protect/microsoft-defender-integrate.md#connect-microsoft-defender-for-endpoint-to-intune).

## Deploy EDR policy

**About the Endpoint detection and response node:**

In the Intune admin center, the Endpoint detection and response node include:
- **Summary** -  Lists all EDR policies and the connector status.
- **EDR Onboarding Status** - Shows onboarding progress and allows deployment of the preconfigured Windows policy.

Every device that reports security telemetry to Microsoft Defender for Endpoint must be onboarded using a configuration package (called an onboarding "blob"). This package contains:

- Tenant-specific configuration - Tells the device which Defender for Endpoint organization to report to.
- Authentication certificates - Enables secure communication with Defender services.
- Reporting settings - Configures what data to send and how frequently.

Whether you use automatic or manual deployment, Intune applies the same onboarding configuration to devices. The difference is how Intune obtains that configuration:

- **Automatic** (recommended) - Intune retrieves the onboarding package from Defender for Endpoint through the configured service connection.
- **Manual** - Use an onboarding package downloaded from the Defender portal when automatic retrieval isn't available.

> [!NOTE]
> The onboarding package is stable and only requires updating in rare scenarios, like when wporking with Microsoft to move your tenant to a new [datacenter geography](/microsoft-365/enterprise/m365-dr-overview#migrationsmoves).

**Choosing your deployment method:**

| Scenario | Recommended Method | Configuration Package Type |
|----------|-------------------|---------------------------|
| No service connection configured between Intune and Defender for Endpoint | [Manual EDR policy](#manual-edr-policy-creation) | Onboard |
| Quick deployment to all Windows devices with service connection active | [Preconfigured Windows EDR policy](#deploy-the-preconfigured-windows-edr-policy) | Auto from connector |
| Targeted deployment with custom settings and active service connection | [Custom automatic EDR policy](#create-custom-edr-policy-all-platforms) | Auto from connector |
| Multiple Defender tenants or air-gapped environments | [Manual EDR policy](#manual-edr-policy-creation) | Onboard |
| Strict change control requiring manual package management | [Manual EDR policy](#manual-edr-policy-creation) | Onboard |


### Create an automatic EDR policy

Best for environments with standard Intune + Defender integration and a single Defender for Endpoint tenant.

**Prerequisites:** Active [service-to-service connection](#configure-the-intunedefender-for-endpoint-connection) between Intune and Defender for Endpoint.

#### Deploy the preconfigured Windows EDR policy

1. Go to **Endpoint security** > **Endpoint detection and response** > **EDR Onboarding Status** tab.
2. Select **Deploy preconfigured policy**.
3. Choose your deployment scope:
   - **Windows + Endpoint detection and response**: Intune-managed devices
   - **Windows (ConfigMgr) + Endpoint detection and response (ConfigMgr)**: Configuration Manager collections
4. Provide a descriptive policy name and optional description.
5. Select **Create** to deploy immediately to all applicable devices.

#### Create custom EDR policy (all platforms)

1. Go to **Endpoint security** > **Endpoint detection and response** > **Create Policy**.
2. Select platform and profile:
   - **Platform**: *Windows*, *macOS*, or *Linux*
   - **Profile**: Endpoint detection and response
3. Configure policy basics with a descriptive name.
4. On **Configuration settings**:
   - **Microsoft Defender for Endpoint client configuration package type**: Select **Auto from connector** (this option only appears when the service-to-service connection is configured).
   - **Sample Sharing**: Choose based on your data sensitivity requirements:
     - **All samples**: Maximum threat detection capability
     - **Send safe samples**: Balanced approach (recommended)
     - **None**: Minimal data sharing
   - **Device Tags** (macOS and Linux only): Configure Type and Value for device filtering and grouping.
5. Assign to appropriate groups.
6. Review and create the policy.

### Manual EDR policy creation

Use this method when your organization can't use the service connection (multiple tenants, air-gapped environments, or strict change control).

**Download the onboarding package**:

1. In the [Microsoft Defender portal](https://security.microsoft.com/), go to **Settings** > **Endpoints** > **Device management** > **Onboarding**.
2. Select the operating system and choose **Mobile Device Management / Microsoft Intune**.
3. Select **Download package**.

**Create the policy**:

1. In Intune, go to **Endpoint security** > **Endpoint detection and response** > **Create Policy**.
2. Select the platform and profile.
3. For **Package type**, choose **Onboard** or **Offboard**.
4. Paste the contents of the downloaded onboarding file.
5. Configure remaining settings, then assign and create the policy.

## Additional profiles for Linux devices

After creating your core EDR policies, you can deploy additional specialized profiles for enhanced security management.

### Create a Linux Global Exclusions policy

> [!NOTE]
> **Linux Global Exclusions**: For Linux devices managed through [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md), you can create a separate **Microsoft Defender Global Exclusions (AV+EDR)** profile. This profile supports path and process name exclusions without wildcards. For details, see [Endpoint detection and response policy for Linux](../protect/endpoint-security-edr-policy.md#linux).


1. Go to **Endpoint security** > **Endpoint detection and response** > **Create Policy**.
2. Select **Linux** for platform and **Microsoft Defender Global Exclusions (AV+EDR)** for profile.
3. Configure exclusions by adding entries with:
   - **Path**: File or directory path to exclude (no wildcards supported).
   - **Process name**: Process name to exclude from EDR monitoring (no wildcards supported).
4. Assign to Linux device groups managed through MDE security settings management.

> [!IMPORTANT]
> Global exclusions are combined with other exclusion sources and result in the union of all exclusions. Adding exclusions can reduce threat detection coverage.

## Configuration Manager deployment

### Tenant attach

Tenant attach enables Intune to deploy EDR policies to Configuration Manager–managed Windows devices.

**Configuration Manager requirements**:  
- Current Branch **2002** or later
- For **2002**, install **KB4563473** (hotfix)

**Tenant attach configuration**:  
- Synchronize device collections to Intune (Cloud Sync).
- Ensure **All Desktop and Server Client** is enabled and synchronized (required for preconfigured Windows EDR policies).

**Permissions**:  
- **Intune Service Administrator** Entra ID built-in role, or equivalent role for tenant attach and endpoint security policy management. 

#### Set up Configuration Manager for EDR

1. **Install Configuration Manager update**: Apply KB4563473 hotfix for Configuration Manager 2002.
2. **Configure tenant attach**: Synchronize Configuration Manager collections to Intune.
3. **Verify connectivity**: Confirm that collections appear in both Configuration Manager and Intune admin centers.

#### Deploy EDR policy to Configuration Manager collections

1. In the Intune admin center, go to **Endpoint security** > **Endpoint detection and response** > **Create Policy**.
2. Select **Windows (ConfigMgr)** platform and **Endpoint detection and response (ConfigMgr)** profile.
3. Configure the same policy settings available for Intune-managed devices.
4. On **Assignments**, select Configuration Manager collections instead of Entra ID groups.
5. Create and deploy the policy.

After you deploy the policy, allow time for **Intune-ConfigMgr synchronization** and **Configuration Manager client policy** evaluation before devices show as onboarded.

For detailed tenant attach configuration, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

## Monitor and validate EDR deployment

**Intune reporting:**  

You can review deployment and onboarding results in the Intune admin center:

1. **Policy compliance**: Go to **Endpoint security** > **Endpoint detection and response** and select your policy to view deployment status.
2. **EDR Onboarding Status tab**: Check for tenant-wide device onboarding summary and drill down to individual device status.
3. **Device details**: Select devices for detailed onboarding status and sensor health.

**Microsoft Defender portal validation:**

In the Defender portal:

1. **Device inventory** (**Assets** > **Devices**) lists onboarded devices shortly after telemetry is received.
2. **Sensor health** shows last seen time, sensor version, and communication status.

3. **Risk assessment** begins after devices submit their initial telemetry.

### Ongoing monitoring

Review the following to ensure continued onboarding success:

- Policy deployment success rates
- Device onboarding status
- Sensor health and communication
- Failed deployments requiring remediation

### Troubleshooting

**Devices do not appear in the Defender portal**

- Confirm the device can reach required endpoints (for example, *.securitycenter.windows.com and *.protection.outlook.com).
- Check the EDR policy compliance status in Intune.
- Ensure the Microsoft Defender for Endpoint service is running on the device.

**"Auto from connector" option isn't available**

- Verify that the Defender connection shows **Connected** under **Tenant administration** > **Connectors and tokens**.
- Allow up to 15 minutes after enabling the connection for the option to appear.
- Ensure your account has appropriate administrative permissions.

For more information, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](/microsoft-365/security/defender-endpoint/troubleshoot-onboarding).

## Offboarding devices

Intune EDR policy supports the option to use an offboarding blob to offboard devices. Offboarding devices from Defender for Endpoint is typically an uncommon but planned process. Some situations that require offboarding include but aren't limited to moving a device out of a test lab, part of device lifecycle management, or required during tenant consolidation.

**To create an offboarding policy:**

1. Download a new offboarding package from the [Microsoft Defender portal](https://security.microsoft.com/) by going to **Settings** > **Endpoints** > **Device management** > **Offboarding**.
2. Select the operating system and choose **Mobile Device Management / Microsoft Intune**.
3. Select **Download package**.
4. Either create a new EDR policy with **Package type** set to **Offboard** and paste the offboarding blob contents, or update an existing offboarding policy by replacing the blob content.

When deploying an offboarding EDR policy in Intune:

- For security reasons, the offboarding blob, or package from Defender will expire seven days after being downloaded. Expired offboarding packages sent to devices are rejected.
- When deployed to a device, the offboarding blob disables the Defender for Endpoint sensor but doesn't remove the Defender for Endpoint client. Offboarding disables but doesn't remove Defender for Endpoint from a device.
- Devices stop sending telemetry to the Defender for Endpoint portal.
- Devices show as "inactive" in Defender after seven days.
- The Intune EDR policy compliance status should show successful deployment.
- Historical data remains in Defender until retention policies remove it.

When you offboard a device from Defender for Endpoint:

- **Telemetry stops**: No new detections, vulnerability, or security data are sent to the Microsoft Defender portal.
- **Device status changes**: Seven days after offboarding, the device's status changes to "inactive".
- **Data retention**: Past data (alerts, vulnerabilities, device timeline) remains in the Defender portal until the configured retention period expires.
- **Device visibility**: The device profile (without data) remains visible in the device inventory for up to 180 days.
- **Exposure score**: Devices inactive for 30+ days don't factor into your organization's exposure score.

For more information, see the following subjects in the Microsoft Defender for Endpoint documentation:

- [Offboard devices using Mobile Device Management tools](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-endpoints-mdm#offboard-devices-using-mobile-device-management-tools)
- [Offboard devices](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/offboard-machines)

## Related content

After onboarding devices with EDR policies, consider deploying additional endpoint security controls:

- [Attack surface reduction rules](/intune/intune-service/protect/endpoint-security-asr-policy)
- [Anti-malware policies](/intune/intune-service/protect/endpoint-security-antivirus-policy)
- [Firewall policies](/intune/intune-service/protect/endpoint-security-firewall-policy)
- [Device compliance policies](/intune/intune-service/protect/device-compliance-get-started)
