# SpaceCatalog data releases

Frozen, versioned copies of the [SpaceCatalog](https://spacecatalog.org) catalogue.

The site is corrected continuously, which is what a reader wants and
the opposite of what a citation needs: a paper's data-availability
section has to name something a referee can fetch in five years and get
the same rows back. A **release** is that name. Each one is published
here as a set of gzipped CSVs with a checksum per file, and nothing in
a published release ever changes.

What each release contains, and how to cite it: https://spacecatalog.org/releases

## Releases

| Release | Date | Objects | DOI |
| --- | --- | --- | --- |
| [DR1](https://github.com/space-catalog/data-releases/releases/tag/dr1) | 2026-08-21 | 223,448 | — |

## What is in DR1

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| `spacecatalog-dr1-objects.csv.gz` | 27,573,650 | `630ba7ae703659f0c4fe67480d11dd1f2c7eafd89bb2443361d68d9e91321398` |
| `spacecatalog-dr1-designations.csv.gz` | 3,531,501 | `1ea90d8d329d8b5b03f84fa15846a9ca2ecada5825dfd984fd0bc156b17114e6` |
| `spacecatalog-dr1-relations.csv.gz` | 37,530 | `b2e41ea6a22427a53abb7e7b09cb4bd875892ac5302e2e233e4dfd2a0e6382ff` |
| `spacecatalog-dr1-sources.csv` | 2,496 | `8f9c4d6441d1ed5c3ba38c35164ae275726167b3609df8e7eb2a1732dcb57ea4` |
| `spacecatalog-dr1-source_disagreements.csv` | 8,628 | `af601cb342ef877bde356bcc2ffff35dda5d0197f8167188482b3f6fd9e4b71b` |
| `LICENSE` | 11,357 | `c71d239df91726fc519c6eb72d318ec65820627232b2f796219e87dcf35d0ab4` |
| `RELEASE.md` | 2,993 | `44e3ae9ce537c5dbc7df1859b20f27ab6bb63b61ca561e6c05bdb100f8a04859` |

`spacecatalog-<release>.tar.gz` holds every one of those files plus
`manifest.json`, which states the row totals per category, the
plausibility results, the cosmology and position epoch the release is
fixed to, and the licence and retrieval date of every upstream.

## Verifying a download

```bash
curl -LO https://github.com/space-catalog/data-releases/releases/download/dr1/spacecatalog-dr1.tar.gz
curl -LO https://github.com/space-catalog/data-releases/releases/download/dr1/spacecatalog-dr1.tar.gz.sha256
shasum -a 256 -c spacecatalog-dr1.tar.gz.sha256
```

The bundle is built reproducibly — gzip's header clock and tar's
per-entry mtimes are zeroed — so the same catalogue packed twice gives
the same checksum, and the number above is a claim you can check rather
than one you have to trust. `SHA256SUMS` inside the archive covers each
file separately.

## Reading the data

One row per object in `objects.csv.gz`, keyed by a permanent slug;
`https://spacecatalog.org/object/<slug>` is the page for it. `designations.csv.gz` gives
every catalogue identifier that resolves to a slug, `relations.csv.gz`
the pairs and the orbits, and `sources.csv` the upstream every row's
`source` column names.

Magnitudes are apparent unless labelled and always carry their band;
distances are light-years with a `distance_method` saying which rung of
the ladder produced them; masses are kilograms; radii say which radius
they are; positions are ICRS J2000.0 degrees except for solar-system
bodies. `properties` is JSON, with published uncertainties under
`uncertainties` as `[minus, plus]`. A `data_quality` string is the
catalogue saying a published figure cannot be right — quote it if you
quote the number.

## Licence

The data is not under a single licence. See `LICENSE`, and
`sources.csv` inside each release for the terms of every upstream row
by row.
