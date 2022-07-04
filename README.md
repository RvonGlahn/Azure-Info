# Azure Topics

## Azure DevOps CI/CD Pipelines (x)

### Pipelines
- get triggert by git events from GitHub and Azure Repos
- use yaml files
  - tasks for special use cases (terraform, python, bash)
  - modularize with templates
  - store artifacts for later use in other stag
- use Library or key Vault to store secrets
  - store in ENV
- local [variables](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch) for info

### Artifacts
- code pakete hosten
  - Pakettypen wie NuGet, npm, Python, Maven und Universelle Pakete
- easy to integrate in DevOps Pipelines

### [Test Plans ](https://docs.microsoft.com/de-de/azure/devops/test/overview)
Testpläne und Testfälle können mit Build- oder Releasepipelinen verknüpft werden
- Tests
  - planned manual testing
  - user acceptance testing
  - exploratory testing
  - feedback from stakeholders
- Dashboards

### Git Integration mit Azure DevOps (x)
- Sign into Azure DevOps using your GitHub credentials
- Connect Azure [Boards](https://docs.microsoft.com/en-us/azure/devops/cross-service/github-integration?view=azure-devops#azure-boards-and-github-integration) project to GitHub repos


## [Azure WebApps](https://docs.microsoft.com/de-de/azure/app-service/overview) (mit C#/.NET)
- Sicherheit, Lastenausgleich, automatische Skalierung und automatisierte Verwaltung
- Vorteile ihrer DevOps-Funktionen nutzen, z. B. Continuous Deployment über Azure DevOps, GitHub, Docker Hub und andere Quellen, Paketverwaltung, Stagingumgebung, benutzerdefinierte Domäne und TLS-/SSL-Zertifikate
- Anwendungsvorlagen

### [Service Plan](https://docs.microsoft.com/de-de/azure/app-service/overview-hosting-plans)
- Mit einem App Service-Plan wird ein Satz mit Computeressourcen für eine auszuführende Web-App definiert
-  Sie können einem vorhandenen Plan weiterhin Apps hinzufügen, solange der Plan über genügend Ressourcen zum Verarbeiten der Last verfügt -> aber nicht immer sinnvoll
- Für jeden App Service-Plan wird Folgendes definiert:
   -  Betriebssystem (Windows, Linux)
   -  Region („USA, Westen“, „USA, Osten“ usw.)
   -  Anzahl von VM-Instanzen
   -  Größe von VM-Instanzen (Klein, Mittel, Groß)
   -  Tarif (Free, Shared, Basic, Standard, Premium, PremiumV2, PremiumV3, Isolated, IsolatedV2)

### [Basics .NET](https://docs.microsoft.com/de-de/dotnet/csharp/tour-of-csharp/)
- [.NET](https://docs.microsoft.com/de-de/dotnet/core/introduction) is similar to JVM and Java 
- [Example](https://docs.microsoft.com/de-de/azure/app-service/quickstart-dotnetcore?tabs=net60&pivots=development-environment-vs)


## AAD Identities (Service Principals, Managed Service Identities, Role Assignments)
Cloud-based identity and access management service
- https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-whatis#terminology
Security Principals: 
- A security principal is an object that represents a user, group, service, or application that's requesting access to Azure resources.
- Azure assigns a unique object ID to every security principal
- https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/security-principals
Best Practices:
- https://docs.microsoft.com/en-us/azure/security/fundamentals/identity-management-best-practices

### Service Principals
The application object is the global representation of your application for use across all tenants, and the service principal is the local representation for use in a specific tenant.

 - identity created for use with applications, hosted services, and automated tools to access Azure resources. 
 - This access is restricted by the roles assigned to the service principal
 - three types of [service principals](https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals):
   - **Application**: In this case, a service principal is a concrete instance created from the application object and inherits certain properties from that application object.
   - **Managed Identity**: Managed identities provide an identity for applications to use when connecting to resources that support Azure AD authentication
   - **Legacy**
- [Example](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal) 


### [Managed Identities](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)
Managed identities eliminate the need for developers to manage credentials.
Authorize the managed identity to have access to the "target" service.
Feature is supported by: [List](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/managed-identities-status)

- use managed identities to authenticate to any resource that supports Azure AD authentication
- System-assigned
  - identity is tied to the lifecycle of that service instance. -> can´t be shared
  - when the resource is deleted, Azure automatically deletes the identity for you
- User-assigned
  - Created as a stand-alone Azure resource. -> can be shared
  - Independent life cycle and must be explicitly deleted.

### RBAC and Role Assignments
 RBAC data is global to ensure that customers can timely access resources regardless from where they are accessing.

[*Role assignment*](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview#role-assignments)
- consists of three elements: security principal, role definition, and scope.
- process of attaching a role definition to a user, group, service principal, or managed identity at a particular scope for the purpose of granting access
- Role assignments are transitive for groups 
- Deny assignments take precedence over role assignments
- [Example](https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-steps) and [Best Practices](https://docs.microsoft.com/en-us/azure/role-based-access-control/best-practices) 

[*Roles*](https://docs.microsoft.com/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles)
- Owner - Has full access to all resources including the right to delegate access to others.
- Contributor - Can create and manage all types of Azure resources but can't grant access to others.
- Reader - Can view existing Azure resources.
- User Access Administrator - Lets you manage user access to Azure resources.
- [Built in Roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles) and [Custom Roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles)

*Role Definition* 
- collection of permissions
- lists the actions that can be performed, such as read, write, and delete

*Security Principal*
- is an object that represents a user, group, service principal, or managed identity that is requesting access to Azure resources

[*Scope*](https://docs.microsoft.com/en-us/azure/role-based-access-control/scope-overview#scope-examples)
- set of resources that the access applies to
- you can specify a scope at four levels: management group, subscription, resource group, or resource
- Scopes are structured in a parent-child relationship -> Lower levels inherit role permissions from higher levels
- simple to determine the scope for a management group, subscription, or resource group. You just need to know the name and the subscription ID. Only Ressources are more tricky


## KeyVault Access Policies
[Key Vault](https://docs.microsoft.com/de-de/azure/key-vault/general/overview) is used to store and manage secrets, keys and certificates
- applications can securely access the information they need by using URIs.
- Authorization may be done via Azure role-based access control (Azure RBAC) or Key Vault access policy
- [key vault access policy](https://docs.microsoft.com/en-us/azure/key-vault/general/security-features) can only be used when attempting to access data stored in a vault -> data plane
  - The data plane allows you to work with the data stored in a key vault. You can add, delete, and modify keys, secrets, and certificates.
- https://docs.microsoft.com/de-de/azure/key-vault/general/overview
- [Example](https://docs.microsoft.com/en-us/azure/key-vault/general/assign-access-policy?tabs=azure-portal)


## Azure SQL Database
- https://docs.microsoft.com/en-us/azure/azure-sql/database/purchasing-models?view=azuresql

### [vCore](https://docs.microsoft.com/en-us/azure/azure-sql/database/service-tiers-sql-database-vcore?view=azuresql)
- provides a choice between a provisioned compute tier and a https://docs.microsoft.com/en-us/azure/azure-sql/database/serverless-tier-overview?view=azuresql
 compute tier
  - The serverless compute tier automatically pauses databases during inactive periods when only storage is billed and automatically resumes databases when activity returns
  - Different types of storage are billed differently same for compute
- A virtual core (vCore) represents a logical CPU and offers you the option to choose between generations of hardware and the physical characteristics of the hardware
- Tiers: General Purpose,	Business Critical,	Hyperscale

### [DTU - database transaction unit](https://docs.microsoft.com/en-us/azure/azure-sql/database/service-tiers-dtu?view=azuresql)
- provides bundled compute and storage packages balanced for common workloads.
- best for customers who want simple, preconfigured resource options
- billed by the number of DTUs you allocate to your database
- Tiers: Basic,	Standard,	Premium

## Azure Data Factory (...)
- Coordinate Data Ingestion
- https://docs.microsoft.com/de-de/azure/data-factory/introduction
  

## Databricks (...)

### Keyvault-backed Secret Scopes
A secret scope is collection of secrets identified by a name
- To reference secrets stored in an Azure Key Vault, you can create a secret scope backed by Azure Key Vault
- [Example](https://docs.microsoft.com/de-de/azure/databricks/security/secrets/secret-scopes)
- 
### How to connect from Databricks notebooks to Azure SQL Database using a Service Principal
- https://docs.microsoft.com/en-us/azure/databricks/tutorials/run-jobs-with-service-principals
