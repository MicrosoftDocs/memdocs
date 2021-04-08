---
title: "Console extension registration through community hub"
description: "Register a console extension through community hub"
titleSuffix: "Configuration Manager"
ms.date: "03/19/2021"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d15d00a9-a77a-4916-88c6-0ac04234fc1e
author: mestew
ms.author: mstewart
manager: dougeby
---

# Console extension registration though community hub
<!--9526630, 3555909-->
Starting in Configuration Manager version 2103, the [community hub](../../../../core/servers/manage/community-hub.md) supports console extensions. Console extension authors can contribute extensions they've written to the community hub. Community hub users can download the extensions and manage the installation of them across their Configuration Manager hierarchy. Contributing extensions through community hub supersedes the [previous deployment process](console-extension-deployment.md).

## Prerequisites

 To register a console extension in the community hub for Configuration Manager admins to download, you'll need the following prerequisites:

- Configuration Manager version 2103, or later
- Meet all of the prerequisites for [contributing to community hub](../../../../core/servers/manage/community-hub-contribute.md)
- Configuration Manager **Full Administrator** with **All** scope rights.

- A [valid payload](#bkmk_cab) in an authenticode-signed `.cab` file once you're ready to publish. Your `.cab` file must contain the following items:
   - A manifest file named `manifest.xml`
   - The author and [version](/dotnet/api/system.version) of the extension must be listed in the `manifest.xml`
   - All relevant files for the extension must be in the `.cab` file
     - Each file must be listed in the manifest and have the correct name and SHA256 hash

## <a name="bkmk_create"></a> Create an extension

Creating your extension for community hub isn't much different from how it was done previously. However, there's no longer a need to install the files in their respective `%ProgramFiles%\Microsoft Endpoint Manager\AdminConsole\XmlStorage\Extensions` folder. This is part of the function of the new `manifest.xml` file. You can still create the following items:
- [Actions](configuration-manager-actions.md)
- [Forms](about-configuration-manager-console-forms.md)
- [Management classes](about-configuration-manager-console-management-classes.md)
- [Nodes](about-configuration-manager-console-nodes.md)
- [Views](about-configuration-manager-console-views.md)
- Integrate your own custom wizards into the Configuration Manager console by using a wizard framework of your choice
   - You can't create wizards by using the existing Configuration Manager console framework.
   - You can't modify or remove steps from the existing Configuration Manager wizards.

> [!TIP]
> From community hub's GitHub repository, you can download [a sample extension's cab file](https://github.com/microsoft/configmgr-hub/blob/master/objects/ConsoleExtensionCab/AllStatusMessageForTsDeployment.cab).

## <a name="bkmk_cab"></a> Create a valid payload cab file

Once you have the files for your extension created, you'll create the `manifest.xml` file, then package them all together in an authenticode-signed `.cab` file.

- A valid payload in an authenticode-signed `.cab` file. Your `.cab` file must contain the following items:
   - A manifest file named `manifest.xml`
   - The author and [version](/dotnet/api/system.version) of the extension must be listed in the `manifest.xml`
   - All relevant files for the extension must be in the `.cab` file
     - Each file must be listed in the manifest and have the correct name and SHA256 hash

Manifest.xml format:

```xml
<CustomExtensionManifest ExtensionID="{A GUID to identify this extension}" Name="{Name of the extension to be shown in the Console Extension node}" Description="{Description of the extension to be shown in the Console Extension node" Version="{The version of the extension to be shown in the Console Extension node. For example:1.0}" Author="{The author of the extension to be shown in the Console Extension node}">
	<Deployments>
		<ActionExtensionDeployment ParentNode="{the GUID that identify the folder/node you want to place the action under}">
			<FileList>
				<File Name="{The name of the xml file that defines the action. For example: MyAction.xml}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
			</FileList>
		</ActionExtensionDeployment>
		<NodeExtensionDeployment ParentNode="{the GUID that identify the folder you want to place the node under}">
			<FileList>
				<File Name="{The name of the xml file that defines the node. For example: MyNode.xml}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
			</FileList>
		</NodeExtensionDeployment>
		<FormExtensionDeployment>
			<FileList>
				<File Name="{The name of the xml file that defines the form. For example: MyForm.xml}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
				<File Name="{The name of the dll file that defines the form. For example: MyForm.dll}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
			</FileList>
		</FormExtensionDeployment>
		<ManagementClassExtensionDeployment>
			<FileList>
				<File Name="{The name of the xml file that defines the WMI class. For example: MyClass.xml}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
				<File Name="{The name of the dll file that defines the WMI class. For example: MyClass.dll}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
			</FileList>
		</ManagementClassExtensionDeployment>
		<ViewExtensionDeployment>
			<FileList>
				<File Name="{The name of the dll file that defines the view. For example: MyView.dll}">
					<Hash Algorithm="sha256">{The SHA256 hash of this file}</Hash>
				</File>
			</FileList>
		</ViewExtensionDeployment>
	</Deployments>
</CustomExtensionManifest>
```

Example manifest.xml file:

```xml
<CustomExtensionManifest ExtensionID="808b9ce3-e574-49be-82be-64ed35d800c5" Name="Nice Console Node and Console Action Extension" Description="Very Useful Extension" Version="1.1" Author="Me">
	<Deployments>
		<NodeExtensionDeployment ParentNode="d61498cb-7b3f-4748-ae3e-026674fb0cbd">
			<FileList>
				<File Name="Test.xml">
					<Hash Algorithm="sha256">543F2947AEA734B6833F275091AC6A159C0FCD341373D6E53062E37281B602B3</Hash>
				</File>
			</FileList>
		</NodeExtensionDeployment>
      <ActionExtensionDeployment ParentNode="172d85e7-bb7a-4479-a6a2-768f175b75cb">
        <FileList>
          <File Name="Test2.xml">
            <Hash Algorithm="sha256">C60FB69B86BF9B2E924FF272292CA2C97864D636B8190C95DC926049651A002E</Hash>
          </File>
        </FileList>
      </ActionExtensionDeployment>
	</Deployments>
</CustomExtensionManifest>
```

## <a name="bkmk_test"></a> Register the extension to a site for testing

When you have your extension built and packaged into an authenticode-signed `.cab` file, you can test it in a Configuration Manager lab environment. You'll do this by posting it through the [administration service](../../../adminservice/usage.md). Once the extension is inserted into the site, you can approve it and install it locally from the **Console Extensions** node.

1. Run the following PowerShell script after editing the `$adminServiceProvider` and `$cabFilePath`: 
   - `$adminServiceProvider` - The top-level SMSProvider server where the administration service is installed
   - `$cabFilePath` - Path to the extension's authenticode-signed `.cab` file
 
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

1. In the Configuration Manager console, go to **Administration** >  **Overview** > **Updates and Servicing** > **Console Extensions**.
1. Select your extension, then choose **Approve Installation**.
1. To install the extension on the current console, select **Install** under **Local Extension**.
1. Rerunning the PowerShell script with the same extension and the same version will overwrite the current existing one.

## Share your extension on community hub

Make sure you've joined the community hub and that you've accepted the invite after your join request is approved. You contribute extensions the same way you would any other community hub object. For more information, see [Contribute to community hub](../../../../core/servers/manage/community-hub-contribute.md).

## Next steps

- [Contribute to community hub](../../../../core/servers/manage/community-hub-contribute.md)
- [Use the community hub](../../../../core/servers/manage/community-hub.md)