# Add `growth.sales_objection_miner`

## What it does

This contributed Codex procedure turns founder-supplied prospect/customer objections into a compact marketing decision brief. It groups recurring concerns, separates observed language from inference, identifies the messaging gap each cluster suggests, and proposes concrete changes to the website, FAQ, sales enablement, or outbound messaging. It also produces a small reversible test plan.

The workflow is deliberately read-only: it does not contact prospects, send messages, modify provider data, publish content, or start another workflow.

## Who would run it

A founder, growth marketer, or sales/marketing lead after a batch of discovery-call notes, win/loss notes, support conversations, or other objection snippets has accumulated.

Inputs are bounded and founder-supplied:
- prospect/customer objections (3–40 items)
- optional target audience
- optional product/positioning context

Output:
- `reports/SALES_OBJECTION_BRIEF.md`

## Why an existing workflow does not cover it

Tin already has `example.feedback_digest`, which demonstrates generic feedback classification and summarization. This workflow has a different marketing outcome: it turns objection patterns into specific messaging-gap diagnoses and executable marketing changes, with a dedicated test plan and evidence/limitations section. It also intentionally treats repeated objection language as directional evidence rather than a representative customer statistic.

## How it works

1. Preserve the supplied objection statements as evidence and redact identifying details.
2. Read only relevant project context that helps interpret product, audience, pricing, or positioning.
3. Normalize wording and cluster objections by underlying buying concern.
4. Separate explicit customer language, recurring patterns in the supplied sample, and inferred marketing implications.
5. Convert material clusters into concrete website/FAQ/sales/outbound messaging changes.
6. Finish with a bounded test plan and explicit evidence limitations.

## Why this is a useful marketing workflow

Current sales guidance commonly emphasizes diagnosing the concern beneath the stated objection rather than replying to the surface wording. HubSpot's current objection-handling guidance describes objection categories such as budget, authority, need, and timing and emphasizes exploring the underlying concern. HubSpot's win-loss guidance likewise describes using reasons for wins/losses to drive targeted change. HubSpot also explicitly describes closed-lost objections and positioning/messaging gaps as useful inputs for marketing/sales alignment. Gong describes using large-scale call analysis to study objection-handling patterns. This package applies that general insight as a repeatable, founder-controlled workflow that converts a small supplied evidence set into marketing work rather than a generic sales script.

Research references:
- https://blog.hubspot.com/sales/handling-common-sales-objections
- https://blog.hubspot.com/sales/questions-to-ask-win-loss-review
- https://blog.hubspot.com/marketing/hubspot-marketing-sales-alignment-tips
- https://www.gong.io/blog/handling-sales-objections

## Testing

Added:
- `workflow_evals/growth.sales_objection_miner/qualification.json` with normal, mixed, and insufficient-evidence cases.
- `tests/test_sales_objection_miner_package.py` with offline manifest, bounds, safety/output, and qualification-shape checks.

The package is intended to be checked with the repository's standard commands:

```bash
uv sync --frozen
uv run tin-lite validate-community
uv run pytest tests/test_sales_objection_miner_package.py
```

The qualification cases are offline and do not use production credentials or paid provider calls.

## What did not work / limitations

An earlier design considered reading a live Gmail inbox automatically. That would have required an available, appropriately scoped project service binding and introduced unnecessary access to personal/customer data. The submitted version instead accepts bounded objection text from the founder and stays read-only, making the contribution fit the current procedure-package contract without inventing a new integration.

Public Registry registration is intentionally not included. The repository docs make `PUBLIC_WORKFLOWS` a maintainer-controlled selection step; merging the source package alone does not activate it.
