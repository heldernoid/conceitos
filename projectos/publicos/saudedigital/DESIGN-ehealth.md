# DESIGN-ehealth.md — Surface 2 · Patient eHealth App

**Status:** v0.4 · Abril 2026
**Form factor:** Android-first (Android 8+, 7-inch and below). Also functions as PWA in mobile browsers. Quadro de telefone de referência: 360 × 760.
**Primary user:** Cidadão moçambicano com smartphone. Secondary: family caregivers managing dependents. Fallback: anyone without a smartphone — addressed via USSD `*166#`.
**Setting:** Public network (Tmcel/Vodacom/Movitel), often 3G or weak signal, daylight readability required.

---

## 1. Product purpose

Three things, in this order:
1. **Lower the threshold to ask for help.** A patient with a fever should reach a nurse in under five taps without leaving home.
2. **Put the citizen in custody of their own record.** They see their consultations, their prescriptions, and — critically — every professional who has accessed their data.
3. **Be honest about reach.** Smartphone penetration is partial. The app explicitly hands users without smartphones a USSD code that does the same essential things.

The app is *not* a fitness tracker, not a wellness brand, not a marketplace. It is a public service.

---

## 2. Information architecture & navigation

Bottom tab bar, 4 items max:

```
Início    Receitas    Registo    Acessos
```

Top of every screen: a clear back affordance + screen title. Identity is implicit (whoever is signed in); a long-press on the avatar opens session, dependents, and language.

```
Onboarding  → telefone → OTP → BI/DIRE/TMP (opcional)
Início      → Pedir triagem · 4 atalhos (Receitas, Registo, Acessos, Familiares)
Triagem     → Sintomas → fila → chat → escalonamento vídeo → receita
Registo     → resumo de saúde · histórico em linguagem do cidadão
Acessos     → trilha de auditoria · sinalizar acesso
Notificações→ push & SMS · banner in-app
USSD hint   → *166# · línguas locais
```

---

## 3. Critical flows (11)

### F1 — Onboarding & identification
3 steps: phone number, OTP (6 digits), optional BI/DIRE/TMP linkage. The app **never** blocks usage on lack of BI; users without ID receive a temporary code (`TMP-YYYY-NNNN`) created by the receiving facility and surfaced here.

### F2 — Home
Greeting + name + identity line. **One primary action above the fold:** "Pedir triagem agora". Four square shortcuts to Receitas / Registo / Acessos / Familiares. Recent activity card. Connectivity surfaces only if degraded.

### F3 — Request triage
Structured chief-complaint chips + duration select + free-text + optional photo. Submitting puts the user in F4. The chip vocabulary is bounded (≈12 symptoms) — anything else goes in the textarea.

### F4 — Triage queue
Position number (very large, very calm), estimated wait, the user's submitted symptom recap, an information banner with hydration / call-1490 advice. Cancel is a secondary action at the bottom.

### F5 — Chat with nurse
Asynchronous text. Nurse identity (name, role, facility). Outbound bubbles right (green-700), inbound left (white). The nurse can send a structured **encaminhamento** card (triage colour + facility + time window) which is the green tinted bubble. Photo attachment supported.

### F6 — Escalation to video
Reached from chat when the nurse escalates. Doctor's name, role, facility, call duration. Picture-in-picture self-view. Top-left strip indicates bandwidth; if poor, an explicit "alternar para áudio?" prompt. Standard call controls: mute, switch to audio, camera, end (red).

### F7 — Receive prescription
QR-prominent. Mono prescription ID, validity badge, list of meds with dose/frequency/duration in plain language, prescriber + facility, nearest pharmacy with stock indicator. Two footer actions: share and find pharmacy.

### F8 — My health record
**Patient-friendly language**, not clinical. "Tem tensão alta controlada e diabetes tipo 2" — not "HTA + DM2". The summary card uses green tint to signal the record overview. Below it, a chronological list with relative dates ("hoje", "12 Março 2026"), what happened in plain words, and who saw them.

### F9 — Access log
The same audit data surfaced in the EMR profile. Each entry: avatar of the professional, name, role, facility, time, what they viewed. Override entries are tinted red and carry a prominent **"Não fui eu — sinalizar"** action.

### F10 — Notifications
Two channels: push (in-app banner cards on lock screen) and SMS (when the user has no data). Override notifications are tinted amber and explain the reason. Prescription notifications are SMS-friendly (≤160 chars, no diacritics).

### F11 — USSD fallback
A dedicated screen explaining `*166#` to people *with* the app, so they can show it to relatives without one. Includes the menu preview, the supported languages, and a print-card option for facility waiting rooms. Note that **`*660#` is reserved for Pensa** — we deliberately picked `*166#` to avoid collision; final code subject to ARECOM allocation.

---

## 4. Components & patterns

| Component | Notes |
|---|---|
| **Phone frame** | 360 × 760 with 28 px status bar + 60 px nav-bottom. All screens render inside it. |
| **Primary action** | Always full-width `btn xl block`. One per screen above the fold. |
| **Symptom chip** | 2-up grid of selectable cards. Selection tints green-100 with green-700 border. |
| **Chat bubble** | 14 px radius, mine right, theirs left. Structured encaminhamento card uses green-100 tint with stronger weight for the action. |
| **Access row** | Avatar + name + role/facility + time + what they viewed. Override variant uses red-100 background and surfaces the flag action. |
| **Notification card** | Mimics the OS banner (lock-screen mock). For SMS, monospace body to read "as the user receives it". |
| **Connectivity** | Lighter than clinician — only shown when degraded (banner) or as a small green pill in the home header. |
| **Language toggle** | Five rows: Portuguese (active), Changana, Macua, Sena, Ndau (label only — placeholder, not translated in this prototype). |

---

## 5. Copy guidelines

- **Patient-friendly first.** "Tensão alta", not "HTA". "Aguardando enfermeiro", not "Triage queue". Clinical names appear when essential (medication names, prescription IDs).
- **Mozambican Portuguese.** "consigo", "telemóvel", "BI", "Centro de Saúde". Avoid Brazilian PT vocabulary.
- **Calm tone.** No exclamation marks except in genuine warnings. No emojis except the camera icon in the symptom photo prompt.
- **Action verbs.** "Pedir triagem", "Confirmar", "Sinalizar".
- **SMS strings.** ≤160 chars, no diacritics, prefix `SAUDE MZ:`, end with a help command (`Resp 1 p/ ajuda`).

---

## 6. Accessibility

- Body text 16 px floor; nothing under 12 px on the phone.
- Touch targets ≥44 × 44 px, 12 px between targets in lists.
- Contrast: text on white ≥ 12:1; status pills ≥ 4.5:1.
- Screen reader: every avatar has an alt label of the person's name + role.
- Daylight: warm off-white background reduces glare vs. pure white.
- Cognitive: numbers (queue position) are oversized; one primary action per screen.

---

## 7. USSD fallback (`*166#`)

The USSD tree mirrors the app:

```
1. Pedir triagem
2. Ver receita activa
3. Confirmar consulta
4. Sinalizar acesso
5. Falar c/ enfermeiro
6. Mudar idioma
```

Each branch is plain-text Portuguese (or Changana/Macua/Sena/Ndau when the user toggles), session-state-only, and produces an SMS confirmation. USSD is the truth source for citizens without smartphones; the app screen exists so smartphone users can show it to their family.

> Code allocation. `*660#` is in use by **Pensa**; we propose `*166#` and treat that as final pending ARECOM allocation. All copy here uses `*166#`.

---

## 8. Visual theme & posture (eHealth)

The patient surface is **the warmest member of the family**. References while drafting: SNS24 mobile (PT), 1177 (SE), Aarogya Setu (IN — for SMS/USSD coexistence). Anti-references: any direct-to-consumer wellness app, any insurance-branded portal.

It must read as **public service**, not as a product. That means:
- **Greater whitespace than the clinical surfaces.** Cards breathe. The patient is anxious, not skimming.
- **Larger touch targets.** Primary actions are `xl` (56 px), block-width.
- **Patient-friendly Portuguese.** Plain words, never clinical jargon. "Tensão alta", not "HTA". "Está em recuperação", not "pós-tratamento".
- **One primary action per screen, above the fold.** Decision fatigue is the enemy.
- **Calm numerals.** Queue position is rendered at 64-px display weight 600 to feel grounded, not alarming.
- **Connectivity is gentle.** Unlike clinician surfaces, the connectivity pill only appears when state is degraded — we don't want a permanent reminder of fragility on the citizen surface.

Brand green appears on: the home greeting plate, primary actions, and the structured "encaminhamento" card from a nurse. Status colour is reserved for triage and prescription state. Photography is absent — placeholder squares throughout.

---

## 9. Component stylings (eHealth)

### Symptom chip grid
- 2-up grid, 12-px gap.
- Each chip: 64-px tall, white surface, 1-px `#D9D7CF` border, 4-px radius.
- 14-px label, 12-px helper text in `#5E5E5E`.
- Selected: green-100 fill, green-700 1-px border, green-700 label.
- Tap target floor 44 px — but visual chip is 64 to feel handleable.

### Triage queue display
- Position number 64-px / weight 600, ink, centered.
- Below: 14-px ink-2 caption "à sua frente", then estimated wait in 13-px ink-3.
- 16-px below: information banner (blue-100 fill) with hydration / 1490 advice.
- Cancel button at the very bottom of the screen, secondary, full-width.

### Chat bubble
- 14-px radius (the eHealth-specific radius — softer than the rest of the system, intentional warmth).
- Mine: right-aligned, green-700 fill, white text, max 78% width.
- Theirs: left-aligned, white fill, 1-px `#D9D7CF` border, ink text, max 78% width.
- **Encaminhamento card** (structured nurse output): green-100 fill, green-700 1-px border, ink text. Header overline "Encaminhamento", title in 15-px / 600, body 13-px, action button right-aligned.
- Timestamps 11-px ink-3 underneath each bubble.

### Prescription QR card
- White surface, 1-px `#D9D7CF` border, 6-px radius (top-level surface).
- Header: prescription ID in mono 15-px, validity badge top-right.
- Centered QR (240-px square), 16-px padding around.
- Below QR: prescriber name + role + facility, then medicines list (each row: med name 14-px / 500, dose + frequency + duration 13-px / 400 / ink-3, mono lot if dispensed).
- Footer: two `lg` actions side by side — "Partilhar" (secondary), "Encontrar farmácia" (primary).

### Access log row
- 64-px row, 1-px bottom hairline.
- 40-px avatar circle (placeholder initials), name 14-px / 500, role + facility 12-px / 400 / ink-3.
- Time stamp right-aligned, 12-px ink-3.
- Override variant: row tinted `#FCEFEC`, additional 13-px red-500 line "Override de emergência" + tap-to-flag button.

### Notification banner mock
- Mimics OS banner: 4-px radius, white fill, 1-px shadow, 12-px padding.
- App icon 24-px square, app name 12-px / 600, time 11-px right.
- Title 14-px / 600, body 13-px, max 2 lines.
- SMS variant: same dimensions, mono body to convey "exactly as received".

### Language toggle
- 5 rows in a card, 48-px each, 1-px `#D9D7CF` between.
- Active row: green-100 fill, green-700 left edge accent (3 px), check mark right.
- Inactive rows: white, ink label, "(placeholder)" suffix in ink-3 12-px.

---

## 10. Layout & spacing (eHealth)

- 360-px design width (widest phones extend with 16-px gutters).
- Status bar 28 px + content + bottom tab 60 px = 760 design height.
- Section spacing: 16 px between cards, 24 px before primary CTA.
- Card padding: 16 px (vs 12 on clinical surfaces).
- Primary CTA always pinned to bottom on flow screens (above the tab bar) with a 12-px backdrop fade.

---

## 11. Do's and Don'ts (eHealth)

### Do
- Lead with **one primary action above the fold** on every screen.
- Use **patient language**: "tensão alta", "está em recuperação".
- Show **who has accessed your record** as a top-level tab — custody is the brand promise.
- Render **prescription QR large** (240 px) and include a fallback ID in mono.
- Include the **`*166#` USSD card** prominently, especially in the help / family-share area.
- Allow **flagging access** with one tap; never bury this behind a menu.
- Keep **animations to 200 ms or less** — patients are often anxious.

### Don't
- **Don't show clinical jargon.** No ICD-10 codes, no "HTA", no "DM2".
- **Don't show connectivity pill when sync is OK.** Reserve the affordance for degraded states.
- **Don't auto-call 1490.** Always require an explicit user tap.
- **Don't push install prompts.** No banners, no overlays.
- **Don't show ads, sponsored content, or tips from non-MISAU sources.** Public service.
- **Don't use emoji.** Including in chat templates and SMS.
- **Don't gate triage on identity verification.** A user with no BI can still ask for help.

---

## 12. Responsive behaviour (eHealth)

| Width | Treatment |
|---|---|
| < 360 px (older Android) | Single column, gutter shrinks to 12 px, body remains 16 px, primary CTA still block. |
| 360–480 px | Default design target. |
| 480–640 px | Same single-column layout, content max-width capped at 480 px and centered. |
| 640–840 px (tablet portrait) | Centered 480-px column on a `bg` page; not a tablet-specific layout. |
| ≥ 840 px (desktop / browser PWA) | Centered 480-px column inside a 1024-px page wrapper with brand strip header — "this is a phone app open in a browser" feels honest. |

**SMS / USSD parity.** Every flow that produces a screen has an SMS-equivalent string ≤ 160 chars and a USSD branch. The app surfaces the USSD code so users can show it to family without smartphones.

---

## 13. Agent prompt guide (eHealth)

### Component prompts
- **Home greeting plate:** "16-px padding card, green-100 fill, green-700 1-px border, 4-px radius. Greeting in 15-px ink, name in 24-px / 600 ink, identity line (BI/DIRE/TMP) in 13-px mono ink-2."
- **Symptom chip:** "64-px tall, white fill, 1-px `#D9D7CF` border, 4-px radius, 12-px padding. 14-px label, 12-px helper. Selected: green-100 fill, green-700 border, green-700 label."
- **Queue position display:** "Centered. 64-px / 600 ink number. 14-px ink-2 caption 'à sua frente'. 13-px ink-3 estimated wait. 16-px below: blue-100 information banner with hydration advice."
- **Encaminhamento card (chat):** "Inside chat thread, full-width bubble, green-100 fill, green-700 1-px border, 14-px radius, 12-px padding. Header overline 'ENCAMINHAMENTO' 11-px / 600 / 0.06em. Title 15-px / 600. Body 13-px. Right-aligned button primary `sm`."
- **Access row (override):** "64-px row, `#FCEFEC` background, 1-px `#E5B7AE` bottom border. 40-px avatar, name 14-px / 500, role + facility 12-px / 400 / `#5E5E5E`. Below: 13-px / 500 / `#C2392A` line 'Override de emergência'. Tap-to-flag button right, ghost variant red text."
- **USSD card:** "White surface, 1-px `#D9D7CF` border, 6-px radius. Header overline 'SEM TELEMÓVEL?' Title 16-px / 600. `*166#` rendered in 28-px mono ink. Below: 13-px ink-2 explanation, 'Imprimir cartão para sala de espera' link in blue-700."

### Iteration guide
1. Open every screen with **one primary action**, block width, `xl` (56-px) height, above the fold.
2. **Patient language only.** If a string includes "DM2" or "HTA", rewrite.
3. **Custody is the brand promise.** Acessos is a top-level tab. Override entries are visually loud.
4. **USSD is not a footnote.** Surface `*166#` whenever a screen mentions help or family.
5. **Calm motion only.** ≤200 ms transitions, no spring overshoots, no skeleton shimmer.

---

## 14. Open questions

- **Local-language translations.** Funded for which subset? Currently shown as labels only.
- **Dependent management.** A mother managing a child's record needs explicit consent flows; out of scope for this prototype.
- **Bandwidth-adaptive video.** Audio-only fallback exists in UI; the actual switch policy (RTT thresholds) is engineering's call.
- **PWA install prompts.** Should the app prompt install on browser PWA? Default off — public service should not nag.
- **Identity flagging policy.** When a user flags an access, what's the SLA for review? (Currently undefined; admin surface assumes 7 days.)
