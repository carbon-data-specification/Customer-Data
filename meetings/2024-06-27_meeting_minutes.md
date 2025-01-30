# CDSC WG1 (Customer Data) Meeting 2024-06-27

Recording: https://zoom.us/rec/share/kEZe8zWKN_jxp4Y089giSxC7qc0uwziS3L5WINm9emGlYLKtYZnt84B5cIpvCCjD.KMIgJ6sIQPqVtA_8

## Agenda
* Welcome
* Timeline and plans for splitting WG1 into WG1 ("Connectivity") and WG3 ("Customer Data")
    * `CDSC-WG1-01` ("Server Metadata") and `CDSC-WG1-02` ("Client Registration") remain in place
    * `CDSC-WG1-03` ("Customer Data") moves to WG3 as `CDSC-WG3-01`
    * Need to make updated [Use Cases](https://customerdata.carbondataspec.org/use-cases) and [Design Principles](https://customerdata.carbondataspec.org/specs/design-principles) for Connectivity WG1.
    * Separate websites, calendars, and mailing lists?
* Review examples for how EACs can be included in the Customer Data spec.

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Eloi Ferrer (Flexidao)
* Don Coffin (GBA)

## Minutes
* Welcome
* WG split logistics
    * Text of scope for new Connectivity WG:
        "This working group focuses on writing free, open specifications for utilities and
        other central entities ("Servers") to provide discovery, registration, connectivity,
        and profile management abilities to third party entities ("Clients"). By providing
        standardized protocols for these abilities, utilities and other central entities can
        significantly scale and streamline adoption and integration of carbon tracking platforms,
        energy management service providers, energy flexibility providers, and other entities
        that can accelerate the energy transition."
* Connectivity working group Use Cases and Design Principles
    * [Hallie] Maybe first two use cases would be the other two WGs?
* [Don] for section referencing Connectivity specs, instead of "based on" use "uses"
* Should moved pages have links to new page or automatically redirect?
    * [Hallie] automatic redirect preferred
    * [Daniel] automatic redirect also preferred
    * [Eloi] automatic redirect also preferred
    * [Don] automatic redirect also preferred
* Migrating Pull Request discussion
* Combined or alternating WG meetings?
    * [Eloi] While attendance is still less, keep it combined
    * [Hallie] Agreed, revist when have a longer group. Maybe send the agenda further in advance.
    * [Don] Consider longer than 60min?
* Connectivity "Launch" items?
    * [Daniel] reads other specs and suggests language to add to them to use the connectivity specs (starting with power systems WG, maybe also SAM WG)
    * [Daniel] demo implementation
    * [Everyone] Continue to do outreach to get utilities looking at the specs
    * [Eloi] Examples of other types of servers, not just utilities (suppliers, etc.), since Connectivity is more broad
    * [Don] Maybe outreach to utilities asking how the onboard 3rd parties.
* Will continue to work towards EAC/supply mix updates to Customer Data spec.
    * [Eloi] Would also like to discuss linkage between usage and supplier data? (forecasts, power outages linkages to specific contracts)

## Closing Discussion
* Consensus to commit this to repo? Yes
