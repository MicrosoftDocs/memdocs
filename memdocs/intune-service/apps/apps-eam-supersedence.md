---
title: Guided update supersedence for Enterprise App Management 
titleSuffix: Microsoft Intune
description: Learn how to update an Enterprise App Catalog app using supersedence with Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 

ms.reviewer: nicolezhao
ms.suite: ems
search.appverid: MET150
ms.custom: 
ms.collection:
- tier1
- M365-identity-device-management
- FocusArea_Apps_EAM
---

# Guided update supersedence for Enterprise App Management

Guided update supersedence for Enterprise App Management allows you to check for updates of Windows (Win32) Enterprise App Catalog apps. You can view an available update for the app and select the option to create a new app with a supersedence relationship for the app it’s updating. Prepopulated attributes are provided when creating the new app.

## View available updates

In the **Overview** pane for a selected Enterprise App Catalog app, you can view the available updates by selecting the tile **Enterprise App Catalog apps with available updates**.

The **Enterprise App Catalog apps with updates** pane provides a list of Enterprise App Catalog apps that can be updated. This list provides the following app details:
- **App name**: - The name of the app.
- **Publisher**: - The publisher of the app.
- **Provisioned version**: - The currently installed app version.
- **Latest available version**: - The new version that is available.

:::image type="content" alt-text="Screenshot the Enterprise App Catalog app list with available updates." source="./media/apps-eam-supersedence/apps-eam-supersedence-02.png" lightbox="./media/apps-eam-supersedence/apps-eam-supersedence-02.png" :::

## Update an Enterprise App Catalog app

1. To update an Enterprise App Catalog app, select the *app name* to display additional options.

    You can update a specific app. This option allows you to update the app with a newer app version. Intune uses information from the Enterprise App Catalog to define properties and settings. You can review and define custom settings as needed. You should consider downloading and exporting the properties of the app before updated.

    Superseding an app creates a new app with the latest app package and sets up the supersedence relationship. Some settings, such as scope tags and assignments won't be copied to the new app.

2. Select the **Update** option for the specific app. 
   The **Update application** pane is displayed.

    :::image type="content" alt-text="Screenshot an Enterprise App Catalog app list the supersedence option." source="./media/apps-eam-supersedence/apps-eam-supersedence-04.png" lightbox="./media/apps-eam-supersedence/apps-eam-supersedence-04.png" :::

3. Select **Supersede app**.

4. Select your app **Assignments**, then **Review + create** the superseded app.

## Next steps

- [Microsoft Intune Enterprise Application Management](../apps/apps-enterprise-app-management.md)
- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
