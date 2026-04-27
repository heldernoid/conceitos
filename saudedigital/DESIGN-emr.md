# DESIGN-emr.md — Surface 1 · Clinician EMR

**Status:** v0.4 · Abril 2026
**Form factor:** Web app on 7″ Android tablet (landscape, 1024×600 floor) and desktop browser (1280+).
**Primary users:** Enfermeiros, técnicos de medicina, médicos. Secondary: directores clínicos.
**Setting:** Centros de Saúde, Hospitais Distritais, Hospitais Provinciais — variable connectivity.

---

## 1. Product purpose

A single national clinical record. Every encounter, every prescription, every lab result attached to one patient identity, accessible at any facility on the network. Offline-first because the network is not always there.

The EMR optimizes for three things, in this order:
1. **Identifying the right patient quickly** — by BI, DIRE, phone, name or temporary code.
2. **Producing a clean clinical record** — chief complaint → vitals → diagnosis → plan → SOAP → signature.
3. **Issuing a prescription that can be dispensed anywhere** — QR-coded, validated, audited.

It deliberately does *not* try to be a billing system, a hospital ERP, or a research platform. Those are downstream of SIS-MA.

---

## 2. Information architecture

```
Sign in (email + password) → Facility selector → Dashboard
└─ Dashboard
   ├─ Sala de espera (today's queue, triage colour, status)
   ├─ Resultados de lab (unread first)
   └─ Alertas clínicos (stock, surveillance, override pending)
└─ Pacientes / Pesquisar
   ├─ Resultado · abrir Patient profile
   ├─ Sem resultado → Criar registo temporário
   └─ Aviso de duplicação → Fundir registos
└─ Patient profile
   ├─ Visão geral · Histórico · Medicação · Lab · Acessos
   ├─ Iniciar consulta (Encounter wizard)
   └─ Override de emergência (justification flow)
└─ Encounter wizard (5 steps) → Prescribe modal (2 steps) → Sign + sync
└─ Estado offline (sync queue, available data, retry)
```

A persistent **top bar** carries: brand, primary nav, connectivity pill, identity badge. Identity is always one click from sign-out and facility switch.

---

## 3. Critical flows

### F1 — Sign in & facility selection
Two-step, deliberately separate. Step 1 authenticates the operator. Step 2 binds the session to a facility (a clinician's authority is facility-scoped). Selection persists for the shift; switching is one click and re-authenticates.

### F2 — Dashboard (today)
Above the fold: today's queue (default sort by triage, then arrival), unread lab results, and clinical alerts. Four KPI cards: patients today, red triage count, lab results count, sync state. The sync KPI is *not* hidden in chrome — it is a primary card.

### F3 — Identify patient
Search supports four input types via segmented control: BI, telephone, name, temporary code. Camera-read of BI is a shortcut for tablets. **No-document path:** if the operator has nothing to type, they create a `TMP-YYYY-NNNN` temporary record from the empty state. The system never blocks treatment for lack of paperwork.

### F4 — Patient profile
Five tabs (Overview, History, Medication, Lab, Access). Overview is the daily working view: vitals, chronic conditions, allergies (red badge in the header), recent access trail (so the clinician sees what the patient sees). The access tab is the same data as in the patient app, surfaced here so clinicians remember they are visible.

### F5 — New encounter
A 5-step wizard: Queixa → Vitais → Diagnóstico (CID-10) → Plano → SOAP. Each step saves a draft locally. The CID-10 picker shows code, label, and any clinical reminder ("Confirmação por TDR obrigatória antes de ACT"). Drafts persist across sessions and across offline periods.

### F6 — Issue prescription
Modal launched from the encounter (or stand-alone). Two steps: compose (search + dosage + duration + route, with interaction/allergy check) and review (QR preview, validity, prescriber, options to SMS the patient and/or surface the QR in the eHealth app). Signing emits `Rx-YYYY-MM-MZ-NNN` and queues for SIS-MA.

### F7 — Merge temporary into BI
Side-by-side compare with the BI record marked as the **winner**. A match score (telephone, DOB, district, surname, sex). Mandatory operator confirmation that they verified identity in person. Action is irreversible from the UI; reversal requires MISAU support.

### F8 — Offline state
Dedicated screen, but offline state is also indicated in the top-bar pill at all times. Lists the pending sync queue (type, patient, detail, time, status), what data is available offline (last 90 days of facility patients, 12-month prescription history, ICD-10 + medicines catalogue), and what is not (national BI search, cross-facility labs, video consult).

### F9 — Emergency override
Used when the patient cannot consent (unconscious, mass casualty). Two-step: justification (≥80 chars, witness selection, type of emergency, acknowledgement of patient notification) and confirmation. Access is granted for 24 h, fully recorded, the patient is notified by SMS, and the facility director plus MISAU review.

---

## 4. Components & patterns

| Component | EMR-specific notes |
|---|---|
| **Top bar** | Always shows facility name as part of the brand stack. Facility = authority. |
| **Connectivity pill** | Three states (`ok`, `syncing`, `offline`). Offline shows queue length. |
| **Patient queue table** | 8-column row: avatar, name+district, doc (mono), age, symptom, triage badge, status, action. Triage colour is the avatar tint as well as the badge. |
| **Encounter stepper** | Linear, but step jumps are allowed once previous steps have data. Draft auto-saves every change. |
| **CID-10 picker** | Code in mono blue, label, optional clinical note. Suggestions ranked by frequency at this facility this season. |
| **Prescription modal** | Right column shows live QR preview at step 2 — the same QR rendered in the eHealth app and scanned at the pharmacy. |
| **Merge view** | Three-column grid: temp / arrow / BI (winner outlined in green). Match-rule list below. |
| **Override banner** | Always red, always at top, never collapsible during the flow. |
| **Empty / offline / error states** | Designed: every list has a one-line headline + sentence + suggested action. Offline is a *first-class screen*, not an error. |

---

## 5. Connectivity & sync model

The EMR is a thick client. Changes are written to a local store, replayed to the server, and acknowledged. The UI surfaces three states only: synced, syncing-with-queue-length, offline-with-queue-length. Conflicts (rare; mostly clinical notes amended at two facilities) surface in a dedicated screen with side-by-side compare; current scope shows the queue but not yet conflict resolution.

Available offline (last 90 days):
- All patients seen at this facility
- Their prescriptions (active + 12-month history)
- ICD-10 catalogue (full)
- Medicines catalogue (MISAU formulary)
- This clinician's drafts

Not available offline:
- National BI/DIRE lookup
- Cross-facility lab results
- Video consultation
- Inter-facility transfers

---

## 6. Accessibility & performance

- Tablet floor: 7″ landscape (1024 × 600). All flows tested at this floor.
- Touch targets ≥44 px. Patient queue rows are 48 px to accommodate gloved fingers.
- Keyboard: full navigation. Encounter wizard uses `Ctrl+S` (save draft) and `Ctrl+→` (next step).
- High contrast: body text is `ink` on `bg`, ratio > 12:1.
- No information by colour alone — every triage and status pill carries a word.

---

## 7. Visual theme & posture (EMR-specific)

The clinician surface reads like a **specialist tool, not a portal**. Information density is high, decoration is absent, and every pixel is earning its place. References while drafting: Epic Hyperspace (target: less hostile), Cerner PowerChart (target: cleaner), DHIS2 (target: warmer). Anti-references: any consumer "wellness" app, any modern fintech dashboard.

The EMR is the only surface where **density is a virtue**. A 7-inch tablet held by a nurse triaging in a corridor must show the patient queue, the triage colour distribution, the lab inbox, and the connectivity state on a single screen. We achieve this through tighter row heights (44 px in tables vs the 48 px floor used elsewhere), 13-px body type in lists, and zero decorative whitespace inside data zones.

The dominant chrome colour is `bg-2` (`#F2F1EB`) used for table headers and group rows — a half-step warmer than the page background. Brand green appears only in: primary actions, the avatar plate of the active patient, and the connectivity pill in its synced state. Triage colour is the strongest non-brand signal on screen and is **always** rendered as both a coloured dot and a written word ("Vermelho").

---

## 8. Component stylings (EMR)

### Patient queue row
- 48-px height (gloved-finger floor), 1-px bottom hairline, hover `bg-2`.
- Columns: 32-px avatar plate (triage-tinted) · name + district stack · BI/DIRE in mono · age · presenting complaint truncated at 40ch · triage badge · status · action button.
- On row hover the entire row is the click target; the action button is keyboard-focusable separately.

### Encounter stepper
- 5 steps, horizontal, 56-px tall band.
- Active step: green-700 number plate, ink label.
- Completed step: green-100 plate, green-700 check mark, ink-2 label.
- Pending: line-bordered plate, ink-3 label.
- Step jumps allowed only once a step has draft data; otherwise the chip is non-interactive (cursor: not-allowed).

### CID-10 picker
- Combobox, 44-px input, 13-px mono code in blue-700, 14-px sans label, optional 12-px ink-3 clinical note row underneath.
- Suggestions ranked by frequency at this facility this season; sentinel suggestions ("Confirmação por TDR obrigatória antes de ACT") render with a 12-px amber leading mark.

### Prescription modal (2-step)
- 720-px width, exception to the 520 modal default — a prescription needs side-by-side review.
- Step 1 (compose): two-column. Left = inputs. Right = live interaction/allergy panel.
- Step 2 (review): two-column. Left = read-only summary. Right = **live QR preview** (the same QR that renders in the patient app and scans at the pharmacy).
- Sign button is `lg` (44-px) primary; cancel returns to step 1.

### Override banner
- Full-bleed red (`#FCEFEC` bg, `#E5B7AE` border, `#C2392A` ink), 12-px padding.
- Always at top of the patient profile during an active override window.
- Includes countdown to expiry (mono) and a "Encerrar override" link aligned right.

---

## 9. Layout & spacing (EMR)

- Top bar 56 px (vs 60 px on patient app — clinicians need vertical real estate).
- Sidebar 264 px — wider than audit (220) because patient names and facility names are long.
- Content max-width: full-bleed inside the 1440-px container; tables stretch.
- Section spacing inside patient profile: 24 px between cards, 16 px within.
- Form rows: 12 px vertical gap, 16 px between fieldsets.

---

## 10. Do's and Don'ts (EMR)

### Do
- Treat **identity verification as a flow, not a field**. BI / DIRE / phone / name / temp code is a segmented control on the search surface.
- Show **draft state on every encounter step** — clinicians are interrupted constantly; "Rascunho guardado às 14:32" is non-negotiable.
- Surface the **patient's access trail** inside the EMR profile, not only in the patient app. Clinicians must remember they are visible.
- Render **prescription QR preview live** on step 2 of the modal — what they sign is what dispenses.
- Allow **temporary records** (`TMP-YYYY-NNNN`) from any empty search state. Treatment never blocks on documentation.
- Allow **offline drafting** of every clinical note, prescription, and SOAP. Local first, sync when possible.

### Don't
- **Don't gate clinical actions on connectivity.** Drafting, signing-locally, queueing — all offline-capable.
- **Don't hide the override banner** — it must be visible for the entire 24-h window.
- **Don't auto-merge records.** Merging is a deliberate two-person verification step.
- **Don't display lab result trends as sparklines** in v0.4 — single-value display only until clinical sign-off.
- **Don't show billing fields** anywhere. Out of scope.
- **Don't allow facility switching mid-encounter** without saving the draft and warning.

---

## 11. Responsive behaviour (EMR)

| Width | Layout |
|---|---|
| ≥ 1280 px | Sidebar 264 + content. Patient profile 3-column (sidebar nav, primary, summary aside). |
| 1024–1280 px | Sidebar 264 + content. Patient profile 2-column (primary + summary aside). |
| 840–1024 px (tablet 10″ landscape) | Sidebar collapses to 60-px icon rail. Patient profile 2-column. |
| 640–840 px (tablet 7″ landscape — **floor**) | Sidebar in drawer. Patient profile 1-column with sticky tab bar. Tables compress to 6 columns max; secondary columns become a tap-to-expand row. |
| < 640 px | Not supported in v0.4. Sign-in works; clinicians redirected to "Use a tablet". |

**Touch behaviour.** Every row is its own hit target on tablet; mouse cursors get a precise hit target on the action button only. Long-press on a queue row opens the patient profile.

---

## 12. Agent prompt guide (EMR)

### Component prompts
- **Patient queue row:** "48-px row, 32-px avatar plate tinted by triage colour, name (14-px / 500) + district (12-px / 400 / `#5E5E5E`) stack, BI in Plex Mono 13-px, triage badge, status badge, primary `sm` action button right-aligned. 1-px `#D9D7CF` bottom hairline. Hover `#F2F1EB`."
- **Encounter step chip:** "44-px circle plate (green-700 active / green-100 completed / line-bordered pending), 14-px label below. Connector hairline `#D9D7CF` between chips."
- **CID-10 row:** "13-px mono code in blue-700, 14-px label, optional 12-px clinical note in ink-3. Hover `#F2F1EB`. Sentinel notes prefixed with 12-px amber square mark."
- **Prescription preview QR:** "180-px square white card, 1-px `#D9D7CF` border, 4-px radius. QR is a flat black-on-white SVG placeholder. Below QR: prescription ID in mono, validity, prescriber name + role."
- **Override banner:** "Full-bleed `#FCEFEC` background, `#E5B7AE` 1-px border, 4-px radius, 12-px padding. Title in `#C2392A` 14-px / 600. Countdown mono right-aligned. 'Encerrar override' link in blue-700."

### Iteration guide
1. Open every patient screen with a **clear identity stack** (name + age + district + BI in mono) before any clinical content.
2. Triage colour appears as **avatar tint + badge + word** — never colour alone.
3. Drafts auto-save and **say so** with a meta line.
4. Two-step confirmation for prescribe, merge, override — **always**.
5. Connectivity pill present in top-right, always.

---

## 13. Open questions

- **Triage taxonomy.** Manchester 4-tier in EMR, simplified for the patient app — needs sign-off on mapping.
- **Lab integration.** Today the EMR lists results but does not display result trends; deferred to v0.5.
- **Inter-facility transfers.** A patient referred from CS Maxixe to HP Inhambane should auto-share the active encounter; not in this prototype.
- **Print receipts.** Physical printout of the prescription for patients without phones — design pending.
- **Multi-facility clinicians.** Some doctors rotate between three facilities — how the session model handles this is open.
