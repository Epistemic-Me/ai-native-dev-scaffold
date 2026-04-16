# AI-Native Development Scaffold — Run Stage

> **Mature engineering org with institutional memory.** Walk baseline + authoritative per-feature specs + product slop filter + compound learning from your own PR history.

This scaffold is the **Run** stage of a Walk → Run → Sprint AI-native maturity staircase. It extends the Walk scaffold with three net-new capabilities that mature engineering orgs need:

1. **Authoritative per-feature specs** (`docs/specs/*`) — one living spec per feature, updated by every PR. The input to auto bug triage. Eliminates the "ask an SME" dependency.
2. **Product slop filter** — stakeholder alignment scoring that can *reject* features, not just approve them. Filters strategically-wrong asks before they hit the roadmap.
3. **Compound learning from your own PR history** — `/compound` extracts episodes from merged PRs so "we solved this shape of problem before" becomes a query, not a memory.

## You Are Here: Walk / Run / Sprint

| Stage | What it is | Scaffold repo |
|---|---|---|
| **Walk** | Context foundation + 5-stage PR lifecycle + docs-gate CI. The operational baseline. | [`ai-native-dev-scaffold-walk`](https://github.com/Epistemic-Me/ai-native-dev-scaffold-walk) |
| **Run** *(← you are here)* | Walk + `docs/specs/` authoritative feature specs + product slop filter + `/compound` (internal episodes). Mature engineering org. | `ai-native-dev-scaffold-run` (this repo) |
| **Sprint** | Run + digital twins of external stakeholders + `/stakeholder-alignment` against customer voice + `/process-transcript` + self-model API. | [`ai-native-dev-scaffold-sprint`](https://github.com/Epistemic-Me/ai-native-dev-scaffold-sprint) |

**Don't start here.** Clone the Walk scaffold first, run it for 2 sprints until the 5-stage lifecycle and docs-gate feel native, then graduate to this repo when scattered feature specs and SME bottlenecks become the limiting factor.

## What Run adds beyond Walk

Everything in Walk plus:

### `docs/specs/` — authoritative per-feature specs

Each feature gets ONE living spec. Every PR that touches the feature updates it. The spec is the input to auto bug triage ("here's the acceptance criteria this feature was built against — does this bug violate it?").

Format:
```
docs/specs/
├── _INDEX.md               # Master registry of all feature specs
├── _TEMPLATE.md            # Blank template
└── {feature-slug}/
    ├── SPEC.md             # Living spec (updated by every touching PR)
    ├── ACCEPTANCE.md       # End-to-end acceptance criteria
    ├── OWNER.md            # Which team owns this feature
    └── HISTORY.md          # Changelog of spec changes with PR links
```

The scaffold ships `docs/specs/_TEMPLATE` and an example spec. Your team populates `docs/specs/*` over 2-3 sprints as you work on each feature.

### Product slop filter

Before a feature enters the roadmap, `/project:slop-filter` scores it against:
- **Strategic fit** — does this match our product direction?
- **Generalizability** — is this for one customer or for the 10,000 enterprise customers?
- **Effort vs. value** — realistic ROI
- **Regression risk** — does this cross domains we're not prepared to support?

Low scores block the feature. This addresses an enterprise VP of DX's concern (Apr 14 2026): *"a lot of [sales asks] we actually want to reject. [...] you're going to end up with product slop."*

### `/project:compound` (internal-only)

Extracts episodes from merged PRs into a local self-model directory (`docs/.compound/`). Supports query-by-pattern:

```bash
/project:compound query "interface migration across domains"
# Returns: [PR-211, PR-287] with RESEARCH.md excerpts and outcome summaries
```

At Run, compound learning is from **your own PR history only**. External customer signal comes at Sprint via `/process-transcript`.

### ADRs with predicted outcomes

Every ADR template at Run has a **predicted outcome** field. At 90 days post-decision, the team reviews: what did we predict? What happened? Calibration becomes measurable.

## What's carried over from Walk

Full Walk stack — nothing is removed:
- `.claude/commands/project/` with all 5-stage lifecycle commands
- `docs/.context/` core set
- `MCP_SERVERS.md` registry
- Credential policy
- `pr-docs-gate.yml` CI
- `docs/prs/` paper trail structure
- ADR index

See [`ai-native-dev-scaffold-walk`](https://github.com/Epistemic-Me/ai-native-dev-scaffold-walk) for the underlying baseline.

## Quick Start

```bash
# 1. Clone and reinitialize
git clone https://github.com/Epistemic-Me/ai-native-dev-scaffold-run.git my-project
cd my-project
rm -rf .git && git init && git add -A && git commit -m "init: run scaffold"

# 2. Populate docs/.context/ (as in Walk)

# 3. Create your first feature spec
cp docs/specs/_TEMPLATE docs/specs/my-feature
# Fill in SPEC.md, ACCEPTANCE.md, OWNER.md

# 4. Start your first PR — it will auto-link to the feature spec
/project:start-pr 001 my-first-feature
```

## Design Principle: Walker Floor, Runner Ceiling

Walk was designed for walkers. Run adds institutional memory without leaving walkers behind. The feature specs and product slop filter benefit walkers most — they stop getting bug tickets they can't understand because now there's an authoritative spec to consult.

## GitHub Copilot Compatibility

Same as Walk — tool-agnostic. Commands are markdown files with explicit context. Works with Copilot CLI, Copilot Cloud Agents, Claude Code, or any AI tool that reads command files.

## References

- **MIT NANDA — GenAI Divide 2025**: https://fortune.com/2025/08/18/mit-report-95-percent-generative-ai-pilots-at-companies-failing-cfo/
- **Anthropic — Claude Code best practices**: https://code.claude.com/docs/en/best-practices
- **GitHub — Continuous AI**: https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/

## License

MIT
