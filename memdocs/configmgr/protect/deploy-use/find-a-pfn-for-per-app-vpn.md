---
title: Find a package family name (PFN) for per-app VPN
titleSuffix: Configuration Manager
description: Learn about the two ways to find a package family name so that you can configure a per-app VPN.
ms.date: 03/29/2022
ms.service: configuration-manager
ms.subservice: protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Find a package family name (PFN) for per-app VPN

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in version 2203, this company resource access feature is no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](../plan-design/resource-access-deprecation-faq.yml).

There are two ways to find a PFN so that you can configure a per-app VPN.

## Find a PFN for an app that's installed on a Windows 10 computer

If the app you're working with is already installed on a Windows 10 computer, you can use the [Get-AppxPackage](/powershell/module/appx/get-appxpackage) PowerShell cmdlet to get the PFN.

The syntax for Get-AppxPackage is:

``` Syntax
Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]
```

> [!NOTE]
> You may have to run PowerShell as an admin in order to retrieve the PFN

For example, to get info on all the universal apps installed on the computer use `Get-AppxPackage`.

To get info on an app you know the name of, or part of the name of, use `Get-AppxPackage *<app_name>`. Note the use of the wildcard character, particularly helpful if you're not sure of the full name of the app. For example to get the info for OneNote, use `Get-AppxPackage *OneNote`.


Here's the information retrieved for OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## Find a PFN if the app is not installed on a computer

1. Go to https://www.microsoft.com/store/apps
2. Enter the name of the app in the search bar. In our example, search for OneNote.
3. Click the link to the app. The URL that you access has a series of letters at the end. In our example, the URL looks like this:
`https://www.microsoft.com/store/apps/onenote/9wzdncrfhvjl`
4. In a different tab, paste the following URL, `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`,  replacing `<app id>` with the app ID you obtained from https://www.microsoft.com/store/apps - that series of letters at the end of the URL in step 3. In our example, example of OneNote, you'd paste: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

In Microsoft Edge, the information you want is displayed; in Internet Explorer, click **Open** to see the information. The PFN value is given on the first line. Here's how the results look for our example:

``` JSON
{
  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",
  "packageIdentityName": "Microsoft.Office.OneNote",
  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",
  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
}
```