---
# required metadata

title: Using Azure Virtual Desktop multi-session with Microsoft Intune
titleSuffix: 
description: Guidelines for using Azure Virtual Desktop multi-session with Microsoft Intune
keywords:
author: smbhardwaj  
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/26/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started; references_regions
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Windows 10 or Windows 11 Enterprise multi-session remote desktops

Azure Virtual Desktop multi-session with Microsoft Intune is now generally available.

You can now use Microsoft Intune to manage Windows 10 or Windows 11 Enterprise multi-session remote desktops in the Microsoft Endpoint Manager admin center just as you can manage a shared Windows 10 or Windows 11 client device. When managing such virtual machines (VMs), you must use device-based configurations. Such configurations require user-less enrollments. 

Windows 10 or Windows 11 Enterprise multi-session is a new Remote Desktop Session Host exclusive to [Azure Virtual Desktop](/azure/virtual-desktop/) on Azure. It provides the following benefits:

- Allows multiple concurrent user sessions.
- Gives users a familiar Windows 10 or Windows 11 experience.
- Supports use of existing per-user Microsoft 365 licensing.

You can manage **Windows 10** and **Windows 11 Enterprise multi-session** VMs created in Azure Government Cloud in US Government Community (GCC), GCC High, and DoD. 

## Overview

Microsoft Intune only supports managing Windows 10 or Windows 11 Enterprise multi-session with device configurations. This means only [policies defined in the OS scope](/windows/client-management/mdm/policy-configuration-service-provider) and apps configured to install in the system context can be applied to Azure Virtual Desktop multi-session VMs. Additionally, all multi-session configurations must be targeted to devices or device groups. User scope policies are not supported at this time.


## Prerequisites

This feature supports Windows 10 or Windows 11 Enterprise multi-session VMs which are:

- Running Windows 10 multi-session, version 1903 or later, or running Windows 11 multi-session.
- Set up as remote desktops in pooled host pools that have been deployed through Azure Resource Manager.
- Running a Azure Virtual Desktop agent version of 1.0.2944.1400 or later.
- [Hybrid Azure AD-joined](/azure/active-directory/devices/hybrid-azuread-join-plan) and enrolled in Microsoft Intune using one of the following methods:
  - Configured with [Active Directory group policy](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy), set to use Device credentials, and set to automatically enroll devices that are Hybrid Azure AD-joined.
  - [Configuration Manager co-management](/configmgr/comanage/overview).
- Azure AD-joined and enrolled in Microsoft Intune by enabling [Enroll the VM with Intune](/azure/virtual-desktop/deploy-azure-ad-joined-vm#deploy-azure-ad-joined-vms) in the Azure portal.

> [!Note]
> If you're joining session hosts to an Azure AD DS domain, you can't manage them using Intune.

> [!IMPORTANT]
> If you’re using Windows 10, versions 2004, 20H2, or 21H1 builds, make sure that you install the July 2021 Windows Update or a later Windows update. Otherwise, remote actions in the Microsoft Endpoint Manager admin center, like remote sync, won’t work correctly. As a result, pending policies assigned to devices might take up to 8 hours to be applied.

See [What is Azure Virtual Desktop?](/azure/virtual-desktop/overview#requirements) for more information about Azure Virtual Desktop licensing requirements.

Windows 10 or Windows 11 Enterprise multi-session VMs are treated as a separate OS edition and some Windows 10 or Windows 11 Enterprise configurations won’t be supported for this edition. Using Microsoft Intune does not depend on or interfere with Azure Virtual Desktop management of the same VM.

## Create the device configuration profile

To configure configuration policies for Windows 10 or Windows 11 Enterprise multi-session VMs, you'll need to use the [Settings catalog](../configuration/settings-catalog.md) in the Microsoft Endpoint Manager admin center.

The existing device configuration profile templates aren't supported for Windows 10 or Windows 11 Enterprise multi-session VMs, with the exception of the following templates:

- [Trusted certificate](../protect/certificates-trusted-root.md#create-trusted-certificate-profiles) - Device (machine) only
- [SCEP certificate](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) - Device (machine) only
- [PKCS certificate](../protect/certificates-pfx-configure.md#create-a-pkcs-certificate-profile) - Device (machine) only
- [VPN](../configuration/vpn-settings-configure.md#create-the-profile) - Device Tunnel only

Microsoft Intune won't deliver unsupported templates to multi-session devices, and those policies appear as *Not applicable* in reports.

### To configure policies

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Windows** > **Configuration profiles** > **Create Profile**.
2. For **Platform**, select **Windows 10 and later**.
3. For **Profile type**, select **Settings catalog (Preview)**, or when deploy settings by using a Template, select **Templates** and then the name of the supported Template.
4. Select **Create**.
5. On the **Basics** page, provide a **Name** and (optionally) **Description** > **Next**.
6. On the **Configuration settings** page, select **Add settings**.
7. Under **Settings picker**, select **Add filter** and select the following options:
    - **Key**: **OS edition**
    - **Operator**: **==**
    - **Value**: **Enterprise multi-session**
    - Select **Apply**. The filtered list now shows all configuration profile categories that support Windows 10 or Windows 11 Enterprise multi-session. You can see the scope for the policy in parentheses (Device or User). Currently, only device settings are supported for multi-session.
8. From the filtered list, pick the categories that you want.
    - For each category you pick, select the settings that you want to apply to your new configuration profile.
    - For each setting, select the value that you want for this configuration profile.
9. Select **Next** when you’re done adding settings.
10. On the **Assignments** page, choose the user groups containing the devices to which you want this profile assigned > **Next**.
11. On the **Scope tags** page, optionally add the scope tags you want to apply to this profile > **Next**. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
12. On the **Review + create** page, choose **Create** to create the profile.

### Administrative templates

Windows 10 or Windows 11 Administrative Templates are supported for Windows 10 or Windows 11 Enterprise multi-session via the Settings catalog with some limitations:

- ADMX-backed policies are supported. Some policies are not yet available in the Settings catalog.
- ADMX-ingested policies are supported, including Office and Microsoft Edge settings available in Office administrative template files and Microsoft Edge administrative template files. For a complete list of ADMX-ingested policy categories, see [Win32 and Desktop Bridge app policy configuration](/windows/client-management/mdm/win32-and-centennial-app-policy-configuration#overview). Some ADMX ingested settings will not be applicable to Windows 10 or Windows 11 Enterprise multi-session.

## Compliance and Conditional access

You can secure your Windows 10 or Windows 11 Enterprise multi-session VMs by configuring compliance policies and Conditional Access policies in the Microsoft Endpoint Manager admin center. The following compliance policies are supported on Windows 10 or Windows 11 Enterprise multi-session VMs:

- Minimum OS version  
- Maximum OS version  
- Valid operating system builds  
- Simple passwords  
- Password type  
- Minimum password length  
- Password Complexity  
- Password expiration (days)  
- Number of previous passwords to prevent reuse  
- Microsoft Defender Antimalware  
- Microsoft Defender Antimalware security intelligence up-to-date  
- Firewall  
- Antivirus
- Antispyware
- Real-time protection  
- Microsoft Defender Antimalware minimum version
- Defender ATP Risk score

All other policies report as **Not applicable**.

> [!Important]
> You’ll need to create a new compliance policy and target it to the device group containing your multi-session VMs. User-targeted compliance configurations aren’t supported.

[Conditional Access policies](../protect/conditional-access.md) support both user and device based configurations for Windows 10 or Windows 11 Enterprise multi-session.

> [!NOTE]
> [Conditional Access for Exchange on-premises](../protect/conditional-access-exchange-create.md) isn't supported for Windows 10 or Windows 11 Enterprise multi-session VMs.

## Endpoint security

You can configure profiles under Endpoint security for multi-session VMs by selecting Platform Windows 10, Windows 11, and Windows Server. 

For more information, see [Manage device security with endpoint security policies in Microsoft Intune](../protect/endpoint-security-policy.md)

## Application deployment

All Windows 10 or Windows 11 apps can be deployed to Windows 10 or Windows 11 Enterprise multi-session with the following restrictions:

- All apps must be configured to install in the system/device context and be targeted to devices. Web apps are always applied in the user context by default so they will not apply to multi-session VMs.
- All apps must be configured with **Required** or **Uninstall** app assignment intent. The **Available apps** deployment intent is not supported on multi-session VMs.  
- If a Win32 app configured to install in the system context has dependencies or supersedence relationship on any apps configured to install in the user context, the app will not be installed. To apply to a Windows 10 or Windows 11 Enterprise multi-session VM, create a separate instance of the system context app or make sure all app dependencies are configured to install in the system context.
- Azure Virtual Desktop RemoteApp and MSIX app attach are not currently supported in Microsoft Intune.

## Script deployment

Scripts configured to run in the system context are supported on Windows 10 or Windows 11 Enterprise multi-session. This can be configured under Script settings by setting **Run this script using the logged on credentials** to **No**.

## Windows Update for Business

You can use the [settings catalog](../configuration/settings-catalog.md) to manage Windows Update settings for quality (security) updates for Windows 10 or Windows 11 Enterprise multi-session VMs. To find the supported settings in the catalog, configure a settings filter for *Enterprise multi-session* and then expand the *Windows Update for Business* category.

The following settings are available in the catalog, with the links opening the Windows CSP documentation:

- [Active Hours End](/windows/client-management/mdm/policy-csp-Update#update-activehoursend)
- [Active Hours Max Range](/windows/client-management/mdm/policy-csp-Update?#update-activehoursmaxrange)
- [Active Hours Start](/windows/client-management/mdm/policy-csp-Update#update-activehoursstart)
- [Block "Pause Updates" ability](/windows/client-management/mdm/policy-csp-Update#update-setdisablepauseuxaccess)
- [Configure Deadline Grace Period](/windows/client-management/mdm/policy-csp-Update#update-configuredeadlinegraceperiod)
- [Defer Quality Updates Period (Days)](/windows/client-management/mdm/policy-csp-Update#update-deferqualityupdatesperiodindays)
- [Pause Quality Updates Start Time](/windows/client-management/mdm/policy-csp-Update#update-pausequalityupdatesstarttime)
- [Quality Update Deadline Period (Days)](/windows/client-management/mdm/policy-csp-Update?#update-configuredeadlineforqualityupdates)

## Remote actions

The following Windows 10 or Windows 11 desktop device remote actions are not supported and will be grayed out in the UI and disabled in Graph for Windows 10 or Windows 11 Enterprise multi-session VMs:

- Autopilot reset
- BitLocker key rotation
- Fresh Start
- Remote lock
- Reset password
- Wipe

## Retirement

Deleting VMs from Azure will leave orphaned device records in the Microsoft Endpoint Manager admin center. They will be automatically cleaned up according to the cleanup rules configured for the tenant.

## Security baselines

Security baselines are not available for Windows 10 or Windows 11 Enterprise multi-session at this time. We recommend that you review the [Available security baselines](../protect/security-baselines.md) and configure the recommended policies and values in the [Settings catalog](../configuration/settings-catalog.md).

## Additional configurations which are not supported on Windows 10 or Windows 11 Enterprise multi-session VMs

Out of Box Experience (OOBE) enrollment isn't supported for Window 10 or Windows 11 Enterprise multi-session. This restriction means that:

- Windows Autopilot and Commercial OOBE aren't supported.
- Enrollment status page isn’t supported.

Windows 10 or Windows 11 Enterprise multi-session managed by Microsoft Intune is not currently supported for China.

## Troubleshooting

The following sections provide troubleshooting guidance for common issues.

### Enrollment issues

|Issue|Detail|
|---------------|---------------------------------|
|Enrollment of hybrid Azure AD joined virtual machine fails|<ul><li>Auto-enrollment is configured to use user credentials. Windows 10 or Windows 11 Enterprise multi-session virtual machines must be enrolled using device credentials.<li>The Azure Virtual Desktop agent you’re using must be version 2944.1400 or later.<li>You have more than one MDM provider, which is not supported.<li>Windows 10 or Windows 11 Enterprise multi-session VM is configured outside of a host pool. Microsoft Intune only supports VMs provisioned as part of a host pool.<li>The Azure Virtual Desktop host pool was not created through the Azure Resource Manager template.|
|Enrollment of Azure AD joined virtual machine fails|<ul><li>The Azure Virtual Desktop agent you’re using is not updated. The agent must be version 2944.1400 or above.<li>Azure Virtual Desktop host pool was not created through the Azure Resource Manager template.|

### Configuration issues

|Issue|Detail|
|--------|------------------------------|
|Settings catalog policy fails|Confirm the VM is enrolled using device credentials. Enrollment with user credentials is not currently supported for Windows 10 or Windows 11 Enterprise multi-session.|
|Configuration policy did not apply|Templates (with the exception of Certificates) are not supported on Windows 10 or Windows 11 Enterprise multi-session. All policies must be created via the settings catalog.|
Configuration policy reports as Not applicable|Some policies are not applicable to Azure Virtual Desktop VMs.|
|Microsoft Edge/Microsoft Office ADMX policy does not show up when I apply the filter for Windows 10 or Windows 11 Enterprise multi-session edition|Applicability for these settings is not based on the Windows version or edition but on whether those apps have been installed on the device. To add these settings to your policy, you may have to remove any filters applied in the settings picker.|
|App configured to install in system context did not apply|Confirm the app does not have a dependency or supersedence relationship on any apps configured to install in user context. User context apps are not currently supported on Windows 10 or Windows 11 Enterprise multi-session.|
|Update rings for Windows 10 and later policy did not apply|Windows Update for Business policies are not currently supported.|

## Next steps

[Learn more about Azure Virtual Desktops](/azure/virtual-desktop/).
