---
# required metadata

title: Intune endpoint detection and response policy.
description: Configure and deploy policies for devices you manage with endpoint security endpoint detection and response policy in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/27/2025
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

# Endpoint detection and response policy for endpoint security in Intune

When you integrate Microsoft Defender for Endpoint with Intune, you can use endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

Endpoint detection and response capabilities of Microsoft Defender for Endpoint provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

Applies to:

- Linux
- macOS
- Windows 10
- Windows 11
- Windows Server 2012 R2 and later *(when managed by Configuration Manager through the [tenant attach](../protect/tenant-attach-intune.md) scenario, or through the [Microsoft Defender for Endpoint Security settings management](../protect/mde-security-integration.md) scenario)*

## About Intune policy for endpoint detection and response

Intune's endpoint detection and response policies include platform-specific profiles to manage the onboarding installation of Microsoft Defender for Endpoint. Each profile includes an *onboarding package* that applies to the device platform that the policy targets. Onboarding packages are how devices are configured to work with Microsoft Defender for Endpoint. After a device onboards, you can start to use threat data from that device.

You create and manage EDR policies from *Endpoint detection and response* node that is in the *Endpoint security* node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

When you create EDR policy to onboard devices, you can use the preconfigured policy option, or create a policy that requires manual configuration of the settings, including identification of the onboarding package:

- **Preconfigured policy**: Supported for only Windows devices, use this option to rapidly deploy a preconfigured EDR onboarding policy to all applicable devices. You can use the preconfigured policy option for devices managed with Intune and for tenant attached devices managed through Configuration Manager. When using the preconfigured option, you can’t edit settings in the policy before its creation and initial deployment. After deployment, you can edit a few select settings. For more information, see [Use a preconfigured EDR policy](#use-a-preconfigured-edr-policy) in this article.

- **Manually create a policy**: Supported for all platforms, use this option to create an onboarding policy you can deploy to discrete groups of devices. When using this path, you can configure any of the available settings in the policy before it deploys to assigned groups. For more information, see [Use a manually created EDR policy](#use-a-manually-created-edr-policy) in this article.

Based on the platform a policy targets, EDR policies for devices you manage with Intune deploy to groups of devices from Microsoft Entra ID, or to collections of on-premises devices that you synchronize from Configuration Manager through the [tenant attach scenario](../protect/tenant-attach-intune.md).

> [!TIP]
> In addition to EDR policy, you can use [device configuration](../protect/advanced-threat-protection-configure.md) policy to onboard devices to Microsoft Defender for Endpoint. However, device configuration policies don't support tenant attached devices.
>
> When using multiple policies or policy types like *device configuration* policy and *endpoint detection and response* policy to manage the same device settings (such as onboarding to Defender for Endpoint), you can create policy conflicts for devices. To learn more about conflicts, see [Manage conflicts](../protect/endpoint-security-policy.md#manage-conflicts) in the *Manage security policies* article.

## Prerequisites for EDR policies

**General**:

- **Tenant for Microsoft Defender for Endpoint** – Your Microsoft Defender for Endpoint tenant must be integrated with your Microsoft Intune tenant (Intune subscription) before you can create EDR policies. For more information, see:

  - [Use Microsoft Defender for Endpoint](advanced-threat-protection.md) for guidance on integrating Microsoft Defender for Endpoint with Microsoft Intune.
  - [Connect Microsoft Defender for Endpoint to Intune](../protect/advanced-threat-protection-configure.md#connect-microsoft-defender-for-endpoint-to-intune) to set up the service-to-service connection between Intune and Microsoft Defender for Endpoint.

**Support for Configuration Manager clients**:

- **Set up tenant attach for Configuration Manager devices** - To support deploying EDR policy to devices managed by Configuration Manager, configure *tenant attach*. This task includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, including the synchronization of Configuration Manager collections to the Microsoft Intune admin center and enabling them to work with policies for endpoint security, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

  For more information about using EDR policies with tenant attached devices, see [Set up Configuration Manager to support EDR policy](#set-up-configuration-manager-to-support-edr-policy) in this article.

## Role-based access controls (RBAC)

For guidance on assigning the right level of permissions and rights to manage Intune endpoint detection and response policy, see [Assign-role-based-access-controls-for-endpoint-security-policy](../protect/endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy).

## About the endpoint detection and response node

In the Microsoft Intune admin center, the *Endpoint detection and response* node is divided into two tabs:

**Summary tab**:  
The Summary tab provides a high-level view of all your EDR policies, both manually configured policies and the policies you create using the Deploy preconfigured policy option.

The Summary tab includes the following areas:

- **Defender for Endpoint Connector status** – This view displays the current connector status for your tenant. The label, Defender for Endpoint Connector Status, is also a link that opens the Defender portal. This view is the same as found on the Endpoint security Overview page.

- **Windows devices onboarded to Defender for Endpoint** – This view shows a tenant-wide status for endpoint detection and response (EDR) onboarding, with counts for both devices that have or haven’t onboarded to Microsoft Defender for Endpoint.

- **Endpoint detection and response (EDR) policies** – Here you can create new manually configured EDR policies, and view the list of all EDR policies for your tenant. The policy list includes both manually configured policies and the policies you create using the Deploy preconfigured policy option.

  Selecting a policy from the list opens a deeper view of that policy where you can review its configuration and choose to edit its details and configuration. If the policy was preconfigured, the settings you can edit are limited.

**EDR Onboarding Status tab**:  
This tab displays a high-level summary of devices that have or haven’t onboarded to Microsoft Defender for Endpoint, and supports drilling into individual devices. This summary includes devices managed by Intune and devices that are managed through the tenant attach scenario and Configuration Manager.

This tab also includes the option to create and deploy a preconfigured onboarding policy for Windows devices.

The EDR onboarding status tab includes:

- **Deploy preconfigured policy** – This option appears near the top of the page, above the onboarding summary chart, and is used to create a preconfigured policy for onboarding Windows devices to Microsoft Defender for Endpoint.

- **The EDR onboarding status summary chart** – This chart displays the counts of devices that have or haven’t onboarded to Microsoft Defender for Endpoint.

- **Device list** – Below the summary chart is a list of devices with details, including:  
  - Device name
  - How the device is managed
  - The devices EDR onboarding status
  - Last check-in time and date
  - The last known state of the devices Defender sensor

## EDR profiles

### Devices managed by Microsoft Intune

#### Linux

To manage EDR for Linux devices, select the **Linux** platform. The following profiles are available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:
  - Devices enrolled with Intune.
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  EDR templates for Linux include two settings for the *Device tags* category from Defender for Endpoint:

  - **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.
  - **Type of tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.

  To learn more about Defender for Endpoint settings that are available for Linux, see [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

- **Microsoft Defender Global Exclusions (AV+EDR)** - Use this profile to manage both endpoint detection and response exclusion and Antivirus exclusions on Linux devices. Exclusions you can deploy through this profile are added to exclusions that devices might receive from other sources, including EDR and Antivirus exclusions managed by Intune or Microsoft Defender Antivirus policies. Settings from multiple sources are subject to policy merge, and create a super set of exclusions for applicable devices and users.

  This profile supports use with:
  - Devices enrolled with Intune.
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  The EDR global exclusion template for Linux includes a simple template where you can **Add** and then edit one or more instances of exclusion configurations. This is the same configuration process as when configuring Intune policy for [Microsoft Defender Antivirus Exclusions](../protect/endpoint-security-antivirus-policy.md#linux) for Linux devices. The EDR global exclusion profile for Linux doesn't replace Microsoft Defender Antivirus Exclusions profiles you might already use for Linux.

  To configure exclusions, each entry you add supports the following options: 
  - **Path** - Define a path to exclude from endpoint detection and response. This can be a file or directory. Wild cards aren't supported. 
  - **Process name** - Define a process name to exclude from endpoint detection and response. This can be a file name or full path. Wild cards aren't supported. 
  
For more information about Linux exclusions, see [Configure and validate exclusions for Microsoft Defender for Endpoint on Linux](/defender-endpoint/linux-exclusions) in the Microsoft Defender documentation.

#### macOS

To manage EDR for macOS devices, select the **macOS** platform. The following profile is available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:
  - Devices enrolled with Intune.
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  EDR templates for macOS include two settings for the *Device tags* category from Defender for Endpoint:

  - **Type of tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
  - **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.

  To learn more about Defender for Endpoint settings that are available for macOS, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.

#### Windows

To manage EDR for Windows devices, select the **Windows** platform. The following profile is available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:

  - Devices enrolled with Intune.
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  > [!NOTE]
  >
  > Beginning on April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows 10, Windows 11, and Windows Server* platform that is now named more simply as *Windows*.
  >
  > The *Windows* platform supports devices communicating through Microsoft Intune or Microsoft Defender for Endpoint. These profiles also add support for the Windows Server platform which isn't supported through Microsoft Intune natively.
  >
  > Profiles for this new platform use the settings format as found in the Settings Catalog. Each new profile template for this new platform includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.

  **Options for** ***Microsoft Defender for Endpoint client configuration package type***:
  
  - *Applies to Windows devices only*

  After you configure the [service-to-service connection](../protect/advanced-threat-protection-configure.md#connect-microsoft-defender-for-endpoint-to-intune) between Intune and Microsoft Defender for Endpoint, the **Auto from connector** option becomes available for the setting **Microsoft Defender for Endpoint client configuration package type**. This option isn't available until you configure the connection.

  When you select **Auto from connector**, Intune automatically gets the onboarding package (blob) from your Defender for Endpoint deployment. This choice replaces the need to manually configure an **Onboard** package for this profile. There isn't an option to automatically configure an offboard package.

### Devices managed by Configuration Manager

[!INCLUDE [EDR policy prerequisites](../includes/tenant-attach-edr-prerequisites.md)]

## Set up Configuration Manager to support EDR policy

Before you can deploy EDR policies to Configuration Manager devices, complete the configurations detailed in the following sections.

These configurations are made within the Configuration Manager console and to your Configuration Manager deployment. If you're not familiar with Configuration Manager, plan to work with a Configuration Manager admin to complete these tasks.

The following sections cover the required tasks:

1. [Install the update for Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Enable tenant attach](#task-2-configure-tenant-attach-and-synchronize-collections)

> [!TIP]
>
> To learn more about using Microsoft Defender for Endpoint with Configuration Manager, see the following articles in the Configuration Manager content:
>
> - [Onboard Configuration Manager clients to Microsoft Defender for Endpoint via the Microsoft Intune admin center](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Intune tenant attach: Device sync and device actions](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### Task 1: Install the update for Configuration Manager

Configuration Manager version 2002 requires an update to support use with Endpoint detection and response policies you deploy from the Microsoft Intune admin center.

**Update details**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

This update is available as an *in-console update* for Configuration Manager 2002.

To install this update, follow the guidance from [Install in-console updates](../../configmgr/core/servers/manage/install-in-console-updates.md) in the Configuration Manager documentation.

After installing the update, return here to continue configuring your environment to support EDR policy from the Microsoft Intune admin center.

### Task 2: Configure tenant attach and synchronize collections

With Tenant attach, you specify collections of devices from your Configuration Manager deployment to synchronize with the Microsoft Intune admin center. After collections synchronize, use the admin center to view information about those devices and to deploy EDR policy from Intune to them.

For more information about the Tenant attach scenario, see [Enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md) in the Configuration Manager content.

#### Enable tenant attach when co-management isn't enabled

> [!TIP]
> You use the **Co-management Configuration Wizard** in the Configuration Manager console to enable tenant attach, but you don't need to enable co-management.

If you're planning to enable co-management, be familiar with co-management, its prerequisites, and how to manage workloads before you continue. See [What is co-management](../../configmgr/comanage/overview.md) in the Configuration Manager documentation.

To enable tenant attach when co-management isn’t enabled, you’ll need to sign-in to the *AzurePublicCloud* for your environment. Before proceeding, review [Permissions and roles](../../configmgr/comanage/overview.md#permissions-and-roles) in the Configuration Manager documentation to ensure you have an account available that can complete the procedure.

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.
2. In the ribbon, select **Configure co-management** to open the wizard.
3. On the **Tenant onboarding** page, select **AzurePublicCloud** for your environment. Azure Government cloud isn't supported.
   1. Select **Sign In** and specify an account that has sufficient permissions to to your *AzurePublicCloud* environment.

The following are supported for devices you manage with Intune:

- Platform: **Windows** - Intune deploys the policy to devices in your Microsoft Entra groups.
- Profile: **Endpoint detection and response**

## Use a preconfigured EDR policy

Intune supports use of a preconfigured EDR policy for Windows devices managed by Intune, and by Configuration Manager through the tenant attach scenario.

On the *EDR Onboarding Status* page of Intune’s Endpoint detection and response policy, select the **Deploy preconfigured policy** option to have Intune create and deploy a preconfigured policy to install Microsoft Defender for Endpoint on applicable devices.

This option is found near the top of the page, above the Windows Devices onboarded to Defender for Endpoint report:

:::image type="content" source="./media/endpoint-security-edr-policy/edr-preconfigured-policy-option.png" alt-text="Screen shot of the admin center that shows where to find the Deploy preconfigured policy option.":::

Before you can select this option, you must successfully configure the **Defender for Endpoint Connector**, which establishes a service-to-service connection between Intune and Microsoft Defender for Endpoint. The policy uses the connector to get a Microsoft Defender for Endpoint onboarding blob for use to onboard devices. For information about configuring this connector, see [Connect Microsoft Defender for Endpoint to Intune](../protect/advanced-threat-protection-configure.md#connect-microsoft-defender-for-endpoint-to-intune) in the *Configure Defender for Endpoint* article.

If you use the tenant attach scenario to support devices managed by Configuration Manager, set up Configuration Manager to support EDR policy from the Microsoft Intune admin center. See [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

### Create the preconfigured EDR policy

When using the **Deploy preconfigured policy** option, you can’t change the default policy configurations for installing Microsoft Defender for Endpoint, scope tags, or assignments. However, after the policy is created, you can edit some of its details, including configuration of assignment filters.

To create the policy:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Endpoint detection and response** > open the **EDR Onboarding Status** tab > select **Deploy preconfigured policy**.

2. On the **Create a profile** page, specify one of the following combinations, and then select **Create**:

   - For devices managed by Intune:
      - Platform = **Windows**
      - Profile = **Endpoint detection and response**

   - For devices managed through the [tenant attach scenario](../protect/tenant-attach-intune.md):
      - Platform = **Windows (ConfigMgr)**
      - Profile = **Endpoint detection and response (ConfigMgr)**

     > [!IMPORTANT]
     >
     > Deployment to tenant attached devices requires the **All Desktop and Server Client** collection to be enabled and synchronized in your tenant.

3. On the **Basics** page, Provide a Name for this policy. Optionally, you can also add a Description.

4. On the **Review and Create** page, you can expand the available categories to review the policy configuration, but you can’t make changes. Intune only uses applicable settings based on the Platform and Profile combination you selected. For example, for devices managed by Intune, the policy targets the *All Devices* group. The *All Desktop and Server clients* group is targeted for tenant attached devices.

Select **Save** to create, and deploy the preconfigured policy.

### Edit a preconfigured EDR policy

After you create a preconfigured policy, you can find it on the **Summary** tab for Endpoint detection and response policy. By selecting a policy, you can then choose to edit some, but not all policy options. For example, for Intune devices, you can edit the following options:

- Basic: You can edit the following options:
  - Name
  - Description
- Configuration setting: The following two settings can be changed from their default of Not configured:
  - Sample Sharing
  - \[Deprecated] Telemetry Reporting Frequency
- Assignments: You can't change the group assignment, but you can add [Assignment filters](../fundamentals/filters.md).

## Use a manually created EDR policy

On the EDR Summary page of Intune’s Endpoint detection and response policy, you can select **Create Policy** to begin the process of manually configuring an EDR policy to onboard devices to Microsoft Defender for Endpoint.

This option is found near the top of the page, above the Windows Devices onboarded to Defender for Endpoint report:

:::image type="content" source="./media/endpoint-security-edr-policy/manually-create-edr-policy.png" alt-text="Screen shot of the admin center that shows where to find the Create Policy option.":::

### Create a manually configured EDR policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

3. Select the platform and profile for your policy. The following information identifies your options:

   - Intune - Intune deploys the policy to devices in your assigned groups. When you create the policy, select:

     - Platform: **Linux**, **macOS**, or **Windows**
     - Profile: **Endpoint detection and response**

   - Configuration Manager - Configuration Manager deploys the policy to devices in your Configuration Manager collections. When you create the policy, select:
     - Platform: **Windows (ConfigMgr)**
     - Profile: **Endpoint detection and response (ConfigMgr)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, Choose **Auto from Connector** for **Microsoft Defender for Endpoint Client configuration package type**. Configure the **Sample Sharing** and **Telemetry Reporting Frequency** settings you want to manage with this profile.

   > [!NOTE]
   > To onboard or offboard tenants using the onboarding file from the Microsoft Defender for Endpoint portal, select either *Onboard* or *Offboard* and supply the contents of the onboarding file to the input directly below the selection.

   When you're done configuring settings, select **Next**.

7. If you use Scope tags, on the **Scope tags** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.

   Select **Next** to continue.

8. On the **Assignments** page, select the groups or collections that receive this policy. The choice depends on the platform and profile you selected:

   - For Intune, select groups from Microsoft Entra.
   - For Configuration Manager, select the collections from Configuration Manager that have synced to the Microsoft Intune admin center and enabled for Microsoft Defender for Endpoint policy.

   You can choose not to assign groups or collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

## Update the onboarding state for a device

Organizations might need to update the onboarding information on a device via Microsoft Intune.

This update can be necessary due to a change in the onboarding payload for Microsoft Defender for Endpoint, or when directed by Microsoft support.

Updating the onboarding information directs the device to start utilizing the new onboarding payload at the next *Restart*.

> [!NOTE]
> This information won't necessarily move a device between tenants without fully offboarding the device from the original tenant. For options migrating devices between Microsoft Defender for Endpoint organizations, engage Microsoft Support.

### Process to update the payload

1. Download the new Mobile Device Management **New** onboarding payload from the Microsoft Defender for Endpoint console.

1. Create a **New Group** to validate the new policies effectiveness.

1. Exclude the **New Group** from your existing EDR policy.

1. Create a **New** Endpoint Detection and Response policy, outlined in [Create EDR policies](./endpoint-security-edr-policy.md#create-a-manually-configured-edr-policy).

1. While creating the policy, select **Onboard** from the client package configuration type, and specify the **contents** of the onboarding file from the Microsoft Defender for Endpoint console.

1. **Assign the policy** to the new group created for validation.

1. **Add** existing devices to the validation group and ensure the changes work as expected.

1. **Expand** the deployment gradually, eventually decommissioning the original policy.

> [!NOTE]
> If previously using the *Auto from connector* option to retrieve the onboarding information, engage Microsoft support to confirm the use of the new onboarding information.
>
> For organizations updating onboarding information at the direction of Microsoft support, Microsoft will direct you when the connector has been updated to use the new onboarding payload.

## EDR policy reports and monitoring

You can view details about the EDR policies you use in the endpoint deployment and response node of the Microsoft Intune admin center.

For policy details, in the admin center, go to **Endpoint security** > **Endpoint deployment and response** > **Summary** tab, and select the policy for which you want to view compliance details:

- For policies that target the **Linux**, **macOS**, or **Windows** platforms (Intune), Intune displays an overview of compliance to the policy. You can also select the chart to view a list of devices that received the policy, and drill-in to individual devices for more details.

- For Windows devices, the chart for **Windows devices onboarded to Defender for Endpoint** displays the count of devices that have successfully onboarded to Microsoft Defender for Endpoint and that have yet to onboard.

  To ensure you have full representation of your devices in this chart, deploy the onboarding profile to all your devices. Devices that onboard to Microsoft Defender for Endpoint by external means, like Group Policy or PowerShell, are counted as **Devices without the Defender for Endpoint sensor**.
- For policies that target the **Windows (ConfigMgr)** platform (Configuration Manager), Intune displays an overview of compliance to the policy that doesn't support drill-in to view additional details. The view is limited because the admin center receives limited status details from Configuration Manager, which manages the deployment of the policy to Configuration Manager devices.

To view details for individual devices, go to **Endpoint security** > **Endpoint deployment and response** > **EDR Onboarding Status** tab, and select a device from the list to view additional device-specific details.

## Next steps

- [Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy).
- Learn more about [endpoint detection and response](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) in the Microsoft Defender for Endpoint documentation.