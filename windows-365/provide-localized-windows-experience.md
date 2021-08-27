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
For users to be productive on their Windows 365 Cloud PC, it's important that Windows be presented to the user in a language in which they are comfortable. Though users always have the ability to change the display language themselves through the Settings app in Windows, the Windows experience is more welcoming if the user experiences the desired language immediately, starting when they first sign in.

To provide a localized Windows experience when users first sign in, there are two steps:
1. [Create a custom device image with the languages installed](#create-a-custom-image-with-the-languages-installed).
2. [Configure the default language using Group Policy](#configure-the-default-language-using-group-policy). 

Cloud PCs provisioned from this image will be fully configured to work in any of the installed languages, without any user action. When the user signs in to the Cloud PC, Group Policy will evaluate and the device set the appropriate pre-installed language as the user's preferred language for Windows. 

## Create a custom image with the languages installed
Creating a custom image with the languages installed is the best way to ensure that the desired languages are available on the Cloud PCs when the user signs in.

### Add languages to Windows and capture the image
Follow the steps in [Add language packs to a Windows 10 multi-session image](/azure/virtual-desktop/language-packs) up to and including [finish customizing your image](/azure/virtual-desktop/language-packs#finish-customizing-your-image) to install the desired languages to your Windows 10 Enterprise custom image.

> [!NOTE]
> Though these instructions are written specifically for Windows 10 Enterprise multi-session, these same steps apply to Windows 10 Enterprise.

### Upload the custom image
Once you have captured the image as an Azure managed image, follow the steps in [Add or delete device images](add-device-images.md) to upload the custom image to the Windows 365 service.

## Configure the default language using Group Policy
Now that the languages are installed on the image that users will receive, you need to create a Group Policy to apply the correct pre-installed language as the default for your users when they sign in for the first time to their Cloud PC. 

The following steps configure [Group Policy Preferences](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn581922(v=ws.11)) to set the PreferredUILanguages Registy value and the Windows Regional Options. These options are then [targeted by security group](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn581922(v=ws.11)#item-level-targeting) to sets of users. Each security group and Group Policy object configures a single language as default for those users. You can use a single image with multiple languages and different Group Policy objects targeted to different groups of users to cater for users with different language default requirements.

1. Create a security group in your Active Directory domain that will map a specific language to a specific set of users in that group.
2. Add all Cloud PC users to this new security group who should receive that language.
3. In Server Manager, open **Group Policy Management** and create a new Group Policy object linked to the Organization Unit (OU) or domain that will contain the Cloud PCs for those users.
4. Right-click the new Group Policy object, and select **Edit...**
5. Navigate to **User Configuration** > **Preferences** > **Windows Settings**, right-click **Registry**, and select **New** > **Registry Item**.
6. Enter the following details in the **General** tab. Here is an example that shows Spanish (Spain) with language code es-ES:
    - Action: Replace
    - Hive: HKEY_CURRENT_USER
    - Key Path: Control Panel\Desktop
    - Value name: PreferredUILanguages
    - Value type: REG_SZ
    - Value data: [Language code].
      > [!Note]
      > To find the language code for your desired language and region combination, see the [language pack list](/windows-hardware/manufacture/desktop/available-language-packs-for-windows#language-packs).
7. Switch to the **Common** tab and check the following three options:
    - **Run in logged-on user's security context (user policy option)**
    - **Apply once and do not reapply** 
    > [!Note]
    > This setting ensures that users can change language options themselves later.
    - **Item-level targeting**
8. Select **Targeting...**, **New Item**, and **Security Group**.
9. Select **...** next to the Group, search for the new security group, select the new security group, and hit **OK**.
10. Select **User in group**, then select **OK** and **OK** to complete the new registry process.
11. In the "Group Policy Management Editor", navigate to **User Configuration** > **Preferences** > **Windows Settings**, right-click **Regional Options**, and select **New** > **Regional Options**.
12. Under "User Locale", select the language and region combination that matches the registry key you created above.
13. After selecting your desired language and region combination from the dropdown, the dropdown menu may be underlined in red, indicating that the selection is not confirmed. Hit the **F5** function key on your keyboard to confirm the selection, resulting in a green underlined dropdown menu.
    
    Before hitting **F5**:
    
    ![An example of the "User Locale" dropdown menu with a red underline, indicating that the selected language choice hasn't been confirmed.](media/provide-localized-windows-experience/regionaloption-selected-redunderline.png)

    After hitting **F5**:
    
    ![An example of the "User Locale" dropdown menu with a red underline, indicating that the selected language choice has been confirmed. ](media/provide-localized-windows-experience/regionaloption-selected-greenunderline.png)

14. Switch to the **Common** tab and check the following three options:
    - **Run in logged-on user's security context (user policy option).**
    - **Apply once and do not reapply.**
    > [!Note]
    > This setting ensures that users can change language options themselves later.
    - **Item-level targeting.**
15. Select **Targeting..**, **New Item**, and **Security Group**.
16. Select **...** next to the Group, search for the new security group, select the new security group, and hit **OK**.
17. Select **User in group**, then select **OK** and **OK** to complete the new registry process.

You can perform these steps for each language you need to provide as the default language for users. If your users have both Cloud PCs and physical devices, you may want to apply [Group Policy loopback](/troubleshoot/windows-server/group-policy/loopback-processing-of-group-policy) so these settings only affect users when they sign in to ther Cloud PC.

> [!NOTE]
> Step 6 above uses the "Replace" command, setting the user's preferred language to just the one language defined in the registry item. If you create multiple Group Policy objects to assign different languages to users, make sure each user is only a member of a single security group that is being targeted.

## Next steps
[Create a provisioning policy](create-provisioning-policy.md)
