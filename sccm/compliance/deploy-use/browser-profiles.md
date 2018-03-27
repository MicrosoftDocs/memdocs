---
title: Configure Microsoft Edge settings
titleSuffix: Configuration Manager
description: Configure settings for the Microsoft Edge web browser on Windows 10 clients
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
---

# Configure Microsoft Edge settings in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<!-- 1357310 -->
Starting in version 1802, for customers who use the [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser on Windows 10 clients, create a Configuration Manager compliance settings policy to configure several Microsoft Edge settings. 



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



## Create the Microsoft Edge browser profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Expand **Compliance Settings** and select the new **Microsoft Edge Browser Profiles** node. Click the ribbon option to **Create Microsoft Edge Browser Policy**.
2. Specify a **Name** for the policy, optionally enter a **Description**, and click **Next**.
3. On the **Settings** page, change the value to **Configured** for the settings to include in this policy, and click **Next**.
4. On the **Supported Platforms** page, select the operating system versions and architectures to which this policy applies, and click **Next**. 
5. Complete the wizard.



## Deploy the policy

1. Select your policy and click the ribbon option to **Deploy**.
2. Click **Browse** to select the user or device collection to which to deploy the policy. 
3. Select additional options as necessary. 
    a. Generate alerts when the policy is not compliant. 
    b. Set the schedule by which the client evaluates the device's compliance with this policy.
4. Click **OK** to create the deployment.



## Next steps

Like any compliance settings policy, the client remediates the settings on the schedule you specify. [Monitor and report on device compliance](/sccm/compliance/deploy-use/monitor-compliance-settings) in the Configuration Manager console.
