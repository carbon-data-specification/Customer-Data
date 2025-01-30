# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-08-08

Recording: https://zoom.us/rec/share/0vfrAvRm5VMWiJkcU1zf8BBeQLFPXyhdIDzbXdGWd-yRclPfCpqXCS35FTDAeNsq.fIzETlgx3bkTekJ5

## Agenda
* Welcome
* Review examples of Usage Segments API for various situations
    * https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg3-01/overview#examples

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Liza Reines (Level 10 Energy)
* Georgios Syranidis (Field Energy)
* Samuel Cheptou (Ganular Energy)
* Jordan Hughes (Apple)
* Eloi Ferrer (Flexidao)

## Minutes
* Welcome and intros
* Going through examples
    * [Eloi] Should we include the ability to differentiate validated vs. estimated readings.
        * [Daniel] Possible options:
            * Add different `format` options:
                * "kwh_fwd" = validated kwhs
                * "kwh_fwd_estimate" = estimated kwhs
                * "kwh_fwd_raw" = received but not yet validated kwhs
                * Question: how does the usage_segment object change over time?
        * [Samuel] In Europe, different versions of validation referred to as "settlement run"
        * [Eloi] Preferr Option 1
        * [Samuel] Option 1 can be okay for use case

```
        # Option 1
        {
            "cds_usagesegment_id": "99999999-ab",
            "cds_created": "2025-02-15T04:00:00Z",
            "cds_modified": "2025-02-15T04:00:00Z",
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-15T00:00:00Z",
            "segment_end": "2024-02-15T00:00:00Z",
            "interval": 2678400,
            "format": ["kwh_fwd_estimate"],
            "values": [
                [
                    {"v": 500.0}
                ]
            ],
        },
        ########replaced by (with updated modified date)
        {
            "cds_usagesegment_id": "99999999-ab",
            "cds_created": "2025-02-15T04:00:00Z",
            "cds_modified": "2025-02-16T00:00:00Z",  # updated
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-15T00:00:00Z",
            "segment_end": "2024-02-15T00:00:00Z",
            "interval": 2678400,
            "format": ["kwh_fwd"],   # updated
            "values": [
                [
                    {"v": 500.0}
                ]
            ],
        },


        # Option 2
        {
            "cds_usagesegment_id": "99999999-ab",
            "cds_created": "2025-02-15T04:00:00Z",
            "cds_modified": "2025-02-15T04:00:00Z",
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-15T00:00:00Z",
            "segment_end": "2024-02-15T00:00:00Z",
            "interval": 2678400,
            "format": ["kwh_fwd_estimate"],
            "values": [
                [
                    {"v": 499.9}
                ]
            ],
        },
        ########replaced by (with updated modified date, with estimate still included)
        {
            "cds_usagesegment_id": "99999999-ab",
            "cds_created": "2025-02-15T04:00:00Z",
            "cds_modified": "2025-02-16T00:00:00Z",  # updated
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-15T00:00:00Z",
            "segment_end": "2024-02-15T00:00:00Z",
            "interval": 2678400,
            "format": ["kwh_fwd_estimate", "kwh_fwd"],   # updated
            "values": [
                [
                    {"v": 499.9},
                    {"v": 500.0}
                ]
            ],
        },
```

    * [Jordan] how do positively disclose gaps?

```
        # Option for disclosing why gaps in data
        {
            "cds_usagesegment_id": "99999999-3c",
            "cds_created": "2025-01-01T00:00:00Z",
            "cds_modified": "2025-01-01T00:00:00Z",
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-15T00:00:00Z",
            "segment_end": "2024-01-18T17:00:00Z",
            "interval": 900,
            "format": ["kwh_fwd"],
            "values": [
                [
                    {"v": 1.24}
                ],
                [
                    {"v": 1.01}
                ],
                ...
            ],
        },
        {
            "cds_usagesegment_id": "99999999-2309",
            "cds_created": "2025-01-01T00:00:00Z",
            "cds_modified": "2025-01-01T00:00:00Z",
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-18T17:00:00Z",
            "segment_end": "2024-01-18T18:00:00Z",
            "interval": 3600,
            "format": ["gap"],
            "values": [
                [
                    {"reason_type": "outage"}
                ],
                ...
            ],
        },
        {
            "cds_usagesegment_id": "99999999-3cb",
            "cds_created": "2025-01-01T00:00:00Z",
            "cds_modified": "2025-01-01T00:00:00Z",
            "related_aggregations": [...],
            "related_accounts": [...],
            "related_servicecontracts": [...],
            "related_servicepoints": [...],
            "related_meterdevices": [...],
            "related_billsections": [...],
            "related_eacs": [...],
            "segment_start": "2024-01-18T18:00:00Z",
            "segment_end": "2024-02-15T00:00:00Z",
            "interval": 900,
            "format": ["kwh_fwd"],
            "values": [
                [
                    {"v": 0.53}
                ],
                [
                    {"v": 1.23}
                ],
                ...
            ],
        },
```

    * [Samuel] For supply_mix, carbon intensity of residual isn't per customer, so shouldn't the `gco2_per_kwh` be in the power systems data APIs?
    * [Samuel] How the grid-supplied mix is represented in this?

```
# alternative way of organizing supply_mix
"format": ["supply_mix"],
"values": [
    [
        [
            {"type": "voluntary/ppa_specific", "mix": 0.25, "gco2_per_kwh": 0.8},  # individually attributable
            {"type": "grid_supply", "mix": 0.10, "gco2_per_kwh": 0.8},  # individually attributable
            {"type": "residual", "mix": 0.65, "gco2_per_kwh": 0.8},  # not attributable
        ]
    ]
],
```




## Closing Discussion
* Consensus to commit this to repo? Yes

