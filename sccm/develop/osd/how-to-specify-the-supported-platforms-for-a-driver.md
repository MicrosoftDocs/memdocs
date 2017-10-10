---
title: "Specify the Supported Platforms for a Driver"
titleSuffix: "Configuration Manager"
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
ms.assetid: 1d0c07a0-dbab-4279-9fa1-114a3d992a24searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Specify the Supported Platforms for a Driver
In System Center Configuration Manager, you specify the supported platforms of a driver in the `SDMPackageXML` property XML of the driver's [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. The XML contains a node `PlatformApplicabilityConditions` to which you add `PlatformApplicabilityCondition` elements for each platform the driver supports.  

> [!NOTE]
>  You should add only platforms that are listed in a [SMS_SupportedPlatforms Server WMI Class](../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md) object. Drivers can only be conditioned for major operating system releases, that is, it is not possible to target drivers at service packs.  

> [!CAUTION]
>  The supported platforms portion of `SDMPackageXML` is the only part of the CI-XML schema that can be edited. You should not make changes to other parts of the XML.  
>   
>  The following XML demonstrates a driver that supports two platforms. For more information about the supported platforms schema, see [Operating System Deployment Driver Supported Platforms Schema](../../develop/reference/osd/operating-system-deployment-driver-supported-platforms-schema.md).  

```  
<PlatformApplicabilityConditions>  
    <PlatformApplicabilityCondition DisplayName="All x64 Windows XP Professional" MaxVersion="5.20.9999.9999" MinVersion="5.20.3790.0" Name="Win NT" Platform="x64">  
        <Query1>SELECT * FROM Win32_OperatingSystem WHERE BuildNumber = '3790' AND OSType=18 AND ProductType=1</Query1>   
        <Query2>SELECT * FROM Win32_Processor WHERE Architecture=9 AND DataWidth=64</Query2>   
        </PlatformApplicabilityCondition>  
    <PlatformApplicabilityCondition DisplayName="All x86 Windows 2000" MaxVersion="5.00.9999.9999" MinVersion="5.00.0000.0" Name="Win NT" Platform="I386">  
        <Query1>SELECT * FROM Win32_OperatingSystem WHERE BuildNumber = '2195' AND OSType=18 AND ServicePackMajorVersion >= 4</Query1>   
        <Query2>SELECT * FROM Win32_Processor WHERE Architecture=0</Query2>   
    </PlatformApplicabilityCondition>  
</PlatformApplicabilityConditions>  
```  

 To validate the platform applicability requirements, use the [SMS_SupportedPlatforms Server WMI Class](../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md) class `Condition` property for the required platform.  

### To specify the supported platforms for a driver  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_Driver Server WMI Class](../../develop/reference/osd/sms_driver-server-wmi-class.md) object for the driver. The driver is identified by the key property `CI_ID`. For information about getting objects by using a key property, see [How to Read a Configuration Manager Object by Using Managed Code](../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)  

3.  Update the driver XML.  

4.  Commit the changes back to the SMS Provider.  

## Example  
 The following example method adds a supported platform to the driver that is identified by `objDriver`. For example, the following calling code adds Windows XP Professional x64 operating system to the driver `objDriver` list of supported platforms. You can get the details for a specific platform from its `SMS_SupportedPlatforms` object instance.  

 `AddSupportedPlatform objDriver, "All x64 Windows XP Professional", "5.20.9999.9999","5.20.3790.0", "Win NT","x64", "SELECT * FROM Win32_OperatingSystem WHERE BuildNumber = 3790 AND OSType=18 AND ProductType=1", "SELECT * FROM Win32_Processor WHERE Architecture=9 AND DataWidth=64"`  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddSupportedPlatform( objDriver, sDisplayName, sMaxVersion, sMinVersion, sName, sPlatform, sQuery1, sQuery2 )  

    Dim xmlDoc  
    Dim objPlatformNode  
    Dim objAttr  
    Dim objQuery1Node  
    Dim objQuery2Node  
    Dim objPlatformsNode  
    Dim objDriverNode  

    ' Load the SDM Package XML.  
    Set xmlDoc = CreateObject("Msxml2.DOMDocument.6.0")  

    xmlDoc.async = False  
    xmlDoc.loadXML(objDriver.Properties_.item("SDMPackageXML"))  
    xmlDoc.setProperty _  
     "SelectionNamespaces","xmlns:dcm='http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration'"  

    ' Create a new platform node.  
    Set objPlatformNode = xmlDoc.createNode _  
    ( 1, "PlatformApplicabilityCondition", _  
     "http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration")  

    ' Set DisplayName.  
    Set objAttr = xmlDoc.createAttribute("DisplayName")  
    objAttr.value = sDisplayName  
    objPlatformNode.setAttributeNode(objAttr)  

    ' Set MaxVersion.  
    Set objAttr = xmlDoc.createAttribute("MaxVersion")  
    objAttr.value = sMaxVersion  
    objPlatformNode.setAttributeNode(objAttr)  

    ' Set MinVersion.  
    Set objAttr = xmlDoc.createAttribute("MinVersion")  
    objAttr.value = sMinVersion  
    objPlatformNode.setAttributeNode(objAttr)  

    ' Set Name.  
    Set objAttr = xmlDoc.createAttribute("Name")  
    objAttr.value = sName  
    objPlatformNode.setAttributeNode(objAttr)  

    ' Set Platform.  
    Set objAttr = xmlDoc.createAttribute("Platform")  
    objAttr.value = sPlatform  
    objPlatformNode.setAttributeNode(objAttr)  

    ' Set Query1.  
    Set objQuery1Node = xmlDoc.createNode(1, "Query1", "http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration")  
    objQuery1Node.text = sQuery1  
    objPlatformNode.appendChild(objQuery1Node)  

    ' Set Query2.  
    Set objQuery2Node = xmlDoc.createNode(1, "Query2", "http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration")  
    objQuery2Node.text = sQuery2  
    objPlatformNode.appendChild(objQuery2Node)  

    ' Append to platforms node.  
    Set objPlatformsNode = xmlDoc.selectSingleNode("/dcm:DesiredConfigurationDigest/dcm:Driver/dcm:PlatformApplicabilityConditions")      
    objPlatformsNode.appendChild(objPlatformNode)  

    ' Increment the version number.  
    Set objDriverNode = xmlDoc.selectSingleNode("/dcm:DesiredConfigurationDigest/dcm:Driver")  
    Set objAttr = objDriverNode.attributes.getNamedItem("Version")  
    objAttr.value = objAttr.value + 1  

    ' Save the object.  
    objDriver.Properties_.item("SDMPackageXML") = xmlDoc.xml  
    objDriver.Put_  

End Sub  
```  

```c#  
public void AddSupportedPlatform(  
    IResultObject driver,  
    string displayName,  
    string maxVersion,  
    string minVersion,  
    string name,  
    string platform,  
    string query1,  
    string query2)  
{  
    try  
    {  
        XmlDocument xmlDoc = new XmlDocument();  
        xmlDoc.LoadXml(driver["SDMPackageXML"].StringValue);  

        string dcmXmlNamespace = "http://schemas.microsoft.com/SystemsCenterConfigurationManager/2006/03/24/DesiredConfiguration";  
        XmlNode condition = xmlDoc.CreateNode  
         (XmlNodeType.Element, "PlatformApplicabilityCondition", dcmXmlNamespace);  

        XmlAttribute displayNameAttribute = xmlDoc.CreateAttribute("DisplayName");  
        displayNameAttribute.Value = displayName;  
        condition.Attributes.SetNamedItem(displayNameAttribute);  

        XmlAttribute osMaxVersionAttribute = xmlDoc.CreateAttribute("MaxVersion");  
        osMaxVersionAttribute.Value = maxVersion;  
        condition.Attributes.SetNamedItem(osMaxVersionAttribute);  

        XmlAttribute osMinVersionAttribute = xmlDoc.CreateAttribute("MinVersion");  
        osMinVersionAttribute.Value = minVersion;  
        condition.Attributes.SetNamedItem(osMinVersionAttribute);  

        XmlAttribute osNameAttribute = xmlDoc.CreateAttribute("Name");  
        osNameAttribute.Value = name;  
        condition.Attributes.SetNamedItem(osNameAttribute);  

        XmlAttribute osPlatformAttribute = xmlDoc.CreateAttribute("Platform");  
        osPlatformAttribute.Value = platform;  
        condition.Attributes.SetNamedItem(osPlatformAttribute);  

        // Create <Query1/> and <Query2/> child nodes.  
        // Then attach to <PlatformApplicabilityCondition/>.  
        XmlNode query1Node = xmlDoc.CreateNode  
            (XmlNodeType.Element, "Query1", dcmXmlNamespace);  
        query1Node.InnerText = query1;  
        condition.AppendChild(query1Node);  

        XmlNode query2Node = xmlDoc.CreateNode  
            (XmlNodeType.Element, "Query2", dcmXmlNamespace);  
        query2Node.InnerText = query2;  
        condition.AppendChild(query2Node);  

        XmlNode platformsNode = xmlDoc["DesiredConfigurationDigest"]["Driver"]["PlatformApplicabilityConditions"];  

         if (platformsNode == null)  
        {  
            Console.WriteLine("empty");  
        }  

        platformsNode.AppendChild(condition);  

        XmlNode driverNode = xmlDoc["DesiredConfigurationDigest"]["Driver"];  
        if (driverNode != null)  
        {  
            int driverVersion = int.Parse(driverNode.Attributes.GetNamedItem("Version").Value) + 1;  
            driverNode.Attributes.GetNamedItem("Version").Value = (driverVersion + 1).ToString();  
        }  
        else  
        {  
            throw new XmlException("Unable to find <Driver/> node while AddingSupportedPlatforms");  
        }  

        // Add the package XML to the driver.  
        StringBuilder xmlText = new StringBuilder();  
        xmlDoc.WriteContentTo(new XmlTextWriter(new StringWriter(xmlText)));  
        driver["SDMPackageXML"].StringValue = xmlText.ToString();  

       driver.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("failed to add supported platform to driver " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`driver`<br /><br /> `objDriver`|-   Managed: `IResultObject`<br />-   VBScript:  [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|-   A valid [SMS_Driver](../../develop/reference/osd/sms_driver-server-wmi-class.md) object. For more information, see [How to Import a Windows Driver Described by an INF File into Configuration Manager](../../develop/osd/how-to-import-a-windows-driver-described-by-an-inf-file.md).|  
|`displayName`<br /><br /> `sDisplayName`|-   Managed: `String`<br />-   VBScript: `String`|The display name for the condition shown in the System Center Configuration Manager console.|  
|`maxVersion`<br /><br /> `sMaxVersion`|-   Managed: `String`<br />-   VBScript: `String`|The maximum supported version.|  
|`minVersion`<br /><br /> `sMinVersion`|-   Managed: `String`<br />-   VBScript: `String`|The minimum supported version.|  
|`name`<br /><br /> `sName`|-   Managed: `String`<br />-   VBScript: `String`|The operating system name.|  
|`platform`<br /><br /> `sPlatform`|-   Managed: `String`<br />-   VBScript: `String`|The platform name.|  
|`query1`<br /><br /> `sQuery1`|-   Managed: `String`<br />-   VBScript: `String`|The first query used to identify the client platform.|  
|`query2`<br /><br /> `sQuery2`|-   Managed: `String`<br />-   VBScript: `String`|The second query used to identify the client platform.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 System.Xml  

 System.IO  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [SMS_SupportedPlatforms Server WMI Class](../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md)   
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Objects](../../develop/core/understand/configuration-manager-objects.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Move a Step to a Different Operating System Deployment Task Sequence Group](../../develop/osd/how-to-move-a-step-to-a-different-task-sequence-group.md)   
 [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md)   
 [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)   
 [SMS_SupportedPlatforms Server WMI Class](../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md)
