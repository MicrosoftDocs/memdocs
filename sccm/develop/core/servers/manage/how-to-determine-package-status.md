---
title: "Determine Package Status"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 005b6456-fbfd-49b3-b701-bf549ff611ce
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Determine Package Status
In System Center Configuration Manager, the software distribution process can take from several minutes to several hours, depending on the site settings, network topography, whether the package includes source files, and the number of distribution points that have been specified for the package. Creating the package, distribution points, programs, and advertisement instances initiates the software distribution process that is managed by the System Center Configuration Manager Distribution Manager.  

 The Distribution Manager must first distribute the package's source files, which is the time-consuming aspect of the software distribution process. Only after the source files are distributed can the advertisements be offered on a site. You can use the package summarizer classes to determine whether a package has been distributed and is ready to be advertised.  

 The level of status detail that you want determines which of the following package summarizer classes to use:  

- [SMS_PackageStatusDetailSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdetailsummarizer-server-wmi-class.md)  

- [SMS_PackageStatusRootSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusrootsummarizer-server-wmi-class.md)  

- [SMS_PackageStatusDistPointsSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdistpointssummarizer-server-wmi-class.md)  

  The `SMS_PackageStatusDetailSummarizer` class gives you package status at the site level and the `SMS_PackageStatusRootSummarizer` class gives you package status for all sites. You can only use the `SMS_PackageStatusDistPointsSummarizer` class if your package contains source files.  

  For packages that do not contain source files, an instance in the root or detail class signifies that the distribution portion of the process is complete (the value for `Targeted` property is 0). For packages that do contain source files, when the value in the `Installed` property equals the value in the `Targeted` property, the source files have been successfully distributed.  

  To determine the status of a package, you can either create your own polling mechanism by using a timer that queries the summarizer for a specific package or you can register for a Windows Management Instrumentation (WMI) temporary intrinsic event that polls for create instance and modify instance events on the summarizer class as the following example shows. You can use your own timer mechanism, or you can create a WMI timer event.  

> [!NOTE]
>  Using WMI to poll for events is expensive and should be used with consideration.  

### To determine package status  

1.  Set up a connection to the System Center Configuration Manager provider namespace.  

2.  Create an event handler to watch for the creation or modification of the [SMS_PackageStatusRootSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusrootsummarizer-server-wmi-class.md).  

## Example  
 The following example asynchronously queries for the creation and modification of the [SMS_PackageStatusRootSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusrootsummarizer-server-wmi-class.md).  

> [!NOTE]
>  It is not possible to use the managed provider libraries to query WMI object instance creation and modification. Therefore the C# sample is written by using the System.Management libraries.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub QueryPackageStatus (connection)  

    Dim query  
    Dim sink  
    Dim minutes  

    Set sink = WScript.CreateObject("wbemscripting.swbemsink","sink_")  

    ' You have to specify a polling interval because Configuration Manager  
    ' does not provide an intrinsic event provider for these classes.  
    Query = "SELECT * FROM __InstanceCreationEvent Within 120 " & _  
            "WHERE TargetInstance.__Class = 'SMS_PackageStatusRootSummarizer' "  
    connection.ExecNotificationQueryAsync sink, query  

    query = "SELECT * FROM __InstanceModificationEvent Within 120 " & _  
            "WHERE TargetInstance.__Class = 'SMS_PackageStatusRootSummarizer' "  
    connection.ExecNotificationQueryAsync sink, query  

    minutes = 0  

    ' Loop for 5 minutes.  
    While minutes < 300  
        wscript.sleep 1000  
        minutes = minutes + 1  
    Wend   

    sink.Cancel  
    Set sink = nothing  

 End Sub     

' The sink subroutine to handle the OnObjectReady   
' event. This is called as each object returns.  
Sub sink_OnObjectReady(statusEvent, octx)  
   Wscript.Echo "Name: " + statusEvent.TargetInstance.Name  
   Wscript.Echo "Targeted: " + CStr(statusEvent.TargetInstance.Targeted)  
   Wscript.Echo "Installed: " + CStr(statusEvent.TargetInstance.Installed)  
   Wscript.Echo  
End Sub  

Sub sink_OnCompleted(Hresult, oErr, oCtx)  
    Wscript.Echo "Finished"  
End Sub  

```  

```c#  

public void QueryPackageStatus(string connectionPath)  
{  
   // WMIEvent we = new WMIEvent();  
    ManagementEventWatcher modifiedWatcher = null;  
    ManagementEventWatcher createdWatcher = null;  
    WqlEventQuery modified;  
    WqlEventQuery created;  

    ManagementOperationObserver observer = new  
        ManagementOperationObserver();  

    // Bind to local computer.  
    ConnectionOptions opt = new ConnectionOptions();  
    opt.EnablePrivileges = true; //sets required privilege  
    ManagementScope scope = new ManagementScope(connectionPath, opt);  

    try  
    {  
        modified = new WqlEventQuery();  
        modified.EventClassName = "__InstanceModificationEvent";  
        modified.WithinInterval = new TimeSpan(0, 0, 120);  
        modified.Condition = @"TargetInstance ISA 'SMS_PackageStatusRootSummarizer'";  
        modifiedWatcher = new ManagementEventWatcher(scope, modified);  

        // Register handler.  
        modifiedWatcher.EventArrived += new EventArrivedEventHandler(this.ObjectReady);  

        created = new WqlEventQuery();  
        created.EventClassName = "__InstanceCreationEvent";  
        created.WithinInterval = new TimeSpan(0, 0, 10);  
        created.Condition = @"TargetInstance ISA 'SMS_PackageStatusRootSummarizer'";  
        createdWatcher = new ManagementEventWatcher(scope, created);  

        createdWatcher.EventArrived += new EventArrivedEventHandler(this.ObjectReady);  

        modifiedWatcher.Start();  
        createdWatcher.Start();  

        // Wait.  
        Console.ReadLine();  
    }  
    catch (ManagementException e)  
    {  
        Console.WriteLine(e.Message);  
    }  
    finally  
    {  
        modifiedWatcher.Stop();  
        createdWatcher.Stop();  
    }  
}  

public void ObjectReady(object sender, EventArrivedEventArgs e)  
{  
    // Get the Event object and display it.  
    PropertyData pd = e.NewEvent.Properties["TargetInstance"];  

    Console.WriteLine("Hello:");  

    if (pd != null)  
    {  
        ManagementBaseObject statusEvent = pd.Value as ManagementBaseObject;  
        Console.WriteLine ("Name: " + statusEvent.Properties["Name"].Value);  
        Console.WriteLine("Targeted: " + statusEvent.Properties["Targeted"].Value);  
        Console.WriteLine("Installed:" + statusEvent.Properties["Installed"].Value);  
        Console.WriteLine();  
    }  
}  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connectionPath`|Managed: `String`|A valid path to the SMS Provider. For example, `root\\sms\\site_CODE`.|  
|`Connection`|VBScript: `SWbemServices`|A valid connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)|  

## Compiling the Code  

### Namespaces  
 System  

 System.Management  

### Assembly  
 System.Management  

## Robust Programming  
 The exception that can be raised is [System.Management.ManagementException](assetId:///System.Management.ManagementException?qualifyHint=False&autoUpgrade=True).  

## See Also  
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_PackageStatusDetailSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdetailsummarizer-server-wmi-class.md)   
 [SMS_PackageStatusRootSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusrootsummarizer-server-wmi-class.md)   
 [SMS_PackageStatusDistPointsSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdistpointssummarizer-server-wmi-class.md)   
 [About Configuration Manager Status Summarizers](../../../../develop/core/servers/manage/about-configuration-manager-status-summarizers.md)
