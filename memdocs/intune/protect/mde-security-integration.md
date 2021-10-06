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

When you use Microsoft Endpoint Manager (MEM) and Microsoft Defender for Endpoint (MDE) in the same Azure Active Directory (Azure AD) tenant, you can use the Microsoft Endpoint Manager to deploy security configurations of devices in your environment. This capability is known as Security Management for Microsoft Defender for Endpoint. With this capability, devices that aren’t managed by a Mobile Device Management (MDM) solution can receive security configurations directly from Microsoft Endpoint Manager.

When devices are managed through this capability:

- You use the Microsoft Endpoint Manager admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups of devices.
- Devices get the policies based on their Azure Active Directory device registration. A device that isn’t already registered in Azure AD does so when it onboards to MDE.
- When a device receives the policy, the Defender for Endpoint components on the device enforce the policy and report on the devices status. The device status is available in the Microsoft Endpoint Manager admin center.

This scenario supports devices that don't enroll with a product like Intune or Configuration Manager. If a device is managed through Intune or Configuration Manager, you use those channels to manage MDE on the device instead.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

<!-- Pending confirmation of applicability:

> [!TIP]
> You can use Security management for MDE to manage MDE on devices that are enrolled with a third-party non-Microsoft MDM.

-->
## Architecture

The following is a conceptual representation of the MDE security configuration management solution. 

:::image type="content" source="./media/mde-security-integration/mde-architecture.png" alt-text="Conceptual representation of the MDE security configuration management solution.":::

1. Devices onboard to MDE.

2. A trust is established between each device and Azure AD. When a device has an existing registration, that is used. When devices haven't registered, a new registration is created.

3. Devices enroll with Microsoft Endpoint Manager. This enrollment enables devices to be managed through the Microsoft Endpoint Manager admin center and is distinct from the act of enrolling a device with a MDM authority like Intune or Configuration Manager.

4. Microsoft Endpoint Management policies for MDE are deployed to devices based on the Azure AD registration of devices, and devices report their MDE status back to the admin center.

## Which solution should I use?

Use the information in the following table to understand which solution to use to manage Defender for Endpoint on your devices:

***Table pending***

## Prerequisites

Review the following sections for requirements and configurations you'll need to successfully use security configuration management for MDE.

### Environment
<!-- Use MDE include if available -->

Your environment must use Azure AD or Hybrid Azure AD. When a device enrolls with MDE, the device is registered automatically:

- New devices are registered in Azure AD at the time they onboard to MDE.
- Existing registrations are used when the device is already present in Azure AD.
- Devices without a domain relationship (workgroup devices) are registered in Azure AD without user interaction.

Devices must have access to the following endpoints:

- `enterpriseregistration.windows.net` – For Azure AD registration.
- `login.microsoftonline.com` – For Azure AD registration.
- `*.dm.microsoft.com` -  The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

### Supported platforms
<!-- Use MDE include if available -->

Policies for MDE security management are supported for the following device platforms:

- Windows 10 Professional/Enterprise (With KB999999)
- Windows 11 Professional/Enterprise (With KB999999)
- Windows Server 2012 R2 with Microsoft Defender for Down-Level Devices
- Windows Server 2019 with Microsoft Defender for Down-Level Devices
- Windows Server 2022 (with KB999999)

### Licensing and subscriptions

To use security management for MDE, you need only a subscription for Microsoft Defender for Endpoint. The source of that license doesn’t matter and might be provided through Microsoft 365, an E5, or a license for only Microsoft Defender for Endpoint.

*Any subscription* that grants MDE licenses also grants your tenant access to the Endpoint security node of the Microsoft Endpoint Manager admin center. The Endpoint security node is where you’ll configure and deploy policies to manage MDE for your devices and monitor device status.

## Configure your tenant
<!-- Use MDE include if available -->
***content pending*** 
<!--  Rough notes:

1.	Configure your Tenant.
IDENTITY
a.	Azure AD Connect:  Ensure Sync Scope is setup properly for AAD Connect.
b.	If you use ADFS:  Federation Claims must be configured properly for ADFS scenarios. (Does hybrid join work correctly? Your probably good to go). 
c.	If Enterprise DRS (Device registration service), take caution. This requires some extra configuration and care. (Should be rare… Escalate that to devs for support…)

FLIP TOGGLES: 
- In MDE: 
  - Enable MDE-attach for security settings management in MEM (This will change, MDE-attach isn’t usable).
- In Microsoft Endpoint Manager: 
  - Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations

*** Any supported device not managed by Microsoft Endpoint Manager, will be queued up to onboard!
-->

## Onboard devices
<!-- use MDE include if availalbe -->

Microsoft Defender for Endpoint supports several options to onboard devices. For current guidance, see [Onboarding tools and methods for Windows devices](microsoft-365/security/defender-endpoint/configure-endpoints?view=o365-worldwide) in the Defender for Endpoint documentation. 

Devices that you manage with Intune or Configuration Manager are not supported for this scenario. 

After devices onboard and they're visible in the Microsoft Endpoint Management admin center, create Azure AD groups for these devices to support deployment of MDE policies.

## Deploy policy

To deploy policy, you'll need an Azure AD group that contains the devices you wan't to deploy policy to. If you haven't created a group with the applicable devices, see `link pending []()`.

Security configuration management supports Antivirus and Firewall policies. 


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

6. On the **Configuration settings** page, expand each group of settings, and configure the settings you want to manage with this profile. To learn more about a setting, expand its information dialog and select the *Learn more* link to view the settings CSP information in the on-line documentation.

   When your done configuring settings, select **Next**.

7. On the **Assignments** page, select the Azure AD groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next** to continue.

   > [!TIP]
   > Assignment filters are not supported for Security Configuration Management profiles.

8. Complete the policy creation process and then on the **Review + create** page, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

9. Wait for the policy to be assigned and view a success indication that policy was applied.

10. Validate settings are applied locally on the client by using the [Get-MpPreference](/powershell/module/defender/get-mppreference#examples?view=windowsserver2019-psreserve-view=true) command utility.

## Monitor status

To monitor security configuration for devices, *pending details*. 

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)