# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-08-29

Recording: https://zoom.us/rec/share/nDHThPR5NQeIgRjjg8llayoySNeF96L1OMBB20dpJ4xfpAcJpGzFzihhqTMqYBgJ.5hP0hXVK_LxwqQIu

## Agenda
* Welcome
* Discuss EAC refactoring
    * https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg3-01/#eac-format

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Don Coffin (GBA)
* Jordan Hughes (Apple)
* Soazig Kaam (Google)
* Hallie Cramer (Google)
* Michael Murray (Mission:Data)
* Kris Donhowe (Renew Home)
* Eloi Ferrer (Flexidao)

## Minutes
* Welcome and overview
* Discussion of `benefiaries` refactoring.
    * [Hallie] and [Eloi] contributed feedback on how utilities allocate things.
* Discussion of `values` issued an retired.
    * [Eloi] Batch-level EACs is monthly, but can have `eac_number` for each MWh of the batch (with no start/end).


For batch-based EACs that just slice EACs up by value and not time?
```
{
    "eacs": [
        {
            "cds_eac_id": "101010101-10",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "eac_number": "AAAZZZ-123",
            "source_id": "101010101-10aaa",
            "source_name": "Company A",
            "destination_id": "101010101-10zzz",
            "destination_name": "Company B",
            "beneficiary_type": "customer",
            "beneficiaries": ["CUST123"],
            "asset_id": "AP111111",
            "asset_commissioned": "2023-12-01", # add?
            "asset_origination": "grid",
            "asset_destination": "grid",
            "technology_type": "solar",
            "emissions_factor_direct": "TODO",  # maybe remove?
            "emissions_factor_lca": "TODO",     # maybe remove?
            "period_start": "2024-01-01T00:00:00Z",
            "period_end": "2024-02-01T00:00:00Z",
            "values": [
                {
                    "eac_number": "AAAZZZ-123-001",
                    "issued": "2024-02-01",
                    "retired": "2024-02-01",
                    "start": null,      # make nullable?
                    "end": null,        # make nullable?
                    "unit": "kwh",
                    "value": 1000.0,
                },
                {
                    "eac_number": "AAAZZZ-123-002",
                    "issued": "2024-02-01",
                    "retired": "2024-02-01",
                    "start": null,
                    "end": null,
                    "unit": "kwh",
                    "value": 1000.0,
                },
                ... # 100 entries total (one for each 1MWh generation)
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

* Technology types for EACs
    * [Daniel] Does an EAC ever have multiple?
    * [Don] rename to generation type?
    * [Eloi] storage is under discussion as possible source types
    * [Jordan] nuclear and ocean/wave as tech types
    * [Eloi] Asset commission dates are relevant
* Asset origination and destination definitions?
    * Need Hallie's perspective

* Rateplan code vs. programs
    * [Daniel] Need program_participations at servicecontract level
    * [Kris] Will ask internally about programs vs. rateplans

* LF Energy Summit is next week!




## Closing Discussion
* Consensus to commit this to repo? Yes

