---
title: "Endpoint Protection malware definitions from network share | System Center Configuration Manager"
description: "Learn how to manually download the latest definition updates from Microsoft and then configure clients to download these definitions."
ms.custom: na
ms.date: 08/05/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: 21
author: NathBarnmanager: angrobe

---

# Enable Endpoint Protection malware definitions to download from a network share for Configuration Manager
 You can manually download the latest definition updates from Microsoft and then configure clients to download these definitions from a shared folder on the network. Users can also initiate definition updates when you use this update source.

> [!NOTE]
>  Clients must have read access to the shared folder to be able to download definition updates.

 For more information about how to download the definition and engine updates to store on the file share, see [Install the latest Microsoft Forefront Security definition updates](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).

## To configure definition downloads from a file share

1.  In the Configuration Manager console, click **Assets and Compliance**.

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.

3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).

4.  In the **Definition updates** section of the antimalware properties dialog box, click **Set Source**.

5.  In the **Configure Definition Update Sources** dialog box, select **Updates from UNC file shares**.

6.  Click **OK** to close the **Configure Definition Update Sources** dialog box.

7.  Click **Set Paths**. Then, in the **Configure Definition Update UNC Paths** dialog box, add one or more UNC paths to the location of the definition updates files on a network share.

8.  Click **OK** to close the **Configure Definition Update UNC Paths** dialog box.


> [!div class="button"]
[Next step >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Back >](endpoint-configure-alerts.md)
