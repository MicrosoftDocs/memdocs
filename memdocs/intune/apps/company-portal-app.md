---
# required metadata

title: How to configure the Company Portal app
titleSuffix: Microsoft Intune
description: Learn how you can apply company-specific branding to the Intune Company Portal app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# How to configure the Microsoft Intune Company Portal app

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The Microsoft Intune company portal is where users access company data and can do common tasks like enrolling devices, installing apps, and locating information for assistance from your IT department. Additionally, the company portal app allows user to securely access company resources. The company portal app provides several different pages, such as Home, Apps, App details, Devices, and Device details. To quickly find apps within the Company Portal, you can filter the apps on the Apps page.

> [!IMPORTANT]
> To support Google’s Firebase Cloud Messaging (FCM), you must update your Android Company Portal app to the latest version.  

> [!Tip]
> When you customize the Company Portal, the configurations apply to both the Company Portal website and Company Portal apps. Note that users must have an Intune license assigned to access the Company Portal website.

By customizing the Company Portal, you will help provide a familiar and helpful experience for your end users. To do this, navigate to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant Administration** > **Branding and customization**, and then configure the required settings.

When a user is installing an iOS/iPadOS application from the Company Portal they will receive a prompt. This occurs when the iOS/iPadOS app is linked to the app store, linked to a volume-purchase program (VPP), or linked to a line-of-business (LOB) app. The prompt allows the users to accept the action or allow management of the app. The prompt will display your company name, or when your company name is unavailable, **Company Portal** will be displayed. 

> [!Note]
> If you are using Azure Government, app logs are offered to the end user to decide how they will share when they initiate the process to get help with an issue. However, if you are not using Azure Government, the Company Portal for Windows 10 will send app logs directly to Microsoft when the user initiates the process to get help with an issue. Sending the app logs to Microsoft will make it easier to troubleshoot and resolve issues. 

## Company information and privacy statement
The company name is displayed as the Company Portal title. The privacy statement is displayed when a user clicks on the privacy link.

| Field name | Max length | More information |
|---|---|---|
|**Company name**| 40 | This name is displayed as the title of the Company Portal and appears as text throughout the Intune user experience. |
| **Privacy statement URL** |     79     | You can specify your own company privacy statement that appears when users click the privacy links from the Company Portal. You must enter a valid URL in the format `<https://www.contoso.com>`. |

> [!NOTE]
> Consistent with Microsoft and Apple policy, we do not sell any data collected by our service to any third parties for any reason.

## Support information
Enter your company's support information to provide your employee with a contact for Intune-related questions.

|Field name|Max length|More information|
|---|---|---|
|**Contact name** | 40 | This name is displayed on the **Help and Support** page. |
|**Phone number** | 20 | This contact number is displayed on the **Help and Support** page to enable employees to contact you for support. |
|**Email address**| 40 | This contact address is displayed on the **Help and Support** page. You must enter a valid email address in the format `alias@domainname.com`. |
|**Website name**| 40 | This name is the friendly name that is displayed for the URL to the support website. If you specify a support website URL and no friendly name, then Go to IT website is displayed on the **Help and Support** page in the Company Portal. |
|**Website URL**| 150 | If you have a support website that you want your users to use, specify the URL here. The URL must be in the format `https://www.contoso.com`. If you don't specify a URL, nothing is displayed for the support website on the **Help and Support** page in the Company Portal. |
| **Additional information**| 120 | Displayed on the **Help and Support** page. |


## Company identity branding customization
You can customize your Company Portal with your company logo, company name, theme color and background.

### Theme color and logo in the Company Portal
Apply a theme color to the Company Portal. Select a standard color or enter a six-digit hex code for a custom color.

|Field name|More information|
|---|---|
|**Select a standard color or enter a six-digit hex code**| Choose **Standard** to visually select a color. Choose **Custom** to select a specific color based on a hex code value.|
|**Choose theme color**| Select a theme color to apply to the Company Portal. You can choose from a standard color, or enter a specific hex code. |
|**Display**| Select whether to display the **Company logo and name**, the **Company logo only**, or the **Company name only**. |
|**Upload your company logo**|You can upload your company logo to show in your Company Portal. Note the text color is automatically chosen to provide the highest level of contrast. For the best appearance, upload a logo with a transparent background.<p><ul><li>Max image size: 400px x 400px</li><li>Maximum file size: 750KB</li><li>File type: PNG, JPG, or JPEG</li></ul>|

After you upload the logo, the preview area will show the logo with the theme color. If you chose to display your company name, it will be shown in black or white in the Company Portal, and it will be chosen automatically to provide the highest level of contrast based on your theme color. The preview area on the screen will not show your company’s name. 

### Logo to use on white or light backgrounds
Choose a logo that will look best on white or light backgrounds.

|Field name|More information|
|---|---|
|**Upload your logo**| This option is available if you have chosen to show the company logo. For the best appearance, upload a logo with a transparent background.<p><ul><li>Max image size: 400px x 400px</li><li>Maximum file size: 750KB</li><li>File type: PNG, JPG, or JPEG</li></ul>|

### Brand image for Company Portal

Display a brand image that reflects your company brand. After you save your changes, you can choose **Preview your settings** in the Intune Web Portal at the top of the pane to see how your configurations will look. Note that you will only be able to preview brand image on an iOS/iPadOS device and not the Intune Web Portal. 

|Field name|More information|
|---|---|
|**Upload your brand image**| This option allows you to display a brand image. On the iOS/iPadOS Company Portal, it shows as a background image on the user's profile page.<p><ul><li>Recommended image width: Greater than 1125px (required to be at least 650 px)</li><li>Max image size: 1.3 MB</li><li>File type: PNG, JPG, or JPEG</li></ul>|

The right brand image can enhance the user’s trust in Company Portal by presenting a strong sense of your company’s brand. Here are some tips you may want to consider for acquiring, choosing, and optimizing the image for Company Portal. 

- Reach out to your marketing or art department. They may already have an approved set of brand images. They may also be able to help you optimize images as needed. 

- Consider both landscape and portrait composition. The image should have sufficient background surrounding the focal point. The image may be cropped differently based on device size, orientation, and platform. 

- Avoid using a generic, stock image. The image should reflect your company’s brand and feel familiar to users. If you don’t have one, it’s better to not use one than use a generic one that has no meaning to your user. 

- Remove unnecessary metadata. Image file can come with metadata such as camera profile, geo location, title, caption, and so on. Use an image optimization tool to strip out this information to maintain quality while meeting file size limit. 

After a brand image is added or changed in Intune, the end user may not see the change on iOS/iPadOS devices until the Company Portal has recognized the change on start up, and then has been restarted to display the brand image. 

### Brand image examples

The following image shows an example iPad branding image:

![Screenshot of example iPhone branding image](./media/company-portal-app/company-portal-app-03.png)

The following image shows an example iPhone branding image:

![Screenshot of example iPad branding image](./media/company-portal-app/company-portal-app-02.png)

## Privacy statement customization

You can customize the privacy statement that appears for your organization on managed iOS/iPadOS devices. This message lists the items that your organization can't see or do on managed iOS/iPadOS devices.

Under **Company Portal customization** > **Device management and privacy message**, you can:

- Accept the **Default** to use the list as shown, or
- Choose **Custom** to customize the the list of items that your organization can’t see or do on managed iOS/iPadOS devices. You can use [markdown](https://daringfireball.net/projects/markdown/) to add bullets, bolding, italics, and links.

## Company Portal derived credentials for iOS devices
Intune supports Personal Identity Verification (PIV) and Common Access Card (CAC) Derived Credentials in partnership with credential providers DISA Purebred, Entrust Datacard, and Intercede. End users will go through additional steps post-enrollment of their iOS/iPadOS device to verify their identity in the Company Portal application. Derived Credentials will be enabled for users by first setting up a credential provider for your tenant, then targeting a profile that uses Derived Credentials to users or devices.

> [!NOTE]
> The user will see instructions about derived credentials based on the link that you have specified via Intune.

For more information about derived credentials for iOS/iPadOS devices, see [Use derived credentials in Microsoft Intune](~/protect/derived-credentials.md).

## Dark Mode for iOS Company Portal

Dark Mode is available for the iOS Company Portal. Users can download company apps, manage their devices, and get IT support in the color scheme of their choice based on device settings. The iOS Company Portal will automatically match the end user's device settings for dark or light mode. 

## Windows Company Portal keyboard shortcuts

End users can trigger navigation, app, and device actions in the Windows Company Portal using keyboard shortcuts (accelerators).

The following keyboard shortcuts are available in the Windows Company Portal app.

| Area | Description | Keyboard shortcut |
|:------------------:|:--------------:|:-----------------:|
| Navigation menu | Navigation | Alt+M |
|  | Home | Alt+H |
|  | All apps | Alt+A |
|  | Installed apps | Alt+I |
|  | Send feedback | Alt+F |
|  | My profile | Alt+U |
|  | Settings | Alt+T |
| Home - Device tile | Rename | F2 |
|  | Remove | Ctrl+D or Delete |
|  | Check access | Ctrl+M or F9 |
| Device details | Rename | F2 |
|  | Remove | Ctrl+D or Delete |
|  | Check access | Ctrl+M or F9 |
| App details | Install | Ctrl+I |
| Devices | Available | Ctrl+D |

End users will also be able to see the available shortcuts in the Windows Company Portal app.

![Screenshot of the available shortcuts in the Windows Company Portal](./media/company-portal-app/company-portal-app-01.png)

## User self-service device actions from the Company Portal

Users can perform actions on their local or remote devices via the Company Portal app or Website. The actions that a user can perform varies based on device platform and configuration. In all cases, the remote device actions can only be performed by device’s Primary User.
- **Retire** – Removes the device from Intune Management. In the company portal app and website, this shows as **Remove**.
- **Wipe** – This action initiates a device reset. In the company portal website this is shown as **Reset**, or **Factory Reset** in the iOS Company Portal App.
- **Rename** – This action changes the device name that the user can see in the Company Portal. It does not change the local device name, only the listing in the Company Portal.
- **Sync** – This action initiates a device check-in with the Intune service. This shows as **Check Status** in the Company Portal.
- **Remote Lock** – This locks the device, requiring a PIN to unlock it.
- **Reset Passcode** – This action is used to reset device passcode. On iOS/iPadOS devices the passcode will be removed and the end user will be required to enter a new code in settings. On supported Android devices, a new passcode is generated by Intune and temporarily displayed in the Company Portal.
- **Key Recovery** – This action is used to recover a personal recovery key for encrypted macOS devices from the Company Portal website. 

### Self Service Actions

Some platforms and configurations do not allow self-service device actions. This table below provides further details about self service actions:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Retire | Available<sup>(1)</sup> | Available | Available | Available<sup>(7)</sup> |
| Wipe | Available | Available<sup>(5)</sup> | NA | Available<sup>(7)</sup> |
| Rename<sup>(4)</sup> | Available | Available | Available | Available |
| Sync | Available | Available | Available | Available |
| Remote Lock | Windows Phone only | Available | Available | Available |
| Reset Passcode | Windows Phone only | Available<sup>(8)</sup> | NA | Available<sup>(6)</sup> |
| Key Recovery | NA | NA | Available<sup>(2)</sup> | NA |

<sup>(1)</sup> **Retire** is always blocked on Azure AD Joined Windows devices.<br>
<sup>(2)</sup> **Key Recovery** for MacOS is only available via the Web Portal.<br>
<sup>(3)</sup> All remote actions are disabled if using a Device Enrollment Manager enrollment.<br>
<sup>(4)</sup> **Rename** only changes the device name in the Company Portal app or Web Portal, not on the device.<br>
<sup>(5)</sup> **Wipe** is not available on User Enrolled iOS devices.<br>
<sup>(6)</sup> **Reset Passcode** is not supported on some Android and Android Enterprise configurations. For more information, see [Reset or remove a device passcode in Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **Retire** and **Wipe** are not available on Android Enterprise Device Owner scenarios (COPE, COBO, COSU).<br> 
<sup>(8)</sup> **Reset Passcode** is not supported on User Enrolled iOS devices.

## Next steps

- [Manually add the Windows 10 Company Portal app by using Microsoft Intune](company-portal-app.md)
