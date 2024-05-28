---
layout: base
nav: specs
title: CDSC-WG1 - 03 Customer Data - Overview
meta_description: Linux Foundation Energy - Carbon Data Specification Consortium (CDSC) - Customer DataWorking Group (WG1) - Specifications - cdsc-wg1-03 - Customer Data - Overview
---
[Home]({{ "/" | relative_url }}) / [Specifications]({{ "/specs" | relative_url }}) / [`cdsc-wg1-03` - Customer Data]({{ "/specs/cdsc-wg1-03" | relative_url }}) / Overview

# Customer Data - Overview

This is a summary overview of [`cdsc-wg1-03`]({{ "/specs/cdsc-wg1-03" | relative_url }}), which
describes how companies and technical users ("Clients") can request access to customer data from
utilities and other centralized entities ("Servers"). This specification builds upon
[`cdsc-wg1-02`]({{ "/specs/cdsc-wg1-02" | relative_url }}), which allows Clients to register with
a Server and be granted access to request various scopes of data from that Server using the OAuth
protocol.

For example, this specification describes how an energy efficiency app can request access from a
utility customer to see their account number, rate plan, and last year of energy usage.

## Customer Data Scopes <a id="scopes" href="#scopes" class="permalink">🔗</a>

* `cds_accounts_basic`
* `cds_accounts_contacts`
* `cds_accounts_detailed`
* `cds_servicecontracts_basic`
* `cds_servicecontracts_suppliers`
* `cds_servicecontracts_detailed`
* `cds_bill_amount_due`
* `cds_bill_statements_basic`
* `cds_bill_statements_detailed`
* `cds_bill_statements_files`
* `cds_bill_sections_basic`
* `cds_bill_sections_detailed`
* `cds_usage_basic`
* `cds_usage_detailed`

## Accounts Endpoint <a id="account-api" href="#account-api" class="permalink">🔗</a>

```
==Request==
GET /api/accounts HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "accounts": [
        {
            "cds_account_id": "111111111111-1",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "cds_account_parent": null,
            "account_number": "22222-222-22222",
            "account_name": "Example Company",
            "account_address": "123 Main St\nAnytown, TX 11111",
            "account_type": "business",
            "account_contacts": [
                {
                    "type": "primary_phone",
                    "value": "+15555555555",
                },
                {
                    "type": "primary_email",
                    "value": "example.company@example.com",
                },
                ...
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Service Contract Endpoint <a id="service-contract-api" href="#service-contract-api" class="permalink">🔗</a>

```
==Request==
GET /api/servicecontracts HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "service_contracts": [
        {
            "cds_servicecontract_id": "3333333333-33",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "cds_account_id": "111111111111-1",
            "account_number": "22222-222-22222",
            "contract_number": "333333-33-333333",
            "contract_address": "123 Main St - PARKING LOT",
            "contract_status": "active",
            "contract_type": "distribution_and_supply",
            "contract_entity": "Demo Utility",
            "contract_start": "2024-01-01",
            "contract_end": null,
            "service_type": "electric",
            "service_class": "commercial",
            "rateplan_code": "COMM-1A",
            "rateplan_name": "General Commerical 1A",
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Service Point Endpoint <a id="service-point-api" href="#service-point-api" class="permalink">🔗</a>

```
==Request==
GET /api/servicepoints HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "service_points": [
        {
            "cds_servicepoint_id": "444444444-44",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "servicepoint_type": "electric_meter",
            "servicepoint_number": "P4444LOT",
            "servicepoint_address": "123 Main St - PARKING LOT\nAnytown, TX 11111",
            "latitude": null,
            "longitude": null,
            "current_servicecontracts": [
                "3333333333-33",
            ],
            "previous_servicecontracts": [],
            "premise_number": "P4444",
            "premise_type": "parking_lot",
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Meter Device Endpoint <a id="meter-device-api" href="#meter-device-api" class="permalink">🔗</a>

```
==Request==
GET /api/meterdevices HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "meter_devices": [
        {
            "cds_meterdevice_id": "55555555-55",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "meter_number": "M55555555",
            "meter_type": "usage_forward_only",
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

## Bill Statement Endpoint <a id="bill-statement-api" href="#bill-statement-api" class="permalink">🔗</a>

```
==Request==
GET /api/billstatements HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "bill_statements": [
        {
            "cds_billstatement_id": "66666666-66",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "cds_account_id": "111111111111-1",
            "account_number": "22222-222-22222",
            "statement_date": "2024-01-01",
            "currency": "USD",
            "file_uri": "https://demoutility.com/api/rawfiles/66666666-66.pdf",
            "file_mimetype": "application/pdf",
            "previous_balance_amount": 10.00,
            "previous_balance_paid": -10.00,
            "previous_balance_unpaid": 0.00,
            "new_charges_amount": 9.99,
            "new_charges": [
                {
                    "name": "Electric Charges",
                    "cost": 4.99,
                },
                {
                    "name": "Account Fixed Fee",
                    "cost": 5.00,
                },
            ],
            "new_balance_amount": 9.99,
            "amount_due": 9.99,
            "amount_due_date": "2024-02-01",
            "shutoff_prevention_minimum_due": null,
            "shutoff_prevention_date": null,
            "program_participations": [
                {
                    "program_type": "financial_program",
                    "name": "Fixed-fee account",
                },
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Bill Section Endpoint <a id="bill-section-api" href="#bill-section-api" class="permalink">🔗</a>

```
==Request==
GET /api/billsections HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "bill_sections": [
        {
            "cds_billsection_id": "77777777-77",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "cds_billstatement_id": "66666666-66",
            "cds_account_id": "111111111111-1",
            "account_number": "22222-222-22222",

            "section_type": "distribution_and_supply_charges",
            "start_date": "2023-12-01",
            "end_date": "2023-12-31",
            "currency": "USD",
            "distribution_entity": {
                "type": "distributor",
                "entity": "Demo Utility",
                "cds_servicecontract_id": "3333333333-33",
                "contract_number": "333333-33-333333",
                "rateplan_code": "COMM-1A",
                "rateplan_name": "General Commerical 1A",
                "program_participations": [
                    {
                        "program_type": "aggregated_demand_response",
                        "name": "Acme Demand Response App",
                    },
                ],
            },
            "load_serving_entity": {
                "type": "distributor",
            },

            "related_servicecontracts": [
                "3333333333-33",
            ],
            "related_servicepoints": [
                "444444444-44",
            ],
            "related_meterdevices": [
                "55555555-55",
            ],
            "related_billsections": [],

            "line_items": [
                {
                    "item_type": "charge",
                    "for": "distribution_entity",
                    "name": "Electric delivery",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "cost": 2.00,
                    "value": 50.0,
                    "rate": 0.0400,
                    "unit": "kwh",
                },
                {
                    "item_type": "subtotal",
                    "for": "distribution_entity",
                    "name": "Total delivery charges",
                    "cost": 2.00,
                },
                {
                    "item_type": "charge",
                    "for": "load_serving_entity",
                    "name": "Electric supply",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "cost": 2.00,
                    "value": 50.0,
                    "rate": 0.0400,
                    "unit": "kwh",
                },
                {
                    "item_type": "subtotal",
                    "for": "load_serving_entity",
                    "name": "Total supply charges",
                    "cost": 2.00,
                },
                {
                    "item_type": "charge",
                    "for": "other",
                    "name": "Local taxes",
                    "cost": 0.99,
                },
                {
                    "item_type": "subtotal",
                    "for": "other",
                    "name": "Total other charges",
                    "cost": 0.99,
                },
                {
                    "item_type": "total",
                    "for": null,
                    "name": "Total electric charges",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "cost": 2.00,
                },
            ],

            "energy_summary": [
                {
                    "summary_type": "meter_reading",
                    "cds_meterdevice_id": "55555555-55",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "start_reading": 100000,
                    "end_reading": 100050,
                    "multiplier": 1,
                    "adjustment": 0,
                    "value": 50.0,
                    "unit": "kwh",
                },
                {
                    "summary_type": "usage_net",
                    "name": "Net Consumption",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "value": 50.0,
                    "unit": "kwh",
                    "tier_level": null,
                    "tou_bucket": null,
                },
                {
                    "summary_type": "usage_reverse",
                    "name": "Feed-in Generation",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "value": -1.0,
                    "unit": "kwh",
                    "tier_level": null,
                    "tou_bucket": null,
                },
                {
                    "summary_type": "usage_forward",
                    "name": "Total Consumption",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "value": 51.0,
                    "unit": "kwh",
                    "tier_level": null,
                    "tou_bucket": null,
                },
                {
                    "summary_type": "demand",
                    "name": "Commercial Peak Demand",
                    "start": "2023-12-01T00:00:00Z",
                    "end": "2024-01-01T00:00:00Z",
                    "value": 0.0,
                    "unit": "kw",
                    "tier_level": null,
                    "tou_bucket": null,
                },
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Aggregation Endpoint <a id="aggregation-api" href="#aggregation-api" class="permalink">🔗</a>

```
==Request==
GET /api/aggregations HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "aggregations": [
        {
            "cds_aggregation_id": "888888888-88",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "aggregation_type": "building",
            "aggregation_number": "B1111111",
            "addresses": [
                {
                    "full_address": "123 Main St\nAnytown, TX 11111",
                },
            ],
            "regions": [],
            "needs_consent": false,
            "consents_required": [],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Usage Segment Endpoint <a id="usage-segment-api" href="#usage-segment-api" class="permalink">🔗</a>

```
==Request==
GET /api/usagesegments HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "usage_segments": [
        {
            "cds_usagesegment_id": "99999999-99",
            "cds_created": "2024-01-01T00:00:00Z",
            "cds_modified": "2024-01-01T00:00:00Z",
            "related_aggregations": [],
            "related_accounts": [
                "111111111111-1",
            ],
            "related_servicecontracts": [
                "3333333333-33",
            ],
            "related_servicepoints": [
                "444444444-44"
            ],
            "related_meterdevices": [
                "55555555-55",
            ]
            "related_billsections": [],
            "segment_start": "2023-12-01T00:00:00Z",
            "segment_end": "2024-01-01T00:00:00Z",
            "interval": 900,
            "format": ["kwh_net", "kwh_fwd", "kwh_rev"],
            "values": [
                [{"v": 1.2}, {"v": 1.2}, {"v": 0.0}],
                [{"v": 1.1}, {"v": 1.1}, {"v": 0.0}],
                ...
            ],
        },
        ...
    ],
    "next": null,
    "previous": null
}
```

## Energy Attribute Certificate Endpoint <a id="eac-api" href="#eac-api" class="permalink">🔗</a>

```
==Request==
GET /api/eacs HTTP/1.1
Host: demoutility.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

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
            "beneficiary_id": "CUST123",
            "program_type": "PPA",
            "asset_id": "AP111111",
            "asset_origination": "grid",
            "asset_destination": "grid",
            "technology_type": "solar",
            "emissions_factor_direct": "TODO",
            "emissions_factor_lca": "TODO",
            "issuance_date": "2024-01-01",
            "retirement_date": "2024-02-01",
            "period_start": "2024-01-01T00:00:00Z",
            "period_end": "2024-02-01T00:00:00Z",
            "value": 1000000,
            "unit": "kwh",
        },
        ...
    ],
    "next": null,
    "previous": null
}
```


---

# Other Drafts <a id="other-drafts" href="#other-drafts" class="permalink">🔗</a>

* Maintainer's draft: [[Website](https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview)] [[Code](https://github.com/daniel-utilityapi/Customer-Data/blob/main/website/specs/cdsc-wg1-03/overview.md)]
