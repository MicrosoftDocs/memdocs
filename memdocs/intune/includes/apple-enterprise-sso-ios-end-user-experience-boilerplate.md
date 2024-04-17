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

:::image type="content" source="../configuration/media/apple-enterprise-sso-plug-in/flow-chart-end-user-iosipados.png" alt-text="End user flow chart when installing SSO app app extension on iOS/iPadOS devices.":::

- If you're not deploying the Microsoft Authenticator app using an app policy, then users must install it manually. Users don't need to use the Authenticator app, it just needs to be installed on the device.

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test single sign-on by opening [Safari in private mode](https://support.apple.com/guide/ipad/browse-the-web-privately-ipad8ea0fc1a/ipados) (opens Apple's web site) and opening the `https://portal.office.com` site. No username and password will be required.

:::image type="content" source="../configuration/media/apple-enterprise-sso-plug-in/ipad-sso-animated.gif" alt-text="Animation showing SSO experience on iPadOS":::
