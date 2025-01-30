# CDSC WG1 (Customer Data) Meeting 2024-02-29

Recording: https://zoom.us/rec/share/51Kqj1WsEb4qewRqbnhTum9Bv20sDPVY4AnGrcnfhVxQjatWPrZavV8lktNWdICw.Zf19bcMPimSpAZqy

## Agenda
* Welcome
* Review progress on CDSC-WG1-02 (Client Registration) specification
    * Maintainer's Draft:
        * Overview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
        * Specification - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/
    * Possible topics:
        * Clients API
        * Client Settings API

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Ben White (Arcadia)
* Andreu Nadal (FlexiDAO)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)
* Jordan Hughes (Apple)

## Minutes
* Welcome and intro
* Overview of Clients API and grouping
    * [Daniel] client_secrets are grouped by common auth methods
    * [Eloi] Does the Server get to choose how credentials are grouped?
        * [Daniel] Not in the current spec
        * [Eloi] Maybe we could on certain use cases define groupings
        * [Daniel] yes, these groupings can be overridden in extended specs to specify special groupings
    * [Eloi] how can the data owner specify scopes?
        * [Daniel] yes, good point, need to include requirements that authorizee must be able to override the authorization request scope
        * [Daniel] do we want to have a "take it or leave it parameter" (TIOLI)?
        * [Eloi] The responsibility should be on the user
        * [Hallie] the user might not know what they need, and the third party might know what's needed more, so TIOLI might be helpful for user messaging
        * [Ben] There's UX to streamline errors for not accepting changes
        * [Daniel] Should the TIOLI parameter and user authorization flexibility of modifying scope be put in CDSC-WG1-02 or CDSC-WG1-03? My default would be include it in 02.
        * [Hallie] Seems right
        * [Eloi] So it's defined in 03 which socpes have which authorization methods (needing data owner consent vs. not)
* Overview of modifying Clients
    * [Daniel] Need to update to allow modifying `redirect_uris` since authorization requests don't have `client_secret`, so can't look up specific Scope Credentials.
    * [Daniel] Overview of 202 Accepted response and async update requests
* Overview of the Client Settings API
    * [Eloi] Why default_scope?
    * [Daniel] Need to have either default_scope or Server needs to reject auth requests with no scope
    * [Eloi] As long as can override the default, sounds good
* Next Steps and Timeline
    * [Daniel] Goal: Open PR for spec -02 by next meeting (2024-03-14)
    * [Daniel] Goal: Open PR for spec -03 by End of Q1 (2024-03-31)
    * [Hallie] Steering committee (2024-03-20)
    * [Daniel] LFEnergy Policy Summitt (2024-05-02) (hopefully give talk on specs)
    * [Daniel] Q2 and Q3, focus on writing additional materials to make specs more accessible (overview, examples, presentations)


## Closing Discussion
* Consensus to commit this to repo? Yes
