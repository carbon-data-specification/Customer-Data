# CDSC WG1 (Customer Data) Meeting 2024-02-01

Recording: https://zoom.us/rec/share/ZGFIupi3vDzl7zntgx4_j6syR5sJsIPDiPvBQO3JeDQQVJS0QHc7eky3-4ihqe6c.L4pK4Zm24ydn2IAI

## Agenda
* Welcome
* Review progress on CDSC-WG1-02 (Client Registration) specification
    * Maintainer's Draft - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
* Any other OAuth extension requirements? (Device Code flow? JWKs?)

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Jordan Hughes (Apple)
* Hallie Cramer (Google)
* Eloi Ferrer (FlexiDAO)
* Madhuban Kumar (CarbonLaces)
* Ben White (Arcadia)
* Natalie Kozlowski (independent)

## Minutes
* Take attendance and welcome
* Overview of progress on spec
    * Overview of what OAuth specs are included
    * What metadata fields from RFC 8414 are REQUIRED and no longer OPTIONAL/RECOMMENDED
        * [Eloi] depending on what scopes requested, the authorization process varies?
        * [Daniel] yes, (see client_admin example with client_credentials grant type)
    * What OAuth 2.0 extensions are required in CDSC-WG1-02:
        * Authorization Server Metadata (RFC8414)
        * Dynamic Client Registration (RFC7591)
        * Token Revocation (RFC7009)
        * Token Introspection (RFC7662)
        * Rich Authorization Requests (RFC9396)
        * Pushed Authorization Requests (RFC9126)
        * Proof Key for Code Exchange (RFC7636)
        * [Jordan] Maybe have also components of Native Apps (RFC8252)?
    * Spec currently doesn't prohibit other RFC extensions (e.g. JWT stuff)
        * [Eloi] Doesn't allowing other methods risk more complexity?
            * [Daniel] I'm currently interpreting other extensions as "additive" as optional enhancements and not a requirement for Clients to accomodate. But if that's not the case, I agree that we should prohibit additional required Client behavior to get access to use the Server.
    * [Jordan] How do clients manage access?
        * [Daniel] Using the default "client_admin" scope and Scope Credentials API

## Closing Discussion
* Consensus to commit this to repo? Yes
