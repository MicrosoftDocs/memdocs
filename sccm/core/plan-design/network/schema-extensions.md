---
title: "Schema extensions"
titleSuffix: "Configuration Manager"
description: "Extend the Active Directory schema to support System Center Configuration Manager."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe
robots: noindex

---
# Schema extensions for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can extend the Active Directory schema to support Configuration Manager. This edits a forest's Active Directory schema to add a new container and several attributes that Configuration Manager sites use to publish key information in Active Directory where clients can securely use it. This information can simplify the deployment and configuration of clients and helps clients locate site resources like servers with deployed content or that provide different services to clients.  

-   It's a good idea to extend the Active Directory schema, but it's not required.  

Before you [extend the Active Directory schema](https://docs.microsoft.com/en-us/sccm/core/plan-design/network/extend-the-active-directory-schema), you should be familiar with Active Directory Domain Services and comfortable with [modifying the Active Directory schema](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## Considerations for extending the Active Directory schema for Configuration Manager  

-   The Active Directory schema extensions for System Center Configuration Manager are unchanged from those that Configuration Manager 2007 and Configuration Manager 2012 use. If you previously extended the schema for either version, you do not have to extend the schema again.  

-   Extending the schema is a forest-wide, one-time, irreversible action.  

-   Only a user who is a member of the Schema Admins Group or who has been delegated sufficient permissions to change the schema can extend the schema.  

-   Although you can extend the schema before or after you run Configuration Manager Setup, it's a good idea to extend the schema before you start to configure your sites and hierarchy settings. This can simplify many of the later configuration steps.  

-   After you extend the schema, the Active Directory global catalog is replicated throughout the forest. Therefore, plan to extend the schema when the replication traffic will not adversely affect other network-dependent processes:  

    -   In Windows 2000 forests, extending the schema causes a full sync of the whole global catalog.  

    -   Beginning with Windows 2003 forests, only the newly added attributes are replicated.  

**Devices and clients that do not use the Active Directory schema:**  

-   Mobile devices that are managed by the Exchange Server connector  

-   The client for Mac computers  

-   The client for Linux and UNIX servers  

-   Mobile devices that are enrolled by Configuration Manager  

-   Mobile devices that are enrolled by Microsoft Intune  

-   Mobile device legacy clients  

-   Windows clients that are configured for Internet-only client management  

-   Windows clients that are detected by Configuration Manager to be on the Internet  

## Capabilities that benefit from extending the schema  
**Client computer installation and site assignment** - When a Windows computer installs a new client, the client searches Active Directory Domain Services for installation properties.  

-   **Workarounds:** If you do not extend the schema, use one of the following options to provide configuration details that computers must install:  

    -   **Use client push installation**. Before you use a client installation method, make sure that all prerequisites are met. For more information, see the 'Installation Method Dependencies' section in [Prerequisites for deploying clients to Windows computers](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers).  

    -   **Install clients manually** and provide client installation properties by using CCMSetup installation command-line properties. This must include the following:  

        -   Specify a management point or source path from which the computer can download the installation files by using the CCMSetup property **/mp:=&lt;management point name computer name\>** or **/source:&lt;path to client source files\>** on the CCMSetup command line during client installation.  

        -   Specify a list of initial management points for the client to use so that it can assign them to the site and then download client policy and site settings. Use the CCMSetup Client.msi property SMSMP to do this.  

    -   **Publish the management point in DNS or WINS** and configure clients to use this service location method.  

**Port configuration for client-to-server communication** - When a client installs, it is configured with port information stored in Active Directory. If you later change the client-to-server communication port for a site, a client can get this new port setting from Active Directory Domain Services.  

-   **Workarounds:** If you do not extend the schema, use one of the following options to provide new port configurations to existing clients:  

    -   **Reinstall clients** by using options that configure the new port.  

    -   **Deploy a custom script to clients that updates the port information**. If clients cannot communicate with a site because of a port change, you cannot use Configuration Manager to deploy this script. For example, you could use Group Policy.  

**Content deployment scenarios** - When you create content at one site and then deploy that content to another site in the hierarchy, the receiving site must be able to verify the signature of the signed content data. This requires access to the public key of the source site where you create this data. When you extend the Active Directory schema for Configuration Manager, a site's public key is available to all sites in the hierarchy.  

-   **Workaround:** If you do not extend the schema, use the hierarchy maintenance tool, **preinst.exe**, to exchange the secure key information between sites.  

     For example, if you plan to create content at a primary site and deploy that content to a secondary site below a different primary site, you must either extend the Active Directory schema to let the secondary site get the source primary site's public key, or use preinst.exe to share keys between the two sites directly.  

## Active Directory attributes and classes  
When you extend the schema for System Center Configuration Manager, the following classes and attributes are added to the schema and available to all Configuration Manager sites in that Active Directory forest.  

-   Attributes:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        on  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classes:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  

>  The  schema extensions might include attributes and classes that are carried forward from previous versions of the product but not used by System Center Configuration Manager. For example:  

>   
>  -   Attribute: cn=MS-SMS-Site-Boundaries  
> -   Class: cn=MS-SMS-Server-Locator-Point  

You can ensure the preceding lists are current by viewing the **ConfigMgr_ad_schema.LDF** file from the **\SMSSETUP\BIN\x64** folder of the System Center Configuration Manager installation media.  
