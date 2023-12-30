---
# required metadata

title: Manage endpoint detection and response settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security endpoint detection and response policy in Microsoft Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/15/2023
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

# Endpoint detection and response policy for endpoint security in Intune

When you integrate Microsoft Defender for Endpoint with Intune, you can use endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

Applies to:

- Linux
- macOS
- Windows 10/11
- Windows Server 2012 R2 and later

Endpoint detection and response capabilities of Microsoft Defender for Endpoint provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

EDR policies include platform-specific profiles to manage settings for EDR. The profiles automatically include an *onboarding package* for Microsoft Defender for Endpoint. Onboarding packages are how devices are configured to work with Microsoft Defender for Endpoint. After a device onboards, you can start to use threat data from that device.

EDR policies deploy to groups of devices in Microsoft Entra ID that you manage with Intune, and to collections of on-premises devices that you manage with Configuration Manager, including Windows servers. The EDR policies for the different management paths require different onboarding packages. Therefore, create separate EDR policies for the different types of devices you manage.

Find the endpoint security policies for EDR under *Manage* in the **Endpoint security** node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Prerequisites for EDR policies

**General**:

- **Tenant for Microsoft Defender for Endpoint** – Your Microsoft Defender for Endpoint tenant must be integrated with your Microsoft Intune tenant (Intune subscription) before you can create EDR policies. See [Use Microsoft Defender for Endpoint](advanced-threat-protection.md) in the Intune documentation.

**Support for Configuration Manager clients**:

- **Set up tenant attach for Configuration Manager devices** - To support deploying EDR policy to devices managed by Configuration Manager, configure *tenant attach*. This task includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, including the synchronization of Configuration Manager collections to the Microsoft Intune admin center and enabling them to work with policies for endpoint security, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

## EDR profiles

### Devices managed by Microsoft Intune

**Linux** - To manage EDR for Linux devices, select the **Linux** platform. The following profile is available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:
  - Devices enrolled with Intune
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  EDR templates for Linux include two settings for the *Device tags* category from Defender for Endpoint:

  - **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.
  - **Type of  tag**  – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.

  To learn more about Defender for Endpoint settings that are available for Linux, see [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

**macOS** - To manage EDR for macOS devices, select the **macOS** platform. The following profile is available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:
  - Devices enrolled with Intune
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  EDR templates for macOS include two settings for the *Device tags* category from Defender for Endpoint:

  - **Type of  tag**  – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
  - **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn’t be repeated in the same profile.

  To learn more about Defender for Endpoint settings that are available for macOS, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.

**Windows** - To manage EDR for Windows devices, select the **Windows 10, Windows 11, and Windows Server** platform. The following profile is available:

- **Endpoint detection and response** - Intune deploys the policy to devices in your assigned groups. This profile supports use with:

  - Devices enrolled with Intune
  - Devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md?pivots=mdssc-preview).

  > [!NOTE]  
  > Beginning on April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows 10, Windows 11, and Windows Server* platform.
  >
  > The *Windows 10, Windows 11, and Windows Server* platform supports devices communicating through Microsoft Intune or Microsoft Defender for Endpoint. These profiles also add support for the Windows Server platform which is not supported through Microsoft Intune natively.
  >
  > Profiles for this new platform use the settings format as found in the Settings Catalog. Each new profile template for this new platform includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.

  **Options for** ***Microsoft Defender for Endpoint client configuration package type***:
  
  - *Applies to Windows devices only*

  After you configure the [service-to-service connection](../protect/advanced-threat-protection-configure.md#connect-microsoft-defender-for-endpoint-to-intune) between Intune and Microsoft Defender for Endpoint, the **Auto from connector** option becomes available for the setting **Microsoft Defender for Endpoint client configuration package type**. This option isn't available until you've configured the connection.

  When you select **Auto from connector**, Intune automatically gets the onboarding package (blob) from your Defender for Endpoint deployment. This replaces the need to manually configure an **Onboard** package for this profile. There's no option to automatically configure an offboard package.

### Devices managed by Configuration Manager

[!INCLUDE [EDR policy prerequisites](../includes/tenant-attach-edr-prerequisites.md)]

## Set up Configuration Manager to support EDR policy

Before you can deploy EDR policies to Configuration Manager devices, complete the configurations detailed in the following sections.

These configurations are made within the Configuration Manager console and to your Configuration Manager deployment. If you're not familiar with Configuration Manager, plan to work with a Configuration Manager admin to complete these tasks.  

The following sections cover the required tasks:

1. [Install the update for Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Enable tenant attach](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
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

#### Enable tenant attach when co-management hasn't been enabled

> [!TIP]
> You use the **Co-management Configuration Wizard** in the Configuration Manager console to enable tenant attach, but you don't need to enable co-management.

If you're planning to enable co-management, be familiar with co-management, its prerequisites, and how to manage workloads before you continue. See [What is co-management?](../../configmgr/comanage/overview.md) in the Configuration Manager documentation.

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.
2. In the ribbon, select **Configure co-management** to open the wizard.
3. On the **Tenant onboarding** page, select **AzurePublicCloud** for your environment. Azure Government cloud isn't supported.
   1. Select **Sign In**. Use your *Global Administrator* account to sign in.

The following are supported for devices you manage with Intune:

- Platform: **Windows 10, Windows 11, and Windows Server** - Intune deploys the policy to devices in your Microsoft Entra groups.
  - Profile: **Endpoint detection and response**

## Create and deploy EDR policies

When you integrate your Microsoft Defender for Endpoint subscription with Intune, you can create and deploy EDR policies. You choose the type of policy to create while configuring a new EDR policy, by choosing a platform for the policy.

Before you can deploy policy to devices managed by Configuration Manager, set up Configuration Manager to support EDR policy from the Microsoft Intune admin center. See [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

> [!TIP]
> In addition to EDR policy, you can use [device configuration](../protect/advanced-threat-protection-configure.md) policy to onboard devices to Microsoft Defender for Endpoint. However, device configuration policies don't support tenant attached devices.
>
> When using multiple polices or policy types like *device configuration* policy and *endpoint detection and response* policy to manage the same device settings (such as onboarding to Defender for Endpoint), you can create policy conflicts for devices. To learn more about conflicts, see [Manage conflicts](../protect/endpoint-security-policy.md#manage-conflicts) in the *Manage security policies* article.

### Create EDR policies

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

3. Select the platform and profile for your policy. The following information identifies your options:

   - Intune - Intune deploys the policy to devices in your assigned groups. When you create the policy, select:

     - Platform: **Linux**, **macOS**, or **Windows 10, Windows 11, and Windows Server**
     - Profile: **Endpoint detection and response**

   - Configuration Manager - Configuration Manager deploys the policy to devices in your Configuration Manager collections. When you create the policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (ConfigMgr)**
     - Profile: **Endpoint detection and response (ConfigMgr)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, Choose **Auto from Connector**  for **Microsoft Defender for Endpoint Client configuration package type**. Configure the **Sample Sharing** and **Telemetry Reporting Frequency** settings you want to manage with this profile. 

   > [!NOTE]
   > To onboard or offboard tenants using the onboarding file from the Microsoft Defender for Endpoint portal, select either *Onboard* or *Offboard* and supply the contents of the onboarding file to the input directly below the selection.

   When you're done configuring settings, select **Next**.

7. If you use Scope tags, on the **Scope tags** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.

   Select **Next** to continue.

8. On the **Assignments** page, select the groups or collections that receive this policy. The choice depends on the platform and profile you selected:

   - For Intune, select groups from Microsoft Entra.
   - For Configuration Manager, select collections from Configuration Manager that you've synced to Microsoft Intune admin center and enabled for Microsoft Defender for Endpoint policy.

   You can choose not to assign groups or collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

## Updating the onboarding state for a device

Organizations may need to update the onboarding information on a device via Microsoft Intune.

This update can be necessary due to a change in the onboarding payload for Microsoft Defender for Endpoint, or when directed by Microsoft support.

Updating the onboarding information directs the device to start utilizing the new onboarding payload at the next *Restart*.

> [!NOTE]
> This information will not necessarily move a device between tenants without fully offboarding the device from the original tenant. For options migrating devices between Microsoft Defender for Endpoint organizations, engage Microsoft Support.

### Process to update the payload

1. Download the new Mobile Device Management **New** onboarding payload from the Microsoft Defender for Endpoint console.

1. Create a **New Group** to validate the new policies effectiveness.

1. Exclude the **New Group** from your existing EDR policy.

1. Create a **New** Endpoint Detection and Response policy, outlined in [Create EDR policies](./endpoint-security-edr-policy.md#create-edr-policies).

1. While creating the policy, select **Onboard** from the client package configuration type, and specify the **contents** of the onboarding file from the Microsoft Defender for Endpoint console.

1. **Assign the policy** to the new group created for validation.

1. **Add** existing devices to the validation group and ensure the changes work as expected.

1. **Expand** the deployment gradually, eventually decommissioning the original policy.

> [!NOTE]
> If previously using the *Auto from connector* option to retrieve the onboarding information, engage Microsoft support to confirm the use of the new onboarding information.
>
> For organizations updating onboarding information at the direction of Microsoft support, Microsoft will direct you when the connector has been updated to leverage the new onboarding payload.

## EDR policy reports

You can view details about the EDR policies you deploy in the Microsoft Intune admin center. To view details, go to **Endpoint security** > **Endpoint deployment and response**, and select a policy for which you want to view compliance details:


- For policies that target the **Linux**, **macOS**, or **Windows 10, Windows 11, and Windows Server** platforms (Intune), Intune displays an overview of compliance to the policy. You can also select the chart to view a list of devices that received the policy, and drill-in to individual devices for more details.

  For Windows devices, the chart for **Devices with Defender for Endpoint sensor** displays only devices that successfully onboard to Microsoft Defender for Endpoint through use of the **Windows 10, Windows 11, and Windows Server** profile. To ensure you have full representation of your devices in this chart, deploy the onboarding profile to all your devices. Devices that onboard to Microsoft Defender for Endpoint by external means, like Group Policy or PowerShell, are counted as **Devices without the Defender for Endpoint sensor**.

- For policies that target the **Windows 10, Windows 11, and Windows Server (ConfigMgr)** platform (Configuration Manager), Intune displays an overview of compliance to the policy that doesn't support drill-in to view additional details. The view is limited because the admin center receives limited status details from Configuration Manager, which manages the deployment of the policy to Configuration Manager devices.

## Next steps

- [Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Learn more about [endpoint detection and response](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) in the Microsoft Defender for Endpoint documentation.
- View details for the settings in the [deprecated](endpoint-security-edr-profile-settings.md) Endpoint detection and response profile for the *Windows 10 and later*
