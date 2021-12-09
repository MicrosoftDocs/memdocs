---
title: "General Configuration Item Example 1"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4c27ec03-c358-4244-a5c5-d0784e5b4713
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# General Configuration Item Example 1
The following example is a general configuration item schema example that checks the registry to see whether, in this case, remote control is enabled in Configuration Manager.  

## General Configuration Item Example  

```  

<?xml version="1.0" encoding="utf-8"?>  

<!--   
The root element for any DCM Digest document is the DesiredConfigurationDigest element referenced below.  All of the XML elements/attributes are defined in the DCM Digest schema definition namespace.  
-->  

<DesiredConfigurationDigest xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration">  

<!--  
Every DCM Digest must contain exactly one configuration item. Specifically one of the following: an application, operatingsystem, general or baseline.  
This digest defines a general configuration item.    
Note:  The term general configuration item has replaced business policy configuration item in recent desired configuration management documentation.  The terms refer to the same type of configuration item.  

The unique identify of the configuration item is the combination of the attributes AuthoringScopeID, LogicalName and Version.   
Each attribute is part of the unique identity of the configuration item; the actual identity is AuthoringScopeID + LogicalName + Version.  

AuthoringScopeID (string) - This attribute corresponds to the author's namespace or identity.  
LogicalName (string) - This attribute identifies the configuration item within the authoring scope.  
Version (string) - This attribute specifies the version of the configuration item.  
-->  

    <BusinessPolicy AuthoringScopeId="ScopeId_F348CC96-19CA-4F5D-9D4F-D1451B5BEB1E" LogicalName="BusinessPolicy_de5ad8df-1600-4984-91ab-7e33e0e7670b" Version="1">  
        <Annotation>  
            <DisplayName Text="Remote Control Is Enabled" />  
            <Description Text="This General CI detects whether remote control is enabled by examining the registry and asserting that the expected value is set (the expected value being 1)." />  
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

            <RootComplexSetting>  

<!--  
A simple setting.   
-->  

                <SimpleSetting LogicalName="RegSetting_60d3f52e-5afa-4864-bbcf-83953c806275" DataType="String">  
                    <Annotation>  
                        <DisplayName Text="Remote control registry value" ResourceId="ID-29d49a44-436a-4dbe-bc15-0db78557a4a6" />  
                        <Description Text="Contains the value obtained from the remote control registry key." ResourceId="ID-bfe89599-45fc-4413-8a17-5fea1ced7bea" />  
                    </Annotation>  

<!--  
Optional element. We raise a warning if the source for this setting does not exist. If so, we include the element and specify the severity of the error. Otherwise, we do not use the element.  
-->  

                    <ExistentialRule Severity="Warning" />  

<!--  
The source of the setting's value. In this case, we're looking for a particular value from the registry.  
-->  

                    <RegistryDiscoverySource Hive="HKEY_LOCAL_MACHINE" Depth="Subtree" Is64Bit="false">  
                        <Key>software\microsoft\sms\client\clientcomponents\remotecontrol</Key>  
                        <ValueName>enabled</ValueName>  
                    </RegistryDiscoverySource>  

<!--  
Rules defined against the value of the setting.  
-->  

                    <Rules>  
                        <Rule xmlns="http://schemas.microsoft.com/SystemsCenterConfigurationManager/2009/06/14/Rules" NonCompliantWhenSettingIsNotFound="false" Severity="Warning" id="Rule_2849425d-0f2b-4d8f-bf63-8113f39c1618">   
                            <Annotation>   
                                <DisplayName ResourceId="ID-91baba67-94bc-4b97-b3da-69ab7ba92235" Text="Remote control is enabled."/>   
                                <Description ResourceId="ID-87277341-e734-42ad-87e3-a89e87e9c320" Text="This checks the registry setting HKEY_LOCAL_MACHINE\software\microsoft\sms\client\clientcomponents\remotecontrol\enabled registry value to identify whether it is enabled (set to "1")."/>   
                            </Annotation>   
                            <Expression> <Operator>Equals</Operator>   
                                <Operands>   
                                    <SettingReference SettingSourceType="Registry" SettingLogicalName="RegSetting_1d07d7eb-23f9-478e-9ed5-ae2fae31d5bf" Version="2" LogicalName="OperatingSystem_9658594e-a4bc-48a7-bb45-6e07d1308d8a" AuthoringScopeId="ScopeId_6F782309-1BE1-43E8-A529-177F93D1D8D2" DataType="Int64" Changeable="false" Method="Value"/> <ConstantValue DataType="Int64" Value="1"/>   
                                </Operands>   
                            </Expression>   
                        </Rule>  
                    </Rules>  
                </SimpleSetting>  
            </RootComplexSetting>  
        </Settings>  
    </BusinessPolicy>  
</DesiredConfigurationDigest>  
```  

## See Also  
[About authoring configuration baselines and items](about-authoring-configuration-baselines-and-configuration-items.md)
