# Knowledge Maintenance Strategy

## Goals
- Keep documentation snapshots for Ghost, Cloudflare R2/Workers/Email, and comparison vendors current so design and implementation agents work from accurate references.
- Capture pricing or API changes quickly enough to adjust product plans before they impact users.

## Cadence & Triggers
- **Monthly checkpoint**: Knowledge Steward agent reruns the crawler and diffs outputs to catch incremental changes in docs or pricing.
- **Event-driven refresh**: Re-run the crawl whenever Cloudflare or Ghost announce major releases, when pricing tiers change, or when a new integration/feature is proposed.
- **Pre-release review**: Implementer agent requests a spot-check of relevant docs before shipping large features (for example, new upload workflows or email flows).

## Tooling
- `scripts/crawl_docs.py` draws from `knowledge/sources.json`. Keep new sources structured by category so reruns stay deterministic.
- Store raw `.html`, `.md`, and `.json` outputs under `knowledge/<category>/<slug>.*`. Avoid manual edits; regenerate via the crawler.
- Summaries live in `knowledge/README.md`. Update citation links when significant doc revisions change line numbers.

## Process Checklist
1. Sync main to ensure you have the latest `knowledge/sources.json`.
2. Run `python3.11 scripts/crawl_docs.py --sources knowledge/sources.json --output knowledge` (use `--category`/`--slug` if scoping the refresh).
3. Inspect the console output for failures; adjust URLs or slugs if vendors restructure navigation.
4. Commit regenerated artifacts along with an updated summary and note noteworthy deltas in the pull request description.
5. Ping the Implementer/Planner agents about breaking changes (for example, pricing adjustments or API deprecations).

## Ownership
- **Knowledge Steward agent** maintains the sources list and executes the cadence.
- **Implementer agent** raises refresh requests when encountering stale behavior during development.
- **Project Lead** approves additions/removals of doc sources to keep the crawl scope aligned with project goals.
