# CDSC WG1 (Customer Data) Meeting 2024-03-28

Recording: https://zoom.us/rec/share/tTtXDm2fjS5e0KMHpG0TLRXaXIv4jH7ZYZaYnDSY-F5ATc1ZeEkyt8VK3_DK0lWp.x9UIYuQ_9MolL6rf

## Agenda
* Welcome
* Review the CDSC-WG1-03 (Customer Data) pull request
    * Pull Request:
        * https://github.com/carbon-data-specification/Customer-Data/pull/26
    * Maintainer's Draft:
        * Specification - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/
        * Overview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)
* Atakan Esen (Apple)
* Andreu Nadal (FlexiDAO)

## Minutes
* Attendance and welcome

* EAC APIs
    * `eac_number` discussion (vs. `cds_eac_id`)
    * hourly EACs, do we need to use "segments" like usage?
    * [Eloi] how it works in EU
```
# Example EAC
* Volume: 100MWh
    * from prod_id 1234
    * issue date 2024-01-01
    * IDs meaning: 1MWh
    * EAC ids:
        * XXX-001
        * ...
        * XXX-100
```
    * [Hallie] see https://energytag.org/api/

* Usage Segments API
    * [Hallie] adding supplier mix to usage values (https://github.com/carbon-data-specification/Customer-Data/pull/26#discussion_r1554439782)
```
    "segment_start": "2023-12-01T00:00:00Z",
    "segment_end": "2024-01-01T00:00:00Z",
    "interval": 3600,
    "format": ["kwh_net", "kwh_fwd", "kwh_rev", "kwh_sources"],
    "values": [
        [
            {"v": 10.5},
            {"v": 10.5},
            {"v": 0.0},
            [
                {
                    "t": "fossil",
                    "v": 5.0,
                },
                {
                    "t": "solar",
                    "v": 2.5,
                    "cds_eac_id": "101010101-A",
                },
                {
                    "t": "wind",
                    "v": 3.0,
                },
            ],
        ],
        ...
    ],
```
    * [Hallie] EAC is the asset-level, and Usage Segments are at the usage-level, so may not be able to be linked.

* [Daniel] What is the EAC associated with (Service Contract? something else?)
    * [Hallie] depends on how the utility sets it up

* [Eloi] maybe would be good to have a mapping of potential use cases?
    * [Daniel] think that's a great idea
    * [Hallie] https://recs.org/download/?file=RECS-International-What-full-disclosure-means-and-why-it-is-so-important_FINAL.pdf&file_type=documents#:~:text=Full%20consumption%20disclosure%20means%20that,based%20on%20the%20residual%20mix.

## Closing Discussion
* Consensus to commit this to repo? Yes
