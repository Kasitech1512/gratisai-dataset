# GratisAI Index dataset

Every free AI tool in the [GratisAI Index](https://gratisai.com.au) directory,
with the pricing label we verified, a one-line reason for that label, and the
date we last checked the vendor's own page.

- **`dataset.json`** — the canonical file, one object with metadata and a `tools` array.
- **`dataset.csv`** — the same rows, flattened for spreadsheets. Arrays are joined with `; `.

Both files are generated from the site's catalogue by `npm run dataset`, so they
cannot drift from the directory. `generated_at` is the date of that build.

## Licence

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Use it commercially,
remix it, redistribute it — attribute it as:

> GratisAI Index (gratisai.com.au)

See [LICENSE](LICENSE).

## Fields

| Field | Meaning |
|---|---|
| `id` | Stable slug, also the URL: `https://gratisai.com.au/tools/<id>` |
| `name`, `tagline`, `description` | What the tool is |
| `website` | Official site |
| `category` | One of: coding, appbuilder, design, content, audio, video3d, research, agents, productivity |
| `subcategories` | Free-text tags |
| `pricing_model` | `100% Free`, `Generous Free Tier`, `Limited Free Tier`, `Open Source`, `Free Trial` |
| `pricing_reasoning` | Why that label, with published limits where they exist |
| `last_verified` | ISO date the entry was checked against the vendor page |
| `sources` | Vendor pages the label is based on |
| `license` | The software licence (not the dataset licence) |
| `platforms` | Where it runs |
| `pros`, `cons` | Short, specific lists |
| `date_added` | When it entered the directory |
| `scope_caveat` | Present when the tool is adjacent to scope; says what it is not |

Label definitions and the verification rules are at
[gratisai.com.au/methodology](https://gratisai.com.au/methodology).

## What is deliberately not included

- **Ratings and review counts.** They are user-submitted on the site and
  computed on read, so there is nothing stable to publish.
- **Upvotes.** Engagement figures that we cannot verify, so they are not
  exported as if they were data.
- **Paid-tier prices.** The dataset describes the free path; paid pricing
  changes often and belongs in the vendor's own page.

## Updates

This repository is a mirror. [`sync-dataset.yml`](.github/workflows/sync-dataset.yml)
fetches `dataset.json` and `dataset.csv` from gratisai.com.au once a day, checks
that the JSON parses and is non-empty, and commits only when the content changes.
To refresh by hand:

```bash
curl -fsSL https://gratisai.com.au/dataset.json -o dataset.json
curl -fsSL https://gratisai.com.au/dataset.csv -o dataset.csv
```

To change what is in the dataset, change the catalogue in the site repository
(`src/data/mockTools.ts`) and run `npm run dataset` there — do not edit the
generated files here.

## Corrections

Spotted a tool whose free tier has changed? Open an issue with the tool id and
the vendor URL you checked. Corrections are made against the vendor's page and
carry the date they were verified.
