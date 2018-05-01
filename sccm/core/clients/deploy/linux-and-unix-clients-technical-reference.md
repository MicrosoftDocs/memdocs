---
title: "UNIX/Linux client component services and commands"
titleSuffix: "Configuration Manager"
description: "Learn about component services and commands on Linux and UNIX clients in System Center Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Linux and UNIX clients component services and commands for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


 The following table identifies the client component services of the Configuration Manager client for Linux and UNIX.  

|File name|More information|  
|---------------|----------------------|  
|ccmexec.bin|This service is equivalent to the ccmexc service on a Windows-based client. It is responsible for all communications with Configuration Manager site system roles, and also communicates with the omiserver.bin service to collect hardware inventory from the local computer.<br /><br /> For a list of supported command line arguments, run **ccmexec -h**|  
|omiserver.bin|This service is the CIM server. The CIM server provides a framework for pluggable software modules called providers. Providers interact with Linux and UNIX computer resources and collect the hardware inventory data. For example, the **process provider** for a Linux computer collects data associated with the Linux operating system processes.|  

 The following tables list commands that you can use to start, stop, or restart the client services (ccmexec.bin and omiserver.bin) on each version of Linux or UNIX. When you start or stop the ccmexec service, the omiserver service also starts or stops.  

|Operating system|Commands|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 and SLES 9|Start: **/etc/init d/ccmexecd start**<br /><br /> Stop: **/etc/init d/ccmexecd stop**<br /><br /> Restart: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Start: **/etc/init d/ccmexecd start**<br /><br /> Stop: **/etc/init d/ccmexecd stop**<br /><br /> Restart: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Start:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Stop:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Start:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Stop:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Start:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Stop:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Start: **/sbin/init.d/ccmexecd start**<br /><br /> Stop: **/sbin/init.d/ccmexecd stop**<br /><br /> Restart: **/sbin/init.d/ccmexecd restart**|  
