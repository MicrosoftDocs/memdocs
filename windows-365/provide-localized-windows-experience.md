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

# Custom device image

## Add languages to Windows


## Configure the default language using group policy
Now that the languages are installed on the custom image, you need to create a group policy to apply the correct pre-installed language to each user's Cloud PC on login.

1. Create a security group per language in your Active Directory domain.
2. Add all users of the respective language to the group as members.
3. Link the GPO to the Organizational Unit (OU) or the domain that will contain your users' Cloud PC devices.
4. Adjust the item-level targeting setting for the Group Policy Preference settings with the group names from Step 1.
5. Enable loopback processing in merge mode in a higher ranking GPO linked to the OU or domain for the Cloud PCs devices.
6. Close the Group Policy Editor


## Capture the image


## Upload the custom image
Once you are done creating the custom image in your Azure subscription, follow the steps in [Add or delete device images](add-device-images.md) to upload the custom image to the Windows 365 service.
