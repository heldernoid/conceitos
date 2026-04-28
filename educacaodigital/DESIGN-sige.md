# DESIGN-sige.md — Surface 1 · SIGE · Sistema Integrado de Gestão Escolar

**Status:** v0.3 · Abril 2026
**Form factor:** Web app on desktop (1280+ floor); secondary support for 10″ tablets in landscape (for visiting inspectors).
**Primary users:** Directores escolares, directores adjuntos, secretários escolares, coordenadores pedagógicos. Secondary: DPEDH provincial inspectors, DED admins.
**Setting:** Direcção da escola (a small office, often shared with the secretariat), DPEDH provincial offices for cross-school views.

---

## 1. Product purpose

A single national school-management record. Every school, every turma, every professor, every aluno, every aula, every nota — retrievable from any school in the system, with permissions tightly scoped (a director sees their school; a DPEDH inspector sees their province; only DED sees nationally).

The SIGE optimizes for three things, in order:
1. **Running the daily business of the school** — turmas, horários, frequência, pautas, comunicação com encarregados.
2. **Producing accountable academic records** — pautas trimestrais validated by the director, certificados de conclusão signed and queued to the DED registry.
3. **Reporting upwards** — to DPEDH (province) and MINEDH (national) without duplicate data entry.

It deliberately does *not* try to be: a payroll system for teachers (that's MEF/MINEDH), a procurement system for school supplies (that's e-PA via Orçamento Aberto), or a calendar system for inter-school sports.

---

## 2. Information architecture

```
Sign in (director email + password + 2FA SMS) → Escola selector → Painel
└─ Painel
   ├─ KPIs (alunos · professores · frequência · sync)
   ├─ Pautas a validar
   ├─ Faltas anómalas
   └─ Avisos da DPEDH
└─ Turmas
   ├─ Lista (por classe, ano, turno)
   ├─ Detalhe → alunos · professores · horário · pautas
   └─ Criar nova turma
└─ Alunos
   ├─ Pesquisar (BI · processo · nome)
   ├─ Ficha do aluno (5 abas: Visão geral · Pautas · Frequência · Família · Saúde)
   └─ Transferir aluno (cross-system call)
└─ Professores
   ├─ Lista, distribuição, carga horária
   └─ Ficha do professor
└─ Pautas
   ├─ Por trimestre · turma · disciplina
   ├─ Validar · assinar · publicar
   └─ Recursos pendentes
└─ Frequência
   ├─ Por turma · diária · semanal · mensal
   └─ Faltas anómalas (auto-detectadas)
└─ Saúde escolar
   └─ Cross-link com Saúde Moçambique (vacinação, vista, dentição)
└─ Relatórios
   ├─ Para DPEDH (mensal)
   └─ Para MINEDH/INDE (anual)
```

Top bar carries: brand, primary nav, connectivity pill, identity badge with school + role. Identity is one click from sign-out and "switch escola" (for inspectors).

---

## 3. Critical flows

### F1 — Sign in & escola bind
Three-step. Step 1: email + password. Step 2: SMS OTP — required because directors approve pautas. Step 3: bind to escola. For multi-school inspectors, escola is a switcher, not a bind.

### F2 — Painel
Above the fold: today's KPIs (alunos matriculados, professores ao serviço, frequência média da semana, estado de sincronização). Pautas a validar pile. Faltas anómalas card. Avisos from DPEDH (often calendar-related: feriados, exames, datas-limite).

### F3 — Turmas (lista e detalhe)
List sorted by classe (1.ª–12.ª) and turno (manhã, tarde, nocturno). Detail page shows: aluno roster (with quick-jump to fichas), assigned professores per disciplina, horário grid (subject-coloured cells), pauta state per trimestre, frequência summary.

### F4 — Ficha do aluno
Five tabs: Visão geral · Pautas · Frequência · Família · Saúde. Visão geral shows BI (read from eBI Governo Digital), responsáveis (encarregados de educação), turma actual, histórico de turmas. The Saúde tab is read-only, fed by a cross-system call to Saúde Moçambique with the parent's consent flag visible — if no consent, the tab shows "Sem partilha de dados de saúde" and a button to request consent.

### F5 — Validar pauta trimestral (two-step)
The professor lança grades in the Caderno do Professor. They arrive in the SIGE as "lançadas". The director reviews: list of students, grades, suspicious patterns (e.g. all 20s, a sudden drop), and the professor's notes. Two-step confirmation: review with checkbox "Verifiquei a coerência das notas" + button "Validar pauta de [Disciplina · Turma · Trimestre]". On confirmation, the pauta is signed, becomes visible to the aluno and encarregado, and is queued for the DED registry.

### F6 — Recurso de nota
An encarregado submits a recurso via the Caderno do Aluno. It arrives in the SIGE recursos pile. The director reviews, contacts the professor for a justification (text), then decides: deferido (note re-opens, professor revises) or indeferido (justifica e arquiva). Always notify the encarregado with the decision in plain language.

### F7 — Transferir aluno
Cross-system call: the SIGE looks up other schools by name/distrito. If the destination school has a DED-registered SIGE, the transfer is one-click; if not (private school, escola comunitária outside the registry), the SIGE generates a transferência document (PDF + QR) for manual delivery.

### F8 — Faltas anómalas
Auto-detected: ≥3 faltas seguidas sem justificação, ≥10 faltas no trimestre, padrão semanal (sempre 6.ª-feira). The director sees the case, contacts the encarregado (system suggests SMS template), and logs the conversation. If no contact possible in 7 dias, escalate to the social worker / acção comunitária.

### F9 — Saúde escolar
The Saúde escolar tab cross-references Saúde Moçambique. The director sees:
- Vacinação status per aluno (válida / em atraso / não disponível)
- Resultado da rotina anual (vista, dentição, peso/altura)
- Casos crónicos sinalizados pelo CS (asma, diabetes, anemia)
The director cannot see clinical detail — only flags and suggested school actions.

### F10 — Relatórios para DPEDH
Monthly report auto-generated: matrículas no mês, transferências, faltas, faltas disciplinares graves, pautas em atraso, infraestrutura (carteiras, livros, casas de banho). The director reviews, comments, and submits. The DPEDH inspector sees the report in their dashboard.

---

## 4. Components & patterns

| Component | SIGE-specific |
|---|---|
| Top bar | School badge "Escola Sec. da Polana · Maputo" |
| Side rail | 220 px indigo-900 fill |
| Pauta table | Grade circles in cells; subject chip in header |
| Horário grid | Subject-coloured cells, mono time labels |
| Aluno ficha | 5 tabs; Saúde tab is a cross-system embed |
| Two-step modal | For pauta validation, transferência, anulação de matrícula |
| Provenance footer | Pauta carries director, school, trimester, validation timestamp |

---

## 5. Critical UI states

### 5.1 Pauta com padrão suspeito
Banner: *"Toda a turma com nota ≥17 — confirme a coerência antes de validar."* or *"Nota média desta turma desceu 4 valores face ao trimestre anterior."*

### 5.2 Aluno com 5 faltas seguidas
Red strip on Ficha: *"5 faltas seguidas (15–19 Mar). A escola deve contactar o encarregado de educação."*

### 5.3 Director de transição (escola sem director nomeado)
Banner: *"Esta escola está sob direcção interina. Acções de validação requerem contra-assinatura da DPEDH."*

### 5.4 Sem rede
Same offline pattern as eBI: dashboard works, validation queues, no cross-system Saúde call.

### 5.5 Ano lectivo a fechar
60 days before year-end, a banner reminds: *"Ano lectivo 2026 termina a 14 Dez. Confirme pautas finais até 30 Nov."*

---

## 6. Academic-state vocabulary

| State | Tone | Verb |
|---|---|---|
| Pauta · rascunho (no Professor) | grey | — |
| Pauta · lançada (no SIGE) | indigo | Validar / Devolver |
| Pauta · validada | green | Publicar |
| Pauta · publicada | green | Imprimir |
| Pauta · em recurso | amber | Decidir recurso |
| Aluno · matriculado | grey | — |
| Aluno · transferido | indigo | Ver destino |
| Aluno · desistente | red | Reactivar |
| Falta · justificada | grey | — |
| Falta · não justificada | amber | Notificar encarregado |
| Falta · disciplinar | red | Iniciar processo |

---

## 7. Two-step confirmations

- **Validar pauta final** — checkbox "Verifiquei a coerência" + OTP do director
- **Anular matrícula** — justificação ≥80 chars + tipo (transferência / desistência / falecimento) + OTP
- **Transferir aluno cross-school** — seleccionar escola destino + motivo + OTP
- **Atribuir falta disciplinar grave** — tipo da infracção + duração da suspensão + comunicação ao encarregado

---

## 8. Cross-system calls

SIGE consumes:
- **eBI (Governo Digital)** — student identity foundation; encarregado identity foundation
- **Saúde Moçambique** — school health flags (with consent)
- **Caderno do Professor** — pauta drafts, attendance, observations
- **Caderno do Aluno** — recursos, justificações de falta, mensagens

SIGE writes to:
- **DED national registry** — validated pautas, certificados de conclusão, transferências
- **DPEDH** — monthly reports
- **Caderno do Aluno** — pauta validated event, mensagens da direcção

---

## 9. Performance & offline

- First paint < 1.5 s on a 2018 desktop
- Pauta table for 40 students renders < 800 ms
- Last 30 days of activity cached for offline review
- Validation cannot happen offline (security ceiling)
- Sync queue retains up to 500 events; visible counter in rail

---

## 10. Open questions for v0.4

- Multi-shift directors (escolas with morning + afternoon + nocturno) — how does shift bind to a director's session?
- Print stylesheet for pauta — needs MINEDH-prescribed format
- Inspector mobile mode — currently desktop-only
- AI assistance for letter drafting (e.g. "draft SMS to encarregado") — out of scope for v0.3

---

*This document is authoritative for the SIGE surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins.*
