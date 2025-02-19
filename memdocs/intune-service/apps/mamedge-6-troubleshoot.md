---
# required metadata

title: Step 6. Troubleshoot Microsoft Edge for Business data security
titleSuffix:
description: Step 6. Troubleshoot Microsoft Edge for Business corporate data security in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/26/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 6. Troubleshoot Microsoft Edge for Business data security

Troubleshooting app protection policies (APP) and app configuration policies (ACP) in Microsoft Intune can involve several steps. 

The following list provides common issues and potential solutions:

- **Verify Policy Assignment:** Ensure that the App Protection Policy is assigned to the correct user group. This ensures that the policy is applied to the intended users.
- **Review Policy Settings:** Check that the necessary conditions and settings are properly defined in the policy. This helps ensure that your App Protection Policy is configured as intended.
- **Update Microsoft Edge:** If Microsoft Edge is crashing during initialization, ensure that the app version and the operating system meet the required conditions.
- **Policy Application:** If a policy setting isn't applied or no policy is applied at all, verify whether the user and Microsoft Edge for Business are targeted by the policy. Also, check if the user has signed in to Microsoft Edge for Business using their targeted corporate account.
- **Data Transfer to Unmanaged Apps:** Users can use the share extension to open work or school data in unmanaged apps, even with the data transfer policy set to Managed apps only or No apps. Intune APP can't control the share extension without managing the device. Therefore, Intune encrypts "corporate" data before sharing it outside the app.
- **Microsoft Authenticator App Requirement:** The user might be prompted to install the Microsoft Authenticator app. This is needed when App Based Conditional Access is applied.
- **Company Portal App Requirement on Android:** On Android, much of the app protection functionality is built into the Company Portal app. Device enrollment isn't required even though the Company Portal app is always required.
- **Save As to Local Storage:** If apps aren't allowing Save As to Local Storage when the policy is enabled, remember that the App behavior for this setting is controlled by the policy.
- **App configuration settings not applying correctly:** If none of your app configuration policy settings are applying correctly to the app based on the communication channel used (Managed Apps or Managed Devices), review the publisher's documentation again for the string or settings used. You may want to try using the other option for device enrollment type of the policy.
- **Sign in with your work account - Microsoft Edge for Business message:** If you encounter the 'Sign in with your work account' error message in Microsoft Edge for Business, it indicates that you have chosen an incorrect enrollment method, resulting in the App Protection Policy not being applied.

    :::image type="content" alt-text="Sign in with your work account - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business63.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business63.png":::

- If you encounter an error like the above, it could mean that you've selected the wrong enrollment method. You might have left a checkmark on 'Select No, sign into this app only'. Redo the enrollment process without selecting this option. Otherwise, the App Protection Policy won't be applied.

    :::image type="content" alt-text="Enrollment Window - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business64.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business64.png":::

Successful app protection policy deployment relies on proper configuration of settings and other dependencies. Always verify that you have met the prerequisites for deploying app protection policies.

If you continue to experience issues, it may be helpful to contact [Microsoft Support](../../get-support.md) for further assistance.

## FAQ

**Does Microsoft Edge for Business require a separate download?**  

No. Microsoft Edge for Business is automatically triggered by signing in with a Microsoft Entra ID.

**is Windows home version supported for MAM for Windows?**

Yes, MAM for Windows does support the Windows Home Edition.

**Will all policies and configurations previously set by IT be applied to Edge for Business?**

Yes, all policies and configurations currently in place will be inherited by Microsoft Edge for Business.

**What impact will this cause to my default browser settings?**

There's no impact on users\' default browser settings.

**What happens to favorites, passwords, and related data?**  

Passwords, favorites, and data currently associated with the user's work profile will be maintained in Microsoft Edge for Business. Passwords, favorites, and data aren't shared between the work browser window and the personal browser window.

**How does MAM for Windows and Microsoft Edge management service differ?**

When comparing MAM for Windows and the Microsoft Edge management service, it's crucial to understand the key differences and choose the right management option for your needs. If you're currently using Microsoft Intune, your focus should be on creating app protection policies and application configuration policies to configure the browser. This ensures a secure enterprise browser configuration for your users.

However, if you're not using Microsoft Intune, the Microsoft Edge management service is the right choice for you. With this service, you can configure the Microsoft Edge for Business policy and configuration for your organization. For more information about Microsoft Edge management service, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecurityWhitepaper).

## Solution results

After completing this solution, you'll have accomplished the following:

- Created different scenarios to configure a **Microsoft Edge for Business** and **Microsoft Application Management** experience, from concept to implementation.

- Understand **app protection policy framework** is and how it can enhance security in your environment. This framework provides a robust layer of security for your environment. It allows admins to control how data is accessed and handled, ensuring that sensitive information is always protected.

- Implemented **Intune Device Encryption and Password Single Sign-On**: With Intune encryption, data is secured at rest and in transit. The password single sign-on feature in Microsoft Edge for Business enhances user convenience without compromising security.

- Created a baseline of **the app configuration policy** that helps achieve another level of security, from Intune encryption to password single sign-on in Microsoft Edge for Business.

- Configured the **Conditional Access Policy**. This feature allows IT Pros to define and implement policies based on conditions such as user role, location, and risk level.

- Understand the **end-user experience**, showing what behavior can be expected once you implement the Microsoft Intune app protection policy for Windows devices.

- Understand key **troubleshooting examples**, some of which were identified during Microsoft's research, and others that were suggested by various professionals in the industry.

Take advantage of these powerful features as an IT professional. You have the capability to build an environment that isn't only secure and efficient, but also user-friendly. Utilize Microsoft Edge for Business and Microsoft Application Management to strengthen your environment.

> [!IMPORTANT]
> Achieving security is not a one-time event, but a continuous process of improvement and adaptation to new challenges. Keep mproving your organization's security stance.

Next, continue to apply the strategies detailed in this solution to your organization's environment.
