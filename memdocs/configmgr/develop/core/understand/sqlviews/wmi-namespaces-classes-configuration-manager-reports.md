---
title: WMI namespaces and classes for reports
titleSuffix: Configuration Manager
description: Configuration Manager WMI namespaces and classes for Configuration Manager reports
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b687399a-b750-42f7-949a-4c757d269d58
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Configuration Manager WMI namespaces and classes for Configuration Manager reports

When Configuration Manager is installed, there are several Windows Management Instrumentation (WMI) namespaces created, and depending on the namespace, hundreds of classes can be created under each namespace. Also, each site might have classes that other sites might not have depending on the specific site settings, the inventory that is tracked, and so forth.

## WMI namespaces created by Configuration Manager

The following WMI namespaces are created by Configuration Manager:

- root\\ccm
  - root\\ccm\\CCMPasswordSettings
  - root\\ccm\\CIModels
  - root\\ccm\\CIStateStore
  - root\\ccm\\CIStore
  - root\\ccm\\CITasks
  - root\\ccm\\ClientSDK
  - root\\ccm\\ContentTransferManager
  - root\\ccm\\DataTransferService
  - root\\ccm\\dcm
  - root\\ccm\\DCMAgent
  - root\\ccm\\evaltest
  - root\\ccm\\Events
  - root\\ccm\\InvAgt
  - root\\ccm\\LocationServices
  - root\\ccm\\Messaging
  - root\\ccm\\NetworkConfig
  - root\\ccm\\PeerDPAgent
  - root\\ccm\\Policy
  - root\\ccm\\PowerManagementAgent
  - root\\ccm\\RebootManagement
  - root\\ccm\\ScanAgent
  - root\\ccm\\Scheduler
  - root\\ccm\\SMSNapAgent
  - root\\ccm\\SoftMgmtAgent
  - root\\ccm\\SoftwareMeteringAgent
  - root\\ccm\\SoftwareUpdates
  - root\\ccm\\StateMsg
  - root\\ccm\\VulnerabilityAssessment
  - root\\ccm\\XmlStore
  - root\\cimv2\\sms
  - root\\smsdm
  - root\\sms
  - root\\sms\\site\_*\<site code\>*

## How to retrieve Configuration Manager WMI namespaces and classes by using a Visual Basic script

An easy way to list the Configuration Manager�related classes that have been created on your site is to run a Microsoft Visual Basic script. The following script will scan all of the classes within each of the WMI namespaces listed above and output the results to a text file.

### To run the script to scan the WMI namespaces and classes

1. Copy the following code into Notepad:

    ```vbscript
        '======================================================================================= 
        ' 
        ' NAME: WMIScan.vbs 
        ' 
        ' AUTHOR:  Microsoft Corporation 
        ' DATE  : 10/24/2013 (Revised for System Center 2012 Configuration Manager by Rob Stack) 
        ' 
        ' COMMENT: Script to scan Configuration Manager WMI classes. 
        ' 
        '======================================================================================= 
         
        Dim SearchChar 
        Dim TotChar 
        Dim RightChar 
        Dim ClassName 
        Dim Computer 
        Dim strComputer 
        Dim strUser 
        Dim strPassword 
        Dim strSiteCode 
        Dim strNameSpace 
        Dim strFolder 
        Dim strFile 
        Dim strLogFile 
        Dim strFullFile 
        Dim strFullLogFile 
        Dim isError 
          
        Const ForWriting = 2 
        Const ForAppending = 8 
        Const adOpenStatic = 3 
        Const adLockOptimistic = 3 
        Const adUseClient = 3 
         
        set colNamedArguments=wscript.Arguments.Named 
        If colNamedArguments.Exists("Sitecode") Then 
          strSiteCode = colNamedArguments.Item("Sitecode") 
        Else 
          WScript.Echo "Invalid Command Line Arguments" & vbCrLf & _ 
            vbCrLf & "Usage: WMIScan.vbs /Sitecode:<sitecode> " & _ 
            "/Computer:<computername>" & vbCrLf & vbCrLf & _ 
            "Example1: WMIScan.vbs /Sitecode:PS1" & vbCrLf & _ 
            "Example2: WMIScan.vbs /Sitecode:PS1 /Computer:Computer1" 
          WScript.Quit(1) 
        End If 
        If colNamedArguments.Exists("Computer") Then 
          strComputer = colNamedArguments.Item("Computer") 
        Else strComputer = "." 
        End If 
         
        'Define the values for files and folders. 
        strFolder = "c:\WMIScan" 
        strFile = "WMIScan.txt" 
        strLogFile = "WMIScan.log" 
        strFullFile = strFolder & "\" & strFile 
        strFullLogFile = strFolder & "\" & strLogFile 
        isError = 0 
         
        'List of Configuration Manager namespaces are put into an array. 
        arrNameSpaces = Array("root\ccm","root\ccm\CCMPasswordSettings","root\ccm\CIModels",_
        "root\ccm\CIStateStore","root\ccm\CIStore","root\ccm\CITasks",_
        "root\ccm\ClientSDK","root\ccm\ContentTransferManager","root\ccm\DataTransferService",_
        "root\ccm\dcm","root\ccm\DCMAgent","root\ccm\evaltest",_
        "root\ccm\Events","root\ccm\InvAgt","root\ccm\LocationServices",_
        "root\ccm\Messaging","root\ccm\NetworkConfig","root\ccm\PeerDPAgent",_
        "root\ccm\Policy","root\ccm\PowerManagementAgent","root\ccm\RebootManagement",_
        "root\ccm\ScanAgent","root\ccm\Scheduler","root\ccm\SMSNapAgent",_
        "root\ccm\SoftMgmtAgent","root\ccm\SoftwareMeteringAgent","root\ccm\SoftwareUpdates",_
        "root\ccm\StateMsg","root\ccm\VulnerabilityAssessment","root\ccm\XmlStore",_
        "root\cimv2\sms","root\smsdm","root\sms",_
        "root\sms\site_"& strSiteCode)
        
        'Creates the folder and files for the scan output and log file. 
        Set objFSO = CreateObject("Scripting.FileSystemObject") 
         
        'Does strFolder Folder exist? If not, it's created. 
        If Not objFSO.FolderExists(strFolder) then 
          Set objFolder = objFSO.CreateFolder(strFolder) 
        End If 
         
        'Creates the WMIScan.txt and WMIScan.log files. 
        Set objFile = objFSO.CreateTextFile(strFullFile) 
        Set objLogFile = objFSO.CreateTextFile(strFullLogFile) 
        objFile.close 
        objLogFile.close 
         
        'Opens the WMIScan.log file in write mode. 
        Set objFSO = CreateObject("Scripting.FileSystemObject") 
        Set objLogFile = objFSO.OpenTextFile(strFullLogFile, ForWriting) 
        objLogFile.WriteLine "********************************************" 
        objLogFile.WriteLine " WMIScan Tool Executed - " & Now() 
        objLogFile.WriteLine "********************************************" 
         
        'Opens the WMIScan.txt file in write mode. 
        Set objFile = objFSO.OpenTextFile(strFullFile, ForWriting) 
        objLogFile.WriteLine "--------------------------------------------" 
        Computer = strComputer 
        If Computer = "." Then Computer = "Local System" 
        objLogFile.WriteLine " Scanning WMI Namespaces On " & Computer 
        objLogFile.WriteLine "--------------------------------------------" 
         
        WScript.echo "Starting WMI scan on " & Computer 
         
        'Create a collection of Namespaces from the array, and 
        ' call the EnumNameSpaces subroutine to do the scan. 
        For Each strNameSpace In arrNameSpaces 
           Call EnumNameSpaces(strNameSpace, strComputer) 
        Next 
        objLogFile.WriteLine "---------------------------------------------" 
        objLogFile.WriteLine " Done scanning WMI Namespaces on " & Computer 
        objLogFile.WriteLine "---------------------------------------------" 
         
        'Close the WMISscan.txt file. 
        objFile.close 
         
        If isError = 1 Then 
          WScript.Echo "WMI Scan has Completed with Errors!" & vbCrLf & _ 
          "Check the " & strLogFile & " file for more details." & vbCrLf & _ 
          vbCrLf & strFile & " & " & strLogFile & " have been written to "_ 
          & strFolder & "." 
        Else 
          WScript.Echo "WMI Scan has Completed without any Errors!" & _ 
          vbCrLf & vbCrLf & strFile & " & " & strLogFile & _ 
          " have been written to " & strFolder & "." 
        End If   
         
        '*************************************************************** 
        '***   Subroutine to do the classes scan on the namespace.   *** 
        '*************************************************************** 
        Sub EnumNameSpaces(strNameSpace, strComputer) 
          Set objSWbemLocator = CreateObject("WbemScripting.SWbemLocator") 
          On Error Resume next 
          Set objSWbemServices= objSWbemLocator.ConnectServer (strComputer,_ 
            strNameSpace) 
          objLogFile.Write "Connecting to the \\" & strComputer & "\" &_ 
            strNameSpace & " WMI NameSpace...." 
          If Err.number = 0 Then  
            objLogFile.WriteLine "Success!!" 
            objLogFile.Write "  Scanning for Classes in "&strNameSpace _ 
              & "..." 
         
            'Create a collection of all the subclasses of the namespace. 
            Set colClasses = objSWbemServices.SubclassesOf() 
         
            'Scan all WMI classes, and write them to the scan1.txt file. 
            objFile.WriteBlanklines(1) 
            objFile.WriteLine "\\" & strComputer & "\" & strNameSpace 
         
            For Each objClass In colClasses 
              SearchChar = instr(objClass.Path_.Path, ":") 
              TotChar = len(objClass.Path_.Path) 
              RightChar = TotChar - SearchChar 
              ClassName = right(objClass.Path_.Path,RightChar) 
              objFile.WriteLine "   " & ClassName 
            Next 
            objLogFile.WriteLine "Success!!" 
          ElseIf Err.Number = -2147024891 Then 
            objLogFile.WriteLine "Error " & Err.Number & _ 
              "! Connection to "& strComputer & " Failed!" 
            isError = 1 
          Elseif Err.Number = -2147217394 Then 
            objLogFile.WriteLine "Error " & Err.Number & "!! Namespace "&_ 
              strNameSpace & " NOT Found!!" 
            isError = 1   
          Else 
            objLogFile.WriteLine "Error " & Err.Number & "!!" 
          isError = 1 
          End If 
         
        End Sub
    ```

1. Create a folder named C:\\WMIScan.
1. Save the script as WMIScan.vbs in the C:\\WMIScan folder.
1. Open a Command Prompt window.
1. Type **C:\\WMIScan\\WMIScan.vbs /sitecode:ABC** and then press **Enter**. Make sure to replace **ABC** with the appropriate site code.

   > [!NOTE]
   > The above command line assumes that the script is run from a Configuration Manager site server. To connect to WMI on a remote site server, use the /computer:&lt;computername&gt; argument to specify the remote computer. For example, to connect to site code ABC on Computer1, you would type C:\WMIScan\WMIScan.vbs /sitecode:ABC /computer:Computer1 in the command line.

The script creates a text file (in C:\\WMIScan) with all of the WMI classes in each of the WMI namespaces for Configuration Manager when run on a Configuration Manager primary site server. A log file is also created listing all of the namespaces scanned and whether the scan was successful. Be aware that some namespaces will not be present on some site servers, depending on which options have been configured.

## See also

[SMS provider WMI schema reference in Configuration Manager](sms-provider-wmi-schema-reference-configuration-manager.md)
