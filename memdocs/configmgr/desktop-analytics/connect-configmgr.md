---
title: Connect Configuration Manager
titleSuffix: Configuration Manager
description: A how-to guide for connecting Configuration Manager with Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to connect Configuration Manager with Desktop Analytics

Desktop Analytics is tightly integrated with Configuration Manager. First, make sure the site is up to date to support the latest features. Then create the Desktop Analytics connection in Configuration Manager. Finally, monitor the health of the connection.

## <a name="bkmk_hotfix"></a> Update the site

First, make sure that your Configuration Manager site is running at least version 1902. For more information, see [Install in-console updates](../core/servers/manage/install-in-console-updates.md).

You also need to install the version 1902 update rollup (4500571) to support integration with Desktop Analytics. For more information on this update, see [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4500571).

1. Update the site with the update rollup for version 1902. For more information, see [Install in-console updates](../core/servers/manage/install-in-console-updates.md).

2. Update clients. To simplify this process, consider using automatic client upgrade. For more information, see [Upgrade clients](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="bkmk_connect"></a> Connect to the service

> [!TIP]
> Prior to starting the wizard, create the target collection mentioned in step 8, as you cannot select outside of the wizard once you start it.

Use this procedure to connect Configuration Manager to Desktop Analytics, and configure device settings. This procedure is a one-time process to attach your hierarchy to the cloud service.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Select **Configure Azure Services** in the ribbon.

    > [!TIP]
    > Connect to the service directly from the **Desktop Analytics Servicing** node. In the Configuration Manager console, go to the **Software Library** workspace, and select the **Desktop Analytics Servicing** node. In the *New to Desktop Analytics?* box, select the second link to *Connect Configuration Manager to the Desktop Analytics service*.

2. On the **Azure Services** page of the Azure Services Wizard, configure the following settings:

    - Specify a **Name** for the object in Configuration Manager.

    - Specify an optional **Description** to help you identify the service.

    - Select **Desktop Analytics** from the list of available services.

   Select **Next**.

3. On the **App** page, select the appropriate **Azure environment**. Then select **Browse** for the web app.

4. If you have an existing app that you want to reuse for this service, choose it from the list, and select **OK**.

5. In most cases, you can create an app for the Desktop Analytics connection with this wizard. Select **Create**.<!-- 3572123 -->

    > [!TIP]
    > If you can't create the app from this wizard, you can manually create the app in Azure AD, and then import into Configuration Manager. For more information, see [Create and import app for Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Configure the following settings in the **Create Server Application** window:

    - **Application Name**: A friendly name for the app in Azure AD.

    - **HomePage URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is `https://ConfigMgrService`.

    - **App ID URI**: This value needs to be unique in your Azure AD tenant. It's in the access token used by the Configuration Manager client to request access to the service. By default this value is `https://ConfigMgrService`.

    - **Secret Key validity period**: choose either **1 year** or **2 years** from the drop-down list. One year is the default value.

    Select **Sign in** . After successfully authenticating to Azure, the page shows the **Azure AD Tenant Name** for reference.

    > [!NOTE]
    > Complete this step as a **Global administrator**. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard.

    Select **OK** to create the web app in Azure AD and close the Create Server Application dialog. On the Server App dialog, select **OK**. Then select **Next** on the App page of the Azure Services Wizard.

7. On the **Diagnostic Data** page, configure the following settings:

    - **Commercial ID**: this value should automatically populate with your organization's ID. If it doesn't, make sure your proxy server is configured to allow all required [endpoints](enable-data-sharing.md#endpoints) before continuing. Alternatively, retrieve your Commercial ID manually from the [Desktop Analytics portal](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Windows 10 diagnostic data level**: select at least **Basic**. See [Diagnostic data levels](enable-data-sharing.md#diagnostic-data-levels)
  
    - **Allow Device Name in diagnostic data**: select **Enable**

        > [!NOTE]
        > Starting with Windows 10 version 1803, the device name isn't sent to Microsoft by default. If you don't send the device name, it appears in Desktop Analytics as "Unknown". This behavior can make it difficult to identify and assess devices.

   Select **Next**. The **Available functionality** page shows the Desktop Analytics functionality that's available with the diagnostic data settings from the previous page. Select **Next** to continue or **Previous** to make changes.

    ![Example Available Functionality page in the Azure Services Wizard](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. On the **Collections** page, configure the following settings:

    - **Display name**: The Desktop Analytics portal displays this Configuration Manager connection using this name. Use it to differentiate between different hierarchies, and to identify collections from separate hierarchies. Use terms to easily distinguish multiple hierarchies in your environment, for example: *test lab* or *production*.

    - **Target collection**: This collection includes all devices that Configuration Manager configures with your commercial ID and diagnostic data settings. It's the full set of devices that Configuration Manager connects to the Desktop Analytics service.

    - **Devices in the target collection use a user-authenticated proxy for outbound communication**: By default, this value is **No**. If needed in your environment, set to **Yes**.

    - **Select specific collections to synchronize with Desktop Analytics**: Select **Add** to include additional collections from your **Target collection** hierarchy. These collections are available in the Desktop Analytics portal for grouping with deployment plans. Make sure to include pilot and pilot exclusion collections.  <!-- 4097528 -->

        > [!TIP]
        > The Select Collections window displays only the collections that are limited by the **Target collection**.
        >
        > In the following example, you select CollectionA as your target collection. Then when you add additional collections, you see CollectionA, CollectionB, and CollectionC. You can't add CollectionD.
        >
        > - CollectionA: limited by the **All Systems** collection
        >     - CollectionB: limited by CollectionA
        >         - CollectionC: limited by CollectionB
        > - CollectionD: limited by **All Systems** collection
        >
        > To manage the collections available in the Desktop Analytics portal for grouping with deployment plans, in the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Select the entry associated with **Desktop Analytics** Azure Service and update your settings in the **Desktop Analytics Collection** page.

        > [!IMPORTANT]
        > These collections continue to sync as their membership changes. For example, your Target collection uses a collection with a Windows 7 membership rule. As those devices upgrade to Windows 10, and Configuration Manager evaluates the collection membership, those devices drop out of the collection and Desktop Analytics.

9. Complete the wizard.

Configuration Manager creates a settings policy to configure devices in the Target Collection. This policy includes the diagnostic data settings to enable devices to send data to Microsoft. By default, clients update policy every hour. After receiving the new settings, it can be several hours more before the data is available in Desktop Analytics.

## <a name="bkmk_monitor"></a> Monitor connection health

Monitor the configuration of your devices for Desktop Analytics. In the Configuration Manager console, go to the **Software Library** workspace, expand the **Desktop Analytics Servicing** node, and select the **Connection Health** dashboard.

For more information, see [Monitor connection health](monitor-connection-health.md).

Configuration Manager synchronizes your collections within 60 minutes of creating the connection. In the Desktop Analytics portal, go to**Global Pilot**, and see your Configuration Manager device collections.

> [!NOTE]
> The Configuration Manager connection to Desktop Analytics relies upon the service connection point. Any changes to this site system role may impact synchronization with the cloud service. For more information, see [About the service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## Next steps

Advance to the next article to enroll devices to Desktop Analytics.
> [!div class="nextstepaction"]
> [Enroll devices](enroll-devices.md)
