# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-03-27

Recording: https://zoom.us/rec/share/NBc-dS8osVWABgiF65iavEUkhrMBiQbJFCu9FL-KCD64-c76ydaEholsvkzRAm0F.pk47ce9SFqafjQU3

## Agenda
* Welcome
* Continue discussion of Customer Data scopes
    * Use Case examples

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Eloi Ferrer (Flexidao)
* Don Coffin (GBA)
* Jordan Hughes (Apple)

## Minutes
* Welcome and attendence
* Scope use case examples
    * Carbon Accounting

```
# 1. Client sends authorization link to customer
https://demoutility.com/oauth/authorize
    ?response_type=code
    &client_id=flexidao
    &redirect_uri=https://flexidao.com/redirect
    &state=flexidao_request_11111111111
    &scope=cds_current_accounts_detailed+cds_bill_statements+cds_usage
    &cds_account_pre_selected=all|manual
    &authorization_details=[
        {
            "type": "cds_current_accounts_detailed",
            "sync_date_end": "1y",
        },
        {
            "type": "cds_bill_statements",
            "statement_date_start": "3y",
            "statement_date_end": "1y",
        },
        {
            "type": "cds_usage",
            "segment_start": "3y",
            "segment_end": "1y",
        },
    ]

# 
POST /token
code=aaaaaaaaaaaaaaaa
&grant_type=authorization_code
...
{
    "access_token": "bbbbbbbbbbbbbbbbbbb",
    ...
    "scope": "cds_current_accounts_detailed cds_bill_statements cds_usage",
    "authorization_details": [
        {
            "type": "cds_current_accounts_detailed",
            "sync_date_end": "2026-01-01T00:00:00Z",
        },
        {
            "type": "cds_bill_statements",
            "statement_date_start": "2021-01-01",
            "statement_date_end": "2026-01-01",
        },
        {
            "type": "cds_usage",
            "segment_start": "2021-01-01T00:00:00Z",
            "segment_end": "2026-01-01T00:00:00Z",
        },
    ]
}



GET /api/cds-accounts
{
    "accounts": [
        {
            ...
            "cds_modified": "2026-01-01T00:00:00Z",   # woudn't change after "sync_date_end" end date
            "cds_synced": "2026-01-01T00:00:00Z",   # woudn't change after "sync_date_end" end date
            ...
        },
    ],
    ...
}

# 2. Get customer's current rate (and nothing else)
https://demoutility.com/oauth/authorize
    ?response_type=code
    &client_id=flexidao
    &redirect_uri=https://flexidao.com/redirect
    &state=flexidao_request_11111111111
    &scope=cds_current_rate_plan
    &authorization_details=[
        {
            "type": "cds_current_rate_plan",
            "sync_date_end": "0d",  # so get current rate, but no further syncing after that
        },
    ]
```

* [Jordan] Ongoing date changes [Daniel][Soazig] add `"cds_synced"`?

## Closing Discussion
* Consensus to commit this to repo? Yes

