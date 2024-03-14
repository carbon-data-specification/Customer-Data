# CDSC WG1 (Customer Data) Meeting 2023-08-31

## Agenda
* Welcome
* Continue work on CDSC-WG1-03 (Customer Data) scopes
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Brett Marraccini (UtilityAPI)
* Eloi Ferrer (FlexiDAO)
* Greg Bytniewski (FlexiDAO)
* Jordan Hughes (Apple)
* Madhuban Kumar (Carbon Laces)
* Pierre Vogler-Finck (consultancy)
* Steven Mazliach (OhmConnect)
* Zachary Snier (DoD CDAO)

## Minutes
* Welcome and attendance
* Going over last meeting's discussion
    * discussion about scopes for Customer Data (csdc-wg1-03)
    * consensus seemed to be moving towards separate scopes for distribution details and retail/supply details
* Current list of Customer Data scopes:
    * `customer_distribution_details` - details about the physical delivery of the service
        * distribution utility (e.g. Oncor)
        * meter number
        * service point id
        * voltage
        * service type (e.g. electricity)
        * etc.
    * `customer_supply_details` - in the moment access? (e.g. what is it right now, or if ongoing access, what is it at that time when accessed in the future)
        * retailer name (e.g. Constellation Energy)
        * retailer tariff (e.g. E1-EV-TOU)
        * customer/account id
        * service contract id
        * history? (previous suppliers)
        * should be time period based or right-now query?
            * should maybe be separate scope?
    * `customer_supply_history` - logs of changes to supplier/tariffs
        * Already included in bill data?

    * `generation_mix` - time period
        * `generation_breakdown` - overall grid generation mix (should be in WG2, since not-customer-specific?)
        * `consumption_breakdown` - your specific tariff's generation mix
            * would be time series based, so would align with WG2 grid-level data
        * `residual_mix` - what remains when you remove all generation covered by EACs (energy attribution certrificates)  (should be in WG2, since not-customer-specific?)

    * `usage_data`
    * `bill_data`
    * `bill_statements`



* Structure of a authorization request
```
?client_id=aaaaaaaa
&authorization_details=[
    {
        "type": "supply_details",
        ...
    },
    {
        "type": "usage_data",
        "start": "-3y",
        "end": "+3y",
        "services": "all",
    },
    {
        "type": "generation_mix",
        "start": "-3y",
        "end": "now",
        "services": ["1111111-1", "222222-2"],
    },
]

When authorized, get access to:
GET /supply_details
GET /usage_data
GET /generation_mix
```


From Customer's point of view:
* Customer account with a utility/supplier
    * [contractual] One or more "Billing Accounts" (e.g. various store locations/buildings)
        * [contractual] One or more Service Contracts (e.g. electric, gas, water)
            * [physical] One or more Service Points (e.g. meter socket)
            * [physical] actual meters
                * usage for those meters
            * [contractual] generation mix for the services
        * [contractual] bills for those billing accounts and services



## Closing Discussion
* Consensus to commit this to repo? Yes
