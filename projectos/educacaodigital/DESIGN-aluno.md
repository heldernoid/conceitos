# DESIGN-aluno.md — Surface 3 · Caderno do Aluno

**Status:** v0.3 · Abril 2026
**Form factor:** Mobile PWA, Android-first. Floor: 360 × 640 px (low-end Android, 2G/3G). Ceiling: tablet, but optimized for phone.
**Primary users:** Alunos (8 anos+). **Co-users:** Encarregados de educação (parents/guardians) — same app, different mode toggle.
**Setting:** Em casa, no recreio, no transporte público, em casa do tio. Frequently shared phones (one phone for the family). Often patchy 2G.

---

## 1. Product purpose

The Caderno do Aluno is the digital counterpart to the physical caderneta — the booklet that goes home with the child carrying the week's TPC, the trimester's pauta, the school's mensagens, and the parent's signature lines. Three priorities:

1. **The child can read what the school says about them.** Pauta, TPC, mensagens, horário — without filtering, without theatre.
2. **The encarregado can act.** Justificar faltas, submeter recurso, confirmar mensagens — directly, without going to the school.
3. **Both can read.** Biblioteca offline (manuais INDE, literatura moçambicana) is downloadable for offline reading.

What it deliberately is *not*:
- Not a social network. Alunos cannot message other alunos in the app.
- Not a gamified study tool. No streaks, points, leaderboards, badges-as-trophies.
- Not a parental surveillance tool. The encarregado sees what the school sends — not the child's private notes.
- Not a chat with the professor. Mensagens are mediated by the direcção via SIGE.

---

## 2. Information architecture

```
Onboarding
├─ BI / Cédula (eBI lookup)
├─ Telefone do encarregado (OTP) · consentimento parental para <18
└─ Selecção de modo (este telemóvel é meu / partilhado com encarregado)

[Hoje] [Pauta] [TPC] [Biblioteca] · 4-tab bottom nav

└─ Hoje
   ├─ Próxima aula (countdown)
   ├─ TPC com prazo próximo
   └─ Mensagens da escola
└─ Pauta
   ├─ Trimestre actual (provisório)
   ├─ Trimestres anteriores
   ├─ Detalhe de nota (componentes + comentário do professor)
   └─ Submeter recurso (acção do encarregado)
└─ TPC
   ├─ Lista por prazo
   ├─ Detalhe + anexos
   └─ Submeter (foto/scan/texto)
└─ Biblioteca
   ├─ Descarregados (offline)
   └─ Catálogo público
└─ Mais
   ├─ Horário
   ├─ Frequência (próprias faltas)
   ├─ Justificar falta (encarregado)
   ├─ Mensagens da escola
   └─ Definições · partilha do telemóvel
```

---

## 3. Critical flows

### F1 — Onboarding com consentimento parental
Step 1: BI ou cédula do aluno. Step 2: telefone do encarregado de educação. Step 3: OTP enviado para encarregado. Step 4: consentimento parental explícito (para <18) — checkbox claro: "Autorizo que [Nome] receba a sua pauta, TPC e mensagens da escola nesta App". Step 5: modo do telemóvel (apenas aluno · partilhado com encarregado · apenas encarregado).

### F2 — Hoje
Carrega rápido em 2G. Próxima aula com countdown. 1–3 cards de TPC pendente. 0–2 mensagens novas da escola. Sem feed, sem notificações de outras pessoas.

### F3 — Pauta (read-only para aluno)
Vista por trimestre. Cada disciplina mostra a nota como **círculo** (mesmo componente que o SIGE e o Professor) — verde aprovado, âmbar limiar, vermelho reprovado. Tap revela detalhe: componentes (avaliação contínua, prova escrita, oralidade) + comentário do professor. **Tom calmo** — sem confetti, sem "🎉".

### F4 — Detalhe de nota e recurso
Detalhe da nota mostra a composição. Botão "Submeter recurso" disponível durante 10 dias após validação — **só visível ao encarregado**, não ao aluno. Submissão: campo de justificação ≥80 chars, anexo opcional (foto do teste), confirmação OTP do encarregado.

### F5 — TPC
Lista ordenada por prazo. Cada cartão mostra: disciplina (chip colorido), título, prazo, estado (a fazer / em curso / submetido / corrigido). Detalhe: instruções, anexos (manual, foto do quadro), botão "Submeter" (foto ou texto). Após correcção, mostra a nota (se houver) e o comentário.

### F6 — Justificar falta (encarregado)
A escola registou uma falta. O encarregado, com OTP, pode justificar com motivo (doença, viagem, luto, outro), texto opcional, e anexo opcional (atestado médico). A justificação chega ao SIGE para aprovação do director.

### F7 — Submeter recurso de nota (encarregado)
Visível apenas se modo encarregado activo. Lista de notas em recurso possível (10 dias após validação). Submissão chega ao SIGE → director → professor → resposta na App.

### F8 — Biblioteca offline
Lista de livros descarregados. Tap abre em modo leitura (sepia, Plex Serif, ajuste de tamanho). Catálogo público acessível em modo online. Trabalhos atribuídos pelo professor pré-marcados.

### F9 — Mensagens da escola
Read-only. Mensagens da direcção, do professor (via direcção), reuniões, eventos. Sem reply directo — para responder, ir à escola ou ligar.

### F10 — Modo partilhado (vários filhos)
Se uma encarregada tem 3 filhos, todos aparecem no swiper do topo. Cada filho tem a sua própria Caderno. Identidade visual diferenciada (cor de turma + iniciais).

---

## 4. Components & patterns

| Component | Caderno do Aluno |
|---|---|
| Phone frame | 360 × 760 in mocks |
| Top bar | 48 px, brand + connectivity + child swiper |
| Bottom nav | 60 px, 4 tabs (Hoje · Pauta · TPC · Biblioteca) |
| Mensagem card | 88 px row, ícone disciplina, título, timestamp |
| Grade row | Grade circle + disciplina + média provisória |
| Book card | 96 × 144 cover, title in serif |
| Reading mode | Sepia background `--sepia-100`, Plex Serif body, 1.7 line-height |

---

## 5. Critical UI states

### 5.1 Pauta provisória
Banner indigo: *"Pauta do 1.º Trimestre ainda em curso. Notas finais publicadas após validação do director."*

### 5.2 Sem rede
*"Sem rede. A última pauta carregada é de 04 Abr."* Pauta cached. TPC list cached. Biblioteca offline available. Submit actions enfileirados.

### 5.3 Reprovação
Vermelho na nota, mas tom calmo. *"Reprovado a Matemática · 8 valores."* Detalhe mostra as componentes e o comentário do professor. **Não há mensagem motivacional gerada pela App** — se há acompanhamento, é o professor que escreve.

### 5.4 Encarregado com 3 filhos
Top swiper carries 3 avatars. Notification badges per child.

### 5.5 Falta detectada
Banner âmbar: *"A escola marcou falta a 14 Abr · Português. Quer justificar agora?"*

---

## 6. Voice & tone

- **Scholarly, not parental.** A criança recebe o mesmo tom factual que o adulto.
- **No exclamation marks.** "Pauta publicada." not "Pauta publicada!"
- **No emoji.** A nota é a nota.
- **Specific.** Sempre nomeia escola, trimestre, professor, disciplina.
- **No motivational copy.** "Reprovou" é "reprovou". A motivação cabe ao professor e ao encarregado, não à App.

---

## 7. Privacy & consent

- **Consentimento parental para <18** — registado, revogável.
- **Modo partilhado** — se o telemóvel é partilhado, é necessário PIN do encarregado para aceder a acções de encarregado (recurso, justificação, mensagens privadas).
- **Sem perfil público.** Sem sugestões de amigos. Sem foto do aluno (excepto cartão oficial).
- **Sem rastreio analítico** — DED guarda apenas o estritamente necessário (logins, sync events).
- **Direito ao apagamento** — após conclusão do ano lectivo, o encarregado pode pedir limpeza dos dados pessoais (não académicos — esses ficam no registo nacional).

---

## 8. Cross-system relationship

Caderno do Aluno reads from:
- **eBI** — identity foundation (one-time)
- **SIGE** — pautas validadas, mensagens da direcção, faltas
- **Caderno do Professor** — TPC, mensagens via direcção
- **Biblioteca Pública** — catálogo, livros descarregáveis

Caderno do Aluno writes to:
- **SIGE** — recursos de nota, justificações de falta, entregas de TPC

---

## 9. Accessibility

- **Body floor:** 16 px. Reading mode adjustable to 18, 20, 22 px.
- **Touch targets:** ≥44 px.
- **Contrast:** AA+ across the indigo + sepia variants.
- **Screen reader:** all grade circles labelled "Disciplina · valor · estado".

---

## 10. Open questions for v0.4

- Bantu language toggle for low-literacy parents (Macua, Changana, Sena)
- Audio version of pauta for parents who don't read fluently
- USSD entry-point for status check (sem internet)
- WhatsApp delivery alternative for mensagens (encarregados que não usam a App)

---

*Authoritative for the Caderno do Aluno surface. DESIGN-system.md wins on conflict.*
