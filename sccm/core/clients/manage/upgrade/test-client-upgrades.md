---
title: "Test client upgrades pre-production collection"
description: "Test client upgrades in a pre-production collection in System Center Configuration Manager."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to test client upgrades in a pre-production collection in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can test a new Configuration Manager client version in a pre-production collection before upgrading the rest of the site with it.  When you do this, only devices that are part of the test collection are upgraded. Once you've had a chance to test the client you can promote the client, which makes the new version of the client software available to the rest of the site.

> [!NOTE]
> To promote a test client to production, you must be logged in as a user with security role of **full administrator** and a security scope of **All**. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration). You must also be logged into a server connected to the central administration site  or a top-level standalone primary site.

 There are 3 basic steps to testing clients in pre-production.  

1.  Configure automatic client upgrades to use a pre-production collection.  

2.  Install a Configuration Manager update that includes a new version of the client.  

3.  Promote the new client to production.  

##  To configure automatic client upgrades to use a pre-production collection  

1. [Set up a collection](..\collections\create-collections.md) that contains the computers you want to deploy the pre-production client to. Don't  include workgroup computers in pre-production collections. They can't use the authentication required for the distribution point to access the pre-production client package.   

1.  In the Configuration Manager console open **Administration** > **Site Configuration** > **Sites**, and choose **Hierarchy Settings**.  

     On the **Client Upgrade** tab of the **Hierarchy Settings Properties**:  

    -   Select **Upgrade all clients in the pre-production collection automatically using pre-production client**  

    -   Enter the name of a collection to use as a pre-production collection  

![Test client upgrades](media/test-client-upgrades.png)

>[!NOTE]
>To change these settings, your account must be a member of the **Full Administrator** security role, and the **All** security scope.


##  To install a Configuration Manager update that includes a new version of the client  

1.  In the Configuration Manager console,  open **Administration** > **Updates and Servicing**, select an **Available** update, and then choose **Install Update Pack**. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.)

     For more information on installing updates, see [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  During installation of the update, on the **Client Options** page of the wizard, select **Test in pre-production collection**.  

3.  Complete the rest of the wizard and install the update pack.  

     After the wizard complete, clients in the pre-production collection will begin to deploy the updated client. You can monitor the deployment of upgraded clients by going to **Monitoring** > **Client Status** > **Pre-production Client Deployment**. For more information, see [How to monitor client deployment status in System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > The deployment status on computers hosting site system roles in a pre-production collection may be reported as **Not compliant** even when the client was successfully deployed. When you promote the client to production, the deployment status is reported correctly.

##  To promote the new client to production  

1.  In the Configuration Manager console, open **Administration** > **Updates and Servicing**, and choose  **Promote Pre-production Client**. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.)

    > [!TIP]
    > The **Promote Pre-production Client** button is also available when you're monitoring client deployments in the console at **Monitoring** > **Client Status** > **Pre-production Client Deployment**.

2.  Review the client versions in production and pre-production, make sure the correct the pre-production collection is specified, and then  click **Promote**, then **Yes**.  

3.  After the dialog box closes, the updated client version will replace the client version in use in your hierarchy. You can then upgrade the clients for your whole site. See [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) for more information.  

>[!NOTE]
>To enable the pre-production client, or to promote a pre-production client to a production client, your account must be a member of a security role that has **Read** and **Modify** permissions for the **Update Packages** object.
>Client upgrades honor any Configuration Manager maintenance windows you have configured.
