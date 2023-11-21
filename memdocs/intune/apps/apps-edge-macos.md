---
# required metadata

title: Add Microsoft Edge to macOS devices using Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Edge to macOS devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/01/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier3
- M365-identity-device-management
- macOS
---

# 使用 Microsoft Intune 將 Microsoft Edge 添加到 macOS 

Before you can deploy, configure, monitor, or protect apps, you must add them to Intune. One of the available [app types](apps-add.md#app-types-in-microsoft-intune) is Microsoft Edge *version 77 and later*. By selecting this app type in Intune, you can assign and install Microsoft Edge *version 77 and later* to devices you manage that run macOS. This app type makes it easy for you to assign Microsoft Edge to macOS devices without requiring you to use the macOS app wrapping tool. To help keep the apps more secure and up to date, the app comes with Microsoft AutoUpdate (MAU).

> [!IMPORTANT]
> 此應用類型提供適用於 macOS 的開發者和測試版頻道。部署僅提供英語 （EN） 版本，但最終使用者可以在瀏覽器的“設置”>“語言”下更改顯示語言。

> [!NOTE]
> Microsoft Edge 版本 77 及更新版本也可用於 Windows 10。

## 先決條件

- macOS 設備必須運行 macOS 10.14 或更新版本，然後才能安裝 Microsoft Edge。

## 將 Microsoft Edge 添加到 IntuneAdd Edge to Intune

可以使用以下步驟將 Microsoft Edge 版本 77 及更高版本添加到 Intune：

1. 登入到 [Microsoft Intune 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431).
2. 選擇“應用”>“所有應用”>“添加”。
3. 在 Microsoft Edge 版本 77 及更高版本下的“應用類型”清單中，選擇“macOS”。

## 配置應用資訊
在此步驟中，將提供有關此應用部署的資訊。此資訊可幫助你識別 Intune 中的應用，並幫助使用者在公司門戶中查找應用。

1. 按兩下應用資訊以顯示「應用資訊」窗格。
2. 在「應用資訊」窗格中，提供有關此應用部署的資訊。此資訊可幫助你識別 Intune 中的應用，並幫助使用者在公司門戶中查找應用。
    - 名稱：輸入應用的名稱，因為它將顯示在公司門戶中。確保所有名稱都是唯一的。如果同一應用名稱存在兩次，則在公司門戶中僅向用戶顯示其中一個應用。
    - 說明：輸入應用的說明。例如，您可以在描述中列出目標使用者。
    - 發行者：Microsoft 顯示為發行者。
    - 類別：（可選）選擇一個或多個內置應用類別或您創建的類別。此設置使用戶在流覽公司門戶時更容易找到應用。
    - 在公司門戶中將其顯示為特色應用：選擇此選項可在使用者瀏覽應用時在公司門戶的主頁上突出顯示該應用。
    - 資訊 URL：（可選）輸入包含此應用相關信息的網站的 URL。該 URL 在公司門戶中顯示給使用者。
    - 隱私 URL：（可選）輸入包含此應用隱私信息的網站的 URL。該 URL 在公司門戶中顯示給使用者。
    - 開發人員：Microsoft 顯示為開發人員。
    - 擁有者：Microsof後續步驟
- To learn how to configure Microsoft Edge on macOS devices, see [Configure Microsoft Edge on macOS devices](/deployedge/configure-microsoft-edge-on-mac).
- To learn about including and excluding app assignments from groups of users, see [Include and exclude app assignments](apps-inc-exl-assignments.md).
- [Assign apps to groups](apps-deploy.md)
