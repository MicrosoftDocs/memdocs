---
title: Capabilities in Technical Preview 1604
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1604.
ms.date: 01/23/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ROBOTS: NOINDEX
manager: apoorvseth
ms.author: banreetkaur
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1604 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1604. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

 The following are new features you can try out with this version.  

##  <a name="BKMK_WindowsVPP"></a> Manage volume-purchased apps from the Windows Store for Business  
 The Windows Store for Business is where you can find and purchase apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can manage volume-purchased apps from the Configuration Manager console, for example:  

-   You can synchronize the list of purchased apps with Configuration Manager  

-   Apps that are synchronized appear in the Configuration Manager console and you can deploy these like any other apps  

-   You can track how many licenses are available, and how many are being used in the Configuration Manager console  

### Try it out!  

##### Scenario 1: Set up Windows Store for Business synchronization  

1.  In Microsoft Entra ID, register Configuration Manager as a "Web Application and/or Web API" management tool. This will give you a client ID that you'll need later.  

    1.  In the **Active Directory** node of [https://portal.azure.com](https://portal.azure.com), select your Microsoft Entra ID, then click **Applications** > **Add**.  

    2.  Click **Add an application my organization is developing**.  

    3.  Enter a name for the application, select **Web application** and/or **Web API**, then click the Next arrow.  

    4.  Enter the same URL for both the **Sign-on URL** and **App ID URI**.  The URL can be anything and doesn't need to resolve to a real address. For example, you can enter **https://&lt;yourdomain\>/sccm**.  

    5.  Complete the wizard.  

2.  In Microsoft Entra ID, create a client key for the registered management tool.  

    1.  Highlight the application you just created and click **Configure**.  

    2.  Under **Keys**, select a duration from the list, and click **Save**.  This will create a new client key.  Don't navigate away from this page until you have successfully onboarded Windows Store for Business to Configuration Manager.  

3.  In the Windows Store for Business, configure Configuration Manager as the store management tool.  

    1.  Open Windows Store for Business and sign-in if prompted.  

    2.  Accept the terms of use if required.  

    3.  Under **Management Tools**, click **Add a management tool**.  

    4.  In **Search for the tool by name**, type the name of the application you created in Microsoft Entra ID previously, then click **Add**.  

    5.  Click **Activate** next to the application you just imported.  

    6.  In the **Show Offline-Licensed Apps** wizard, click **Yes** if you want to allow offline-licensed applications to be purchased.  

4.  Purchase at least one app from the Windows Store for Business.  

5.  In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, then click **Windows Store for Business**.  

6.  On the **Home** tab, in the **Create** group, click **Add Windows Store for Business Account**.  

7.  Add your tenant ID, client ID, and client key from Microsoft Entra ID, then complete the wizard.  

8.  Once you're done, you'll see the account you configured in the **Windows Store for Business Accounts** list in the Configuration Manager console.  

##### Scenario 2: Create and deploy a Configuration Manager application from a Windows Store for Business offline licensed app  

1.  In the **Software Library** workspace of the Configuration Manager console, expand **Application Management**, then click **License Information for Store Apps**.  

2.  The **Purchased Windows Store for Business apps** list shows a list of apps that were synchronized from the store. Choose the app you want to deploy, then, in the **Home** tab, in the **Create** group, click **Create Application**.  

3.  A Configuration Manager application is created containing the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.  

##  <a name="BKMK_PFW"></a> Improvements to Microsoft Passport for Work management  
 You can now deploy Passport for Work policies to domain-joined Windows 10 devices managed by the Configuration Manager client.  

##  <a name="bkmk_switchsup"></a> Option for clients to switch to a new software update point  
 In the 1604 Technical Preview, you can enable the option for Configuration Manager clients to switch to a new software update point when there are issues with the active software update point. For this option, you must have multiple software update points available on a primary site. You enable this option on a device collection, and once enabled, the clients in the collection will look for another software update point at the next scan when the client fails to successfully connect to the active software update point. Depending on your WSUS configuration settings (update classifications, products, etc.), the switch to a new software update point will generate additional network traffic. Therefore, you should only use this option when necessary.  

#### To enable the option to switch software update points  

1.  In the Configuration Manager console, go to **Assets and Compliance > Overview > Device collections**.  

2.  On the **Home** tab, in the **Collection** group, click **Client Notification**, and then click **Switch to Next Software Update Point**.  

> [!NOTE]  
>  This option is only available on sites that  have multiple software update points.  

##  <a name="bkmk_peercache"></a> Client settings to manage Client Cache Settings and client Peer Cache  
 Technical preview version 1604 introduces two new device  client settings that affect the use of a client's cache. Both can be used individually but are configured on the same property sheet for client settings and combine to help you manage deployment of content to your clients in remote locations.  

-   First is **client Peer Cache**, a built-in Configuration Manager solution for clients to share content with other clients directly from their local cache. For Peer Cache clients to share content, they must be members of the same boundary group. Peer Cache doesn't replace the use of other solutions like BracnchCache but instead works side-by-side to give you more options to extend traditional content deployment solutions like distribution points.  

     After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in its boundary group.  The client that operates as a peer content source will submit a list of available content it has cached to its management point. Then, when the next client in that boundary group requests that content, the peer cache source is offered as a potential content source along with all distribution points that are configured to be fast. The client selects a random content source from this combined pool of content sources. Clients will only seek content from a distribution point that is configured to be slow when no fast distribution points or peer cache sources are present in the boundary group.  

-   The second new setting lets you **manage the size of the cache** on clients. You can set the cache to have a maximum size in megabytes and  a maximum size as a percentage of the clients drive space.  The client enforces the setting that is reached first.  

To help you understand the use of client Peer Cache, you can view the **Client Data Sources** dashboard. In the console go to **Monitoring > Client Status > Client Data Sources**. Here you can select a time period to apply to the dashboard. Then, in the display, you can select the boundary group or package for which you want to view information. When viewing information, you can hover your mouse over the surface to see more details about the different content or policy sources.  

 You can also use a new report, **Client Data Sources - Summarization**, to view a summarization of the client data sources for each boundary group.   
**Requirements to use Peer Cache:**  

-   You must configure your site with a **Network Access Account** that has **Full Control** to the cache folder on each client. By default, this is  **%windir%\ccmcache**  

-   Clients can only transfer content using Peer Cache when they're members of the same boundary group.  

#### To configure Client Peer Cache client settings  

1.  Both settings are configured on the same page of client settings. In the Configuration Manager console, go to **Administration > Client Settings**, and then open device client settings object you want to use. You can also modify the Default Client Settings object.  

2.  From the list of available settings, select **Client Cache Settings**.  

3.  To manage the size of the cache, set **Configure client cache size** equal to **Yes**. Then you can configure the maximum cache size for both megabytes and as a percentage of the clients drive space.  

4.  To enable clients to participate in client Peer Cache, set **Enable Configuration Manager client in full OS to share content** equal to **Yes**. Then you can configure the ports that clients use, including if they will HTTP or HTTPS.  

### Try it out!  
 Try to complete the following tasks and then use the feedback information near the top of this topic to let us know how it worked:  

1.  Modify client settings to specify  a  new size for client cache, and then confirm this setting on a client.  

2.  Use client settings to configure multiple clients to use Peer Cache  

3.  Deploy content to clients so that some or most clients get that content from another client by using Peer Cache.  You can confirm the content source that is used by viewing new dashboard.  

    > [!NOTE]  
    >  To complete this task with the technical preview and a single distribution point, configure the distribution point to be slow for the network location of all your clients. Then,  distribute the content to a single client.  After that client gets the content, you can distribute the content to additional clients that should find local peers to use as a content source before using the distribution point that is considered to be slow from the client's location.  

##  <a name="bkmk_passport"></a> Support for Passport for Work as a KSP  
 Configuration Manager lets you integrate with Microsoft Passport for Work which is an alternative sign-in method that uses Active Directory, or a Microsoft Entra account to replace a password, smart card, or virtual smart card.  
Passport lets you use a user gesture to log in, instead of a password. A user gesture might be a simple PIN, biometric authentication such as Windows Hello, or an external device such as a fingerprint reader.  

-   You can use Configuration Manager to control which gestures users can and can't use to log in, and to configure PIN complexity requirements.  

-   You can store authentication certificates in the Passport for Work key storage provider (KSP).  

When a user creates a Passport PIN, Windows sends a notification which Configuration Manager listens for.  This allows Configuration Manager to quickly become aware of which users have created a Passport PIN. Configuration Manager can then also issue new certificates to those users if  Passport is used as the Key Storage Provider in a certificate profile.  

##  <a name="bkmk_onpremdha"></a> On-premises Device Health Attestation  
 Health attestation for Windows 10 devices can now be configured to communicate using the on-premises infrastructure.  Administrators can specify whether reporting is done via the cloud or on-premises resources.  If **on-premises** is selected for health attestation reporting, then a URI can be specified for the service. This enables client PCs without internet access to use enable and manage devices using health attestation.  

#### Enable health attestation for on-premises devices  

1.  In the Configuration Manager console, navigate **Administration** > **Overview** > **Client settings**, and then set **Use on-premises Healthy Attestation Service** to **Yes**.  

2.  Specify the **On-premise Health Attestation Service URL**, and then click **OK**.  

To try it out, configure on-premises Health Attestation Service using client agent settings.  

##  <a name="BKMK_Smart"></a> SmartLock setting for Android devices  
 A new setting, **Allow SmartLock and other trust agents** has been added to the **Android and Samsung KNOX** configuration item that lets you control the SmartLock feature on compatible Android devices. This phone capability, sometimes known as trust agents lets you disable or bypass the device lock screen password if the device is in a trusted location such as when it's connected to a specific Bluetooth device, or when it's near to an NFC tag. You can use this setting to prevent end users from configuring SmartLock.  
