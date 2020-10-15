---
# required metadata

title: Manage endpoint detection and response settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security endpoint detection and response policy in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/07/2020
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
ms.reviewer: mattsha


---

# Endpoint detection and response policy for endpoint security in Intune

When you integrate Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) with Intune, you can use endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender ATP.

The capabilities of Microsoft Defender ATP endpoint detection and response provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

EDR policies include platform-specific profiles to manage settings for EDR. The profiles automatically include an *onboarding package* for Microsoft Defender ATP. Onboarding packages are how devices are configured to work with Microsoft Defender ATP. After a device onboards, you can start to use threat data from that device.

EDR policies deploy to groups of devices in Azure Active Directory (Azure AD) that you manage with Intune, and to collections of on-premises devices that you manage with Configuration Manager, including Windows servers. The EDR policies for the different management paths require different onboarding packages. Therefore, you’ll create separate EDR policies for the different types of devices you manage.

Find the endpoint security policies for EDR under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

View [settings for Endpoint detection and response profiles](endpoint-security-edr-profile-settings.md).

## Prerequisites for EDR policies

**General**:

- **Tenant for Microsoft Defender Advanced Threat Protection** – Your Microsoft Defender ATP tenant must be integrated with your Microsoft Endpoint Manager tenant (Intune subscription) before you can create EDR policies. See [Use Microsoft Defender ATP](advanced-threat-protection.md) in the Intune documentation.

**Support for Configuration Manager clients**:

- **Set up tenant attach for Configuration Manager devices** - To support deploying EDR policy to devices managed by Configuration Manager, configure *tenant attach*. This includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, including the synchronization of Configuration Manager collections to the Microsoft Endpoint Manager admin center and enabling them to work with endpoint security policies, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

## EDR profiles

[View the settings](endpoint-security-edr-profile-settings.md) you can configure for the following platforms and profiles.

**Intune** – The following are supported for devices you manage with Intune:

- Platform: **Windows 10 and later** - Intune deploys the policy to devices in your Azure AD groups.
- Profile: **Endpoint detection and response (MDM)**

**Configuration Manager** - The following are supported for devices you manage with Configuration Manager:

- Platform: **Windows 10 and Windows Server (ConfigMgr)** - Configuration Manager deploys the policy to devices in your Configuration Manager collections.
- Profile: **Endpoint detection and response (ConfigMgr)**

## Set up Configuration Manager to support EDR policy

Before you can deploy EDR policies to Configuration Manager devices, complete the configurations detailed in the following sections.

These configurations are made within the Configuration Manager console and to your Configuration Manager deployment. If you’re not familiar with Configuration Manager, plan to work with a Configuration Manager admin to complete these tasks.  

The following sections cover the required tasks:

1. [Install the update for Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Enable tenant attach](#task-2-configure-tenant-attach-and-synchronize-collections)  

> [!TIP]
> To learn more about using Microsoft Defender ATP with Configuration Manager, see the following articles in the Configuration Manager content:
>
> - [Onboard Configuration Manager clients to Microsoft Defender ATP via the Microsoft Endpoint Manager admin center](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
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

- Platform: **Windows 10 and later** - Intune deploys the policy to devices in your Azure AD groups.
  - Profile: **Endpoint detection and response (MDM)**

### Devices managed by Configuration Manager *(In preview)*

The following are supported for devices you manage with Configuration Manager through the *tenant attach* scenario:

- Platform: **Windows 10 and Windows Server (ConfigMgr)** - Configuration Manager deploys the policy to devices in your Configuration Manager collections.
  - Profile: **Endpoint detection and response (ConfigMgr) (Preview)** - Manage [Endpoint detection and response policy settings for Configuration Manager devices](../protect/endpoint-security-edr-profile-settings.md#endpoint-detection-and-response-configmgr), when you use tenant attach.

    This profile is supported with devices that are tenant attached and run the following platforms:
    - Windows 10 and later (x86, x64, ARM64).
    - Windows 8.1 (x84, x64)
    - Windows 7 SP1 (x84, x64)
    - Windows Server 2019 and later (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)


## Create and deploy EDR policies

When you integrate your Microsoft Defender ATP subscription with Intune, you can create and deploy EDR policies. There are two distinct types of EDR policy you can create. One policy type for devices you manage with Intune through MDM. The second type is for devices you manage with Configuration Manager.

You choose the type of policy to create while configuring a new EDR policy, by choosing a platform for the policy.

Before you can deploy policy to devices managed by Configuration Manager, set up Configuration Manager to support EDR policy from the Microsoft Endpoint Manager admin center. See [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).


### Create EDR policies

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Endpoint detection and response** > **Create Policy**.

3. Select the platform and profile for your policy. The following information identifies your options:

   - Intune - Intune deploys the policy to devices in your Azure AD groups. When you create the policy, select:
     - Platform: **Windows 10 and later**
     - Profile: **Endpoint detection and response (MDM)**

   - Configuration Manager - Configuration Manager deploys the policy to devices in your Configuration Manager collections. When you create the policy, select:
     - Platform: **Windows 10 and Windows Server (ConfigMgr)**
     - Profile: **Endpoint detection and response (ConfigMgr)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, configure the settings you want to manage with this profile. The onboarding package is automatically included and isn’t something you can configure.

   When your done configuring settings, select **Next**.

7. *This step only applies for the **Endpoint detection and response (MDM)** profile*:  

   On the **Scope tags** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

8. On the **Assignments** page, select the groups or collections that will receive this policy. The choice depends on the platform and profile you selected:

   - For Intune, you’ll select groups from Azure AD.
   - For Configuration Manager, you'll select collections from Configuration Manager that you’ve synced to Microsoft Endpoint Manager admin center and enabled for Microsoft Defender ATP policy.

   You can choose not to assign groups or collections at this time, and later edit the policy to add an assignment.

   When ready to continue, select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**.

   The new profile is displayed in the list when you select the policy type for the profile you created.

## EDR policy reports

You can view details about the EDR policies you deploy in the Microsoft Endpoint Manager admin center. To view details, go to **Endpoint security** > **Endpoint deployment and response**, and select a policy for which you want to view compliance details:

- For policies that target the **Windows 10 and later** platform (Intune), you’ll see an overview of compliance to the policy. You can also select the chart to view a list of devices that received the policy, and drill-in to individual devices for more details.

  The chart for **Devices with ATP sensor** displays only devices that successfully onboard to Microsoft Defender ATP through use of the **Windows 10 and later** profile. To ensure you have full representation of your devices in this chart, deploy the onboarding profile to all your devices. Devices that onboard to Microsoft Defender ATP by external means, like Group Policy or PowerShell, are counted as **Devices without the ATP sensor**.

- For policies that target the **Windows 10 and Windows Server (ConfigMgr)** platform (Configuration Manager), you’ll see an overview of compliance to the policy but can't drill-in to view additional details. The view is limited because the admin center receives limited status details from Configuration Manager, which manages the deployment of the policy to Configuration Manager devices.

[View the settings](endpoint-security-edr-profile-settings.md) you can configure for both platforms and profiles.

## Next steps

- [Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Learn more about [endpoint detection and response](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) in the Microsoft Defender ATP documentation.