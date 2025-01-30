# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-08-15

Recording: https://zoom.us/rec/share/5CWOVtaOcxFdtMSqIsOnnl0P29DXSc6EJlqk6_67ED_jHjehU3fJlDmky7ZwJcr3.K71VY764rMeRhPWq

## Agenda
* Welcome
* Discuss advanced scope options

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Don Coffin (GBA)
* Liza Reines (Level 10 Energy)
* Olivia Vasquez

## Minutes
* Welcome
* Overview of last week's Usage Segment examples
    * [Daniel] Went through examples on https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg3-01/overview#examples
    * [Hallie] How connecting EACs at account or usage level?

```
# possible alternative to EAC example
{
    "cds_usagesegment_id": "99999999-vc3",
    "cds_created": "2025-01-01T00:00:00Z",
    "cds_modified": "2025-01-01T00:00:00Z",
    "related_aggregations": [...],
    "related_accounts": [...],
    "related_servicecontracts": [...],
    "related_servicepoints": [...],
    "related_meterdevices": [...],
    "related_billsections": [...],
    "segment_start": "2024-01-01T00:00:00Z",
    "segment_end": "2024-02-01T00:00:00Z",
    "interval": 2678400,
    "format": ["kwh_fwd", "eacs"],
    "values": [
        [
            {"v": 1000.0},
            [
                {
                    "csc_eac_id": "99999999-dk3",
                    "allocation": 1000.0,  # [Hallie] to think about where this can go (should it be in the EAC object instead?)
                },
            ],
        ]
    ],
},



{
    "eacs": [
        {
            "cds_eac_id": "99999999-dk3",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            ...
            "eac_number": "AAAZZZ-123",
            ...
            "beneficiary_id": "Green Pool A",
            "program_type": "TARIFF",
            ...
            "period_start": "2024-01-01T00:00:00Z",
            "period_end": "2024-02-01T00:00:00Z",
            "interval": 2678400,
            "unit": "kwh",
            "values": [
                {
                    "eac_number": "AAAZZZ-123-0001",
                    "value": 400000.0,
                },
            ],
        },
        ...
    ],
    ...
}
```

* Scope advanced examples `authorization_details_fields`

```
GET /oauth/authorize
?client_id=11111111
&response_type=code
&scope=bills+intervals
&authorization_details=URIENCODED([
    {
        "type": "bills",
        "historical_start": "2020-01-01",
        "ongoing_end": "3y",
        "device_pubkey": {...<jwk_public>...},
    },
    {
        "type": "intervals",
        "device_pubkey": {...<jwk_public>...},
    },
])

{
    "grants": [
        {
            "grant_id": "8888888888",
            "uri": "https://demoutility.com/api/clients/11111111/grants/8888888888",
            "replacing": [],
            "replaced_by": [],
            "parent": null,
            "children": [],
            "created": "2022-01-01T00:00:00Z",
            "modified": "2022-01-01T00:00:00Z",
            "not_before": null,
            "not_after": null,
            "eta": null,
            "expires": null,
            "status": "active",
            "client_id": "aaaaaaaaaa",
            "cds_client_uri": "https://demoutility.com/api/clients/11111111",
            "scope": "bills intervals",
            "authorization_details": [
                {
                    "type": "bills",
                    "historical_start": "2020-01-01",
                    "ongoing_end": "3y",
                    "device_pubkey": {...<jwk_public>...},
                },
                {
                    "type": "intervals",
                    "device_pubkey": {...<jwk_public>...},
                },
            ],
            "receipt_confirmations": [],
            "enabled_scope": "client_admin",
            "enabled_authorization_details": [],
            "sub_authorization_scopes": [],
        },
    ],
}


GET /api/accounts
Authorization: Bearer aaaaaaaaaaaaaaaaaaaaa

<encrypted with device_pubkey>({
    ...payload here
})
```




```
# if always included, then how does that make sense for client_credentials grant?
POST /oauth/token
&grant_type=client_credentials
&scope=power_systems_data
&authorization_details=URIENCODED([
    {
        "type": "power_systems_data",
        "device_pubkey": {...<jwk_public>...},
    },
])
```



## Closing Discussion
* Consensus to commit this to repo? Yes


