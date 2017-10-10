---
title: "Connect to an SMS Provider by Using WMI"
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
ms.assetid: 8f5ee4ee-11bf-4ff3-95c9-4ec046308902searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Connect to an SMS Provider in Configuration Manager by Using WMI
Before connecting to the SMS Provider for a local or remote System Center Configuration Manager site server, you first need to locate the SMS Provider for the site server. The SMS Provider can be either local or remote to the Configuration Manager site server you are using. The Windows Management Instrumentation (WMI) class `SMS_ProviderLocation` is present on all Configuration Manager site servers, and one instance will contain the location for the Configuration Manager site server you are using.  

 You can connect to the SMS Provider on a Configuration Manager site server by using the WMI [SWbemLocator](http://go.microsoft.com/fwlink/?LinkId=44022) object or by using the Windows Script Host `GetObject` method. Both approaches work equally well on local or remote connections, with the following limitations:  

-   You must use `SWbemLocator` if you need to pass user credentials to a remote computer.  

-   You cannot use `SWbemLocator` to explicitly pass user credentials to a local computer.  

 There are several different syntaxes that you can use to make the connection, depending on whether the connection is local or remote. After you are connected to the SMS Provider, you will have an [SWbemServices](http://go.microsoft.com/fwlink/?LinkId=44023) object that you use to access System Center Configuration Manager objects.  

> [!NOTE]
>  If you need to add context qualifiers for the connection, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).  

### To connect to an SMS provider  

1.  Get a [WbemScripting.SWbemLocator](https://msdn.microsoft.com/library/aa393719.aspx) object.  

2.  Set the authentication level to packet privacy.  

3.  Set up a connection to the SMS Provider by using the [SWbemLocator](https://msdn.microsoft.com/library/aa393719.aspx) object [ConnectServer](https://msdn.microsoft.com/library/aa393720.aspx) method. Supply credentials only if it is a remote computer.  

4.  Using the [SMS_ProviderLocation](../../../develop/reference/misc/sms_providerlocation-server-wmi-class.md) object *ProviderForLocalSite* property, connect to the SMS Provider for the local computer and receive a [SWbemServices object](https://msdn.microsoft.com/library/aa393854.aspx).  

5.  Use the [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx) object to access provider objects. For more information, see [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md).  

## Example  
 The following VB Script example connects to the server. It then attempts to connect to the SMS Provider for that server. Typically this will be the same computer. If it is not, [SMS_ProviderLocation](../../../develop/reference/misc/sms_providerlocation-server-wmi-class.md) provides the correct computer name.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Function Connect(server, userName, userPassword)  

    On Error Resume Next  

    Dim net  
    Dim localConnection  
    Dim swbemLocator  
    Dim swbemServices  
    Dim providerLoc  
    Dim location  

    Set swbemLocator = CreateObject("WbemScripting.SWbemLocator")  

    swbemLocator.Security_.AuthenticationLevel = 6 'Packet Privacy.  

    ' If the server is local, do not supply credentials.  
    Set net = CreateObject("WScript.NetWork")   
    If UCase(net.ComputerName) = UCase(server) Then  
        localConnection = true  
        userName = ""  
        userPassword = ""  
        server = "."  
    End If  

    ' Connect to the server.  
    Set swbemServices= swbemLocator.ConnectServer _  
            (server, "root\sms",userName,userPassword)  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't connect: " + Err.Description  
        Connect = null  
        Exit Function  
    End If  

    ' Determine where the provider is and connect.  
    Set providerLoc = swbemServices.InstancesOf("SMS_ProviderLocation")  

        For Each location In providerLoc  
            If location.ProviderForLocalSite = True Then  
                Set swbemServices = swbemLocator.ConnectServer _  
                 (location.Machine, "root\sms\site_" + _  
                    location.SiteCode,userName,userPassword)  
                If Err.Number<>0 Then  
                    Wscript.Echo "Couldn't connect:" + Err.Description  
                    Connect = Null  
                    Exit Function  
                End If  
                Set Connect = swbemServices  
                Exit Function  
            End If  
        Next  
    Set Connect = null ' Failed to connect.  
End Function  
```  

## Compiling the Code  
 This C# example requires:  

## Comments  
 The sample method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)
|A valid connection to the SMS Provider.|  
|`taskSequence`|-   Managed: `IResultObject`<br />-   VBScript:  `SWbemObject`|A valid task sequence ([SMS_TaskSequence](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)).|  
|`taskSequenceXML`|-   Managed: `String`<br />-   VBScript: `String`|A valid task sequence XML.|  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 Using script to pass the user name and password is a security risk and should be avoided where possible.  

 The preceding example sets the authentication to packet privacy. This is the same managed SMS Provider.  

 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md)   
 [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md)   
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)
