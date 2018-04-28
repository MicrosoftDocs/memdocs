---
title: Configure discovery
titleSuffix: Configuration Manager
description: Configure discovery methods to find resources to manage from your network, Active Directory, and Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configure discovery methods for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Configure discovery methods to find resources to manage from your network, Active Directory, and Azure Active Directory (Azure AD). First enable and then configure each method that you want to use to search your environment. You can also disable a method by using the same procedure that you use to enable it. The only exceptions to this process are Heartbeat Discovery and Server Discovery:  

-   By default, **Heartbeat Discovery** is already enabled when you install a Configuration Manager primary site. It is configured to run on a basic schedule. Keep Heartbeat Discovery enabled. It ensures that the discovery data records (DDRs) for devices are up-to-date. For more information about Heartbeat Discovery, see [About Heartbeat Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   **Server Discovery** is an automatic discovery method. It finds computers that you use as site systems. You can't configure or disable it.  

### Enable a configurable discovery method  
 > [!NOTE]  
 > The following information doesn't apply to Azure AD User Discovery. Instead, see [Configure Azure AD User Discovery](#azureaadisc) later in this article.

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and then select **Discovery Methods**.  

2.  Select the discovery method for the site where you want to enable discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**. Then on the **General** tab, check the **Enable &lt;discovery method\>** box.  

     If this box is already checked, you can disable the discovery method by unchecking the box.  

4.  Choose **OK** to save the configuration.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configure Active Directory Forest Discovery  
To finish the configuration of Active Directory Forest Discovery, you must configure settings in two locations:  

-   In the **Discovery Methods** node, you can:

    - Enable this discovery method.
    - Set a polling schedule.
    - Select whether discovery automatically creates boundaries for the Active Directory sites and subnets that it discovers.  

-   In the **Active Directory Forests** node, you can:

    - Add forests that you want to discover.
    - Enable discovery of Active Directory sites and subnets in that forest.
    - Configure settings that enable Configuration Manager sites to publish their site information to the forest.
    - Assign an account to use as the Active Directory Forest Account for each forest.  

Use the following procedures to enable Active Directory Forest Discovery, and to configure individual forests for use with Active Directory Forest Discovery.  

#### To enable Active Directory Forest Discovery  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Select the Active Directory Forest Discovery method for the site where you want to configure discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  On the **General** tab, check the box to enable discovery. Or you can configure discovery now, and then return to enable discovery later.  

5.  Specify options to create site boundaries for discovered locations.  

6.  Specify a schedule for when discovery runs.  

7.  When you finish the configuration of Active Directory Forest Discovery for this site, choose **OK** to save the configuration.  

#### To configure a forest for Active Directory Forest Discovery  

1.  In the **Administration** workspace, choose **Active Directory Forests**. If Active Directory Forest Discovery has previously run, you see each discovered forest in the results pane. The local forest and any trusted forests are discovered when Active Directory Forest Discovery runs. Only untrusted forests must be manually added.  

    -   To configure a previously discovered forest, select the forest in the results pane. Then on the **Home** tab, in the **Properties** group, choose **Properties** to open the forest properties. Continue with step 3.  

    -   To configure a new forest that is not listed, on the **Home** tab, in the **Create** group, choose **Add Forest** to open the **Add Forests** dialog box. Continue with step 3.  

2.  On the **General** tab, finish configurations for the forest that you want to discover, and specify the **Active Directory Forest Account**.  

    > [!NOTE]  
    >  Active Directory Forest Discovery requires a global account to discover and publish to untrusted forests. If you don't use the computer account of the site server, you can select only a global account.  

3.  If you plan to let sites publish site data to this forest, on the **Publishing** tab, finish configurations for publishing to this forest.  

    > [!NOTE]  
    >  If you let sites publish to a forest, you must extend the Active Directory schema of that forest for Configuration Manager. The Active Directory Forest Account must have Full Control permissions to the System container in that forest.  

4.  When you finish the configuration of this forest for use with Active Directory Forest Discovery, choose **OK** to save the configuration.  



##  <a name="BKMK_ConfigADDiscGeneral"></a> Configure Active Directory Discovery for computers, users, or groups  
 To configure discovery of computers, users, or groups, use the information in these sections for the following discovery methods:  

-   Active Directory Group Discovery  

-   Active Directory System Discovery  

-   Active Directory User Discovery  

> [!NOTE]  
>  The information in this section doesn't apply to Active Directory Forest Discovery.  

 Although each of these discovery methods is independent of the others, they share similar options. For more information about these configuration options, see [Shared options for Group, System, and User discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  The Active Directory polling by each of these discovery methods can generate significant network traffic. Consider scheduling each discovery method to run at a time when this network traffic doesn't adversely affect business uses of your network.  

#### To configure Active Directory Group Discovery  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Choose the **Active Directory Group Discovery** method for the site where you want to configure discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  On the **General** tab, check the box to enable discovery. Or you can configure discovery now, and then return to enable discovery later.  

5.  Choose **Add** to configure a discovery scope, choose either **Groups** or **Location**, and finish the following configurations in the **Add Groups** or **Add Active Directory Location** dialog box:  

    1.  Specify a **Name** for this discovery scope.  

    2.  Specify an **Active Directory Domain** or **Location** to search:  

        -   If you chose **Groups**, specify one or more Active Directory groups to be discovered.  

        -   If you chose **Location**, specify an Active Directory container as a location to be discovered. You can also enable a recursive search of Active Directory child containers for this location.  

    3.  Specify the **Active Directory Group Discovery Account** that is used to search this discovery scope.  

    4.  Choose **OK** to save the discovery scope configuration.  

6.  Repeat step 6 for each additional discovery scope that you want to define.  

7.  On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.  

8.  Optionally, on the **Option** tab configure options to filter out or exclude stale computer records from discovery. Also configure the discovery of the membership of distribution groups.  

    > [!NOTE]  
    >  By default, Active Directory Group Discovery discovers only the membership of security groups.  

9. When you have finished configuring Active Directory Group Discovery for this site, choose **OK** to save the configuration.  

#### To configure Active Directory System Discovery  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Select the method for the site where you want to configure discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  On the **General** tab, check the box to enable discovery. Or you can configure discovery now, and then return to enable discovery later.  

5.  Choose the **New** icon ![New icon](media/Disc_new_Icon.gif) to specify a new Active Directory container. In the **Active Directory Container** dialog box, finish the following configurations:  

    1.  Specify one or more locations to search.  

    2.  For each location, specify options that change the search behavior.  

    3.  For each location, specify the account to use as the **Active Directory Discovery Account**.  

        > [!TIP]  
        >  For each specified location, you can configure a set of discovery options and a unique Active Directory Discovery Account.  

    4.  Choose **OK** to save the Active Directory container configuration.  

6.  On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.  

7.  Optionally, on the **Active Directory Attributes** tab, you can configure additional Active Directory attributes for computers that you want to discover. The default object attributes are also listed.  

8.  Optionally, on the **Option** tab, you can configure options to filter out or exclude stale computer records from discovery.  

9. When you have finished configuring Active Directory System Discovery for this site, choose **OK** to save the configuration.  

#### To configure Active Directory User Discovery  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Choose the **Active Directory User Discovery** method for the site where you want to configure discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  On the **General** tab, check the box to enable discovery. Or you can configure discovery now, and then return to enable discovery later.  

5.  Choose the **New** icon ![New icon](media/Disc_new_Icon.gif) to specify a new Active Directory container. In the **Active Directory Container** dialog box, finish the following configurations:  

    1.  Specify one or more locations to search.  

    2.  For each location, specify options that change the search behavior.  

    3.  For each location, specify the account to use as the **Active Directory Discovery Account**.  

        > [!NOTE]  
        >  For each specified location, you can configure a unique set of discovery options and a unique Active Directory Discovery Account.  

    4.  Choose **OK** to save the Active Directory container configuration.  

6.  On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.  

7.  Optionally, on the **Active Directory Attributes** tab, you can configure additional Active Directory attributes for computers that you want to discover. The default object attributes are also listed.  

8.  When you have finished configuring Active Directory User Discovery for this site, choose **OK** to save the configuration.  



## <a name="azureaadisc"></a> Configure Azure AD User Discovery
Azure AD User Discovery isn't enabled or configured the same as other discovery methods. Configure it when you onboard the Configuration Manager site to Azure AD. When you [Configure Azure Services](/sccm/core/servers/deploy/configure/azure-services-wizard) for **Cloud Management**, you can also enable and configure this discovery method. 

When configuring the **Cloud Management** Azure service: 
- On the **Discovery** page of the wizard, click **Enable Azure Active Directory User Discovery**. 
- Click **Settings**. 
- In the Azure AD User Discovery Settings dialog box, configure a schedule for when discovery occurs. You can also enable delta discovery, which only checks for new or changed accounts in Azure AD. 

For more information, see [Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Before you *import* the Azure AD app into Configuration Manager, you need to grant the server application permission to read directory data from Azure AD. 
 >  - In the [Azure portal](https://portal.azure.com), go to the **Azure Active Directory** blade. 
 >  - Click **App registrations**, and switch to **All apps** if necessary. 
 >  - Select the server app of type *Web app / API*, and then click **Settings**. 
 >  - Click **Required permissions**, and then click **Grant permissions**.
 >  
 > If you *create* the server app from Configuration Manager, Azure AD automatically creates the permissions with the application. You still need to give consent to the application in the Azure portal.

 > [!Note]  
 > If the user is a federated or synchronized identity, you must use Configuration Manager [Active Directory user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) as well as Azure AD user discovery. For more information about hybrid identities, see [Define a hybrid identity adoption strategy](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configure Heartbeat Discovery  
 By default, Heartbeat Discovery is enabled when you install a Configuration Manager primary site. As a result, you only have to configure the schedule for how often clients send the Heartbeat Discovery data record to a management point when you don't want to use the default of every seven days.  

> [!NOTE]  
>  If both client push installation and the site maintenance task for **Clear Install Flag** are enabled at the same site, set the schedule of Heartbeat Discovery to be less than the **Client Rediscovery period** of the **Clear Install Flag** site maintenance task. For more information about site maintenance tasks, see [Maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### To configure the Heartbeat Discovery schedule  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Choose **Heartbeat Discovery** for the site where you want to configure Heartbeat Discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  Configure the frequency with which clients submit a Heartbeat discovery data record, and then choose **OK** to save the configuration.  



##  <a name="BKMK_ConfigNetworkDisc"></a> Configure Network Discovery  
 To help you configure Network Discovery, use the information in these sections.  

###  <a name="BKMK_AboutConfigNetworkDisc"></a> About configuring Network Discovery  
 Before you configure Network Discovery, you must understand the following topics:  

-   Available levels of Network Discovery  

-   Available Network Discovery options  

-   Limiting Network Discovery on the network  

For more information, see [About Network Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 The following sections provide information about common configurations for Network Discovery. You can configure one or more of these configurations for use during the same discovery run. If you use multiple configurations, you must plan for the interactions that can affect the discovery results.  

 For example, you might want to discover all Simple Network Management Protocol (SNMP) devices that use a specific SNMP community name. Additionally, for the same discovery run, you might disable discovery on a specific subnet. When discovery runs, Network Discovery doesn't discover the SNMP devices with the specified community name on the subnet that you've disabled.  

####  <a name="BKMK_DetermineNetTopology"></a> Determine your network topology  
 You can use a topology-only discovery to map your network. This kind of discovery doesn't discover potential clients. The topology-only Network Discovery relies on SNMP.  

 When you're mapping your network topology, you must configure the **Maximum hops** on the **SNMP** tab in the **Network Discovery Properties** dialog box. Just a few hops can help control the network bandwidth that is used when discovery runs. As you discover more of your network, you can increase the number of hops to gain a better understanding of your network topology.  

 After you understand your network topology, you can configure additional properties for Network Discovery to discover potential clients and their operating systems while you're using available configurations to limit the network segments that Network Discovery can search.  

####  <a name="BKMK_LimitBySubnet"></a> Limit searches by using subnets  
 You can configure Network Discovery to search specific subnets during a discovery run. By default, Network Discovery searches the subnet of the server that runs discovery. Any additional subnets that you configure and enable apply only to SNMP and Dynamic Host Configuration Protocol (DHCP) search options. When Network Discovery searches domains, it isn't limited by configurations for subnets.  

 If you specify one or more subnets on the **Subnets** tab in the **Network Discovery Properties** dialog box, only the subnets that are marked as **Enabled** are searched.  

 When you disable a subnet, it's excluded from discovery, and the following conditions apply:  

-   SNMP-based queries do not run on the subnet.  

-   DHCP servers do not reply with a list of resources located on the subnet.  

-   Domain-based queries can discover resources that are located on the subnet.  

####  <a name="BKMK_SearchByDomain"></a> Search a specific domain  
 You can configure Network Discovery to search a specific domain or set of domains during a discovery run. By default, Network Discovery searches the local domain of the server that runs discovery.  

 If you specify one or more domains on the **Domains** tab in the **Network Discovery Properties** dialog box, only the domains that are marked as **Enabled** are searched.  

 When you disable a domain, it's excluded from discovery, and the following conditions apply:  

-   Network Discovery does not query domain controllers in that domain.  

-   SNMP-based queries can still run on subnets in the domain.  

-   DHCP servers can still reply with a list of resources located in the domain.  

####  <a name="BKMK_LimitBySNMPname"></a> Limit searches by using SNMP community names  
 You configure Network Discovery to search a specific SNMP community or set of communities during a discovery run. By default, the community name of **public** is configured for use.  

 Network Discovery uses community names to gain access to routers that are SNMP devices. A router can supply Network Discovery with information about other routers and subnets that are linked to the first router.  

> [!NOTE]  
>  SNMP community names resemble passwords. Network Discovery can get information only from an SNMP device for which you've specified a community name. Each SNMP device can have its own community name, but often the same community name is shared among several devices. Additionally, most SNMP devices have a default community name of **public**. But some organizations delete the **public** community name from their devices as a security precaution.  

 If multiple SNMP communities are shown on the **SNMP** tab in the **Network Discovery Properties** dialog box, Network Discovery searches them in the order in which they're shown. To help minimize network traffic that is generated by attempts to contact a device by using different names, ensure that the most frequently used names are at the top of the list.  

> [!NOTE]  
>  Along with using the SNMP community name, you can specify the IP address or resolvable name of a specific SNMP device. You do this action on the **SNMP Devices** tab in the **Network Discovery Properties** dialog box.  

####  <a name="BKMK_SearchByDHCP"></a> Search a specific DHCP server  
 You can configure Network Discovery to use a specific DHCP server or multiple servers to discover DHCP clients during a discovery run.  

 Network Discovery searches each DHCP server that you specify on the **DHCP** tab in the **Network Discovery Properties** dialog box. If the server that is running discovery leases its IP address from a DHCP server, you can configure discovery to search that DHCP server by checking the **Include the DHCP server that the site server is configured to use** box.  

> [!NOTE]  
>  To successfully configure a DHCP server in Network Discovery, your environment must support IPv4. You can't configure Network Discovery to use a DHCP server in a native IPv6 environment.  

###  <a name="BKMK_HowToConfigNetDisc"></a> How to configure Network Discovery  
 Use the following procedures to first discover only your network topology, and then to configure Network Discovery to discover potential clients by using one or more of the available Network Discovery options.  

##### To determine your network topology  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Choose **Network Discovery** for the site where you want to run Network Discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

    -   On the **General** tab, check the **Enable network discovery** box, and then choose **Topology** from the **Type of discovery** options.  

    -   On the **Subnets** tab, check the **Search local subnets** box.  

        > [!TIP]  
        >  If you know the specific subnets that constitute your network, uncheck the **Search local subnets** box. Then use the **New** icon ![New icon](media/Disc_new_Icon.gif) to add the specific subnets that you want to search. For large networks, it's often best to search only one or two subnets at a time to minimize the use of network bandwidth.  

    -   On the **Domains** tab, check the **Search local domain** box.  

    -   On the **SNMP** tab, use the **Maximum hops** drop-down list to specify how many router hops Network Discovery can take in mapping your topology.  

        > [!TIP]  
        >  When you first map your network topology, configure just a few router hops to minimize the use of network bandwidth.  

4.  On the **Schedule** tab, choose the **New** icon ![New icon](media/Disc_new_Icon.gif) to set a schedule for running Network Discovery.  

    > [!NOTE]  
    >  You can't assign a different discovery configuration to separate Network Discovery schedules. Each time Network Discovery runs, it uses the current discovery configuration.  

5.  Choose **OK** to accept the configurations. Network Discovery runs at the scheduled time.  

##### To configure Network Discovery  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration**, and then choose **Discovery Methods**.  

2.  Choose **Network Discovery** for the site where you want to run Network Discovery.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  On the **General** tab, check the **Enable network discovery** box, and then select the type of discovery that you want to run from the **Type of discovery** options.  

5.  To configure discovery to search subnets, choose the **Subnets** tab, and then configure one or more of the following options:  

    -   To run discovery on subnets that are local to the computer that runs discovery, check the **Search local subnets** box.  

    -   To search a specific subnet, make sure that the subnet is listed in **Subnets to search** and has a **Search** value of **Enabled**:  

        1.  If the subnet is not listed, choose the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New Subnet Assignment** dialog box, enter the **Subnet** and **Mask** information, and then choose **OK**. By default, a new subnet is enabled for search.  

        2.  To change the **Search** value for a listed subnet, select the subnet, and then choose the **Toggle** icon to switch the value between **Disabled** and **Enabled**.  

6.  To configure discovery to search domains, choose the **Domains** tab, and then configure one or more of the following options:  

    -   To run discovery on the domain of the computer that runs discovery, check the **Search local domain** box.  

    -   To search a specific domain, make sure that the domain is listed in **Domains** and has a **Search** value of **Enabled**:  

        1.  If the domain is not listed, choose the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **Domain Properties** dialog box, enter the **Domain** information, and then choose **OK**. By default, a new domain is enabled for search.  

        2.  To change the **Search** value for a listed domain, select the domain, and then choose the **Toggle** icon to switch the value between **Disabled** and **Enabled**.  

7.  To configure discovery to search specific SNMP community names for SNMP devices, choose the **SNMP** tab, and then configure one or more of the following options:  

    -   To add an SNMP community name to the list of **SNMP Community names**, choose the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New SNMP Community Name** dialog box, specify the **Name** of the SNMP community, and then choose **OK**.  

    -   To remove an SNMP community name, select the community name, and then choose the **Delete** icon ![Delete icon](media/Disc_delete_Icon.gif).  

    -   To adjust the search order of SNMP community names, select a community name, and then choose the **Move Item Up** icon ![Move UP Icon](media/Disc_moveUp_Icon.gif) or the **Move Item Down** icon ![Move Down Icon](media/Disc_moveDown_Icon.gif). When discovery runs, community names are searched in a top-to-bottom order. Keep the following points in mind.

        > [!NOTE]  
        >  Network Discovery uses SNMP community names to gain access to routers that are SNMP devices. A router can inform Network Discovery about other routers and subnets linked to the first router.  

        -   SNMP community names resemble passwords.  

        -   Network Discovery can get information only from an SNMP device for which you have specified a community name.  

        -   Each SNMP device can have its own community name, but often the same community name is shared among several devices.  

        -   Most SNMP devices have a default community name of **Public**. You can use that if you do not know any other community names. However, some organizations delete the **Public** community name from their devices as a security precaution.  

8.  To configure the maximum number of router hops for use by SNMP searches, choose the **SNMP** tab, and then select the number of hops from the **Maximum hops** drop-down list.  

9. To configure an SNMP device, choose the **SNMP Devices** tab. If the device is not listed there, choose the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New SNMP Device** dialog box, specify the IP address or device name of the SNMP device, and then choose **OK**.  

    > [!NOTE]  
    >  If you specify a device name, Configuration Manager must be able to resolve the NetBIOS name to an IP address.  

10. To configure discovery to query specific DHCP servers for DHCP clients, choose the **DHCP** tab, and then configure one or more of the following options:  

    -   To query the DHCP server on the computer that is running discovery, choose to **Always use the site server’s DHCP server**.  

        > [!NOTE]  
        >  To use this option, the server must lease its IP address from a DHCP server and can't use a static IP address.  

    -   To query a specific DHCP server, choose the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New DHCP Server** dialog box, specify the IP address or server name of the DHCP server, and then choose **OK**.  

        > [!NOTE]  
        >  If you specify a server name, Configuration Manager must be able to resolve the NetBIOS name to an IP address.  

11. To configure when discovery runs, choose the **Schedule** tab, and then choose the **New** icon ![New icon](media/Disc_new_Icon.gif) to set a schedule for running Network Discovery.  

     You can configure multiple recurring schedules and multiple schedules that have no recurrence.  

    > [!NOTE]  
    >  If multiple schedules are shown on the **Schedule** tab at the same time, all schedules result in a run of Network Discovery as it is configured at the time indicated in the schedule. This behavior is also true for recurring schedules.  

12. Choose **OK** to save your configurations.  

###  <a name="BKMK_HowToVerifyNetDisc"></a> How to verify that Network Discovery has finished  
 The time that Network Discovery requires to finish can vary depending on one or more of the following factors:  

-   The size of your network  

-   The topology of your network  

-   The maximum number of hops that are configured to find routers in the network  

-   The type of discovery that is being run  

Because Network Discovery doesn't create messages to alert you when discovery has finished, you can use the following procedure to verify when discovery has finished.  

##### To verify that Network Discovery has finished  

1.  In the Configuration Manager console, choose **Monitoring**.  

2.  In the **Monitoring** workspace, expand **System Status**, and then choose **Status Message Queries**.  

3.  Choose **All Status Messages**.  

4.  On the **Home** tab, in the **Status Message Queries** group, choose **Show Messages**.  

5.  In the **Select date and time** drop-down list, select a value that includes how long ago the discovery started, and then choose **OK** to open the **Configuration Manager Status Message Viewer**.  

    > [!TIP]  
    >  You can also use the **Specify date and time** option to select a given date and time that you ran discovery. This option is useful when you ran Network Discovery on a given date and want to retrieve messages from only that date.  

6.  To validate that Network Discovery has finished, search for a status message that has the following details:  

    -   Message ID: **502**  

    -   Component: **SMS_NETWORK_DISCOVERY**  

    -   Description: **This component stopped**  

    If this status message isn't present, Network Discovery hasn't finished.  

7.  To validate when Network Discovery started, search for a status message that has the following details:  

    -   Message ID: **500**  

    -   Component: **SMS_NETWORK_DISCOVERY**  

    -   Description: **This component started**  

    This information verifies that Network Discovery started. If this information isn't present, reschedule Network Discovery.  
