# CDSC WG1 (Customer Data) Meeting 2024-05-23

Recording: https://zoom.us/rec/share/u-F1KZfWXgdA464mTgXL6YexctNE4dyJco1AdMY978AtFJ7NIs8fSgqWQBeltBB2.0BAgYth1kOKCx2oj

## Agenda
* Welcome
* Review comments on CDSC-WG1-02 ("Client Registration"):
    * Pull request (with comments): https://github.com/carbon-data-specification/Customer-Data/pull/25
    * Rendering of spec: https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Kris Donhowe (Renew Home)
* Don Coffin (GBA)
* Bruno Menu (Granular Energy)
* Eloi Ferrer (Flexidao)
* Madhuban Kumar (CarbonLaces)

## Minutes
* Welcome and intros
* Pivot to CDSC-WG1-03 comment review
    * [Kris] comment in pull request about CARE and FERA
        * discounted tariff programs
        * [Daniel] need to distinguish between account-level attributes and service-contract attributes that affect the rate/charges calculations
        * [Don] in SCE, CARE is the actual rate (not a modifier)
        * [Don] also life support was the plan name
    * [Don] will find hundreds of these across the country
    * [Daniel] Example: DRAM program in CA
        * [Kris] effects aren't shown on the bill, but are paid out separately
        * [Daniel] where should a note of the customer participating in this program live?
    * [Daniel] Another example: EV charging special time periods
    * [Daniel] Add catch-all list of `???` objects for Servers denoting additional attributes/flags/program participation
        * Should these be split out by type (e.g. rateplan modifiers vs. participation vs. ...)?
        * Should they a flat list with `type`?
        * Should they a flat list with no `type`?
        * Should the Server be required to disclose what strings _could_ be in this list on their metadata?


In Service Contract object:
```
{
    ...
    "service_contract_attributes": [
        {
            "name": "DRAM",
            "status": "ACTIVE",
        },
        ...
    ],
    ...
}
```

In Client object:
```
{
    ...
    "cds_server_metadata": "https://.../cdsc.json",
    ...
}
```

In Server Metadata object:
```
{
    ...
    "oauth_metadata": "https://.../oauth-authorization-server",
    ...
}
```

In Oauth Metadata object:
```
{
    ...
    "possible_service_contract_attributes": [
        {
            "name": "DRAM",
            "description": "Participation in CA's DRAM program",
        },
    ],
    ...
}
```

    * [Kris] Info on whether `meter_type` is for EV charging, etc.?


Meter Devices:
```
{
    "meter_devices": [
        {
            "cds_meterdevice_id": "55555555-55",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "meter_number": "M55555555",
            "meter_type": "usage_net",
            "meter_use_case": "general",
            "submeter_of": [],
            "current_servicepoints": [
                "444444444-44",
            ],
            "previous_servicepoints": [],
        },
        {
            "cds_meterdevice_id": "55555555-55-subEV",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "meter_number": "SUB55555555-1234",
            "meter_type": "usage_forward_only",
            "meter_use_case": "ev_charging",
            "submeter_of": [
                "55555555-55",
            ],
            "current_servicepoints": [
                "444444444-44",
            ],
            "previous_servicepoints": [],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```


Usage Segment:
```
{
    "usage_segments": [
        {
            ...
            "cds_meterdevice_ids": [
                "55555555-55",          # main meter
                "55555555-55-subEV",    # submeter
            ]

            "segment_start": "2023-12-01T00:00:00Z",
            "segment_end": "2024-01-01T00:00:00Z",
            "interval": 900,
            "format": [
                {
                    "type": "kwh_net",
                    "cds_meterdevice_ids": ["55555555-55"],
                },
                {
                    "type": "kwh_fwd",
                    "cds_meterdevice_ids": ["55555555-55-subEV"],
                },
            ],
            "values": [
                [{"v": 1.2}, {"v": 1.2}],
                [{"v": 2.1}, {"v": 1.1}],
                ...
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```
    * [Eloi] Utility may not have access to submeter data?
        * [Daniel] Correct, so maybe that needs to be in the registration requirements disclosure (that Server only provides Usage Segments for meters it owns)?
        * [Eloi] In EU, DSO may have access to main meter, but supplier may have their own submeter data.
        * [Don] For apartments, EV charging gets billed to building owner, not tenants.



## Closing Discussion
* Consensus to commit this to repo? Yes
