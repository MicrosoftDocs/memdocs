---
title: Import admin console extensions for Configuration Manager
titleSuffix: Configuration Manager
description: Learn about importing Configuration Manager console extensions
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Import Configuration Manager console extensions

*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager 2103, you can import console extensions to be used in your environment. These extensions show up under the **Console extensions** node. Importing and just having extensions in the console doesn't make them immediately available. An administrator still has to approve the extension for the site and enable notifications. Then console users can install the extension to their local console. For more information about managing and installing console extensions, see [Manage Configuration Manager console extensions](admin-console-extensions.md).

Based on the version of Configuration Manager you're running, different import options are available. Initially, only signed extensions could be imported through the administration service. Support for importing unsigned extensions was added later. Then a wizard that could import both signed and unsigned extensions for you without having to run a script was introduced in version 2111.  


|Configuration Manager version| 2103| 2107 | 2111 or later|
|---|---|---|---|
|Import a signed extension| Yes | Yes | Yes |
|Import an unsigned extension| No | Yes, when you [allow unsigned](#bkmk_allow-unsigned) | Yes, when you [allow unsigned](#bkmk_allow-unsigned)|
|Import from the [administration service](../../../develop/adminservice/usage.md) with a PowerShell script| Yes, signed extensions only | Yes | Yes | 
|Import from the **Import Console Extension** wizard | No | No | Yes|

## How to import console extensions

To import console extensions, you'll follow four basic steps. Exactly how you can import will be determined by the version of Configuration Manager you're using and if the extension is signed or not. To import and install a hierarchy approved console extension, the high-level steps are:

1. Determine if you need to [allow unsigned](#bkmk_allow-unsigned) hierarchy approved console extensions (version 2107 and later).
1. Import the console extension using one of the following methods:
    - [Import a signed console extension with a script](#bkmk_signed_admin) (version 2103 and later)
    - [Import an unsigned console extension with a script](#bkmk_unsigned_admin) (version 2107 and later)
    - [Use the **Import Console Extension** wizard](#bkmk_wizard) (version 2111 and later)
1. [Test the extension](#bkmk_local_install) in a local console.
1. [Enable notifications](#bkmk_enable-notifications) to allow console users to install the console extension.

[!INCLUDE [Allow unsigned console extensions notifications](includes/console-extensions-allow-unsigned.md)]

## <a name="bkmk_signed_admin"></a> Import a signed console extension with a script

(*Applies to Configuration Manager version 2103 or later*)

When you have an extension packaged in a signed `.cab` file, you can import it into Configuration Manager. You'll do this by posting it through the [administration service](../../../develop/adminservice/usage.md) using a PowerShell script. Once the extension is inserted into the site, you can approve and install it locally from the **Console Extensions** node. To import, run the following PowerShell script after editing the `$adminServiceProvider` and `$cabFilePath`:

   - `$adminServiceProvider` - The top-level SMSProvider server where the administration service is installed
   - `$cabFilePath` - Path to the extension's signed `.cab` file
 
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
            } | ConvertTo-Json
    
    $result = Invoke-WebRequest -Method Post -Uri $adminServiceURL -Body $Body -Headers $Headers -UseDefaultCredentials
    
if ($result.StatusCode -eq 200) {Write-Host "$cabFileName was published successfully."}
else {Write-Host "$cabFileName publish failed. Review AdminService.log for more information."}
```

## <a name="bkmk_unsigned_admin"></a> Import an unsigned console extension with a script
<!--9761129-->
(*Applies to Configuration Manager version 2107 or later*)

Starting in Configuration Manager version 2107, you can choose to allow unsigned hierarchy approved console extensions. It's a best practice to always used signed extensions to minimize security risks and to confirm the authenticity of a console extension. However, in some cases you may need to allow unsigned console extensions due to an unsigned internally developed extension, or for testing your own custom extension in a lab.

When you have the `.cab` file for an extension, you can test it in a Configuration Manager lab environment. You'll do this by posting it through the [administration service](../../../develop/adminservice/usage.md). Once the extension is inserted into the site, you can approve it and install it locally from the **Console Extensions** node. To import, run the following PowerShell script after editing the `$adminServiceProvider` and `$cabFilePath`:

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

> [!NOTE]
> Currently, when an unsigned extension isn't [enabled for user notification](#bkmk_enable-notifications), in the **Console Extensions** node, the **Required** column remains blank instead of populating a value of **No**. <!--10349053, 10401804 -->

## <a name="bkmk_wizard"></a> Import console extensions wizard
<!--9741121, 9761129-->
(*Applies to Configuration Manager version 2111 or later*)

Starting in version 2111, you can use the **Import Console Extension** wizard to import [console extensions](admin-console-extensions.md) that are managed for the hierarchy. You no longer need to use a PowerShell script to import a signed or unsigned console extension. To import a console extension using the wizard:

1. From the **Administration** workspace, expand **Updates and Servicing**, then select the **Console Extensions** node.
1. Select **Import Console Extension** from either the ribbon or the right-click menu.
1. When the wizard launches, select **Browse** and navigate to the extension's cab file.
1. If needed, select the option for **Allow extension to be unsigned**.
1. Select **Next** to review the import summary, then complete the wizard to import the extension.

> [!Note] 
> To import unsigned extensions, the **Hierarchy approved console extensions can be unsigned** option needs to be enabled in the **Hierarchy Settings**. For more information, see [Allow unsigned hierarchy approved console extensions](#bkmk_allow-unsigned).


[!INCLUDE [console extensions local install](includes/console-extensions-local-install.md)]

[!INCLUDE [console extensions enable notification](includes/console-extensions-enable-notification.md)]

## Next steps

 - [Manage console extensions](admin-console-extensions.md)
 - [Console extensions from Community hub](community-hub-extensions.md)
 - [Develop custom console extensions](../../../develop/core/servers/console/console-extension-register.md)
