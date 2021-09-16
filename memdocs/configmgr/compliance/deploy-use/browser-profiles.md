---
title: Configure Microsoft Edge settings
titleSuffix: Configuration Manager
description: Configure settings for the Microsoft Edge Legacy web browser on Windows 10 clients
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/02/2021
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.localizationpriority: medium
---

# Configure Microsoft Edge Legacy settings in Configuration Manager

> [!IMPORTANT]
> If you're using Microsoft Edge version 77 or later, and are trying to open the settings pane, enter `edge://settings/profiles` in the browser address bar instead of search. For more information, see [Get to know Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> This article is for IT professionals to manage Microsoft Edge Legacy settings with Microsoft Endpoint Configuration Manager.

*Applies to: Configuration Manager (current branch)*

<!-- 1357310 -->
For customers who use the [Microsoft Edge Legacy](/microsoft-edge/deploy/) web browser on Windows 10 clients, create a Configuration Manager compliance policy to configure the browser settings.

> [!WARNING]
> This feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Support ends for the Microsoft Edge Legacy desktop application on March 9, 2021. With the April cumulative update for Windows 10, the new Microsoft Edge replaces Microsoft Edge Legacy. For more information, see [New Microsoft Edge to replace Microsoft Edge Legacy with April’s Windows 10 Update Tuesday release](https://techcommunity.microsoft.com/t5/microsoft-365-blog/new-microsoft-edge-to-replace-microsoft-edge-legacy-with-april-s/ba-p/2114224).<!-- 9388900 -->

This policy only applies to clients on Windows 10, version 1703 or later, and Microsoft Edge Legacy version 45 and earlier. <!--511552-->

For more information on managing Microsoft Edge version 77 or later with Configuration Manager, see [Deploy Microsoft Edge, version 77 and later](../../apps/deploy-use/deploy-edge.md). For more information on configuring policies for Microsoft Edge version 77 or later, see [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies).

## Policy settings

This policy currently includes the following settings:

- **Set Microsoft Edge browser as default**: configures the Windows 10 default app setting for web browser to Microsoft Edge

- **Allow address bar drop-down**: Requires Windows 10, version 1703 or later. For more information, see [AllowAddressBarDropdown browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).

- **Allow sync favorites between Microsoft browsers**: Requires Windows 10, version 1703 or later. For more information, see [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).

- **Allow clear browsing data on exit**: Requires Windows 10, version 1703 or later. For more information, see [ClearBrowsingDataOnExit browser policy](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).

- **Allow Do Not Track headers**: For more information, see [AllowDoNotTrack browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).

- **Allow autofill**: For more information, see [AllowAutofill browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).

- **Allow cookies**: For more information, see [AllowCookies browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).

- **Allow pop-up blocker**: For more information, see [AllowPopups browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).

- **Allow search suggestions in address bar**: For more information, see [AllowSearchSuggestionsinAddressBar browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).

- **Allow send intranet traffic to Internet Explorer**: For more information, see [SendIntranetTraffictoInternetExplorer browser policy](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).

- **Allow password manager**: For more information, see [AllowPasswordManager browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).

- **Allow Developer Tools**: For more information, see [AllowDeveloperTools browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).

- **Allow extensions**: For more information, see [AllowExtensions browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

> [!TIP]
> For more information on using group policy to configure these and other settings, see [Microsoft Edge Legacy group policies](/microsoft-edge/deploy/group-policies/).

### Configure Windows Defender SmartScreen settings for Microsoft Edge Legacy
<!--1353701-->
This policy adds three settings for [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). The policy now includes the following additional settings on the **SmartScreen Settings** page:

- **Allow SmartScreen**: Specifies whether Windows Defender SmartScreen is allowed. For more information, see the [AllowSmartScreen browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Users can override SmartScreen prompt for sites**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about potentially malicious websites. For more information, see the [PreventSmartScreenPromptOverride browser policy](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Users can override SmartScreen prompt for files**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about downloading unverified files. For more information, see the [PreventSmartScreenPromptOverrideForFiles browser policy](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## Create the browser profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Expand **Compliance Settings** and select the **Microsoft Edge Browser Profiles** node. In the ribbon, select **Create Microsoft Edge profile**.

2. Specify a **Name** for the policy, optionally enter a **Description**, and select **Next**.

3. On the **General Settings** page, change the value to **Configured** for the settings to include in this policy. To continue the wizard, make sure to configure the setting to **Set Edge Browser as default**.

4. Configure settings on the **SmartScreen Settings** page.

5. On the **Supported Platforms** page, select the OS versions and architectures to which this policy applies.

6. Complete the wizard.

## Deploy the policy

1. Select your policy, and in the ribbon select **Deploy**.

2. **Browse** to select the user or device collection to which to deploy the policy.

3. Select additional options as necessary:

    1. Generate alerts when the policy isn't compliant.

    2. Set the schedule by which the client evaluates the device's compliance with this policy.

4. Select **OK** to create the deployment.

## Next steps

Like any compliance settings policy, the client remediates the settings on the schedule you specify. [Monitor and report on device compliance](monitor-compliance-settings.md) in the Configuration Manager console.