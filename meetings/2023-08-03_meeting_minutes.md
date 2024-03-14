# CDSC WG1 (Customer Data) Meeting 2023-08-03

## Agenda
* Welcome
* Work on CDSC-WG1-03 (Customer Data) scopes:
    * Work on draft list of scopes and authorization_details fields for initial spec
    * Issue #24 - https://github.com/carbon-data-specification/Customer-Data/issues/24
    * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Bailey Kane (UtilityAPI)
* Zachary Snier (DoD CDAO)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)


## Minutes
* Welcome and attendance
* (Daniel) Overview of current draft list of customer data scopes
    * Data fields (account details, service details, program details, bills, usage, aggregates)
        * `account_details` - access to metadata about a customer's current utility accounts (also commonly called "Contract Accounts", "Customer Accounts", "Billing Accounts", etc.)
            * used for overall account status/management (current account balance, etc.)
        * `service_details` - access to metadata about a customer's current utility services (electric, gas, water, etc.) (also commonly called "Service Agreements", "Agreements", "Contracts", etc.). NOT physical things, but business agreements to deliver/provide commodity or service to customer.
            * used for individual service project feasibility and monitoring
            * (Eloi) in liberalized markets, a service has both distribution utility and retailer, so should this be two scopes (one for distribution service, one for retail service)?
                * One option, have two scopes (`delivery_details`, `supply_details`).
                    * Pros:
                            * allows Energinet to only offer `delivery_details`, so clients know they won't be getting supplier details
                    * Cons:
                        * For utilities that can provide both, they are different endpoints that clients have to link up with each other
                    * Example:
```
# on client metadata
{
    "cds_authorization_details": [
        {
            "type": "delivery_details",
        },
        { # not included in Energinet
            "type": "supply_details",
        },
    ]
}

# on vertically intergrated utility
GET /delivery_details
{
    "delivery_details": [
        {
            "id": "1234",
            "started": "2023-01-01T00:00:00Z",
            "modified": "2023-01-01T00:00:00Z",
            "verified": "2023-01-30T00:00:00Z",
            "commodity": "electric",
            "delivery_contract_id": "aaaaaabbbbbbb",
            "service_address": "123 Main St",
            "meter_numbers": [...],

            # (Eloi) should we include grid mix in delivery details?
            "region": "33333333", # allows lookup of gen mix based on location
            "pnode": "aaaaa-1",
        }
    ],
}
GET /supply_details
{
    "supply_details": [
        {
            "id": "2345",
            "started": "2023-01-01T00:00:00Z",
            "modified": "2023-01-01T00:00:00Z",
            "verified": "2023-01-30T00:00:00Z",
            "delivery_id": "1234",
            "supplier": "ABC Supply Co",
            "supplier_contract_id": "848484848484",
            "tariff_name": "E-1 Residential",
            "tariff_code": "E1R", #--> (Daniel) map to power system field for carbon/generation mix for that tariff_code?
                                  # (Hallie) maybe also include actual generation mix? maybe as different API?
                                  # (Zachary) need to look at generation mix on hourly basis by 2030, and shorter time periods thereafter
                                  # (Daniel) is tariff the lookup for gen mix? or is contract id?
        }
    ],
}

# on Energinet
GET /delivery_details
{
    "delivery_details": [
        {
            "id": "1234",
            "commodity": "electric",
            "service_contract_id": "aaaaaabbbbbbb",
            "meter_numbers": [...],
        }
    ],
}
```
                * Another option: have both included in same scope (`service_details`), but somehow communicate to client that utility can only provide partial data fields
                    * Pros:
                        * allows Energinet to only offer `delivery_details`, so clients know they won't be getting supplier details
                    * Cons:
                        * For utilities that can provide both, they are different endpoints that clients have to link up with each other
                    * Example:
```
# on client metadata
{
    "cds_authorization_details": [
        {
            "type": "service_details",
            "fields_included": [
                "commodity",
                "distribution_details",
                "supply_details", # not included for Energinet
            ],
        }
    ]
}

# on vertically integrated utility
GET /service_details
{
    "service_details": [
        {
            "id": "1234",
            "commodity": "electric",
            "distribution_details": {
                "service_contract_id": "aaaaaabbbbbbb",
                "meter_numbers": [...],
            },
            "supply_details": {
                "supplier": "ABC Supply Co",
                "service_contract_id": "848484848484",
                "tariff": "E-1 Residential",
            },
        }
    ]
}
# on Energinet (Denmark distribution)
GET /service_details
{
    "service_details": [
        {
            "id": "1234",
            "commodity": "electric",
            "distribution_details": {
                "service_contract_id": "aaaaaabbbbbbb",
                "meter_numbers": [...],
            },
        }
    ]
}
```
                * Preference: (Eloi, Hallie), have split scopes for distribution and supply
                    * Unclear what the two scopes should be called
                * "Supply" naming:
                    * (Eloi) "Retailer", "Retail Details", "Load Serving Entity (LSE)" (CA), "Generation"
                        * "Supply" can be misunderstood as DSO supplying the electricity
                        * `service_retail_details` and `service_distribution
                * "Delivery" naming:
                    * (Daniel) "Distribution", "Distribution", "Delivery"





    * Authorization UX customization (pre-filling usernames, pre-selecting authentication paths, etc.)
    * Account/service selection (pre-selecting which services or accounts are requested to be shared)
    * Duration (time periods for requested data fields)
    * Client credentials/admin management related (non-customer facing oauth)
        * Should NOT be part of CDSC-WG1-03??? Should these be in CDSC-WG1-02?
            * `client_admin` - scope to allow access token to view and modify client registration (included in CDSC-WG1-02)
            * `cds_server_metadata` - scope to allow access token to view just client-specific authenticated CDS Server Metadata included in the client registration
                * (Daniel) Is this needed? Is there need to allow access tokens that can just see the private metadata endpoint, but not the full client registration? Current assumption is no, so this scope isn't needed and can be cut.


## Closing Discussion
* Consensus to commit this to repo? Yes
