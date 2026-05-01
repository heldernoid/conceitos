# DESIGN-audit.md — Surface 4 · Audit & Oversight

**Status:** v0.4 · Abril 2026
**Form factor:** Desktop browser, ≥1280 px. Information-dense; designed to live on a 24″ monitor.
**Primary user:** Auditors at MISAU/DPI (Direcção de Protecção da Informação) and provincial DPSs. Secondary: Inspector-General, Direcção de Saúde Pública, ANARME.
**Setting:** Office, deliberate review work, never time-critical.

---

## 1. Product purpose

The audit surface exists because every other surface in the platform is auditable. A patient who flags an access, a pharmacist who flags a prescription, an emergency override at 22:48 — all flow here. The product makes three promises explicit:

1. **Nothing happens off the record.** Every read, every write, every override is signed and chained.
2. **Patients can challenge any access.** A flag opens a case with a real SLA, assigned to a real auditor.
3. **The auditors themselves are audited.** Every query an auditor runs is logged in a separate stream visible only to the Inspector-General.

This surface is *not* a security operations centre and not a real-time intrusion-detection system. It's a **deliberate review tool** — calm, dense, and traceable.

---

## 2. Information architecture

```
Sidebar (sticky)
├─ Visão geral          → national KPIs, provincial map, top critical events, heatmap
├─ Stream de eventos    → live feed, filters by severity / role / province
├─ Casos abertos        → list + detail (timeline, evidence, hypotheses, decision)
├─ Consultas e relatórios → structured query builder + saved reports
└─ Políticas & papéis   → role matrix, override/2FA/retention policies, change history
```

Top bar carries brand, primary nav, a live-stream pill, the auditor identity, and a link to this design doc.

---

## 3. Screens

### S1 — Visão geral
Four KPI cards (auditable events, overrides, patient flags, open cases) with weekly deltas. A provincial bar chart of accesses per 1 000 inhabitants — the auditor's first reflex on a Monday morning. Right column: top critical events (max 4) and a 7-day compliance bar chart (override-with-reason, patient notifications, 2FA, log integrity). Below: a 7×24 heatmap of access volume by hour of day, with after-hours cells outlined by a dashed amber border to flag investigation.

### S2 — Stream de eventos
The live event feed. Six-column rows: timestamp (mono), actor + role label, action + subject, location, role badge, status. Three states: OK, warning (amber tint), flagged (red tint). Filter chips at the top control severity and dimensions; the seg-control is the primary filter. Every block of events is hash-chained — the surface always shows the integrity status as a tail note.

### S3 — Casos
Two views: list and detail.

**List** — case ID (mono), severity badge, title, who/where, age, SLA remaining, assigned auditor. Cases sort by SLA criticality, not creation time.

**Detail** — central focus of the audit surface.
- Header: case ID, severity, type, SLA, investigator
- **Timeline**: every relevant event in order. Tinted dots mark warning and flagged events. This is the auditor's primary instrument.
- **Provas e anexos**: signed log files, source documents (admission sheets), and recordings (e.g. patient-verification calls).
- **Right column**: people involved (patient, professional, facility), **hypotheses ranked by likelihood** (most-likely / plausible / improbable — explicit reasoning, not a black box), and the **decision** form (4 outcomes: resolve / process failure / suspected misuse / escalate to ANARME or OM).

Decisions are signed, become part of the public audit log, and are visible to both the professional and the patient.

### S4 — Consultas e relatórios
A structured query builder ("show me / where / and / and / period / group by") that returns metadata only — never clinical content. A live preview pane on the right shows the current query result. Below: saved queries (Top prescritores Tabela II, sessions out-of-hours, patients with > 3 flags, etc.), shareable with ANARME or DPSs. The blue privacy strip makes the boundary explicit.

### S5 — Políticas & papéis
Role matrix (5 roles × 4 capabilities + count). Then six policy cards covering Override, 2FA, Retention, Cross-facility, Right-to-be-forgotten, Auditor-of-auditor. Each card shows version, last change, and conformance %. Edits require 2 approvals and are themselves logged.

---

## 4. Components & patterns

| Component | Audit-specific notes |
|---|---|
| **Stream row** | Read-dense; mono timestamp aids vertical scanning. Severity by row tint, not icon, so colourblind users still distinguish via background luminance. |
| **Heatmap** | 7×24 grid using oklch lightness for intensity. Dashed amber outlines mark after-hours intensity above threshold. |
| **Case timeline** | Tri-column event row (timestamp / dot / event). Warning and flagged events tint dot only — the row itself stays neutral so the timeline reads continuous. |
| **Hypotheses card** | Three labelled rows (mais provável / plausível / improvável). Forces the auditor to write reasoning, not just a verdict. |
| **Decision form** | A select + a justification textarea. The note about signed visibility appears below the form. |
| **Query builder** | Stacked select rows in a "show me / where / and …" pattern. Less power than SQL, more legible than SQL, and **all queries are logged**. |
| **Role badge** | Five colour variants (doc/nurse/pharm/admin/pat) used consistently across feed, cases and EMR access logs. |
| **Policy card** | Title, version chip, last-change date, conformance badge. Six total — never more on one screen. |

---

## 5. Severity & SLAs

| Severity | Visual | Default SLA | Examples |
|---|---|---|---|
| Crítico (red) | red dot, red row tint | 7 days, escalate after 24h | override without reason, suspected fraud |
| Alto (amber) | amber dot, amber row tint | 7 days | cross-facility cluster, prescription tampering, after-hours pattern |
| Médio (grey) | grey dot, no row tint | 14 days | auth-error spikes, narcotics ledger drift |

SLA timers freeze when a case is in "aguardando resposta do profissional" and resume on response.

---

## 6. Privacy & integrity

- The audit surface displays **metadata** (who, when, where, action type, subject identity) — **never clinical content**. Reading clinical content from this surface is not possible by design.
- Every event is hashed with the previous event's hash; tampering breaks the chain and surfaces as a top-level alarm.
- **Auditor-of-auditor:** every action an auditor takes (query executed, case opened, decision signed) is written to a separate log accessible only to the Inspector-General. The "Logs do auditor" sidebar item links there.
- Decisions on cases are visible to the implicated professional and to the patient. A patient who flagged an access sees the outcome in their app.

---

## 7. Roles & permissions

| Role | Surface access |
|---|---|
| **DPI auditor** | All five views. Cannot edit policies. |
| **Provincial auditor (DPS)** | All five views, scoped to their province. |
| **Inspector-General** | All views + the auditor-of-auditor log. |
| **MISAU policy admin** | Política & papéis only. Edits require dual approval. |
| **ANARME / OM observer** | Read-only access to overview + saved queries shared with them. |

---

## 8. Visual theme & posture (Audit)

The audit surface is **the most institutional in the family**. References while drafting: Bloomberg Terminal (target: warmth without losing density), national tax authority dashboards, the OSCE election-observation toolkit. Anti-references: SOC tools (Splunk, Elastic SIEM), IDS dashboards — those are real-time and red-heavy. Audit is **slow, deliberate review**, not alarming.

The dominant chrome colour is `green-900` (`#0F3D27`) for the sidebar — the deepest brand surface in the system. The content area is `bg-2` (`#F2F1EB`) — a half-step warmer than the page background — to signal "data working surface". Tables are wide, dense, mono-rich. Severity reads via row-tint luminance (not icons alone) so colourblind auditors can still distinguish.

The audit surface is **the only one where 13-px body type appears in tables** (vs 14 elsewhere). Auditors review hundreds of events per session and need vertical density. Conversely, decision and hypothesis writing zones use 14-px body to encourage careful prose.

---

## 9. Component stylings (Audit)

### Stream row
- 44-px row, 1-px bottom hairline.
- Columns: timestamp (mono 13-px / 500 ink) · actor (14-px / 500 ink) + role label (12-px / 400 ink-3) · action description (13-px ink-2) · location (13-px ink-3) · role badge · status badge.
- Row tints: warning `#FFFBEF`, flagged `#FCEFEC`, normal white.
- Hover: row darkens by one luminance step (warning → `#FEF6E0`, flagged → `#F8E4DF`).
- Click opens case-detail or event-detail pane.

### Heatmap (7 × 24)
- 24 columns × 7 rows of 28-px cells.
- Cell fill via `oklch()` with constant chroma + variable lightness scaled to event count.
- After-hours cells (22:00–05:59) above threshold get a 1-px dashed `#C8911E` outline.
- Axis labels: 11-px / 600 / 0.06em UPPERCASE ink-3.
- Tooltip on hover: 12-px ink, white surface, 1-px hairline, mono count.

### Case-list row
- 56-px row, 7 columns: case ID (mono 13-px / 500 / blue-700) · severity dot (8-px) · title (14-px / 500 ink) · who/where (12-px ink-3) · age (12-px mono ink-3) · SLA remaining (mono, coloured by criticality) · assigned auditor avatar + name.
- Sort default: SLA criticality, NOT creation time. SLA < 24 h tints the SLA cell red; 24–72 h amber.

### Case timeline
- Tri-column rows inside the case-detail page: 100-px timestamp column (mono 13-px ink-3) · 24-px dot column · event description column (14-px ink).
- Dot variants: 8-px circle, neutral `#8A8A8A`, warning `#C8911E`, flagged `#C2392A`.
- Connecting line between dots: 1-px `#D9D7CF`.
- Row itself stays neutral background — the timeline reads continuous; only the dot signals severity.

### Hypotheses card
- White surface, 1-px `#D9D7CF`, 4-px radius, 16-px padding.
- Three labelled rows: "Mais provável", "Plausível", "Improvável" — overline 11-px / 600 / 0.06em UPPERCASE ink-3.
- Each row has a 14-px body field, multi-line, with auditor's reasoning required.
- A meta line at the bottom: "Sem hipóteses, nenhuma decisão pode ser assinada." — enforces the methodology.

### Decision form
- Select with 4 outcomes: Resolver · Falha de processo · Suspeita de uso indevido · Escalar para ANARME / OM.
- Below select: 14-px body textarea (max 2 000 chars).
- Below textarea: 12-px ink-3 note "A sua decisão é assinada e fica visível para o profissional implicado e para o utente sinalizador."
- Submit button: `lg` primary, full-width, 14-px / 500 "Assinar decisão".

### Query builder
- Stacked select rows in a "show me X / where Y / and Z / period / group by" pattern.
- Each row: label (overline 11-px / 600 / 0.06em UPPERCASE ink-3) · select control (36-px tall).
- Add-row button: ghost variant, "+ adicionar condição".
- Right column: live preview pane with metadata-only result rows.
- Privacy strip across the top: blue-100 fill, blue-700 1-px border, ink text "Esta consulta retorna apenas metadados. Nunca exibe conteúdo clínico. Cada execução é registada no log auditor-do-auditor."

### Policy card
- White surface, 1-px `#D9D7CF`, 4-px radius, 16-px padding.
- Title 16-px / 600 ink + version chip (`v3.2`, mono 11-px in green-100 plate).
- Body 13-px ink-2 with policy summary.
- Footer: last-change date (12-px ink-3 mono) + conformance badge (green-100 if ≥ 95%, amber if 80–94%, red if < 80%).
- "Ver histórico" link blue-700 right-aligned.

### Role badge
- 22-px height, 0 8-px padding, 11-px radius, 11-px / 500 text.
- Five fixed variants: Médico (blue-100/blue-700) · Téc. Medicina (green-100/green-700) · Enfermeiro/a (green-100/green-700, lighter weight) · Farmacêutico/a (amber-100/amber-500) · Administrativo (neutral) · Cidadão/ã (white + 1-px hairline).
- **Variants are fixed across the platform** — same colours on EMR access log, audit feed, and patient app.

---

## 10. Layout & spacing (Audit)

- Sidebar 220 px, sticky, `green-900` fill, white items.
- Top bar 56 px with brand stack, primary nav (overview / stream / cases / queries / policies), live-stream pill, identity badge, link to design doc.
- Content area `bg-2` (`#F2F1EB`) — distinguishes audit from clinician/patient surfaces.
- Cards inside content: 24-px gutter, 16-px internal padding.
- Tables: full-bleed inside content with 24-px outer padding, no card wrapper (audit tables are *the* working surface).

---

## 11. Do's and Don'ts (Audit)

### Do
- Render **metadata only**. Who, when, where, action, subject identity. Never the clinical content of an encounter.
- Sign **every decision**. Decisions are public to the implicated professional and the flagging patient.
- Show the **audit chain integrity status** as a tail note on every event view.
- Force **hypothesis writing** before decision. The hypothesis card is the methodology.
- Surface **auditor-of-auditor logs** to the Inspector-General role only.
- Tint severity into the row background, not via icon alone (colourblind support).
- Default sort cases by **SLA criticality**, not creation time.
- Treat **patient flags as real cases** with auditor assignment and SLA — never auto-resolve.

### Don't
- **Don't show clinical content.** Even an encounter SOAP excerpt is a violation of the surface's promise.
- **Don't auto-suggest decisions** in v0.4. Hypotheses are human-written; ML risks anchoring.
- **Don't allow a single auditor to close their own case** without dual review for severity-critical.
- **Don't expose audit data to non-audit roles** beyond the read-only ANARME/OM observer scope.
- **Don't allow free-text SQL.** All queries go through the structured builder and are logged.
- **Don't display real-time alerts as a primary affordance.** Audit is review work, not SOC.

---

## 12. Responsive behaviour (Audit)

| Width | Treatment |
|---|---|
| ≥ 1920 px (wide) | Sidebar 220 + content max 1440 + side gutters absorb extra. Tables expand to use full content width. |
| 1440–1920 px | Default design target. Sidebar 220 + content. |
| 1280–1440 px | Same layout, table density unchanged. |
| 1024–1280 px | Sidebar collapses to 60-px icon rail (hover-expand). Tables compress secondary columns (location merges into actor stack). |
| 768–1024 px | Sidebar in drawer. Tables become scrollable horizontally with sticky first column (case ID / timestamp). |
| < 768 px | Not supported. Auditors are office workers; sign-in works but redirects to "Use a desktop". |

---

## 13. Agent prompt guide (Audit)

### Component prompts
- **Stream row:** "44-px row, 1-px `#D9D7CF` bottom hairline. Mono timestamp 13-px / 500 ink. Actor name 14-px / 500 ink + role 12-px ink-3 stack. Action 13-px ink-2. Location 13-px ink-3. Role badge. Status badge. Tints: warning `#FFFBEF`, flagged `#FCEFEC`, normal white."
- **Heatmap cell:** "28-px square cell, oklch fill with constant chroma and variable lightness mapped to event count. After-hours cells above threshold get 1-px dashed `#C8911E` outline. 11-px UPPERCASE 0.06em axis labels in ink-3."
- **Case timeline event:** "Tri-column row: 100-px timestamp column (mono 13-px ink-3) · 24-px dot column · event description (14-px ink). Dot 8-px circle, severity-tinted. Connecting line 1-px `#D9D7CF`. Row background stays neutral."
- **Hypotheses card:** "White surface, 1-px `#D9D7CF`, 4-px radius. Three labelled rows: 'Mais provável', 'Plausível', 'Improvável' — overline 11-px UPPERCASE 0.06em ink-3. Each row a multi-line text field. Bottom meta: 'Sem hipóteses, nenhuma decisão pode ser assinada.' in 12-px ink-3."
- **Privacy strip (queries):** "Full-width strip, blue-100 fill, 1-px blue-700 border, 4-px radius, 12-px padding. 13-px ink. Always present above the query builder."
- **Policy card:** "White, 1-px `#D9D7CF`, 4-px radius, 16-px padding. Title 16-px / 600 + version chip (mono 11-px in green-100 plate). Body 13-px ink-2. Footer: mono 12-px ink-3 last-change date + conformance badge (green / amber / red by threshold)."

### Iteration guide
1. **Density is the default.** 13-px body in tables, 44-px rows, mono everywhere it's an identifier.
2. **Severity by row tint, not icon.** Colourblind support is non-negotiable.
3. **Hypotheses → decision.** No decision without written hypothesis.
4. **Metadata only.** If a screen shows clinical content, it's not audit — escalate.
5. **Sign everything.** Decisions are public to the people they touch.
6. **Audit-of-audit is real.** Every query an auditor runs is logged in a separate stream.

---

## 14. Open questions

- **Inter-rater reliability.** Two auditors closing similar cases may decide differently. Do we sample for consistency? Run blind double-reviews? (Recommend yes, monthly.)
- **Auto-triage.** Should we surface ML-suggested hypotheses on the case detail? The hypotheses card today is human-written. Auto-suggestions risk anchoring bias.
- **Public transparency report.** Are aggregated audit numbers published quarterly? The platform supports this; it's a policy decision, not a design one.
- **Patient-flagged false positives.** What happens when a patient repeatedly flags legitimate accesses (denial, confusion, mistrust)? Out of scope for v0.4 but needs a thoughtful counsellor flow.
- **Provincial SLAs.** Cabo Delgado and Niassa have lower bandwidth and fewer auditors; should SLAs there be longer rather than missed?
