# CDSC WG1 (Customer Data) Meeting 2022-06-23

## Agenda
* Welcome
* Review open pull requests:
    * Pull Request #13 - Add granular certification data to list of needs in use cases (https://github.com/carbon-data-specification/Customer-Data/pull/13)
* Review other open issues:
    * Issue #7 - Review preliminary list of specifications to develop (https://github.com/carbon-data-specification/Customer-Data/issues/7)
    * Issue #15 - Discuss server discovery spec draft overview ("Server Metadata") (https://github.com/carbon-data-specification/Customer-Data/issues/15)
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Stephen Suffian (WattCarbon)

## Minutes
* Hallie: maybe granular certification data (#13) should be in WG2 (power systems working group)?
* Stephen: commented on similar topic in #15
    * what a customer's carbon is on the customer side of things
    * maybe combo of market/location is in WG2 and customer is in WG1
* Hallie: maybe it is a split use case
    * in the power systems group, if going to directly to power system operator, will need the consent of the contracted developer and contracted customer
* Stephen: this situation sounds very customer-y
    * on the grid side, it would be more nodal focused
* Daniel:
    * so the "meter" on the producer's side also needs consent from the producer
    * so it's getting data from "edge meters" that are more in the customer working group realm
    * but for internal grid meters (e.g. nodes) that's more in the power systems group to get the data for
* Hallie: for CCAs
    * where you are in a CCA, where procurment is more group-to-group vs. direct access where it's one-to-one
    * also, multi-stakeholder PPAs? contract just says what proportion of it each stakeholder gets
* Daniel: so summary of discussion
    * for public tariff/node level mix data, that data formats should be in power systems working group since "grid-level" data
    * for individual direct access or "sleeved" one-off contracts, that is "customer-specific" so needs consent from customer, and data format for that production data should still also be in power systems working group
    * however, the _consent_ part of getting a production dataset (e.g. if needing producer consent or customer/offtaker consent), that process should be defined in the customer data working group
* Hallie: so for #13, it focuses on _how_ to get the certificate data, not the data formats themselves, so this is in-line with the previous discussion

* Daniel: changing topics
    * Do pull requests need final approval for merging at meetings? or can they be merged via mailing list "last call" announcment?
* Stephen: 2nd option seems fine
* Hallie: 2nd option done with strategy committee
* Daniel: changing dates on #13 to 6/27 for last call and 7/1 for merge

* Daniel: summarized #7, will focus on #15 next time (will have actual spec and not just overview)

## Closing Discussion
* Consensus to commit this to repo? Yes
