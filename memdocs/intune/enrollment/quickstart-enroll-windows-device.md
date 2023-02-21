---
# required metadata

title: Quickstart - Enroll your Windows 10/11 desktop device in Microsoft Intune
description: Quickstart - Use the Company Portal to enroll your Windows 10/11 desktop device into Microsoft Intune.
services: microsoft-intune
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/04/2021
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Quickstart: Enroll your Windows device  

**Applies to**
- Windows 10 
- Windows 11 

In this quickstart, you'll first take the role of an Intune user and enroll a device running Windows 10/11 into Microsoft Intune. Then you'll return to Intune and confirm that the device enrolled.  

Enrolling your devices into Microsoft Intune allows you to access your organization's secure data, including email, files, and other resources, from your Windows device. This is true for both devices running Windows 10/11 devices (including desktop) and Windows 10 Mobile devices. Enrolling your devices helps secure this access for both you and your organization, and helps keep your work data separate from your personal data. 

> [!TIP]
> Find out what happens when you [enroll your device in Intune](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md) and what that means for the [information on your device](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

## Prerequisites

- Microsoft Intune subscription - [sign up for a free trial account](../fundamentals/free-trial-sign-up.md)
- To complete this quickstart, you must complete the steps to [setup automatic enrollment in Intune](quickstart-setup-auto-enrollment.md).

## Confirm Windows version  

Before enrolling your Windows device, you must confirm the version of Windows that you have installed.

1. Right-click the Windows **Start** icon and select **Settings** to display Windows Settings options.

   ![Screenshot of Windows Settings - System](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Select **System** > **About**. 

   ![Screenshot of your system settings](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > You can also type the phrase "About your PC" into the **search bar**, then select **About your PC**.

3. In the **Settings** window you will see a list of **Windows specifications** for your PC. Within this list, locate the **Version**.

4. Confirm that the Windows **Version** is Windows 10 (version 1607 or later) or Windows 11 (version 21H2 or later). 

    > [!IMPORTANT]
    > The steps presented in this quickstart are for Windows 10 (version 1607 or higher) or Windows 11 (version 21H2 or later). If your version is 1511 or earlier, see [Enroll device running Windows 10, version 1511 and earlier](../user-help/enroll-windows-10-device.md#enroll-windows-10-version-1511-and-earlier-device).  

## Enroll Windows 10/11 desktop

1. Return to Windows Settings and select **Accounts**.

   ![Screenshot of your system settings - Accounts](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Select **Access work or school** > **Connect**.

    ![Select Access work school account](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Enter the username and password for your work account, and then select **Next**. If you followed the [create a user and assign a license](../fundamentals/quickstart-create-user.md) quickstart, you can sign in with the user account that you created.  

   ![Enter your work or school account](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    You'll see a message indicating that your company or school is registering your device.

4. When you see the **You're all set!** screen, select **Done**.   

5. You will now see the added account as part of the **Access work or school** settings on your device.    

   ![Screenshot of newly added account](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    If you followed the previous steps, but still can't access your work or school email account and files, follow the steps in [Troubleshoot Windows 10/11 device access](../user-help/troubleshoot-your-windows-10-device-windows.md).  

## Confirm your device enrollment in Intune  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a Global Administrator.
2. Select **Devices** > **All devices** to view the enrolled devices in Intune.
3. Verify that you have an additional device enrolled within Intune.

   ![Screenshot of Intune-enrolled devices](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## Clean up resources

To unenroll your Windows device, see [Remove your Windows device from management](../user-help/unenroll-your-device-from-intune-windows.md).

## Next steps

In this quickstart, you learned how to enroll a Windows 10/11 device into Intune. You can learn about other ways to enroll devices across all platforms. For more information about using devices with Intune, see [Use managed devices to get work done](../user-help/use-managed-devices-to-get-work-done.md).

To follow this series of Intune quickstarts, continue to the next quickstart.

> [!div class="nextstepaction"]
> [Quickstart: Set a required password length for Android devices](../protect/quickstart-set-password-length-android.md)
