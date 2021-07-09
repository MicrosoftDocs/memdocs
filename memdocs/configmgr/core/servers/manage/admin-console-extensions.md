---
title: Console extensions for Configuration Manager
titleSuffix: Configuration Manager
description: Learn about managing Configuration Manager console extensions
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dfda09bc-5eca-4fb6-9064-4e51705cfe58
author: mestew
ms.author: mstewart
manager: dougeby
---

# Manage Configuration Manager console extensions

*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager 2103, the **Console extensions** node allows you to start managing the approval and installation of console extensions used in your environment. Having extensions in the console doesn't make them immediately available. First, an administrator has to approve the extension for the site and enable notifications. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](#bkmk_notification). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

The new style of console extensions have the following benefits:

1. Centralized management of console extensions for the site from the console instead of manually placing binaries on individual consoles.
1. A clear separation of console extensions from different extension providers.
1. The ability for admins to have more control over which console extensions are loaded and used in the environment, to keep them more secure.
1. A hierarchy setting that allows for only using the new style of console extension.
   > [!Important]
   > If this setting is used, your old style extensions that aren't approved through the **Console Extensions** node will no longer be able to be used. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](updates.md#bkmk_Baselines). The setting remains `disabled` by default, if you upgraded from a version prior to 2103. If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

The old style of console extensions may start being phased out in favor of the new style, which is more secure and centrally managed.

[!INCLUDE [console extensions node](includes/console-extensions-node.md)]

## <a name="bkmk_notification"></a> Console extension installation notifications
<!--3555909-->
[!INCLUDE [console extensions notifications](includes/console-extensions-notifications.md)]

## <a name="bkmk_unsigned"></a> Import unsigned console extensions for hierarchy approval
<!--9761129-->
(*Applies to Configuration Manager version 2107 or later*)

Starting in Configuration Manager version 2107 , you can choose to allow unsigned hierarchy approved console extensions. You may need to allow unsigned console extensions due to an unsigned internally developed extension, or for testing your own custom extension in a lab. To import and install an unsigned hierarchy approved console extension, the high-level steps are:

   1. [Allow unsigned](#bkmk_allow-unsigned) hierarchy approved console extensions.
   1. [Import](#bkmk_import-unsigned) the unsigned console extension.
   1. [Test](#bkmk_local_install) the the unsigned console extension in a local console.
   1. [Enable notifications](#bkmk_enable-notifications) to allow console users to install the unsigned console extension.

### <a name="bkmk_allow-unsigned"></a> Allow unsigned hierarchy approved console extensions

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**.
1. Select **Hierarchy Settings** from the ribbon.
1. On the **General** tab, enable the **Hierarchy approved console extensions can be unsigned** option.
1. Select **Ok** when done to close the **Hierarchy Settings Properties**.

### <a name="bkmk_import-unsigned"></a> Import the unsigned console extension

When you have the `.cab` file for an extension, you can test it in a Configuration Manager lab environment. You'll do this by posting it through the [administration service](../../../develop/adminservice/usage.md). Once the extension is inserted into the site, you can approve it and install it locally from the **Console Extensions** node.

Run the following PowerShell script after editing the `$adminServiceProvider` and `$cabFilePath`:
   - `$adminServiceProvider` - The top-level SMSProvider server where the administration service is installed
   - `$cabFilePath` - Path to the extension's  `.cab` file

```powershell
$adminServiceProvider = "SMSProviderServer.contoso.com"
$cabFilePath = "C:\Testing\MyExtension.cab"
$adminServiceURL = "https://$adminServiceProvider/AdminService/v1/ConsoleExtensionMetadata/AdminService.UploadExtension"
$cabFileName = (Get-Item -Path $cabFilePath).Name
$Data = Get-Content $cabFilePath
$Bytes = [System.IO.File]::ReadAllBytes($cabFilePath)
$base64Content = [Convert]::ToBase64String($Bytes)
$Headers = @{
    "Content-Type" = "Application/json"
}
$Body = @{
            CabFile = @{
                FileName = $cabFileName
                FileContent = $base64Content
            }
            AllowUnsigned = $true
        } | ConvertTo-Json
$result = Invoke-WebRequest -Method Post -Uri $adminServiceURL -Body $Body -Headers $Headers -UseDefaultCredentials
if ($result.StatusCode -eq 200) {Write-Host "$cabFileName was published successfully."}
else {Write-Host "$cabFileName publish failed. Review AdminService.log for more information."}
```

## Next steps

- [Console tips](admin-console-tips.md)
- [Configuration Manager console notifications](admin-console-notifications.md)
