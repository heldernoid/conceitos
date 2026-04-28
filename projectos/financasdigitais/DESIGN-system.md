# DESIGN-system.md — Finanças Digitais Moçambique

**Status:** v0.3 · Abril 2026
**Owner:** MEF · Autoridade Tributária · Direcção de Finanças Digitais (DFD, fictícia neste protótipo)
**Scope:** Foundations shared by the five product surfaces (Portal AT, e-Factura, Cidadão Contribuinte, Portal Comercial, SISTAFE Interop).

---

## 1. Visual theme & atmosphere

Finanças Digitais reads like **fiscal infrastructure** — the digital counterpart to the cartório dos impostos, the contabilista's desk, the official seal at the bottom of an authentic factura. Reference points: well-designed national tax authorities (HMRC, Estonia eMaksuamet, Portugal e-Fatura, Singapore IRAS, Norway Skatteetaten), the typography of legal/financial documents, and the gravity of receipts that are evidence of tax obligation.

Anti-references: fintech consumer apps with neon gradients and bouncy animations, "save 30% with this trick" copy, gamified savings widgets, anything that treats taxation as casual transaction.

The base canvas is the warm off-white (`#FAFAF7`) shared across the Conceitos family. Pure white reads as marketing; warm off-white reads as official document paper. The brand is anchored by **deep burgundy** (`#7A1F26`) — chosen because it carries fiscal gravity (the colour of seals, of legal stamps, of receipts that mean something) without slipping into corporate red. **Deeper burgundy** (`#5A1A1F`) appears in sidebars and dark hero panels; **darkest burgundy** (`#3D0F12`) in the government strip.

A **gold accent** (`#C49B3F`) is reserved for the ceremonial moments — the validated factura seal, the "Carimbada AT" stamp, the certificado fiscal. It is the digital equivalent of an embossed gold seal on a paper document. Like the sepia in Educação Digital's Biblioteca, the gold is rare — it appears only when the State has stamped something.

A **closed tax-type palette** distinguishes the five major taxes across all surfaces: IVA (azul institucional), IRPS (burgundy), IRPC (ocre), ISPC (verde simplificado), Aduaneiro (roxo), SISA (verde imobiliário). These colours are used consistently — IVA is always `#1F4D7A`, whether on a factura, in a Portal AT report, or in the public dashboard.

**MISAU green** (`#1B5E3F`) appears as accent for "validado · pago · liquidado" status — the same way it does in the rest of the family, signalling that the State has verified.

Typography uses **IBM Plex Sans** (UI), **IBM Plex Mono** (NUITs, processo numbers, MZN amounts), and **IBM Plex Serif** (formal certificates, legal preambles). The mono is used heavily here — every NUIT, every processo, every MZN amount is mono. Weights are **400 / 500 / 600**; 700 is forbidden.

What distinguishes the system is its commitment to **fiscal honesty over fintech comfort**. Tax owed is shown clearly, with all decomposition visible. There is no "pay in 3 instalments and feel good" dark pattern. Provenance is mandatory: which fiscal entered the assessment, which director signed the cobrança coerciva, which empresa emitted the factura. Every MZN flows from somewhere to somewhere; the path is always visible.

**Key characteristics**

- Warm off-white canvas (`#FAFAF7`) — never pure white
- Burgundy (`#7A1F26`) as the singular brand anchor; deeper burgundies for chrome
- Tax-type palette (6 closed colours) used consistently
- Gold (`#C49B3F`) reserved for "Carimbada AT" / official seal moments
- MISAU green for "validado / pago" status
- IBM Plex Sans 400/500/600; **Plex Mono used heavily for NUITs, MZN amounts, processo numbers**
- Plex Serif for formal certificates and legal preambles only
- **No 700, no display weights, no decorative type**
- Borders before shadows — 1-px hairlines (`#D9D7CF`) carry structure
- Tight radius scale: 2 / 4 / 6 px max
- Status colours reserved for fiscal state (em mora · liquidado · em fiscalização · em recurso), not "delete" buttons
- Provenance always visible — emissor, beneficiário, fiscal, timestamp, hash
- Two-step confirmation mandatory for every irreversible fiscal action (anular factura, lançar cobrança coerciva, encerrar processo)
- Mobile floor 16 px body; touch targets ≥ 44 px
- Currency: always MZN, mono, with thousands separator (`12 450,00`)

---

## 2. Purpose & posture

Finanças Digitais is **fiscal infrastructure**, not a fintech consumer product. Every surface decision answers to seven principles:

1. **Honest, not comfortable.** Tax owed is shown directly with decomposition. No "soften the bill" dark patterns.
2. **Predictable before elegant.** Pautas look like pautas; facturas look like facturas; same components on every surface.
3. **Built for cheap phones, market vendors, 2G, USSD fallback.** The fastest path to emit a factura is < 30 seconds. USSD `*146#` works for the no-smartphone universe.
4. **Mozambican Portuguese.** All copy in PT-MZ; realistic NUIT format (9 digits), MZN amounts, real institutions (AT, MEF, SISTAFE, BdM, INSS).
5. **Provenance mandatory.** Every factura, every assessment, every cobrança carries author, timestamp, and a verifiable QR.
6. **Confirmation for fiscal action.** Anular factura, lançar cobrança coerciva, mudar regime de tributação require structured justification + OTP.
7. **Public dashboards by default.** Where the State has aggregate fiscal data that is not personally identifiable, it is published — receitas por imposto, taxa de cumprimento, relação com OE.

---

## 3. Color palette & roles

### 3.1 Brand
| Token | Hex | Role |
|---|---|---|
| `burg-900` | `#3D0F12` | Government strip, deepest chrome |
| `burg-800` | `#5A1A1F` | Sidebar fill, dark hero panels |
| `burg-700` | `#7A1F26` | Primary CTA, brand anchor, default action, links, focus |
| `burg-600` | `#9A2F36` | Hover/active brand surfaces, selected nav |
| `burg-100` | `#F2DCDE` | Tinted surfaces, selected chips, active nav background |
| `burg-50` | `#F9EFF0` | Hover row tint on tables, subtle fills |

### 3.2 Tax-type palette (closed)
| Token | Hex | Imposto |
|---|---|---|
| `tax-iva` | `#1F4D7A` | IVA · Imposto sobre Valor Acrescentado |
| `tax-irps` | `#5A1A1F` | IRPS · Imposto sobre Rendimento Pessoas Singulares |
| `tax-irpc` | `#7A5018` | IRPC · Imposto sobre Rendimento Pessoas Colectivas |
| `tax-ispc` | `#1B5E3F` | ISPC · Imposto Simplificado Pequenos Contribuintes |
| `tax-aduan` | `#5C2D7A` | Aduaneiro |
| `tax-sisa` | `#2E5C3A` | SISA · Imposto sobre transmissões |

> **Tax palette rule.** These are *the* six tax-type colours. They cannot be used as decorative palette anywhere else. IVA is always `#1F4D7A` — whether on a factura, in a Portal AT cobrança report, or in the SISTAFE public dashboard.

### 3.3 Ceremonial · Gold (uso restrito)
| Token | Hex | Role |
|---|---|---|
| `gold-700` | `#8C6A1E` | Carimbada AT text, certificado headers |
| `gold-500` | `#C49B3F` | Selo de validação, factura stamp, NUIT card accent |
| `gold-100` | `#F2E6CC` | Selo background fill |

> Gold appears only on State-stamped artifacts. Never as primary action, never as decoration.

### 3.4 Verification
| Token | Hex | Role |
|---|---|---|
| `green-700` | `#1B5E3F` | "Liquidado · pago · validado pela AT" |
| `green-100` | `#E4EFE9` | Verified surface tint |

### 3.5 Text · Surface
`ink #1A1A1A` · `ink-2 #3A3A3A` · `ink-3 #5E5E5E` · `bg #FAFAF7` · `bg-2 #F2F1EB` · `line #D9D7CF`

### 3.6 Status (fiscal state only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Liquidado, conforme, pago, regular |
| `amber-500` | `#C8911E` | Em mora, aguarda validação, prestação parcial |
| `red-500` | `#C2392A` | Cobrança coerciva, fiscalização aberta, NUIT suspenso |

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ diacritics)
- **Mono:** IBM Plex Mono — **used heavily** for NUITs, processo numbers, MZN amounts, OTP codes, hash de factura
- **Serif:** IBM Plex Serif — formal certificates, legal preambles, official receipts

### 4.2 Weights
- **400** body
- **500** UI labels, buttons
- **600** headings, MZN amounts
- **700 forbidden**

### 4.3 Mono
Mono is used pervasively here. Examples:
- NUIT: `400 281 749`
- Processo: `P-2026-IRPS-MAP-04412`
- Factura: `FT 2026/00284`
- MZN: `12 450,00 MZN`
- Hash: `f8a3d7c2`
- OTP: `4 9 1 3 0 7`

### 4.4 PT-MZ specifics
- NUIT format: 9 digits, formatted `XXX XXX XXX`
- Currency: MZN, decimal comma, thousands space — `12 450,00 MZN` not "12,450.00"
- Tax periods: `1.º Tri 2026`, `Fev 2026` (mensal), `2026` (anual)
- Real institutions: AT (Autoridade Tributária), MEF (Ministério da Economia e Finanças), SISTAFE, INSS, BdM (Banco de Moçambique), DAF (Direcção de Área Fiscal)

---

## 5. Spacing & layout

### 5.1 Grid
- 8-px base unit
- Common steps: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Page max width: **1440 px** for Portal AT and Comercial; **1200 px** for landing/SISTAFE; **360 px** phone for e-Factura and Cidadão

### 5.2 Containers
| Container | Padding | Max width |
|---|---|---|
| Admin shell (Portal AT) | 20 px | 1440 |
| Comercial shell | 20 px | 1440 |
| Public landing | 24 px | 1200 |
| Phone (e-Factura, Cidadão) | 16 px | 360 |
| SISTAFE dashboards | 24 px | 1200 |
| Card | 14 px | — |
| Modal | 16 px | 520 |

### 5.3 Borders & corners
- Hairlines: 1 px solid `--line`
- Radii: 2 (badge), 4 (card / button / input), 6 (NUIT card hero). **Never** > 6.
- Factura uses **dashed** dividers (mimicking perforated paper receipts)

---

## 6. Components

### 6.1 Buttons, Inputs, Cards, Tables, Govt strip, Top bar, Side rail, Phone frame, Stepper, QR
Same component shapes as the family. Burgundy replaces navy/indigo in CTAs, focus rings, active nav. Brand mark redrawn as **stamped square with diagonal slash and gold dot** — reading as a fiscal seal.

### 6.2 NUIT card (`.nuit-card`)
Hero component. Burgundy gradient background, NUIT number in mono, name, QR code, gold accent. Shows on Cidadão home, Portal AT contribuinte detail, e-Factura company profile.

### 6.3 Factura (`.factura`)
Mono-typeset receipt with dashed divider lines mimicking perforated paper. Mandatory fields: NUIT emissor, NUIT comprador, items, IVA breakdown, IRPS retido (if applicable), QR, hash AT, timestamp.

### 6.4 Tax chip (`.tax`)
22-px height, 11-px text, white text on tax-coloured fill. Used in cobrança lists, dashboards, factura headers.

### 6.5 MZN big number (`.mzn`)
Mono, weight 600, slight negative letter-spacing. Variants `lg` (32px) and `xl` (44px). Used on dashboards, receipts, payment screens.

### 6.6 QR square (`.qr-square`)
Mock QR component (8×8 grid of dark/light squares). Used in factura validation, NUIT digital, payment requests.

### 6.7 Bar (execution / progress)
Same as the family. Burgundy default fill; gold variant for ceremonial progress; tax-coloured fills allowed only inside fiscal content.

---

## 7. State patterns

### 7.1 Connectivity & USSD
Three states (online · sync queue · offline). e-Factura has explicit USSD fallback path documented per surface.

### 7.2 Fiscal state
Documents pass through: `rascunho` → `emitida` → `validada AT` → `liquidada` (or `em mora` → `cobrança coerciva`).

### 7.3 Two-step confirmation
Required for: anular factura emitida, mudar regime de tributação, lançar cobrança coerciva, encerrar processo de fiscalização, suspender NUIT, declarar imposto final.

### 7.4 Provenance footer
Every factura carries: NUIT emissor, NUIT comprador, número, hash AT, timestamp, link de validação pública.

### 7.5 Empty states
Plain language. "Sem facturas emitidas este mês." + a single CTA.

### 7.6 Public visibility
Aggregate dashboards exposed by default at `dados.financas.gov.mz`: receitas por imposto, taxa de cumprimento, distribuição geográfica, ligação ao OE.

---

## 8. Accessibility

- AA+ contrast on all text including tax chips
- Focus rings: 2-px burgundy-700, 1-px offset
- Touch targets ≥ 44 px on mobile
- Body floor: 16 px on mobile, 14 px on desktop
- Tax chips carry the imposto name in text, never colour-only
- MZN amounts include screen-reader label: "doze mil quatrocentos e cinquenta meticais"
- USSD `*146#` is the official low-tech fallback for status checks

---

## 9. Content & voice

### 9.1 Voice
- **Direct, not friendly.** "Tem 12 450 MZN em mora desde 15 Fev." not "Há um pequeno valor pendente :)"
- **Specific.** Always name the tax, the period, the law article.
- **Educational where useful.** Inline explainers for tax mechanics ("ISPC: 3% sobre vendas brutas, sem IVA, sem IRPS"), but never patronizing.
- **No incentives copy.** "Pay early!" is not a feature here.

### 9.2 Naming
- Real institutions: AT (Autoridade Tributária), MEF, SISTAFE, BdM, INSS, DAF (Direcção de Área Fiscal), DPF (Direcção Provincial de Finanças)
- Fictional **DFD** (Direcção de Finanças Digitais) is consistently labelled
- Real laws referenced: Código IVA (Lei 32/2007), Código IRPS (Lei 33/2007), Código IRPC (Lei 34/2007), Código ISPC (Lei 5/2009)
- Names: realistic Mozambican (NUIT contribuinte personal: ~9 digits)

### 9.3 Numbers
- NUIT: 9 digits formatted `XXX XXX XXX`
- Personal NUIT: starts 1 (singular)
- Empresa NUIT: starts 4 (colectiva)
- Processo: `P-2026-IRPS-MAP-04412` (ano, imposto, província, sequencial)
- Factura: `FT 2026/00284`
- MZN format: `12 450,00 MZN` (decimal comma, thousands space)

---

## 10. Cross-system relationship

Finanças Digitais is the fourth sister system in the **Conceitos** family. Shared with Saúde, Governo, Educação:
- Plex type system, warm off-white canvas, radius scale, spacing grid
- Connectivity-pill pattern, two-step confirmation, provenance footer

Differs on:
- **Anchor colour** — green (Saúde), navy (Governo), indigo (Educação), **burgundy (Finanças)**
- **Vocabulary** — clinical · civic · academic · **fiscal**
- **Form factors** — Saúde leads tablets in CS; Governo desktops in conservatórias; Educação tablets in classrooms; **Finanças leads with phones in markets and desktops in DAFs**

Cross-system identity:
- **eBI of Governo Digital is the source of truth for personal NUIT** — the AT consumes it for IRPS profile binding. NUIT is bound to BI. A child's tutored NUIT (rare) is bound via parental consent.
- **SIGE de Educação Digital** doesn't directly write to Finanças, but Finanças *does* show "matriculada na Esc. Sec. da Polana" as deduction-eligible context.
- **INSS** (segurança social) is a separate system, but the e-Factura surface helps the trabalhador independente with INSS payment alongside ISPC/IRPS.

---

## 11. What is intentionally *not* in the system

- **No tax avoidance helper.** No "smart suggestions to pay less". The system computes what the law says.
- **No predatory collection mechanics.** Cobrança coerciva is a serious legal step, not a notification spam.
- **No private financial planning.** Finanças Digitais is fiscal record, not personal banking.
- **No third-party advertising.** No "credit score tip!" cards from sponsors.
- **No advisory AI claims for legal interpretation.** Tax law interpretation requires a contabilista or jurista — the app does not give legal advice.

---

## 12. Open questions for v0.4

- Audio receipts for low-literacy market vendors (text-to-speech in Macua, Changana, Sena)
- Negotiated payment plans for ISPC arrears (currently on/off; no plan UI)
- Cross-border e-Factura with SADC neighbours (Tanzania, South Africa)
- Bank API integration — débito directo for declarações
- Print stylesheet for declaração final
- Accessibility audit by specialist

---

*Authoritative for cross-surface decisions. When a surface document contradicts this document, this one wins.*
