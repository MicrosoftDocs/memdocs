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
For users to be productive on their Windows 365 Cloud PC, it's important that Windows be presented to the user in a language in which they are comfortable. Though users always have the ability to change the display language themselves through the time and language settings in Windows, the Windows experience is more welcoming if the user experiences the desired language immediately, starting when they first sign in.

To provide a localized Windows experience when users first sign in, there are two steps:
1. [Create a custom device image with the languages installed](#create-a-custom-image-with-the-languages-installed).
2. [Configure the default language using group policy](#configure-the-default-language-using-group-policy). 

Cloud PCs provisioned from this image will be fully configured to work in any of the installed languages, without any user action. When the user signs in to the Cloud PC, group policy will evaluate and the device set the appropriate pre-installed language as the user's preferred language for Windows. 

## Create a custom image with the languages installed
Creating a custom image with the languages installed is the best way to ensure that the desired languages are available on the Cloud PCs when the user signs in.

### Add languages to Windows and capture the image
Follow the steps in [Add language packs to a Windows 10 multi-session image](/azure/virtual-desktop/language-packs) up to and including [finish customizing your image](/azure/virtual-desktop/language-packs#finish-customizing-your-image) to install the desired languages to your Windows 10 Enterprise custom image.

> [!NOTE]
> Though these instructions are written specifically for Windows 10 Enterprise multi-session, these same steps apply to Windows 10 Enterprise.

### Upload the custom image
Once you have captured the image as an Azure managed image, follow the steps in [Add or delete device images](add-device-images.md) to upload the custom image to the Windows 365 service.

## Configure the default language using group policy
Now that the languages are installed on the image that users will receive, you need to create a group policy to apply the correct pre-installed language as the default for your users when they sign in to their Cloud PC.

1. Create a security group in your Active Directory domain that will map a specific language to a specific set of users.
2. Add all Cloud PC users to this new security group who should receive that language.
3. In Server Manager, open **Group Policy Management** and create a new group policy object linked to the Organization Unit (OU) or domain that will contain the Cloud PCs for those users.
4. Right-click the new group policy object, and select **Edit...**
5. Navigate to **User Configuration** > **Preferences** > **Windows Settings**, right-click **Registry**, and select **New** > **Registry Item**.
6. Enter the following details in the **General** tab. Here is an example that shows Spanish (Spain) with language code es-ES:
    - Action: Replace
    - Hive: HKEY_CURRENT_USER
    - Key Path: ControlPanel\Desktop
    - Value name: PreferreUILanguages
    - Value type: REG_SZ
    - Value data: [Language code].
        !Note: To find the language code for your desired language and region combination, see (link).
7. Switch to the **Common** tab and check the following three options:
    - **Run in logged-on user's security context (user policy option)**
    - **Apply once and do not reapply**
    - **Item-level targeting**
8. Select **Targeting...**, **New Item**, and **Security Group**.
9. Select **...** next to the Group, search for the new security group, select the new security group, and hit **OK**.
10. Select **User in group**, then select **OK** and **OK** to complete the new registry process.
11. In the "Group Policy Management Editor", navigate to **User Configuration** > **Preferences** > **Windows Settings**, right-click **Regional Options**, and select **New** > **Regional Options**.
12. Switch to the **Common** tab and check the following three options:
    - **Run in logged-on user's security context (user policy option).**
    - **Apply once and do not reapply.**
    - **Item-level targeting.**
13. Select **Targeting..**, **New Item**, and **Security Group**.
14. Select **...** next to the Group, search for the new security group, select the new security group, and hit **OK**.
15. Select **User in group**, then select **OK** and **OK** to complete the new registry process.

You can perform these steps for each language you need to provide as the default language for users. If your users have both Cloud PCs and physical devices, you may want to apply [group policy loopback](/troubleshoot/windows-server/group-policy/loopback-processing-of-group-policy) so these settings only affect users when they sign in to ther Cloud PC.

> [!NOTE]
> Step 6 above uses the "Replace" command, setting the user's preferred language to just the one language defined in the registry item. If you create multiple group policies to assign different languages to users, make sure users are only targeted by a single group policy object.

## Next steps
[Create a provisioning policy](create-provisioning-policy.md)
