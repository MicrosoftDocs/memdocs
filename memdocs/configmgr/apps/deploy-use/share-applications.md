---
title: "Share applications in the Software Center"
titleSuffix: "Configuration Manager"
description: "Share a link to an application in the Software Center in Configuration Manager."
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Share an application from Software Center

*Applies to: Configuration Manager (current branch)* <!-- 1706 -->

You can copy a hyperlink to an application in Software Center using the  ![Share](media/share15.png)  **Share** button in the Application Details view. You can only share hyperlinks for applications. If the application becomes unavailable, the hyperlink opens a window with an application unavailable message.

1. Choose **Applications**, and then choose the application.
2. Click the ![Share](media/share15.png) **Share** button.
3. Click **Copy** in the window.
4. Paste the URL into an email to share the application.  

> [!TIP]  
>  To create a link in an Outlook email, press **CTRL** + **K** and then paste the URL.  
>  
> By default, Outlook shows a security alert for the Software Center protocol when the recipient clicks the link. Prevent this in your environment by adding a trusted protocol key to the registry. For example, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
