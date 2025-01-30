# Joint CDSC WG1 & WG3 (Connectivity and Customer Data) Meeting 2024-09-12

Recording: https://zoom.us/rec/share/Bev0VZAZB4Ka71vzWev7uL2oKl9MGFpVEwS6ScUoeAUMkloq5Uxm9oVXDDOZHXoM.wpfiZErK5PpBOwX2

## Agenda
* Welcome
* Takeaways from LF Energy Summit
* Usage Segment formats
    * `kwh_net`
    * `kwh_fwd`
    * `kwh_rev`
    * `kw_demand`
    * `supply_mix`
    * ...

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Jordan Hughes (Apple)
* Don Coffin (GBA)
* Kris Donhowe (Renew Home)
* Killian Daly (EnergyTag)
* Hallie Carrao (Google)
* Eloi Ferrer (Flexidao)
* Susanne Mueller (Level 10 Energy)

## Minutes
* Welcome
* [Daniel] Summary and takeaways from LF Energy Summit (last week in Brussels)
    * [Daniel] Thought it went quite well
    * [Eloi] The need was there. A bit lost initially, so would have helped to do the spec presentation first, then discuss the needs. Maybe follow up with folks when we have a recording.
    * [Jordan] Noted growth in AI. May drive demand for better data access.
* [Don] Noticed more comments on EACs in pull request
* Talk about EAC comments

```
# PJM example
"values": [
    {
        "eac_number": "unitID_2023110104_xxxxxxxx - 1.000000 to 46.106820",
        "start": "2024-01-01T00:00:00Z",
        "end": "2024-01-01T01:00:00Z",
        ...
        "unit": "MWh"
        "value": 45.106820,
    },
    {
        "eac_number": "unitID_2023110104_xxxxxxxx - 46.106820 to 100.111",
        "start": "2024-01-01T01:00:00Z",
        "end": "2024-01-01T02:00:00Z",
        ...
        "unit": "MWh"
        "value": 54.00418,
    },
    ...
]

# EU example
"source_id": ...
"period_start": "2024-01-01T00:00:00Z",
"period_end": "2024-02-01T00:00:00Z",
"values": [
    {
        "eac_number": "871111799993800111150395776055",
        "start": null,
        "end": null,
        ...
        "unit": "MWh"
        "value": 1,
    },
    {
        "eac_number": "871111799993800111150395776056",
        "start": null,
        "end": null,
        ...
        "unit": "MWh"
        "value": 1,
    },
    ...for 30 MWh
]
```

* [Don] What about two types: fixed value batch and time based batch?
* [Kris] How will these be used to look up in the registry? Time range is very useful for querying.
* [Eloi] Like simplifying fields to only what's needed.

## Closing Discussion
* Consensus to commit this to repo? Yes

