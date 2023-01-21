# CDSC WG1 (Customer Data) Meeting 2022-08-25

## Agenda
* Welcome
* Merge open pull requests with consensus:
    * Pull Request #13 - Add granular certification data to list of needs in use cases (https://github.com/carbon-data-specification/Customer-Data/pull/13)
* Review other open issues:
    * Issue #15 - Discuss server discovery spec draft overview ("Server Metadata") (https://github.com/carbon-data-specification/Customer-Data/issues/15)
    * Issue #16 - Discuss client authorization goals ("Granting Access") (https://github.com/carbon-data-specification/Customer-Data/issues/16)
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Chris Foster (LO3 Energy)
* Deirdre Lord (Megawatt Hour)
* Eloi Fabrega Ferrer (FlexiDAO)
* Hallie Cramer (Google)
* Klaar De Schepper (Flux Tailor)
* Kris Donhowe (Google)
* Natalie Kozlowski (independent)
* Nick Burgess (JB&B)
* Stephen Suffian (WattCarbon)

## Minutes
* Review and merge Pull #13
    * Request any last comments from group
    * No additional comment given
    * Merged into main

* Review Issue #15 - Server Metadata spec
    * Overview page draft is written
    * Inspired by https://www.rfc-editor.org/rfc/rfc8414
    * Klaar: profiles concept is also in NIST Smart Grid Interoperability Framework
        * Fallon, Cheyney O, and David Wollman. n.d. "DRAFT NIST Framework and Roadmap for Smart Grid Interoperability DRAFT NIST Framework and Roadmap for Smart Grid Interoperability."
        * https://www.federalregister.gov/documents/2020/09/18/2020-20587/draft-nist-framework-and-roadmap-for-smart-grid-interoperability-standards-release-40.
    * `UtilityMetadata['id']`
        * Daniel: Not enforcable to be globally unique, since CDSC-WG1 isn't a governing body
        * Klaar: Possible to use EIA number?
            * Daniel: do suppliers have EIA numbers? Klaar: yes
        * Hallie: do tranmission operator have EIA numbers?
        * Daniel: is this US only? Klaar: yes
        * Daniel: Overall strategy when it comes to external "IDs" (like EIA number):
            * Prefer to have that as a separate field (e.g. `"eia_id": "123123123"`)
            * Help resolve conflicts?
            * Should not use globally unique IDs at all?
                * Tend to see this as creating more problems than it solves
        * Chris: if not governing body, where would id registration occur, what would prevent squatting
        * Daniel: will be requesting from specific domain, so would the domain be a better "id" than a self-assigned id?
        * Daniel: perhaps using something similar to html's canonical url (e.g. `<link rel="canonical" href="https://www.website.com/page/" />`)
        * Klaar: EIA has mergers and acquisitions list, so "alias" concept does exist in their structure as well
    * `UtilityMetadata['coverage']`
        * links to list of "coverage entries"
        * Klaar: this is awesome
        * Deirdre: do we need a different coverage type for transmission operators? Daniel: would probably just have an empty coverage_entries list
        * Daniel: overall strategy for this:
            * "lists" should always be paginated (i.e. have a "next" and "previous")
    * `UtilityMetadata['infrastructure_types|commodity_types']`
        * Klaar: EIA has similar identifiers
    * `UtilityMetadata['capabilities']`
        * Daniel: what the utility can do

## Closing Discussion
* Consensus to commit this to repo? Yes
