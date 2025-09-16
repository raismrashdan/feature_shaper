# Feature Shaper — Spec
_Version: 1.0.0_

## Purpose
Turn plain-English feature intents into **drift-proof, machine-readable** work artifacts for Squads. The Feature Shaper does three things only: **Intake → Slice/Route → Ready-to-Build Packets**.

## Scope (and Non-Scope)
- **In scope:** translating intent, defining acceptance criteria (Gherkin), sequencing by dependencies, and emitting JSON artifacts.
- **Out of scope:** product strategy, code implementation, long-form PRDs, sprint governance.

## Inputs & Outputs
**Input:** your plain-English request.  
**Outputs:**
1. **Story Pack** (`story_pack.schema.json`) — the single source of truth for *what* and *why success*.
2. **Execution Packet(s)** (`execution_packet.schema.json`) — squad-targeted, sliceable work items with Gherkin AC.

### Story Pack (contract)
A compact description that a) captures intent and constraints, and b) sets success and guardrails.

```json
{
  "schema_version": "1.0.0",
  "story_id": "LP-023",
  "title": "Collect emails on landing and send a welcome email",
  "intent": "Add a waitlist box to the hero. Store email in Supabase. Send welcome if email service is configured.",
  "constraints": ["Use next-supabase-starter", "Accessible (WCAG AA)", "No PII in client logs"],
  "success_metrics": {
    "primary": [{"metric": "submit_rate", "target": ">=6%"}],
    "guardrails": [{"metric": "page_speed_lcp", "target": "<=2.5s"}]
  },
  "nfr": ["LCP<=2.5s", "Server secrets never exposed"],
  "risks": ["Spam signups"],
  "references": ["repo://", "org://design-system/forms"],
  "experiment": {"flag": "lp_email_form_v1", "variants": ["on", "off"]},
  "site_id": "my-landing-01",
  "tags": ["landing", "email", "waitlist"]
}
