---
title: Calling Code Snippets
titleSuffix: Configuration Manager
description: How to set up the calling code for the code examples that are used throughout the Configuration Manager Software Development Kit (SDK).
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8d5d026f-18da-43c4-8427-575716351925
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Calling Configuration Manager Code Snippets
The following code samples show how to set up the calling code for the code examples that are used throughout the Configuration Manager Software Development Kit (SDK).  

 Replace the SNIPPETMETHOD snippet with the snippet that you want to run. In most cases you will need to make changes, such as adding parameters, to make the code work.   

 For more information about remote Windows Management Instrumentation (WMI) connections, see [Connecting to WMI on a Remote Computer](/windows/win32/wmisdk/connecting-to-wmi-on-a-remote-computer).  

## Example  

```vbs  
Dim connection  
Dim computer  
Dim userName  
Dim userPassword  
Dim password 'Password object  

Wscript.StdOut.Write "Computer you want to connect to (Enter . for local): "  
computer = WScript.StdIn.ReadLine  

If computer = "." Then  
    userName = ""  
    userPassword = ""  
Else  
    Wscript.StdOut.Write "Please enter the user name: "  
    userName = WScript.StdIn.ReadLine  

    Set password = CreateObject("ScriptPW.Password")   
    WScript.StdOut.Write "Please enter your password:"   
    userPassword = password.GetPassword()   
End If  

Set connection = Connect(computer,userName,userPassword)  

If Err.Number<>0 Then  
    Wscript.Echo "Call to connect failed"  
End If  

Call SNIPPETMETHODNAME (connection)  

Sub SNIPPETMETHODNAME(connection)  
   ' Insert snippet code here.  
End Sub  

Function Connect(server, userName, userPassword)  

    On Error Resume Next  

    Dim net  
    Dim localConnection  
    Dim swbemLocator  
    Dim swbemServices  
    Dim providerLoc  
    Dim location  

    Set swbemLocator = CreateObject("WbemScripting.SWbemLocator")  

    swbemLocator.Security_.AuthenticationLevel = 6 'Packet Privacy  

    ' If  the server is local, don not supply credentials.  
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

```c#  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ComponentModel;  
using Microsoft.ConfigurationManagement.ManagementProvider;  
using Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine;  

namespace ConfigurationManagerSnippets  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // Setup snippet class.  

            string computer = "";  
            string userName = "";  
            string password = "";  

            SnippetClass snippets = new SnippetClass();  

            Console.WriteLine("Computer you want to connect to (Enter . for local): ");  
            computer = Console.ReadLine();  
            Console.WriteLine();  

            if (computer == ".")  
            {  
                computer = System.Net.Dns.GetHostName();  
                userName = "";  
                password = "";  
            }  
            else  
            {  
                Console.WriteLine("Please enter the user name: ");  
                userName = Console.ReadLine();  

                Console.WriteLine("Please enter your password:");  
                password = snippets.ReturnPassword();  
            }  

            // Make connection to provider.  
            WqlConnectionManager WMIConnection = snippets.Connect(computer, userName, password);  

            // Call snippet function and pass the provider connection object.  
            snippets.SNIPPETMETHODNAME(WMIConnection);  
        }  
    }  

    class SnippetClass  
    {  
        public WqlConnectionManager Connect(string serverName, string userName, string userPassword)  
        {  
            try  
            {                 
                SmsNamedValuesDictionary namedValues = new SmsNamedValuesDictionary();  
                WqlConnectionManager connection = new WqlConnectionManager(namedValues);  
                if (System.Net.Dns.GetHostName().ToUpper() == serverName.ToUpper())  
                {  
                    connection.Connect(serverName);  
                }  
                else  
                {  
                    connection.Connect(serverName, userName, userPassword);  
                }  
                return connection;  
            }  
            catch (SmsException ex)  
            {  
                Console.WriteLine("Failed to Connect. Error: " + ex.Message);  
                return null;  
            }  
            catch (UnauthorizedAccessException ex)  
            {  
                Console.WriteLine("Failed to authenticate. Error:" + ex.Message);  
                return null;  
            }  
        }  

        public void SNIPPETMETHODNAME(WqlConnectionManager connection)  
        {  
            // Insert snippet code here.  
        }  

        public string ReturnPassword()  
        {  
            string password = "";  
            ConsoleKeyInfo info = Console.ReadKey(true);  
            while (info.Key != ConsoleKey.Enter)  
            {  
                if (info.Key != ConsoleKey.Backspace)  
                {  
                    password += info.KeyChar;  
                    info = Console.ReadKey(true);  
                }  
                else if (info.Key == ConsoleKey.Backspace)  
                {  
                    if (!string.IsNullOrEmpty(password))  
                    {  
                        password = password.Substring  
                        (0, password.Length - 1);  
                    }  
                    info = Console.ReadKey(true);  
                }  
            }  
            for (int i = 0; i < password.Length; i++)  
                Console.Write("*");  
            return password;  
        }  
    }  
}  
```  

## Compiling the Code  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

> [!NOTE]
>  The assemblies are in the \<Program Files>\Microsoft Endpoint Manager\AdminConsole\bin folder.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Robust Programming  
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).
