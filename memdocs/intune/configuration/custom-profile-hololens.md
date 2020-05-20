---
# required metadata
title: Use Windows Defender Application Control on HoloLens 2 devices in Microsoft Intune - Azure | Microsoft Docs
description: Configure the Windows Defender Application Control (WDAC) CSP to allow or block apps from opening on HoloLens 2 devices in Microsoft Intune. Use PowerShell and a custom configuration profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use WDAC and Windows PowerShell to allow or blocks apps on HoloLens 2 devices with Microsoft Intune

To allow or block specific apps from running on Microsoft HoloLens 2 devices, use a custom configuration profile in Intune.

Microsoft HoloLens 2 devices support the [Windows Defender Application Control (WDAC) CSP](https://docs.microsoft.com/windows/client-management/mdm/applicationcontrol-csp). This WDAC CSP replaces the [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp), and is based on the [Windows Defender Application Control (WDAC) feature](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). You can also [use multiple WDAC policies](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

In Intune, using a custom profile is the only way to allow or prevent apps from opening on HoloLens 2 devices.

This feature applies to:

- HoloLens 2 devices running Windows Holographic for Business

This article shows you how to:

1. Using Windows PowerShell, create WDAC policies.
2. Using Windows PowerShell, convert the WDAC policy rules to XML, update the XML, and then convert the XML to a binary file.
3. In Microsoft Intune, apply the WDAC policy using a [custom device configuration profile](custom-settings-windows-10.md).

Use the steps in this article as a template to allow or deny specific apps from opening on HoloLens 2 devices.

## Prerequisites

- Be familiar with Windows PowerShell.
- Sign in to Intune as a member of:

  - **Policy and Profile Manager** or **Intune Role Administrator** Intune role

    OR

  - **Global Administrator** or **Intune Service Administrator** Azure AD role

  [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information.

- Create a user group or devices group with your HoloLens 2 devices.

## Example

This example uses Windows PowerShell to create a Windows Defender Application Control (WDAC) policy. The policy prevents specific apps from opening. Then, use Intune to deploy the policy to HoloLens 2 devices.

1. On your desktop computer, open the **Windows PowerShell** app.
2. Get information about the installed application package on your desktop computer:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    For example, enter:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Next, confirm the package has application attributes:

    ```powershell
    $package1
    ```

    You'll see attributes similar to the following app details:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Create a WDAC policy, and add the app package to the DENY rule:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Repeat steps 2 and 3 for any other applications you want to DENY:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    For example, enter:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Convert the WDAC policy to **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    To target all versions of an app, in newPolicy.xml, be sure `PackageVersion="65535.65535.65535.65535"` is in Deny node:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    For `PackageFamilyNameRules`, you can use the following versions:

    - **Allow**: Enter `PackageVersion, 0.0.0.0`, which means "Allow this version and above".
    - **Deny**: Enter `PackageVersion, 65535.65535.65535.65535`, which means "Deny this version and below".

6. Merge **newPolicy.xml** with the default policy that's on your desktop computer. This step creates **mergedPolicy.xml**. For example, allow the Windows, WHQL signed drivers, and Store signed apps to run:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Disable the **Audit mode** rule in **mergedPolicy.xml**. When you merge, audit mode is automatically turned on:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Enable the **InvalidateEAs on a reboot** rule in **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    For more information on these rules, see [Understand WDAC policy rules and file rules](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Convert **mergedPolicy.xml** to binary format. This step creates **compiledPolicy.bin**:

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Copy the following script, as save it as a `.ps1` file. Then, execute this `.ps1` PowerShell script in the PowerShell window.

    This script converts the **compiledPolicy.bin** binary file to a base64 string. You'll add this converted **compiledPolicy.bin** binary file to Intune.

    ```powershell
    param(
    [Parameter(Mandatory=$true)]
    [string]$sourceFilePath,
    [Parameter(Mandatory=$true)]
    [string]$targetFilePath
    )
    
    Write-Output "Reading from $sourceFilePath"
    [byte[]]$bytes = Get-Content "$sourceFilePath" -Encoding byte
    
    $output = [System.Convert]::ToBase64String($bytes)
    
    Write-Output "Writing to $targetFilePath"
    
    Set-Content -Path "$targetFilePath" -Value $output -Encoding Ascii
    ```

11. Create the custom device configuration profile in Intune:

    1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a Windows 10 custom device configuration profile.

        For the specific steps, see [Create a custom profile using OMA-URI in Intune](custom-settings-configure.md).

    2. When you create the profile, enter the following settings:

      - **OMA-URI**: Enter `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>`. Replace `<PolicyGUID>` with the PolicyTypeID node in the **mergedPolicy.xml** file you created in step 6.

        Using our example, enter `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076`.

        The policy GUID **must match** the PolicyTypeID node in the **mergedPolicy.xml** file (created in step 6).

      - **Data type**: Set to **Base64 file**. It automatically converts the file from bin to base64.
      - **Certificate file**: Upload the **compiledPolicy.bin** binary file (created in step 9, and converted in step 10).

      Your settings look similar to the following settings:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Add a custom OMA-URI to configure ApplicationControl CSP in Microsoft Intune.":::

When the profile is applied to your HoloLens 2 group, check the profile status. After the profile successfully applies, reboot the HoloLens 2 devices. Using Windows PowerShell, you can see the apps being denied, and prevented from opening.

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Learn more about custom profiles in Intune](custom-settings-configure.md).
