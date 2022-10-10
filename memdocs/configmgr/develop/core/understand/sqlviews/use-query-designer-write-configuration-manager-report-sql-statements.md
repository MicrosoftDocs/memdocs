---
title: Using query designer to write report SQL statements
titleSuffix: Configuration Manager
description: Information about using query designer to write report SQL statements for Configuration Manager reports.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 624e2cb1-db83-4e68-b9c1-335f7b3832c7
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Using query designer to write report SQL statements for Configuration Manager reports

To help you to write SQL statements for Configuration Manager reports, you can use the query design tool found in SQL Server Management Studio. For some administrators, it is much easier to use Query Designer in Microsoft SQL Server to create the SQL statement for the Configuration Manager report. This tool has a variety of features that help in designing and testing queries. For some administrators, it is much easier to use Query Designer in Microsoft SQL Server to create the SQL statement for the Configuration Manager report. This tool has a variety of features that help in designing and testing queries.

## Using query designer to create report queries

Writing SQL statements in the Query Designer component of the Microsoft SQL Server�Management Studio provides a graphical interface for writing queries. You can create a new query or copy a query from an existing Configuration Manager report, paste the SQL statement into the **SQL** pane of the Query Designer, and easily add views, create joins, select columns to display, add criteria, sort data, and so on. Query Designer provides the following panes:

- **Diagram** pane: Provides the ability to join the views on specific columns and select the columns to display as part of the query results.
- **Criteria** pane: Provides the ability to create aliases for columns, configure the sort order for the query results, configure filters, and so on.
- **SQL** pane: Provides the ability to manipulate the SQL statement.
- **Results** pane: Provides the query results when the **Execute SQL** action is initiated.

## Query designer considerations

When using Query Designer, you should be aware of the following points so that your queries and reports work as expected.

## Report prompt query variables

Many predefined Configuration Manager reports have report prompts. These report prompts require the user to enter a value for a specified view column. The value is stored in a variable, and the variable is then used to filter the query result set. These variables will not work in Query Designer, so you must change the variable to a static value or the query will fail. The following example shows a query from a Configuration Manager report that contains a variable representing a specific collection ID and how this variable is modified so that Query Designer can be used:

**Query from a Configuration Manager report:**

```sql
    SELECT Name 
    FROM v_FullCollectionMembership 
    WHERE CollectionID = @collid 
```

**Change the variable to the desired static value:**

```sql
    SELECT Name 
    FROM v_FullCollectionMembership 
    WHERE CollectionID = 'SMS00001' 
```

After the query has been modified in Query Designer and is ready to be used in a Configuration Manager report, the query can be copied into Report Builder and modified so that the original report prompt variable replaces the static value entered above.

## Report links

If you change the column order by modifying the query in a predefined report and if the report has a link to another report that requires a column number, the link can pass data from the wrong column to the target report. To prevent this, verify that the correct column numbers are specified in the link.

## See also

[How to create a SQL statement by using query designer](how-to-create-sql-statement-using-query-designer.md)
