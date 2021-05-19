---
# required metadata

title: Using Windows Virtual Desktop multi-session with Microsoft Intune
titleSuffix: 
description: Guidelines for using Windows Virtual Desktop multi-session with Microsoft Intune
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 5/24/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
---

# Windows 10 Enterprise multi-session remote desktops

You can now use Microsoft Intune to manage Windows 10 Enterprise multi-session remote desktops just as you can manage a shared Windows 10 client device. When managing such VMs, you must use device-based configurations. Such configurations require user-less enrollments.

> [!IMPORTANT]
> The feature is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended for use in production. Certain features might not be supported, or might have restricted behavior. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms).

Windows 10 Enterprise multi-session is a new Remote Desktop Session Host exclusive to [Windows Virtual Desktop]( https://docs.microsoft.com/azure/virtual-desktop/) on Azure. It provides the following benefits:

- Allows multiple concurrent user sessions.
- Gives users a familiar Windows 10 experience.
- Supports use existing per-user Microsoft 365 licensing.

## Prerequisites

This public preview feature supports Windows 10 Enterprise multi-session VMS which are:

- Running Winodws 10 multi-session, version 1903 or later.
- [Hybrid Azure AD-joined]( https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).
- Set up as remote desktops in pooled host pools in Azure.
- Enrolled in Intune using one of the following methods:
  - Configured with [Active Directory group policy]( https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy), set to use Device credentials, and set to automatically enroll devices that are hybrid Azure AD joined.
  - [Configuration Manager co-management]( https://docs.microsoft.com/configmgr/comanage/overview).
  - [Configure Automatic enrollment] to automatically enroll devices that are Hybrid Azure AD joined.

For more information on Windows Virtual Desktop licensing requirements, see [What is Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview.md#requirements).

Windows 10 Enterprise multi-session VMs are treated as a separate OS edition and some existing Windows 10 Enterprise configurations won’t be supported for this edition.  Intune management does not depend on or interfere with Windows Virtual Desktop management of the same VM.

## Create the device configuration profile

Intune only supports managing Windows 10 Enterprise multi-session by using device configurations. This means only policies defined in the OS scope and apps configured to install in the system context can be applied to WVD multi-session VMs. Additionally, all multi-session configurations must be targeted to devices or device groups.

Existing device configuration profiles are not supported for Windows 10 Enterprise multi-session VMs, with the exception of Certificate profiles, which are available under Templates. Note that we only support device certificates at this point.

To configure configuration policies for Windows 10 Enterprise multi-session VMs, you must configure using the [Settings catalog](../configuration/settings-catalog.md)

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Windows** > **Configuration profiles** > **Create Profile**.
2. For **Platform**, select **Windows 10 and later**.
3. For **Profile type**, select **Settings Catalog (Preview)**
4. Select **Create**.
5. On the **Basics** page, provide a **Name** and (optionally) **Description** > **Next**.
6. On the **Configuration settings** page, select **Add settings**.
7. Under **Settings picker**, select **Add filter** and select the following options:
    - **Key**: **OS edition**
    - **Operator**: **==**
    - **Value**: **Enterprise multi-session**
    - Select **Apply**. The filtered list now shows all configuration profile categories that support Windows 10 Enterprise multisession. You can see the scope for the policy in parentheses (Device or User). Currently, only device settings are supported for multisession.
8. From the filtered list, pick the categories that you want.
    - For each category you pick, select the settings that you want to apply to your new configuration profile.
    - For each setting, select the value that you want for this configuration profile.
9. Select **Next** when you’re done adding settings.
10. On the **Assignments** page, choose the user groups containing the devices to which you want this profile assigned > **Next**.
11. On the **Scope tags** page, optionally add the scope tags you want to apply to this profile > **Next**. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
12. On the **Review + create** page, choose **Create** to create the profile.

### Administration templates

Windows 10 Administrative Templates are supported for Windows 10 Enterprise multi-session by using the Settings catalog. There are some limitations:

- All ADMX-backed policies are supported. Some policies are not yet available in the Settings catalog.
- ADMX-ingested policies are not currently supported. This includes Office and Microsoft Edge settings available in Office administrative template files and Microsoft Edge administrative template files. For a complete list of ADMX-ingested policy categories, see [Win32 and Desktop Bridge app policy configuration]( https://docs.microsoft.com/windows/client-management/mdm/win32-and-centennial-app-policy-configuration.md#overview).

## Compliance and Conditional access

Device compliance settings for Windows 10 Enterprise multi-session are limited in the preview. Changes can’t be made to a multi-session VM that would cause non-compliance. As a result, all VMs are marked as Compliant by default.

You can secure your Windows 10 Enterprise multi-session VMs by configuring compliance policies and Conditional Access policies in the Endpoint Manager admin center. The following compliance policies are supported on Windows 10 Enterprise multi-session VMs:

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

[!Important] You’ll need to create a new compliance policy and target it to the device group containing your multi-session VMs. User-targeted compliance configurations aren’t supported.

[Conditional Access policies](../protect/conditional-access.md) support both user and device based configurations for Windows 10 Enterprise multi-session.  

## Application deployment

All Windows 10 apps can be deployed to Windows 10 Enterprise multi-session with the following restrictions:

- All apps must be configured to install in the system/device context and be targeted to devices. Web apps are always applied in the user context by default so they will not apply to multi-session VMs.
- All apps must be configured with **Required** or **Uninstall** app assignment intent. The **Available apps** deployment intent is not supported on multi-session VMs.  
- If a Win32 app configured to install in the system context has dependencies or supersedence relationship on any apps configured to install in the user context, the app will not be installed. To apply to a Windows 10 Enterprise multi-session VM, create a separate instance of the system context app or make sure all app dependencies are configured to install in the system context.
- Windows Virtual Desktop RemoteApp and MSIX app attach are not currently supported in Intune.

## Script deployment

Scripts configured to run in the system context are supported on Windows 10 Enterprise multi-session. This can be configured under Script settings by setting **Run this script using the logged on credentials** to **No**.

## Windows Update for Business

Windows Update for Business policies are not currently supported for Windows 10 Enterprise multi-session.  
We recommend that you swap the OS image in Azure if you need the latest security updates. If you use the Azure Gallery image, you always get the latest security updates and can make sure all VMs are up-to-date and secured.

## Remote actions

The following Windows 10 desktop device remote actions are not supported and will be grayed out in the UI and disabled in Graph for Windows 10 Enterprise multi-session VMs:

- Autopilot reset
- BitLocker key rotation
- Fresh Start
- Remote lock
- Reset password
- Wipe

## Retirement

Deleting VMs from Azure will leave orphaned device records in Intune. They will be automatically cleaned up according to the cleanup rules configured for the tenant.

## Additional configurations which are not supported on Windows 10 Enterprise multi-session VMs

Out of Box Experience (OOBE) enrollment isn't supported for Window 10 Enterprise multi-session. This restriction means that:

- Windows Autopilot and Commercial OOBE aren't supported.
- Enrollment status page isn’t supported.

Windows 10 Enterprise multi-session managed by Intune is not currently supported for US Government Community (GCC), GCC High, DoD, or China.

## Next steps

[Learn more about Windows Virtual Desktops](/azure/virtual-desktop/).
