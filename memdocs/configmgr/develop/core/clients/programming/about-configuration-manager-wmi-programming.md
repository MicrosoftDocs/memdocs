---
title: About Configuration Manager WMI Programming
titleSuffix: Configuration Manager
description: Programming the Configuration Manager client WMI provider differs according to the programming language you use.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: concept-article
ms.assetid: a7d16ad6-fc1f-4eb5-a190-1d9fc06c3678
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3


---
# About Configuration Manager WMI programming

Programming the Configuration Manager client Windows Management Instrumentation (WMI) provider differs according to the programming language you use.

## C&#35;

If you use C#, use the System.Management namespace. It provides access to a rich set of management information and management events about the system, devices, and applications that are instrumented to the WMI infrastructure.  

> [!NOTE]
> The managed Configuration Manager library is for use with a Configuration Manager site server and cannot be used to access client WMI namespaces.  

For more information about connecting to the Configuration Manager client WMI namespace by using the System.Management namespace, see [How to connect to the Configuration Manager client WMI namespace by using System.Management](how-to-connect-to-the-client-wmi-namespace.md).

For more information about using Configuration Manager client WMI namespace objects by using the System.Management namespace, see [How to read a WMI object by using System.Management](how-to-read-a-wmi-object-by-using-system.management.md).

For more information about using the System.Management namespace, see [System.Management Namespace](/dotnet/api/system.management).

## VBScript

If you use VBScript, you access and use Configuration Manager client WMI objects by using the same coding techniques that are used for accessing other WMI objects, including the Configuration Manager WMI objects. For more information, see the [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page).

## Client WMI namespace

The Configuration Manager client WMI namespace begins at `\\<client>\root\ccm`. For example, `root\ccm` contains the [SMS_Client](../../../reference/core/clients/client-classes/sms_client-client-wmi-class.md) class that can be used to get and set client information.

## See also

- [How to call a WMI class method by using System.Management](how-to-call-a-wmi-class-method-by-using-system.management.md)
- [How to connect to the Configuration Manager client WMI namespace by using System.Management](how-to-connect-to-the-client-wmi-namespace.md)
- [How to perform an asynchronous query by using System.Management](how-to-perform-an-asynchronous-query-by-using-system.management.md)
- [How to perform a synchronous query by using System.Management](how-to-perform-a-synchronous-query-by-using-system.management.md)
- [How to read a WMI object by using System.Management](how-to-read-a-wmi-object-by-using-system.management.md)
- [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)
- [System.Management namespace](/dotnet/api/system.management)
