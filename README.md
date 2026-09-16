# Manufacturing Energy Analytics

## Project charter
Build a reproducible manufacturing data platform using a real steel-industry energy dataset, with the final interactive dashboard hosted in Streamlit in Snowflake and accessible from a Mac browser.

Proposed repository: `Qb1005/manufacturing-energy-analytics`
Proposed GitHub Project: `Manufacturing Energy Analytics — Delivery Roadmap`
Status: complete issue-content draft; GitHub creation pending authenticated access. Nothing in this plan claims an implementation has been delivered.

## Dataset decision
Recommended source: [UCI Steel Industry Energy Consumption](https://archive.ics.uci.edu/dataset/851/steel+), DOI https://doi.org/10.24432/C52G8C. UCI describes real measurements from DAEWOO Steel in South Korea, 35,040 records, and CC BY 4.0 attribution requirements. Verify the downloaded file's schema, period, timestamp conventions, and granularity in issue 1.2 rather than assuming them from secondary articles.

Source attribution: V E, S., Shin, C., & Cho, Y. (2021). Steel Industry Energy Consumption [Dataset]. UCI Machine Learning Repository.

Why this source: manageable size, interpretable energy measurements, timestamps, and load categories support a clear dashboard and real data-engineering exercises. Kaggle AI4I 2020 is explicitly synthetic. UCI SECOM is real manufacturing quality data but anonymous sensor features make an introductory business dashboard less interpretable.

Scope limit: this is factory energy analytics, not a full MES/ERP production system. Do not invent machines, work orders, actual shifts, downtime, production quantities, defect rates, OEE, energy per item, or financial savings. The source's CO2 field name and published unit are inconsistent; do not publish an emissions KPI until resolved. Any optional tariff assumptions or historical arrival simulation must be labeled explicitly.

## End-to-end architecture
Original source snapshot → checksum manifest → chronological batch replay → Python validation/load → Snowflake RAW + OPS audit → dbt STAGING + MARTS → Streamlit in Snowflake.

GitHub PR → offline checks → reviewed main revision → DEV migration/load/dbt/validation → TEST → PROD approval → PROD → dashboard release/verification.

One source snapshot and one reviewed revision are the release contract. Historical data is not a live production feed.

## Dashboard deliverables
1. Overview: total kWh, trend, observed period and completeness, load mix.
2. Operating Patterns: daily/hourly profiles, weekday/weekend comparisons, highest-consumption intervals, filters.
3. Data Quality: batches, accepted/rejected rows, duplicate handling, missing intervals and lineage.

Metric definitions must specify units and grain. Sum interval energy; do not sum power factors. Do not label maximum interval energy as instantaneous peak power. Separate ingestion recency from the age of source observations. Compare only compatible complete periods.

## Execution environment
Use Streamlit in Snowflake with an explicitly selected supported warehouse runtime and the smallest practical warehouse. Verify account availability and runtime configuration before implementation. Snowflake is removing legacy Snowsight dashboards, so they are not the delivery target. No Windows or Power BI Desktop is required for the selected path. Account access, warehouse usage, and viewer permissions remain prerequisites.

## Project board
Statuses: Backlog → Ready → In Progress → Review → Done.
Fields: Phase, Priority (P1/P2), Delivery (MVP/Extension), Evidence (Missing/Partial/Complete), Execution (Planned/Implemented/Simulated/Deferred).
Views: Board by Status, Table grouped by Phase, Evidence Review filtered to Review or missing evidence.
Create real parent/sub-issue relationships and add every issue to the Project. Only 1.1 starts Ready; remaining items start Backlog. Use one issue in progress for step-by-step learning. Do not mark the old demo's work complete in this new repo without reproducing or explicitly carrying over its evidence.

## Files
- ROADMAP.md: full parent and sub-issue content.
- issues/: each issue body as a separate Markdown file.
- issues.json: stable planning keys, titles, parent keys, bodies and initial status; not GitHub issue IDs.

## Milestones
- Dashboard MVP: phases 1–7, completed only when the Snowflake app works and metrics reconcile.
- Engineering portfolio: phases 8–11, with AWS execution or clearly labeled local simulation.

## Sources
- Dataset: https://archive.ics.uci.edu/dataset/851/steel+
- Alternative: https://archive.ics.uci.edu/dataset/179/secom
- Synthetic Kaggle alternative: https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020/data
- Streamlit app creation: https://docs.snowflake.com/en/developer-guide/streamlit/app-development/creating-your-app
- Legacy dashboard retirement: https://docs.snowflake.com/en/release-notes/bcr-bundles/un-bundled/bcr-2260
