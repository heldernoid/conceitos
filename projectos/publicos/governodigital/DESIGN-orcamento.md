# DESIGN-orcamento.md — Surface 4 · Orçamento Aberto

**Status:** v0.3 · Abril 2026
**Form factor:** Web (responsive desktop + mobile). Public-facing — no authentication.
**Primary users:** Cidadãos, jornalistas, organizações da sociedade civil (CIP, OXFAM-MZ, MISA), auditores externos, parlamentares.
**Setting:** Browser, on any device. The lowest-bandwidth path is critical because rural users still need access.

---

## 1. Product purpose

A public window into how the Mozambican State raises and spends money. Three jobs, in order:

1. **Show the totals** — receita do Estado, despesa, défice, projecções por ano fiscal, em MZN.
2. **Make execution visible** — by sector, by province, by month — so a citizen, a journalist, or an auditor can see whether the OE is being executed as voted.
3. **Open the contract layer** — every public contract above MZN 5 milhões in a searchable, downloadable, citable ledger. Click → see the contract, the sector, the procurement procedure, the supplier, the values, the addenda.

It deliberately does *not* try to be: a financial dashboard for ministry staff (those are SISTAFE views), an investment-attraction site for foreign capital, or an editorial platform.

---

## 2. Information architecture

```
Hero · totais OE 2026
└─ Execução do Estado
   ├─ Por sector (12 sectores)
   ├─ Por província (11 províncias)
   └─ Por classificação económica (despesa corrente / investimento / dívida)
└─ Receita
   ├─ Impostos · IRPS · IRPC · IVA · ICE
   ├─ Royalties (gás, carvão, mineração)
   └─ Doadores e créditos externos
└─ Contratos públicos
   ├─ Lista (filtros: sector · província · valor · ano · estado)
   ├─ Detalhe do contrato
   └─ Reportar irregularidade
└─ Dados abertos
   └─ CSV · JSON · API (todos os endpoints públicos)
└─ Sobre & metodologia
```

Public site uses the standard top bar with no login affordance. Footer carries: methodology link, data sources, last-updated timestamp, contact (UGD + IGF).

---

## 3. Critical flows

### F1 — Visão geral
Hero with the headline numbers: receita arrecadada vs orçamentada, despesa executada, défice, taxa de execução global. Below, the sector view by default — citizens want to see "where is my money going?"

### F2 — Execução por sector
12 sectors as a sortable table with execution bars. Sectors over-executing flagged in red; under-executing in amber; on-track in ochre (default fiscal accent). Click a sector → drill-down with monthly trend and top sub-programmes.

### F3 — Execução por província
11 provinces in a sorted list. Each shows: orçamentado, executado, %, nº de contratos públicos. Map view as a v0.4 thing — v0.3 is a list, because tables download better and read in low bandwidth.

### F4 — Contratos públicos
The "killer feature" of this surface. Searchable ledger of every contract above MZN 5 milhões. Filters: sector, province, year, supplier, value range, procurement procedure (concurso público / ajuste directo), state. Each row links to a detail page.

### F5 — Detalhe do contrato
A single page per contract with: identity (CT-YYYY-MIN-NNNN), sector, project name, supplier (NUIT, name, country if foreign), value (initial, addenda, total), procurement procedure, dates (signed, started, due), state (active / done / suspended / canceled), addenda log, payments log (where SISTAFE permits), and a *Reportar irregularidade* button.

### F6 — Reportar irregularidade
A simple form: contract reference, type of concern (controlled list), description (free text), optional contact. Submission goes to **IGF (Inspecção Geral das Finanças)** — not to UGD, not to the contracting ministry. The submitter can opt to remain anonymous.

### F7 — Dados abertos
A page listing every public dataset, with CSV, JSON, and API endpoints. Each dataset has a "snapshot ZIP" for offline analysis. License: CC BY 4.0.

### F8 — Receitas
Two views: by source (impostos / royalties / doadores) and by month. Royalties from gás and carvão are highlighted because they account for ~24% of receita and have high public interest.

---

## 4. Components & patterns

| Component | Orçamento-specific notes |
|---|---|
| Top bar | Public; no login link. "Última actualização" pinned to the right. |
| Govt strip | Includes "Dados oficiais · MEF · SISTAFE · IGF" |
| Hero numbers | Display-weight (44 px) for headlines; mono for values |
| Bar (.bar.ochre / .amber / .red) | The standard execution component on this surface |
| Filters strip | Sticky, collapses to a single button on mobile |
| Contract row | Compact: ID, sector, supplier, value, %, state |
| Contract detail | Two-column on desktop: header + addenda log |
| Empty states | "Sem contratos com estes filtros — relaxe um critério ou descarregue o dataset completo." |
| Footer | Includes methodology link and per-page "como foi calculado isto?" toggle |

---

## 5. Critical UI states

### 5.1 Sector over-executing
Red bar + a small footnote explaining over-execution can mean: budget transfer from another sector (legitimate), unforeseen expenditure (legitimate), or a procedural irregularity (audit). The site does *not* judge — it shows.

### 5.2 Sector under-executing late in the year
Amber bar; a contextual note ("MZN X mM por executar com 3 meses restantes") to invite scrutiny.

### 5.3 Contract suspended or canceled
Red badge "Suspenso" or "Anulado" with the reason from MEF where available.

### 5.4 Data lag
A persistent timestamp at the top of each page: *"Dados de SISTAFE actualizados em 03 Abr 2026 às 23:00 CAT — atraso máximo: 7 dias."*

### 5.5 Ministério recusa publicar contrato
Some contracts are flagged "ocultos por classificação de defesa". The list still shows the slot, with state "ocultado" and the legal basis (Lei N° X/Y). The user knows the contract exists even if the value is hidden.

---

## 6. Fiscal vocabulary

The Orçamento surface introduces vocabulary specific to public finance:

| Term | Meaning here |
|---|---|
| OE | Orçamento do Estado · annual budget |
| mM | mil milhões (10⁹ MZN), used for headline figures |
| Execução | What % of budgeted has been actually spent |
| Cabimentação | Reserved (committed but not paid) — rendered as a hashed bar |
| Pagamento | Effectively paid |
| Adenda | Contract amendment — listed in the detail page |
| Concurso público / Ajuste directo / Concurso limitado | Procurement procedures, badged differently |

---

## 7. Cross-system relationship

Orçamento Aberto reads from:

- **SISTAFE** (real, MEF) — receita and despesa execução
- **e-PA** (real, plataforma de aquisições) — public contracts
- **Tribunal Administrativo** — court rulings on public-contract disputes (referenced, link out)
- **IGF** — receives the irregularity reports

Orçamento Aberto does *not* call into eBI or App do Cidadão. It is the only surface in the Governo Digital family that doesn't touch the citizen identity — by design. Citizens read it without logging in; they cannot personalise it; the State cannot track readership beyond aggregate metrics.

---

## 8. Performance & low-bandwidth

- Hero loads in < 2.5 s on a 2018 phone over 3G
- Tables paginate at 50 rows; sortable client-side; full dataset always available as CSV download
- Charts deferred-load below the fold
- A "modo simples" toggle disables all charts and shows numbers only — works on the slowest connections and old devices
- All text is selectable and citable; URLs are stable and shareable (every contract has a permanent URL)

---

## 9. Accessibility

- AA+ contrast on all text
- Tables semantic with `<thead>`, `<th scope>`, captions
- Charts have a tabular alternative below
- Numbers in mono for screen-reader pronunciation control
- "Modo simples" doubles as a high-contrast / no-chart mode

---

## 10. Trust & methodology

- Every page footer carries a link to the methodology document (versioned)
- Discrepancy between OE voted and OE rectified is shown in a "Histórico do OE 2026" panel
- The site never asserts political conclusions — it shows the data and links to context (Tribunal Administrativo rulings, IGF reports, parlamentar Q&A)
- An "errata" log records corrections to historical data
- A public Git repo holds the data pipeline (referenced in the footer)

---

## 11. Open questions for v0.4

- Map view of província execution — needs a bandwidth-considered SVG strategy
- Multi-year comparisons (2024 vs 2025 vs 2026) — UI not yet drafted
- Citizen comments on contracts — risky for moderation; deferred
- Mobile detail-page format for very long contract texts (e.g. 80-page concession contracts) — current PDF-link approach is fine
- Bantu language toggle — same blocker as other surfaces

---

*This document is authoritative for the Orçamento Aberto surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins.*
