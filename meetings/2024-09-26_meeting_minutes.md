# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-09-26

Recording: https://zoom.us/rec/share/NI-B9TI1Y4jqzV19iIWwgC_8sVidmqpUcuNeHuvl0JBytuRbb6p1CGJAJFH9tbfn.W5k_rk7pmFaxMM5V

## Agenda
* Welcome
* EAC object refactor: Moving data to external resource via `eac_data_url` and `eac_format`
    * Spec: https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg3-01/#eac-format
    * Example: https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg3-01/overview#eac-api
* What external resource formats should we pre-define for `eac_format` (if any)?

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Jordan Hughes (Apple)
* Don Coffin (GBA)
* Soazig Kaam (Google)
* Hallie Carrao (Google)

## Minutes
* Welcome and attendence
* Overivew of EAC refactor
    * [Hallie] sometimes pdfs, csvs, but more are having APIs
    * [Eloi] get files from the registry, different formats, but generally containing the same fields
    * [Eloi] risk: utilities will just put their attestation
        * legal doc just saying the green energy volumes (not coming from a registry, just the utility)
        * (which isn't what we want)

```
# PDF from a registry (customer assignment)
{
    "cds_eac_id": "99999999-dk3",
    "cds_created": "2024-01-01T00:00:00Z",
    "cds_modified": "2024-01-01T00:00:00Z",
    "eac_numbers": ["AAAZZZ-123"],
    "eac_format": "certiq",
    "eac_data_url": "https://demoutility.com/eacs/static/aaaaa.pdf",
    "assignment_type": "customer",
    "assignments": ["ABC Company"],
    "production_start": "2024-01-01T00:00:00Z",
    "production_end": "2024-02-01T00:00:00Z",
}

# CSV export from a registry (rateplan assignment)
{
    "cds_eac_id": "99999999-dk3",
    "cds_created": "2024-01-01T00:00:00Z",
    "cds_modified": "2024-01-01T00:00:00Z",
    "eac_numbers": ["AAAZZZ-123"],
    "eac_format": "ofgem_export_csv",
    "eac_data_url": "https://demoutility.com/eacs/static/ofgem_export_csv_aaaaa123.csv",
    "assignment_type": "rateplan",
    "assignments": ["GreenChoice"],
    "production_start": "2024-01-01T00:00:00Z",
    "production_end": "2024-02-01T00:00:00Z",
}

# attestation from a utility
{
    "cds_eac_id": "99999999-dk3",
    "cds_created": "2024-01-01T00:00:00Z",
    "cds_modified": "2024-01-01T00:00:00Z",
    "eac_numbers": [],
    "eac_format": "attestation",
    "eac_data_url": "https://demoutility.com/eacs/static/aaaaa.pdf",
    "assignment_type": "customer",
    "assignments": ["ABC Company"],
    "production_start": "2024-01-01T00:00:00Z",
    "production_end": "2024-02-01T00:00:00Z",
}

# API-based registry
{
    "cds_eac_id": "99999999-dk3",
    "cds_created": "2024-01-01T00:00:00Z",
    "cds_modified": "2024-01-01T00:00:00Z",
    "eac_numbers": [],
    "eac_format": "certiq_api",
    "eac_data_url": "https://demoutility.com/certiq-mirror/certs/123123123123.json",
    "assignment_type": "customer",
    "assignments": ["ABC Company"],
    "production_start": "2024-01-01T00:00:00Z",
    "production_end": "2024-02-01T00:00:00Z",
}
```

* TODO:
    * `beneficiary_type` --> `assignment_type`
    * `beneficiaries` --> `assignments`
    * `period_start` --> `production_start`
    * `period_end` --> `production_end`

* Is this the right direction?
    * [Hallie] the right direction
    * [Eloi] right direction
    * [Hallie] like that it's based on what the registry is providing

```
# Metadata format
{
    ...
    "cds_eac_formats": {
        "ofgem_export_csv": {
            "id": "ofgem_export_csv",
            "name": "Ofgem registry report export",
            "description": "A CSV export of the certificate reports from the Ofgem registry."
            "documentation": "https://ofgem.gov.uk/docs/cert-format",
        },
        ...
    }
    ...
}
```


## Closing Discussion
* Consensus to commit this to repo? Yes

