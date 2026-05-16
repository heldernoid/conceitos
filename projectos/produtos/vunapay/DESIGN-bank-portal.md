# DESIGN-bank-portal.md - VunaPay

**Status:** v0.1
**Screens:** Dashboard, Transactions, Participants
**Surface:** Bank admin web
**Primary users:** Compliance officers, operations and treasury staff at participating banks. Secondary: regulators with read-only access.
**Form factor:** Desktop, 1280px design width, sticky-sidebar layout that collapses to a single column under 1100px.

## 1. Purpose

The bank portal is the operational nerve centre that participating banks use to monitor their flows on the VunaPay network - to confirm settlement is working, to reconcile in real time, to investigate exceptions, and to demonstrate compliance to internal and external auditors. Where the consumer app is about a single transfer's certainty, the portal is about the aggregate health of thousands per minute. The same green-and-gold tokens carry through, but density is much higher and the typography leans on JetBrains Mono for every numeric column so eyes can scan figures fast.

## 2. Information architecture

A persistent left sidebar holds the brand mark, the bank name ("Banco de Beira · Portal"), seven nav items (Visão geral, Transações, Bancos participantes, Liquidação, Disputas, Relatórios, Definições), and a footer block with the signed-in user's name, role, and the theme toggle. The main pane carries a header (page title, contextual subtitle, page-level actions) and then page-specific content.

**Dashboard** stacks four KPI cards (transactions today, volume today, average settlement time, success rate), a 2/3-column charts row (7-day volume bars + settlement-time histogram), and a live transaction feed table with eight rows that subtly pulse to signal liveness.

**Transactions** is a two-column layout: a 260px sticky filter panel on the left (date range, direction, status checkboxes, counterparty bank checkboxes with colour dots, amount range, apply/clear) and a results pane on the right with a summary bar, a table of expandable rows, and pagination at 50 per page.

**Participants** opens with a network-status banner, then a 2-column card grid of all 8 banks (each with colour accent, status badge, four KPIs, BIC code), and a sticky right-column health card showing pairwise latency in an 8×8 matrix plus an active-incident card.

## 3. Critical flows

**F1 - Spot a problem.** From the dashboard the user sees the success rate dip and a critical-tinted row in the live feed. They click into transactions, filter by status=Falhada, expand the failed row to read the central-clearing signature and the per-leg timing, then assign it to the disputes queue.

**F2 - Reconcile a counterparty's day.** From participants the user clicks "Ver transações" on a bank's card, landing in transactions pre-filtered to that counterparty. The summary bar shows the filtered total volume which they cross-check against the counterparty's own report.

**F3 - Export for audit.** With filters applied, the user uses Exportar CSV (full row data) or Exportar PDF (summary + first 200 rows + central-clearing signatures) from the page header.

**F4 - Track an incident.** On participants the user sees BDT in the warn state. The incident card explains the SLA breach and the timeline of escalation. Clicking the bank card opens BDT's detail view with the historical latency chart.

## 4. Components &amp; patterns

| Element | Component | Notes |
|---|---|---|
| Sidebar | Sticky 248px column with brand, nav-items, user footer | Active state uses brand-subtle background. |
| KPI card | `.stat-card` with mono value + coloured trend | Trend arrow + delta + comparison period. |
| Bar chart | Hand-rolled CSS grid of bars | Today is brand-2; weekend bars dim to ink-4 to imply lower volume is expected. |
| Histogram | 8-bucket distribution | Median and P99 callouts under the chart in mono. |
| Live table | `.tbl` with bank logos in the De/Para columns | Top row pulses; status badges colour-coded. |
| Filter panel | Sticky left column with sectioned controls | Counterparty list uses 8px colour dots so the visual mapping matches the bank cards on the participants screen. |
| Expandable row | Click to reveal full account numbers, phones, note, central-clearing signature | Compliance staff need raw numbers, but they live one click deeper than the default scan. |
| Pagination | Mono numbers + chevrons | 50 / page is the default; matches typical reconciliation batch size. |
| Bank card | Colour-accent strip + logo + KPI 2×2 + footer link | Status badge sits in the head row, BIC in the footer. |
| Health matrix | 8×8 grid of latency cells | Cells coloured against a 2.5s / 5s threshold. |
| Incident card | Warn-tinted with icon + plain-language explanation | Always names which bank, what's wrong, when it was detected, and the next step. |

## 5. States &amp; edge cases

When the network is degraded (one or more banks in warn or down) the network-status banner switches from green to warn or critical and the failing bank's card gets the matching badge. When filters return zero rows the table shows a centred empty state with an action to clear filters. When the user lacks export permission the export buttons are disabled with a tooltip explaining the missing role.

## 6. Copy &amp; content rules

Portuguese is primary, with English acceptable for technical financial terms (BIC, P99). Plain words, no jargon: "liquidada" for settled, "tempo médio" for average settlement time, "tempo limite" for timeout, "operacional" for healthy. Times and IDs are always mono. Currency follows MZN format (`1.500,00`); large totals abbreviate to millions with a comma decimal (`MZN 11,2M`).

## 7. Responsive behaviour

Above 1100px the sidebar is sticky and the two-column layouts hold. Below 1100px the sidebar collapses to a top bar with a hamburger and the content panes stack vertically; tables become horizontally scrollable rather than reflowing.

## 8. Accessibility notes

All status colours are paired with an icon and text label. The live feed's pulse animation respects `prefers-reduced-motion`. Bank colour dots in the filter list are decorative; the bank name is the screen-reader value. The latency matrix is supplemented with a hidden `<table>` of the same data for screen-reader users.

## 9. Open questions

Whether the live feed should be driven by Server-Sent Events vs WebSocket is open; both are proven for this density. Whether to allow PDF export of expanded rows (i.e. every transaction's full detail) is open; current direction is no by default for performance - provide a "Exportar com detalhes" toggle that warns about file size.
