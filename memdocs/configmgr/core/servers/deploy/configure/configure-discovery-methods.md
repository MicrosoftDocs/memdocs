---
title: Configure discovery
titleSuffix: Configuration Manager
description: Configure discovery methods to find resources to manage from your network, Active Directory, and Microsoft Entra ID.
ms.date: 04/25/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure discovery methods for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configure discovery methods to find resources to manage from your network, Active Directory, and Microsoft Entra ID. First enable and then configure each method that you want to use to search your environment. You can also disable a method by using the same procedure that you use to enable it. The only exceptions to this process are Heartbeat Discovery and Server Discovery:  

- By default, **Heartbeat Discovery** is already enabled when you install a Configuration Manager primary site. It's configured to run on a basic schedule. Keep Heartbeat Discovery enabled. It makes sure that the discovery data records (DDRs) for devices are up to date. For more information about Heartbeat Discovery, see [About Heartbeat Discovery](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Server Discovery** is an automatic discovery method. It finds computers that you use as site systems. You can't configure or disable it.  

## <a name="BKMK_ConfigADForestDisc"></a> Active Directory Forest Discovery  

To finish the configuration of Active Directory Forest Discovery, configure settings in the following locations of the Configuration Manager console:  

- In the **Discovery Methods** node:

  - Enable this discovery method.  

  - Set a polling schedule.  

  - Select whether discovery automatically creates boundaries for the Active Directory sites and subnets that it discovers.  

- In the **Active Directory Forests** node:

  - Add forests that you want to discover.  

  - Enable discovery of Active Directory sites and subnets in that forest.  

  - Configure settings that enable Configuration Manager sites to publish their site information to the forest.  

  - Assign an account to use as the Active Directory Forest Account for each forest.  

Use the following procedures to enable Active Directory Forest Discovery, and to configure individual forests for use with Active Directory Forest Discovery.  

### Configure Active Directory Forest Discovery  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Discovery Methods** node.  

2. Select the Active Directory Forest Discovery method for the site where you want to configure discovery.  

3. On the **Home** tab of the ribbon, select **Properties**.  

4. On the **General** tab of the properties, configure the following settings:  

    - Enable the discovery method.

    - Specify options to create site boundaries for discovered locations.  

    - Specify a schedule for when discovery runs.  

5. Select **OK** to save the configuration.  

### Configure a forest for Active Directory Forest Discovery  

1. In the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Active Directory Forests** node. If Active Directory Forest Discovery has previously run, you see each discovered forest in the results pane. When this discovery method runs, it discovers the local forest and any trusted forests. Manually add untrusted forests.  

    - To configure a previously discovered forest, select the forest in the results pane. In the ribbon, select **Properties** to open the forest properties.

    - To configure a new forest that isn't listed, on the **Home** tab of the ribbon, in the **Create** group, select **Add Forest**. This action opens the **Add Forests** dialog box.

2. On the **General** tab, finish configurations for the forest that you want to discover, and specify the **Active Directory Forest Account**. For more information on this account, see [Accounts](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Active Directory Forest Discovery requires a global account to discover and publish to untrusted forests. If you don't use the computer account of the site server, you can only select a global account.  

3. If you plan to let sites publish site data to this forest, on the **Publishing** tab, finish configurations for publishing to this forest.  

    > [!NOTE]  
    > If you let sites publish to a forest, extend the Active Directory schema of that forest for Configuration Manager. The Active Directory Forest Account must have Full Control permissions to the System container in that forest.  

4. Select **OK** to save the configuration.  


## <a name="BKMK_ConfigADDiscGeneral"></a> Active Directory discovery for computers, users, or groups  

To configure discovery of computers, users, or groups, start with these common steps:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Discovery Methods** node.  

2. Select the method for the site where you want to configure discovery.  

3. On the **Home** tab of the ribbon, select **Properties**.  

4. On the **General** tab of the properties, select the checkbox to enable discovery. Or you can configure discovery now, and then return to enable discovery later.  

Then use the information in the following sections to configure the specific discovery methods:  

- [Active Directory Group Discovery](#bkmk_config-adgd)  

- [Active Directory System Discovery](#bkmk_config-adsd)  

- [Active Directory User Discovery](#bkmk_config-adud)  

> [!NOTE]  
> The information in this section doesn't apply to Active Directory Forest Discovery.  

Although each of these discovery methods is independent of the others, they share similar options. For more information about these configuration options, see [Shared options for group, system, and user discovery](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> The Active Directory polling by each of these discovery methods can generate significant network traffic. Consider scheduling each discovery method to run at a time when this network traffic doesn't adversely affect business uses of your network.  

### <a name="bkmk_config-adgd"></a> Configure Active Directory Group Discovery  

1. On the **General** tab of the Active Directory Group Discovery Properties window, select **Add** to configure a discovery scope. Select either **Groups** or **Location**. Then finish the following configurations in the **Add Groups** or **Add Active Directory Location** dialog box:  

    1. Specify a **Name** for this discovery scope.  

    2. Specify an **Active Directory Domain** or **Location** to search:  

        - If you chose **Groups**, specify one or more Active Directory groups to discover.  

        - If you chose **Location**, specify an Active Directory container as a location to discover. You can also enable a recursive search of Active Directory child containers for this location.  

    3. Specify the **Active Directory Group Discovery Account** that the site uses to search this discovery scope. For more information, see [Accounts](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Select **OK** to save the discovery scope configuration.  

2. Repeat the previous steps for each other discovery scope that you want to define.  

3. On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.

4. On the **Options** tab, configure settings to filter out or exclude stale computer records from discovery. Also configure the discovery of the membership of distribution groups.  

    > [!NOTE]  
    > By default, Active Directory Group Discovery discovers only the membership of security groups.
    > Even if selecting the checkbox, Configuration Manager doesn't discover the Distribution Group itself but its members and populates **Distribution group - members relations** in the database.

5. Select **OK** to save the configuration.  

### <a name="bkmk_config-adsd"></a> Configure Active Directory System Discovery  

1. On the **General** tab of the Active Directory System Discovery Properties window, select the **New** icon ![New icon](media/Disc_new_Icon.gif) to specify a new Active Directory container. In the **Active Directory Container** dialog box, finish the following configurations:  

    1. Type or browse to a location for the **Path**. This value is a valid LDAP path to a container or organizational unit (OU). The site queries this path for resources. For example, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Specify options that change the search behavior:  

        - **Discover objects within Active Directory groups**: The site also looks at the membership of groups in this path.  

        - **Recursively search Active Directory child containers**: If you enable this option, the site searches any other containers or OUs within the above path. If you disable this option, the site only searches for resources in the specific path.  

          Select subcontainers to exclude from this recursive search. This option helps to reduce the number of discovered objects. Select **Add** to choose the containers under the above path. In the Select New Container dialog box, select a child container to exclude. Select **OK** to close the Select New Container dialog box.<!--1358143-->

          > [!Tip]  
          > - The list of Active Directory containers in the Active Directory System Discovery Properties window includes a column **Has Exclusions**. When you select containers to exclude, this value is **Yes**.
          > - Starting in version 2203, you can exclude subcontainers in untrusted domains for **Active Directory System Discovery** and **Active Directory User Discovery**. 
  

    3. For each location, specify the account to use as the **Active Directory Discovery Account**. For more information, see [Accounts](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > For each specified location, you can configure a set of discovery options and a unique Active Directory Discovery Account.  

    4. Select **OK** to save the Active Directory container configuration.  

2. On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.  

3. On the **Active Directory Attributes** tab, configure other Active Directory attributes for computers that you want to discover. This tab lists the default object attributes.  

    > [!Tip]  
    > For example, your organization uses the **Description** attribute on the computer account in Active Directory. Select **Custom**, and add `Description` as a custom attribute. After this discovery method runs, this attribute shows on the device Properties tab in the Configuration Manager console.<!--513948-->  

4. On the **Options** tab, configure settings to filter out or exclude stale computer records from discovery.  

5. Select **OK** to save the configuration.  

### <a name="bkmk_config-adud"></a> Configure Active Directory User Discovery  

1. On the **General** tab of the Active Directory User Discovery Properties window, select the **New** icon ![New icon](media/Disc_new_Icon.gif) to specify a new Active Directory container. In the **Active Directory Container** dialog box, finish the following configurations:  

    1. Specify one or more locations to search.  

    2. For each location, specify options that change the search behavior.  

    3. For each location, specify the account to use as the **Active Directory Discovery Account**. For more information, see [Accounts](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > For each specified location, you can configure a unique set of discovery options and a unique Active Directory Discovery Account.  

    4. Select **OK** to save the Active Directory container configuration.  

2. On the **Polling Schedule** tab, configure both the full discovery polling schedule and delta discovery.  

3. On the **Active Directory Attributes** tab, configure other Active Directory attributes for computers that you want to discover. This tab lists the default object attributes.  

4. Select **OK** to save the configuration.  

#### Exclude organizational units (OU) from Active Directory User Discovery
<!--5193509-->
Starting in version 2103, you can exclude OUs from Active Directory User Discovery. To exclude an OU:

1. From the Configuration Manager console, go to **Administration** > **Hierarchy Configuration** > **Discovery Methods**.

1. Select **Active Directory User Discovery** then select **Properties** from the ribbon.

1. On the **General** tab of the Active Directory User Discovery Properties window, select the **New** icon to specify a new Active Directory container or **Edit** to change an existing one.

1. In the **Active Directory Container** dialog box, locate the search option named **Select sub containers to be excluded from discovery**.

1. Select **Add** to add an exclusion or **Remove** to remove an existing exclusion.

1. Select **OK** to save the Active Directory container configuration.

> [!TIP]
> Starting in version 2203, you can exclude subcontainers in untrusted domains for **Active Directory System Discovery** and **Active Directory User Discovery**.

## <a name="azureaadisc"></a> Microsoft Entra user Discovery

Microsoft Entra user Discovery isn't enabled or configured the same as other discovery methods. Configure it when you onboard the Configuration Manager site to Microsoft Entra ID.

For more information, see [Microsoft Entra user Discovery](about-discovery-methods.md#azureaddisc).

<a name='prerequisites-for-azure-ad-user-discovery'></a>

### Prerequisites for Microsoft Entra user Discovery

To enable and configure this discovery method, [Configure Azure Services](azure-services-wizard.md) for **Cloud Management**.

If you use Configuration Manager to *create* the Azure app, it configures the app with the necessary permissions.

If you create the app in Azure first, and then *import* it into Configuration Manager, you need to manually configure the app. This configuration includes granting the server app permission to read directory data.

1. Open the [Azure portal](https://portal.azure.com) as a user with *Global Admin* permissions. Go to **Microsoft Entra ID**, and select **App registrations**. Switch to **All applications** if necessary.

1. Select the target application.

1. In the **Manage** menu, select **API permissions**.  

    1. On the **API permissions** panel, select **Add a permission**.  

    2. In the **Request API permissions** panel, switch to **APIs my organization uses**.  

    3. Search for and select the **Microsoft Graph** API.  

    4. Select the **Application permissions** group. Expand **Directory**, and select **Directory.Read.All**.  

    5. Select **Add permissions**.  

1. On the **API permissions** panel, in the **Grant consent** section, select **Grant admin consent...**. Select **Yes**.  

<a name='configure-azure-ad-user-discovery'></a>

### Configure Microsoft Entra user Discovery

When configuring the **Cloud Management** Azure service:

- On the **Discovery** page of the wizard, select the option to **Enable Microsoft Entra user Discovery**.
- Select **Settings**.
- In the Microsoft Entra user Discovery Settings dialog box, configure a schedule for when discovery occurs. You can also enable delta discovery, which only checks for new or changed accounts in Microsoft Entra ID.

> [!Note]  
> If the user is a federated or synchronized identity, you must use Configuration Manager [Active Directory user discovery](about-discovery-methods.md#bkmk_aboutUser) as well as Microsoft Entra user discovery. For more information about hybrid identities, see [Define a hybrid identity adoption strategy](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="bkmk_azuregroupdisco"></a> Microsoft Entra user Group Discovery

<!--3611956-->

You can discover user groups and members of those groups from Microsoft Entra ID. When the site finds users in Microsoft Entra groups that it hasn't previously discovered, it adds them as new user resources in Configuration Manager. A user group resource record is created when the group is a security group.

<a name='prerequisites-for-azure-ad-user-group-discovery'></a>

### Prerequisites for Microsoft Entra user Group Discovery

- Cloud Management [Azure service](azure-services-wizard.md)
- Permission to read and search Microsoft Entra groups

### Log files

Use the SMS_AZUREAD_DISCOVERY_AGENT.log for troubleshooting. This log is also shared with Microsoft Entra user discovery. For more information, see [Log files](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

<a name='enable-azure-ad-user-group-discovery'></a>

### Enable Microsoft Entra user group discovery

To enable discovery on an existing **Cloud Management** Azure service:

1. Go to the **Administration** workspace, expand **Cloud Services**, then select the **Azure Services** node.
1. Select one of your Azure services, then select **Properties** in the ribbon.
1. In the **Discovery** tab, check the box to **Enable Microsoft Entra group Discovery**, then select **Settings**.
1. Select **Add** under the **Discovery Scopes** tab.
    - You can modify the **Polling Schedule** in the other tab.
1. Select one or more user groups. You can **Search** by name.
    - You'll be prompted to sign in to Azure when you select **Search** the first time.
1. Select **OK** when you finish selecting groups.
1. Once discovery finishes running, you can browse your Microsoft Entra user groups in the **Users** node.

To enable discovery when configuring a new **Cloud Management** Azure service:

- On the **Discovery** page of the wizard, select the option to **Enable Microsoft Entra group Discovery**.
- Select **Settings**.
- In the Microsoft Entra group Discovery Settings dialog box, configure your discovery scope and a schedule for when discovery occurs.


## <a name="BKMK_ConfigHBDisc"></a> Heartbeat Discovery

Configuration Manager enables the Heartbeat Discovery method when you install a primary site. If you want to use the default schedule of every seven days, there's nothing else to configure. Otherwise, you only have to configure the schedule for how often clients send the Heartbeat Discovery data record to a management point.  

> [!NOTE]  
> If you enable both client push installation and the site maintenance task for **Clear Install Flag** at the same site, set the schedule of Heartbeat Discovery to be less than the **Client Rediscovery period** of the **Clear Install Flag** site maintenance task. By default, this task runs every 21 days. Heartbeat discovery should run more frequently than the task, or clients will unnecessarily reinstall. For more information about site maintenance tasks, see [Maintenance tasks](../../manage/maintenance-tasks.md).<!-- 7355291 -->

### Configure the Heartbeat Discovery schedule  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Discovery Methods** node.  

2. Select the **Heartbeat Discovery** method for the site where you want to configure Heartbeat Discovery.  

3. On the **Home** tab of the ribbon, select **Properties**.  

4. Configure the frequency with which clients submit a Heartbeat discovery data record. Then select **OK** to save the configuration.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="BKMK_ConfigNetworkDisc"></a> Network Discovery  

Before you configure Network Discovery, understand the following topics:  

- Available levels of Network Discovery  

- Available Network Discovery options  

- Limiting Network Discovery on the network  
 
For more information, see [About Network Discovery](about-discovery-methods.md#bkmk_aboutNetwork).  

The following sections provide information about common configurations for Network Discovery. You can configure one or more of these configurations for use during the same discovery run. If you use multiple configurations, plan for the interactions that can affect the discovery results.  

For example, you discover all Simple Network Management Protocol (SNMP) devices that use a specific SNMP community name. For the same discovery run, you disable discovery on a specific subnet. When discovery runs, Network Discovery doesn't discover the SNMP devices with the specified community name on the subnet that you've disabled.  

### <a name="BKMK_DetermineNetTopology"></a> Determine your network topology  

You can use a topology-only discovery to map your network. This kind of discovery doesn't discover potential clients. The topology-only Network Discovery relies on SNMP.  

When you're mapping your network topology, configure the **Maximum hops** on the **SNMP** tab in the **Network Discovery Properties** dialog box. Just a few hops can help control the network bandwidth that's used when discovery runs. As you discover more of your network, increase the number of hops to gain a better understanding of your network topology.  

After you understand your network topology, configure the properties for Network Discovery. These properties help to discover potential clients and their operating systems. Also configure Network Discovery to limit the network segments that it can search.  

For more information, see [How to determine your network topology](#bkmk_proc-top)

### Network Discovery search options

Configuration Manager supports the following methods to search the network:

- [Limit searches by using subnets](#BKMK_LimitBySubnet)
- [Search a specific domain](#BKMK_SearchByDomain)
- [Limit searches by using SNMP community names](#BKMK_LimitBySNMPname)
- [Search a specific DHCP server](#BKMK_SearchByDHCP)

#### <a name="BKMK_LimitBySubnet"></a> Limit searches by using subnets  

You can configure Network Discovery to search specific subnets during a discovery run. By default, Network Discovery searches the subnet of the server that runs discovery. Any other subnets that you configure and enable apply only to SNMP and DHCP search options. When Network Discovery searches domains, it isn't limited by configurations for subnets.  

If you specify one or more subnets on the **Subnets** tab in the **Network Discovery Properties** dialog box, it only searches the subnets that you mark as **Enabled**.  

When you disable a subnet, the site excludes it from discovery, and the following conditions apply:  

- SNMP-based queries don't run on the subnet.  

- DHCP servers don't reply with a list of resources located on the subnet.  

- Domain-based queries can discover resources that are located on the subnet.  

#### <a name="BKMK_SearchByDomain"></a> Search a specific domain  

You can configure Network Discovery to search a specific domain or set of domains during a discovery run. By default, Network Discovery searches the local domain of the server that runs discovery.  

If you specify one or more domains on the **Domains** tab in the **Network Discovery Properties** dialog box, it only searches the domains that you mark as **Enabled**.  

When you disable a domain, the site excludes it from discovery, and the following conditions apply:  

- Network Discovery doesn't query domain controllers in that domain.  

- SNMP-based queries can still run on subnets in the domain.  

- DHCP servers can still reply with a list of resources located in the domain.  

#### <a name="BKMK_LimitBySNMPname"></a> Limit searches by using SNMP community names  

You configure Network Discovery to search a specific SNMP community or set of communities during a discovery run. By default, the method configures the **public** community name.  

Network Discovery uses community names to gain access to routers that are SNMP devices. A router can supply Network Discovery with information about other routers and subnets that are linked to the first router.  

> [!NOTE]  
> SNMP community names resemble passwords. Network Discovery can get information only from an SNMP device for which you've specified a community name. Each SNMP device can have its own community name, but often the same community name is shared among several devices. Additionally, most SNMP devices have a default community name of **public**. But some organizations delete the **public** community name from their devices as a security precaution.  

If you include more than one SNMP community on the **SNMP** tab in the **Network Discovery Properties** dialog box, it searches them in the order in which they're shown. Make sure that the most frequently used names are at the top of the list. This configuration helps to minimize network traffic that the site generates when it tries to contact a device by using different names.

> [!NOTE]  
> Along with using the SNMP community name, you can specify the IP address or resolvable name of a specific SNMP device. You do this action on the **SNMP Devices** tab in the **Network Discovery Properties** dialog box.  

#### <a name="BKMK_SearchByDHCP"></a> Search a specific DHCP server  

You can configure Network Discovery to use a specific DHCP server or multiple servers to discover DHCP clients during a discovery run.  

Network Discovery searches each DHCP server that you specify on the **DHCP** tab in the **Network Discovery Properties** dialog box. If the server that's running discovery leases its IP address from a DHCP server, you can configure discovery to search that DHCP server. Enable this behavior with the option to **Include the DHCP server that the site server is configured to use**.  

> [!NOTE]  
> To successfully configure a DHCP server in Network Discovery, your environment must support IPv4. You can't configure Network Discovery to use a DHCP server in a native IPv6 environment.  

### <a name="BKMK_HowToConfigNetDisc"></a> How to configure Network Discovery  

Use the following procedures to first discover only your network topology, and then to configure Network Discovery to discover potential clients by using one or more of the available Network Discovery options.  

#### <a name="bkmk_proc-top"></a> How to determine your network topology  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Discovery Methods** node.  

2. Select the **Network Discovery** method for the site where you want to discover network resources.  

3. On the **Home** tab of the ribbon, select **Properties**.  

    - On the **General** tab, select the option to **Enable network discovery**. Then select **Topology** from the **Type of discovery** options.  

    - On the **Subnets** tab, select the **Search local subnets** option.  

      > [!TIP]  
      > If you know the specific subnets that constitute your network, deselect the **Search local subnets** checkbox. Then select the **New** icon ![New icon](media/Disc_new_Icon.gif), and add the specific subnets that you want to search. For large networks, search only one or two subnets at a time to minimize the use of network bandwidth.  

    - On the **Domains** tab, select the option to **Search local domain**.  

    - On the **SNMP** tab, select an option from the **Maximum hops** drop-down list. This option specifies how many router hops Network Discovery can take in mapping your topology.  

      > [!TIP]  
      > When you first map your network topology, configure just a few router hops to minimize the use of network bandwidth.  

4. On the **Schedule** tab, select the **New** icon ![New icon](media/Disc_new_Icon.gif), and set a schedule for running discovery. The **Duration** is the period of time that Network Discovery has to complete the search for resources. On smaller subnets, an hour may be enough, but searching across an enterprise network with multiple router hops will take longer. If Network Discovery runs out of time, a message is logged in **Netdisc.log**.

    > [!NOTE]  
    > You can't assign a different discovery configuration to separate Network Discovery schedules. Each time Network Discovery runs, it uses the current discovery configuration.  

5. Select **OK** to accept the configurations. Network Discovery runs at the scheduled time.  


#### <a name="bkmk_proc-config"></a> How to configure Network Discovery  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Discovery Methods** node.  

2. Select the **Network Discovery** method for the site where you want to discover network resources.  

3. On the **Home** tab of the ribbon, select **Properties**.  

4. On the **General** tab, select the option to **Enable network discovery**.  

    - Select from the **Type of discovery** options the type of discovery that you want to run.  

    - Enable the **Slow network** option for Configuration Manager to make automatic adjustments for low-bandwidth networks.  

5. To configure discovery to search subnets, switch to the **Subnets** tab. Then configure one or more of the following options:  

    - To run discovery on subnets that are local to the computer that runs discovery, enable the option to **Search local subnets**.  

    - To search a specific subnet, make sure that the subnet is listed in **Subnets to search** and has a **Search** value of **Enabled**:  

      1. If the subnet isn't listed, select the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New Subnet Assignment** dialog box, enter the **Subnet** and **Mask** information, and then select **OK**. By default, a new subnet is enabled for search.  

      2. To change the **Search** value for a listed subnet, select it in the list. Then select the **Toggle** icon to switch the value between **Disabled** and **Enabled**.  

6. To configure discovery to search domains, switch to the **Domains** tab. Then configure one or more of the following options:  

    - To run discovery on the domain of the computer that runs discovery, enable the option to **Search local domain**.  

    - To search a specific domain, make sure that the domain is listed in **Domains** and has a **Search** value of **Enabled**:  

      1. If the domain isn't listed, select the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **Domain Properties** dialog box, enter the **Domain** information, and then select **OK**. By default, a new domain is enabled for search.  

      2. To change the **Search** value for a listed domain, select it in the list. Then select the **Toggle** icon to switch the value between **Disabled** and **Enabled**.  

7. To configure discovery to search specific SNMP community names for SNMP devices, switch to the **SNMP** tab. Then configure one or more of the following options:  

    - To add an SNMP community name to the list of **SNMP Community names**, select the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New SNMP Community Name** dialog box, specify the **Name** of the SNMP community, and then select **OK**.  

    - To remove an SNMP community name, select the community name, and then select the **Delete** icon ![Delete icon](media/Disc_delete_Icon.gif).  

    - To adjust the search order of SNMP community names, select a community name from the list. Then select the **Move Item Up** icon ![Move UP Icon](media/Disc_moveUp_Icon.gif) or the **Move Item Down** icon ![Move Down Icon](media/Disc_moveDown_Icon.gif). When discovery runs, community names are searched in a top-to-bottom order. 

    - To configure the maximum number of router hops for use by SNMP searches, select the number of hops from the **Maximum hops** drop-down list.  

8. To configure an SNMP device, switch to the **SNMP Devices** tab. If the device isn't listed, select the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New SNMP Device** dialog box, specify the IP address or device name of the SNMP device, and then select **OK**.  

    > [!NOTE]  
    > If you specify a device name, Configuration Manager must be able to resolve the NetBIOS name to an IP address.  

9. To configure discovery to query specific DHCP servers, switch to the **DHCP** tab. Then configure one or more of the following options:  

    - To query the DHCP server on the computer that is running discovery, enable the option to **Always use the site server's DHCP server**.  

      > [!NOTE]  
      > To use this option, the server must lease its IP address from a DHCP server and can't use a static IP address.  

    - To query a specific DHCP server, select the **New** icon ![New icon](media/Disc_new_Icon.gif). In the **New DHCP Server** dialog box, specify the IP address or server name of the DHCP server, and then select **OK**.  

      > [!NOTE]  
      > If you specify a server name, Configuration Manager must be able to resolve the NetBIOS name to an IP address.  

10. To configure when discovery runs, switch to the **Schedule** tab. Then select the **New** icon ![New icon](media/Disc_new_Icon.gif) to set a schedule for running Network Discovery. You can configure multiple recurring schedules, and multiple schedules that have no recurrence.  

    > [!NOTE]  
    > If the **Schedule** tab shows more than one schedule at the same time, Network Discovery runs for all schedules as it's configured at the time indicated in the schedule. This behavior is also true for recurring schedules.  

11. Select **OK** to save your configurations.  

### <a name="BKMK_HowToVerifyNetDisc"></a> How to verify that Network Discovery has finished  

The time that Network Discovery requires to finish can vary depending on one or more of the following factors:  

- The size of your network  

- The topology of your network  

- The maximum number of hops that are configured to find routers in the network  

- The type of discovery that is being run  

Network Discovery doesn't create messages to alert you when it's finished. Use the following procedure to verify when discovery has finished:  

1. In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and then select the **Status Message Queries** node.  

2. Select the **All Status Messages** query.  

3. On the **Home** tab of the ribbon, in the **Status Message Queries** group, select **Show Messages**.  

4. In the All Status Messages window, select a value from the **Select date and time** drop-down list that includes how long ago the discovery started. Then select **OK** to open the **Configuration Manager Status Message Viewer**.  

    > [!TIP]  
    > You can also use the **Specify date and time** option to select a given date and time that you ran discovery. This option is useful when you ran Network Discovery on a given date and want to retrieve messages from only that date.  

5. To validate that Network Discovery has finished, search for a status message that has the following details:  

    - Message ID: **502**  

    - Component: **SMS_NETWORK_DISCOVERY**  

    - Description: **This component stopped**  

    If this status message isn't present, Network Discovery hasn't finished.  

6. To validate when Network Discovery started, search for a status message that has the following details:  

    - Message ID: **500**  

    - Component: **SMS_NETWORK_DISCOVERY**  

    - Description: **This component started**  

    This information verifies that Network Discovery started. If this information isn't present, reschedule Network Discovery.  
