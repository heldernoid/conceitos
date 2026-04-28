# DESIGN-system.md — Educação Digital Moçambique

**Status:** v0.3 · Abril 2026
**Owner:** MINEDH · Direcção de Educação Digital (DED, fictícia neste protótipo)
**Scope:** Foundations shared by the five product surfaces (SIGE, Caderno do Professor, Caderno do Aluno, Biblioteca Pública, Portal de Matrículas).

---

## 1. Visual theme & atmosphere

Educação Digital reads like **scholarly infrastructure** — the digital counterpart to a well-organized school office, a teacher's desk, a public library reading room. Reference points kept open while drafting: the visual language of well-designed national education systems (gov.uk schools, India DIKSHA, Estonia eKool, Singapore SLS), the typography of academic publishing, and the calm authority of public-library wayfinding. Anti-references: edutech consumer apps with gamification overlays, animated mascots, "streak" mechanics, or any UI that treats learning as a points-earning game.

The base canvas is the same **warm off-white** (`#FAFAF7`) used across the Conceitos family — pure white reads as "marketing surface" and the warm tone signals that the surface is for the daily work of education. The brand is anchored by a single **scholarly indigo** (`#322B7A`) — chosen to feel intellectual and ceremonial without slipping into corporate purple. A **deeper indigo** (`#241F58`) appears in sidebars and dark hero panels; a **darkest indigo** (`#1A1740`) in the government strip. **MISAU green** (`#1B5E3F`) is *not absent* — it appears as an accent for "verified / signed / stamped by State" status, signalling that a document carries the same evidentiary weight as a government-issued document, but it is **never** a primary brand colour here.

A small **subject palette** is unique to this surface family. Six colours encode academic disciplines (Português · Matemática · Ciências · História · Arte · Educação Física) and appear consistently across pautas, horários, planos de aula, and the Biblioteca catalogue. They are *not* a free design vocabulary — they are a closed set, reused identically by every surface.

A **sepia accent** (`#5C4A2E` / `#8C7045`) is reserved for the Biblioteca Pública surface, signalling "reading" and the warmth of paper. Like the ochre in govdigital's Orçamento Aberto, it is scoped to one surface and never bleeds into chrome.

Typography uses **IBM Plex Sans** (UI), **IBM Plex Mono** (codes — student IDs, NUIT-like school codes, processo numbers), and **IBM Plex Serif** (book titles, library reading mode, formal documents). The serif appears only in academically-meaningful contexts — not as decoration. Weights are **400 / 500 / 600**; 700 is forbidden.

What distinguishes the system is its commitment to **academic dignity over engagement metrics**. There are no streaks, no badges-as-trophies, no public leaderboards, no "study harder!" exclamation marks. Grades are shown as plain circles with the mark; pass/fail is communicated through colour, not emoji. Provenance is always visible: which professor entered the grade, which director approved the pauta, which librarian verified the book.

**Key characteristics**

- Warm off-white canvas (`#FAFAF7`) — never pure white
- Scholarly indigo (`#322B7A`) as the singular brand anchor; deeper indigos for chrome
- Subject palette (6 closed colours) for academic content, identical across surfaces
- Sepia accent (`#5C4A2E`) reserved for Biblioteca Pública
- MISAU green reserved for "signed / stamped / verified by State" affordances only
- IBM Plex Sans 400/500/600; Plex Mono for codes; Plex Serif for book titles & reading mode
- **No 700, no display weights, no decorative type**
- Borders before shadows — 1-px hairlines (`#D9D7CF`) carry the structure
- Tight radius scale: 2 / 4 / 6 px max — never pills, never `50%` cards (except the **grade circle**)
- Status colours reserved for academic state (aprovado / pendente / dispensado / faltoso), not "delete" buttons
- Provenance always visible — professor, director, librarian, timestamp
- Two-step confirmation mandatory for every irreversible academic action (lançar pauta final, anular matrícula, transferir aluno)
- No engagement gamification — no streaks, no points, no "you did it!"
- Mobile floor 16 px body; touch targets ≥ 44 px

---

## 2. Purpose & posture

Educação Digital is **education infrastructure**, not an edutech consumer product. The design system exists to make every surface feel like the same institution: calm, scholarly, predictable, dignified.

Every component decision answers to seven principles:

1. **Calm, not engaging.** No gradients, glassmorphism, or theatrical shadows. No streaks, badges-as-trophies, or "you're amazing!" microcopy. Solid colour blocks, clear hierarchy.
2. **Predictable before elegant.** Grid-aligned layouts; pautas look like pautas; horários look like horários; same components on every surface.
3. **Built for cheap tablets and 2G phones.** AA+ contrast, ≥44 px touch targets, ≥16 px body on mobile, ≥14 px on desktop, supports 7″ Android in landscape.
4. **Mozambican Portuguese.** All copy in PT-MZ; realistic names, provinces, districts, schools, subjects. Real institution names where they exist (MINEDH, DPEDH, INDE); fictional DED where it doesn't.
5. **Provenance always visible.** Grades show the entering professor; pautas show the approving director; library records show the contributing institution.
6. **Confirmation for academic action.** Lançar pauta final, anular matrícula, transferir aluno, atribuir falta disciplinar require two taps and structured justification.
7. **Children matter, but they are not the user we optimize for.** Children read what their teachers and parents enter — they are not a marketing audience. The Caderno do Aluno is calm and informative; it is not designed to "delight".

---

## 3. Color palette & roles

### 3.1 Brand
| Token | Hex | Role |
|---|---|---|
| `indigo-900` | `#1A1740` | Government strip, deepest chrome |
| `indigo-800` | `#241F58` | Sidebar fill, dark hero panels |
| `indigo-700` | `#322B7A` | Primary CTA, brand anchor, default action, links, focus |
| `indigo-600` | `#443A99` | Hover/active brand surfaces, selected nav |
| `indigo-100` | `#E5E2F2` | Tinted surfaces, selected chips, active nav background |
| `indigo-50` | `#F2F0F8` | Hover row tint on tables, subtle fills |

### 3.2 Subject palette (closed, academic content only)
| Token | Hex | Disciplina |
|---|---|---|
| `subj-port` | `#7A2E3D` | Português |
| `subj-mat` | `#1F4D7A` | Matemática |
| `subj-ciencias` | `#1B5E3F` | Ciências (Naturais, Bio, Quím, Fís) |
| `subj-hist` | `#7A5018` | História · Geografia |
| `subj-arte` | `#5C2D7A` | Educação Visual · Artística |
| `subj-ed-fis` | `#2E5C3A` | Educação Física |

> **Subject palette rule.** These are *the* six subject colours. They cannot be used as decorative palette anywhere else. A "Português" badge in the SIGE pauta uses the same `#7A2E3D` as the "Português" book cover in the Biblioteca catalogue. Consistency across surfaces is what allows a parent to glance at their child's Caderno do Aluno and recognize the subject from the colour alone.

> **What if a subject is missing.** If MINEDH adds Tecnologias de Informação (TI) or Educação Cívica as standalone disciplines, v0.4 expands the palette. v0.3 covers the six core subjects of the EP1, EP2, and ESG curricula.

### 3.3 Verification (limited)
| Token | Hex | Role |
|---|---|---|
| `green-700` | `#1B5E3F` | "Signed by director" / "Carimbada" / "Verified by State" |
| `green-100` | `#E4EFE9` | Verified surface tint |

### 3.4 Text · Surface (same across the family)
`ink #1A1A1A` · `ink-2 #3A3A3A` · `ink-3 #5E5E5E` · `bg #FAFAF7` · `bg-2 #F2F1EB` · `line #D9D7CF`

### 3.5 Status (academic state only)
| Token | Hex | Reserved for |
|---|---|---|
| `good-700` | `#1B6B3A` | Aprovado, presente, conforme, livro disponível |
| `amber-500` | `#C8911E` | Pendente, ausente justificado, aguarda director, livro requisitado |
| `red-500` | `#C2392A` | Reprovado, ausente injustificado, expirado, livro extraviado |

### 3.6 Library accent (Biblioteca Pública only)
| Token | Hex | Role |
|---|---|---|
| `sepia-700` | `#5C4A2E` | Reading-mode text headers, library nav active |
| `sepia-500` | `#8C7045` | Bar fills on reading-progress, accents |
| `sepia-100` | `#F2EAD6` | Reading-mode page background, library section tint |

The sepia palette is **scoped to the Biblioteca Pública surface** and to the reading-mode of any document opened from any surface. It is the only place where a non-indigo/non-status colour appears prominently. The choice signals "paper / reading / warmth" without inheriting institutional weight.

---

## 4. Typography rules

### 4.1 Family
- **Primary:** IBM Plex Sans (Latin Extended for full PT-MZ diacritics + Bantu coverage)
- **Mono:** IBM Plex Mono — exclusively for student IDs, school codes, processo numbers, OTP codes
- **Serif:** IBM Plex Serif — book titles, reading mode, library catalogue typography, formal academic documents (declarações, certificados)

### 4.2 Weights in production
- **400** body
- **500** UI labels, buttons
- **600** headings
- **700 forbidden**

### 4.3 Scale
Identical to the family scale (display 44 / h1 32 / h2 24 / h3 18 / h4 15 / lead 16 / body 14 / meta 12 / overline 11).

### 4.4 Mono
Plex Mono is used for: student IDs (`A-2026-EP2-INH-04412`), school codes (`ESC-INH-0124`), processo numbers (`P-2026-MAT-INH-0034`), OTP codes, pauta seal hashes. **Never as decorative type.**

### 4.5 Serif
Plex Serif is used for: book titles in the Biblioteca, reading-mode body in long-form readers, the formal name of a certificate ("Certificado de Conclusão do Ensino Primário"), and the name of a school in formal documents. **Never as UI chrome, button label, or table header.**

### 4.6 PT-MZ specifics
Same as the family — diacritics, currency formatting, dates, BI format. Specific to education:
- Ensino Primário (EP1: 1.ª–5.ª classe; EP2: 6.ª–7.ª)
- Ensino Secundário Geral (ESG: 8.ª–10.ª; ESG2: 11.ª–12.ª)
- Trimestres labelled `1.º Tri`, `2.º Tri`, `3.º Tri`
- Grade scale 0–20 (Portuguese tradition); pass mark 10
- Oral/escrito/auto-avaliação composition where applicable

---

## 5. Spacing & layout

### 5.1 Grid
- 8-px base unit
- Common steps: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64
- Page max width: **1440 px** for SIGE; **1200 px** for landing/biblioteca/matrículas; **360 px** phone for Caderno do Aluno; **1024 px** tablet for Caderno do Professor

### 5.2 Containers
| Container | Padding | Max width |
|---|---|---|
| Admin shell (SIGE) | 20 px | 1440 |
| Public landing | 24 px | 1200 |
| Phone (PWA) | 16 px | 360 |
| Tablet (Professor) | 16 px | 1024 |
| Biblioteca reading mode | 32 px | 720 (reading column) |
| Card | 14 px | — |
| Modal | 16 px | 520 |

### 5.3 Borders & corners
- Hairlines: 1 px solid `--line`
- Inner separators: 1 px solid `--line-2`
- Radii: 2 (badge), 4 (card / button / input), 6 (hero card). **Never** > 6.
- **Exception:** the **grade circle** (`.grade`) uses `border-radius: 50%` because a grade is a numerical mark, not a UI affordance — the circle reads as "stamp", not as "pill".

---

## 6. Components

### 6.1 Buttons, Inputs, Cards, Badges, Tables, Govt strip, Top bar, Side rail, Phone frame, Stepper, QR
Same component shapes as the family. Indigo replaces navy in CTAs, focus rings, active nav. Brand mark redrawn as a **stamped square with three horizontal bars and a vertical spine** — reading as an open book stamp.

### 6.2 Subject chip (`.subj`)
22-px height, 11-px text, white text on subject-coloured fill. Used in pauta tables, horário cells, plano de aula headers, book covers, library filters.

### 6.3 Grade circle (`.grade`)
36-px circle with 2-px border, mono numeric text. Variants: pass (green), fail (red), borderline 9–10 (amber), empty (dashed border). Used in pautas, the Caderno do Aluno's summary, and any grade reveal. **The circle is the canonical grade representation across the family** — never a star, never a thumbs-up.

### 6.4 Book card (`.book`)
2:3 aspect ratio cover, gradient fill from subject palette, title in serif on cover, author + year in sans below. Used in Biblioteca catalogue, Caderno do Aluno offline reader, library suggestions.

### 6.5 Bar (execution / progress)
Same as govdigital. Indigo default fill; sepia variant for reading progress; subject-coloured fills allowed only inside academic content.

### 6.6 Pauta cell
Tables with columns per subject and rows per student render grade circles in cells; an empty dashed circle means "ainda por lançar". Hover reveals the entering professor.

---

## 7. State patterns

### 7.1 Connectivity
Three states (online · sync queue · offline). SIGE uses sync queue counts in the rail; phone surface shows a banner when offline.

### 7.2 Academic state
Documents pass through: `rascunho` → `lançado pelo professor` → `validado pelo director` → `assinado / publicado`. Grades follow: `provisório` → `final` → (`recurso pendente` | `confirmado`).

### 7.3 Two-step confirmation
Required for: lançar pauta final, anular matrícula, transferir aluno entre escolas, atribuir falta disciplinar grave (≥3 dias), aprovar candidatura à matrícula em escola sobrelotada (override DPEDH).

### 7.4 Provenance footer
Every academic document carries: ano lectivo, escola, turma, processo, professor/director assinante, timestamp, and (where applicable) a verifiable QR linking back to the DED registry.

### 7.5 Empty states
Plain language. Never illustrations. Never a child-cartoon. "Sem trabalhos de casa esta semana" + a single ghost button "Ver horário" is enough.

### 7.6 No engagement mechanics
**Forbidden patterns**: streaks ("4 dias seguidos!"), confetti on grade reveal, "level up", points/coins, public leaderboards, push notifications about other students' achievements.

---

## 8. Accessibility

- AA+ contrast on all text including subject chips
- Focus rings: 2-px indigo-700, 1-px offset
- Touch targets ≥ 44 px on mobile and tablet
- Body floor: 16 px on mobile, 14 px on desktop
- Subject chips carry the subject name in text, never colour-only
- Grade circles include screen-reader text: "Matemática · 14 valores · aprovada"
- Library reading mode has a typography toggle (size, line-height, sepia/white)

---

## 9. Content & voice

### 9.1 Voice
- **Scholarly, not parental.** "A pauta do 1.º trimestre será publicada a 15 Abr." not "Quase lá! Veja já a sua pauta!"
- **Specific.** Always name the school, the trimester, the class, the professor.
- **Equal across stakeholders.** A parent reads the same factual tone as a director; a child reads the same factual tone as a professor.

### 9.2 Naming
- Real institutions where they exist (MINEDH, DPEDH provincial, INDE, IFP)
- Fictional **DED** is consistently labelled
- School names: realistic Mozambican (Escola Secundária da Polana, Escola Primária Completa de Maxixe, Liceu Eduardo Mondlane, Escola Comunitária de Mocímboa)
- Names of students / professors: realistic Mozambican (Naila Sumaila, Eulália Mussagy, Tomás Macuácua, Carlos Bila)

### 9.3 Numbers
- Student ID: `A-2026-EP2-INH-04412` (ano, ciclo, província, sequencial)
- Professor ID: `P-INH-2018-0042`
- School code: `ESC-INH-0124`
- Grade range: `0–20`, pass mark `10`

---

## 10. Cross-system relationship with Saúde Moçambique and Governo Digital

Educação Digital is the third sister system in the **Conceitos** family. They share:
- The Plex type system, the warm off-white canvas, the radius scale, the spacing grid
- Connectivity-pill pattern, two-step confirmation, provenance footer
- Borders before shadows, no-700-weight rule

They differ on:
- **Anchor colour** — green (Saúde), navy (Governo), **indigo (Educação)**
- **Vocabulary** — clinical state · civic state · **academic state**
- **Form factors** — Saúde leads with 7″ tablets in CS; Governo with desktops in conservatórias; **Educação leads with 10″ tablets in classrooms and a PWA in pockets**

Cross-system identity:
- **eBI of Governo Digital is the source of truth for student identity** — the SIGE consumes it for matrícula and transferência. A child's BI/registo de nascimento *is* their student identity foundation.
- **Saúde Moçambique cross-references** for school health checks (vacinação, vista, dentição) — the SIGE shows a "Saúde escolar" tab that links to the Saúde record (with parental consent visible).
- **DED never writes back to eBI**. Educação reads identity; it doesn't modify civic records.

---

## 11. What is intentionally *not* in the system

- **No engagement mechanics.** No streaks, no points, no badges-as-trophies, no public leaderboards.
- **No edutech AI tutoring claims.** v0.3 doesn't show generative AI for students; it would be inappropriate without curriculum-level review.
- **No avatars with photos by default.** Initials only for UI; photos appear only on official cartões do aluno (verification documents) — never as "social profile pictures".
- **No private messaging between students.** The platform is school-mediated.
- **No advertising, no third-party trackers, no "Login with Google".**
- **No dark mode** in classroom surfaces (sala de aula has fluorescent or sun light; dark mode reads as "leisure"). The Biblioteca Pública has a sepia reading mode — a deliberate exception.

---

## 12. Open questions for v0.4

- Bantu language toggle (Macua, Changana, Sena) — pending UX research with EP1 students
- USSD entry-point for matrícula status check — flow drafted, not built
- Print stylesheet for the certificado de conclusão — needs MINEDH-prescribed format
- Voice/audio support in the Caderno do Aluno for low-literacy parents — research not started
- Accessibility audit by a specialist — current AA+ claim is internal QA only
- Tactile / printed companion docs — what does the printed pauta look like when sent home?

---

*This document is the source of truth for cross-surface decisions. When a surface document contradicts this document, this one wins.*
