---
title: Policy Spy
titleSuffix: Configuration Manager
description: Use Policy Spy to view and troubleshoot the policy system on Configuration Manager clients.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Policy Spy

*Applies to: Configuration Manager (current branch)*

Policy Spy is one of the [Configuration Manager tools](tools.md). It's a tool for viewing and troubleshooting the policy system on Configuration Manager clients. Run **PolicySpy.exe** to open the user interface. For more information on command-line usage, see [Command-line syntax](#bkmk_policyspy-syntax).

> [!Important]  
> Run Policy Spy as an administrator. If you don't **Run as administrator**, you see the following error in Client Info:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> Command-line syntax

Policy Spy is primarily intended for use through its user interface. It does provide limited command-line options to support automation and batch processing.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### Option: `/export`
This option silently exports the policy of the local or remote computer. `<ExportFilename>` is the file name to which the tool saves the XML exported policy. If you specify the `<computername>` option, Policy Spy exports the policy of that computer instead of the local computer.

> [!Note]  
> This command-line option doesn't provide a way to specify user credentials. To use alternative credentials to access a remote computer, use the **runas** command to open a new command prompt with the required security credentials.  


## Usage

### Tools menu

The following actions are available in the **Tools** menu:  

- **Open Remote**: Connects to the Configuration Manager client policy on a remote computer. Use the Connect dialog box to retrieve the name of the remote computer and optional user credentials. If the connection fails, it displays error information in the Client Info pane. If the connection fails again, try connecting by selecting **Refresh** on the **Edit** menu, or by pressing F5.  

- **Open File**: Opens a policy export file (XML) created by the **Export Policy** option. The tool displays the exported policy exactly the same as a live policy. It disables some features that only apply when you connect to an actual client.  

- **Request Machine Assignments**: Triggers a request for machine policy assignments on the target computer. This feature is disabled when viewing exported policy.  

- **Evaluate Machine Policy**: Triggers a machine policy evaluation on the target computer. This feature is disabled when viewing an exported policy.  

- **Request User Assignments**: Triggers a request for user policy assignments for the currently signed-in user. This feature is only available when viewing a policy on the local computer.  

- **Evaluate User Policy**: Triggers a user policy evaluation for the currently signed-in user. This feature is only available when viewing a policy on the local computer.  

- **Reset Policy**: Removes all non-default policies and resets the policy cookies for the site. It then triggers a request for machine policy assignments. This feature is disabled when viewing an exported policy.  

- **Export Policy**: Exports the target computer's policy to an XML file. View this file on any computer with Policy Spy. To open the export file, select **Open File** on the **Tools** menu. This feature is disabled when viewing an exported policy.  


### Edit menu

The following actions are available in the **Edit** menu:  

- **Delete**: Deletes the instance selected in the Results pane. This action is only supported for policy instances. If you try to delete anything other than policy instances, the tool displays an error message. This feature is disabled when viewing an exported policy.  

- **Refresh**: Refreshes all results to view the latest information. All tree nodes that are expanded before refreshing are automatically expanded afterward. If Policy Spy hasn't successfully connected to the target computer's policy, it tries to connect again. This feature is disabled when viewing an exported policy.  

- **Clear Events**: Clears all items from the Events tab.  



## Results pane

The results pane displays different views of the policy system on the target computer. Access these views by clicking on one of the following four tabs: 
- [Actual](#bkmk_policyspy-actual)
- [Requested](#bkmk_policyspy-requested)
- [Default](#bkmk_policyspy-default)
- [Events](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> Actual

This tab displays the current policy of the client. The current policy determines a client's behavior and the behavior of its client agents, such as software distribution and inventory. The tab displays results in a tree format with a root node for the computer namespace and each user-specific namespace. Expand a namespace node to display a list of classes. Expand a class to display a list of its instances. The class list includes only classes that have instances.


### <a name="bkmk_policyspy-requested"></a> Requested

This tab displays the policy assignments that the client retrieved from its assigned site. The tab displays results in tree format with a root node for the Machine namespace and each user-specific namespace. Expanding a namespace node displays the following nodes:  

- **Configuration**: Displays a list of configuration classes derived from CCM_Policy_Config, which includes policy object, assignments, and others.  

- **Settings**: Displays all active settings generated by policies. Settings are displayed under the Configuration node. 

> [!Note]   
> Multiple instances can exist with the same name because the client hasn't merged these settings into a final resultant set. Policy Spy displays instances under this node by using the RealKey properties instead of their true policy keys. Correlate these instances to the resultant set displayed on the Actual tab.  


### <a name="bkmk_policyspy-default"></a> Default

This tab displays the same information as the **Requested** tab. It also includes contents of the DefaultMachine and DefaultUser namespaces.


### <a name="bkmk_policyspy-events"></a> Events

This tab displays policy agent events as they happen. The view creates a WMI event subscription for all events derived from CCM_PolicyAgent_Event. The view shows a maximum of 200 events. It removes the oldest events from the top of the list, as necessary. If you select the last item in the list, the list automatically scrolls down as it adds new events. Otherwise, the view maintains its current position, and you must scroll down or press the End key to view new events. This view is always empty when viewing an exported policy.



## Client Info pane
The Client Info pane displays a list of properties for the target computer. It displays the following properties, if available:  
- Name
- ID
- Version
- Site
- Assigned MP
- Resident MP
- Proxy MP
- Proxy State



## Details pane
The Details pane displays detailed information about the current selection. If no selection is active, it displays information about Policy Spy itself, including the version. Otherwise, it displays a Manage Object Format (MOF) representation of the selected item.

Policy Spy uses its own MOF-generation routine to create a more user-friendly HTML display than the plain-text MOF generated by WMI. This behavior allows Policy Spy to add the following features to make the MOF more legible:  

- Syntax highlighting  

- Indented objects and arrays  

- Properties are arranged into system, inherited, and local groups. By default, it collapses the system and inherited groups. You can immediately see which properties the instance actually uses.  

- Copy MOF or copy plain-text MOF to the clipboard. This feature is useful for pasting the MOF into other applications by directly calling the MofComp tool.  

For instances of Policy objects derived from CCM_Policy_Policy, the details pane displays the policy body below the MOF that displays. If the client hasn't downloaded the policy body, Policy Spy displays a hyperlink. Click the link to download the policy body directly from the client's management point. If the tool successfully downloads the policy body, it replaces the hyperlink with the contents of the reply. Otherwise, Policy Spy updates the display indicating that the request failed.

