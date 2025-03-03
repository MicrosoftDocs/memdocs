---
# required metadata
title: Use Windows Defender Application Control on HoloLens 2 devices in Microsoft Intune
description: Configure the Windows Defender Application Control (WDAC) CSP to allow or block apps from opening on HoloLens 2 devices in Microsoft Intune. Use PowerShell and a custom configuration profile.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/06/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
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

Using Windows PowerShell and Microsoft Intune, you can use the WDAC CSP to allow or block specific apps from opening on Microsoft HoloLens 2 devices. For example, you might want to allow or prevent an app from opening on HoloLens 2 devices in your organization.

This feature applies to:

- HoloLens 2 devices running Windows Holographic for Business
- Windows 10/11

The WDAC CSP is based on the [Windows Defender Application Control (WDAC) feature](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). You can also [use multiple WDAC policies](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

This article shows you how to:

1. Use Windows PowerShell to create WDAC policies.
2. Use Windows PowerShell to convert the WDAC policy rules to XML, update the XML, and then convert the XML to a binary file.
3. In Microsoft Intune, create a [custom device configuration profile](custom-settings-windows-holographic.md), add this WDAC policy binary file, and apply the policy to your HoloLens 2 devices.

In Intune, you must create a custom configuration profile to use the Windows Defender Application Control (WDAC) CSP. 

Use the steps in this article as a template to allow or deny specific apps from opening on HoloLens 2 devices.

## Prerequisites

- Be familiar with Windows PowerShell. For information on the execution policy options, go to [Windows PowerShell about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).
- To configure the Intune policy, at a minimum, sign into the Intune admin center as a member of the **Policy and Profile Manager** built-in Intune role.

  For information on the Intune built-in roles, and what they can do, go to:

  - [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)
  - [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md)

- Create a user group or devices group with your HoloLens 2 devices. For information on groups, go to [User groups vs. device groups](device-profile-assign.md#user-groups-vs-device-groups).

## Step 1 - Create the WDAC policy using Windows PowerShell

This example uses Windows PowerShell to create a Windows Defender Application Control (WDAC) policy. The policy prevents specific apps from opening.

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

    App details similar to the following attributes are shown:

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
    > You can block apps that are only installed on HoloLens devices. For more information, go to [package family names for apps on HoloLens](/hololens/windows-defender-application-control-wdac#package-family-names-for-apps-on-hololens).

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

    For information on these rules, go to [Understand WDAC policy rules and file rules](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

10. Convert **mergedPolicy.xml** to binary format. This step creates **compiledPolicy.bin**. In [Step 2 - Create an Intune policy and deploy the policy to HoloLens 2 devices](#step-2---create-an-intune-policy-and-deploy-the-policy-to-hololens-2-devices), you add this **compiledPolicy.bin** binary file to an Intune policy.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

## Step 2 - Create an Intune policy and deploy the policy to HoloLens 2 devices

In this step, you create a custom device configuration profile in Intune. In the custom policy, you add the **compiledPolicy.bin** binary file you created in [Step 1 - Create the WDAC policy using Windows PowerShell](#step-1---create-the-wdac-policy-using-windows-powershell). Then, use Intune to deploy the policy to HoloLens 2 devices.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a Windows custom device configuration profile.

    For the specific steps, go to [Create a custom profile using OMA-URI in Intune](custom-settings-configure.md).

2. When you create the profile, enter the following settings:

    - **OMA-URI**: Enter `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>/Policy`. Replace `<PolicyGUID>` with the PolicyTypeID node in the **mergedPolicy.xml** file you created in step 6.

      Using our example, enter `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076/Policy`.

      The policy GUID **must match** the PolicyTypeID node in the **mergedPolicy.xml** file (created in step 6).

      The OMA-URI uses the [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp). For information on the nodes in this CSP, go to [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp).

    - **Data type**: Set to **Base64 file**. It automatically converts the file from bin to base64.
    - **Certificate file**: Upload the **compiledPolicy.bin** binary file (created in step 10).

    Your settings look similar to the following settings:

    :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Add a custom OMA-URI to configure ApplicationControl CSP in Microsoft Intune.":::

3. When the profile is [assigned](device-profile-assign.md) to your HoloLens 2 group, check the profile status. After the profile successfully applies, reboot the HoloLens 2 devices.

## Related articles

- [Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
- [Learn more about custom profiles in Intune](custom-settings-configure.md).
