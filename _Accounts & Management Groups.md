## Accounts & Management Groups

### Accounts

Azure subscriptions are bound to: Accounts.

These accounts will be subscription and Billing owners and need to have MFA
(Multi-factor authentication) enabled.

### Subscriptions

The Azure account is a global unique entity that gets you access to Azure
services and your Azure subscriptions. You can create multiple subscriptions in
your Azure account to create separation e.g., for billing or management
purposes. In your subscription(s) you can manage resources in resources groups.
Azure subscription can have a trust relationship with an Azure Active Directory
(Azure AD) instance.

![Management Groups & Subscriptions](/images/ManagementGroupsandSubscriptions.png "Management Groups & Subscriptions")

Depending on the size of the environment, you may have one or many
subscriptions, you may have a Subscription to separate resources for:

-   Production

-   Development

-   Sandbox (testing)

| Environment | Azure Region   | Azure Service | Example Name                  |
|-------------|----------------|---------------|-------------------------------|
| Production  | Australia East | Subscription  | company-application1-sub-prod |

Depending on the size of the environment, it is best to start with one
subscription for Production resources (most resources can be moved across
subscriptions) and add additional subscriptions where/as needed.

Each subscription is also managed by resource quotas, for example if you were
setting up a reasonably large Azure Virtual Desktop farm, you may have the
session hosts in another subscription to prevent any issues creating Virtual
Machines on another subscription.

### Resource Groups

A resource group is a container that holds related resources for an Azure
solution.

The resource group can include all the resources for the solution, or only those
resources that you want to manage as a group. You decide how you want to
allocate resources to resource groups based on what makes the most sense for
your organization.

Generally, add resources that share the same lifecycle to the same resource
group so you can easily deploy, update, and delete them as a group.

A Resource Group should be created for each application separately, it is also
recommended to separate Production and Development resources into separate
resource groups.

Resource Groups also allow you to enable Locks, to prevent anyone from deleting
or modifying the resources in, this is extremely useful when working with
infrastructure resources, such as Networks.

| Environment | Application Name | Azure Region   | Azure Service  | Example Name                      |
|-------------|------------------|----------------|----------------|-----------------------------------|
| Production  | application1     | Australia East | Resource Group | company-application1-rg-au-e-prod |

### Management Groups

Azure management groups provide a level of scope above subscriptions.

You organize subscriptions into containers called "management groups" and apply
your governance conditions to the management groups. All subscriptions within a
management group automatically inherit the conditions applied to the management
group. You can build a flexible structure of management groups and subscriptions
to organize your resources into a hierarchy for unified policy and access
management.

It is recommended to use management groups to deploy:

-   Access rights

-   Policies

![Management Groups](/images/ManagementGroup.png "Management Groups")

### Azure Policies

Resource policies will be used to assign resource tags to resources, to control
costs by limiting the types of resources that can be created and to restrict
resources to preferred Azure locations. Azure policy is a default allow and
explicit deny system.

Azure Policies can be deployed to Subscriptions/Resource Groups and Management
Groups, example policies to deploy as a base could be:

**Built-in policies**

-   **Allowed locations**

Resources should be created only in the Australian regions below. Attempts to
create resources in other regions will be denied and audited.

-   Australia East

-   Australia Southeast

-   **Allowed virtual machine SKUs**

-   Production Environments - Virtual Machines should be configured to use
    managed disks

-   Non-Production Environments - Virtual Machines should be configured to use
    managed disks

-   Virtual Machines must be provisioned based on the least number of resources
    required.

-   **Allowed storage account SKUs**

-   Production Environments – Storage accounts created for production
    subscriptions should use one of the following storage account SKU's:

-   Standard_GRS. Geo-redundant storage

-   Standard_RAGRS. Read access geo-redundant storage

-   Non-Production Environments – Storage accounts created for non-production
    subscriptions should use one of the following storage account SKU's:

-   Standard_LRS. Locally redundant storage

-   Standard_ZRS. Zone-redundant storage

-   Premium_LRS. Premium locally redundant storage

-   **CIS Level 1 Benchmark**

-   CIS Level 1 Auditing policies will be deployed across all Clients against
    the Client Management Group.

-   **Apply tag and default value**

Tags should be applied to all Azure resources using policies. When a resource
tag is not provided, the resource creation should be denied and audited (changed
from audit and create to deny)

Tags should be applied using policy sets that can be reused.

-   **Require storage account encryption**

Encryption should be enabled for all storage accounts. Since only newly created
data will be encrypted, all existing data must be encrypted by moving between
storage accounts that are configured for encryption or between containers after
enabling encryption on the relevant storage account.

-   **New Zealand Information Security Manual**

This initiative includes policies that address a subset of New Zealand
Information Security Manual controls.

### Resource Locks

Resource Locks must be used to protect production resources (such as Virtual
Networks, or Domain Controllers) from being accidently deleted.

-   Who can create or delete locks in your organization?

To create or delete management locks, you must have access to
Microsoft.Authorization/\* or Microsoft.Authorization/locks/\* actions. Of the
built-in roles, only Owner and User Access Administrator are granted those
actions. Access should be controlled using RBAC.

-   **CanNotDelete** means authorized users can still read and modify a
    resource, but they can't delete the Resource.

-   **ReadOnly** means authorized users can read a resource, but they can't
    delete or update the Resource. Applying this lock is similar to restricting
    all authorized users to the permissions granted by the **Reader** role.

    **Exceptions**

-   For example, placing a ReadOnly lock on a storage account prevents all users
    from listing the keys. The list keys operation is handled through a POST
    request because the returned keys are available for write operations. For
    another example, placing a ReadOnly lock on an App Service resource prevents
    Visual Studio Server Explorer from displaying files for the Resource because
    that interaction requires write access.
