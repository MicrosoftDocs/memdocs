---
# required metadata

title: Use Microsoft Defender for Endpoint Security Configuration Management in Microsoft Endpoint manager
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/16/2021
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

When you use Microsoft Endpoint Manager (MEM) and Microsoft Defender for Endpoint (MDE) in the same Azure Active Directory (Azure AD) tenant, you can use the Microsoft Endpoint Manager to deploy security configurations of devices in your environment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this capability, devices that aren’t managed by a Mobile Device Management (MDM) solution can receive security configurations directly from Microsoft Endpoint Manager.

When devices are managed through this capability:

- You use the Microsoft Endpoint Manager admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups of devices.
- Devices get the policies based on their Azure Active Directory device registration. A device that isn’t already registered in Azure AD does so when it onboards to MDE.
- When a device receives the policy, the Defender for Endpoint components on the device enforce the policy and report on the devices status. The device status is available in the Microsoft Endpoint Manager admin center.

This scenario supports devices that don't enroll with a product like Intune or Configuration Manager. When a device is managed through Intune or Configuration Manager, The device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune or Configuration Manager to deploy policy for Defender to your MDM-managed devices.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

## Architecture

The following diagram is a conceptual representation of the MDE security configuration management solution. 

:::image type="content" source="./media/mde-security-integration/mde-architecture.png" alt-text="Conceptual representation of the MDE security configuration management solution.":::

1. Devices onboard to MDE.

2. A trust is established between each device and Azure AD. When a device has an existing registration, that is used. When devices haven't registered, a new registration is created.

3. Devices report their Azure AD registration to Microsoft Endpoint Manager. This act enables Microsoft Endpoint Manager to create policies that target devices that have onboarded to MDE.

4. Microsoft Endpoint Management policies for MDE deploy to devices based on the Azure AD registration of devices, and devices report their MDE status back to the admin center.

## Which solution should I use?

Microsoft Endpoint Manager includes several methods and policy types to manage the configuration of  Defender for Endpoint on devices. The following information can help you understand which scenarios support which policy types.

|Device management scenario    | Available policies and profiles     | Information   |  
|------------------------|------------------------|------------------------|
|**MDM**: <br><br>- Intune <br><br>- Configuration Manager | **Device configuration**: <br><br>- *Endpoint protection* (Template) profile<br><br>- *Device restriction* (Template) profile | Device configuration template is a profile that groups related settings. Endpoint protection profiles include a range of settings from disk encryption, BitLocker,  and Defender Antivirus. Device restriction profiles can manage limited aspects of device security, how users share data, and more. <br><br>Unless you need a broad protection policy that manages settings that protect different aspects of an endpoint, consider using endpoint security profiles or security baselines, which both focus directly on the configuration of security. |
|  | **Device configuration policy**: <br><br>- *Settings catalog profile* | A settings catalog profile is a device configuration policy you customize by selecting each setting that you want to manage. Settings are not limited to a single product or feature area. Because you must identify and add each setting you want to manage, they can exclude any settings you don't willfully intend to manage. |
|  | **Security baselines**:<br><br>- *All security baselines* | A series of security configuration profiles that are composed of Microsoft recommended security settings for different products like Defender, Edge, or Windows. The recommendations are from the relevant product teams and enable you to quickly deploy a secure configuration for that product to devices. <br><br>While you can configure and deploy any available security baseline, only devices that run the product the baseline configures, like *Defender for Endpoint* or *Edge*, can apply the configurations from the baseline.  |
|**MDM with MDE**:<br><br>- Intune<br><br>- Configuration Manager<br><br>- Defender for Endpoint | **Endpoint security**:<br><br>- **Attack surface reduction** policy > all profiles<br><br>- **Endpoint detection and response** policy > all profiles <br><br>This device management scenario also supports all the options for the *MDM* scenario. |  Endpoint security includes a series of policy types that help security admins to focus on the task of securing MDM enrolled devices. As security focused policies, they remove the overhead of unrelated settings.<br><br>The policy types listed for this scenario have the extra requirement that devices run Defender for Endpoint.<br><br>Several of the endpoint security policies also support the Security Configuration for Defender through the selection of profiles for *Windows 10, Windows 11, and Windows Server (Preview)*. |
|**MDE only**:<br><br>- Defender for Endpoint<br><br>Devices that are managed through MDM do not support this solution. | **Endpoint security**:<br><br>- **Antivirus policy**  >  **Windows 10, Windows 11, and Windows Server (Preview) profile**<br><br>- **Firewall policy**   >  *Windows 10, Windows 11, and Windows Server (Preview) profile* | For devices that run Defender for Endpoint but  aren't enrolled with Intune or Configuration manager, you can use the **Windows 10, Windows 11, and Windows Server (Preview)** profile for Antivirus or Firewall policy to directly configure Microsoft Defender for Endpoint.<br><br>These profiles include the same range of settings you can configure for MDM-managed devices but are not supported for MDM-managed devices. |

## Prerequisites

Review the following sections for requirements and configurations you'll need to successfully use security configuration management for MDE.

### Environment

Your environment must use Azure AD or Hybrid Azure AD. When a device enrolls with MDE, the device is registered automatically:

- New devices are registered in Azure AD at the time they onboard to MDE.
- Existing registrations are used when the device is already present in Azure AD.
- Devices without a domain relationship (workgroup devices) are registered in Azure AD without user interaction.

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` – For Azure AD registration.
- `login.microsoftonline.com` – For Azure AD registration.
- `*.dm.microsoft.com` -  The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

### Supported platforms

Policies for MDE security management are supported for the following device platforms:

- Windows 10 Professional/Enterprise (With KB999999)
- Windows 11 Professional/Enterprise (With KB999999)
- Windows Server 2012 R2 with Microsoft Defender for Down-Level Devices
- Windows Server 2019 with Microsoft Defender for Down-Level Devices
- Windows Server 2022 (with KB999999)

### Licensing and subscriptions

To use security management for MDE, you need:

- A subscription with licenses for Microsoft Defender for Endpoint. The source of that license doesn’t matter and might be provided through Microsoft 365, an E5, or a license for only Microsoft Defender for Endpoint.

  *Any subscription* that grants MDE licenses also grants your tenant access to the Endpoint security node of the Microsoft Endpoint Manager admin center. The Endpoint security node is where you’ll configure and deploy policies to manage MDE for your devices and monitor device status.

- A subscription that includes Azure AD P1.

## Configure your Tenant to support MDE Security Configuration Management

To support MDE security configuration management through the Microsoft Endpoint Manager admin center, you must enable communication between them from within each console.

1. Sign in to [Microsoft 365 Defender portal](https://security.microsoft.com/) and go to **Settings** > **Endpoints** > **Advanced Features** and enable **MDE-attach for security setting management in MEM**:

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-defender.png" alt-text="Enable MDE settings management in the Defender console.":::

2. Make sure the relevant users have permissions to manage endpoint security settings in Microsoft Endpoint Manager or grant them with the required permission. Go to **Settings** > **Permissions** > **Roles** > **Add item**, and select Manage **Endpoint Security settings in Microsoft Endpoint Manager**:

   :::image type="content" source="./media/mde-security-integration/add-role.png" alt-text="Grant users permissions to manage settings.":::

3. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

4. Select **Endpoint security** > **Microsoft Defender for Endpoint**, and set **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations (Preview)** to **On**.

   :::image type="content" source="./media/mde-security-integration/enable-mde-settings-management-mem.png" alt-text="Enable MDE settings management in the Microsoft Endpoint Manager admin center.":::

   When you set this option to On, all supported devices in your tenant that aren’t managed by Microsoft Endpoint Manager will qualify to onboard to Microsoft Defender for Endpoint.

## Onboard devices

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboarding tools and methods for Windows devices](/microsoft-365/security/defender-endpoint/configure-endpoints?view=o365-worldwide) in the Defender for Endpoint documentation. 

Devices that you manage with Intune or Configuration Manager are not supported for this scenario.

Devices that onboard are automatically registered with your Azure AD and are visible in the Microsoft Endpoint Management admin center. You'll create Azure AD groups for these devices to support deployment of MDE policies.

## Create Azure AD Groups

After devices onboard to Defender for Endpoint, you'll need to create groups so to support deployment of policy for MDE.

To identify devices that have enrolled with MDE but aren't managed by Intune or Configuration Manager:

1. Sign in to [Microsoft 365 Defender portal](https://security.microsoft.com/).

2. Go to **Devices**, and then select the column **Managed by** to sort the view of devices.

   Devices that onboard to MDE and have registered but aren't managed by Intune or Configuration Manager display **MDE** in the *Managed by* column. These are the devices that can receive policy for security management for Microsoft Defender for Endpoint.

You can create groups for these devices [in Azure AD](azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) or [from within the Microsoft Endpoint Manager admin center](../fundamentals/groups-add.md).

## Deploy policy

AFter creating one or more Azure AD groups that contain devices managed by MDE, you can create and deploy the following policies policies for Security Management for Microsoft Defender for Endpoint to those groups:

- Antivirus
- Firewall

> [!TIP]
> Avoid deploying multiple policies that manage the same setting to a device.
>
> MEM supports deploying multiple instances of each endpoint security policy type to the same device, with each policy instance being received by the device separately. Therefore, a device might receive separate configurations for the same setting from different policies, which results in a conflict. MEM doesn't identify the conflict before the policy deploys, and it is Defender for Endpoint on the device that manages conflicts. After resolving conflicts, Defender reports the devices configuration back to MEM where one or more policies might display an error or misconfiguration.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Endpoint security** and then select the type of policy you want to configure, either Antivirus or Firewall, and then select **Create Policy**.  

3. Enter the following properties or the policy type you selected:

   - For Antivirus policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Microsoft Defender Antivirus (Preview)**

   - For Firewall policy, select:
     - Platform: **Windows 10, Windows 11, and Windows Server (Preview)**
     - Profile: **Microsoft Defender Firewall (Preview)**

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, select the settings you want to manage with this profile. To learn more about a setting, expand its information dialog and select the *Learn more* link to view the CSP information for the setting in the on-line documentation.

   When your done configuring settings, select **Next**.

7. On the **Assignments** page, select the Azure AD groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next** to continue.

   > [!TIP]
   > Assignment filters are not supported for Security Configuration Management profiles.

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. Validate settings are applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples?view=windowsserver2019-psreserve-view=true) command utility.

## Monitor status

Status and reports for MDE policies are available form the policy node under Endpoint security in the Microsoft Endpoint Manager admin center admin center.

Drill in to the policy type, Antivirus or Firewall, and then select the policy to view its status. Policies for MDE have a *Policy type* of either *Microsoft Defender Antivirus (Preview)* or *Microsoft Defender Firewall (Preview)*.

When you select a policy, you'll see information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see that devices per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)