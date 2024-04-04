---
# required metadata

title: Configure proxy settings for the Intune Connector for Active Directory
description: Covers how to configure the Intune Connector for Active Directory to work with existing on-premises proxy servers.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 8/1/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

# optional metadata
 
#ROBOTS:
#audience:

ms.reviewer: tanvira
ms.suite: ems
search.appverid: 
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
---

# Work with existing on-premises proxy servers

This article explains how to configure the Intune Connector for Active Directory to work with outbound proxy servers. It's intended for customers with network environments that have existing proxies.

By default, the Intune Connector for Active Directory will attempt to automatically locate a proxy server on the network using Web Proxy Auto-Discovery (WPAD). If this has been configured on your network, other configuration may not be required. When changes are needed, the following sections describe how to override the default settings, using [the standard .NET Framework capabilities for configuring proxy settings](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings). More options are described in that documentation.

For more information about how connectors work, see [Understand Microsoft Entra application proxy connectors](/azure/active-directory/manage-apps/application-proxy-connectors).

## Completely bypass outbound proxies

You can configure the connector to bypass your on-premises proxy to ensure it uses direct connectivity to the Azure services. We recommend this approach, as long as your network policy allows for it, because it means that you have one less configuration to maintain.

To disable outbound proxy usage for the connector, edit the ``:ProgramFiles%\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config`` file and set the default proxy to ` "False" ` as shown in the following code example:  

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

To ensure that the Connector Updater service also bypasses the proxy, make a similar change to C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Be sure to make copies of the original files, in case you need to revert to the default .config files.

Once the configuration files have been modified, you'll need to restart the Intune Connector service.

1. Open **services.msc**.
2. Find and select the **Intune ODJConnector Service**.
3. Select **Restart**.  

## Specifying an alternative proxy server

If a different proxy server (for example, one that bypasses authentication) needs to be used with the Intune Connector for Active Directory, this can be specified in a similar manner. To use a different proxy, edit the ``:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config`` file and add the proxy address and proxy port in the section shown in this code sample:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

To ensure that the Connector Updater service also bypasses the proxy, make a similar change to C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Be sure to make copies of the original files, in case you need to revert to the default .config files.

Once the configuration files have been modified, you'll need to restart the Intune Connector service.

1. Open **services.msc**.
2. Find and select the **Intune ODJConnector Service**.
3. Select **Restart**.  

## Next steps

[Manage your devices](../remote-actions/device-management.md)
