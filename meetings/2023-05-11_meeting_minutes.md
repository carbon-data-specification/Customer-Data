# CDSC WG1 (Customer Data) Meeting 2023-05-11

## Agenda
* Welcome
* Call for consensus of Design Principles:
    * Issue #18 - https://github.com/carbon-data-specification/Customer-Data/issues/18
    * Pull Request #22 - https://github.com/carbon-data-specification/Customer-Data/pull/22
    * Maintainer's preview - https://daniel-utilityapi.github.io/Customer-Data/specs/design-principles
* Continue review and feedback on Server Metadata (CDSC-WG1-01) draft:
    * Issue #15 - https://github.com/carbon-data-specification/Customer-Data/issues/15
    * Pull Request #23 - https://github.com/carbon-data-specification/Customer-Data/pull/23
    * Maintainer's preview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-01/
* Discuss client registration (CDSC-WG1-02) specification outline:
    * Issue #16 - https://github.com/carbon-data-specification/Customer-Data/issues/16
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)

## Minutes
* Intros
* Went through comments on Design Principles
    * Daniel - do we need to have a separate section just for backwards compatiblity
    * Hallie and Eloi - fine being included in extensibility
    * Hallie - rename to "Build in flexibility"
    * Daniel - made changes to pull request
* Call for consensus on merging Design Principles
    * Daniel - yes
    * Hallie - yes
    * Eloi - yes
    * Daniel - merging!
* Server Metadata
    * Eloi - elaborated on comments (https://github.com/carbon-data-specification/Customer-Data/pull/23#issuecomment-1506672798)
        * Can include granular access details?
        * Daniel - data access granularity may be registration specific
        * Daniel - Two options:
            * Include in client oauth scopes_supported?
            * Include in CDS server metadata capabilities
        * Eloi and Daniel - agree that need to provide "what can I get?" before registering
        * Daniel - Eloi raises good point on providing costs alongside capabilities
* Discussion on talk at LFEnergy summit

## Closing Discussion
* Consensus to commit this to repo? Yes
