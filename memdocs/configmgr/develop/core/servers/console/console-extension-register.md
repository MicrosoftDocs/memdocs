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
<!--9526630-->
The [community hub](../../../../core/servers/manage/community-hub.md) supports sharing extensions to the Configuration Manager console. To register a console extension in the community hub for Configuration Manager admins to download, you'll need the following:

- Meet all of the prerequisites for [contributing to community hub](../../../../core/servers/manage/community-hub-contribute.md)
- A valid payload in an authenticode-signed `.cab` file. Your `.cab` file must contain the following:
   - A manifest file named `manifest.xml`
   - The author and version of the extension must be listed in the `manifest.xml`
   - All relevant files for the extension must be in the `.cab` file
     - Each file must be listed in the manifest and have the correct name and SHA256 hash


## Register the extension to a site for testing

1. Craft the `json` to be used in the body of the HTTP request

```json
{
CabFile:{
FileName:"[cab file name that has suffix .cab]",
FileContent:"[Base64 encoded string of cab file's content (See the section below for how to create this cab)]",                
}
}
```

1. Make a HTTP request to the [administration service](../../../adminservice/usage.md).

```http
verb: HTTP post
uri: https://[YourProviderMachineName]/AdminService/v1/ConsoleExtensionMetadata/AdminService.UploadExtension
body: the json string above
requester: the super admin's context

```
<!--

When you get an extension from the hub, it's available in the **Console extensions** node in the console. Getting an extension from the hub doesn't make it immediately available. First, an administrator has to approve the extension for the site. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](../../../../servers/manage/community-hub.md#bkmk_hub_os). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

## Prerequisites
To register a console extension for download in community hub, you'll need to meet all fo the prerequisites for [contributing to community hub](../../../../core/servers/manage/community-hub-contribute.md)

-->