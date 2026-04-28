# DESIGN-professor.md — Surface 2 · Caderno do Professor

**Status:** v0.3 · Abril 2026
**Form factor:** 10″ Android tablet, **landscape**, single-handed-friendly. Floor: 1024 × 600 px (low-end Android tablets distributed by DED). Ceiling: any tablet.
**Primary user:** Professor (EP1, EP2, ESG, ESG2). Secondary: substituto, coordenador pedagógico que assiste à aula.
**Setting:** Sala de aula. Classroom light is fluorescent or sun glare; the tablet is held in one hand while a chalk is in the other. Sometimes shared between professores em postos pequenos.

---

## 1. Product purpose

The Caderno do Professor is the digital substitute for the **caderno cinzento** that every Mozambican professor carries to class — the physical notebook with the day's plan, the chamada, marks scribbled in the margins, and the disciplinary notes. It is **not** a replacement for the curriculum (INDE owns that), nor for the teacher's personal pedagogical voice. It is a **scaffold** that gets the busy-work out of the way so the professor can teach.

Three priorities in order:
1. **Speed in class.** Chamada in <60 seconds for a 36-student turma. Lançar nota in 2 taps.
2. **Survives offline.** Sala de aula often has no rede — the app works without it for the entire day.
3. **Honest provenance.** Every grade and observation carries the professor and the timestamp; nothing happens "automatically" without a name.

What it deliberately is *not*:
- Not a chat app for parents (mensagens go through SIGE → SMS gateway, not direct).
- Not a content authoring tool — planos de aula are written in plain text or attached PDF; INDE recursos are linked, not embedded.
- Not a peer comparison surface — a professor doesn't see *other* turmas' average to compare against theirs.

---

## 2. Information architecture

```
Sign in (operator + escola + turno · 2FA SMS)
└─ Hoje
   ├─ Próxima aula (countdown)
   ├─ Turmas do dia
   └─ Tarefas pendentes (chamadas, notas, observações)
└─ Aula em curso
   ├─ Chamada (lista de alunos · presente / falta / atraso)
   ├─ Plano da aula (objectivos, conteúdo, exercícios)
   ├─ Lançar nota individual
   ├─ Observação pedagógica (texto livre)
   └─ Trabalho de casa (anexo, prazo)
└─ Pautas
   ├─ Por trimestre · disciplina · turma
   ├─ Componer (avaliação contínua + escrita + oralidade)
   └─ Lançar para validação do director
└─ Comunicação
   └─ Mensagem ao encarregado (via SIGE → SMS)
└─ Recursos
   └─ Manuais INDE · Biblioteca Pública
└─ Offline / Sync
```

A 4-tab bottom bar: **Hoje · Aula · Pautas · Mais**. Top bar carries: brand, current turma badge, connectivity pill, identity. Critical-path actions are reachable in ≤ 2 taps from "Hoje".

---

## 3. Critical flows

### F1 — Sign in & turno bind
Operator + escola code + password. SMS OTP. Bind to turno (manhã / tarde / noite) — important because a professor may teach in two different schools across shifts.

### F2 — Hoje
Header shows the date, the school, the turno, and the next aula (countdown). Below: a card per aula of the day with chamada / nota / observação status indicators (done / pending). Tarefas pendentes pile shows things from yesterday that aren't sealed (e.g. an unmarked chamada).

### F3 — Chamada (≤60 s for 36 alunos)
Default state: all alunos `presente` (toggle to `falta` or `atraso` on tap). Mass actions: "Marcar todos presentes" / "Iniciar com todos faltosos" depending on professor preference. Chamada is timestamped; once sealed at end of aula, no edits without director countersignature.

### F4 — Plano de aula
Pre-loaded from the professor's planos (created earlier or copied from INDE template). Three blocks: objectivos · conteúdo · exercícios. Inline checkbox to mark "dado" / "não dado" for accountability. Time on task tracked passively.

### F5 — Lançar nota individual (avaliação contínua)
Tap an aluno → "Adicionar nota" → seleccionar tipo (oral · escrita · trabalho · prova de unidade) → introduzir 0–20 → opcional comentário → guardar. The note is a **draft** until the trimester pauta is composed and submitted.

### F6 — Observação pedagógica
Text-only note tied to an aluno. Tone guide visible: "Descreva comportamento, não juízo de carácter." Examples shown collapsed. Sensitive observations (saúde, família) flagged separately and shared only with the director, not exposed to the encarregado in the App.

### F7 — Mensagem ao encarregado
Templated SMS sent through SIGE (not directly from the device). Templates: ausência, comportamento, reunião, parabéns, urgência. The message is logged in the SIGE family tab.

### F8 — Trabalho de casa
Anexo (PDF, foto, link Biblioteca), prazo, distribuição (toda a turma · grupo). Aparece no Caderno do Aluno e na App do Encarregado.

### F9 — Compor pauta trimestral
At end of trimestre, the professor composes the final pauta from accumulated drafts. The interface shows: avaliação contínua (média de N notas) · prova escrita · oralidade · final calculada com ponderação INDE 30/50/20. The professor can override, with mandatory justification. Submeter → vai para o SIGE para validação do director.

### F10 — Sem rede (offline)
Banner amber: *"Sem rede. Tudo o que fizer fica guardado e sincroniza assim que houver ligação."* All flows work; the sync indicator shows count of pending events. Cross-system calls (eBI lookup, Saúde) are disabled until rede.

---

## 4. Components & patterns

| Component | Caderno do Professor |
|---|---|
| Tablet shell | 1024 × 680 frame in mocks, 16 px padding |
| Top bar | 56 px, school + turno + connectivity |
| Bottom nav | 64 px, 4 tabs, 24 px icons, 11 px labels |
| Chamada cell | 64 px row · aluno avatar + name + 3-state segmented |
| Plano de aula | Numbered list with checkbox + time-on-task |
| Nota chip | Same grade circle as SIGE, sm variant |
| SMS template | Pre-filled, professor edits, ≤160 chars |

The tablet form factor uses larger touch targets (44 px floor, 56 px preferred) and respects Android system gesture areas at the screen bottom.

---

## 5. Critical UI states

### 5.1 Chamada não fechada
End-of-aula prompt: *"A chamada de Mat 8.ª A ainda está aberta. Fechar agora?"* Cannot close without confirming.

### 5.2 Aluno não reconhecido
If the professor has a substitute and an unknown aluno (newly transferred, not yet in roster), a "+ Adicionar aluno" temporary slot is created — flagged for the director to resolve.

### 5.3 Pauta com nota vazia
*"3 alunos sem nota de oralidade. Não pode lançar."* Block + jump-to-row.

### 5.4 Observação sensível
*"Esta observação parece sensível (saúde, família). Quer que fique apenas visível ao director?"* Default no, with a single tap to convert.

### 5.5 Rede instável
Sync queue counter visible. Failed sync after 3 retries → red badge "Sincronização a falhar — contacte DED".

---

## 6. Voice & tone

- Direct, like the chalkboard. Short sentences.
- Verbs in the imperative for the professor's own actions ("Lance a nota", "Confirme a chamada").
- No exclamation marks, ever.
- No motivational copy ("Vamos lá, pode fazer mais!").
- The professor is treated as a competent professional. The app does not nag.

---

## 7. Cross-system relationship

Caderno do Professor reads from:
- **eBI / SIGE** — student identity (BI, photo for cartão, encarregado)
- **INDE recursos** — plano de aula templates, manuais
- **Biblioteca Pública** — para anexar trabalho de casa

Caderno do Professor writes to:
- **SIGE** — pautas (drafts and submissions), chamada, observações pedagógicas
- **Caderno do Aluno** — TPC, mensagens via direcção
- **App do Encarregado (modo encarregado do Caderno do Aluno)** — mensagens via SIGE

---

## 8. Open questions for v0.4

- Multi-professor co-teaching (TI co-teach com Mat, EVT co-teach com EF) — model not finalized
- Recovery if tablet shared between turnos and one professor logs out mid-aula — graceful handover not designed
- Voice-to-text for observações pedagógicas (offline) — research not started
- Print stylesheet for caderno físico de cópia — out of scope v0.3

---

*Authoritative for the Caderno do Professor surface. DESIGN-system.md wins on conflict.*
