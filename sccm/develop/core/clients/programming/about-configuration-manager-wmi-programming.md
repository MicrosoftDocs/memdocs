---
title: "About Configuration Manager WMI Programming"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a7d16ad6-fc1f-4eb5-a190-1d9fc06c3678
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Configuration Manager WMI Programming
Programming the System Center Configuration Manager client Windows Management Instrumentation (WMI) provider differs according to the programming language you use.  

## C#  
 If you are using C#, you should use the System.Management namespace, which provides access to a rich set of management information and management events about the system, devices, and applications that are instrumented to the WMI infrastructure.  

> [!NOTE]
>  The managed System Center Configuration Manager library is for use with a System Center Configuration Manager site server and cannot be used to access client WMI namespaces.  

 For more information about connecting to the Configuration Manager client WMI namespace by using the System.Management namespace, see [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md).  

 For more information about using Configuration Manager client WMI namespace objects by using the System.Management namespace, see [How to Read a WMI Object by Using System.Management](../../../../develop/core/clients/programming/how-to-read-a-wmi-object-by-using-system.management.md).  

 For more information about using the System.Management namespace, see [System.Management Namespace](http://go.microsoft.com/fwlink/?LinkID=84308).  

## VBScript  
 If you are using VBScript you access and use Configuration Manager client WMI objects by using the same coding techniques that are used for accessing other WMI objects, including the Configuration Manager WMI objects. For more information see the [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950).  

## Client WMI Namespace  
 The Configuration Manager client WMI namespace begins at \\\\<client\>\root\ccm. For example, root\ccm contains the [SMS_Client](../../../../develop/reference/core/clients/client-classes/sms_client-client-wmi-class.md) class that can be used to get and set client information.  

## See Also  
 [Configuration Manager Programming Fundamentals](../../../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Call a WMI Class Method by Using System.Management](../../../../develop/core/clients/programming/how-to-call-a-wmi-class-method-by-using-system.management.md)   
 [How to Connect to the Configuration Manager Client WMI Namespace by Using System.Management](../../../../develop/core/clients/programming/how-to-connect-to-the-client-wmi-namespace.md)   
 [How to Perform an Asynchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-an-asynchronous-query-by-using-system.management.md)   
 [How to Perform a Synchronous Query by Using System.Management](../../../../develop/core/clients/programming/how-to-perform-a-synchronous-query-by-using-system.management.md)   
 [How to Read a WMI Object by Using System.Management](../../../../develop/core/clients/programming/how-to-read-a-wmi-object-by-using-system.management.md)   
 [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=43950)   
 [System.Management Namespace](http://go.microsoft.com/fwlink/?LinkId=111708)
