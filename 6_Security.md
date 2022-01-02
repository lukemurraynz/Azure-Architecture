## Security

### Azure PaaS to on-premises connectivity

Azure Private Endpoint will be configured for PaaS resources which only need to
be accessed on an internal network.

Azure Private Link enables you to access Azure PaaS Services (for example, Azure
Storage and SQL Database) and Azure hosted customer-owned/partner services over
a [private
endpoint](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)
in your virtual network. Traffic between your virtual network and the service
travels the Microsoft backbone network. Exposing your service to the public
internet is no longer necessary.

## RBAC

Role Based Access Control will be used across Azure resources and resource
groups.

Each Azure Resource Group will have an Azure Active Directory group created for
it with Contributor access. This allows any user a member of the group to only
have access to the Resource Group resources only.

Users are to be added to groups ONLY – not directly to the resources or resource
groups, so simplify management and increase visibility.

### Microsoft Defender for Cloud

Microsoft Defender for Cloud has two main goals:

-   to help you understand your current security situation

-   to help you efficiently and effectively improve your security

The central feature in Defender for Cloud that enables you to achieve those
goals is secure score. Defender for Cloud continually assesses your resources,
subscriptions, and organization for security issues. It then aggregates all the
findings into a single score so that you can tell, at a glance, your current
security situation: the higher the score, the lower the identified risk level.

Defender for Cloud and Security contacts will be enabled on all subscriptions,
Basic is Free.
