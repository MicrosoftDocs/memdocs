---
title: Configure Microsoft Edge settings
titleSuffix: Configuration Manager
description: Configure settings for the Microsoft Edge web browser on Windows 10 clients
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6


---

# Configure Microsoft Edge settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

<!-- 1357310 -->
Starting in version 1802, for customers who use the [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser on Windows 10 clients, create a Configuration Manager compliance settings policy to configure several Microsoft Edge settings. 

This policy only applies to clients on Windows 10, version 1703 or later. <!--511552-->


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


### Configure Windows Defender SmartScreen settings for Microsoft Edge
<!--1353701-->
Starting in version 1806, this policy adds three settings for [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). The policy now includes the following additional settings on the **SmartScreen Settings** page:

- **Allow SmartScreen**: Specifies whether Windows Defender SmartScreen is allowed. For more information, see the [AllowSmartScreen browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Users can override SmartScreen prompt for sites**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about potentially malicious websites. For more information, see the [PreventSmartScreenPromptOverride browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Users can override SmartScreen prompt for files**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about downloading unverified files. For more information, see the [PreventSmartScreenPromptOverrideForFiles browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## Create the Microsoft Edge browser profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Expand **Compliance Settings** and select the **Microsoft Edge Browser Profiles** node. Click the ribbon option to **Create Microsoft Edge profile**.
2. Specify a **Name** for the policy, optionally enter a **Description**, and click **Next**.
3. On the **General Settings** page, change the value to **Configured** for the settings to include in this policy, and click **Next**. The setting to **Set Edge Browser as default** must be configured to continue.
4. In version 1806 and later, configure settings on the **SmartScreen Settings** page, and then click **Next**. 
5. On the **Supported Platforms** page, select the OS versions and architectures to which this policy applies, and click **Next**. 
6. Complete the wizard.



## Deploy the policy

1. Select your policy and click the ribbon option to **Deploy**.
2. Click **Browse** to select the user or device collection to which to deploy the policy. 
3. Select additional options as necessary.  
     a. Generate alerts when the policy is not compliant.  
     b. Set the schedule by which the client evaluates the device's compliance with this policy. 
4. Click **OK** to create the deployment.



## Next steps

Like any compliance settings policy, the client remediates the settings on the schedule you specify. [Monitor and report on device compliance](monitor-compliance-settings.md) in the Configuration Manager console.
