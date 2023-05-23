# CDSC WG1 (Customer Data) Meeting 2023-04-13

## Agenda
* Welcome
* Continue review of design principles:
    * Issue #18 - https://github.com/carbon-data-specification/Customer-Data/issues/18
    * Pull Request #22 - https://github.com/carbon-data-specification/Customer-Data/pull/22
    * Maintainer's preview - https://daniel-utilityapi.github.io/Customer-Data/specs/design-principles
* Review server metadata (CDSC-WG1-01) specification draft:
    * Issue #15 - https://github.com/carbon-data-specification/Customer-Data/issues/15
    * Pull Request #23 - https://github.com/carbon-data-specification/Customer-Data/pull/23
    * Maintainer's preview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-01/
* Discuss client registration (CDSC-WG1-02) specification ideas:
    * Issue #16 - https://github.com/carbon-data-specification/Customer-Data/issues/16
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Jordan Hughes (Apple)
* Madhuban Kumar (CarbonLaces)

## Minutes
* Introductions
* Reviewed comments on Pull #22
    * Daniel inclined to support another "Be Adaptable" principle, though hasn't reviewed in depth
    * Hallie agrees, though hasn't reviewed in depth
    * Jordan agrees, though hasn't reviewed in depth
    * Madhuban agrees, space is so dynamic
    * Daniel to incorporate Be Adaptive into the pull request, as well as fixing typos from other comments
* Review Pull #23
    * Daniel talked about .well-known urls
    * Daniel went through changes from last edit
        * removed "id", replaced with canonical "cds_metadata_url"
        * added "support"
        * added "created" and "updated"
        * added "related_metadata", so can point to other metadata for servers
        * Moved "coverage" to capability
    * Daniel discussed with Jordan the definitions of Client and Server
    * Daniel pointed out Servers don't _have_ to only publish well-known metadata, and can have other endpoints
    * Daniel went through how to extend capabilities in other specs
    * Daniel said WG2 could add their data specs as a "capability" to the server metadata
        * Hallie agreed
    * Daniel went over Coverage endpoint format
    * Hallied asked if request for additional Coverage Entry Types
        * Daniel liked that idea and wants suggestions of new types, especially non-geographic types
    * Daniel discussed why only one of map image or geogjson was required instead of just geojson
        * Jordan suggested including geojson version, and Daniel agreed
    * For coverage, how do we do intersections/unions?
        * Hallie - maybe splitting up coverage_entries into different types of entries?
        * Daniel - also how do we have subset coverages for specific capabilities?
    * Call for consensus on minutes

## Closing Discussion
* Consensus to commit this to repo? Yes
