# CDSC WG1 (Customer Data) Meeting 2024-04-25

Recording: https://zoom.us/rec/share/ag-Z8gqt4F4SjdJ52KAEg8qE-g_nX8cYQteb0tW3HfYf1O-g9QW9lv9ZT4HZSKb8.QT7qmwjLI9tRippy

## Agenda
* Welcome
* Review comments on the CDSC-WG1-03 (Customer Data) pull request
    * Pull Request (with feedback/comments):
        * https://github.com/carbon-data-specification/Customer-Data/pull/26
    * Maintainer's Draft:
        * Specification - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/
        * Overview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Atakan Esen (Apple)
* Madhuban Kumar (CarbonLaces)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)

## Minutes
* Welcome and attendance
* Going through comments on Pull Request #26
    * [Eloi] How to know what meters are associated with service points?
        * [Daniel] Top-to-bottom are done via GET query parameters, and bottom-to-top is in values in the objects
```
GET /servicecontracts
{
    "service_contracts": [
        {"cds_servicecontract_id": "3333333333-33", ...},
        ...
    ],
    ...
}


GET /servicepoints?current_servicecontracts=3333333333-33
{
    "service_points": [
        {"cds_servicepoint_id": "444444444-44", ..., "current_servicecontracts": ["3333333333-33"], ...},
        ...
    ],
    ...
}

GET /meterdevices?current_servicepoints=444444444-44
{
    "meter_devices": [
        {"cds_meterdevice_id": "55555555-55", ..., "current_servicepoints": ["444444444-44"], ...},
        ...
    ],
    ...
}
```

    * [Hallie] Billing cycle to Bill Statement?
        * [Daniel] Maybe better to put in the Bill Section?
        * [Hallie] Start/end date should be sufficient in the Bill Section
        * [Atakan] Are start/end always dates or can they be times?
            * [Daniel] Good thing to consider (maybe allowing dates and datetimes)
        * [Madhuban] Bill estimates (vs. actual readings) important to note when they happen
        * [Madhuban] Need visibility into type of meter
            * credit meter - fuel poverty ("top up their meter")
                * have fixed charge + usage for whatever you prepay for
                * meter turns off when run out of credit
            * regular meter
                * readings and billed normally
            * "credit soft"
                * like credit meter, but don't cut you off when run out of credit?
            * credit meters can become tricky when utility does estimates and true-ups (can overcharge an "estimate")
    * [Hallie] Why sometimes start/end in some bill section line items?
        * [Daniel] Some charges aren't based on start/end date
        * [Daniel] type can be subtotal/total, so can't just sum up line items (maybe we should move those out?)
        * [Hallie] want to filter on type of charge (demand, usage, etc.)
            * [Daniel] Maybe we can add a "item_category" (e.g. "demand charge", "usage charge", etc.)
        * [Hallie] How do bill corrections happen?
            * [Eloi] Normally publish a new bill statement with a correction in it
            * [Daniel] "cds_modified" indicates when the data changed, but should we add a "last_checked"?
            * [Eloi] End user can be expecting something is there already, but isn't there, so they need to know that the Server has checked recently, and didn't just quit.

* Quickly going through comments in last 7min


## Closing Discussion
* Consensus to commit this to repo? Yes
