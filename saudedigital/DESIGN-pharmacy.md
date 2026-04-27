# DESIGN-pharmacy.md — Surface 3 · Pharmacy System

**Status:** v0.4 · Abril 2026
**Form factor:** Browser-based. Designed-for-tablet (10″ landscape) and phone (camera). Desktop ≥1280 px also supported.
**Primary user:** Pharmacists at ANARME-licensed pharmacies (≈1 900 in country).
**Setting:** Retail counter, queue, frequent interruptions, mixed connectivity.

---

## 1. Product purpose

Move a patient from "I have a QR code" to "I have my medicine" in under 90 seconds. The pharmacy system is the most time-pressured surface in the platform, so the design prioritizes **speed at the counter** and **traceability after the fact**, in that order.

The system also enforces three policy goals:
1. **Authentic prescriptions only** — every QR is verified against MISAU's prescription registry before dispense actions are exposed.
2. **Stock truth** — partial dispense is a first-class flow because rotures are common; patients are notified to return.
3. **Controlled-substance accountability** — Tabela II dispenses require dual confirmation and feed a digital narcotics log.

---

## 2. Information architecture

```
Sign in (pharmacy + ANARME number + PIN) → Home (Dispensar)
└─ Home
   ├─ Câmara/QR scan area (primary)
   ├─ Manual entry (numeric keypad)
   └─ Recent dispenses (this hour)
└─ Rx Detail
   ├─ Items + dosage + stock per item
   ├─ Patient + prescriber + facility metadata
   └─ Actions: Iniciar dispensa · Sinalizar suspeita
└─ Dispense (3 steps: items → lot/exp → confirm)
└─ Complete (success + next action)
└─ Controlled-substance gate (2-step PIN flow)
└─ Suspicious flag (modal)
└─ Daily summary (KPIs, top meds, restock)
└─ History (today's dispenses, status)
```

A persistent **top bar** carries the brand, primary nav (Dispensar / Fila / Histórico / Resumo), connectivity pill, and identity badge with ANARME licence.

---

## 3. Critical flows (8)

### F1 — Sign in
Pharmacy → ANARME number → PIN. Pharmacy choice is sticky for the shift; PIN auto-locks after 10 min idle. Sign-in opens a "shift" record that stamps every dispense with the operator and is closed at end-of-day from the Daily summary.

### F2 — Scan / manual entry
The home screen is dominated by a dark-green scan area with a live camera preview frame and clear instruction copy. A secondary action opens a numeric keypad modal for manual code entry (used when the patient received the code by SMS).

### F3 — Rx detail
Three-column information: items (with dosage and live per-item stock), patient, prescriber + facility + validity. Receita ID and validity are first-class badges in the title. A blue "Verificação MISAU" strip confirms authenticity. Two CTAs: amber "Sinalizar suspeita" and primary "Iniciar dispensa".

### F4 — Dispense (3 steps)
Step 1 confirms which items are being dispensed (out-of-stock items are pre-set to "no" and tinted amber). Step 2 captures lot and expiry per dispensed item. Step 3 is the irreversible confirmation: identity check + counselling check + (when partial) explicit acknowledgement that the patient is notified to return.

### F5 — Partial dispense
A first-class branch, not an error. When stock = 0 for any item, the row tints amber, the item is excluded by default in step 1, and the confirmation copy makes it clear the patient is notified by SMS to return. Dispensing other items still updates the prescription state to "Parcialmente dispensada".

### F6 — Complete
A clean confirmation card: green check, prescription ID, time, pharmacist, and clear next action ("Voltar à fila"). A subtle "ainda assim sinalizar" link is offered for 60 seconds after — pharmacists sometimes want to flag *after* dispensing.

### F7 — Suspicious-flag modal
Reason select (5 choices), free-text description, "Bloquear esta receita até revisão" toggle (default on). Submitting sends to the pharmacy director, the prescriber, and the MISAU audit team. Copy explicitly states that false flags are themselves audited — to discourage misuse.

### F8 — Controlled-substance gate
Two steps: identity verification (BI physically checked), then PIN confirmation by the responsible pharmacist (named, ANARME-licensed). Lot, expiry and quantity captured. The dispense feeds the pharmacy's digital narcotics log (Tabela II), with running balance shown in the right column.

### F9 — Daily summary
KPIs (receitas, itens, controladas, tempo médio na fila), top dispensed medicines, flagged events, suggested restock. "Fechar turno" closes the operator's shift record.

---

## 4. Components & patterns

| Component | Pharmacy-specific notes |
|---|---|
| **Scan area** | Dark green panel with corner brackets and laser line. The only screen real estate large enough to be unmissable across a counter. |
| **Manual keypad** | 12-key numeric pad with `-` and backspace. Triggers from a secondary button to keep the scan path primary. |
| **Item row** | 5-column row: check, name+qty+form, dosage/lot/expiry (state-dependent), stock, status. Out-of-stock rows tint amber and are non-interactive. |
| **KPI strip** | 4 panels at top of Home and Summary. Numbers oversized to read from across the counter. |
| **Two-step confirmation** | Mandatory for dispense and controlled flows. "Confirmar dispensa parcial" copy is explicit — the operator knows it's irreversible from this UI. |
| **Suspicious flag modal** | Always tinted amber. Submission emits to three audiences. |
| **Recent-dispenses list** | 5-column row with prescription ID (mono), patient, items count, time, status badge. |

---

## 5. Speed budget & interaction notes

- Counter target: **scan to "complete" in ≤ 30 seconds** for a 1-item dispense; ≤ 90 s for a 3-item dispense.
- Keyboard-friendly: `Enter` advances every step; `Esc` cancels and returns to scan.
- Numeric keypad sized for single-thumb use on a tablet camera.
- Lot/expiry fields autofill from the last dispense of the same lot to reduce typing; mono font for trace clarity.
- Identity check checkbox is opt-in, but the confirm button is disabled until it's checked — no accidental dispenses.

---

## 6. Stock & sync

- Item-level stock comes from the pharmacy's local store, synchronized to MISAU twice daily.
- A roture flips the row to amber and the prescription to partial. Restock suggestions surface in the Daily summary.
- Suggested-pharmacy hint on the patient app (eHealth F7) is informed by stock; that signalling is asynchronous and best-effort.

---

## 7. Audit & accountability

- Every dispense is signed by the operator (ANARME number) and the shift record (pharmacy + start/end).
- Controlled substances feed the digital narcotics log with running balance, conciliated monthly.
- Suspicious flags route to the audit surface (S4) and feed the "patient-flagged events" + "anomaly" queues there.
- The patient is always notified by SMS for: dispense complete, partial dispense, flagged prescription. Notification copy is templated and ≤160 chars.

---

## 8. Visual theme & posture (Pharmacy)

The pharmacy surface is **a counter tool, not a workstation**. References while drafting: airline check-in counters, parcel-delivery scanners, supermarket POS in low-volume mode. Anti-references: e-commerce admin dashboards, fintech "send money" UIs.

The dominant visual is the **scan area** — a dark `green-900` (`#0F3D27`) panel with bright corner brackets and a soft laser line. It dominates the screen because it is the action 95% of the time. Everything else is restrained chrome.

KPI numerals are oversized (40–48 px) to be readable from the patient's side of the counter. Item rows are 56-px (taller than EMR's 48-px) because pharmacists are often standing and reading at arm's length. Status badges are amber-heavy because **partial dispense is the common case, not the exception** — almost every prescription in rural pharmacies has at least one out-of-stock item.

---

## 9. Component stylings (Pharmacy)

### Scan area
- Full-width inside the home content zone, 320–400 px tall.
- `green-900` (`#0F3D27`) fill with a subtle 4-px inner border in `green-700`.
- Four 32-px corner brackets in white, 3-px stroke.
- A 1-px white laser line at vertical center, 60% opacity.
- Title above scan area: 20-px / 600 ink "Apontar para QR da receita". Helper: 14-px ink-2 "Ou inserir código manualmente".
- Below scan area: secondary `lg` button "Inserir código manualmente" — keypad icon left, label centered.

### Manual keypad modal
- 360-px width centered modal, white surface, 6-px radius.
- 3 × 4 keypad: digits 1–9, then `-` (for hyphenated codes), `0`, backspace.
- Keys 64-px square, 1-px `#D9D7CF` border, 4-px radius, 24-px / 500 mono.
- Display field above keypad: 56-px tall, mono 28-px, ink, right-aligned.

### Item row
- 56-px row, 1-px bottom hairline.
- Columns: 24-px check · name + form + qty (14-px / 500 ink, 12-px / 400 ink-3) · dosage / lot / expiry (state-dependent, 13-px mono when set) · stock indicator · status badge.
- **Out-of-stock state:** row fill `#FFFBEF`, amber-500 left edge accent (3 px), check disabled, status badge "Sem stock".
- **Partial state:** check unchecked by default, status badge amber "Excluir da dispensa".

### KPI strip
- 4 panels, equal width, 12-px gap.
- Each panel: white surface, 1-px `#D9D7CF` border, 4-px radius, 16-px padding.
- Overline 11-px / 600 / 0.06em UPPERCASE in ink-3.
- Number: 40-px / 600 ink (48-px on Daily summary).
- Caption: 12-px ink-3.

### Confirmation step (dispense)
- Two-column layout inside a 720-px modal (exception to 520 default).
- Left: read-only summary of items + lot/expiry + patient.
- Right: identity check (checkbox + 14-px label), counselling check (checkbox + 14-px label), partial-dispense acknowledgement (only if partial), `xl` primary "Confirmar dispensa".
- Confirm button **disabled until both checks are ticked** — disabled state is `bg-2` with ink-4 label.

### Suspicious-flag modal
- 520-px width, white, 1-px `#D9D7CF`, 6-px radius.
- Title 18-px / 600 ink "Sinalizar suspeita".
- Subtitle 13-px ink-2 "Apenas use em caso de receita suspeita. Falsos sinais são auditados."
- Reason select (5 options), free-text 4-line textarea (max 280 chars).
- Toggle "Bloquear esta receita até revisão" — default ON, 14-px label, 22-px switch.
- Footer: secondary "Cancelar" left, danger "Submeter sinalização" right.

### Controlled-substance gate
- Step 1: identity verification — BI physical-check checkbox, 14-px label "Verifiquei o BI físico do utente".
- Step 2: PIN — 4-digit numeric input, 56-px tall, mono 28-px, centered. Pharmacist name and ANARME number rendered above as static text.
- Right column throughout: digital narcotics log preview (Tabela II) — running balance in mono.

### Recent-dispenses row
- 48-px row, 5 columns: prescription ID in mono 13-px / 500 / blue-700 · patient name 14-px / 500 ink · items count 13-px ink-2 · time 12-px ink-3 · status badge.

---

## 10. Layout & spacing (Pharmacy)

- Top bar 56 px, identity badge includes ANARME number in mono.
- Content max-width 1280 px on desktop; full-bleed on tablet.
- Home: scan area dominates 60% of viewport; KPI strip above; recent dispenses below.
- Modals are wider (520 → 720 for the dispense confirm) because pharmacists need more side-by-side context.
- Section spacing 16 px; KPI panels 12-px gap.

---

## 11. Do's and Don'ts (Pharmacy)

### Do
- Make the **scan area visually dominant**. It's the primary action 95% of the time.
- Treat **partial dispense as a first-class flow**, not an error. Status badge amber, not red.
- Always require **two checks** (identity + counselling) before the irreversible confirm.
- Capture **lot and expiry per dispensed item** in mono for trace clarity.
- Show **stock per item live** on Rx detail, with the per-item icon.
- Send **SMS notification to patient** for every dispense outcome, including partial.
- Surface **digital narcotics log preview** during controlled-substance flows.

### Don't
- **Don't allow dispense without QR verification.** Manual entry is allowed but goes through the same MISAU verification strip.
- **Don't display patient clinical notes.** Pharmacy sees prescriber metadata only — not the encounter SOAP.
- **Don't let an out-of-stock item silently fail.** Tint amber, set status, exclude from dispense, surface in Daily summary as restock.
- **Don't auto-cancel idle sessions** mid-dispense. Lock after 10 min of true idle, but never inside an active flow.
- **Don't route flags only to the prescriber.** Pharmacy director + prescriber + MISAU audit always.

---

## 12. Responsive behaviour (Pharmacy)

| Width | Treatment |
|---|---|
| ≥ 1280 px (desktop) | Top bar + content. KPI strip 4-up, scan area 60% width with sidebar of recent dispenses. |
| 1024–1280 px | Same layout, KPI strip 4-up, recent dispenses below scan area. |
| 768–1024 px (tablet 10″ landscape) | KPI strip 4-up, scan area full-width, recent dispenses below. |
| 600–768 px (tablet 7″ landscape) | KPI strip 2-up (2 rows), scan area full-width, recent dispenses scroll. |
| < 600 px (phone) | Phone is a **camera-only mode**. Scan + manual entry only; recent dispenses hidden. The full app requires tablet+. |

**Camera-permission denied state.** Render an empty-state card in place of the scan area: square placeholder mark, headline "Câmara bloqueada", body "Pode abrir as definições do navegador ou inserir o código manualmente.", primary action "Inserir código manualmente".

---

## 13. Agent prompt guide (Pharmacy)

### Component prompts
- **Scan area:** "Full-width, 320-px tall, `#0F3D27` fill, 4-px inner `#1B5E3F` border. Four 32-px white corner brackets with 3-px stroke. 1-px white laser line at vertical center, 60% opacity. Title above: 20-px / 600 ink. Helper: 14-px / 400 ink-2."
- **Item row (in-stock):** "56-px row, white fill, 1-px bottom hairline `#D9D7CF`. Check 24-px left. Name 14-px / 500 ink, form + qty 12-px ink-3 below. Dosage / lot / expiry in mono 13-px. Stock indicator (right). Status badge."
- **Item row (out-of-stock):** "Same as in-stock but: row fill `#FFFBEF`, 3-px `#C8911E` left edge, check disabled, status badge amber 'Sem stock'."
- **KPI panel:** "White, 1-px `#D9D7CF`, 4-px radius, 16-px padding. Overline 11-px / 600 UPPERCASE / 0.06em ink-3. Number 40-px / 600 ink. Caption 12-px ink-3."
- **Confirmation modal:** "720-px wide, white, 1-px `#D9D7CF`, 6-px radius. 2 columns. Right column: identity + counselling checkboxes, partial-dispense ack if applicable, `xl` primary button disabled until both checks ticked."
- **Suspicious-flag modal:** "520-px wide. Title 18-px / 600 ink. Subtitle 13-px ink-2 with 'Falsos sinais são auditados.' explicit. Reason select, 280-char textarea, ON-by-default block toggle. Footer: secondary 'Cancelar' + danger 'Submeter'."

### Iteration guide
1. **Speed at the counter is the metric.** Every additional click on the dispense path must be justified.
2. **Out-of-stock is amber, not red.** Red means "do not dispense"; amber means "this item is excluded but the rest proceeds".
3. **Two-check gate is non-negotiable.** Identity + counselling before confirm.
4. **Lot + expiry in mono.** Pharmacists scan strings; mono helps.
5. **Recent dispenses visible at all times** — the pharmacist's working memory of the last hour.

---

## 14. Open questions

- **Cash & insurance integration.** Out of scope for this MVP — but the system already records itemised dispenses, so cash registers can hook in later.
- **Multi-pharmacist counter.** Today the shift is single-operator. Some larger pharmacies have parallel counters; we'd need parallel shift records.
- **Offline counter.** Pharmacy offline behaviour is undefined here; current scope assumes connectivity is acceptable in urban pharmacies. Rural deployment will need a queue-and-sync model similar to EMR.
- **Returns / reversal.** A patient returns expired medicine — no flow yet. Likely a v0.5 addition.
- **Camera permission denial.** UX when camera is blocked needs a designed empty state directing to manual entry; partial today.
