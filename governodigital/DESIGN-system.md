# DESIGN-system.md — Governo Digital Moçambique

**Status:** v0.3 · Abril 2026
**Owner:** Unidade de Governação Digital (UGD)
**Scope:** Foundations shared by the five product surfaces (eBI, App do Cidadão, Balcão, Orçamento Aberto, Auditoria).

---

## 1. Visual theme & atmosphere

Governo Digital reads like **state-administration infrastructure** — closer to a national civil registry counter or a public-finance reporting portal than to a consumer service. Reference points kept open while drafting: gov.uk (UK), Estonia e-Eesti, India DigiLocker, Brazil gov.br, Portugal ePortugal, Singapore Singpass. Anti-references: marketing-led "super-apps", fintech, and any UI that styles itself after social media.

The base canvas is the same **warm off-white** (`#FAFAF7`) used across the Conceitos family — pure white reads as "marketing surface" and the warm tone signals that the surface is for civic work. The brand is anchored by a single **administrative navy** (`#1F3A5F`) — chosen to differentiate from MISAU green (which is reserved for health) while remaining within the muted-institutional vocabulary of the Mozambican state. A **deeper navy** (`#152A45`) appears in sidebars and dark hero panels; a **darkest navy** (`#0E1F36`) in the government strip. **MISAU green** (`#1B5E3F`) is *not absent* — it appears as an accent for "verified / signed / stamped" status, signalling that the action carries the same evidentiary weight as a government-issued document, but it is **never** a primary brand colour here.

Typography uses **IBM Plex Sans** (UI) and **IBM Plex Mono** (codes — BIs, NUITs, processo numbers, contract IDs). Plex was chosen because it is open-source, ships excellent diacritics for Portuguese (and reasonable coverage for Bantu transliterations), and reads as "institutional" rather than as a startup choice. The weight range is intentionally narrow — **400 / 500 / 600** — and **700 is forbidden in production**: a heavier weight would tip the surface into commercial territory.

What distinguishes the system is its commitment to **provenance over decoration**. Every document, every requerimento, every transparency record carries a visible identifier (process number, signing officer, timestamp, source ministry) — never tucked behind menus. Cards prefer 1-px borders to drop shadows; shadows appear only when an element is genuinely floating (modal, popover). Radii top out at **6 px** — generous-rounded card culture is rejected, because rounded edges in Mozambican civil-service UI carry an "informal" connotation that would undermine documentary authority.

**Key characteristics**

- Warm off-white canvas (`#FAFAF7`) — never pure white
- Administrative navy (`#1F3A5F`) as the singular brand anchor; deeper navies for chrome
- MISAU green (`#1B5E3F`) reserved for "signed / stamped / verified" affordances only
- IBM Plex Sans 400/500/600 — **no 700, no display weights**
- Mono (Plex Mono) for civic identifiers: BIs, NUITs, processos, contratos, OE códigos
- Borders before shadows — 1-px hairlines (`#D9D7CF`) carry the structure
- Tight radius scale: 2 / 4 / 6 px max — never pills, never `50%` cards
- Status colours reserved for documentary state, not "delete" buttons
- Provenance always visible — issuer, timestamp, signing chain
- Two-step confirmation mandatory for every irreversible civic action
- Mobile floor 16 px body; touch targets ≥ 44 px

---

## 2. Purpose & posture

Governo Digital is **state infrastructure**, not a consumer product. The design system exists to make every surface feel like the same institution: calm, restrained, predictable, accountable.

Every component decision answers to six principles:

1. **Calm, not promotional.** No gradients, glassmorphism, or theatrical shadows. Solid colour blocks, clear hierarchy, generous whitespace.
2. **Predictable before elegant.** Grid-aligned layouts; forms look like forms; same components on every surface.
3. **Built for sunlight & cheap tablets.** AA+ contrast, ≥44 px touch targets, ≥16 px body on mobile, ≥14 px on desktop, supports 7″ Android in landscape.
4. **Mozambican Portuguese.** All copy in PT-MZ; realistic names, provinces, districts, civic scenarios. Real institution names where the institution exists; fictional UGD where it doesn't.
5. **Provenance always visible.** Process numbers, signing officers, timestamps, and source ministries are surfaced — never hidden behind menus.
6. **Confirmation for civic action.** Issue / sign / merge / cancel / void require two taps and (where applicable) mandatory justification.

---

## 3. Color palette & roles

### 3.1 Brand
| Token | Hex | Role |
|---|---|---|
| `navy-900` | `#0E1F36` | Government strip, deepest chrome |
| `navy-800` | `#152A45` | Sidebar fill, dark hero panels |
| `navy-700` | `#1F3A5F` | Primary CTA, brand anchor, default action, links, focus |
| `navy-600` | `#2B4E7E` | Hover/active brand surfaces, selected nav |
| `navy-100` | `#E4E9F1` | Tinted surfaces, selected chips, active nav background |
| `navy-50` | `#F1F4F9` | Hover row tint on tables, subtle fills |

### 3.2 Verification (limited)
| Token | Hex | Role |
|---|---|---|
| `green-700` | `#1B5E3F` | "Signed" / "Stamped" / "Verified by State" affordance — never a default action |
| `green-100` | `#E4EFE9` | Verified surface tint, signed-document strip |

> **Cross-system note.** Green is the brand colour of *Saúde Moçambique*. In Governo Digital, green appears **only** on affordances that carry documentary weight — a successful signature, a stamped certidão, a verified record. This is deliberate: the cross-system semantic is "this carries the authority of the state".

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

### 3.5 Status (civic only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Successful sync, paid, accepted, conformant |
| `amber-500` | `#C8911E` | Awaiting, pending document, partial, override registered |
| `red-500` | `#C2392A` | Rejected, expired, voided, suspected fraud |

> **Status colour rule.** These hexes are reserved for **civically meaningful state**. Do *not* use red for "delete" buttons in admin views; do *not* use green for generic confirmations. A consistent status vocabulary is what allows a clerk or citizen to read the state of a process at a glance.

### 3.6 Fiscal accent (Orçamento Aberto only)
| Token | Hex | Role |
|---|---|---|
| `ochre-700` | `#7A5018` | Fiscal headline numbers, primary axis on charts |
| `ochre-500` | `#B07728` | Bar fills, fiscal accents |
| `ochre-100` | `#F1E2C7` | Background tint for fiscal surfaces |

The ochre palette is **scoped to the Orçamento Aberto surface** and the fiscal section of the App do Cidadão. It is the *only* place where a non-navy/non-status colour appears prominently. The choice signals "money / accounting" without inheriting the alarm semantics of red or the success semantics of green.

### 3.7 Premium / programme accents
None. There is **no premium tier**. The platform is universal civic infrastructure.

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ diacritics + Bantu coverage)
- **Mono:** IBM Plex Mono — exclusively for civic identifiers (BI, NUIT, processo, contrato, OE-código), never as decoration

### 4.2 Weights in production
- **400** body text
- **500** UI labels, buttons, metadata
- **600** headings, emphasis
- **700 forbidden.** A heavier weight tips the surface into commercial territory.

### 4.3 Scale
| Token | Size | Use |
|---|---|---|
| `t-display` | 44/1.1 | Landing hero only |
| `t-h1` | 32/1.15 | Surface hero, marketing-style entry |
| `t-h2` | 24/1.2 | Section heading |
| `t-h3` | 18/1.3 | Card title, subsection |
| `t-h4` | 15/1.35 | Small panel header |
| `t-lead` | 16/1.5 | Lead paragraphs, mobile body |
| `t-body` | 14/1.45 | Default desktop body |
| `t-meta` | 12/1.4 | Metadata |
| `t-cap` | 12/1.4 | Caption |
| `t-overline` | 11/1.4, ALLCAPS, +.08em | Section eyebrow |

### 4.4 Mono
Plex Mono is used for: BI numbers (`110100099876C`), NUIT (`401236789`), processo numbers (`P-2026-0084-MAP`), contract IDs (`CT-2026-MOPHRH-0142`), OE budget codes (`02.04.00.00`), OTP codes, payment references. **Never as decorative type.**

### 4.5 PT-MZ specifics
- Diacritics covered: ã õ ç á é í ó ú â ê î ô û à è
- Province names use full diacritics (Niassa, Cabo Delgado, Nampula, Tete, Zambézia, Manica, Sofala, Inhambane, Gaza, Maputo Província, Maputo Cidade)
- Currency: `MZN 1 234,56` (space-separated thousands, comma decimal)
- Dates: `04 Abr 2026` or `04/04/2026` — never US format
- BI format: `NNNNNNNNNNNNNL` (13 digits + control letter), grouped `110100099876 C` for display

---

## 5. Spacing & layout

### 5.1 Grid
- 8-px base unit
- Common steps: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Page max width: **1440 px** for admin surfaces; **1200 px** for marketing/landing/orçamento; **360 px** phone frame for mobile mocks

### 5.2 Containers
| Container | Padding | Max width |
|---|---|---|
| Admin shell | 20 px | 1440 |
| Public landing | 24 px | 1200 |
| Phone (PWA) | 16 px | 360 |
| Card | 14 px | — |
| Modal | 16 px | 520 |

### 5.3 Borders & corners
- Hairlines: 1 px solid `--line`
- Inner separators: 1 px solid `--line-2`
- Radii: 2 (badge), 4 (card / button / input), 6 (hero card). **Never** > 6.

---

## 6. Components

### 6.1 Buttons
- **Primary** (`.btn`): navy-700 fill, white text, 36 px tall by default
- **Sizes:** sm 28 / default 36 / lg 44 / xl 56 (xl reserved for landing CTAs)
- **Secondary** (`.btn.secondary`): white fill, ink text, line border
- **Ghost** (`.btn.ghost`): transparent until hover
- **Danger** (`.btn.danger`): red-700 fill — reserved for irreversible voids
- **Success** (`.btn.success`): green-700 fill — reserved for "Sign / Stamp / Issue" actions only

### 6.2 Inputs
- 36 px tall standard, 44 px on mobile (and on Balcão tablet)
- 1-px line border, 2-px navy-700 focus ring (inset)
- `.field` wraps label + input + hint/err

### 6.3 Cards
- White fill, 1-px line border, 4-px radius
- Header / body / footer slots (`.hd` / `.bd` / `.ft`)

### 6.4 Badges
Six tones: default · green · amber · red · blue · ochre · dark. Used for civic state, never as marketing emphasis.

### 6.5 Tables
Header in 11-px uppercase ink-3 over bg-2; row dividers in line-2; hover bg-2; selected navy-100. **Always sortable** for queues and ledgers.

### 6.6 Govt strip
Persistent darkest-navy strip at the top of every public-facing page. Carries: `República de Moçambique · UGD · Protótipo · Versão`. Mirrors the `gov.uk` and `gov.br` pattern of placing the state context above all chrome.

### 6.7 Top bar
56-px white bar with brand left, primary nav middle, connectivity + identity right. Identity is one click from sign-out and "switch facility / posto".

### 6.8 Side rail (admin)
220-px navy-900 fill, used by Auditoria. Groups labelled in 10-px uppercase ink-3 (over dark — `#8aa1bd`).

### 6.9 Phone frame
360 × 760, 34-px outer radius, 24-px screen radius. Used as a fixed device frame for the App do Cidadão and the citizen portion of the Auditoria flows.

### 6.10 Stepper
Used in multi-step civic flows (requerimentos, fusão de duplicados, pagamento). 20-px circles in navy-700 (active) / navy-100 (done) / bg-2 (pending).

### 6.11 QR
Used for: identity proof at balcão, comprovativo de requerimento, pagamento M-Pesa/eMola, signed certidão. Always rendered with provenance text underneath (process number + issued-at).

### 6.12 Bar (Orçamento)
8-px height, line-2 border. Fills: navy-700 (default), ochre-500 (fiscal), amber-500 (warning), red-500 (over-budget), good-700 (under-target). Used in budget-execution and contract-progress views.

---

## 7. State patterns

### 7.1 Connectivity
Three states surfaced in the connectivity pill:
- **Online + sync clean** (green dot)
- **Online + sync queue** (amber dot, count visible)
- **Offline** (grey dot)

### 7.2 Document state
Civic documents pass through: `rascunho` → `submetido` → `em análise` → `assinado` / `rejeitado` → (`emitido` | `arquivado`). Each state has a badge tone and a verb the operator can take.

### 7.3 Two-step confirmation
Required for: emitir BI, anular requerimento, fundir duplicados, registar óbito, cancelar contrato público, dispensar dados (auditoria override). Each requires:
1. A modal with a typed/structured justification (≥80 chars or controlled vocabulary)
2. A confirmation button labelled with the *consequence* ("Emitir BI definitivo", not "Confirmar")

### 7.4 Provenance footer
Every issued document carries: process number (mono), issued-at (date + time + timezone), signing officer (name + role + posto), and a verifiable QR. The QR resolves to a UGD-hosted page that re-displays the document with a "verified by State" green tick.

### 7.5 Empty states
Use plain language. Never illustrations. "Sem requerimentos pendentes" + a single ghost button "Novo requerimento". Never a smiley empty state.

---

## 8. Accessibility

- AA+ contrast on all text
- Focus rings: 2-px navy-700, 1-px offset
- Keyboard reachable order matches reading order on every surface
- Touch targets ≥ 44 px on mobile and Balcão tablet
- Screen-reader labels on every status badge ("Estado: assinado")
- Body floor: 16 px on mobile, 14 px on desktop — **never below**
- Language attribute always `lang="pt-MZ"` on document; `lang="en"` only on the OG card metadata

---

## 9. Content & voice

### 9.1 Voice
- **Civic, not corporate.** "Pode levantar o seu BI no Posto X" — not "Get your ID now!"
- **Active, not bureaucratic.** "Submeta o requerimento" — not "Proceda à submissão do referido requerimento"
- **Specific, not vague.** Always name the responsible body, the deadline, the cost.

### 9.2 Naming
- Real geographies (provinces, districts, postos administrativos)
- Real institution names where the institution exists (BAÚ, SISTAFE, SADC, IGF, MEF)
- Fictional **UGD** is consistently labelled as such in the protótipo
- Names of citizens / clerks: realistic Mozambican (Sumaila, Joaquina, Tomás, Felisberta, Cuamba, Macuácua, Massingue, Sitói, Chongo)

### 9.3 Numbers
- Currency `MZN 12 450,00`
- BI displayed in groups: `110100099876 C`
- NUIT: `401 236 789`
- Phone: `+258 84 123 4567`

---

## 10. Cross-system relationship with Saúde Moçambique

Governo Digital and Saúde Moçambique are sister systems in the **Conceitos** family. They share:

- The Plex type system, the warm off-white canvas, the radius scale, the spacing grid
- The connectivity-pill pattern, the two-step confirmation pattern, the provenance footer
- The "borders before shadows" discipline, the "no 700 weight" rule

They differ on:

- **Anchor colour** — green (health, MISAU) vs navy (administration, UGD)
- **Vocabulary** — clinical state vs civic / documentary state
- **Form factors** — Saúde leads with 7″ tablets in Centros de Saúde; Governo leads with desktops in conservatórias and a PWA on citizen phones
- **Authority** — Saúde grants clinical override; Governo grants civic override (e.g. registration without a parent's BI in remote areas)

Where they overlap (e.g. a citizen with a chronic condition needing both a renewed BI and a prescription), the eBI of Governo Digital is the **source of truth for identity** — Saúde Moçambique calls into the eBI registry, never the other way round.

---

## 11. What is intentionally *not* in the system

- No dark mode (counter and conservatória environments are well-lit; dark mode would carry an "informal" connotation in civil-service UI)
- No avatars with photos by default (initials only — protects against impersonation in queue displays at the Balcão)
- No badges higher than 22 px tall (we resist visual escalation)
- No animation beyond 150 ms transitions on hover/state
- No emoji in the UI chrome (only inside citizen-authored free text — e.g. notes on a requerimento)
- No social-media login (state identity is the only identity)

---

## 12. Open questions for v0.4

- USSD entry-points for the eBI status check and requerimento status check — fluxo and copy not yet drafted
- Tactile / printed companion docs — what does the paper requerimento look like when the citizen prints from the app? Out of scope for v0.3.
- Bantu language toggle — research with users of Macua, Changana, Sena before drafting any localized strings
- Print stylesheet for the issued certidão — needs to match the existing BAÚ paper format byte-for-byte to avoid disputes at the counter
- Accessibility audit by a specialist — current AA+ claim is internal QA only

---

*This document is the source of truth for cross-surface decisions. When a surface document (DESIGN-ebi, DESIGN-cidadao, etc.) contradicts this document, this one wins. Surface documents may add specifics; they may not loosen the rules.*
