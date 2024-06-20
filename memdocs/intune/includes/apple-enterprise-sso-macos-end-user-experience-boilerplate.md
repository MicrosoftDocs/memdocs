---
title: include file
description: include file
author: MandiOhlinger
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/16/2024
ms.author: mandia
ms.custom: include file
ms.reviewer: miepping
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. -->

## End user experience

:::image type="content" source="../configuration/media/apple-enterprise-sso-plug-in/flow-chart-end-user-macos.png" alt-text="End user flow chart when installing SSO app app extension on macOS devices in Microsoft Intune.":::

- If you're not deploying the Company Portal app using an app policy, then users must install it manually. Users don't need to use the Company Portal app, it just needs to be installed on the device.

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test single sign-on by opening [Safari in private mode](https://support.apple.com/guide/safari/browse-privately-ibrw1069/mac)  (opens Apple's web site) and opening the `https://portal.office.com` site. No username and password will be required.

:::image type="content" source="../configuration/media/apple-enterprise-sso-plug-in/macos-sso-animated.gif" alt-text="Users signs in to app or website to bootstrap the SSO app extension on iOS/iPadOS and macOS devices in Microsoft Intune.":::

On macOS, when users sign in to a work or school app, they're prompted to opt in or out of SSO. They can select **Don't ask me again** to opt out of SSO and block future requests.

Users can also manage their SSO preferences in the Company Portal app for macOS. To edit preferences, go to the Company Portal app menu bar > **Company Portal** > **Settings**. They can select or deselect **Don't ask me to sign in with single sign-on for this device**.

:::image type="content" source="../configuration/media/apple-enterprise-sso-plug-in/macos-sso-dont-ask.png" alt-text="Don't ask me to sign in with single sign-on for this device.":::
