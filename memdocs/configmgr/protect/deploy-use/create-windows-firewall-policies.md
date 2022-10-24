---
title: Windows Firewall policies for Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to create and deploy firewall policies for Endpoint Protection in System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Create and deploy Windows Firewall policies for Endpoint Protection in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Firewall policies for Endpoint Protection in Configuration Manager let you perform basic Windows Firewall configuration and maintenance tasks on client computers in your hierarchy. You can use Windows Firewall policies to perform the following tasks:  

-   Control whether Windows Firewall is turned on or off.  

-   Control whether incoming connections are allowed to client computers.  

-   Control whether users are notified when Windows Firewall blocks a new program.  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Windows Firewall Policies**.  

3.  On the **Home** tab, in the **Create** group, click **Create Windows Firewall Policy**.  

4.  On the **General** page of the **Create Windows Firewall Policy Wizard**, specify a name and an optional description for this firewall policy, and then click **Next**.  

5.  On the **Profile Settings** page of the wizard, configure the following settings for each network profile:  

    > [!NOTE]  
    >  For more information about network profiles, see the Windows documentation.  

    -   **Enable Windows Firewall**  

        > [!NOTE]  
        >  If **Enable Windows Firewall** is not enabled, the other settings on this page of the wizard are unavailable.  

    -   **Block all incoming connections, including those in the list of allowed programs**  

    -   **Notify the user when Windows Firewall blocks a new program**  

6.  On the **Summary** page of the wizard, review the actions to be taken, and then complete the wizard.  

7.  Verify that the new Windows Firewall policy is displayed in the **Windows Firewall Policies** list.  

##  <a name="BKMK_Assign"></a> To deploy a Windows Firewall policy  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Windows Firewall Policies**.  

3.  In the **Windows Firewall Policies** list, select the Windows Firewall policy that you want to deploy.  

4.  On the **Home** tab, in the **Deployment** group, click **Deploy**.  

5.  In the **Deploy Windows Firewall Policy** dialog box, specify the collection to which you want to assign this Windows Firewall policy, and specify an assignment schedule. The Windows Firewall policy evaluates for compliance by using this schedule and the Windows Firewall settings on clients to reconfigure to match the Windows Firewall policy.  

6.  Click **OK** to close the **Deploy Windows Firewall Policy** dialog box and to deploy the Windows Firewall policy.  

    > [!IMPORTANT]  
    >  When you deploy a Windows Firewall policy to a collection, this policy is applied to computers in a random order over a 2 hour period to avoid flooding the network.
