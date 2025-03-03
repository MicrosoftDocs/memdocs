---
title: How users enroll devices
titleSuffix: Configuration Manager
description: Understand how users enroll devices with on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: article
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# How users enroll devices with on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager on-premises mobile device management (MDM), users can enroll their devices. There are two prerequisites:

- With client settings, you grant the user permission to enroll.

- You install the required trusted root certificate on the device.

For more information on how to set up enrollment, see [Set up device enrollment for on-premises MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md).

## <a name="bkmk_enrollDesk"></a> Enroll Windows 10

1. On a Windows 10 computer, go to **Settings**.

1. Select **Accounts**, and then select **Access work or school**.

1. Select **Connect**, enter your user principal name (UPN), and select **Continue**. The UPN may be the same as your email address, for example, jdoe@contoso.com.

1. Enter the fully qualified domain name (FQDN) of the enrollment proxy point, and select **Continue**.

1. Enter your password, and select **Sign in**.

1. Windows doesn't need to remember the sign-in info for this action, so select **Skip**.

After a short time, the device enrolls with Configuration Manager.

## <a name="bkmk_enrollMob"></a> Enroll Windows 10 Mobile

1. On a Windows 10 Mobile device, go to **Settings**.

1. Select **Accounts**, and then select **Work access**.

1. Select **Connect**.

1. Enter your UPN and the FQDN of the enrollment proxy point. Then select **Connect**.

1. On the next screen, enter your UPN and password, and then select **Sign-in**.

After a short time, the device enrolls with Configuration Manager. Select **Done**.

## <a name="bkmk_verify"></a> Verify enrollment

Use the Configuration Manager console to verify that devices are enrolled successfully. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select **Devices**. Browse or search for the enrolled device in the list of devices.
