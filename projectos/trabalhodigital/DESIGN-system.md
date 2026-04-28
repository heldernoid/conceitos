# DESIGN-system.md — Trabalho Digital Moçambique

**Status:** v0.3 · Abril 2026
**Owner:** MTSS · INSS · IGT · INEFP · Direcção de Trabalho Digital (DTD, fictícia neste protótipo)
**Scope:** Foundations shared by the five product surfaces (Trabalhador, Empregador, INSS, IGT, INEFP).

---

## 1. Visual theme & atmosphere

Trabalho Digital reads like the **infrastructure of the working day** — the digital equivalent of the fardamento, the carteira profissional, the recibo dobrado no bolso. Reference points: ILO digital platforms, Brazil's eSocial, India's e-Shram, South Africa's Department of Employment and Labour. Physical reference points: the orange capacete on a Maputo construction site, the alta-visibilidade of road workers, the carimbo seco on a contracto de trabalho, the carteira do INSS folded in a wallet.

Anti-references: tech-startup gig-work aesthetics, slick "find a job in 5 minutes" UX that hides protection mechanisms, gamified compliance that makes labour rights feel like an achievement to unlock.

The base canvas is a **warmer cream** (`#FAF8F4`) than other systems — the off-white of a workshop floor, of recycled paper. The brand is anchored by **deep construction orange** (`#B8501C`) — chosen for three reasons: (1) it reads instantly as "trabalho/construção" without explanation, (2) it carries the dignity of manual labour and high-visibility safety, and (3) it distinguishes Trabalho cleanly from the other five sister systems (Saúde green, Governo navy, Educa indigo, Finanças burgundy, Justiça slate). **Deeper orange** (`#7A3611`) appears in sidebars; **darkest orange** (`#5A2509`) in the government strip.

A **safety yellow** (`#D69E1A`) — high-visibility hi-vis — is reserved for safety-critical content: risk meters, IGT urgent flags, hi-vis stripes on documents that protect workers (auto de notícia, certidão IGT). This is the safety vest of the design system.

A **steel grey** (`#3D444F`) appears as structural support — for industrial sectors, for headers in the Empregador portal, for nav rails in admin systems.

A **closed sector palette** distinguishes 10 economic sectors across all surfaces: Construção (orange), Mineração (cobre), Agricultura (oliva), Pescas (teal), Comércio (roxo), Serviços (azul), Indústria (steel), Doméstico (brass), Sector Público (verde), Informal (âmbar). These colours are used consistently — Mineração is always `#5C3A24`, whether on a worker's profile, an empresa's HR page, or in dados.trabalho.gov.mz.

**MISAU green** (`#1B5E3F`) appears as accent for "regular · em ordem · subsídio aprovado · pensão activa" final states.

Typography uses **IBM Plex Sans** (UI), **IBM Plex Mono** (NUITs, BIs, números de inscrição INSS, NUEL, NUSS), and **IBM Plex Serif** — used for serious labour documents: contractos, autos de notícia da IGT, certificados de formação INEFP, certidões de pensão. The serif carries the weight of writing meant to be archived and produced as evidence.

What distinguishes the system is **respect for the worker's autonomy**. The Trabalhador app shows rights articulated, not buried. Salary breakdown is itemized, not just totalised. Inspection complaints can be anonymous. Formation completion certificates are owned by the worker, not the employer. The system never frames labour rights as bureaucratic friction.

**Key characteristics**

- Warm cream canvas (`#FAF8F4`) — never pure white
- Construction orange (`#B8501C`) as the singular brand anchor
- Sector palette (10 closed colours)
- Safety yellow (`#D69E1A`) reserved for safety-critical and hi-vis content
- MISAU green for "regular · subsídio aprovado · pensão activa"
- IBM Plex Sans 400/500/600 in UI; **Plex Serif used for contractos, autos, certificados**
- Plex Mono for NUITs, BIs, números de inscrição INSS, NUEL, NUSS
- **No 700, no display weights, no decorative type**
- Borders before shadows — 1-px hairlines (`#D7D9DD`) carry structure
- Tight radius scale: 2 / 4 / 6 px max
- Status colours reserved for procedural state, not "delete" buttons
- Provenance always visible — quem, quando, com que fundamento legal (Lei do Trabalho 23/2007, Lei da Segurança Social 4/2007)
- Two-step confirmation mandatory for every irreversible action (rescindir contracto, cancelar inscrição, encerrar empresa, anular pensão, aplicar coima ≥ 100 SMN)
- Multilingue mandatory in Trabalhador app (PT-MZ + Macua + Changana + Sena + Nyungwe)
- Mobile floor 16 px body; touch targets ≥ 44 px (≥ 48 px on field tablet)
- Worker number format: **NUSS** (Número Único de Segurança Social) `12-1234567-8` — like Saúde NUS
- Empresa: **NUEL** (Número Único de Empresa Laboral) `E-2026-MAP-018421`
- Contract: **CT-2026-MAP-001284**
- Auto IGT: **AI-2026-MAP-04218**

---

## 2. Purpose & posture

Trabalho Digital is **labour infrastructure**, not a recruiting platform. Every surface decision answers to seven principles:

1. **Direitos visíveis, não escondidos.** Salary breakdown shows every line. Discount for INSS is named, not just deducted.
2. **Tripartismo respeitado.** Worker, employer, State each have distinct surfaces with distinct affordances. Same data viewed three ways.
3. **Cumprir é mais fácil que evadir.** Empregador portal pre-fills declarations; auto-calculates IRPS retido; submits to INSS in one click. Friction belongs on shortcuts, not on compliance.
4. **Mozambican Portuguese · with local languages.** Macua, Changana, Sena, Nyungwe disponíveis em qualquer ecrã do Trabalhador. PT-MZ for institutional surfaces.
5. **Provenance obrigatória.** Quem registou, quando, com base em que lei. Contractos referenciam Lei 23/2007. INSS referencia Lei 4/2007.
6. **Confirmação para acto irreversível.** Rescisão, cancelamento, encerramento, coima alta — todos com OTP + justificação ≥ 80 chars.
7. **Por defeito público.** Estatísticas (salário médio por sector, taxa de informalidade, acidentes de trabalho, vagas em aberto) em `dados.trabalho.gov.mz`. Dados pessoais protegidos por sigilo de função.

---

## 3. Color palette & roles

### 3.1 Brand · Orange
| Token | Hex | Role |
|---|---|---|
| `orange-900` | `#5A2509` | Government strip, deepest chrome |
| `orange-800` | `#7A3611` | Sidebar fill, dark hero panels |
| `orange-700` | `#94431A` | Hover dark surfaces |
| `orange-600` | `#B8501C` | **Primary CTA, brand anchor**, links, focus |
| `orange-500` | `#D26B2C` | Hover light, highlight |
| `orange-400` | `#E68E4F` | Info accent |
| `orange-100` | `#F8E4D2` | Tinted surfaces, selected chips |
| `orange-50` | `#FCF1E7` | Hover row tint |

### 3.2 Sector palette (closed)
| Token | Hex | Sector |
|---|---|---|
| `sec-construcao` | `#B8501C` | Construção |
| `sec-mineracao` | `#5C3A24` | Mineração |
| `sec-agricultura` | `#5A6E2C` | Agricultura |
| `sec-pescas` | `#1F4A52` | Pescas |
| `sec-comercio` | `#7A4A8C` | Comércio |
| `sec-servicos` | `#3A6E7A` | Serviços |
| `sec-industria` | `#62697A` | Indústria |
| `sec-domestico` | `#A6843E` | Doméstico |
| `sec-publico` | `#1B5E3F` | Sector Público |
| `sec-informal` | `#9A6A00` | Economia Informal |

### 3.3 Safety yellow · hi-vis (uso restrito)
| Token | Hex | Role |
|---|---|---|
| `safety-700` | `#9A7100` | Hi-vis text |
| `safety-500` | `#D69E1A` | Risk meter alert, IGT urgent flag, hi-vis stripe |
| `safety-100` | `#FBEFC9` | Safety surface tint |

> Safety yellow appears only on safety-critical and protective content. Never decorative.

### 3.4 Steel · structural
| Token | Hex | Role |
|---|---|---|
| `steel-700` | `#3D444F` | Industrial sector header, side rail accent |
| `steel-500` | `#62697A` | Indústria sector chip |
| `steel-100` | `#E1E4E9` | Steel-tinted surfaces |

### 3.5 Verification
| Token | Hex | Role |
|---|---|---|
| `green-700` | `#1B5E3F` | "Regular · subsídio aprovado · pensão activa" |
| `green-100` | `#E4EFE9` | Verified surface tint |

### 3.6 Status (procedural state only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Pago, em dia, conforme |
| `amber-500` | `#C8911E` | Pendente, prazo, em análise |
| `red-500` | `#C2392A` | Em mora, infracção, suspenso |

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ + local-language diacritics)
- **Mono:** IBM Plex Mono — NUITs, BIs, NUSS, NUEL, contractos, OTPs
- **Serif:** IBM Plex Serif — **used for contractos, autos de notícia, certificados, certidões de pensão.** Documents that constitute proof.

### 4.2 Weights
- 400 body
- 500 UI labels, buttons
- 600 headings, MZN amounts, document titles
- 700 forbidden

### 4.3 Mono examples
- NUSS: `12-4218925-3`
- NUEL: `E-2026-MAP-018421`
- Contracto: `CT-2026-MAP-001284`
- Auto IGT: `AI-2026-MAP-04218`
- BI: `110100442918`
- NUIT: `400 304 188`
- Hash: `f8a3d7c2`

### 4.4 PT-MZ specifics
- Real institutions: MTSS (Ministério do Trabalho e Segurança Social), INSS (Instituto Nacional de Segurança Social), IGT (Inspecção Geral do Trabalho), INEFP (Instituto Nacional de Emprego e Formação Profissional), OTM (Organização dos Trabalhadores de Moçambique), CTA (Confederação das Associações Económicas), AAEM (Associação dos Antigos Empregados de Minas)
- Legal references: Lei do Trabalho 23/2007, Lei da Segurança Social 4/2007, Decreto 51/2017 (regulamento), Convenções OIT (29, 87, 98, 105, 111, 138, 182)
- Local languages embedded where appropriate: Macua (Emakhuwa), Changana (Xichangana), Sena (Cisena), Nyungwe (Cinyungwe)

---

## 5. Spacing & layout

### 5.1 Grid
- 8-px base unit
- Common steps: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Page max width: **1440 px** (Empregador, INSS, IGT admin); **1200 px** (landing); **360 px** (Trabalhador phone); **980 px** (tablet — IGT field)

### 5.2 Containers
| Container | Padding | Max width |
|---|---|---|
| Admin shell (INSS, Empregador) | 20 px | 1440 |
| IGT admin | 20 px | 1440 |
| Public landing | 24 px | 1200 |
| Trabalhador phone | 16 px | 360 |
| Tablet (IGT field) | 14 px | 980 |
| Card | 14 px | — |
| Modal | 16 px | 520 |
| Auto / contracto | 22 px | — |

### 5.3 Borders & corners
- Hairlines: 1 px solid `--line`
- Radii: 2 (badge), 4 (card / button / input), 6 (worker card hero). **Never** > 6.
- Auto / contracto documents use **dashed** dividers in the footer

---

## 6. Components

### 6.1 Buttons, Inputs, Cards, Tables, Govt strip, Top bar, Side rail, Phone frame, Tablet frame, Stepper, QR
Same shapes as the family. Orange replaces the other anchors. Brand mark redrawn as **square with hard-hat silhouette** — orange filled, white capacete outline reading as construção/segurança.

### 6.2 Worker card (`.worker-card`)
Hero component. Orange gradient, NUSS in mono, worker name, current employment status, QR for public verification. Shows on Trabalhador home, Empregador worker detail, INSS profile.

### 6.3 Auto · serifed document (`.auto`)
Used for: contracto de trabalho, auto de notícia da IGT, certificado INEFP, certidão de pensão. Plex Serif body, dashed footer with brass/safety seal.

### 6.4 Sector chip (`.sec`)
22 px height, 11 px text, white text on category-coloured fill. Used in worker profile, empresa list, IGT inspection target.

### 6.5 Risk meter (`.risk`)
3-bar safety indicator (low / med / high / critical). Used in IGT inspection planning, empresa risk profile, sector overview.

### 6.6 Payslip (`.payslip`)
Mono-font itemized payslip. Used in Trabalhador (read), Empregador (issue). Lines for base salário, horas extra, abonos, descontos INSS, retenção IRPS, líquido.

### 6.7 Hi-vis stripe (`.hivis`)
Yellow-black 45° stripe. Used as safety accent on landing page, in IGT urgent banners, on auto de notícia headers.

### 6.8 QR square (`.qr-square`)
Mock QR, used on contractos, certificados INEFP, autos IGT for public validation at `trabalho.gov.mz/v/<hash>`.

---

## 7. State patterns

### 7.1 Worker employment state
`não inscrito → inscrito INSS → contractado → activo → suspenso (doença/maternidade) → terminado → pensão`

### 7.2 Contract state
`rascunho → assinado pelas partes → registado MTSS → vigente → em rescisão → terminado / litigado`

### 7.3 IGT inspection state
`agendada → notificada → em campo → autuada → audiência conciliatória → coima OU regularização → arquivada / escalada`

### 7.4 INSS contribution state
`devida → declarada → paga → em mora → executada coercivamente`

### 7.5 Two-step confirmation
Required for:
- Rescindir contracto sem aviso prévio
- Cancelar inscrição INSS
- Encerrar empresa (NUEL)
- Anular pensão
- Aplicar coima ≥ 100 salários mínimos
- Embargar obra (IGT)

### 7.6 Provenance footer
Every auto, contracto, certificado carries: instituição, autor, data, hora, hash DTD, QR de validação pública.

### 7.7 Public visibility
Aggregate dashboards exposed by default at `dados.trabalho.gov.mz`: salário médio por sector, taxa de informalidade, acidentes de trabalho por província, vagas em aberto INEFP, autos por sector.

---

## 8. Accessibility & language

- AA+ contrast on all text including sector chips
- Focus rings: 2-px orange-600, 1-px offset
- Touch targets ≥ 44 px on mobile, ≥ 48 px on tablet (IGT inspectores em campo)
- Body floor: 16 px on mobile/tablet, 14 px on desktop
- Sector chips carry the sector name in text, never colour-only
- **Trabalhador multilingue mandatory:** PT-MZ + Macua + Changana + Sena + Nyungwe. Switch persistente.
- USSD `*146#` is the official low-tech fallback for status checks (consultar contracto, ver descontos INSS, denunciar à IGT)

---

## 9. Content & voice

### 9.1 Voice
- **Directo, claro, sem jargão jurídico desnecessário.** "O teu patrão tem 14 dias para pagar. Caso contrário, podes denunciar à IGT." not "Decorrido o prazo legal sem cumprimento da obrigação..."
- **Específico legalmente quando importa.** Em autos da IGT, em contractos, em certificados — citação plena de artigos da Lei 23/2007.
- **Educacional onde necessário.** Glossário inline para termos técnicos quando aparecem em ecrãs do Trabalhador (ex.: "o que é INSS?", "o que é IRPS?"). Mas nunca paternalista.

### 9.2 Naming
- Real institutions: MTSS, INSS, IGT, INEFP, OTM, CTA, AAEM
- Fictional **DTD** (Direcção de Trabalho Digital) is consistently labelled
- Real laws referenced: Lei do Trabalho 23/2007, Lei da Segurança Social 4/2007, Decreto 51/2017
- Convenções OIT relevantes citadas onde aplicável

---

## 10. Cross-system relationship

Trabalho Digital is the **sixth system** in the Conceitos family. Shared with Saúde, Governo, Educação, Finanças, Justiça:
- Plex type system, warm canvas, radius scale, spacing grid
- Connectivity-pill pattern, two-step confirmation, provenance footer

Differs on:
- **Anchor colour** — green (Saúde), navy (Governo), indigo (Educação), burgundy (Finanças), slate (Justiça), **orange (Trabalho)**
- **Vocabulary** — clinical · civic · academic · fiscal · judicial · **laboral**
- **Form factors** — Trabalho leads on mobile (worker), desktop (employer + admin), and tablet (IGT field).

Cross-system identity:
- **eBI of Governo Digital** is the source of truth for personal identity. Trabalho consumes it for any worker identification.
- **NUIT of Finanças Digitais** is the source of truth for employer identity. IRPS retido pelos empregadores reverte automaticamente para SISTAFE.
- **NUS of Saúde Digital** cruza com NUSS para subsídios de doença e maternidade.
- **Tribunais Laborais of Justiça Digital** — IGT escala para tribunal laboral quando conciliação falha.
- **Cadastro Predial** — IGT usa para georreferenciar obras inspeccionadas.

---

## 11. What is intentionally *not* in the system

- **No outcome prediction** for litigation (mirrors Justiça stance).
- **No employer rating system.** Aggregate stats yes, "this employer is rated 3.2 stars" no.
- **No gamification of compliance.** Cumprir não é "achievement". Não cumprir tem consequências reais, não pontos.
- **No predatory job-board mechanics.** No "apply in 60s" affiliate. INEFP é referência directa, sem comissão.
- **No third-party advertising.** No sponsored content.
- **No surveillance of workers.** Localização do trabalhador não é exposta ao empregador. IGT pode geo-localizar inspeccções *de obras*, não de pessoas.
- **No automated termination** of contracts. Rescisões requerem two-step e justificação.

---

## 12. Open questions for v0.4

- Trabalhadores migrantes (sazonais África do Sul, Suazilândia)
- Economia informal — como inscrever vendedoras de mercado sem coerção?
- Acidentes de trabalho — fluxo emergência (199 + INSS + IGT em paralelo)
- Pensões antigas (mineiros AAEM África do Sul) — reconciliação histórica
- Acessibilidade audit por trabalhadores com deficiência

---

*Authoritative for cross-surface decisions. When a surface document contradicts this document, this one wins.*
