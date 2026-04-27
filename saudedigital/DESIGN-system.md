# DESIGN-system.md — Saúde Moçambique

**Status:** v0.4 · Abril 2026
**Owner:** Gabinete de Sistemas de Informação para Saúde
**Scope:** Foundations shared by the four product surfaces (EMR, eHealth, Pharmacy, Audit).

---

## 1. Visual theme & atmosphere

Saúde Moçambique reads like **public-service infrastructure with a clinical conscience** — closer to a national tax portal or a hospital admission counter than to a consumer app. Reference points kept open while drafting: SNS24 (PT), gov.uk (UK), 1177 Vårdguiden (SE), e-Eesti (EE). Anti-references: marketing-led healthcare apps, fintech, Silicon Valley product UI.

The base canvas is a **warm off-white** (`#FAFAF7`), not pure white. Pure white reads as "marketing surface" under the equatorial daylight that floods most rural CSs through unshaded windows; the warm off-white reduces glare and signals that the surface is for work. The brand is anchored by a single **MISAU green** (`#1B5E3F`) — historically associated with the Ministry's coat of arms and consistent with how the public already recognises health-service materials in Mozambique. A **dark navy** (`#1F3A5F`) appears only in *information-bearing* contexts (links, focus rings, structural navigation) — never decoratively.

Typography uses **IBM Plex Sans** (UI) and **IBM Plex Sans Mono** (codes, doses, lot numbers, prescription IDs). Plex was chosen because it is open-source, ships excellent diacritics for Portuguese (and reasonable coverage for Bantu transliterations of Changana/Macua/Sena/Ndau), and reads as "institutional" rather than as a startup choice. The weight range is intentionally narrow — **400 / 500 / 600** — and **700 is forbidden in production**: a heavier weight would tip the surface into commercial territory.

What distinguishes the system from typical "gov-tech" is its commitment to **state visibility over decoration**. Connectivity, sync queue length, identity, prescription state, and audit footprint are present on every screen — never tucked behind menus. Cards prefer 1-px borders to drop shadows; shadows appear only when an element is genuinely floating (modal, popover). Radii top out at **6 px** — generous-rounded card culture is rejected, because rounded edges in Mozambican civil-service UI carry an "informal" connotation that would undermine clinical authority.

**Key characteristics**

- Warm off-white canvas (`#FAFAF7`) — never pure white
- MISAU green (`#1B5E3F`) as the singular brand anchor; deeper greens for sidebar fills
- Information navy (`#1F3A5F`) for links, focus, and structure — never decoration
- IBM Plex Sans 400/500/600 — **no 700, no display weights**
- Mono (Plex Mono) for clinical identifiers: prescriptions, doses, lots, BIs
- Borders before shadows — 1-px hairlines (`#D9D7CF`) carry the structure
- Tight radius scale: 2 / 4 / 6 px max — never pills, never `50%` cards
- Status colours reserved for clinical state, not "delete" buttons
- Connectivity pill always present on clinician/pharmacist surfaces
- Two-step confirmation mandatory for every irreversible clinical action
- Mobile floor 16 px body; touch targets ≥ 44 px

---

## 2. Purpose & posture

Saúde Moçambique is **public health infrastructure**, not a consumer product. The design system exists to make every surface feel like the same institution: calm, restrained, predictable, accessible.

Every component decision answers to six principles:

1. **Calm, not promotional.** No gradients, glassmorphism, or theatrical shadows. Solid colour blocks, clear hierarchy, generous whitespace.
2. **Predictable before elegant.** Grid-aligned layouts; forms look like forms; same components on every surface.
3. **Built for sunlight & cheap tablets.** AA+ contrast, ≥44 px touch targets, ≥16 px body on mobile, ≥14 px on desktop, supports 7″ Android in landscape.
4. **Mozambican Portuguese.** All copy in PT-MZ; realistic names, provinces, districts, clinical scenarios. ICD-10 PT.
5. **State always visible.** Connectivity, sync queue, identity, prescription state never hidden behind menus.
6. **Confirmation for clinical action.** Prescribe / dispense / merge / emergency override require two taps and (where applicable) mandatory justification.

---

## 3. Color palette & roles

### 3.1 Brand
| Token | Hex | Role |
|---|---|---|
| `green-900` | `#0F3D27` | Sidebar fill, deep brand surfaces, dark hero panels |
| `green-700` | `#1B5E3F` | Primary CTA, brand anchor, default action |
| `green-600` | `#247A52` | Hover/active brand surfaces |
| `green-100` | `#E4EFE9` | Tinted surfaces, success backgrounds, selected chips |

### 3.2 Information & structure
| Token | Hex | Role |
|---|---|---|
| `blue-900` | `#152A45` | Information emphasis, dark info banners |
| `blue-700` | `#1F3A5F` | Links, focus rings, structural navigation |
| `blue-100` | `#E4E9F1` | Information backgrounds, table-row selection |

### 3.3 Text
| Token | Hex | Role |
|---|---|---|
| `ink` | `#1A1A1A` | Body text — warm near-black, **never `#000`** |
| `ink-2` | `#3A3A3A` | Secondary text, labels |
| `ink-3` | `#5E5E5E` | Tertiary, metadata, timestamps |
| `ink-4` | `#8A8A8A` | Disabled |

### 3.4 Surface
| Token | Hex | Role |
|---|---|---|
| `bg` | `#FAFAF7` | App background — **warm off-white**, not pure white |
| `bg-2` | `#F2F1EB` | Subtle fills, table headers, hover background |
| `line` | `#D9D7CF` | Primary 1-px borders |
| `line-2` | `#E8E6DF` | Inner separators, hairlines |

### 3.5 Status (clinical only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Successful sync, dispensed, conformant |
| `amber-500` | `#C8911E` | Warning, partial dispense, override registered, awaiting |
| `red-500` | `#C2392A` | Critical, expired, blocked, suspected misuse |

> **Status colour rule.** These hexes are reserved for **clinically meaningful state**. Do *not* use red for "delete" buttons in admin views; do *not* use green for generic confirmations. A consistent status vocabulary is what allows a clinician to read severity at a glance under pressure.

### 3.6 Premium / programme accents
None. There is **no premium tier**. Resist the temptation to introduce one for "VIP" facilities or private practitioners — the platform is universal infrastructure.

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ diacritics + Bantu coverage)
- **Mono:** IBM Plex Sans Mono — used **only** for: prescription IDs, BI / DIRE numbers, lot numbers, dosages, ANARME registration numbers, audit hashes, USSD codes
- **System fallbacks:** `-apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif`

### 4.2 Hierarchy

| Role | Size | Weight | Line height | Tracking | Notes |
|---|---|---|---|---|---|
| Display | 44 px | 600 | 1.05 | -0.01em | Reserved for landing/hero only |
| H1 | 32 px | 600 | 1.1 | -0.005em | Page titles |
| H2 | 24 px | 600 | 1.15 | normal | Section headers |
| H3 | 18 px | 600 | 1.2 | normal | Panel headers |
| H4 | 15 px | 600 | 1.3 | normal | Card subheaders |
| Lead | 16 px | 400 | 1.5 | normal | Intro paragraphs |
| Body | 14 px | 400 | 1.5 | normal | Default body, desktop |
| Body Mobile | 16 px | 400 | 1.5 | normal | **Floor on phone surfaces** |
| Body Strong | 14 px | 500 | 1.5 | normal | Emphasis in tables/lists |
| Meta | 12 px | 400 | 1.4 | normal | Timestamps, helper text |
| Overline | 11 px | 600 | 1.3 | 0.06em | UPPERCASE, section labels |
| Mono inline | 13 px | 400/500 | 1.4 | normal | IDs, doses, codes |

### 4.3 Principles
- **No 700.** Production never uses bold-bold; 600 carries every emphasis. A 700 would push the system toward commercial visual language.
- **No italics for emphasis.** Italics are reserved for genuine bibliographic references in DESIGN docs; in product they're avoided because of poorer Portuguese diacritic rendering at small sizes.
- **Tracking is largely default.** Headlines get a hair of negative tracking (-0.005 to -0.01em) but never enough to read as "designed".
- **Mono carries authority for codes.** A prescription ID set in mono signals "this is a verifiable identifier"; the same string in proportional font would feel decorative.
- **Diacritics first.** Every type choice is checked against `ã ç é ó ú` and `Ñ` (used in Bantu transliteration). Plex passes; Inter and Roboto are rejected for thinner diacritic forms.

---

## 5. Component stylings

### Buttons
- **Variants:** `primary` (green-700 fill, white text), `secondary` (white fill, 1-px line, ink text), `ghost` (transparent, ink text), `danger` (red-500 fill), `amber` (sinalizar / atenção), `disabled`.
- **Sizes:** `sm` 28 / default 36 / `lg` 44 / `xl` 56. `block` modifier stretches full width — the default on mobile primaries.
- **Padding:** 0 14 px (sm), 0 16 px (default), 0 20 px (lg), 0 24 px (xl).
- **Radius:** 4 px universally. **No pill buttons.**
- **Focus ring:** `outline: 2px solid #FFBF47; outline-offset: 1px` — the gov.uk amber ring, chosen for high contrast against any background colour.
- **Hover:** background shifts ½ token darker; no transform, no shadow.

### Inputs
- Default 36 px height, `lg` 44 px on mobile and tablet.
- 1-px `line` border, 4-px radius, 0 10-px padding, 14-px text.
- Labels above field; helper text 12 px below; error text 12 px red.
- Phone inputs always carry `+258` prefix in a non-editable left adornment.
- Date inputs format as `DD/MM/AAAA` placeholder; always a calendar picker on tablet.
- Mono fields (prescription ID, lot, BI) render in Plex Mono.

### Cards
- 1-px `line` border, 4-px radius, white fill.
- Optional `hd` (header) and `ft` (footer) zones separated by a hairline `line-2`.
- Domain variants: **patient**, **encounter**, **prescription**, **audit-entry** — each shares chrome but differs in metadata zones.
- **No drop shadow.** If lift is required, use the modal/popover shadow tokens — only floating elements get shadows.

### Tables
- Sticky header: 11-px UPPERCASE overline, `bg-2` fill.
- Body row 44-px, 13-px text, hairline bottom border.
- Hover: `bg-2` fill on the entire row.
- Selected: `blue-100` fill, blue-700 left edge accent (3 px).
- First column for IDs uses Plex Mono.

### Badges
- 22-px height, 0 8-px padding, 11-px text weight 500, 11-px radius.
- Variants: neutral (`bg-2` + ink), green, amber, red, blue, dark.
- **Reserved vocabularies** (do not invent new labels):
  - **Prescription:** Pendente · Parcialmente dispensada · Dispensada · Expirada · Sinalizada
  - **Triage (Manchester):** Vermelho · Amarelo · Verde · Azul
  - **Audit:** Normal · Fora do âmbito · Override de emergência · Sinalizado pelo paciente
  - **Role (audit/EMR):** Médico · Téc. Medicina · Enfermeiro/a · Farmacêutico/a · Administrativo · Cidadão/ã

### Connectivity pill
- Always visible on EMR/Pharmacy/Audit. Three states:
  - **Sincronizado** — green-100 bg, green-700 text + dot
  - **A sincronizar · N alterações** — amber bg, amber-500 text
  - **Offline · N alterações em fila** — neutral bg, ink-2 text
- On the patient app: lighter rendering, only shown when offline.

### Identity badge
- Top-right of every web surface: 28-px avatar, name (14 px / 600), role + facility (11 px / 400 ink-3).
- Click opens session menu: trocar unidade, terminar sessão, levantar preocupação.

### Modal & confirmation
- Centered, max 520-px width, white, 1-px line border, **6-px radius** (only place the larger radius is used).
- Two-step pattern: step 1 review, step 2 attribute (signature, lot, justification).
- Backdrop: `rgba(20,20,20,.4)`.
- Close affordance always top-right; cancel returns to step 1, never out of the flow.

### Banner (inline alerts)
- Full-width within container, 4-px radius, 12-px padding, 1-px border in matching family.
- Variants: neutral (`bg-2`), amber (`#FEF6E0` / `#E7D49C`), red (`#FCEFEC` / `#E5B7AE`), blue (`#E4E9F1` / `#BFCBDD`).
- Always include a leading 16-px square mark (icon-shaped placeholder); never use emoji.

### Phone frame
- 360 × 760, 10-px black bezel, 24-px outer radius, 4-px inner.
- Status bar 28 px (left: clock; right: signal/battery placeholders).
- Bottom tab bar 60 px, 4 max tabs.

### Side rail
- Admin/audit only. 220-px wide, `green-900` fill, 14-px sans white items.
- Group headers 10-px UPPERCASE, 50% opacity white.
- Active item: white left edge accent (3 px) + slightly lighter row fill.

---

## 6. Layout principles

### Spacing system
- **Base unit:** 4 px.
- **Scale:** 4 / 6 / 8 / 10 / 12 / 14 / 16 / 20 / 24 / 32 / 48 / 64.
- 8-px and 16-px are the workhorses; 24-px and 32-px reserved for between-section breathing room.

### Grid & container
- Desktop content max-width: **1440 px**, with 24-px gutters.
- Tablet (7"–10"): full-bleed with 16-px gutters.
- Phone: 16-px gutters; component padding 14–16 px.
- Sidebar widths: 220 px (audit) / 264 px (EMR); never variable per page.

### Whitespace philosophy
- **Civil-service density.** Forms and tables are packed; whitespace is for *between* sections and around primary actions, not within data displays.
- A clinician's screen should fit "one patient's relevant clinical context" without scrolling at 1366×768.
- Patient app prefers more breathing room — 12–16 px between cards — because the user is anxious, not skimming.

### Border-radius scale
| Token | Px | Use |
|---|---|---|
| `r-0` | 0 | Tables, full-bleed surfaces |
| `r-1` | 2 | Chips, pills, inline tags |
| `r-2` | 4 | **Default** — buttons, inputs, cards |
| `r-3` | 6 | Modals, popovers — top-level surfaces only |
| Circle | 50% | Avatars only — never buttons or controls |

---

## 7. Depth & elevation

| Level | Treatment | Use |
|---|---|---|
| **0 — Flat** | No shadow, no border | Page background, body copy zones |
| **1 — Bordered** | 1-px `line` border | Cards, panels, list rows, tables |
| **2 — Hairline lift** | `0 1px 0 rgba(20,20,20,.04)` | Sticky table headers, fixed top bar |
| **3 — Modal/popover** | `0 2px 6px rgba(20,20,20,.06)` | Modals, dropdowns, calendar popover |
| **4 — Focus** | `outline: 2px solid #FFBF47; offset 1px` | Any interactive focus |

**Shadow philosophy.** Saúde Moçambique deliberately rejects the warm-multi-layer shadow vocabulary common in commercial UI. Cards do not float; they sit on the canvas, separated by hairlines. Shadows mean "this element is genuinely above the page" — i.e. a modal or a popover. This makes the whole surface feel structural, like printed forms.

---

## 8. Patterns

### Connectivity protocol
Every clinician/pharmacist screen subscribes to a global sync state. UI never *hides* offline; instead it shows the queue length and disables actions that require server ack (sending an SMS, opening a video call). Local actions (writing notes, drafting prescriptions) remain available and queue.

### Two-step confirmation
Apply to: prescribing, dispensing, merging records, emergency override, flagging suspicious access. Step 1 is a **review** screen. Step 2 captures the operator-attributable detail (signature, lot, justification) and emits the action. Cancellation always returns to step 1, never out of the flow.

### Empty states
Every list has a designed empty state with: a square placeholder mark, a one-line headline, a one-sentence explanation, and one suggested action. Example: "Ainda não tem consultas registadas. Quando uma unidade sanitária registar uma consulta consigo, aparecerá aqui."

### Error states
Inline first (field-level). Page-level only when the whole flow cannot proceed. Always include the user's next step ("Criar registo temporário", "Tentar novamente", "Contactar suporte").

### Notification copy
Plain Portuguese, present tense, name the facility. Example: "O seu registo foi consultado no Centro de Saúde de Maxixe a 14/04/2026 às 22:48 pelo Dr. Adérito Mucopo (Médico)."

---

## 9. Accessibility

- Contrast ≥ 4.5:1 for text, ≥ 3:1 for UI affordances. The warm off-white background is selected to keep `ink` body contrast above 12:1.
- Focus visible on every interactive element; 2-px amber ring.
- Touch targets ≥ 44 × 44 px on mobile and tablet, ≥ 32 × 32 px on desktop.
- All form fields have programmatic labels.
- No information conveyed by colour alone — badges always include text.
- Patient app supports Portuguese default with placeholders for **Changana, Macua, Sena, Ndau** (label only in this prototype).

---

## 10. Brand mark

A 24 × 24 dark-green square containing a white cross. Wordmark "Saúde Moçambique" set in IBM Plex Sans 600, with a tertiary line below ("Plataforma Nacional de Saúde") in 11-px uppercase. Mark and wordmark are always rendered together unless space forbids; favicon is the mark alone. **No glossy, no gradient, no animation.**

---

## 11. Do's and Don'ts

### Do
- Use **`#1A1A1A`** for body text — warm near-black, never `#000`.
- Use **MISAU green (`#1B5E3F`)** as the primary action and brand anchor.
- Use **`#FAFAF7`** as page background — warm off-white reduces glare under daylight.
- Use **IBM Plex Sans 400 / 500 / 600** — a tight three-weight range carries every UI need.
- Use **Plex Mono** for prescription IDs, BI, lot numbers, dosages, and audit hashes.
- Use **1-px hairline borders** before reaching for shadows.
- Apply **2-step confirmation** for any clinical action that emits a record.
- Keep **status colours reserved for clinical state** (success / partial / critical).
- Render the **connectivity pill** on every clinician/pharmacist screen, always.
- Use the **gov.uk amber focus ring** (`#FFBF47`, 2 px, 1 px offset) on every interactive element.
- Show identity (name + role + facility) top-right on every web surface.
- Write copy in **PT-MZ**: "telemóvel", "consigo", "BI", "Centro de Saúde". Never Brazilian PT.

### Don't
- **Don't use weight 700 in production** — 600 is the maximum. Bold-bold reads as commercial.
- **Don't use pure black `#000`** for text or surfaces. The warmth matters under daylight.
- **Don't use red for non-clinical destructive actions** ("Apagar rascunho" is neutral, not red).
- **Don't use rounded pills or `50%`-radius cards.** Avatars only get the circle.
- **Don't introduce gradients, glassmorphism, or multi-layer shadows.** Borders carry structure.
- **Don't hide connectivity, sync queue, or identity** behind menus — they are always-visible state.
- **Don't use emoji** — including in notifications and SMS. The platform is institutional.
- **Don't use brand green decoratively.** Reserve it for actions and brand surfaces.
- **Don't display clinical content on the audit surface.** Audit shows metadata only.
- **Don't write copy in clinical jargon on the patient app.** "Tensão alta", not "HTA"; "está em recuperação", not "em pós-tratamento".
- **Don't auto-resolve flagged records.** A patient flag opens a real case with an SLA.
- **Don't introduce additional brand colours** for "VIP" or "private" tiers. There aren't any.

---

## 12. Responsive behaviour

### Breakpoints
| Name | Width | Surfaces | Notes |
|---|---|---|---|
| Phone S | < 360 px | eHealth | Single column, 14-px gutters, body 16 px. Older Android. |
| Phone | 360–480 px | eHealth | Default mobile target. |
| Phone L | 480–640 px | eHealth | Larger Android phones; same single-column layout. |
| Tablet 7″ | 640–840 px | EMR, Pharmacy | 7-inch landscape Android — primary clinician surface. Two-column patient view. |
| Tablet 10″ | 840–1024 px | EMR, Pharmacy | Three-column patient + summary. |
| Desktop | 1024–1440 px | All | Full sidebar + multi-column dashboards. |
| Desktop L | 1440–1920 px | EMR, Audit | Audit dashboards expand to wide tables. |
| Wide | > 1920 px | Audit | Maximum content 1440 px, side gutters absorb extra. |

### Touch target rules
- Mobile and tablet: ≥ 44 × 44 px hit areas. Spacing ≥ 8 px between adjacent interactive elements.
- Desktop with mouse: ≥ 32 × 32 px is acceptable; tables expand row hover area to full row.

### Collapsing strategy
- Sidebar (audit / EMR): expanded → icon-only 60 px → off-canvas drawer triggered by hamburger.
- Tables: never horizontal scroll on phone; collapse to stacked-row card layout.
- Multi-column patient view: 3 → 2 → 1 column.
- Top bar nav: full → overflow menu → drawer.
- Modals: 520-px max → full-bleed sheet on phone with 16-px top inset.

### Image / placeholder behaviour
Photography is **not** part of the system. Every "image" in the prototype is a designed placeholder square showing the asset class (`Foto`, `Logotipo`, `Selo`, `Mapa`). Real implementation will source imagery from MISAU asset library and apply a 4-px radius mask consistent with cards.

---

## 13. Agent prompt guide

### Quick colour reference
- Background: `#FAFAF7` (warm off-white)
- Surface: `#FFFFFF`
- Text: `#1A1A1A` (warm near-black)
- Brand action: `#1B5E3F` (MISAU green)
- Sidebar / hero: `#0F3D27` (deep green)
- Information / link: `#1F3A5F` (navy)
- Border: `#D9D7CF` (warm hairline)
- Success: `#1B6B3A`  · Warning: `#C8911E`  · Critical: `#C2392A`
- Focus ring: `#FFBF47` 2 px / 1 px offset

### Component prompt examples
- **Patient card:** "White surface, 1-px `#D9D7CF` border, 4-px radius, no shadow. Header zone: 12-px padding, ink-2 overline, ink h3. Body: 14-px Plex Sans, 1.5 line height. Footer hairline `#E8E6DF`. **No drop shadow.**"
- **Primary button:** "Green-700 (`#1B5E3F`) fill, white text, 36-px height, 0 16-px padding, 4-px radius, 14-px Plex Sans 500. Hover green-600. Focus: 2-px `#FFBF47` outline at 1-px offset. **No shadow, no transform.**"
- **Prescription badge:** "11-px Plex Sans 500, 22-px height, 0 8-px padding, 11-px radius. Variants reserved: Pendente (neutral), Parcialmente dispensada (amber), Dispensada (green), Expirada (red), Sinalizada (red)."
- **Connectivity pill:** "22-px height, 0 8-px padding, 11-px radius. Three states: Sincronizado (green-100 bg, green-700 dot + text), A sincronizar (amber-100 bg, amber-500), Offline (bg-2, ink-2). Always visible, top-right of identity badge."
- **Modal:** "520-px max width, white, 1-px `#D9D7CF` border, 6-px radius, `0 2px 6px rgba(20,20,20,.06)` shadow. Backdrop `rgba(20,20,20,.4)`. Two-step: step 1 review, step 2 mandatory justification + sign."
- **Identity badge:** "28-px avatar circle, name 14-px / 600, role + facility 11-px / 400 / `#5E5E5E` underneath. Top-right of header. Click → session menu."
- **Audit event row:** "13-px Plex Sans body, mono timestamp `#5E5E5E`. Severity by row tint only (red `#FCEFEC`, amber `#FFFBEF`). Role badge in role-coloured family. Hairline bottom border, no shadow."

### Iteration guide
1. Start from the **off-white background** and **1-px hairline grid**. If a screen looks dramatic, you've already lost the system.
2. Brand green is for **actions and brand surfaces only**. If you've used green more than three times on a screen, remove the decorative ones.
3. Every interactive element gets the **amber focus ring** — keyboard access is non-negotiable.
4. Mono is for **identifiers and codes**. If you reach for mono for stylistic reasons, stop.
5. Status colour means **clinical state**. Never use red as "destructive" or green as "success" outside the clinical vocabulary.
6. Two-step confirmation is **mandatory** for every action that emits a clinical record. No exceptions.
7. Every screen must show **connectivity, identity, and (where applicable) prescription/audit state**.
8. Copy is **PT-MZ**, **plain language on patient surfaces**, **clinical vocabulary on EMR**.

---

## 14. Open questions

- **Logo lock-up with MISAU coat of arms.** Final cobranding pending DGS approval.
- **Manchester vs. simplified triage.** EMR uses Manchester 4-tier; eHealth shows a simplified version to citizens. Need clinical sign-off on mapping.
- **Languages beyond Portuguese.** Translation scope for Changana, Macua, Sena, Ndau pending budget confirmation.
- **Print styles.** Receita physical printout from the EMR is not yet specified.
- **Dark mode.** Not in v0.4 scope. EMR/Audit on outdoor tablets may need it; pending pilot feedback.
