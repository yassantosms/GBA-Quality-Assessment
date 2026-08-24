# flow-quality-assessment

**Cursor skill** for running a **Nubank product flow Quality Assessment** across three complementary pillars and generating an auditable HTML dashboard with the quadrant map (Star / Hidden Gem / Table Stakes / Skip).

## The 3 pillars

| Pillar | Role on the map | Scale | Parameters |
|---|---|---|---|
| **Craft** | X-axis → Magic | 1–5 | 6 (Navigation & Flow Logic, Performance & Resilience, Interaction/Motion & Feedback, Layout & Surface Craft, Brand & Content Compliance, Smart & Personal) |
| **User Experience Impact** | Y-axis → Customer Value | 1–5 | 3 (JTBD Efficiency, Customer Clarity, Trust) |
| **Business Impact** | Dot size | 1 / 3 / 5 | 1 per metric provided |

Craft and Value cut at **3** to position the flow. Business Impact sets dot size. Aggregation is always a **simple average**.

## User inputs

The rubric is fixed; what varies by product/team is provided at the start of the session. The skill runs **partially** — you don’t need all three to begin:

| Pillar | Input | Runs without? |
|---|---|---|
| Craft (Magic) | Flow only | ✅ runs on its own |
| User Experience Impact (Value) | Flow + **JTBDs** | needs JTBDs |
| Business Impact (dot size) | **Metrics** (name + target + stretch + reported) | needs metrics |

**The flow can come in three ways:**
- **Video / screen recording (strongly recommended):** best for motion, loading, overlaps, and the real end-to-end path. Embedded in the dashboard Evidence column.
- **Figma (preferred for components/tokens):** link(s) inspected via Figma MCP → detects NuDS V3 components, flags deprecations, checks localization, reads real tokens/typography.
- **Screenshots / screens:** images or PDF → observable assessment (component/token detection limited).

Supports the **same flow across multiple geos** (BR / MX / CO) for side-by-side comparison.

## Default output

- **Dashboard UI in English** (unless the user asks for another language).
- **Summary layout:** Evidence (video or screenshots) | Main issues | Quadrant map — three columns on the summary sheet.
- Media files live in the same folder as the HTML (relative paths).

## NuDS v3 as a live source

NuDS v3 rules are **not frozen in the skill** (they change over time). The skill consults the design system via the session connector (zeroheight/MCP or Glean). If unavailable (e.g. SSO), dependent parameters are marked as “subject to NuDS v3 validation.”

## How to scale to another team

No file edits required to adopt. Each team only provides **its own JTBDs and metrics** at the start of the conversation — the rubric (Annex A in `SKILL.md`) is the same for everyone. That keeps assessments comparable across teams.

## Structure

```
flow-quality-assessment/
├── SKILL.md            # instructions + full anchor rubric (Annex A) — source of truth
├── README.md           # this file
└── assets/
    └── rubric.json     # machine-readable rubric (labels, colors, quadrants, rules)
```

## Rubric origin

Official rubric “Craft / User Experience Impact / Business Impact — Parameters Score” (internal GBA deck, pp. 8–17). Level descriptions in `SKILL.md` are literal transcriptions from that source.
