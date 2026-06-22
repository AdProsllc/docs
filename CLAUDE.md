# AdPros — docs.adpros.com

Source for the internal docs site at https://docs.adpros.com. Every top-level directory is one published page.

## Repo structure

- `index.html` — password-gated page directory (the landing page at docs.adpros.com)
- `<slug>/index.html` — one published page per directory (case studies, briefs, frameworks, email digests, client work)
- `CNAME` — custom domain config for GitHub Pages

Each page is a self-contained HTML file with inline CSS, a password gate (`AP-GATE` block near the top), and the actual content inside `<div id="ap-content">`.

## How to query this content

The fastest commands for finding things across all pages:

- **Find pages by topic**: `grep -ril "<term>" --include="*.html" .`
- **List all pages**: `ls -d */ | sort`
- **Recently published**: `git log --oneline --name-only --since="30 days ago" -- '*/index.html'`
- **Last-modified date for a page**: `git log -1 --format="%ai" -- "<slug>/index.html"`
- **Read a page**: open `<slug>/index.html` and skip the `<head>`, `<style>`, `<script>`, and `AP-GATE` block (lines ~160-200). The substance lives inside `<div id="ap-content">`.

## Topic shortcuts

Common asks map to these directory clusters:

- **Agent / AI agent work** — `ai-agent-map`, `ai-agent-pipeline`, `ad-library-agents`, `agent-schema`, `agentic-taxonomy-v3`, `always-on-intelligence-layer`, `competitor-analysis-agent-sop`
- **Brand intelligence (BIE)** — `brand-intelligence-analyzer`, `47-skin-brand-intelligence`, `ag1-brand-intelligence`, `ag1-brand-intake`, `broya-brand-intelligence`, `broya-headline-matrix`
- **Pricing / commercial models** — `creator-commission-model`, `performance-pricing-model`, `performance-pricing-model-v2`, `tiktok-shop-agency-financial-model`, `turbotax-live-business-model`
- **Email digests** — `email-digest-YYYY-MM-DD/`
- **Client work** — `47-skin*`, `infiniwell*`, `nehal-*`, `broya-*`, `turbotax-*`, `ag1-*`

## Question patterns

- *"Show me pages about X"* → grep across all `*/index.html`, return a list of slugs with one-line context and the live URL (`https://docs.adpros.com/<slug>/`)
- *"What did we conclude about X?"* → grep, then read top 2-3 hits and synthesize
- *"Summarize the [slug] page"* → read that page's `<div id="ap-content">`, summarize substance only
- *"Most recent thinking on X"* → grep + `git log` to sort by publish date
- *"What's new this week?"* → `git log --since="7 days ago" --name-only -- '*/index.html'`

## Conventions

- Every published page uses the same chrome (header logo + footer logo, both 81×81 SVG)
- Pages are all password-gated with the same client-side SHA-256 gate — content is in source, but the live URL requires the password
- New pages are added via the `/publish` skill workflow; commits look like `feat: publish <slug>`
