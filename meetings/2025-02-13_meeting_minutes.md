# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-02-13

Recording: https://zoom.us/rec/share/9VuHUE0T-55-KE1HMebYTzll56tGODDhKC8UvrnzVYzYHG5aDx5G2efe2tUlw5A.pC5KiVM5SJ9g4C2b

## Agenda
* Welcome
* Discuss updates to Client Registration spec (Grants Admin, Credentials API, and Server-Provided Files)
    * https://github.com/carbon-data-specification/Connectivity/pull/5

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Soazig Kaam (Google)
* Jordan Hughes (Apple)
* Eloi Ferrer (Flexidao)
* Don Coffin (GBA)

## Minutes
* Welcome
* Changes to the spec
    * New `grant_admin` scope
    * New `cds_server_provided_files_api`
    * Default `redirect_uri` for authorization-based clients
    * Moving Scope from Credentials to Client objects
    * JWK as field type in auth details

* [Eloi] Is the Server-Provided Files used for customer data? How does authorization happen?
    * [Jordan] Could this be used in lieu of providing a real customer data spec?

* Planned for next time
    * Clarify that server-provided files are NOT intended to stand in for customer data sharing spec.
    * Update with examples
    * Add JWK to server-provide files auth details list
    * Customer Data updates!

## Closing Discussion
* Consensus to commit this to repo? Yes

