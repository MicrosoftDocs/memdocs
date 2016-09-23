---
# required metadata

title: Determine the software update point infrastructure | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: e4c8ce1c-fe0d-4989-8d82-3c5776772243

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


#  <a name="BKMK_SUPInfrastructure"></a> Determine the software update point infrastructure  
 The central administration site and all child primary sites must have a software update point where you will deploy software updates. As you plan for the software update point infrastructure, you need to determine the following dependencies: where to install the software update point for the site; which sites require a software update point that accepts communication from Internet-based clients; whether you will configure the software update point as an NLB cluster’ and whether you need a software update point at a secondary site. Use the following sections to determine the software update point infrastructure.  

> [!IMPORTANT]  
>  For information about the internal and external dependencies that are required for software updates, see [Prerequisites for software updates in System Center Configuration Manager](../../sum/plan-design/prerequisites-for-software-updates.md).  

##  <a name="BKMK_SUP"></a> Software update points in Configuration Manager  
 You can add multiple software update points at a Configuration Manager primary site. The ability to have multiple software update points at a site provides fault tolerance without requiring the complexity of NLB. However, the failover that you receive with multiple software update points is not as robust as NLB for pure load balancing, but it is rather designed for fault-tolerance. Also, the failover design of the software update point is different than the pure randomization model that is used in the design for management points. Unlike in the design of management points, in the software update points there are client and network performance costs that are associated with switching to a new software update point. When the client switches to a new WSUS server to scan for software updates, the result is an increase in the catalog size and associated client-side and network performance demands. Therefore, the client preserves affinity with the last software update point for which it successfully scanned.  

 The first software update point that you install on a primary site is the synchronization source for all additional software update points that you add at the primary site. After you added your software update points and initiated software updates synchronization, you can view the status of the software update points and the synchronization source from the **Software Update Point Synchronization Status** node in the **Monitoring** workspace.  

 When a software update point fails, and that software update point is configured as the synchronization source for the other software update points at the site, you must manually remove the failed software update point and select a new software update point to use as the synchronization source. For more information about how to remove a software update point, see the [Remove the software update point site system role](../../sum/deploy-use/configure-software-updates.md#BKMK_RemoveSUP) section in the [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md) topic.  

###  <a name="BKMK_SUPList"></a> Software update point list  
 Configuration Manager provides the client with a software update point list in the following scenarios: when a new client receives the policy to enable software updates, or when a client cannot contact its software update point and needs to switch to another software update point. The client randomly selects a software update point from the list, and it prioritizes the software update points that are in the same forest. Configuration Manager provides clients with a different list depending on the type of client.  

-   **Intranet-based clients**: Receive a list of software update points that you can configure to allow connections only from the intranet, or a list of software update points that allow Internet and intranet client connections.  

-   **Internet-based clients**: Receive a list of software update points that you configure to allow connections only from the Internet, or a list of software update points that allow Internet and intranet client connections.  

###  <a name="BKMK_SUPSwitching"></a> Software update point switching  
 If you have multiple software update points at a site, and then one fails or becomes unavailable, clients will connect to a different software update point and continue to scan for the latest software updates. When a client is first assigned a software update point, it will stay assigned to that software update point unless it fails to scan for software updates on that software update point.  

 The scan for software updates can fail with a number of different retry and non-retry error codes. When the scan fails with a retry error code, the client starts a retry process to scan for the software updates on the software update point. The high-level conditions that result in a retry error code are typically because the WSUS server is unavailable or because it is temporarily overloaded. The client uses the following process when it fails to scan for software updates:  

1.  The client scans for software updates at its scheduled time, or when it is initiated through the control panel on the client, or by using the SDK. If the scan fails, the client waits 30 minutes to retry the scan, and it uses the same software update point.  

2.  The client retries a minimum of four times at 30 minute intervals. After the fourth failure, and after it waits an additional two minutes, the client will move to the next software update point in the software update point list.  

3.  After a successful scan, the client will continue to connect to the software update point.  

 The following list provides additional information that you can consider for software update point retry and switching scenarios:  

-   If a client is disconnected from the corporate intranet and fails to scan for software updates, it will not switch to another software update point. This is an expected failure, because the client cannot reach the corporate network or the software update point that allows connection from the intranet. The Configuration Manager client determines the availability of the intranet software update point.  

-   If Internet-based client management is enabled, and there are multiple software update points that are configured to accept communication from clients on the Internet, the switching process will follow the standard retry process that is described in the previous scenario.  

-   If the scan process started, but the client was powered down before the scan completed, it is not considered a scan failure and it does not count as one of the four retries.  

###  <a name="BKMK_ManuallySwitchSUPs"></a>Manually switching clients to a new software update point
Beginning in Configuration Manager version 1606, you can enable the option for Configuration Manager clients to switch to a new software update point when there are issues with the active software update point. This option results in changes only when a client receives multiple software update points from a management point.  

Enable this option on a device collection or on a set of selected devices. Once enabled, the clients will look for another software update point at the next scan. Depending on your WSUS configuration settings (update classifications, products, whether the software update points share a WSUS database, etc.), the switch to a new software update point will generate additional network traffic. Therefore, you should only use this option when necessary.  

#### To enable the option to switch software update points  

1.  In the Configuration Manager console, go to **Assets and Compliance > Overview > Device collections**.  

2.  On the **Home** tab, in the **Collection** group, click **Client Notification**, and then click **Switch to Next Software Update Point**.  


###  <a name="BKMK_SUP_CrossForest"></a> Software update points in an untrusted forest  
 You can create one or more software update points at a site to support clients in an untrusted forest. To add a software update point in another forest, you must first install and configure a WSUS server in the forest. Then start the wizard to add a Configuration Manager site server with the software update point site system role. In the wizard, configure the following settings to successfully connect to WSUS in the untrusted forest:  

-   Specify a Site System Installation account that can access the WSUS server in the forest.  

-   Specify the WSUS Server Connection account to use to connect to the WSUS server.  

 For example, you have a primary site in forest A with two software update points (SUP01 and SUP02). Also, for the same primary site you have two software update points (SUP03 and SUP04) in forest B. When the switching occurs in this example, the software update points from the same forest as the client are prioritized first.  

###  <a name="BKMK_WSUSSyncSource"></a> Use an existing WSUS server as the synchronization source at the Top-level site  
 Typically, the top-level site in your hierarchy is configured to synchronize software updates metadata with Microsoft Update. When your corporate security policy does not allow access to the Internet from the top-level site, you can configure the synchronization source for the top-level site to use an existing WSUS server that is not in your Configuration Manager hierarchy. For example, you might have a WSUS server installed in your DMZ that has Internet access, but your top-level site does not. You can configure the WSUS server in the DMZ as your synchronization source for software updates metadata. You must ensure that the WSUS server in the DMZ synchronizes software updates that meet the criteria that you need in your Configuration Manager hierarchy. Otherwise, the top-level site might not synchronize the software updates that you expect. When you install the software update point, configure a WSUS connection account that has access to the WSUS server in the DMZ and confirm that the firewall permits traffic for the appropriate ports. For more information about the ports that are used by the software update point to the synchronization source, see the [Software Update Point -- &gt; Upstream WSUS Server](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS) section in the [Ports used in System Center Configuration Manager](../../core/plan-design/hierarchy/ports.md) topic.  

###  <a name="BKMK_NLBSUPSP1"></a> Software update point configured to use an NLB  
 Software update point switching will likely address the fault tolerance needs that you have. However, NLB is more robust than software update point failover for pure load balancing, and NLB can increase the reliability and performance of a network. Though there is no option in the Configuration Manager console to configure the software update point to use NLB, you have the option to configure NLB by using the Set-CMSoftwareUpdatePoint PowerShell cmdlet. For more information about the Set-CMSoftwareUpdatePoint PowerShell cmdlet, see the [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834)  

###  <a name="BKMK_SUPSecSite"></a> Software update point on a secondary site  
 The software update point is optional on a secondary site. When you install a software update point on a secondary site, the WSUS database is configured as a replica of the default software update point at the parent primary site. You can install only one software update point at a secondary site. The devices that are assigned to a secondary site are configured to use a software update point at the parent site when a software update point is not installed at the secondary site. Typically, you will install a software update point at a secondary site when there is limited network bandwidth between the devices that are assigned to the secondary site and the software update points at the parent primary site, or when the software update point approaches the capacity limit. After a software update point is successfully installed and configured at the secondary site, a site-wide policy is updated for client computers that are assigned to the site, and they will start to use the new software update point.  

