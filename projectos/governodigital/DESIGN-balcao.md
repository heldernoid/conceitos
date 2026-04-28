# DESIGN-balcao.md — Surface 3 · Balcão Digital

**Status:** v0.3 · Abril 2026
**Form factor:** 10″ tablet in landscape (1024×768 floor) at the counter, optionally a 14″ second screen.
**Primary users:** Operadores BAÚ, ajudantes de conservatória, atendedores de postos avançados.
**Setting:** Postos BAÚ (≈230 nationwide), postos avançados em zonas rurais, pop-up registration drives.

---

## 1. Product purpose

The Balcão is where citizens who cannot — or prefer not to — use the App do Cidadão get the same service. It is the *physical bridge* between citizen and Estado: a tablet on the counter where an operator runs the same wizards, but on behalf of the citizen, with explicit identification and consent.

Three jobs, in order:

1. **Identify the citizen quickly** — by QR scan from the App do Cidadão (when they have one), by physical BI, or by name + parents + DOB if they don't.
2. **Run the same requerimento wizard** as the App, but with the operator filling in. The citizen is named on every screen, every confirmation; the operator is a custodian, not a user.
3. **Move the queue** — show ticket order, predicted wait, who's next, and what they came for, so the posto can plan and citizens are not surprised.

It deliberately does *not* try to be: a financial register, a stock manager for the BAÚ counter, an HR system for operators (those are separate tools).

---

## 2. Information architecture

```
Sign in (operator + posto + 2FA SMS) → Painel da fila
└─ Painel da fila
   ├─ Tickets do dia (A-001, A-002, …)
   ├─ Em curso (no balcão agora)
   └─ Próximos (a chamar)
└─ Identificar cidadão
   ├─ Scan QR (App do Cidadão)
   ├─ BI número
   └─ Sem documento → Criar registo / pedir override
└─ Atendimento (em curso)
   ├─ Ficha do cidadão (read-only mirror of eBI)
   ├─ Wizard assistido (5 passos)
   └─ Pagamento + recibo
└─ Fim de dia
   ├─ Fecho de caixa (numerário · M-Pesa · eMola)
   ├─ Tickets pendentes
   └─ Sincronização
```

A persistent **side rail** (220 px) carries posto identity and primary nav. The main panel is a queue or an active atendimento. **Identity badge** with operator and posto is always visible top-right; click to switch posto or sign out.

---

## 3. Critical flows

### F1 — Sign in & posto bind
Same three-step pattern as eBI (operator + password + SMS OTP), with an additional posto bind. The shift defaults to today; switching posto re-authenticates.

### F2 — Painel da fila
Queue view: tickets sorted by call order, with type, citizen name (if pre-checked-in via App), predicted duration, and current state (à espera / em curso / concluído / saiu da fila). KPIs in the rail: tickets por atender, tempo médio de espera, tickets concluídos hoje.

### F3 — Chamar próximo
A single button "Chamar A-016 — Sumaila Dauto · Certidão de nascimento". Hits the queue display in the lobby, marks the ticket "em curso", and opens the citizen identification screen.

### F4 — Identificar via QR
Default mode for citizens with the App. The operator taps "Ler QR", the camera opens (or if a QR scanner is hardware-attached, that), the citizen shows the QR from their App, and the system loads the ficha. The QR is the same dynamic-rotating one from the App, validated server-side, so a screenshot from yesterday won't work.

### F5 — Identificar sem App
Three sub-flows:
- **Com BI físico**: operator types the BI; system loads the ficha
- **Sem BI**: name + DOB + parents → search; if a single match, load; if multiple, disambiguate; if none, offer "novo registo de nascimento" or "override de emergência"
- **Cidadão recém-nascido (a registar)**: novo registo de nascimento path

### F6 — Atendimento (em curso)
Split layout: ficha do cidadão (left, read-only) + wizard (right). The wizard is the same eBI 5-step wizard, but with one banner pinned at top: *"Atendimento de Felisberta S. Cuamba · BI 110100099876 C · ticket A-016 · operador F. Chongo"*. Every confirmation modal explicitly names the citizen, not "o cidadão".

### F7 — Pagamento no balcão
Three rotas: M-Pesa push (to the citizen's phone), eMola, or numerário (counter cash). Cash is recorded explicitly with a denomination breakdown — the system asks how the operator received the cash (which notes), to make end-of-day cash close auditable.

### F8 — Recibo & impressão
After signing, the system shows a receipt preview that prints to the counter receipt printer (where one exists) or generates a PDF that can be shared to the citizen's phone via QR. The receipt always contains: process number, citizen, operator, posto, amount, payment method, date/time, and a verification QR.

### F9 — Final do atendimento
Operator marks "atendimento concluído", returns to the queue. The system asks for an optional satisfaction tap from the citizen on a separate small screen (3 levels: bom · médio · mau). This is never shown to the operator.

### F10 — Fecho de dia
End of shift: the system shows numerário esperado (sum of cash payments today) vs numerário declarado (operator counts and types the total). If they don't match, a discrepância is logged and routed to the conservador and to UGD audit. Cash discrepancies do *not* block end-of-day — the discrepancy is an audit record, not a punishment trigger.

---

## 4. Components & patterns

| Component | Balcão-specific notes |
|---|---|
| Side rail | 220 px navy-900 fill. Carries posto badge "BAÚ Inhambane Central · Balcão 2", primary nav, and current ticket. |
| Main panel | Single panel always — operators do not multitask. |
| Queue table | Compact, sticky header, sort by ticket order default. |
| Citizen banner | Pinned at top of every atendimento screen — operator cannot dismiss. |
| Wizard | Same as eBI. Inputs are 44 px tall (tablet ergonomics). |
| Cash dialog | Denomination breakdown grid (200 / 500 / 1000 MT notes), running total. |
| Receipt preview | A4 portrait preview in a panel; print/share/PDF actions below. |
| End-of-day modal | Two-step: count cash, confirm; system asks for explicit override if mismatch. |

---

## 5. Critical UI states

### 5.1 No QR / no BI / no documents
The "sem documento" screen is the empty state, not an error. It frames the situation as routine: *"O cidadão não tem documentos consigo. Pode ainda assim ser atendido — registe os dados e veja se encontramos correspondência. Caso contrário, abra um override de emergência."*

### 5.2 Citizen who is also in another queue
If the same BI is open in another posto in the last 30 minutes, a banner: *"Atendimento aberto em Maputo Central há 12 min. Continuar aqui pode duplicar o requerimento."*

### 5.3 Pagamento falhado
M-Pesa push timed out → the operator sees a clear retry / fallback to numerário, never a generic "tente novamente".

### 5.4 Final do dia com discrepância
A red banner persists in the rail until the conservador acknowledges. The operator can clock out; the conservador sees the discrepância on their next sign-in.

### 5.5 Posto offline
The painel da fila still works for "chamar próximo"; identification works by BI lookup against the local cache; new requerimentos go to the offline queue. End-of-day cash close still works (offline cash record).

---

## 6. Civic-state vocabulary at the Balcão

The Balcão re-uses the closed civic-state vocabulary from DESIGN-system.md. One addition unique to this surface:

| State | Tone | Verb |
|---|---|---|
| Em fila | grey | Chamar |
| Em curso (no balcão) | blue | Continuar |
| Concluído | green | Imprimir recibo |
| Saiu da fila | amber | Reabrir / Marcar ausente |

---

## 7. Two-step confirmations

Specific to Balcão:

- **Receber numerário** — operator types denomination breakdown; confirmation labels the consequence ("Registar MZN 250,00 em numerário").
- **Atendimento sem documentação** — operator confirms the citizen is the person the record refers to (by community knowledge or by witness operator). Justification ≥ 80 chars.
- **Fechar dia com discrepância** — modal explicitly states the difference and that the conservador will be notified.

---

## 8. Cross-system calls

The Balcão calls into:

- **eBI** — read citizen identity, write atendimento records, write requerimento drafts and submissions
- **App do Cidadão** — write a "documento assinado" event when applicable (so the citizen sees the receipt arrive in their phone in real time, even if they don't have the App now they can re-bind it later)
- **Auditoria** — every read and every cash event is logged

The Balcão does *not* call directly into Saúde Moçambique (health is a separate counter and a separate session). Cross-Estado handoffs happen via the eBI source-of-truth.

---

## 9. Performance & ergonomics

- 44-px inputs and buttons (tablet)
- Side rail collapses to 64 px on 1024-wide tablets to give the wizard more room
- Queue paint < 1 s on a 2020 Android tablet
- The receipt printer is queried on app start; if not present, the print button is replaced by "Gerar PDF e enviar para o cidadão"
- Operator cannot accidentally close an atendimento — closing requires confirmation

---

## 10. Open questions for v0.4

- Hardware fingerprint reader at the counter — flow stubbed, not built
- Citizen-facing second screen (satisfaction tap, document preview) — drafted only as concept
- How to handle the citizen who shows up with a printed receipt and asks "where's my BI?" — needs a "consulta de processo" lookup independent of the wizard
- Print stylesheet for the BAÚ paper format — out of scope until UGD prescribes
- Two-operator counters (one identifies, the other processes) — common in larger postos; not modelled in v0.3
- Accessibility for low-literacy operators — should the wizard expose a "read aloud" mode?

---

*This document is authoritative for the Balcão Digital surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins.*
