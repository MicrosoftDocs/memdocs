---
title: "Create custom reports"
titleSuffix: "Configuration Manager"
description: "Define report models to meet your business requirements, and then deploy the report models to Configuration Manager."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Creating custom report models for System Center Configuration Manager in SQL Server Reporting Services*Applies to: System Center Configuration Manager (Current Branch)*
Sample report models are included in System Center Configuration Manager, but you can also define report models to meet your own business requirements, and then deploy the report model to Configuration Manager to use when you create new model-based reports. The following table provides the steps to create and deploy a basic report model.  

> [!NOTE]  
>  For the steps to create a more advanced report model, see the [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) section in this topic.  

|Step|Description|More information|  
|----------|-----------------|----------------------|  
|Verify that SQL Server Business Intelligence Development Studio is installed|Report models are designed and built by using SQL Server Business Intelligence Development Studio. Verify that SQL Server Business Intelligence Development Studio is installed on the computer on which you are creating the custom report model.|For more information about SQL Server Business Intelligence Development Studio, see the SQL Server 2008 documentation.|  
|Create a report model project|A report model project contains the definition of the data source (a .ds file), the definition of a data source view (a .dsv file), and the report model (an .smdl file).|For more information, see the [To create the report model project](#BKMK_CreateReportModelProject) section in this topic.|  
|Define a data source for a report model|After creating a report model project, you have to define one data source from which you extract business data. Typically, this is the Configuration Manager site database.|For more information, see the [To define the data source for the report model](#BKMK_DefineReportModelDataSource) section in this topic.|  
|Define a data source view for a report model|After defining the data sources that you use in your report model project, the next step is to define a data source view for the project. A data source view is a logical data model based on one or more data sources. Data source views encapsulate access to the physical objects, such as tables and views, contained in underlying data sources. SQL Server Reporting Services generates the report model from the data source view.<br /><br /> Data source views facilitate the model design process by providing you with a useful representation of the data that you specified. Without changing the underlying data source, you can rename tables and fields, and add aggregate fields and derived tables in a data source view. For an efficient model, add only those tables to the data source view that you intend to use.|For more information, see the [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) section in this topic.|  
|Create a report model|A report model is a layer on top of a database that identifies business entities, fields, and roles. When published, by using these models, Report Builder users can develop reports without having to be familiar with database structures or understand and write queries. Models are composed of sets of related report items that are grouped together under a friendly name, with predefined relationships between these business items and with predefined calculations. Models are defined by using an XML language called Semantic Model Definition Language (SMDL). The file name extension for report model files is .smdl.|For more information, see the [To create the report model](#BKMK_CreateReportModel) section in this topic.|  
|Publish a report model|To build a report by using the model that you just created, you must publish it to a report server. The data source and data source view are included in the model when it is published.|For more information, see the [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) section in this topic.|  
|Deploy the report model to Configuration Manager|Before you can use a custom report model in the **Create Report Wizard** to create a model-based report, you must deploy the report model to Configuration Manager.|For more information, see the [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) section in this topic.|  

## Steps for creating a basic report model in SQL Server Reporting Services  
 You can use the following procedures to create a basic report model that users in your site can use to build particular model-based reports based on data in a single view of the Configuration Manager database. You create a report model that presents information about the client computers in your site to the report author. This information is taken from the **v_R_System** view in the Configuration Manager database.  

 On the computer where you perform these procedures, ensure that you have installed SQL Server Business Intelligence Development Studio and that the computer has network connectivity to the reporting services point server. For detailed information about SQL Server Business Intelligence Development Studio, see the SQL Server 2008 documentation.  

###  <a name="BKMK_CreateReportModelProject"></a> To create the report model project  

1.  On the desktop, click **Start**, click **Microsoft SQL Server 2008**, and then click **SQL Server Business Intelligence Development Studio**.  

2.  After **SQL Server Business Intelligence Development Studio** opens in Microsoft Visual Studio, click **File**, click **New**, and then click **Project**.  

3.  In the **New Project** dialog box, select **Report Model Project** in the **Templates** list.  

4.  In the **Name** box, specify a name for this report model. For this example, type **Simple_Model**.  

5.  To create the report model project, click **OK**.  

6.  The **Simple_Model** solution is displayed in **Solution Explorer**.  

    > [!NOTE]  
    >  If you cannot see the **Solution Explorer** pane, click **View**, and then click **Solution Explorer**.  

###  <a name="BKMK_DefineReportModelDataSource"></a> To define the data source for the report model  

1.  In the **Solution Explorer** pane of **SQL Server Business Intelligence Development Studio**, right-click **Data Sources** to select **Add New Data Source**.  

2.  On the **Welcome to the Data Source Wizard** page, click **Next**.  

3.  On the **Select how to define the connection** page, verify that **Create a data source based on an existing or new connection** is selected, and then click **New**.  

4.  In the **Connection Manager** dialog box, specify the following connection properties for the data source:  

    -   **Server name**: Type the name of your Configuration Manager site database server, or select it in the list. If you are working with a named instance instead of the default instance, type &lt;*database server*>\\&lt;*instance name*>.  

    -   Select **Use Windows Authentication**.  

    -   In **Select or enter a database name** list, select the name of your Configuration Manager site database.  

5.  To verify the database connection, click **Test Connection**.  

6.  If the connection succeeds, click **OK** to close the **Connection Manager** dialog box. If the connection does not succeed, verify that the information you entered is correct, and then click **Test Connection** again.  

7.  On the **Select how to define the connection** page, verify that **Create a data source based on an existing or new connection** is selected, verify that the data source you have just specified is selected in **Data connections**, and then click **Next**.  

8.  In **Data source name**, specify a name for the data source, and then click **Finish**. For this example, type **Simple_Model**.  

9. The data source **Simple_Model.ds** is now displayed in **Solution Explorer** under the **Data Sources** node.  

    > [!NOTE]  
    >  To edit the properties of an existing data source, double-click the data source in the **Data Sources** folder of the **Solution Explorer** pane to display the data source properties in Data Source Designer.  

###  <a name="BKMK_DefineReportModelDataSourceView"></a> To define the data source view for the report model  

1.  In **Solution Explorer**, right-click **Data Source Views** to select **Add New Data Source View**.  

2.  On the **Welcome to the Data Source View Wizard** page, click **Next**. The **Select a Data Source** page is displayed.  

3.  In the **Relational data sources** window, verify that the **Simple_Model** data source is selected, and then click **Next**.  

4.  On the **Select Tables and Views** page, select the following view in the **Available objects** list to be used in the report model: **v_R_System (dbo)**.  

    > [!TIP]  
    >  To help locate views in the **Available objects** list, click the **Name** heading at the top of the list to sort the objects in alphabetical order.  

5.  After selecting the view, click **>** to transfer the object to the **Included objects** list.  

6.  If the **Name Matching** page is displayed, accept the default selections, and click **Next**.  

7.  When you have selected the objects that you require, click **Next**, and then specify a name for the data source view. For this example, type **Simple_Model**.  

8.  Click **Finish**. The **Simple_Model.dsv** data source view is displayed in the **Data Source Views** folder of **Solution Explorer**.  

###  <a name="BKMK_CreateReportModel"></a> To create the report model  

1.  In **Solution Explorer**, right-click **Report Models** to select **Add New Report Model**.  

2.  On the **Welcome to the Report Model Wizard** page, click **Next**.  

3.  On the **Select Data Source Views** page, select the data source view in the **Available data source views** list, and then click **Next**. For this example, select **Simple_Model.dsv**.  

4.  On the **Select report model generation rules** page, accept the default values, and then click **Next**.  

5.  On the **Collect Model Statistics** page, verify that **Update model statistics before generating** is selected, and then click **Next**.  

6.  On the **Completing the Wizard** page, specify a name for the report model. For this example, verify that **Simple_Model** is displayed.  

7.  To complete the wizard and create the report model, click **Run**.  

8.  To exit the wizard, click **Finish**. The report model is shown in the Design window.  

###  <a name="BKMK_PublishReportModel"></a> To publish the report model for use in SQL Server Reporting Services  

1.  In **Solution Explorer**, right-click the report model to select **Deploy**. For this example, the report model is **Simple_Model.smdl**.  

2.  Examine the deployment status at the lower left corner of the **SQL Server Business Intelligence Development Studio** window. When the deployment has finished, **Deploy Succeeded** is displayed. If the deployment fails, the reason for the failure is displayed in the **Output** window. The new report model is now available on your SQL Server Reporting Services website.  

3.  Click **File**, click **Save All**, and then close **SQL Server Business Intelligence Development Studio**.  

###  <a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1. Locate the folder in which you created the report model project. For example, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;Project Name\>.*  

2. Copy the following files from the report model project folder to a temporary folder on your computer:  

   -   *&lt;Model Name\>* **.dsv**  

   -   *&lt;Model Name\>* **.smdl**  

3. Open the preceding files by using a text editor, such as Notepad.  

4. In the file *&lt;Model Name\>***.dsv**, locate the first line of the file, which reads as follows:  

    **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

    Edit this line to read as follows:  

    **&lt;DataSourceView xmlns="<http://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView"\>**  

5. Copy the entire contents of the file to the Windows Clipboard.  

6. Close the file *&lt;Model Name\>***.dsv**.  

7. In the file *&lt;Model Name\>***.smdl**, locate the last three lines of the file, which appear as follows:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Paste the contents of the file *&lt;Model Name\>***.dsv** directly before the last line of the file (**&lt;SemanticModel\>**).  

9. Save and close the file *&lt;Model Name\>***.smdl**.  

10. Copy the file *&lt;Model Name\>***.smdl** to the folder *%programfiles%*\Microsoft Configuration Manager \AdminConsole\XmlStorage\Other on the Configuration Manager site server.  

    > [!IMPORTANT]  
    >  After copying the report model file to the Configuration Manager site server, you must exit and restart the Configuration Manager console before you can use the report model in the **Create Report Wizard**.  

##  <a name="AdvancedReportModel"></a> Steps for Creating an Advanced Report Model in SQL Server Reporting Services  
 You can use the following procedures to create an advanced report model that users in your site can use to build particular model-based reports based on data in multiple views of the Configuration Manager database. You create a report model that presents information about the client computers and the operating system installed on these computers to the report author. This information is taken from the following views in the Configuration Manager database:  

- **V_R_System**: Contains information about discovered computers and the Configuration Manager client.  

- **V_GS_OPERATING_SYSTEM**: Contains information about the operating system installed on the client computer.  

  Selected items from the preceding views are consolidated into one list, given friendly names, and then presented to the report author in Report Builder for inclusion in particular reports.  

  On the computer where you perform these procedures, ensure that you have installed SQL Server Business Intelligence Development Studio and that the computer has network connectivity to the reporting services point server. For detailed information about SQL Server Business Intelligence Development Studio, see the SQL Server documentation.  

#### To create the report model project  

1.  On the desktop, click **Start**, click **Microsoft SQL Server 2008**, and then click **SQL Server Business Intelligence Development Studio**.  

2.  After **SQL Server Business Intelligence Development Studio** opens in Microsoft Visual Studio, click **File**, click **New**, and then click **Project**.  

3.  In the **New Project** dialog box, select **Report Model Project** in the **Templates** list.  

4.  In the **Name** box, specify a name for this report model. For this example, type **Advanced_Model**.  

5.  To create the report model project, click **OK**.  

6.  The **Advanced_Model** solution is displayed in **Solution Explorer**.  

    > [!NOTE]  
    >  If you cannot see the **Solution Explorer** pane, click **View**, and then click **Solution Explorer**.  

#### To define the data source for the report model  

1.  In the **Solution Explorer** pane of **SQL Server Business Intelligence Development Studio**, right-click **Data Sources** to select **Add New Data Source**.  

2.  On the **Welcome to the Data Source Wizard** page, click **Next**.  

3.  On the **Select how to define the connection** page, verify that **Create a data source based on an existing or new connection** is selected, and then click **New**.  

4.  In the **Connection Manager** dialog box, specify the following connection properties for the data source:  

    -   **Server name**: Type the name of your Configuration Manager site database server, or select it in the list. If you are working with a named instance instead of the default instance, type &lt;*database server*>\\&lt;*instance name*>.  

    -   Select **Use Windows Authentication**.  

    -   In the **Select or enter a database name** list, select the name of your Configuration Manager site database.  

5.  To verify the database connection, click **Test Connection**.  

6.  If the connection succeeds, click **OK** to close the **Connection Manager** dialog box. If the connection does not succeed, verify that the information you entered is correct, and then click **Test Connection** again.  

7.  On the **Select how to define the connection** page, verify that **Create a data source based on an existing or new connection** is selected, verify that the data source you have just specified is selected in the **Data connections** list box, and then click **Next**.  

8.  In **Data source name**, specify a name for the data source and then click **Finish**. For this example, type **Advanced_Model**.  

9. The data source **Advanced_Model.ds** is displayed in **Solution Explorer** under the **Data Sources** node.  

    > [!NOTE]  
    >  To edit the properties of an existing data source, double-click the data source in the **Data Sources** folder of the **Solution Explorer** pane to display the data source properties in Data Source Designer.  

#### To define the data source view for the report model  

1. In **Solution Explorer**, right-click **Data Source Views** to select **Add New Data Source View**.  

2. On the **Welcome to the Data Source View Wizard** page, click **Next**. The **Select a Data Source** page is displayed.  

3. In the **Relational data sources** window, verify that the **Advanced_Model** data source is selected, and then click **Next**.  

4. On the **Select Tables and Views** page, select the following views in the **Available objects** list to be used in the report model:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     After selecting each view, click **>** to transfer the object to the **Included objects** list.  

   > [!TIP]  
   >  To help locate views in the **Available objects** list, click the **Name** heading at the top of the list to sort the objects in alphabetical order.  

5. If the **Name Matching** dialog box appears, accept the default selections, and click **Next**.  

6. When you have selected the objects you require, click **Next**, and then specify a name for the data source view. For this example, type **Advanced_Model**.  

7. Click **Finish**. The **Advanced_Model.dsv** data source view is displayed in the **Data Source Views** folder of **Solution Explorer**.  

#### To define relationships in the data source view  

1.  In **Solution Explorer**, double-click **Advanced_Model.dsv** to open the Design window.  

2.  Right-click the title bar of the **v_R_System** window to select **Replace Table**, and then click **With New Named Query**.  

3.  In the **Create Named Query** dialog box, click the **Add Table** icon (typically the last icon in the ribbon).  

4.  In the **Add Table** dialog box, click the **Views** tab, select **V_GS_OPERATING_SYSTEM** in the list, and then click **Add**.  

5.  Click **Close** to close the **Add Table** dialog box.  

6.  In the **Create Named Query** dialog box, specify the following information:  

    -   **Name:** Specify the name for the query. For this example, type **Advanced_Model**.  

    -   **Description:** Specify a description for the query. For this example, type **Example Reporting Services report model**.  

7.  In the **v_R_System** window, select the following items in the list of objects to display in the report model:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  In the **v_GS_OPERATING_SYSTEM** box, select the following items in the list of objects to display in the report model:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. To present the objects in these views as one list to the report author, you must specify a relationship between the two tables or views by using a join. You can join the two views by using the object **ResourceID**, which appears in both views.  

10. In the **v_R_System** window, click and hold the **ResourceID** object and drag it to the **ResourceID** object in the **v_GS_OPERATING_SYSTEM** window.  

11. Click **OK.**  

12. The **Advanced_Model** window replaces the **v_R_System** window and contains all of the necessary objects required for the report model from the **v_R_System** and the **v_GS_OPERATING_SYSTEM** views. You can now delete the **v_GS_OPERATING_SYSTEM** window from the Data Source View Designer. Right-click the title bar of the **v_GS_OPERATING_SYSTEM** window to select **Delete Table from DSV**. In the **Delete Objects** dialog box, click **OK** to confirm the deletion.  

13. Click **File**, and then click **Save All**.  

#### To create the report model  

1.  In **Solution Explorer**, right-click **Report Models** to select **Add New Report Model**.  

2.  On the **Welcome to the Report Model Wizard** page, click **Next**.  

3.  On the **Select Data Source View** page, select the data source view in the **Available data source views** list, and then click **Next**. For this example, select **Simple_Model.dsv**.  

4.  On the **Select report model generation rules** page, do not change the default values, and click **Next**.  

5.  On the **Collect Model Statistics** page, verify that **Update model statistics before generating** is selected, and then click **Next**.  

6.  On the **Completing the Wizard** page, specify a name for the report model. For this example, verify that **Advanced_Model** is displayed.  

7.  To complete the wizard and create the report model, click **Run**.  

8.  To exit the wizard, click **Finish**.  

9. The report model is shown in the Design window.  

#### To modify object names in the report model  

1.  In **Solution Explorer**, right-click a report model to select **View Designer**. For this example, select **Advanced_Model.smdl**.  

2.  In the report model Design view, right-click any object name to select **Rename**.  

3.  Type a new name for the selected object, and then press Enter. For example, you could rename the object **CSD_Version_0** to read **Windows Service Pack Version**.  

4.  When you have finished renaming objects, click **File**, and then click **Save All**.  

#### To publish the report model for use in SQL Server Reporting Services  

1.  In **Solution Explorer**, right-click **Advanced_Model.smdl** to select **Deploy**.  

2.  Examine the deployment status at the lower left corner of the **SQL Server Business Intelligence Development Studio** window. When the deployment has finished, **Deploy Succeeded** is displayed. If the deployment fails, the reason for the failure is displayed in the **Output** window. The new report model is now available on your SQL Server Reporting Services website.  

3.  Click **File**, click **Save All**, and then close **SQL Server Business Intelligence Development Studio**.  

#### To deploy the custom report model to Configuration Manager  

1. Locate the folder in which you created the report model project. For example, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;Project Name\>.*  

2. Copy the following files from the report model project folder to a temporary folder on your computer:  

   -   *&lt;Model Name\>* **.dsv**  

   -   *&lt;Model Name\>* **.smdl**  

3. Open the preceding files by using a text editor, such as Notepad.  

4. In the file *&lt;Model Name\>***.dsv**, locate the first line of the file, which reads as follows:  

    **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

    Edit this line to read as follows:  

    **&lt;DataSourceView xmlns="<http://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView"\>**  

5. Copy the entire contents of the file to the Windows Clipboard.  

6. Close the file *&lt;Model Name\>***.dsv**.  

7. In the file *&lt;Model Name\>***.smdl**, locate the last three lines of the file, which appear as follows:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Paste the contents of the file *&lt;Model Name\>***.dsv** directly before the last line of the file (**&lt;SemanticModel\>**).  

9. Save and close the file *&lt;Model Name\>***.smdl**.  

10. Copy the file *&lt;Model Name\>***.smdl** to the folder *%programfiles%*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other on the Configuration Manager site server.  

    > [!IMPORTANT]  
    >  After copying the report model file to the Configuration Manager site server, you must exit and restart the Configuration Manager console before you can use the report model in the **Create Report Wizard**.  
