---
# required metadata

title: Troubleshoot mobile application management 
titleSuffix: Microsoft Intune
description: This topic describes some troubleshooting tips for Conditional Access deployments.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: cd5a0a3b-0013-4be3-a233-ce6e9083149f

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot mobile application management

This topic provides solutions to common problems that have occurred when using Intune App Protection (also referred to as MAM or mobile application management).

If this information does not solve your problem, see [How to get support for Microsoft Intune](../fundamentals/get-support.md) to find more ways to get help.

## Common IT administrator issues

These are common issues an IT administrator may experience when using Intune app protection policies.

| Issue | Description | Resolution |
| -- | -- | -- |
| Policy not applied to Skype for Business | App protection policy without device enrollment, made in the Azure portal, is not applying to the Skype for Business app on iOS/iPadOS and Android devices. | Skype for Business must be set up for modern authentication.  Please follow instructions in [Enable your tenant for modern authentication](https://social.technet.microsoft.com/wiki/contents/articles/34339.skype-for-business-online-enable-your-tenant-for-modern-authentication.aspx) to set up modern authentication for Skype. |
| Office app policy not applied | App protection policies are not applying to any [supported Office App](https://www.microsoft.com/cloud-platform/microsoft-intune-partners) for any user. | Confirm that the user is licensed for Intune and the Office apps are targeted by a deployed app protection policy. It can take up to 8 hours for a newly deployed app protection policy to be applied. |
| Admin can't configure app protection policy in Azure portal | IT administrator user is unable to configure app protection policies in Azure portal. | The following user roles have access to the Azure portal: <ul><li>Global administrator, which you can set up in the [Microsoft 365 admin center](https://admin.microsoft.com/)</li><li>Owner, which you can set up in the [Azure portal](https://portal.azure.com/).</li><li>Contributor, which you can set up in the [Azure portal](https://portal.azure.com/).</li></ul> Refer to [Role-based administration control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md) for help setting up these roles.|
|User accounts missing from app protection policy reports | Admin console reports do not show user accounts to which app protection policy was recently deployed. | If a user is newly targeted by an app protection policy, it can take up to 24 hours for that user to show up in reports as a targeted user. |
| Policy changes not working | Changes and updates to app protection policy can take up to 8 hours to apply. | If applicable, the end-user can log out of the app and log back in to force sync with service. |
| App protection policy not working with DEP | App protection policy is not applying to Apple DEP devices. | Please ensure you are using User Affinity with Apple Device Enrollment Program (DEP). User Affinity is required for any app that requires user authentication under DEP. <br><br>Refer to [Automatically enroll iOS/iPadOS devices with Apple's Device Enrollment Program](../enrollment/device-enrollment-program-enroll-ios.md) for more information on iOS/iPadOS DEP enrollment.|
| Data transfer policy not working with iOS/iPadOS | The **Allow app to transfer data to other apps** and **Allow app to receive data from other apps** policies do not successfully manage data transfer in iOS/iPadOS. | See [How to manage data transfer between iOS/iPadOS apps in Microsoft Intune](data-transfer-between-apps-manage-ios.md). |

## Common end-user issues

Common end-user issues are broken down in the following categories:

* **Normal usage scenarios**: An end-user might experience these scenarios on apps that have an Intune app protection policy. These are not actual issues, but may be perceived as bugs or errors.

* **Normal usage dialogs**: These are usage dialogs an end-user might see in apps that have an Intune app protection policy. These messages and dialogs do **not** indicate an error or bug.

* **Error messages and dialogs**: These are error messages and dialogs an end-user might see on apps that have an Intune app protection policy. These often indicate an error was made by the IT administrator or a bug with Intune app protection.

### Normal usage scenarios

Platform | Scenario | Explanation |
---| --- | --- |
iOS | The end-user can use the iOS/iPadOS share extension to open work or school data in unmanaged apps, even with the data transfer policy set to **Managed apps only** or **No apps.** Doesn't this leak data? | Intune app protection policy cannot control the iOS/iPadOS share extension without managing the device. Therefore, **Intune encrypts "corporate" data before sharing it outside the app**. You can validate this by attempting to open the "corporate" file outside of the managed app. The file should be encrypted and unable to be opened outside the managed app.
iOS | Why is the end-user **prompted to install the Microsoft Authenticator app** | This is needed when App Based Conditional Access is applied, see [Require approved client app](https://docs.microsoft.com/azure/active-directory/conditional-access/app-based-conditional-access).
Android | Why does the end-user **need to install the Company Portal app**, even if I'm using MAM app protection without device enrollment?  | On Android, much of app protection functionality is built into the Company Portal app. **Device enrollment is not required even though the Company Portal app is always required**. For app protection without enrollment, the end-user just needs to have the Company Portal app installed on the device.
iOS/Android | App Protection policy not applied on draft email in the Outlook app | Since Outlook supports both corporate and personal context, it does not enforce MAM on draft email.
iOS/Android | App Protection policy not applied on new documents in WXP (Word,Excel,PowerPoint) | Since WXP supports both corporate and personal context, it does not enforce MAM on new documents until they are saved in an identified corporate location like OneDrive.
iOS/Android | Apps not allowing Save As to Local Storage when policy is enabled | The App behavior for this setting is controlled by the App Developer.
Android | Android has more restrictions than iOS/iPadOS on what "native" apps can access MAM protected content | Android is an open platform and the "native" app association can be changed by the end-user to potentially unsafe apps. Apply [Data transfer policy exceptions](app-protection-policies-exception.md) to exempt specific apps.
Android | Azure Information Protection (AIP) can Save as PDF when Save As is prevented | AIP honors the MAM policy for 'Disable printing' when Save as PDF is used.
iOS | Opening PDF attachments in Outlook app fails with "Action Not Allowed | This can occur if the user has not authenticated to Acrobat Reader for Intune, or has used thumbprint to authenticate to their organization. Open Acrobat Reader beforehand and authenticate using UPN credentials.


### Normal usage dialogs

Platform | Message or dialog | Explanation |
--- | --- | --- |
iOS, Android | **Sign-in**: To protect its data, your organization needs to manage this app. To complete this action, sign in with your work or school account. | The end-user must sign in with their work or school account in order to use this app, which requires an app protection policy. In order for the policy to apply, the user must authenticate against Azure Active Directory.
iOS, Android |**Restart Required**: Your organization is now protecting its data in this app. You need to restart the app to continue. | The app has just received an Intune app protection policy and must restart in order for the policy to apply.
iOS, Android |**Action Not Allowed**: Your organization only allows you to open work or school data in this app. | The IT administrator has set the **Allow app to receive data from other apps** to **Managed apps only**. Therefore, the end-user can only transfer data into this app from other apps that have an app protection policy.
iOS, Android |**Action Not Allowed**: Your organization only allows you to transfer its data to other managed apps. | The IT administrator has set the **Allow app to transfer data to other apps** to **Managed apps only**. Therefore, the end-user can only transfer data out of this app to other apps that have an app protection policy.
iOS, Android |**Wipe Alert**: Your organization has removed its data associated with this app. To continue, restart the app. | The IT administrator has initiated an app wipe using Intune app protection.
Android | **Company Portal required**: To use your work or school account with this app, you must install the Intune Company Portal app. Click “Go to store” to continue. | On Android, much of app protection functionality is built into the Company Portal app. **Device enrollment is not required even though the Company Portal app is always required**. For app protection without enrollment, the end-user just needs to have the Company Portal app installed on the device.

### Error messages and dialogs on iOS

Error message or dialog | Cause | Remediation |
-- | --- | --- |
**App Not Set Up**: This app has not been set up for you to use. Contact your IT administrator for help. | Failure to detect a required app protection policy for the app. |Make sure an iOS app protection policy is deployed to the user's security group and targets this app.
**Welcome to the Intune Managed Browser**: This app works best when managed by Microsoft Intune. You can always use this app to browse the web, and when it is managed by Microsoft Intune you gain access to additional data protection features. | Failure to detect a required app protection policy for the Intune Managed Browser app. <br><br>The user can still use the app to browse the web, but the app is not managed by Intune. | Make sure an iOS app protection policy is deployed to the user's security group and targets the Intune Managed Browser app.
**Sign-in Failed**: We can't sign you in right now. Please try again later. | Failure to enroll the user with the MAM service after the user attempts to sign in with their work or school account. | Make sure an iOS app protection policy is deployed to the user's security group and targets this app.
**Account Not Set Up**: Your organization has not set up your account to access work or school data. Please contact your IT administrator for help. | The user account does not have an Intune A Direct license. | Make sure the user's account has an Intune license assigned in the [Microsoft 365 admin center](https://admin.microsoft.com).
**Device Non-Compliant**: This app cannot be used because you are using a jailbroken device. Contact your IT administrator for help. | Intune detected the user is on a jailbroken device. | Reset the device to default factory settings. Follow [these instructions](https://support.apple.com/HT201274) from the Apple support site.
**Internet Connection Required**: You must be connected to the Internet to verify that you can use this app. | The device is not connected to the Internet. | Connect the device to a WiFi or Data network.
**Unknown Failure**: Try restarting this app. If the problem persists, contact your IT administrator for help. | An unknown failure occurred. | Wait a while and try again. If the error persists, create a [support ticket](../fundamentals/get-support.md#create-an-online-support-ticket) with Intune.
**Accessing Your Organization's Data**: The work or school account you specified does not have access to this app. You may have to sign in with a different account. Contact your IT administrator for help. | Intune detects the user attempted to sign in with second work or school account that is different from the MAM enrolled account for the device. Only one work or school account can be managed by MAM at a time per device. | Have the user sign in with the account whose username is pre-populated by the sign-in screen. You may need to [configure the user UPN setting for Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm). <br> <br> Or, have the user sign in with the new work or school account and remove the existing MAM enrolled account.
**Connection Issue**: An unexpected connection issue occurred. Check your connection and try again.  |  Unexpected failure. | Wait a while and try again. If the error persists, create a [support ticket](../fundamentals/get-support.md#create-an-online-support-ticket) with Intune.
**Alert**: This app can no longer be used. Contact your IT administrator for more information. | Failure to validate the app's certificate. | Make sure the app version is up-to-date. <br><br> Reinstall the app.
**Error**: This app has encountered a problem and must close. If this error persists, please contact your IT administrator. | Failure to read the MAM app PIN from the Apple iOS Keychain. | Restart the device. Make sure the app version is up-to-date. <br><br> Reinstall the app.

### Error messages and dialogs on Android

Dialog/Error message | Cause | Remediation |
-- | --- | --- |
**App not set up**: This app has not been set up for you to use. Contact your IT administrator for help. | Failure to detect a required app protection policy for the app. |Make sure an Android app protection policy is deployed to the user's security group and targets this app.
**Failed app launch**: There was an issue launching your app. Try updating the app or the Intune Company Portal app. If you need help, contact your IT administrator. | Intune detected valid app protection policy for the app, but the app is crashing during MAM initialization. | Make sure the app version is up-to-date. <br><br> Make sure the Intune Company Portal app is installed and up-to-date on the device. <br><br> If the error persists, use the Company Portal app to send logs to Intune or create a [support ticket](../fundamentals/get-support.md#create-an-online-support-ticket).
**No apps found**: There are no apps on this device that your organization allows to open this content. Contact your IT administrator for help. | The user tried to open work or school data with another app, but Intune cannot find any other managed apps that are allowed to open the data. | Make sure an Android app protection policy is deployed to the user's security and targets at least one other MAM-enabled app that can open the data in question.
**Sign-in failed**: Try to sign in again. If this problem persists, contact your IT administrator for help. | Failure to authenticate the account with which the user attempted to sign in. | Make sure the user signs in with the work or school account that is already enrolled with the Intune MAM service (the first work or school account that was successfully signed into in this app). <br><br> Clear the app's data. <br><br> Make sure the app version is up-to-date. <br><br> Make sure the Company Portal version is up-to-date.
**Internet connection required**: You must be connected to the Internet to verify that you can use this app. | The device is not connected to the Internet. | Connect the device to a WiFi or Data network.
**Device noncompliant**: This app can't be used because you are using a rooted device. Contact your IT administrator for help. | Intune detected the user is on a rooted device. | Reset the device to default factory settings.
**Account not set up**: This app must be managed by Microsoft Intune, but your account has not been set up. Contact your IT administrator for help. | The user account does not have an Intune A Direct license. | Make sure the user's account has an Intune license assigned in the [Microsoft 365 admin center](https://admin.microsoft.com).
**Unable to register the app**: This app must be managed by Microsoft Intune, but we were unable to register this app at this time. Contact your IT administrator for help. | Failure to automatically enroll the app with the MAM service when app protection policy is required. | Clear the app's data. <br><br> Send logs to Intune through the Company Portal app or file a support ticket. For more information, see [How to get support for Microsoft Intune](../fundamentals/get-support.md).

## Next steps

- [Validating your mobile application management setup](app-protection-policies-validate.md)
- Learn how to use log files to troubleshoot Intune App Protection policy, see [https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)
- For additional Intune troubleshooting information, see [Use the troubleshooting portal to help users at your company](../fundamentals/help-desk-operators.md). 
- Learn about any known issues in Microsoft Intune. For more information, see [Known issues in Microsoft Intune](../known-issues.md).
- Need extra help? See [How to get support for Microsoft Intune](../fundamentals/get-support.md).
