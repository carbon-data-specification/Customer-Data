# CDSC WG1 (Customer Data) Meeting 2024-06-06

Recording: https://zoom.us/rec/share/4Tw4GDoS-PkKSDUrvX67Zv0ktlBvDqt-rXG4RdBu9sYmEn0Hx3aezYyHzVLLkMZr.itfZ2kyN6gu82X7m

## Agenda
* Welcome
* Review how EACs fit into the Customer Data specification (CDSC-WG1-03):
    * Pull request (with comments): https://github.com/carbon-data-specification/Customer-Data/pull/26
    * Relevant part of the spec: https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/#eac-api

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Don Coffin (GBA)
* Atakan Esen (Apple)
* Hallie Cramer (Google)
* Karl Breustedt (Singularity Energy)
* Kris Donhowe (Renew Home)
* Samuel Cheptou (Granular Energy)
* Eloi Ferrer (Flexidao)

## Minutes
* Intro, welcome, and attendance

* EAC API overview
    * [Don] Isn't EAC a wholesale object?
    * [Hallie] For some portion of the supply mix, there may be EACs representing part of that supply.
    * [Hallie] Utilities who provide this may be pulling it from a registry.
    * [Samuel] Does EAC object represent contract or a proper EAC?
        * [Daniel] EAC API represents a proper EAC, not a contract.
            * However, contracts are represented in the ServiceContract API

    * [Hallie] "beneficiary_id" refers to what specific entry ID the "program_type" is going towards
        * `{..."program_type": "PPA", "beneficiary_id": "CUST123", ...}`
        * `{..."program_type": "rateplan", "beneficiary_id": "E-1", ...}`
    * [Samuel] what is source/destination names?
        * [Hallie] source=generator/asset, destination=whoever retires the RECs (if utility is doing it on behalf of customer, the destination=utility)
    * [Daniel] What does retiring mean?
        * [Hallie] "issuance", "transfer", "cancel/retire"
    * [Daniel] Should we restrict the EACs API to only canceled/retired EACs?
        * [Hallie/Eloi] Yes

* EAC matching to supply mix/usage
    * [Hallie/Samuel] The one that does the EAC usage match-up for the client isn't always the biller?
        * [Daniel] Two usage segments, one from each entity.
    * [Samuel] How do we relate sub-hourly usage with month-long EAC units?
        * [Samuel] keeping consumption and attribution/allocation separate
```
# just consumption (15min intervals)
{
    "segment_start": "2023-12-01T00:00:00Z",
    "segment_end": "2024-01-01T00:00:00Z",
    "interval": 900,
    "format": ["kwh_net", "supply_mix"],
    "values": [
        [{"v": 1.2}, {"solar": 0.5, "base": 0.5}],
        [{"v": 1.2}, {"solar": 0.8, "base": 0.2}],
        [{"v": 1.2}, {"solar": 0.2, "base": 0.8}],
        [{"v": 1.2}, {"solar": 0.5, "base": 0.5}],
        ...
    ],
},
# then in EAC API add related_* fields?
{
    "eacs": [
        {
            "cds_eac_id": "101010101-10",
            ...
            "related_servicecontracts": [
                "11111111111",
            ],
            ...
            "period_start": "2024-01-01T00:00:00Z",
            "period_end": "2024-02-01T00:00:00Z",
            "value": 1000000,
            "unit": "kwh",
        },
    ],
    "next": null,
    "previous": null
}
```
    * [Karl] How will this link to EnergyTag standard?
        * [Hallie] These EAC objects are coming from utilities, and could include EnergyTags in their objects


## Closing Discussion
* Consensus to commit this to repo? Yes
