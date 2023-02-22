---
# required metadata

title: Manage endpoint detection and response settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security endpoint detection and response policy in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/06/2022
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

- Windows 10/11
- Windows Server 2012 R2 and later

The capabilities of Microsoft Defender for Endpoint endpoint detection and response provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

EDR policies include platform-specific profiles to manage settings for EDR. The profiles automatically include an *onboarding package* for Microsoft Defender for Endpoint. Onboarding packages are how devices are configured to work with Microsoft Defender for Endpoint. After a device onboards, you can start to use threat data from that device.

EDR policies deploy to groups of devices in Azure Active Directory (Azure AD) that you manage with Intune, and to collections of on-premises devices that you manage with Configuration Manager, including Windows servers. The EDR policies for the different management paths require different onboarding packages. Therefore, you’ll create separate EDR policies for the different types of devices you manage.

Find the endpoint security policies for EDR under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).


## Prerequisites for EDR policies

**General**:

- **Tenant for Microsoft Defender for Endpoint** – Your Microsoft Defender for Endpoint tenant must be integrated with your Microsoft Endpoint Manager tenant (Intune subscription) before you can create EDR policies. See [Use Microsoft Defender for Endpoint](advanced-threat-protection.md) in the Intune documentation.

**Support for Configuration Manager clients**:

- **Set up tenant attach for Configuration Manager devices** - To support deploying EDR policy to devices managed by Configuration Manager, configure *tenant attach*. This includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, including the synchronization of Configuration Manager collections to the Microsoft Endpoint Manager admin center and enabling them to work with endpoint security policies, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

## EDR profiles

### Devices managed by Microsoft Endpoint Manager

**Intune** – The following are supported for devices you manage with Intune:

- Platform: **Windows 10, Windows 11, and Windows Server**
  - Profile: **Endpoint detection and response** - Intune deploys the policy to devices in your Azure AD groups. Profiles for this platform can be used with devices enrolled with Intune, and with devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md).
  
  > [!NOTE]  
  > Beginning on April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows 10, Windows 11, and Windows Server* platform.
  >
  > The *Windows 10, Windows 11, and Windows Server* platform supports devices communicating with Endpoint Manager through Microsoft Intune or Microsoft Defender for Endpoint. These profiles also add support for the Windows Server platform which is not supported through Microsoft Intune natively.
  >
  > Profiles for this new platform use the settings format as found in the Settings Catalog. Each new profile template for this new platform includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.

**Options for** ***Microsoft Defender for Endpoint client configuration package type***:  

After you configure the [service-to-service connection](../protect/advanced-threat-protection-configure.md#enable-microsoft-defender-for-endpoint-in-intune) between Intune and Microsoft Defender for Endpoint, the **Auto from connector** option becomes available for the setting **Microsoft Defender for Endpoint client configuration package type**. This option is not available until you've configured the connection.

When you select **Auto from connector**, Intune automatically gets the onboarding package (blob) from your Defender for Endpoint deployment. This replaces the need to manually configure an **Onboard** package for this profile. There is no option to automatically configure an offboard package.

### Devices managed by Configuration Manager

[!INCLUDE [EDR policy prerequisites](../includes/tenant-attach-edr-prerequisites.md)]

## Set up Configuration Manager to support EDR policy

Before you can deploy EDR policies to Configuration Manager devices, complete the configurations detailed in the following sections.

These configurations are made within the Configuration Manager console and to your Configuration Manager deployment. If you’re not familiar with Configuration Manager, plan to work with a Configuration Manager admin to complete these tasks.  

The following sections cover the required tasks:

1. [Install the update for Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Enable tenant attach](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> To learn more about using Microsoft Defender for Endpoint with Configuration Manager, see the following articles in the Configuration Manager content:
>
> - [Onboard Configuration Manager clients to Microsoft Defender for Endpoint via the Microsoft Endpoint Manager admin center](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Microsoft Endpoint Manager tenant attach: Device sync and device actions](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### Task 1: Install the update for Configuration Manager

Configuration Manager version 2002 requires an update to support use with Endpoint detection and response policies you deploy from the Microsoft Endpoint Manager admin center.

**Update details**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

You’ll find this update as an *in-console update* for Configuration Manager 2002.

To install this update, follow the guidance from [Install in-console updates](../../configmgr/core/servers/manage/install-in-console-updates.md) in the Configuration Manager documentation.

After installing the update, return here to continue configuring your environment to support EDR policy from the Microsoft Endpoint Manager admin center.

### Task 2: Configure tenant attach and synchronize collections

With Tenant attach you specify collections of devices from your Configuration Manager deployment to synchronize with the Microsoft Endpoint Manager admin center. After collections synchronize, use the admin center to view information about those devices and to deploy EDR policy from Intune to them.  

For more information about the Tenant attach scenario, see [Enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md) in the Configuration Manager content.

#### Enable tenant attach when co-management hasn’t been enabled

> [!TIP]
> You use the **Co-management Configuration Wizard** in the Configuration Manager console to enable tenant attach, but you don’t need to enable co-management.

If you're planning to enable co-management, be familiar with co-management, its prerequisites, and how to manage workloads before you continue. See [What is co-management?](../../configmgr/comanage/overview.md) in the Configuration Manager documentation.

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.
2. In the ribbon, click **Configure co-management** to open the wizard.
3. On the **Tenant onboarding** page, select **AzurePublicCloud** for your environment. Azure Government cloud isn't supported.
   1. Click **Sign In**. Use your *Global Administrator* account to sign in.

The following are supported for devices you manage with Intune:

- Platform: **Windows 10, Windows 11, and Windows Server** - Intune deploys the policy to devices in your Azure AD groups.
  - Profile: **Endpoint detection and response**

## Create and deploy EDR policies

When you integrate your Microsoft Defender for Endpoint subscription with Intune, you can create and deploy EDR policies. There are two distinct types of EDR policy you can create. One policy type for devices you manage with Intune through MDM. The second type is for devices you manage with Configuration Manager.

You choose the type of policy to create while configuring a new EDR policy, by choosing a platform for the policy.

Before you can deploy policy to devices managed by Configuration Manager, set up Configuration Manager to support EDR policy from the Microsoft Endpoint Manager admin center. See [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

> [!TIP]
> In addition to EDR policy, you can use [device configuration](../protect/advanced-threat-protection-configure.md) policy to onboard devices to Microsoft Defender for Endpoint. However, device configuration policies don't support tenant attached devices.
>
> When using multiple polices or policy types like *device configuration* policy and *endpoint detection and response* policy to manage the same device settings (such as onboarding to Defender for Endpoint), you can create policy conflicts for devices. To learn more about conflicts, see [Manage conflicts](../protect/endpoint-security-policy.md#manage-conflicts) in the *Manage security policies* article.

### Create EDR policies

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

3. Select the platform and profile for your policy. The following information identifies your options:

   - Intune - Intune deploys the policy to devices in your Azure AD groups. When you create the policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server**
     - Profile: **Endpoint detection and response**

   - Configuration Manager - Configuration Manager deploys the policy to devices in your Configuration Manager collections. When you create the policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (ConfigMgr)**
     - Profile: **Endpoint detection and response (ConfigMgr)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, Choose **Auto from Connector**  for **Microsoft Defender for Endpoint Clinet configuration package type**. Configure the **Sample Sharing** and **Telemetry Reporting Frequency** settings you want to manage with this profile. 

   When your done configuring settings, select **Next**.

7. *This step only applies for the **Endpoint detection and response** profile and the Windows 10, Windows 11, and Windows Server platform*:  

   On the **Scope tags** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

8. On the **Assignments** page, select the groups or collections that will receive this policy. The choice depends on the platform and profile you selected:

   - For Intune, you’ll select groups from Azure AD.
   - For Configuration Manager, you'll select collections from Configuration Manager that you’ve synced to Microsoft Endpoint Manager admin center and enabled for Microsoft Defender for Endpoint policy.

   You can choose not to assign groups or collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

## EDR policy reports

You can view details about the EDR policies you deploy in the Microsoft Endpoint Manager admin center. To view details, go to **Endpoint security** > **Endpoint deployment and response**, and select a policy for which you want to view compliance details:

- For policies that target the **Windows 10, Windows 11, and Windows Server** platform (Intune), you’ll see an overview of compliance to the policy. You can also select the chart to view a list of devices that received the policy, and drill-in to individual devices for more details.

  The chart for **Devices with Defender for Endpoint sensor** displays only devices that successfully onboard to Microsoft Defender for Endpoint through use of the **Windows 10, Windows 11, and Windows Server** profile. To ensure you have full representation of your devices in this chart, deploy the onboarding profile to all your devices. Devices that onboard to Microsoft Defender for Endpoint by external means, like Group Policy or PowerShell, are counted as **Devices without the Defender for Endpoint sensor**.

- For policies that target the **Windows 10, Windows 11, and Windows Server (ConfigMgr)** platform (Configuration Manager), you’ll see an overview of compliance to the policy but can't drill-in to view additional details. The view is limited because the admin center receives limited status details from Configuration Manager, which manages the deployment of the policy to Configuration Manager devices.



## Next steps

- [Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Learn more about [endpoint detection and response](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) in the Microsoft Defender for Endpoint documentation.

View details for the settings in the deprecated Endpoint detection and response profile for the *Windows 10 and later* platform:

- [Endpoint detection and response profile settings](endpoint-security-edr-profile-settings.md) you can configure for both platforms and profiles.
