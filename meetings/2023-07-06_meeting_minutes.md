# CDSC WG1 (Customer Data) Meeting 2023-07-06

## Agenda
* Welcome
* Review OAuth specs:
    * Rich Authorization Requests - https://www.rfc-editor.org/rfc/rfc9396
    * Pushed Authorization Requests - https://www.rfc-editor.org/rfc/rfc9126.html
* Continue discussion of CDSC-WG1-02 (Client Registration) and CDSC-WG1-03 (Customer Data):
    * Topics:
        * Using Rich Authorization Requests only?
    * Issue #16 - https://github.com/carbon-data-specification/Customer-Data/issues/16
        * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
    * Issue #24 - https://github.com/carbon-data-specification/Customer-Data/issues/24
        * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Brett Marraccini (UtilityAPI)
* Bailey Kane (UtilityAPI)
* Eloi Ferrer (FlexiDAO)
* Paul Pergolizzi (Office of Secretary of Defense)
* Jordan Hughes (Apple)
* Zachary Snier (Office of Secretary of Defense)
* Grzegorz Bytniewski (FlexiDAO)

## Minutes
* Introductions
* Agenda overview
* Daniel: Going over RAR and PAR specs
    * Greg: what about large payloads (talked about PAR)
    * Jordan: more customizable from a client, still undecided
    * Someone: oauth servers may not have RAR yet
    * Greg: how to specify what parameter, since utilities have different names for the same things (e.g. meters/service points/etc.)
    * Greg: what is the level of adoption of RAR?
    * Eloi: can do PAR before RAR?
    * Daniel: could offer both scope and auth_details in same server metadata, but require they be the same list and define in auth_details descriptions
    * Eloi: focus on end users leads us to offer more options
    * Greg: offer RAR, then add PAR later?
    * Greg: given that scopes not used for granular auths, auth_details step in right direction
* Review minutes

```
Scratch pad:

# normal OAuth 2.0
GET /oauth/authorize
    ?client_id=aaaaaaaaaa
    &scope=bills
    &response_type=code
    &redirect_uri=https://example.com
    &state=abc123




# OAuth Rich Authorization Requests (RFC9396)
AUTHORIZATION_DETAILS='[
    {
        "type": "bills",
        "meters": ["11111111"], (optional, default is select all)
        "historical_start": "3y", (optional, default is 3 years)
        "ongoing_end": "1y", (optional, default is 1 year)
    },
    ...
]'
GET /oauth/authorize
    ?client_id=aaaaaaaaaa
    &authorization_details=URLENCODED($AUTHORIZATION_DETAILS)
    &response_type=code
    &redirect_uri=https://example.com
    &state=abc123

# OAuth Rich Authorization Requests (large payloads, using RFC9126)
POST /oauth/pushed-auths
    client_id=aaaaaaaaaa
    &authorization_details=URLENCODED($AUTHORIZATION_DETAILS)
    &response_type=code
    &redirect_uri=https://example.com
    &state=abc123
<<< {
    "request_uri": "urn:ccccccccccccccccccccccc",
    "expires_in": 90
}
GET /oauth/authorize
    ?client_id=aaaaaaaaaa
    &request_uri=urn:ccccccccccccccccccccccc


# Server Metadata
{
    ...
    "scopes_supported": [
        "client_admin",
        "accounts",
        "services",
        "programs",
        "bills",
        "usage",
        "aggregate_usage"
    ],
    "authorization_details_types_supported": [
        "client_admin",
        "accounts",
        "services",
        "programs",
        "bills",
        "usage",
        "aggregate_usage"
    ],
    ...


    "cds_authorization_details_type_descriptions": {
        "client_admin": {
            "description": "..."
            "optional_parameters": {
                ...
            }
        },
        "bills": {
            "description": "..."
            "optional_parameters": {
                "historical_start": ...
            }
        },
    }
}
```

## Closing Discussion
* Consensus to commit this to repo? Yes
