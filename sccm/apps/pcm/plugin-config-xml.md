---
title: Plug-in configuration XML
titleSuffix: Configuration Manager
description: Technical reference for the XML elements of the Package Conversion Manager plug-in.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Technical reference for the Package Conversion Manager plug-in configuration XML

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1357861-->

This article describes the XML elements in the Configuration Manager configuration file (Microsoft.ConfigurationManagement.exe.config) that control the operation of the Package Conversion Manager plug-in. For more information on how to use this plug-in, see [How to use the Package Conversion Manager plug-in](/sccm/apps/pcm/how-to-use-plug-in).



## XML configuration elements

The following table describes the XML elements in the Configuration Manager configuration file that relate to the Package Conversion Manager plug-in.

|Element  |Type  |Description  |
|---------|---------|---------|
|**PcmPlugIn**|String|The name of the script or executable to use as the Package Conversion Manager plug-in.|
|**PcmPlugInTimeoutMilliseconds**|Integer|The maximum amount of time, in milliseconds, to wait for the Package Conversion Manager plug-in script or executable to complete the processing of a package.|
|**PcmPluginExitCode**|Integer|The expected exit code from the plug-in process. This value indicates success. All other codes are considered an error.|
|**ForceRequirementsExtraction**|Boolean|Allow automatic conversion to use collection requirements associated with a package. This should only be set to True when working with a Package Conversion Manager plug-in that's designed to make decisions about which requirements to use.|



## Sample configuration XML

This section provides an example of the Package Conversion Manager configuration XML elements in the Configuration Manager configuration file, **Microsoft.ConfigurationManagement.exe.config**. By default, this file is in the following path:  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

In the sample, the elements related to Package Conversion Manager are inside the following element:
`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

