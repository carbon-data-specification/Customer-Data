# CDSC WG1 (Customer Data) Meeting 2023-06-08

## Agenda
* Welcome
* Debrief from LFEnergy Summit
* Other working groups (WG2, SAM) extending CDSC-WG1-01 and CDSC-WG1-02
* Continue discussion of CDSC-WG1-02 (Client Registration):
    * Issue #16 - https://github.com/carbon-data-specification/Customer-Data/issues/16
    * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-02/overview
* Continue discussion of CDSC-WG1-03 (Customer Data):
    * Issue #24 - https://github.com/carbon-data-specification/Customer-Data/issues/24
    * Render - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Eloi Fabrega Ferrer (FlexiDAO)
* Grzegorz Bytniewski (FlexiDAO)
* Steve Suffian (WattCarbon)
* Jordan Hughes (Apple)
* Erdem Unal (Blok-Z)

## Minutes
* Took attendance and welcome
* LFEnergy summit debrief
    * Eloi and Daniel did a talk
    * Think it went well
    * Trying to get more companies involved
    * Questions that the audience brought up:
        * Questions about the scope of the working group
        * Denmark energy data hub
        * Whether we would connect with other data hubs that already exist, will they follow this standard
    * Should find a recording of the talk (maybe put them in the working group folder?)
    * Lot of other really good talks
    * Good insight into the other project spaces, and how we fit in
    * [Daniel] Approached by two other working group maintainers about possible collaborations
        * CDSC WG2 (power systems data, i.e. Steve)
        * SAM WG (super advanced metering, Utilidata)
* possible collaborations with other LFEnergy working groups
    * could these other specs use -01 and -02 as framework for providing discovery and client registration
    * is this going beyond our scope?
    * [Greg] how would organize it?
        * be another group?
        * does the first two specs need to be spun off to another working group?
    * [Steve] for now first two can be built in service of 3rd spec
        * in future iterations could be taken over by another working group
        * don't want to complicate building 3rd spec by overhead
        * for WG2, they would reference WG1 spec
    * [Daniel] my major concern on splitting out the specs is just current number of people involved is pretty low
        * propose that we keep -01 and -02 in WG1 for now, with possibility of splitting them into separate working group in the future
        * not any opposition
* Continue discussion on -02 spec
    * https://github.com/carbon-data-specification/Customer-Data/issues/16
    * scopes should be flat or nested?
        * [Steve] flat is more discoverable
        * [Greg] GCP has conditions, so could be similar to nested structure

```
Coding brainstorming scratch pad

        Option 1:
        /oauth/authorize
        ?client_id=aaaaaaaaaaaaa
        &response_type=code
        &scope=
            bills_pdf
            historical_2y
            bills_amount_due
            ongoing_1y

        Option 2:
        /oauth/authorize
        ?client_id=aaaaaaaaaaaaa
        &response_type=code
        &scope=
            bills_pdf
        &duration=
            historical_2y

        Option 3:
        Rich Authorization Request (rfc9396)
        "authorization_details": [
            {
                "type": "bills_pdf",
                "actions": ["read"],
                "duration": "historical_2y",
            },
            {
                "type": "bills_amount_due",
                "actions": ["read"],
                "duration": "ongoing_1y",
            },
            ...
        ]
        * [Greg] this is very similar to GCP
        * [Steve] differentator between type and condition
        * [Daniel] I need to read more up on rfc9396
```

* [Daniel] In addition to scopes for data fields,
modifiers/conditions on those data fields (e.g. duration),
there's also UX/preselectors for clients to customize
streamlined user authorization flow (e.g. select_by_account_numbers=*)

* Call for closing changes?


## Closing Discussion
* Consensus to commit this to repo? Yes
