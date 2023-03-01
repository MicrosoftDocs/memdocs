---
title: Evaluation of the computer information for a specific computer report
titleSuffix: Configuration Manager
description: A predefined report in Configuration Manager that combines multiple SQL views to obtain the required data.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3c4286f0-b210-4ea3-a58e-342b2f9a98f2
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Evaluation of the Computer information for a specific computer report in Configuration Manager

The **Computer information for a specific computer** report is one of the predefined reports in Configuration Manager, and is a good example of a report that combines multiple SQL views to obtain the required data. To open the report properties, use the following procedure:

## To examine the Computer information for a specific computer report

1. In the Configuration Manager console, select **Monitoring**.
1. In the **Monitoring** workspace, select Reporting, and then select **Reports**.
1. From the list of displayed reports, select **Computer information for a specific computer** and then, in the **Home** tab, in the **Report Group** group, select **Edit**.
1. After Report Builder opens, in the **Report Data** pane, expand **Datasets** and then double-click **DataSet0** to examine the SQL statement for the report which appears as follows:
    
   ```sql
        SELECT distinct SYS.Netbios_Name0, SYS.User_Name0, SYS.User_Domain0,  SYS.Resource_Domain_OR_Workgr0,
                    OPSYS.Caption0 as C054, OPSYS.Version0,
                    MEM.TotalPhysicalMemory0,
                    STUFF((SELECT (N','+IPAddr.IP_Addresses0) AS [text()]
                    FROM fn_rbac_RA_System_IPAddresses(@UserSIDs)  IPAddr
                    WHERE SYS.ResourceID = IPAddr.ResourceID for xml path(N''))
                    ,1,1,N'') as IP_Addresses0, -- if there are multiple IP address then combine them together
                    Processor.Manufacturer0,
                    CSYS.Model0, Processor.Name0, Processor.MaxClockSpeed0, SYS.Is_AOAC_Capable0
                    FROM fn_rbac_R_System(@UserSIDs)  SYS
                    LEFT JOIN  fn_rbac_GS_X86_PC_MEMORY(@UserSIDs)  MEM on SYS.ResourceID = MEM.ResourceID
                    LEFT JOIN  fn_rbac_GS_COMPUTER_SYSTEM(@UserSIDs)  CSYS on SYS.ResourceID = CSYS.ResourceID
                    LEFT JOIN  fn_rbac_GS_PROCESSOR(@UserSIDs)  Processor  on Processor.ResourceID = SYS.ResourceID
                    LEFT JOIN fn_rbac_GS_OPERATING_SYSTEM(@UserSIDs)  OPSYS on SYS.ResourceID=OPSYS.ResourceID
                    WHERE SYS.Netbios_Name0 = @variable
                    ORDER BY SYS.Netbios_Name0, SYS.Resource_Domain_OR_Workgr0
   ```

1. Close the **Dataset Properties** dialog box and then double-click **DataSetAdminID** to examine the SQL statement that presents a list of possible computers for the user to choose. This appears as follows:
    
   ```sql
        SELECT dbo.fn_rbac_GetAdminIDsfromUserSIDs(@UserTokenSIDs) as userSIDs
   ```
   
   This report contains a more complex SQL statement that combines multiple SQL views to obtain the desired data. The query results will list the NetBIOS name, user name, operating system, memory, and more with the NetBIOS name used as the variable in the report prompt **(WHERE SYS.Netbios_Name0 = @variable)**. The query retrieves information from six different SQL Server views (**v_R_System**, **v_RA_System_IPAddresses**, **v_GS_X86_PC_MEMORY**, **v_GS_COMPUTER_SYSTEM**, **v_GS_PROCESSOR**, and **v_GS_OPERATING_SYSTEM**) that are joined together by using the **ResourceID** column from the **v_R_System** view and where the NetBIOS name in the **v_R_System** view is equal to the one provided in the report prompt. Finally, the results are ordered first by the **Netbios Name** column and then the **User Domain** column.

   The report prompt will display **Computer Name** as the prompt text and has a variable named **variable** that will be populated by the user. You can examine details about the variables and parameters used by the report in the **Parameters** node of the **Report Data** pane.
1. Close Report Builder.

## See also

[Evaluation of the All collections report in Configuration Manager](evaluation-all-collections-report-configuration-manager.md)  
