---
# required metadata
title: Provide users a localized Windows experience
titleSuffix:
description: Learn how to provide a localized Windows experience for your users.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/05/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---
# Provide users a localized Windows experience
For users to be productive on their Windows 365 Cloud PC, it's important that Windows be presented to the user in a language in which they are comfortable. Though users always have the ability to change the display language themselves through the time and language settings in Windows, the Windows experience is more welcoming if the user experiences the desired language immediately, starting with their first logon.

To provide a localized Windows experience starting at first logon, there are two steps:
- [Create a custom device image with the languages installed](#create-a-custom-image-with-the-languages-installed).
- [Configure the default language using group policy](#configure-the-default-language-using-group-policy). 

Cloud PCs provisioned from this image will be fully configured to work in any of the installed languages, without any user action. When the user logs in to the Cloud PC, group policy will evaluate and the device set the appropriate pre-installed language as the user's preferred language for Windows. 

## Create a custom image with the languages installed
Creating a custom image with the languages installed is the best way to ensure that the desired languages are available on the Cloud PCs when the user logs in.

### Add languages to Windows and capture the image
Follow the steps in [Add language packs to a Windows 10 multi-session image](https://docs.microsoft.com/azure/virtual-desktop/language-packs) to install the desired languages to your Windows 10 Enterprise custom image.

Note:
- Though these instructions are wrriten for Windows 10 Enterprise multi-session, these same steps apply to Windows 10 Enterprise, which Windows 365 supports.
- Follow all of the steps up and through [Finish customizing your image](https://docs.microsoft.com/azure/virtual-desktop/language-packs#finish-customizing-your-image).

### Upload the custom image
Once you have captured the image as an Azure managed image, follow the steps in [Add or delete device images](add-device-images.md) to upload the custom image to the Windows 365 service.

## Configure the default language using group policy
Now that the languages are installed on the image that users will receive, you need to create a group policy to apply the correct pre-installed language as the default for your users when they sign in to their Cloud PC.

1. Create a security group per language in your Active Directory domain.
2. Add all users of the respective language to the group as members.
3. Link the GPO to the Organizational Unit (OU) or the domain that will contain your users' Cloud PC devices.
4. Adjust the item-level targeting setting for the Group Policy Preference settings with the group names from Step 1.
5. Enable loopback processing in merge mode in a higher ranking GPO linked to the OU or domain for the Cloud PCs devices.
6. Close the Group Policy Editor

## Next steps
[Create a provisioning policy](create-provisioning-policy.md)