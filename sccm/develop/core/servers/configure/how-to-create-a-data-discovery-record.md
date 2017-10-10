---
title: "Create a Data Discovery Record"
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
ms.assetid: aab98600-7a43-4a03-ba05-3fcb828e6c82searchScope: - ConfigMgr SDK
caps.latest.revision: 14
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Data Discovery Record
The data discovery record (DDR), in System Center Configuration Manager, specifies the resource type, the discovery process, the site that discovered the resource, and the resource properties. System Center Configuration Manager provides six library functions that you use to create your own DDRs. For more information. see [About Creating a Data Discovery Record](../../../../develop/core/servers/configure/about-creating-a-data-discovery-record.md).  

### To create a data discovery record  

1.  Create a new instance of the `SMSResGen` class.  

2.  Create a new DDR by using the `NewDDR` method.  

3.  Add properties to the DDR by using the `ADDPROP_` methods.  

4.  Write the new DDR to a file by using the `DDRWrite` method.  

## Example  
 The following example creates a DDR.  

```vbs  

Sub CreateNewDDR()  

    ' Define constants.  
    Const ADDPROP_NONE  = &H0  
    Const ADDPROP_GUID  = &H2  
    Const ADDPROP_KEY   = &H8  
    Const ADDPROP_ARRAY = &H10  

    ' Define variables.  
    Dim newDDR  
    Dim siteCode  
    Dim computerName  
    Dim siteName  
    Dim newIPAddress(2), newIPSubnet(2), newMACAddress(2)  

    ' Load variables with values.  
    siteCode = "ABC"  
    computerName="ComputerName"  
    siteName="Active Directory Site Name"  
    newIPAddress(0)="123.234.12.23"  
    newIPAddress(1)="123.234.12.32"  
    newIPSubnet(0)="123.234.12.0"  
    newIPSubnet(1)="123.234.12.0"  
    newMACAddress(0)="00:02:A5:B1:11:68"  
    newMACAddress(1)="00:02:A5:B1:11:69"  

    ' Load an instance of the SMSResGen.dll.  
    Set newDDR=CreateObject("SMSResGen.SMSResGen.1")  

    ' Create a new DDR using the DDRNew method.  
    newDDR.DDRNew "System", "CustomAgent", siteCode  

    ' Add properties to the new DDR using the DDRAddString method and the previously defined variables.  
    newDDR.DDRAddString "NetBIOS Name", computerName, 64, ADDPROP_KEY  
    newDDR.DDRAddString "AD Site Name", siteName, 64, ADDPROP_NONE  

    ' Add properties to the new DDR using the DDRAddStringArray method and the previously defined variables.   
    newDDR.DDRAddStringArray "IP Addresses", Array(newIPAddress(0),newIPAddress(1)), 64, ADDPROP_ARRAY  
    newDDR.DDRAddStringArray "MAC Addresses", Array(newMACAddress(0),newMACAddress(1)), 64, ADDPROP_ARRAY OR ADDPROP_KEY  
    newDDR.DDRAddStringArray "IP Subnets", Array(newIPSubnet(0),newIPSubnet(1)), 64, ADDPROP_ARRAY  

    ' Write new DDR to file.  
    newDDR.DDRWrite "NewDDR.DDR"  
    wscript.echo "Created new DDR."  

End Sub  

```  

```c#  

public void CreateNewDDR()  
{  
    try  
    {            
        // Define and set the required variables.   
        string Computer = "ComputerName";  
        string SiteName = "Active Directory Site Name";  
        string[] IPAddress  = new string[] { "123.234.12.23", "123.234.12.32" };  
        string[] IPSubnet   = new string[] { "123.234.12.0", "123.234.12.0" };  
        string[] MACAddress = new string[] { "00:02:A5:B1:11:68", "00:02:A5:B1:11:68" };  
        string siteCode = "TQ1";  

        // Create the SMSResGenClass instance.  
        SMSRSGENCTLLib.SMSResGen newDDR = new SMSRSGENCTLLib.SMSResGen();  

        // Create a new DDR using the DDRNew method.  
        newDDR.DDRNew("System", "CustomAgent", siteCode);  

        // Add properties to the new DDR using the DDRAddString method and the previously defined variables.  
        newDDR.DDRAddString("NetBIOS Name", Computer, 64, SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_KEY);  
        newDDR.DDRAddString("AD Site Name", SiteName, 64, SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_NONE);  

        // Add properties to the new DDR using the DDRAddStringArray method and the previously defined variables.   
        newDDR.DDRAddStringArray("IP Subnets", IPAddress, 64, SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_ARRAY);  
        newDDR.DDRAddStringArray("MAC Addresses", MACAddress, 64, SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_ARRAY | SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_KEY);  
        newDDR.DDRAddStringArray("IP Subnets", IPSubnet, 64, SMSRSGENCTLLib.DDRPropertyFlagsEnum.ADDPROP_ARRAY);  

        // Write new DDR to file.  
        newDDR.DDRWrite("NewDDR.DDR");  
        Console.WriteLine("Created new DDR.");          
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create DDR. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

## Compiling the Code  

> [!IMPORTANT]
>  This VBScript and C# examples require **smsrsgen.dll** and **smsrsgenctl.dll**, respectively. Both files are included as a part of the downloadable Configuration Manager SDK (in the "Redistributables" folder).  
>   
>  The file smsrsgenctl.dll is a 32-bit dll and must be registered on the system that will run the application. In addition, the application using smsrsgenctl.dll should be compiled as an x86 application.  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Configuration Manager SDK](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Discovery](../../../../develop/core/servers/configure/discovery.md)   
 [Extending Resource Discovery](../../../../develop/core/servers/configure/extending-resource-discovery.md)   
 [SMSResGen COM Automation Class](../../../../develop/reference/core/servers/configure/smsresgen-com-automation-class.md)
