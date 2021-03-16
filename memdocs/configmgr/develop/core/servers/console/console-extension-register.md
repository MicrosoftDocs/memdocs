---
title: "Console extension registration for community hub"
titleSuffix: "Configuration Manager"
ms.date: "03/26/2021"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d15d00a9-a77a-4916-88c6-0ac04234fc1e
author: mestew
ms.author: mstewart
manager: dougeby
---

# Console extension registration for community hub
<!--9526630, 3555909-->
The [community hub](../../../../core/servers/manage/community-hub.md) supports sharing extensions to the Configuration Manager console. To register a console extension in the community hub for Configuration Manager admins to download, you'll need the following:

- Meet all of the prerequisites for [contributing to community hub](../../../../core/servers/manage/community-hub-contribute.md)
- A valid payload in an authenticode-signed `.cab` file. Your `.cab` file must contain the following:
   - A manifest file named `manifest.xml`
   - The author and [version](/dotnet/api/system.version) of the extension must be listed in the `manifest.xml`
   - All relevant files for the extension must be in the `.cab` file
     - Each file must be listed in the manifest and have the correct name and SHA256 hash

## <a name="bkmk_create"></a> Create an extension

Creating your extension for community hub isn't much different from how it was done previously. However, there is no longer a need to install the files in their respective `%ProgramFiles%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\Extensions` folder. This is part of the function of the new `manifest.xml` file. You can still create the following items:
- [Actions](configuration-manager-actions.md)
- [Forms](about-configuration-manager-console-forms.md)
- [Management classes](about-configuration-manager-console-management-classes.md)
- [Nodes](about-configuration-manager-console-nodes.md)
- [Views](about-configuration-manager-console-views.md)
- Integrate your own custom wizards into the Configuration Manager console by using a wizard framework of your choice
   - You can't create wizards by using the existing Configuration Manager console framework.
   - You can't modify or remove steps from the existing Configuration Manager wizards.


## <a name="bkmk_cab"></a> Create a valid payload cab file

- A valid payload in an authenticode-signed `.cab` file. Your `.cab` file must contain the following:
   - A manifest file named `manifest.xml`
   - The author and [version](/dotnet/api/system.version) of the extension must be listed in the `manifest.xml`
   - All relevant files for the extension must be in the `.cab` file
     - Each file must be listed in the manifest and have the correct name and SHA256 hash

Sample xml file:

```xml
<CustomExtensionManifest ExtensionID="{A GUID to identify this extension}" Name="{Name of the extension to be shown in the Console Extension node}" Description="{Description of the extension to be shown in the Console Extension node" Version="{The version of the extension to be shown in the Console Extension node. For example:1.0}" Author="{The author of the extension to be shown in the Console Extension node}">
   <Deployments>
     <ActionExtensionDeployment ParentNode="{the GUID that identify the folder/node you want to place the action under}">
       <FileList>
         <File Name="{The name of the xml file that defines the action. For example: MyAction.xml}">
           <Hash Algorithm="sha256">{The sha256 of this file}</Hash>
         </File>
       </FileList>
     </ActionExtensionDeployment>
     <NodeExtensionDeployment ParentNode="{the GUID that identify the folder you want to place the node under}">
       <FileList>
         <File Name="{The name of the xml file that defines the node. For example: MyNode.xml}">
           <Hash Algorithm="sha256">{The sha256 of this file}</Hash>
         </File>
       </FileList>
     </NodeExtensionDeployment>
     <FormExtensionDeployment>
       <FileList>
         <File Name="{The name of the xml file that defines the form. For example: MyForm.xml}">
           <Hash Algorithm="sha256">{The sha256 of this file}</Hash>
         </File>
         <File Name="{The name of the dll file that defines the form. For example: MyForm.dll}">
           <Hash Algorithm="sha256">{The sha256 of this file}</Hash>
         </File>
       </FileList>
     </FormExtensionDeployment>
<ManagementClassExtensionDeployment>
<FileList>
<File Name="{The name of the xml file that defines the wmi class. For example: MyClass.xml}">
<Hash Algorithm="sha256">{The sha256 of this file}</Hash>
</File>
<File Name="{The name of the dll file that defines the wmi class. For example: MyClass.dll}">
<Hash Algorithm="sha256">{The sha256 of this file}</Hash>
</File>
</FileList>
</ManagementClassExtensionDeployment>
<ViewExtensionDeployment>
<FileList>
<File Name="{The name of the dll file that defines the view. For example: MyView.dll}">
<Hash Algorithm="sha256">{The sha256 of this file}</Hash>
</File>
</FileList>
</ViewExtensionDeployment>
</Deployments>
</CustomExtensionManifest>
```

## <a name="bkmk_test"></a> Register the extension to a site for testing

When you have your extension built, you'll want to test it in a Configuration Manager environment. You'll do this by sending it through the [administration service](../../../adminservice/usage.md).


```powershell
$adminServiceURL = "https://server.contoso.com/AdminService/v1/ConsoleExtensionMetadata/AdminService.UploadExtension"
$cabFilePath = "C:\Testing\MyExtension.cab"

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

Invoke-RestMethod -Method Post -Uri "$($adminServiceURL)" -Body $Body -Headers $Headers -UseDefaultCredentials | Out-Null
```

Take 2 

```powershell
$adminServiceProvider = "server.contoso.com"
$cabFilePath = "C:\Testing\MyExtension.cab"
$adminServiceURL = "https://$adminServiceProvider/AdminService/v1/ConsoleExtensionMetadata/AdminService.UploadExtension"
$cabFileName = (Get-Item -Path $cabFilePath).Name
$Data = Get-Content $cabFilePath
$Bytes = [System.IO.File]::ReadAllBytes($cabFilePath)
$base64Content = [Convert]::ToBase64String($Bytes)
$Headers = @{​​​​​
    "Content-Type" = "Application/json"
}​​​​​
$Body = @{​​​​​
            CabFile = @{​​​​​
                FileName = $cabFileName
                FileContent = $base64Content
            }​​​​​
        }​​​​​ | ConvertTo-Json
$result = Invoke-WebRequest -Method Post -Uri $adminServiceURL -Body $Body -Headers $Headers -UseDefaultCredentials
if ($result.StatusCode -eq 200) {​​​​​Write-Host "$cabFileName was published successfully."}​​​​​ 
else {​​​​​Write-Host "$cabFileName upload failed. Please review AdminService.log for more information."}​​​​​
```


<!--

When you get an extension from the hub, it's available in the **Console extensions** node in the console. Getting an extension from the hub doesn't make it immediately available. First, an administrator has to approve the extension for the site. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](../../../../servers/manage/community-hub.md#bkmk_hub_os). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

## Prerequisites
To register a console extension for download in community hub, you'll need to meet all fo the prerequisites for [contributing to community hub](../../../../core/servers/manage/community-hub-contribute.md)

-->