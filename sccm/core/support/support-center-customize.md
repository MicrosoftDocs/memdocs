---
title: Customize Support Center
titleSuffix: Configuration Manager
description: Customize the Support Center configuration file.
ms.date: 11/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Customize Support Center

*Applies to: System Center Configuration Manager (Current Branch)*

The [Support Center](/sccm/core/support/support-center) tool includes a configuration file that you can customize. By default, when you install Support Center, this file is in the following path: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. The configuration file changes the behavior of the program:

  - [Customize data collection](#bkmk_datacoll): Edit the sets of registry keys and WMI namespaces that it includes during data collection  

  - [Customize log groups](#bkmk_loggroups): Define new groups of log files using regular expressions. Also add other log files to log groups.  

  - [Collect additional log files using wildcards](#bkmk_wildcards): Use wildcard searches to collect additional log files  

To make these changes, you need local administrative permissions on the client where you've installed Support Center. Make these customizations using a text or XML editor, such as Notepad or Visual Studio.

> [!Important]  
> The Support Center configuration file is an XML-formatted file. It's essential to the operation of Support Center. Modifying this file is only recommended for users who are familiar with XML and regular expressions.  

Before you customize the Support Center configuration file, save a backup of the original. This backup allows you to recover the original Support Center functionality if you make mistakes while editing the file. If you don’t create a backup, and Support Center doesn't function correctly after you modify the configuration file, reinstall Support Center. You can also copy a configuration file from another installation of Support Center.



## <a name="bkmk_datacoll"></a> Customize data collection

To customize the collection of data on the client, modify the Support Center configuration file using XML elements contained within the `<dataCollectorSettings>` element.


### WMI data collection

The `<CcmWmiDataCollector>` element contains a `<collectionScopes>` element. Use this element to change the WMI namespaces from which Support Center collects data. It also includes an `<ignoreScopes>` element. Use this element to filter out the collection of data from portions of the namespaces defined in the `<collectionScopes>` element.  
    
#### Example
The default configuration file collects data from the `root\ccm` namespace. It includes this path in an `<add/>` element in `<collectionScopes>`. 

It also ignores everything under the `\cimodels`, `\invagt`, `\events`, and `\policy` paths for this namespace. It includes these paths in `<add/>` elements contained within `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### Registry data collection

The `<RegistryDataCollector>` element contains a `<registryKeys>` element. Use this element to change the registry keys and subkeys that Support Center collects under the `HKEY_LOCAL_MACHINE` path. Support Center doesn't support the collection of registry data from other root registry paths.

#### Example
To collect registry keys for the classic programs installed on the device, add the following `<add/>` element in the `<registryKeys>` element: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="bkmk_loggroups"></a> Customize log file groups

To customize which log files Support Center collects, and how it presents them in the **Log groups** list, use elements in the `<logGroups>` element. When you start Support Center, it scans this section of the configuration file. It then creates a group on the **Log groups** list for each unique key attribute value found in the `<add/>` elements contained in the `<logGroups>` element.

  - **Component log group**: The `<componentLogGroup>` element uses a key attribute to define the name of the log group that appears in the list. It also uses a value attribute that contains a regular expression (regex). It uses this regex to collect a set of related log files.  

  - **Static log group:** The `<staticLogGroup>` element uses a key attribute to define the name of the log group that appears in the list. It also uses a value attribute that defines a log file name.  

If the same key attribute value is used in an `<add/>` element within both the `<componentLogGroup>` element and the `<staticLogGroup>` element, Support Center creates a single group. This group includes the log files defined by both elements that use the same key.

#### Example
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="bkmk_wildcards"></a> Collecting additional log files using wildcards

To collect additional log files, use wildcards in the file path or filename. These wildcards include system-wide environment variables such as `%WINDIR%`, but exclude user-scoped environment variables such as `%USERPROFILE%`. To collect additional log files using this non-recursive log file search, use an `<add/>` element within the `<additionalLogFiles>` element. 

These examples show how Support Center uses this feature in the default configuration file.

#### Example 1: Collect all Windows Update log files in the Windows directory
The following element collects any file named `WindowsUpdate.log` found in the Windows directory: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### Example 2: Collect all log files in the Windows Logs directory
The following element collects any file that ends in `.log` found in the Windows logs directory: 

`<add key="%WINDIR%\logs\*.log" />`

#### Full example XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```