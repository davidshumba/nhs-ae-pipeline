# NHS A&E Performance Pipeline

A tested data pipeline for NHS England's monthly A&E performance data, built to answer one question properly:

> **How does performance against the 4-hour A&E standard vary across NHS trusts, and how has it changed over time?**

The NHS standard is that 95% of A&E patients are admitted, transferred or discharged within 4 hours. This project ingests the published monthly data, validates it, stores it in a local analytical database and analyses it in SQL.

**Status:** 🚧 In progress (v0.1 target: 30 November 2026)

---

## How it works

```
NHS England monthly CSVs
        │
        ▼
   ingest  (Python)        download / load each month's file
        │
        ▼
  validate (Python)        schema, types, missing values, duplicate months
        │
        ▼
    store  (DuckDB)        one clean, queryable table
        │
        ▼
  analyse  (SQL)           trust-level performance, trends over time
```

| Layer | Tool | Why |
|---|---|---|
| Ingestion & validation | Python, pandas | Readable, testable transformation logic |
| Storage | DuckDB | Fast analytical SQL on a single file, no server to run |
| Analysis | SQL | Window functions and aggregations where they belong |
| Testing | pytest | Every validation rule has a test |
| CI | GitHub Actions | Tests run on every push |

## Project structure

```
src/nhs_ae/   pipeline code (ingest, validate, load)
tests/        pytest test suite
sql/          analysis queries
data/raw/     downloaded source files (not committed)
```

## Getting started

```bash
git clone https://github.com/davidshumba/nhs-ae-pipeline.git
cd nhs-ae-pipeline
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e ".[dev]"
pytest
```

## Roadmap

- [x] Project structure, packaging and test setup
- [ ] Ingest monthly A&E CSVs into DuckDB
- [ ] Validation rules with tests (schema, types, nulls, duplicates)
- [ ] SQL analysis: trust-level 4-hour performance, monthly trends
- [ ] GitHub Actions CI running pytest on every push
- [ ] Findings write-up and "what I'd do differently"

## Findings

*Coming with v0.1.*

## Data source

[NHS England: A&E Attendances and Emergency Admissions](https://www.england.nhs.uk/statistics/statistical-work-areas/ae-waiting-times-and-activity/), published monthly. Contains public sector information licensed under the Open Government Licence v3.0.

## Licence

MIT
