---
title: Supported Microsoft Intune apps
titleSuffix:
description: This topic provides lists of support partner and Microsoft apps that are commonly used with Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/05/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 003ce5af-7ee1-43fb-8d16-9d08c7957a85
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Intune protected apps  

The apps listed in this topic are supported partner and Microsoft apps that are commonly used with Microsoft Intune. Intune protected apps are enabled with a rich set of mobile application protection policies. These apps allow you to:

- Restrict copy-and-paste and save-as functions
- Configure web links to open inside the secure Microsoft browser
- Enable multi-identity use and app-level Conditional Access
- Apply data loss prevention policies without managing the user's device
- Enable app protection without requiring enrollment
- Enable app protection on devices managed with 3rd party EMM tools

> [!NOTE]
> For your client line-of-business apps, you can incorporate mobile app management using the [Intune App Software Development Kit](../developer/app-sdk.md) (SDK), or the [App Wrapping Tool for iOS](../developer/app-wrapper-prepare-ios.md) and the [App Wrapping Tool for Android](../developer/app-wrapper-prepare-android.md).

The following tables provide details of supported partner and Microsoft apps that are commonly used with Microsoft Intune.

## Microsoft apps
The below apps support Intune App Protection Policies. Apps are also capable of supporting advanced App Protection Policy and App Configuration Policy settings. The below table identifies the capabilities of each app. 

> [!NOTE]
> For more information on Conditional Access support, see [App protection policy requirement](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-app-protection-policy).

For more information on the columns within the **Advanced App Configuration and Protection Policy feature support** section, see:

- [Multi-identity](app-protection-policy.md#multi-identity)
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
- [iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps) and [Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps) Allow only configured organization accounts in multi-identity apps
- [iOS](app-protection-policy-settings-ios.md#functionality) and [Android](app-protection-policy-settings-android.md#functionality) Sync policy managed app data with native apps
- [iOS](app-protection-policy-settings-ios.md#functionality) and [Android](app-protection-policy-settings-android.md#functionality) Org data notifications
- [iOS](app-protection-policy-settings-ios.md#data-transfer) and [Android](app-protection-policy-settings-android.md#data-transfer) Open data into Org documents (open from)
- [iOS](app-protection-policy-settings-ios.md#data-transfer) and [Android](app-protection-policy-settings-android.md#data-transfer) Save copies of org data (save as)


<table>
<thead>
  <tr class="header">
    <th rowspan="2">App</th>
    <th rowspan="2">Platform</th>
    <th rowspan="2">App Protection Policy</th>
    <th colspan="6">Advanced App Configuration and Protection Policy feature support</th>
  </tr>
  <tr>
    <td><b>App configuration</b></td>
    <td><b>Org allowed accounts</b></td>
    <td><b>Sync org data with native apps</b></td>
    <td><b>Org data notifications</b></td>
    <td><b>Org <i>open from</i> locations</b></td>
    <td><b>Org <i>save as</i> locations</b></td>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Field Service Mobile</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.d365.fs.mobile">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://apps.apple.com/us/app/field-service-mobile/id1414669075">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Azure Information Protection Viewer</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.ipviewer">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/rms-sharing/id689516635">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Bookings</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.exchange.bookings">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-bookings/id1065657468">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Cortana</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.cortana">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://apps.apple.com/us/app/cortana/id1054501703">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Dynamics CRM</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.crm.crmphone">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/app/microsoft-dynamics-crm/id678800460">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Edge</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.emmx">Google Play</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://aka.ms/edgeappconfig">Edge app config</a></td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-edge/id1288723196">App Store</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://aka.ms/edgeappconfig">Edge app config</a></td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Excel</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.excel">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-excel/id586683407">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Kaizala</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.mobile.polymer">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/in/app/microsoft-kaizala/id1112208399">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>Microsoft Launcher</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.launcher">Google Play</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://docs.microsoft.com/mem/intune/apps/configure-microsoft-launcher">Launcher app config</a></td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Office</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.officehubrow">Google Play</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://docs.microsoft.com/mem/intune/apps/manage-microsoft-office">Office app config</a></td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://apps.apple.com/app/microsoft-office/id541164041">App Store</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://docs.microsoft.com/mem/intune/apps/manage-microsoft-office">Office app config</a></td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft OneDrive</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.skydrive">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/onedrive-cloud-storage-for/id477537958">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft OneNote</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.onenote">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-onenote-for-iphone/id410395246">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Outlook</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.outlook">Google Play</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://aka.ms/omappconfig">Outlook app config</a></td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-outlook/id951937596">App Store</a></td>
    <td>Supported</td>
    <td>Supported, see <a href="https://aka.ms/omappconfig">Outlook app config</a></td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Planner</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.planner">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-planner/id1219301037">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft PowerApps</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.msapps">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/powerapps/id1047318566">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Power Automate</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.flow">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-flow/id1094928825">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Power BI</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.powerbim">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-power-bi/id929738808">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft PowerPoint</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.powerpoint">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-powerpoint/id586449534">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft SharePoint</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.sharepoint">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-sharepoint/id1091505266">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Skype for Business</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.lync15">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/app/skype-for-business-formerly/id605841731">App Store</a></td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft StaffHub</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=ols.microsoft.com.shiftr">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-staffhub/id1122181468?mt=8">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Stream</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.stream">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-stream/id1401013624">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Teams</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.teams">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-teams/id1113153706">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft To-Do</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.todos">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-to-do/id1212616790">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>Microsoft Visio</td>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-visio-viewer-flowcharts-and-diagrams/id1139787983">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Word</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.microsoft.office.word">Google Play</a></td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/microsoft-word/id586447913">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>Supported</td>
  </tr>
  <tr>
    <td rowspan="2">Microsoft Yammer</td>
    <td>Android - <a href="https://play.google.com/store/apps/details?id=com.yammer.v1">Google Play</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
  <tr>
    <td>iOS - <a href="https://itunes.apple.com/us/app/yammer/id289559439">App Store</a></td>
    <td>Supported</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td>N/A</td>
    <td>Not supported</td>
    <td>Not supported</td>
    <td><font color="red">UNKNOWN</font></td>
  </tr>
</tbody>
</table>

## Partner apps 
Apps are capable of supporting advanced App Protection Policy and App Configuration Policy settings. For more information, contact the app vendor.

| App   title | App description | App store links for supported   platform(s) | 
|-------------------------------------------------|-------------------------|---------------------------------------------|
| **Acronis Access**<p><img alt="Partner app - Acronis Access icon" src="./media/apps-supported-intune-apps/icon-p-acronis-access.png" width="100"> | Safely access your business files from anywhere and any device with Acronis Access. Easily share documents with colleagues, customers, and vendors while keeping files and data secure and private, where only you and your organization can touch them. The app is designed for extreme ease of use with unparalleled security, privacy, and management capabilities. | [App Store link (iOS)](https://itunes.apple.com/us/app/acronis-access/id429704844?mt=8) |                       
| **Adobe Acrobat Reader**<p><img alt="Partner app - Adobe Acrobat Reader icon" src="./media/apps-supported-intune-apps/icon-p-adobe-acrobat-reader.png" width="100"> | Open, view, and work with PDFs in a Microsoft Intune managed environment with Adobe Acrobat Reader. Available for iOS/iPadOS and Android. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.adobe.reader),<br>[App Store link (iOS)](https://apps.apple.com/app/adobe-acrobat-reader-for-pdf/id469337564) |                      
| **Blackberry Enterprise BRIDGE**<p><img alt="Partner app - Blackberry Enterprise BRIDGE icon" src="./media/apps-supported-intune-apps/icon-p-blackberry-enterprise-bridge.png" width="100"> | BlackBerry Enterprise BRIDGE allows you to securely view, edit, and save documents using Intune-managed Microsoft apps, such as Microsoft Word, Microsoft PowerPoint, and Microsoft Excel from BlackBerry Dynamics. You can share your documents as email attachments and maintain data encryption during the document-sharing process between BlackBerry Dynamics and Intune-managed mobile apps. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.blackberry.intune.bridge),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/blackberry-enterprise-bridge/id1305494864?mt=8) |
| **Bluejeans Video Conferencing**<p><img alt="Partner app - Bluejeans Video Conferencing icon" src="./media/apps-supported-intune-apps/icon-p-bluejeans.png" width="100"> | BlueJeans delivers a premium video conferencing experience that is optimized for the mobile workforce. With amazing features, like Dolby Voice® audio, BlueJeans helps make every meeting more productive regardless of where the participants are located.<p>Features:<p><ul><li>Participate in BlueJeans video meetings with up to 150 attendees.</li><li>Experience HD video and Dolby Voice® audio for the highest fidelity meetings.</li><li>Share and receive content for maximum productivity on-the-go.</li><li>Facilitate professional meetings with intuitive controls that make meeting moderation a breeze.</li><li>Integrate your calendar to enable one touch to join and easily jump from meeting-to-meeting.</li><li>Eliminate low-bandwidth spots with intelligent bandwidth management that optimize network settings.</li><li>Select safe driving mode while on the road for distraction-free meetings.</li></ul> | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.bluejeansnet.Base),<br>[App Store link (iOS)](https://apps.apple.com/app/bluejeans-video-conferencing/id560788314) |
| **Board Papers**<p><img alt="Partner app - Board Papers icon" src="./media/apps-supported-intune-apps/icon-p-board-papers.png" width="100"> | Board Papers is a board portal solution that combines an iPad application with Microsoft SharePoint® integration. | [App Store link (iOS)](https://apps.apple.com/app/board-papers/id458518678) |
| **Breezy for Intune**<p><img alt="Partner app - Breezy icon" src="./media/apps-supported-intune-apps/icon-p-breezy.png" width="100"> | Breezy For Intune provides secure print capabilities for your iOS device. Our integration with Intune ensures that your data stays secure while on-device, and own our end-to-end encryption and enterprise grade security ensure that it stays that way on its way to the printer. | [App Store link (iOS)](https://apps.apple.com/us/app/breezy-for-intune/id1447680750?mt=8) |
| **Box for EMM**<p><img alt="Partner app - Box for EMM icon" src="./media/apps-supported-intune-apps/icon-p-box-for-emm.png" width="100"> | Keep your employees connected and collaborative while you centrally manage security, policy, and provisioning across any mobile device using Box for EMM. | [App Store link (iOS)](https://itunes.apple.com/us/app/box-for-emm/id882085676?mt=8) |
| **CellTrust SL2&trade; for Microsoft Intune**<p><img alt="Partner app - CellTrust SL2 for Microsoft Intune icon" src="./media/apps-supported-intune-apps/icon-p-celltrust-sl2.png" width="100"> | CellTrust SL2&trade; for Microsoft Intune is an enterprise-level application that works by assigning a secure Mobile Business Number (MBN) on bring-your-own devices to keep personal and business communications separate on a single device. The seamless solutions secures SMS messages and business calls on the device without using the personal number. This capability is vital for enterprises that require greater security for business communications, as well as archiving for eDiscovery and compliance needs. <br><br> Microsoft Intune is a cloud-based service in the enterprise mobility management (EMM) space that helps enable your workforce to be productive while keeping your corporate data protected. <br><br> CellTrust SL2&trade; for Microsoft Intune delivers a powerful enterprise mobility platform, allowing employees to work on the go—with easy access to secure business applications, and voice and text messaging. The app was developed with Microsoft Intune SDKs and customized features to allow organizations to tailor it based on their industry and IT needs. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.celltrust.sl2_intune),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/celltrust-sl2-for-intune/id1442087513?mt=8) |
| **Cisco Jabber for Intune**<p><img alt="Partner app - Cisco Jabber for Intune icon" src="./media/apps-supported-intune-apps/icon-p-ciscojabber.png" width="100"> | Cisco Jabber for Intune is for admins to organize and protect BYOD environments with mobile application management (MAM). This app allows admins to protect corporate data while keeping employees connected. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.cisco.im.intune),<br>[App Store link (iOS)](https://apps.apple.com/app/cisco-jabber-for-intune/id1487776871) |               
| **Citrix Secure Mail**<p><img alt="Partner app - Citrix Secure Mail icon" src="./media/apps-supported-intune-apps/icon-p-citrix-secure-mail.png" width="100"> | Citrix Secure Mail is a containerized email, calendar, and contacts app with a rich user experience. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.citrix.mail.droid),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/citrix-secure-mail/id1155203964?mt=8) |               
| **Citrix ShareFile for Intune**<p><img alt="Partner app - Citrix ShareFile for Intune icon" src="./media/apps-supported-intune-apps/icon-p-citrix-sharefile.png" width="100">| Protect corporate data while accessing and sharing files from ShareFile. It directly integrates with Microsoft Word, Excel, and PowerPoint, to allow access to files from ShareFile without ever leaving your office application.| [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.citrix.sharefile.intune),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/citrix-sharefile-for-intune/id1056495502?mt=8) | 
| **Egress Secure Mail for Intune**<p><img alt="Partner app - Egress Secure Mail icon" src="./media/apps-supported-intune-apps/icon-p-egress-secure-mail-icon.png" width="100"> | Send and receive encrypted   emails and files from your mobile device. Egress Secure Email provides   user-friendly tools to secure sensitive data, with end-to-end encryption,   access revocation and message restrictions to empower users to stay in   control of the information they share.<p>The Egress Secure Email app   requires you to be a licensed user of the Egress platform, with a valid   subscription and appropriate infrastructure. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.egress.switchdroid.intune) | 
| **Hearsay Relate for Intune**<p><img alt="Partner app - Hearsay Relate for Intune icon" src="./media/apps-supported-intune-apps/icon-p-hearsay-relate-icon.png" width="100"> | Hearsay Relate for Intune enables advisors to manage and nurture their book of business in a protected BYOD environment with mobile application management (MAM). This version of Hearsay Relate allows IT administrators to protect corporate data while keeping advisors in touch with their book of business.<br><br> Hearsay Relate, a mobile application that enables financial services professionals to move business forward. Leverage compliant texting and seamless voice calling to connect with your entire book of business. Stay productive with calendar integration to set appointments, and schedule reminder messages for upcoming meetings, birthday greetings, and more.<br>Hearsay Relate for Intune gives enterprise users all the features they expect from Hearsay Relate, while providing IT administrators the MAM functionality they need to keep corporate data safe. In the event of a lost or stolen device, IT can remove Hearsay Relate for Intune from the device along with any sensitive data associated with it. | [Google Play link (Android)]( https://play.google.com/store/apps/details?id=com.hearsaysocial.messages.intune),<br>[App Store link (iOS)](https://apps.apple.com/app/hearsay-relate-for-intune/id1501771956) | 
| **iBabs for Intune**<p><img alt="Partner app - iBabs for Intune icon" src="./media/apps-supported-intune-apps/icon-p-ibabs.png" width="100">| ISEC7 Mobile Exchange Delegate allows authorized representatives via iPhone and iPad to agree to appointments for their colleagues, to manage their contacts, and to answer emails on behalf of other users. | [App Store link (iOS)](https://itunes.apple.com/us/app/ibabs-for-intune/id1130847428?mt=8) |
| **ISEC7 MED for Intune**<p><img alt="Partner app - ISEC7 MED for Intune icon" src="./media/apps-supported-intune-apps/icon-p-isec7-med.png" width="100">| Make your meetings simpler, more substantive, and more environmentally friendly. | [App Store link (iOS)](https://apps.apple.com/app/isec7-med-for-intune/id1491037389?ls=1) |
| **Lexmark Mobile Print Intune**<p><img alt="Partner app - Lexmark Mobile Print Intune icon" src="./media/apps-supported-intune-apps/icon-p-lexmark-mobile-print.png" width="100">| Mobile computing has become pervasive—it's simply a state of always on, barrier-free connectedness that entertains, enlightens and helps you get more work done. <br><br>While business users expect desktop and mobile printing to be equally convenient, IT managers know how complicated it can be to provide seamless output due to mobile's unique characteristics. With connectivity, security and network challenges to solve across multiple operating systems, providing your users with the flexible printing they expect can be complex. <br><br>Lexmark offers the experience and innovation to help you meet the printing needs of your users in a way that's easy and hassle-free for IT. By addressing your challenges with a comprehensive set of tools and options, we can help you achieve a mobile printing experience that is more transparent, simple and secure.  | [App Store link (iOS)](https://itunes.apple.com/us/app/lexmark-mobile-print-intune/id1368424840?ls=1&mt=8) |
| **Meetio Enterprise**<p><img alt="Partner app - Meetio Enterprise icon" src="./media/apps-supported-intune-apps/icon-p-meetio.png" width="100">| Meetio's mobile app for organizations using Meetio room management solutions. Meetio Enterprise simplifies your workday by allowing you to schedule meetings and meeting rooms - all at once, while you're on the go. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.getmeetio.personal),<br>[App Store link (iOS)](https://apps.apple.com/us/app/meetio/id1340190306) |
| **Nine Work for Intune**<p><img alt="Partner app - Nine Work for Intune icon" src="./media/apps-supported-intune-apps/icon-p-nine-work.png" width="100"> | Nine is a full-fledged email application for Android based on Direct Push technology to synchronize with Microsoft Exchange Server using Microsoft Exchange ActiveSync, and also designed for entrepreneurs or ordinary people who want to have efficient communication with their colleagues, friends, and family members at any time, anywhere. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.ninefolders.hd3.work.intune),<br>[App Store link (iOS)](https://apps.apple.com/us/app/nine-mail-email-calendar/id1079689905) |  
| **Now<sup>&#174;</sup> Mobile - Intune**<p><img alt="Partner app - Now Mobile for Intune icon" src="./media/apps-supported-intune-apps/icon-p-now-mobile.png" width="100"> | Now employees can find answers and get work done across IT, HR, Facilities, Finance, Legal and other departments, all from a modern mobile app powered by the Now Platform<sup>&#174;</sup>.<p>The Now Platform<sup>&#174;</sup> delivers employee experiences and productivity through digital workflows across departments, systems and people.<p>Examples of things you can do in the app:<ul><li>IT: Request a laptop or a reset password</li><li>Facilities: Find and book a conference room</li><li>Finance: Request a corporate credit card</li><li>Legal: Have a new vendor sign a non-disclosure agreement (NDA)</li><li>HR: Find the next company holiday and check the vacation policy</li></ul><p>Now<sup>&#174;</sup> Mobile powered by the Now Platform<sup>&#174;</sup> - finally work life can be as great as real life | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.servicenow.requestor.mam.intune),<br>[App Store link (iOS)](https://apps.apple.com/us/app/now-mobile-intune/id1494183300) | 
| **PrinterOn for Microsoft**<p><img alt="Partner app - PrinterOn for Microsoft icon" src="./media/apps-supported-intune-apps/icon-p-printeron.png" width="100"> | PrinterOn's wireless mobile printing solutions enable users to remotely print from anywhere at any time over a secure network.| [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.printeron.droid.phone),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/printeron-for-microsoft/id1258715414?mt=8) | 
| **Qlik Sense Mobile**<p><img alt="Partner app - Qlik Sense Mobile icon" src="./media/apps-supported-intune-apps/icon-p-qlik.png" width="100"> | Qlik Sense is a market leading, next generation application for self-service oriented analytics. Qlik's patented associative technology allows people to easily combine data from many different sources and explore it freely, without the limitations of query-based tools. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.qlik.qliksense.mobile),<br>[App Store link (iOS)](https://apps.apple.com/us/app/qlik-sense-mobile/id1217049362) | 
| **SAP Fiori**<p><img alt="Partner app - SAP Fiori icon" src="./media/apps-supported-intune-apps/icon-p-sap-fiori.png" width="100"> | Increase your daily productivity by tackling your most common business tasks anywhere and anytime with the SAP Fiori Client mobile app for iPhone and iPad. Deliver a next-level mobile experience with enhanced attachment handling and full-screen operations using this enhanced mobile runtime for the Web version of over 750 SAP Fiori app. Plus, access custom SAP Fiori mobile apps—built by customers using SAP Fiori mobile service—that are ready to support Intune mobile app management. | [App Store link (iOS)](https://itunes.apple.com/us/app/sap-fiori-client/id824997258?mt=8) |  
| **ServiceNow<sup>&#174;</sup> Agent - Intune**<p><img alt="Partner app - ServiceNow Agent icon" src="./media/apps-supported-intune-apps/icon-p-servicenow-agent.png" width="100"> | ServiceNow Mobile Agent app delivers out-of-the-box, mobile-first experiences for the most common service desk agent workflows, making it easy for agents to triage, act on and resolve requests on the go. The app enables service desk agents to promptly manage and resolve end user issues from their mobile devices. Agents use the app’s intuitive interface to accept and update work even without Internet connectivity. The app greatly simplifies work by leveraging native device capabilities for tasks like navigation, barcode scanning, or collecting a signature.<br><br>The app comes with out-of-the-box workflows for service desk agents in IT, Customer Service, HR, Field Services, Security Ops and IT Asset Management. Organizations can easily configure and extend the workflows to meet their own unique needs.<p>With Mobile Agent you can:<ul><li>Manage the work assigned to your teams.</li><li>Triage incidents and cases.</li><li>Act on approvals with swipe gestures and quick actions.</li><li>Complete work while offline.</li><li>Access the full issue details, activity stream, and related lists of records.</li><li>Optimize workflows with location, camera, and touchscreen hardware</li></ul> | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.servicenow.fulfiller.mam.intune),<br>[App Store link (iOS)](https://apps.apple.com/us/app/servicenow-agent-intune/id1494183149) |  
| **ServiceNow<sup>&#174;</sup> Onboarding - Intune**<p><img alt="Partner app - ServiceNow Onboarding icon" src="./media/apps-supported-intune-apps/icon-p-servicenow-onboarding.png" width="100"> | ServiceNow<sup>&#174;</sup> Mobile Onboarding empowers new hires to complete tasks, view content, and get help across departments—including IT, HR, Facilities, Finance, and Legal—all from a single native mobile app.<br><br>Streamline the onboarding experience by allowing new hires to:<ul><li>Order a laptop and phone from IT.</li><li>Setup a workspace with Facilities.</li><li>Sign a non-disclosure agreement (NDA) from Legal.</li><li>Submit a photo and update their profile with HR.</li><li>Review an expense policy from Finance and get help if they have questions.</li></ul>Powered by the Now Platform<sup>&#174;</sup>, Mobile Onboarding manages workflows across multiple departments and systems, hiding the complexity of backend processes. New hires don't even have to know which departments are involved in any given process. They receive a simple and easy onboarding experience and can complete tasks before they even start, ensuring they are day-one ready. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.servicenow.onboarding.mam.intune),<br>[App Store link (iOS)](https://apps.apple.com/app/servicenow-onboarding-intune/id1494184220) |  
| **Smartcrypt for Intune**<p><img alt="Partner app - Smartcrypt for Intune icon" src="./media/apps-supported-intune-apps/icon-p-smartcrypt.png" width="100"> | Smartcrypt for Intune is specifically designed for existing PKWARE customers operating in an Intune environment. Smartcrypt lets you get your work done on the go. It's fast, secure and simple to use so you can be productive from anywhere. If you are unsure if you have Smartcrypt please contact your company's IT administrator. With Smartcrypt, you can: Encrypt and decrypt files using Smartkeys, Decrypt archives with X.509 Digital Certificates, Create and manage Smartkeys, Perform digital signing and authentication of data with X.509 Digital Certificates, Encrypt and decrypt files with Strong Passphrase encryption, including AE2, Login with existing Active Directory credentials, Create and view unencrypted zip archives. Smartcrypt armors data at its core, eliminating vulnerabilities everywhere data is used, shared or stored. For nearly three decades, PKWARE has provided encryption and compression software to more than 30,000 enterprise customers and over 200 government agencies. Available for iOS/iPadOS and Android. | [App Store link (iOS)](https://apps.apple.com/app/smartcrypt-for-intune/id1489232256) |  
| **Speaking Email**<p><img alt="Partner app - Speaking Email icon" src="./media/apps-supported-intune-apps/icon-p-speaking-email-icon.png" width="100">   | Get more time in your day by having your email read to you on the move. Voice commands and simple gestures designed to be safe to use while driving give you the ability to archive, flag or even reply on the move.<p>Smart content detection skips over disclaimers, reply headers, and email signatures to speak only the content without the clutter.<p>Employees can sign in via Intune to access Microsoft 365 Exchange email. | [App Store link (iOS)](https://itunes.apple.com/app/apple-store/id991406423?ct=intune) | 
| **Synergi Life**<p><img alt="Partner app - Synergi Life icon" src="./media/apps-supported-intune-apps/icon-p-synergi-life.png" width="100"> | Synergi Life Mobile App, an extension of Synergi Life, lets users easily create observations and incident reports anytime and from anywhere, using their phones to take a snapshot and make a voice recording.<p>Synergi Life (previously named Synergi) is a complete business solution for risk and QHSE management, managing all non-conformances, incidents, risk, risk analyses, audits, assessments and improvement suggestions.<p>The Synergi Life Mobile App requires you to be a licensed user of the Synergi Life risk and QHSE management system, and have the necessary back-end licensed software and services. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.dnv.mobilesolutions.synergimobile.uibase), [App Store link (iOS)](https://itunes.apple.com/us/app/synergi-life/id641181737)  |  
| **Tableau Mobile for Intune**<p><img alt="Partner app - Tableau Mobile for Intune icon" src="./media/apps-supported-intune-apps/icon-p-tableau.png" width="100"> | Tableau Mobile gives you the freedom to stay on top of your data, no matter where you are or when you need it. With a fast, intuitive, and interactive experience, explore your dashboards and find just what you’re looking for, all from the convenience of your mobile device.<p>The Tableau Mobile app requires a Tableau Server or Tableau Online account. Please note, it does not work with Tableau Public.<p>Features:<p><ul><li>Interactive previews let you access your data even when you’re offline.</li><li>Mark your favorite dashboards or views to always have them at your fingertips.</li><li>Scroll, search, and browse your organization’s dashboards with a navigation experience that’s both intuitive and familiar.</li><li>Interact with your data to ask and answer questions on the go.</li></ul> | [App Store link (iOS)](https://apps.apple.com/app/tableau-mobile-for-intune/id1500089067)  |  
| **Tact for Intune**<p><img alt="Partner app - Tact for Intune icon" src="./media/apps-supported-intune-apps/icon-p-tact-icon.png" width="100"> | Tact for Intune is the first CRM and Sales Assistant that unifies data from Salesforce.com, email, calendar, maps and other everyday tools into a conversational, human-friendly experience. Powered by AI, Tact automates the administrative work for the salesperson, unifies CRM with other data sources to deliver a single pane of glass, and pushes intelligence to each seller in order to nudge them into high-performance behavior. Enterprises can now gain increased seller productivity, richer customer data and better CRM adoption while ensuring enterprise-grade security at the application layer with Tact for Intune. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.tactile.tact.intune), [App Store link (iOS)](https://apps.apple.com/us/app/tact-for-intune/id1477117416?mt=8)  |  
| **Vera for Intune**<p><img alt="Partner app - Vera for Intune icon" src="./media/apps-supported-intune-apps/icon-p-vera.png" width="100"> | Encrypt, track, and revoke access to files and email attachments directly from your mobile device with Vera for Intune. Protect your most valuable information, no matter what apps you use: Microsoft, Box, Google, Dropbox, and more. | [App Store link (iOS)](https://itunes.apple.com/us/app/vera-for-intune/id1235182010?mt=8) |  
| **Workspace ONE Send**<p><img alt="Partner app - Intune partner app - Workspace ONE Send icon" src="./media/apps-supported-intune-apps/icon-p-workspace-one-send-icon.png" width="100"> | Workspace ONE Send provides seamless editing and sending capabilities for customers using Microsoft Intune to manage Microsoft 365 apps using VMware productivity apps. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=com.airwatch.vmsend),<br>[App Store link (iOS)](https://itunes.apple.com/us/app/vmware-workspace-one-send/id1336333505?mt=8) |
| **Zero for Intune**<p><img alt="Partner app - Zero for Intune icon" src="./media/apps-supported-intune-apps/icon-p-zero.png" width="100"> | The ZERØ for Intune application is specifically designed for MDM deployment via Microsoft Intune. This app allows both ZERØ and Microsoft Intune customers to take advantage of a secure Intune MDM deployment, as well as organize and protect BYOD environments with mobile application management (MAM). | [App Store link (iOS)](https://apps.apple.com/app/zero-for-intune/id1508485761) |  
| **Zoom for Intune**<p><img alt="Partner app - Zoom for Intune icon" src="./media/apps-supported-intune-apps/icon-p-zoom.png" width="100"> | Zoom is your communications hub for meetings, webinars, chat and cloud phone. Start or join meetings with flawless video, crystal clear audio and instant screen sharing from desktop, mobile or conference rooms. | [Google Play link (Android)](https://play.google.com/store/apps/details?id=us.zoom.videomeetings4intune),<br>[App Store link (iOS)](https://apps.apple.com/us/app/zoom-for-intune/id1462818858?mt=8) |  

## Next steps

To learn how to add apps for each platform to Intune, see:

- [Android store apps](store-apps-android.md)
- [Android LOB apps](lob-apps-android.md)
- [iOS store apps](store-apps-ios.md)
- [iOS LOB apps](lob-apps-ios.md)
- [Web apps (for all platforms)](web-app.md)
- [Microsoft store apps](store-apps-windows.md)
- [Windows LOB app](lob-apps-windows.md)
- [Microsoft 365 apps for Windows 10](apps-add-office365.md)
- [Microsoft 365 apps for macOS](apps-add-office365-macos.md)
- [Built-in apps](apps-add-built-in.md)
- [Win32 apps](app-management.md)
