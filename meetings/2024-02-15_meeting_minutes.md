# CDSC WG1 (Customer Data) Meeting 2024-02-15

Recording: https://zoom.us/rec/share/9j2v6i3l4kCuWOLQC0FrNZkUV0QvHxHi54wyQxTZyT05pjSIzU7abLDKyoetMRo.G-l6vCHseohlmOOq

## Agenda
* Welcome
* Review progress on CDSC-WG1-02 (Client Registration) specification
    * Maintainer's Draft:
        * Overview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
        * Specification - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/
    * Possible topics:
        * Client Registration Request and Response
        * Overview of the various included APIs

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Grzegorz Bytniewski (FlexiDAO)
* Hallie Cramer (Google)
* Brett Marraccini (UtilityAPI)
* Michael Murray (Mission:Data)
* Jordan Hughes (Apple)
* Natalie Kozlowski (independent)
* Eloi Ferrer (FlexiDAO)
* Madhuban Kumar (CarbonLaces)

## Minutes
* Welcome and intros
* Brief overview of what was discussed last time
* Overview of how parent `response_types_supported` etc. is a union of all `cds_scope_descriptions` values.
* [Michael] how does initial scope of use disclosures work when business may want to change that in the future?
    * [Daniel] short answer, not allowed in this new spec
    * [Michael] what other things are rigid and require registration?
    * [Daniel] short answer, changes allowed via Client Settings API
    * [Michael] what about starting to impose "unlisted" requirements after registration?
    * [Daniel] short answer, can be managed via the Client Updates API
* Fees discussion
    * [Daniel] registration fields are tied to scopes, and `payment_required` has an amount, so if fees are different, current draft would have to have different `scope` for each type of fee, but will disclose fees before registration
    * [Eloi] makes sense
    * [Hallie] maybe have fees that can support tiers, also what about usage-based fees?
    * [Michael] volume based fees are also common, including fees that have a threshold
    * [Eloi] would be nice to have usage-based fees disclosed up front, but seems like it would be hard to implement
    * [Eloi] maybe having extra documentation on the utility side?
    * [Daniel] yeah, something like a boolean `tos_agreement` or `schedule_of_fees_agreement` with documentation links to the agreements, and Clients have to submit `true` when registering
    * [Michael] sounds great
* Avoiding collisions for extended fields by prefixing with `cds_*`.
* [Michael] How would bulk authorizations work?
    * [Daniel] In spec 03, would be in the Authorization Scopes list, and would be `client_credentials`-based and not `authorization_code`-based. But will likely need to add a authorization submission API to spec 03 to allow client_credentials-based grant submissions.
    * [Michael] can this be used related to "offline" or "out-of-band" authorizations?
    * [Daniel] grants can be listed using the Grants API, so maybe we can add a `grant_type` to that out-of-band grants can show up in that and Clients can know whether a grant can use `client_credentials` to access the data instead of the normal `authorization_code`


## Closing Discussion
* Consensus to commit this to repo? Yes
