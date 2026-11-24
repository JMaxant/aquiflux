# Context

What this project is about, in domain terms, and the vocabulary we use in code.

## The question

**How, and how fast, does rain reach groundwater?**

Rain that is not evaporated or taken up by plants seeps into the ground and refills
underground water reserves (*aquifers*). This refill is called **recharge**. Some aquifers react
within days (fractured granite in Brittany, karst), others over months (chalk in northern
France). `aquiflux` explores this relationship using French open data, one *département* at a
time.

## Data sources

| Source | What it gives | Access |
|---|---|---|
| [Hub'Eau, *Piézométrie*](https://hubeau.eaufrance.fr/page/api-piezometrie) | Monitoring stations and their groundwater level time series | REST/JSON API, no key, paginated |
| [Météo-France, *Données climatologiques de base quotidiennes*](https://www.data.gouv.fr/datasets/donnees-climatologiques-de-base-quotidiennes) | Daily rainfall, temperatures… per weather station | CSV files per département (used from phase 5) |

Field-level details of the Hub'Eau API are documented as they are explored (phase 1).

## Glossary

| Term (code) | French / source term | Meaning |
|---|---|---|
| `aquifer` | *nappe (phréatique), aquifère* | Underground layer of rock or sediment holding water. |
| `recharge` | *recharge* | Water that reaches and refills an aquifer. |
| `station` | *piézomètre, station de mesure* | A borehole where the groundwater level is measured. |
| `bss_code` | `code_bss` | National identifier of a station in the *Banque du Sous-Sol* (BSS). |
| `department_code` | `code_departement` | French *département* code: `01`–`95`, `2A`, `2B`, `971`–`976`. |
| `measurement` | *mesure* | One groundwater observation at a station on a date. |
| `time_series` | *chronique* | The ordered measurements of one station. |
| `groundwater_level` | `niveau_nappe_eau` | Water level as an altitude, in metres above the national reference (NGF). |
| `depth_to_water` | `profondeur_nappe` | Distance from the ground surface down to the water, in metres. |
| `weather_station` | *station météo* | A Météo-France station (phase 5). |
| `rainfall` | `RR` | Daily precipitation, in millimetres (phase 5). |

**NGF** (*Nivellement Général de la France*) is the French reference for altitudes.
`groundwater_level` and `depth_to_water` describe the same water from two viewpoints; we store
both (see ADRs).
