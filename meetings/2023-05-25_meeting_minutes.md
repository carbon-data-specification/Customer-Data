# CDSC WG1 (Customer Data) Meeting 2023-05-25

## Agenda
* Welcome
* Discuss client registration outline (CDSC-WG1-02):
    * Issue #16 - https://github.com/carbon-data-specification/Customer-Data/issues/16
    * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
* Discuss customer data scope design (CDSC-WG1-03):
    * Issue #24 - https://github.com/carbon-data-specification/Customer-Data/issues/24
    * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview
* Extensions for WG2
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer WG1)
* Eloi Ferrer (FlexiDAO)
* Grzegorz Bytniewski (FlexiDAO)
* Jordan Hughes (Apple)
* Steve Suffian (WattCarbon) (Maintainer WG2)

## Minutes
* Intros
* Overview of CDSC-WG1-01
    * Daniel - through metadata endpoint and capabilities framework
    * Greg - discussed how to define capabilities
    * Daniel - so WG2's capabilities could extend 01 spec to add Power Systems data capabilities
* Overview of CDSC-WG1-02
    * Daniel - adds capability to 01 spec "oauth"
        * oauth metadata extends rfc8414 (OAuth 2.0 Authorization Server Metadata)
        * normal OAuth metadata
        * adds CDS-specific extension to OAuth metadata format
        * also extends rfc7591 (OAuth 2.0 Dynamic Client Registration Protocol)
        * went through client extra registration fields and scope descriptions
    * Eloi - so if don't want to submit fields, this is a way to limit registration
        * pricing important to disclose
        * Daniel - good thing to add to scope requirements list
    * Jordan - native app support (no client_secret)
        * Daniel - yes, in OAuth 2.1, they use authorization_code with token_endpoint_auth_method=none + code_challenge
    * Daniel - client registration object format overview
        * settings api
        * updates api
        * scope credentials api
* Overview of CDSC-WG1-03
    * Daniel went through scopes and scope modifiers idea
        * Steve - what if scope modifier has less requirements???
        * Daniel - great question
            * should be nested or flat?
* WG2
    * could extend 01 and 02 to include their APIs in capabilities and scopes_supported


## Closing Discussion
* Consensus to commit this to repo? Yes
