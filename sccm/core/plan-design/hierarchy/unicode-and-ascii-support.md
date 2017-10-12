---
title: "Unicode and ASCII Support"
titleSuffix: "Configuration Manager"
description: "Learn about support for Unicode and ASCII characters in System Center Configuration Manager objects."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Unicode and ASCII support in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager creates most objects by using Unicode characters. However, several objects support ASCII characters only or they have other limitations.  

 The following sections list the objects that must use characters from the ASCII character set only, or that have additional limitations.  

-   [Objects that use ASCII characters](#BKMK_ASCIIchar)  

-   [Additional limitations](#BKMK_OtherCharLimitations)  

-   [Configuration Manager objects that are not localized](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objects that use ASCII characters  
 Configuration Manager supports the ASCII character set only when you create the following objects:  

-   Site code  

-   All site system server computer names  

-   The following Configuration Manager accounts:  

    > [!NOTE]  
    >  These accounts support ASCII characters and RUS characters on a site that runs in Russian.  

    -   Client push installation account  

    -   Health state reference publishing account  

    -   Health state reference querying account  

    -   Management point database connect account  

    -   Network access account  

    -   Package access account  

    -   Standard sender account  

    -   Site system installation account  

    -   Software update point connection account  

    -   Software update point proxy server account  

    > [!NOTE]  
    >  The accounts that you specify for role-based administration support Unicode.  
    >   
    >  The Reporting Services point account supports Unicode, with the exception of RUS characters.  

-   Fully-qualified domain name (FQDN) for site servers and site systems  

-   Installation path for Configuration Manager  

-   SQL Server instance names  

-   The path for the following site system roles:  

    -   Application Catalog web service point  

    -   Application Catalog website point  

    -   Enrollment point  

    -   Enrollment proxy point  

    -   Reporting services point  

    -   State migration point  

-   The path for the following folders:  

    -   The folder that stores client state migration data  

    -   The folder that contains the Configuration Manager reports  

    -   The folder that stores the Configuration Manager backup  

    -   The folder that stores the installation source files for site setup  

    -   The folder that stores the prerequisite downloads for use by setup  

-   The path for the following objects:  

    -   IIS website  

    -   Virtual application installation path  

    -   Virtual application name  

-   The following objects for AMT and out-of-band management:  

    -   The FQDN of the AMT-based computer  

    -   The computer name of the AMT-based computer  

    -   The domain NetBIOS name  

    -   The wireless profile name and SSID  

    -   The trusted root certification authority name  

    -   The name of the certification authority (CA) and template names  

    -   The file name and path for the IDE redirection image file  

    -   The contents of the AMT data storage  

-   Boot media ISO file names  

##  <a name="BKMK_OtherCharLimitations"></a> Additional limitations  
 The following are additional limitations for supported character sets and language versions:  

-   Configuration Manager does not support changing the locale of the site server computer.  

-   An enterprise certification authority (CA) does not support client computer names that use double-byte character sets (DBCS). The client computer names that you can use are restricted by the PKI limitation of the IA5 character set. In addition, Configuration Manager does not support CA names or subject name values that use DBCS.  

##  <a name="BKMK_LangNonLocalize"></a> Configuration Manager objects that are not localized  
 The Configuration Manager database supports Unicode for most objects that it stores, and when possible, it displays this information in the operating system language that matches the locale of a computer. For the client interface or Configuration Manager console to display information in the computer's operating system language, the computer's locale must match a client or server language that you install at a site.  

 However, several Configuration Manager objects do not support Unicode, and they are stored in the database by using ASCII, or they have additional language limitations. This information is always displayed by using the ASCII character set or in the language that was in use when the object was created.  
