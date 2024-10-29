<!-- This include is part of the Intune Data Warehouse documentation. -->

<a name='azure-ad-and-intune-credential-requirements'></a>

## Microsoft Entra ID and Intune credential requirements

Authentication and authorization are based on Microsoft Entra credentials and Intune role-based access control (RBAC). All global administrators and Intune service administrators for your tenant have access to the Data warehouse by default. Use Intune roles to provide access for more users by giving them access to the **Intune data warehouse** resource.

Requirements for accessing the Intune Data Warehouse (including the API) are:

- User must have a minimum of one of the following roles:
  - An Intune service administrator
  - User with role-based access to **Intune data warehouse** resource
  - User-less authentication using [application-only authentication](../developer/data-warehouse-app-only-auth.md) 

> [!IMPORTANT]
> To be assigned an Intune role and access the Intune Data Warehouse, the user must have an Intune license. For more information, see [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md) and [Microsoft Intune licensing](../fundamentals/licenses.md).
