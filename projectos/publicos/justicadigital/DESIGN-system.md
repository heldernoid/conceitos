# DESIGN-system.md — Justiça Digital Moçambique

**Status:** v0.3 · Abril 2026
**Owner:** MJCR · Tribunal Supremo · Direcção de Justiça Digital (DJD, fictícia neste protótipo) · DNRN
**Scope:** Foundations shared by the five product surfaces (Portal MJCR, Tribunal Comunitário, Cidadão/Justiça, Cadastro Predial, Registos Públicos).

---

## 1. Visual theme & atmosphere

Justiça Digital reads like **judicial infrastructure** — the digital equivalent of the togaed magistrate, the certified copy from the Cartório, the bound case file in the registry. Reference points: HMCTS (UK), Brazil's CNJ public portals, Estonia's e-Justice, Singapore Judiciary's JustisOne, and physical reference points: the Tribunal Supremo building in Maputo, the leather-bound Códigos, the carimbo seco on a certidão.

Anti-references: aggressive "tech-meets-law" startup aesthetics, bright primary colors, anything that suggests speed at the cost of solemnity, gamified compliance. Justice is not optimised for time-to-conversion.

The base canvas is the warm off-white (`#FAFAF7`) shared across the Conceitos family. The brand is anchored by **deep slate / charcoal** (`#2A2F3A`) — chosen because it carries judicial gravity (the colour of the toga, of legal binders, of seriousness without aggression) and distinguishes Justiça cleanly from the other four sister systems (Saúde green, Governo navy, Educa indigo, Finanças burgundy). **Deeper slate** (`#1F242E`) appears in sidebars; **darkest slate** (`#1A1D24`) in the government strip.

A **brass accent** (`#A6843E`) — oxidised, warm, never bright gold — is reserved for ceremonial moments: the carimbo on an acta, the certidão validada, the decisão final assinada digitalmente. Like the gold in Finanças, brass is rare. It is the visual signal that the State has *decided*, not merely processed.

A **closed case-type palette** distinguishes 7 process categories across all surfaces: Cível (slate), Criminal (red), Laboral (amber), Família (brass), Administrativo (teal), Comercial (brown), Comunitário (green-MISAU adjacent). These colours are used consistently — Criminal is always `#9C2A1A`, whether on a pauta in the Portal MJCR, in the Cidadão home, or in dados.justica.gov.mz.

**MISAU green** (`#1B5E3F`) appears as accent for "validado · arquivado · transitado em julgado" final states.

Typography uses **IBM Plex Sans** (UI), **IBM Plex Mono** (process numbers, NUITs, hashes), and **IBM Plex Serif** — used here more than in any other sister system, because **judicial documents are serif documents**. Actas, acordos, decisões, despachos: all serif. The serif carries the weight of writing meant to be archived.

What distinguishes the system is **respect for legal form**. Documents look like documents. Decisions are signed visibly. Provenance is mandatory. The system never shows a "decision" without showing who made it, when, and how it can be appealed.

**Key characteristics**

- Warm off-white canvas (`#FAFAF7`) — never pure white
- Slate (`#2A2F3A`) as the singular brand anchor
- Case-type palette (7 closed colours)
- Brass (`#A6843E`) reserved for "Carimbada DJD" / decisão final / certidão
- MISAU green for "transitado em julgado · arquivado"
- IBM Plex Sans 400/500/600 in UI; **Plex Serif used heavily for actas, acordos, despachos, decisões**
- Plex Mono for process numbers, NUIT, BI, hashes
- **No 700, no display weights, no decorative type**
- Borders before shadows — 1-px hairlines (`#D7D9DD`) carry structure
- Tight radius scale: 2 / 4 / 6 px max
- Status colours reserved for procedural state, not "delete" buttons
- Provenance always visible — quem, quando, com que fundamento legal
- Two-step confirmation mandatory for every irreversible judicial action (encerrar processo, sentenciar revel, arquivar mediação, anular escritura)
- Multilingue mandatory in Tribunal Comunitário (PT-MZ + Macua + Changana + Sena)
- Mobile floor 16 px body; touch targets ≥ 44 px
- Process number format: **P-2026-CIV-MAP-00481** (ano, espécie, província, sequencial)
- Acta number: **AC-2026-04-1248**
- DUAT number: **DUAT-2026-MAP-001284**

---

## 2. Purpose & posture

Justiça Digital is **judicial infrastructure**, not a legal-tech consumer product. Every surface decision answers to seven principles:

1. **Solene, não friendly.** Documents look serious. Sentences are explained but never softened.
2. **Forma legal sempre.** Despacho com cabeçalho, fundamentação, assinatura. Acordo de mediação com partes nomeadas e termos claros.
3. **Sistema dual reconhecido.** Tribunais comunitários têm o mesmo respeito visual que tribunais judiciais — não são "subordinados" no design.
4. **Mozambican Portuguese · with local languages.** PT-MZ é a base. Macua, Changana, Sena disponíveis em qualquer ecrã do Tribunal Comunitário.
5. **Provenance obrigatória.** Quem proferiu, quando, com base em que lei, e como se recorre.
6. **Confirmação para acto judicial.** Sentenciar à revelia, encerrar mediação sem acordo, arquivar processo, anular escritura — todos com OTP + justificação ≥ 80 chars.
7. **Por defeito público.** Estatísticas (tempo médio de processo, taxa de mediação, processos pendentes) em `dados.justica.gov.mz`. Identidade das partes em processos sigilosos protegida.

---

## 3. Color palette & roles

### 3.1 Brand · Slate
| Token | Hex | Role |
|---|---|---|
| `slate-900` | `#1A1D24` | Government strip, deepest chrome |
| `slate-800` | `#1F242E` | Sidebar fill, dark hero panels |
| `slate-700` | `#2A2F3A` | Primary CTA, brand anchor, default action, links, focus |
| `slate-600` | `#3A414F` | Hover/active surfaces, selected nav |
| `slate-500` | `#4F5868` | Muted accent, cível chip |
| `slate-100` | `#E0E3E8` | Tinted surfaces, selected chips |
| `slate-50` | `#EFF1F4` | Hover row tint |

### 3.2 Process-type palette (closed)
| Token | Hex | Espécie |
|---|---|---|
| `case-civel` | `#4F5868` | Cível |
| `case-criminal` | `#9C2A1A` | Criminal |
| `case-laboral` | `#9A6A00` | Laboral |
| `case-familia` | `#7A5A1E` | Família e Menores |
| `case-admin` | `#3A6E7A` | Administrativo (TA) |
| `case-comercial` | `#5C3A24` | Comercial |
| `case-comunitario` | `#2E5C3A` | Comunitário |

### 3.3 Ceremonial · Brass (uso restrito)
| Token | Hex | Role |
|---|---|---|
| `brass-700` | `#7A5A1E` | Carimbo text, acta header titles |
| `brass-500` | `#A6843E` | Selo de validação, certidão stamp |
| `brass-100` | `#EDE3CC` | Selo background fill |

> Brass appears only on State-stamped artifacts. Never as primary action, never as decoration.

### 3.4 Verification
| Token | Hex | Role |
|---|---|---|
| `green-700` | `#1B5E3F` | "Transitado em julgado · arquivado" |
| `green-100` | `#E4EFE9` | Verified surface tint |

### 3.5 Status (procedural state only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Concluído, transitado, conforme |
| `amber-500` | `#C8911E` | Pendente, em audiência, prazo |
| `red-500` | `#C2392A` | Em mora processual, revelia, suspenso |

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ + local-language diacritics)
- **Mono:** IBM Plex Mono — process numbers, NUITs, BIs, hashes, OTPs
- **Serif:** IBM Plex Serif — **used heavily for actas, acordos, despachos, decisões, certidões.** Judicial documents are serif documents.

### 4.2 Weights
- 400 body
- 500 UI labels, buttons
- 600 headings, MZN amounts, document titles
- 700 forbidden

### 4.3 Mono examples
- Processo: `P-2026-CIV-MAP-00481`
- Acta: `AC-2026-04-1248`
- DUAT: `DUAT-2026-MAP-001284`
- BI: `110100442918`
- NUIT: `100 281 749`
- Hash: `f8a3d7c2`
- OTP: `4 9 1 3 0 7`

### 4.4 PT-MZ specifics
- Real institutions: MJCR, Tribunal Supremo, Tribunal Administrativo (TA), PGR, OAM, DNRN, DPCT (Direcção Provincial de Coordenação Territorial)
- Legal references: Lei 4/92 (tribunais comunitários), Código Civil, Código Penal, Lei de Terras (19/97), Lei do Notariado (4/2009)
- Local languages embedded where appropriate: Macua, Changana, Sena (and Português)

---

## 5. Spacing & layout

### 5.1 Grid
- 8-px base unit
- Common steps: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Page max width: **1440 px** (Portal MJCR, Cadastro, Registos); **1200 px** (landing); **360 px** (Cidadão phone); **980 px** (tablet — Comunitário)

### 5.2 Containers
| Container | Padding | Max width |
|---|---|---|
| Admin shell (Portal MJCR) | 20 px | 1440 |
| Cadastro / Registos | 20 px | 1440 |
| Public landing | 24 px | 1200 |
| Cidadão phone | 16 px | 360 |
| Tablet (Comunitário) | 14 px | 980 |
| Card | 14 px | — |
| Modal | 16 px | 520 |
| Acta | 22 px | — |

### 5.3 Borders & corners
- Hairlines: 1 px solid `--line`
- Radii: 2 (badge), 4 (card / button / input), 6 (process card hero). **Never** > 6.
- Acta documents use **dashed** dividers in the footer (mimicking certified perforated edges)

---

## 6. Components

### 6.1 Buttons, Inputs, Cards, Tables, Govt strip, Top bar, Side rail, Phone frame, Tablet frame, Stepper, QR
Same shapes as the family. Slate replaces the other anchors. Brand mark redrawn as **square with horizontal brass bar and vertical white axis** — reading as a stylised gavel/balance.

### 6.2 Process card (`.proc-card`)
Hero component. Slate gradient, processo number in mono, party names, current state, QR for public consultation. Shows on Cidadão home, Portal MJCR detail, public consultation page.

### 6.3 Acta (`.acta`)
**Serifed document component.** White background, serif body, dashed footer. Used for: acta de audiência, acordo de mediação, despacho, sentença, certidão, escritura.

### 6.4 Case-type chip (`.case`)
22 px height, 11 px text, white text on category-coloured fill. Used in pauta, lista de processos, filtros.

### 6.5 Timeline (`.timeline`)
Process events in chronological order, immutable. Used in Portal MJCR detail, Cidadão process tracking.

### 6.6 QR square (`.qr-square`)
Mock QR, used in actas, certidões, citações.

### 6.7 Bar (progress, prazos)
Standard bar with slate default. Amber for prazo expiring, red for em mora processual, brass for certidão validity.

---

## 7. State patterns

### 7.1 Process state
Documents pass through:
`distribuído → autuado → em instrução → em audiência → sentenciado → transitado em julgado → arquivado`

For mediação:
`solicitada → convocada → audiência marcada → em mediação → acordo / sem acordo → arquivada / escalada`

### 7.2 Confidentiality
Three levels:
- **Público** (default for cível, comercial, administrativo)
- **Restrito** (família, menores, laboral)
- **Sigiloso** (criminal sensível, processo de juízes/PGR)

### 7.3 Two-step confirmation
Required for:
- Sentenciar à revelia
- Encerrar mediação sem acordo
- Arquivar processo definitivamente
- Anular escritura registada
- Cancelar DUAT
- Suspender certidão emitida

### 7.4 Provenance footer
Every acta carries: tribunal, juiz, secretário, data, hora, hash AT, link de validação pública.

### 7.5 Public visibility
Aggregate dashboards exposed by default at `dados.justica.gov.mz`: tempo médio por espécie, taxa de mediação bem-sucedida, pendentes por tribunal, ranking provincial.

---

## 8. Accessibility & language

- AA+ contrast on all text including case chips
- Focus rings: 2-px slate-700, 1-px offset
- Touch targets ≥ 44 px on mobile, ≥ 48 px on tablet (Comunitário · used by older juízes)
- Body floor: 16 px on mobile/tablet, 14 px on desktop
- Case chips carry the espécie name in text, never colour-only
- **Tribunal Comunitário multilingue mandatory:** PT + Macua + Changana + Sena. Switch persistent across session.
- USSD `*147#` is the official low-tech fallback for status checks

---

## 9. Content & voice

### 9.1 Voice
- **Solene, claro.** "Foi proferido despacho a 14 Abril 2026 pelo Juiz da 3.ª Secção Cível do Tribunal Judicial da Cidade de Maputo." not "O seu processo avançou! 🎉"
- **Específico legalmente.** Cita o artigo, a lei, o tribunal.
- **Educacional onde necessário.** Glossário inline para termos jurídicos quando aparecem em ecrãs do Cidadão. Mas nunca paternalista.

### 9.2 Naming
- Real institutions: MJCR (Ministério da Justiça, Assuntos Constitucionais e Religiosos), Tribunal Supremo, Tribunal Administrativo (TA), Procuradoria-Geral da República (PGR), Ordem dos Advogados de Moçambique (OAM), Direcção Nacional dos Registos e Notariado (DNRN), Direcção Provincial de Coordenação Territorial (DPCT)
- Fictional **DJD** (Direcção de Justiça Digital) is consistently labelled
- Real laws referenced: Lei 4/92 (tribunais comunitários), Constituição art. 4 e 223, Código Civil, Código Penal, Lei de Terras 19/97, Lei do Notariado 4/2009, Estatuto dos Magistrados Judiciais

---

## 10. Cross-system relationship

Justiça Digital is the **fifth and final** sister system in the Conceitos family. Shared with Saúde, Governo, Educação, Finanças:
- Plex type system, warm off-white canvas, radius scale, spacing grid
- Connectivity-pill pattern, two-step confirmation, provenance footer

Differs on:
- **Anchor colour** — green (Saúde), navy (Governo), indigo (Educação), burgundy (Finanças), **slate (Justiça)**
- **Vocabulary** — clinical · civic · academic · fiscal · **judicial**
- **Form factors** — Justiça leads desktops in tribunals, tablets in tribunais comunitários, phones in cidadão pocket

Cross-system identity:
- **eBI of Governo Digital** is the source of truth for personal identity. Justiça consumes it for any party identification.
- **NUIT of Finanças** is the source of truth for fiscal identity (SISA on imobiliário, certidão fiscal for empresa cases).
- **eRegistos / Conservatórias** of Governo Digital — Justiça Digital handles Civil/Comercial/Predial registos that operate as judicial sub-systems. The line is blurry by design (DNRN sits across both ministerial structures).
- **Cadastro Predial** cross-references with the territorial database referenced by Governo Digital.

---

## 11. What is intentionally *not* in the system

- **No outcome prediction.** No "chance of success" widget for litigants. The system is a record-keeper, not an oracle.
- **No tribunal ranking by win-rate.** Aggregate stats yes, individual judge scoring no.
- **No automated sentencing.** AI does not decide. Decisions are human, signed, appealable.
- **No predatory legal-aid mechanics.** No "find a lawyer in 60 seconds" affiliate scheme. OAM directory is straight referral.
- **No third-party advertising.** No sponsored content of any kind.
- **No surveillance hooks.** Public access is anonymous (no login required for public consultation).

---

## 12. Open questions for v0.4

- Audio for low-literacy users in Tribunal Comunitário (TTS in Macua, Changana, Sena)
- Print stylesheet for actas and certidões (every conservatória still prints)
- Sigilo gradient (sigiloso, restrito, público) automation rules
- Cross-border: extradition / transfer flows with SADC
- Accessibility audit by visual / motor specialists
- Auditoria do TA (Tribunal Administrativo) embebida directamente no Portal MJCR

---

*Authoritative for cross-surface decisions. When a surface document contradicts this document, this one wins.*
