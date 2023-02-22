---
# required metadata
title: Use Windows Defender Application Control on HoloLens 2 devices in Microsoft Intune
description: Configure the Windows Defender Application Control (WDAC) CSP to allow or block apps from opening on HoloLens 2 devices in Microsoft Intune. Use PowerShell and a custom configuration profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/18/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use WDAC and Windows PowerShell to allow or blocks apps on HoloLens 2 devices with Microsoft Intune

Microsoft HoloLens 2 devices support the [Windows Defender Application Control (WDAC) CSP](/windows/client-management/mdm/applicationcontrol-csp), which replaces the [AppLocker CSP](/windows/client-management/mdm/applocker-csp).

Using Windows PowerShell and Microsoft Intune, you can use the WDAC CSP to allow or block specific apps from opening on Microsoft HoloLens 2 devices. For example, you may want to allow or prevent the Cortana app from opening on HoloLens 2 devices in your organization.

This feature applies to:

- HoloLens 2 devices running Windows Holographic for Business

The WDAC CSP is based on the [Windows Defender Application Control (WDAC) feature](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). You can also [use multiple WDAC policies](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

This article shows you how to:

1. Use Windows PowerShell to create WDAC policies.
2. Use Windows PowerShell to convert the WDAC policy rules to XML, update the XML, and then convert the XML to a binary file.
3. In Microsoft Intune, create a [custom device configuration profile](custom-settings-windows-holographic.md), add this WDAC policy binary file, and apply the policy to your HoloLens 2 devices.

In Intune, you must create a custom configuration profile to use the Windows Defender Application Control (WDAC) CSP. 

Use the steps in this article as a template to allow or deny specific apps from opening on HoloLens 2 devices.

## Prerequisites

- Be familiar with Windows PowerShell.
- Sign in to Intune as a member of:

  - **Policy and Profile Manager** or **Intune Role Administrator** Intune role

    OR

  - **Global Administrator** or **Intune Service Administrator** Azure AD role

  [Role-based access control (RBAC) with Intune](../fundamentals/role-based-access-control.md) has more information.

- Create a user group or devices group with your HoloLens 2 devices. For more information, see [User groups vs. device groups](device-profile-assign.md#user-groups-vs-device-groups).

## Example

This example uses Windows PowerShell to create a Windows Defender Application Control (WDAC) policy. The policy prevents specific apps from opening. Then, use Intune to deploy the policy to HoloLens 2 devices.

1. On your desktop computer, open the **Windows PowerShell** app.
2. Get information about the installed application package on your desktop computer and HoloLens:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    For example, enter:

    ```powershell
    $package1 = Get-AppxPackage -name Microsoft.MicrosoftEdge
    ```

    Next, confirm the package has application attributes:

    ```powershell
    $package1
    ```

    You'll see attributes similar to the following app details:

    ```powershell
    Name              : Microsoft.MicrosoftEdge
    Publisher         : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        :
    Version           : 44.20190.1000.0
    PackageFullName   : Microsoft.MicrosoftEdge_44.20190.1000.0_neutral__8wekyb3d8bbwe
    InstallLocation   : C:\Windows\SystemApps\Microsoft.MicrosoftEdge_8wekyb3d8bbwe
    IsFramework       : False
    PackageFamilyName : Microsoft.MicrosoftEdge_8wekyb3d8bbwe
    PublisherId       : 8wekyb3d8bbwe
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

    > [!NOTE]
    > You can block apps that are only installed on HoloLens devices. For more information, see [package family names for apps on HoloLens](/hololens/windows-defender-application-control-wdac#package-family-names-for-apps-on-hololens). 

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

6. If you plan to deploy and run any apps that didn't originate from the Microsoft Store, such as line of business apps (see [App Management](/hololens/app-deploy-overview)), then explicitly allow these apps by adding their signer to the WDAC policy.

    > [!NOTE]
    > Using WDAC and LOB apps is currently only available in [Windows Insiders features for HoloLens](/hololens/hololens-insider).

    For example, you plan on deploying `ATestApp.msix`. `ATestApp.msix` is signed by the `TestCert.cer` certificate. Use the following Windows PowerShell script to add the signer to the WDAC policy:
    
    ```powershell
    Add-SignerRule -FilePath .\newPolicy.xml -CertificatePath .\TestCert.cer -User
    ```

7. Merge **newPolicy.xml** with the default policy that's on your desktop computer. This step creates **mergedPolicy.xml**. For example, allow the Windows, WHQL signed drivers, and Store signed apps to run:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

8. Disable the **Audit mode** rule in **mergedPolicy.xml**. When you merge, audit mode is automatically turned on:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

9. Enable the **InvalidateEAs on a reboot** rule in **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    For more information on these rules, see [Understand WDAC policy rules and file rules](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

10. Convert **mergedPolicy.xml** to binary format. This step creates **compiledPolicy.bin**. You'll add this **compiledPolicy.bin** binary file to Intune.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

11. Create the custom device configuration profile in Intune:

    1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a Windows 10/11 custom device configuration profile.

        For the specific steps, see [Create a custom profile using OMA-URI in Intune](custom-settings-configure.md).

    2. When you create the profile, enter the following settings:

      - **OMA-URI**: Enter `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>/Policy`. Replace `<PolicyGUID>` with the PolicyTypeID node in the **mergedPolicy.xml** file you created in step 6.

        Using our example, enter `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076/Policy`.

        The policy GUID **must match** the PolicyTypeID node in the **mergedPolicy.xml** file (created in step 6).

        The OMA-URI uses the [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp). For more information on the nodes in this CSP, go to [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp).

      - **Data type**: Set to **Base64 file**. It automatically converts the file from bin to base64.
      - **Certificate file**: Upload the **compiledPolicy.bin** binary file (created in step 9).

      Your settings look similar to the following settings:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Add a custom OMA-URI to configure ApplicationControl CSP in Microsoft Intune.":::

11. When the profile is [assigned](device-profile-assign.md) to your HoloLens 2 group, check the profile status. After the profile successfully applies, reboot the HoloLens 2 devices.

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Learn more about custom profiles in Intune](custom-settings-configure.md).
