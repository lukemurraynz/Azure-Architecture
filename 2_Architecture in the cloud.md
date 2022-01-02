### **Architecture in the cloud**

Solution architecture is concerned with the planning, design, implementation,
and ongoing improvement of a technology system. The architecture of a system
must balance and align the business requirements with the technical capabilities
that are needed to execute those requirements. The finished architecture is a
balance of risk, cost, and capability throughout the system and its components.

Running a solution in the cloud does not reduce the need for requirements to be
clear. In fact, the flexibility and power provided by the cloud means that it is
even more important to have clear requirements from business stakeholders;
otherwise, you could end up solving for problems that don't exist, missing an
important design decision, or going beyond the available budget by adding
unnecessary resiliency.

**Non-functional requirements (NFRs)**

Below is a short-list of NFRs (not exhaustive) that may be provided by the
business to help inform the design of a solution.

[**Reliability
requirements**](https://docs.microsoft.com/en-gb/azure/architecture/framework/resiliency/overview#define-requirements)

-   Service level agreement (SLA)

-   Uptime objective

-   Recovery time objective (RTO)

-   Recovery point objective (RPO)

[**Security
requirements**](https://docs.microsoft.com/en-gb/azure/architecture/framework/security/governance)

-   Geographical location

-   Compliance and legislation

-   Identity and access management

-   Privacy

-   Public or private endpoints (or both)

-   OWASP

-   Hybrid connectivity

-   DDOS

**Performance requirements**

-   Peak throughput, e.g., Requests per minute (RPM), active users

-   Business plan for growth

-   UX metrics (e.g., Page load time)

-   Asynchronous vs Synchronous operations

-   Workload profile (predictable, unpredictable, peak time of day)

-   Data estate size and growth rate

-   Time-to-live (TTL) of reports and views (real-time vs eventual consistency)

**Operational requirements**

-   Prod and non-prod environments (Dev/Test, QA, Pre-prod, Prod)

-   Release frequency (hours / days / months)

-   Time to onboard (new customer)

**Cost optimization**

-   Cost per user

-   Target hosting costs as percentage of revenue

-   Pricing model

-   Tenancy model

**Azure SLAs**

-   Familiarize yourself with [Azure service-level
    agreements](https://azure.microsoft.com/en-au/support/legal/sla/)

-   An Azure Service-level Agreement (SLA) can also be read as a minimum
    service-level objective (SLO).

-   An SLA is a financial guarantee, not an absolute guarantee

-   Read the SLA details carefully, particularly the definition of "downtime"
    for each service, which give important hints about failure modes

For example, in the [SLA for Azure SQL
Database](https://azure.microsoft.com/en-au/support/legal/sla/sql-database/v1_4/),
"downtime" is defined as:

"The total accumulated Deployment Minutes across all Databases in a given
Microsoft Azure subscription during which the Database is unavailable. A minute
is considered unavailable for a given Database if all continuous attempts by
Customer to establish a connection to the Database within the minute fail."

The Azure SQL Database team expect almost all outages to be transient (brief and
non-recurring). Therefore, the retry pattern should be used to continuously
retry for up to a minute. This is typical in cloud services; retry has been the
default behaviour in ADO.NET since .NET Framework 4.6.1.
