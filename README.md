# IoT Connectivity and SIMs

The common IoT-connectivity vocabulary -- SIM cards and eSIM profiles, their data usage, and the connectivity plans they are on -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Connectivity, IoT Connectivity, eSIM, SIM, Cellular IoT, Mobile Data, Travel eSIM, MVNO in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| sim | 10 | 10 | iccid 80%, status 60%, id 50%, imsi 50% | sims 7, esims 2, esim 1, sim 1 |
| data_usage | 6 | 6 | id 67%, data_used 50% | usage 5, usages 1, sessions 1 |

Cohort: 35 providers with harvested OpenAPI, 10 crosswalks. Of the providers exposing a sim: 50% create, 90% list, 100% fetch, 40% update, 20% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- SIMs agree on iccid, status, id and imsi: the ICCID is the key every connectivity platform shares, because it is printed on the card and burned into the eSIM profile.
- Data usage agrees on id and data_used; the unit (bytes, MB, KB) is fixed per provider and is not stated in the field.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- iccid is kept as a property in its own right, not mapped to id, because most platforms carry both.
- Connectivity plans were dropped: a plan is a commercial bundle shaped by each provider.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
