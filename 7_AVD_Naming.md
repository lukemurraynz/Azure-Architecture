Internal

Naming Convention: - Resource Group - Resource Type - Environment - #

* rg-avd-prod-01 This would contain the host pool, workspace, app groups, virtual machines
* rg-networking-prod-01 This would contain all networking components (vnet, vnet gateway etc.)

* Host pool names: hp-aue-dev-001 (host pool + region + environment + number)
* Resource group: rg-avd-aue-001 (resource group + service + region + number)

* VM Name prefix: aue-avd-dev (region + service + enviroment)

External

Different clients are under different management groups, or subscriptions where possible.
