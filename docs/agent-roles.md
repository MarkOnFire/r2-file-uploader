# Project Agent Roles

## Planner (you are here)
- Maintain the application plan, curate documentation, and coordinate handoffs between agents.
- Approve updates to `knowledge/sources.json` and major architectural changes before implementation starts.

## Implementer Agent
- Owns end-to-end delivery of features listed in `docs/application-plan.md`.
- Tasks include coding the Cloudflare Worker, front-end uploader, R2 integrations, and email flows.
- Must produce test evidence (CLI + manual Ghost checks) and update READMEs before marking a feature complete.

## Knowledge Steward Agent
- Executes the cadence outlined in `docs/knowledge-maintenance.md`.
- Keeps `knowledge/` artifacts fresh, highlights doc/pricing deltas, and proposes source additions/removals.
- Partners with Implementer to investigate unexpected API behavior.

## QA & Verification Agent
- Designs and runs smoke/regression tests across the Worker API, R2 uploads, Ghost embed, and email notifications.
- Maintains a manual test matrix (attach to `docs/` as needed) and signs off on releases.
- Coordinates with Implementer to reproduce bugs and validates fixes before deployment.

## Ops & Cost Analyst Agent
- Tracks Cloudflare usage metrics, Worker CPU time, R2 storage growth, and email throughput.
- Provides monthly cost reports using inputs from `docs/cost-analysis.md` and alerts the team when usage nears free-tier caps.
- Evaluates alternative tech stacks or SaaS replacements when costs or requirements change.
