# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-02-27

Recording: https://zoom.us/rec/share/rBqt1jkRaHXmXtkOY2_lHtN7nCPpUvBten31k365Wd31ot-lftF71cJ7lNiinGg.Orvnybg4dHobH0Lt

## Agenda
* Welcome
* Example updates for Client Registration spec
    * https://daniel-utilityapi.github.io/Connectivity/specs/cdsc-wg1-02/overview
* Discussion of Customer Data scopes and Authorization Details fields
    * Customer-authorized scopes (i.e. `grant_type=authorization_code`):
        * `cds_current_rate_plan`
        * `cds_current_accounts_basic`
        * `cds_current_accounts_detailed`
        * `cds_historical_bill_statements`
        * `cds_historical_bill_sections`
        * `cds_historical_usage`
    * Client-submitted scopes (i.e. `grant_type=client_credentials`):
        * `cds_account_lookup`
        * `cds_aggregation_lookup`
        * `cds_customerdata_request`

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Don Coffin (GBA)
* Soazig Kaam (Google)
* Jordan Hughes (Apple)

## Minutes
* Welcome
* Overview modifications to connectivity spec and examples since last time
* Updated list of Customer Data scopes
    * Customer-authorized scopes (i.e. `grant_type=authorization_code`):
        * `cds_current_rate_plan`
        * `cds_current_accounts_basic`
        * `cds_current_accounts_detailed`
        * `cds_historical_amount_due`
        * `cds_historical_bill_statements`
        * `cds_historical_bill_sections`
        * `cds_historical_usage`
        * `cds_ongoing_amount_due`
        * `cds_ongoing_bill_statements`
        * `cds_ongoing_bill_sections`
        * `cds_ongoing_usage`
        * `cds_aggregation_inclusion`
    * Client-submitted scopes (i.e. `grant_type=client_credentials`):
        * `cds_account_lookup`
        * `cds_aggregation_lookup`
        * `cds_aggregation_data`
        * `cds_customerdata_request`

## Closing Discussion
* Consensus to commit this to repo? Yes

