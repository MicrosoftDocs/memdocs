---
title: Enable Win32 apps on S mode devices
titleSuffix: Microsoft Intune
description: Learn how to enable Win32 apps on S mode devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/07/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Enable Win32 apps on S mode devices

[Windows 10 S mode](/windows/deployment/s-mode) is a locked-down operating system that only runs Store apps. By default, Windows S mode devices don't allow installation and execution of Win32 apps. These devices include a single *Win 10S base policy*, which locks the S mode device from running any Win32 apps on it. However, by creating and using an **S mode supplemental policy** in Intune, you can install and run Win32 apps on Windows 10 S mode managed devices. By using the [Microsoft Defender Application Control (WDAC)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) PowerShell tools, you can create one or more supplemental policies for Windows S mode. You must sign the supplemental policies with the [Device Guard Signing Service (DGSS)](/microsoft-store/device-guard-signing-portal) or with [SignTool.exe](/windows/security/threat-protection/windows-defender-application-control/use-signed-policies-to-protect-windows-defender-application-control-against-tampering) and then upload and distribute the policies via Intune. As an alternative, you can sign the supplemental policies with a codesigning certificate from your organization, however the preferred method is to use DGSS. In the instance that you use the codesigning certificate from your organization, the root certificate that the codesigning certificate chains up to, must be present on the device.

By assigning the S mode supplemental policy in Intune, you enable the device to make an exception to the device's existing S mode policy, which allows the uploaded corresponding signed app catalog. The policy sets an allowlist of apps (the app catalog) that can be used on the S mode device.

> [!NOTE]
> Win32 apps on S mode devices are only supported on Windows 10 November 2019 Update (build 18363) or later versions.

<!-- Add WDAC tooling diagram  -->

The steps to allow Win32 apps to run on a Windows 10 device in S mode are the following:

1. Enable S mode devices through Intune as part of Windows 10 S enrollment process.
1. Create a supplemental policy to allow Win32 apps:
   - You can use [Microsoft Defender Application Control (WDAC)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) tools to create a supplemental policy. The base policy ID within the policy must match the S mode base policy ID (which is hard coded on the client)​. Also, make sure that the policy version is higher than the previous version.
   - You use DGSS to sign your supplemental policy. For more information, see [Sign code integrity policy with Device Guard signing](/microsoft-store/sign-code-integrity-policy-with-device-guard-signing).
   - You upload the signed supplemental policy to Intune by creating a Windows 10 S mode supplemental policy (see below).
1. You allow Win32 app catalogs through Intune:
   - You create catalog files (one for every app) and signs them using DGSS or other certificate infrastructure.
   - You package the signed catalog into the *.intunewin* file using the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730). There are no naming restrictions when creating a catalog file using the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730). When generating the *.intunewin* file from the specified source folder and setup file, you can provide a separate folder containing only catalog files by using the -a cmdline option. For more information, see [Win32 app management - Prepare the Win32 app content for upload](apps-win32-app-management.md#prepare-the-win32-app-content-for-upload).
   - Intune applies the signed app catalog to install the Win32 app on the S mode device using the [Intune Management Extension](intune-management-extension.md).

> [!NOTE]
> Line-of-business (LOB) `.appx` and `.appx` bundles on Windows 10 S mode will be supported via Microsoft Store for Business (MSFB) signing.
>
> **S mode supplemental policy** for apps must be delivered via Intune Management Extension.
>
> S mode policies are enforced at the device level. Multiple targeted policies will be merged on the device. The merged policy will be enforced on the device.

To create a Windows 10 S mode supplemental policy, use the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **S mode supplemental policies** > **Create policy**.
3. Before adding the **Policy file**, you must create and sign it. For more information, see:
    - [Create a WDAC policy using PowerShell tools and convert it to a binary format](/windows/security/threat-protection/windows-defender-application-control/lob-win32-apps-on-s)
    - [Sign using Device Guard Signing Service](/microsoft-store/device-guard-signing-portal) **(recommended)**

4. On the **Basics** page, add the following values:

    | Value | Description |
    |--------------|------------------------------------------------|
    | Policy file | The file that contains the WDAC policy. |
    | Name | The name of this policy. |
    | Description | [Optional] The description of this policy. |

1. Select **Next: Scope tags**.<br>
   On the **Scope tags** page you can optionally configure scope tags to determine who can see the app policy in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

1. Select **Next: Assignments**.<br>
   The **Assignments** page allows you can assign the policy to users and devices. It's important to note that you can assign a policy to a device whether or not the device is managed by Intune.
1. Select **Next: Review + create** to review the values you entered for the profile.
1. When you're done, select **Create** to create the S mode supplemental policy in Intune.

Once the policy is created, you'll see it added to the list of S mode supplemental policies in Intune. Once the policy is assigned, the policy gets deployed to the devices. Note that you must deploy the app to same security group as the supplemental policy​. You can start targeting and assigning apps to those devices. This will allow your end users to install and execute the apps on the S mode devices.

## Removal of S mode policy

Currently, to remove the S mode supplemental policy from the device, you must assign and deploy an empty policy to overwrite the existing S mode supplemental policy.

## Policy Reporting​

The S mode supplemental policy, which is enforced at device level, only has device level reporting.​ Device level reporting is available for success and error conditions.

Reporting values that are shown in the Microsoft Intune admin center for S mode reporting policies:

- **Success**: The S mode supplemental policy is in effect.
- **Unknown**: The status of the S mode supplemental policy isn't known.
- **TokenError**: The S mode supplemental policy is structurally okay but there's an error with authorizing the token.
- **NotAuthorizedByToken**: The token doesn't authorize this S mode supplemental policy.
- **PolicyNotFound**: The S mode supplemental policy isn't found.

## Next steps

- For more information, see [Win32 apps on s mode](/windows/security/threat-protection/windows-defender-application-control/lob-win32-apps-on-s).
- For more information about adding apps to Intune, see [Add apps to Microsoft Intune](apps-add.md).
- For more information about Win32 apps, see [Intune Win32 app management](apps-win32-app-management.md).
