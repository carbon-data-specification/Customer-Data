# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-01-30

Recording: https://zoom.us/rec/share/2uQiT__8qXjkYr1Hq_5geasWdZQfZ8jE-wisV48zA4ToZXlKCKroFw3xyAFya8fF.oolKggUh8YvSrGPh

## Agenda
* Welcome
* Discuss updates to Client Registration spec (Messages API and removing Client Settings and Directory APIs)
    * https://github.com/carbon-data-specification/Connectivity/pull/5

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Soazig Kaam (Google)
* Jordan Hughes (Apple)
* Patrick Davis (Clear Trace)
* Don Coffin (GBA)
* Dionna Glaze (Google)
* Eloi Ferrer (Flexidao)

## Minutes
* Welcome and attendance
* Recent restructuring:
    * Client Updates API --> Client Messages API
    * Removed Directory API
    * Removed Client Settings API
* Planned changes:
    * Removing Scope Credentials fields: `scope`, `authorization_details`, `response_types`, `grant_types`, `token_endpoint_auth_method`, `redirect_uris`, `authorization_endpoint`, `token_endpoint`
        * Maybe rename Scope Credentials API --> Client Credentials API?
        * Move scope management to Clients API
    * Including JWK public key type in Authorization Details Field Formats
    * Including Server Metadata coverage in Scope Descriptions
* Next steps:
    * Make planned changes to PR #5.
    * Call for "stability" review for Connectivity specs.
    * Merge in PRs #4 & #5 as "stable" drafts (still clearly marked as drafts).
    * Subsequent changes and feedback will be individual PRs.

## Closing Discussion
* Consensus to commit this to repo? Yes

