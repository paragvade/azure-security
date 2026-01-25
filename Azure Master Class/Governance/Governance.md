## Why Govern cloud?
- In on-prem set up, app team goes to operations team for spinning up resources they want. Operations team checks resources requested against organization's policy. If request meets criteria, resources are created. Else, sent back to App team
- In Cloud - App team has direct access to spin up resources. Hence, a mechanism to 'enforce' organization's policies is required = Governance
- Cloud works on 'shared responsibility' model and it applied to governance and compliance as well. Purview Portal helps track compliance status.

## Azure governance components
### Management Groups
- MGs can be used to organize subscriptions based on various criterial like business unit, geography, environment, etc and implement policies at MG level
- There's a fixed Root MG. Below this, there can be up tp 6 levels of MGs. 
- Max MGs per tenant = 10000
- Usually, entra permissions are separate from Azure permissions. But Global Admin in Entra can elevate his access and get something like User Access Administrator over all subscriptions. Imp break glass capability to fix things is something is locked down.
- **IMP Concept 'Relation between tenant and Entra ID'**: Tenant is an 'instance' of Entra ID, hence technically, it is called as Entra ID tenant (Old name- Azure AD tenant). When org requests ANY microsoft cloud service - Azure, M365, etc - Microsoft provisions a dedicated tenant. Entra ID is like a building and Tenant is . Every subscription has to be part of exactly one tenant. Tenant provides identity plane. Hence, using your security reader role, you can see all subscriptions in the tenant. 

### Subscriptions
- Limits - unlimited number of subscriptions in a tenant, 980 RGs per subscription, 50 tags per subscription


### Resource Groups
- Every azure resource lives in only one RG
- RGs cannot be nested - there cannot be a RG inside another RG
- Resources with common lifecycle (deployed and deleted together) can be grouped inside a RG. Better for having related resources together and can be deleted conveniently in one go.
- Granular access control is another purpose of RG. RBAC permissions can be applied at RG level. 
- Azure policies can also be applied on a RG (Policies can be applied on single resource as well)
- Region needs to be selected while creating a RG. But just metadata lives in this region. Resources from different regions can be in same RG.
- Once created, RG can not be renamed. If need to rename, create a new RG and move resources to that RG


### Naming Standard
-  Should be able to read the name of the resource and know basic info about it like purpose, account, region, etc. Org must have a naming convention- applied uniformly across cloud and on-prem.

### Tags
- Org also must have tagging strategy. Useful for sophesticated filtering and reporting on resources.
- Microsoft suggests some minimum tags like- Workload name, Data classification(Green, Yellow, Red), Business criticality(Low, Med, High), Business Unit (LRL, MQ, etc), Environment, Azure region, Owner, etc. Not just keys but values of tags should also be standardized. Else, Environment: Prod, Production, prod = inconsistency.
- Can use Policy to enforce consistent tagging. Be carefuly of 'Deny' effect of such policy.
- Tags are not inherited by default. But can have azure policy like 'Inherit tags from RG/Sub if missing'

### Locks
- To protect against accidental deletion
- Types- Read-only (resource becomes immutable) and Delete (resource can be modified, but not deleted)
- Scope is inherited down the resources
- Applies to Control plane only (ARM), not data plane. E.g. Read-only lock on key-vault= cannot create a new secret (control plane action) but application retrieving secret key vault data plane API=allowed

### Quick note on ARM
- Everything in Azure is made of resources. Resources are defined in Resource providers. Resource has properties and actions. Knowing this is imp to understand Policies. Properties section of Resource is used in Policies (in 'field' section)
- E.g. While deploying Storage account using terraform, type=Microsoft.Storage/storageAccounts. ARM receives request --> routes to Microsoft.Storage provider. If there's policy that blocks storage accounts with HTTP, the policy 'field' check resource properties in the ARM request.


### RBAC
- Role is collection of permissions. Role is ***generally*** applied on a 'Group' and security principal (users, service principals) are added to group. Then scope of the role is decided while 'Assigning' the role = decides where permissions mentioned in the role can be performed.
- Role can be scoped at resource level also. But gets tricky to manage. Better- group resources logically in RGs and apply at RG scope. Or sub/MG.
- Generally, RBAC roles allow control plane action. But some roles also support data plane action - which required access keys earlier. Integrating data plane action with RBAC improves security(no shared keys to leak/rotate, granular permissions and auditable via Entra ID) E.g. Key Vault Secrets User, Storage Blob Data Reader
- If multiple roles assigned to user = gets sum of all permissions


Custom Role
- If no built in role for your use case
- Custom role contains- Actions NotActions
- DataActions NotDataActions
- 5000 custom roles per tenant

Not active, but Eligible assignment. Just enough permission + just in time


### ABAC
- RBAC has limitations when it comes to granular permissions. ABAC solves it. ABAC is attaching conditions to existing RBAC roles. This is very helpful when in scenarios like grant access to only particular data objects in a storage account.
- Not all RBAC roles support it, but list is growing.
- Conditions can be based on resource, user, etc. E.g. resource name, resource subnet, user name, time of accessing, etc 

### Azure Policy
- Conditions around attributes of a resource that are exposed as **'aliases'**
- On top of ARM. Nothing can escape = Portal. CLI, etc
- Can be Enforced/Audit (start with Audit to understand effect of policy)
- Policies grouped into **Initiatives** - easy to track compliance. Built in Initiatives for major compliance frameworks e.g. NIST, PCI, Reserve Bank of India. 
- Initiatives also make assignments easy. Don't have to assigne each policy separately.
- DINE effect- after something is created, check condition and do something
- Can exclude some resources/RGs from scope during assignment
 
### Deployment Stacks
- Blueprints are deprecated in favour of Deployment Stacks
- Resources with same lifecycle deployed together
- Can mark resources as Unmanaged - and they can be deleted/managed independently
- Can protect resources against deletion


### Azure Resource Graph
- Stores resource configs, relationships and changes in config. 
- Can be queries using KQL. Resources can be queries AT SCALE
- ARM is not queries directly - will take many API calls and iterating through many subscriptions. Azure Resource Graph is actually **continuously updated index of all resources**. It is **eventually consisten**t** i.e. changes in ARM are updated eventually (seconds to minutes), not in real time.
- Respects RBAC - can only see what you have permissions over
- Use cases
    - Find all storage accounts with public acccess enabled
    - Identify all VMs without endpoint protection installed
    - Track confic changes e.g. When particular NSG rule changes?

### Azure Advisor
- Provides recommentations in key areas. Should be checked weekly.
- Recommendations in categories- cost, securrity, reliability, operational excellence
- Can set up alerts based on new recommendations- e.g. If Azure Advisor recommendation in particular category e.g. Security with 'impact' level 'high' --? Action Group should send email
- Advisor score calculates how much of azure advisor recommentations are actioned 

