---
title: "Application Configuration Item Example 2"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: f359d17d-d2dc-4b34-9e1b-5c5c1d5fe060searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Application Configuration Item Example 2
In System Center Configuration Manager, the following Application Configuration Item Instance example determines whether Notepad.exe is installed.  

## Application Configuration Item Example  

```  
<?xml version="1.0" encoding="utf-8"?>  

<!--   
The root element for any DCM Digest document is the DesiredConfigurationDigest element referenced below.  All of the XML elements/attributes are defined in the DCM Digest schema definition namespace.  
-->  

<DesiredConfigurationDigest xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration">  

<!--  
Every DCM Digest must contain exactly one configuration item. Specifically one of the following: an application, operatingsystem, general or baseline.  
This digest defines an application configuration item.    

The unique identify of the configuration item is the combination of the attributes AuthoringScopeID, LogicalName and Version.   
Each attribute is part of the unique identity of the configuration item; the actual identity is AuthoringScopeID + LogicalName + Version.  

AuthoringScopeID (string) - This attribute corresponds to the author’s namespace or identity.  
LogicalName (string) - This attribute identifies the configuration item within the authoring scope.  
Version (string) - This attribute specifies the version of the configuration item.  
-->  

    <Application AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="Application_171bae6f-5661-4bb8-a703-270b131e4c4c" Version="1" Is64Bit="false">  
        <Annotation>  
            <DisplayName Text="Notepad" />  
            <Description Text="Detects Notepad.exe via script-based discovery" />  
        </Annotation>  

<!--  
There are no parts defined for this configuration item.  
Parts are physical things with fixed lists of properties.Mandatory element tag for the section of the DCM Digest used to define Object parts, including:  
File  
Folder  
Assembly (registered in the Global Assembly Cache (GAC))  
RegistryKey  
-->  

        <Parts>  
            <ParentReferences />  
        </Parts>  

<!--  
There are no settings defined for this configuration item.   
Settings are configurable name/value pairs which influence the behavior of hardware and software. DCM can discover settings using any of the supported providers, including:  
Registry  
WMI (WQL query)  
Microsoft SQL Server (SQL query)  
Active Directory (LDAP)  
XML (XPath query)  
IIS Metabase  
Script (JScript/VBScript/PowerShell)  
-->  

        <Settings>  

<!--  
RootComplexSetting is the root container for all settings. Every configuration item has one of these, even if there are no actual settings defined.  
-->  
            <RootComplexSetting />  

        </Settings>  

<!--  
This application is discovered via script-based discovery. If it does exist (is discovered) the system then discovers the parts and settings. Finally, the system evaluates the rules (if any) defined against the part property values and the setting values.  
-->  

<!--  
IMPORTANT:  Insert a script here - not just the name of the script, but the actual script code. Returning a value from the script indicates that the application exists, not returning a value indicates that the application was not found.  
-->  
        <ScriptDiscoveryInfo ScriptType="VBScript">  
            <Script>   
                     Dim filesys  
                     Set filesys = CreateObject("Scripting.FileSystemObject")   
                     If filesys.FileExists("c:\notepad.exe") Then  
                     wscript.echo("Notepad.exe Exists")  
                     Else  
                    ' Returning nothing, as the application does not exist.  
                     End If    
            </Script>  
        </ScriptDiscoveryInfo>  
    </Application>  
</DesiredConfigurationDigest>  
```  

## See Also  
 [Authoring Compliance Settings Configuration Baselines and Configuration Items](../../develop/compliance/authoring-compliance-settings-configuration-baselines-and-configuration-items.md)
