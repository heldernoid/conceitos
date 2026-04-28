# DESIGN-auditoria.md — Surface 5 · Auditoria de Acessos

**Status:** v0.3 · Abril 2026 · esboço (depth lower than the other four surfaces — calls out where v0.4 will close the gap).
**Form factor:** Web admin app on desktop (1280+ floor). Citizen-facing portion is a re-skin of the existing Acessos tab in the App do Cidadão.
**Primary users:** UGD audit team (≈12 analistas), provincial conservadores (read-only), IGF auditors (read-only export).
**Setting:** UGD HQ in Maputo + provincial conservatórias. Always online (no offline auditor mode).

---

## 1. Product purpose

A single window into every read and write of every citizen record across the Governo Digital family. Three jobs, in order:

1. **Show the audit log.** Every consult, every emit, every merge, every override — searchable, filterable, exportable.
2. **Surface anomalies.** Operators with unusual access patterns; postos with cash discrepancies; cross-system calls without a stated reason; provisional records overdue for review.
3. **Process citizen reports.** When a citizen flags an access in the App do Cidadão, that report enters a queue here; UGD analyst reviews, contacts the operator if needed, decides, notifies the citizen.

It deliberately does *not* replace IGF (financial audit) or the Tribunal Administrativo (judicial review). Auditoria is a process control — not a judicial body.

---

## 2. Information architecture

```
Side rail (navy-900) · UGD Auditoria
└─ Painel
   ├─ KPIs do dia (acessos, reports pendentes, anomalias)
   ├─ Reports do cidadão · em fila
   └─ Anomalias detectadas
└─ Log de acessos
   ├─ Filtros (operador · posto · cidadão · tipo · data · sistema)
   ├─ Tabela paginada
   └─ Detalhe de acesso → linkagem ao processo / ficha
└─ Reports de cidadãos
   ├─ Em fila · em investigação · respondidos
   └─ Detalhe → workflow de investigação
└─ Padrões anómalos
   ├─ Operador com volume atípico
   ├─ Acessos fora do horário do posto
   ├─ Postos com discrepância de caixa
   └─ Provisórios não revistos
└─ Exportação
   ├─ Para IGF (CSV assinado)
   └─ Para Tribunal Administrativo (a pedido)
└─ Vista do cidadão (espelho)
   └─ O que o cidadão vê na sua App
```

Side rail (220 px navy-900) carries the primary nav. Top bar is minimal — the rail does the work.

---

## 3. Critical flows

### F1 — Painel
KPIs do dia: total de acessos (24 h), reports pendentes, anomalias por rever, provisórios a expirar. Below: top 10 most-recently flagged events; fila de reports do cidadão (sorted by age).

### F2 — Log de acessos
Massive paginated table. Each row: who (operator), when (timestamp), where (posto + IP), what (action: consultou / emitiu / corrigiu / fundiu / cancelou), on whom (cidadão BI), why (reason field, if entered), system (eBI / Balcão / App do Cidadão / Saúde Moçambique cross-call). Filters at the top. Default sort: most recent first.

### F3 — Detalhe de um acesso
Click a row → page with the full audit record, the citizen's snapshot at the time, the operator's other accesses that day, and a link to the process if the access was tied to one. From here the analyst can: marcar como conforme, sinalizar para revisão, abrir investigação.

### F4 — Padrões anómalos (auto-detectados)
The system flags four classes of pattern, all of which appear as cards on the painel and as a dedicated tab:
- **Operador com volume atípico**: > 200 consultas em 24 h, ou >3σ acima da média do operador
- **Acessos fora do horário**: consultas entre 22:00 e 06:00 sem motivo registado
- **Posto com discrepância repetida**: discrepância de caixa em ≥3 dias do mês
- **Provisório não revisto**: registo provisório a aproximar-se dos 90 dias sem validação

### F5 — Report do cidadão · workflow
1. **Recepção** — entra na fila com referência R-2026-AUD-NNNN.
2. **Triagem** — analista UGD lê; cruza com o log; classifica.
3. **Investigação** — se necessário, contacta o operador, o conservador do posto, e o cidadão.
4. **Decisão** — quatro saídas: *acesso conforme* (operador justificou) · *acesso conforme com recomendação* (a UGD recomenda formação) · *acesso impróprio* (medida disciplinar) · *acesso fraudulento* (encaminhar ao Ministério Público).
5. **Notificação** — o cidadão recebe a decisão na App; o operador recebe pelo seu canal interno.

### F6 — Investigação · página
Side-by-side: o report do cidadão · o registo do log · timeline da investigação · histórico de decisões similares. Botões: contactar operador, contactar conservador, contactar cidadão, decidir.

### F7 — Vista do cidadão (espelho)
Uma versão da Acessos tab da App do Cidadão, embutida aqui, para que o analista veja exactamente o que o cidadão vê. Lembrete cultural: o cidadão é a primeira linha de defesa.

### F8 — Exportação para IGF
Mensal. CSV assinado digitalmente pela UGD com o conjunto fechado de eventos do mês. Hash publicado em `orcamento.gov.mz` para verificação.

---

## 4. Components & patterns

| Component | Auditoria-specific notes |
|---|---|
| Side rail | 220 px navy-900. Groups: Operação · Reports · Padrões · Exportação. |
| Painel KPIs | Four large numbers. Anomaly count in amber; report queue in blue. |
| Log table | Compact, sticky header, dense (10 rows visible without scroll). Sortable. |
| Filter strip | Sticky. Up to 6 chips active. Reset on one click. |
| Detail page | Two-column. Left: the event. Right: context (other events same day, same operator). |
| Workflow stepper | 5 steps for report investigation. |
| Decision buttons | Four states: conforme · recomendação · impróprio · fraudulento. Each requires justification ≥ 100 chars and analyst SMS-OTP. |
| Cidadão mirror | Embedded phone frame so the analyst sees the citizen's view. |

---

## 5. Civic-state vocabulary additions

| State | Tone | Verb |
|---|---|---|
| Acesso conforme | grey | Arquivar |
| Em revisão | blue | Continuar investigação |
| Acesso conforme c/ recomendação | amber | Notificar conservador |
| Acesso impróprio | red | Iniciar processo disciplinar |
| Acesso fraudulento | red | Encaminhar ao MP |

---

## 6. Two-step confirmations

- **Decidir um report do cidadão** — justificação ≥ 100 chars + SMS OTP do analista
- **Encaminhar ao Ministério Público** — justificação ≥ 200 chars + SMS OTP + assinatura digital do director da UGD
- **Exportar log para IGF** — confirma que a janela temporal está correcta + hash gerado e publicado

---

## 7. Cross-system relationship

Auditoria reads from **all** other surfaces (eBI, App do Cidadão, Balcão, Orçamento Aberto). It is the only surface that reads everything. It writes nothing into the other surfaces — exception: a *notificação ao cidadão* that appears in the App do Cidadão's "Reports" timeline (see DESIGN-cidadao.md F4).

The Auditoria surface does *not* see the content of citizen documents (e.g. the actual text of a certidão). It sees the *event* of access — by whom, when, why, and which document.

---

## 8. Privacy & ethics

- Analysts cannot read a citizen's record content. They see access *metadata*.
- Every analyst action is itself logged — auditing the auditors.
- The citizen who reports an access is **not revealed to the operator**. Only the analyst sees both sides.
- Reports older than 90 days without a decision are auto-escalated to the director da UGD.
- Aggregate, anonymised statistics are published quarterly (number of reports, decisions, average time to resolve).

---

## 9. Open questions for v0.4 — *and there are several*

This surface is the least developed in v0.3 — it's the **scaffold**, not a closed design.

- **Anomaly detection** — current rules are static (volume, hours, days). v0.4 needs a discussion with UGD on what counts as "atypical" without unfairly flagging operators in postos remotos with intermittent connectivity.
- **Operator self-defence** — if an operator's pattern is flagged, can they see the flag and defend? Procedurally important but not yet drafted.
- **Bulk export to IGF** — schema, signing, hash publication — drafted but not built.
- **Decision audit trail** — currently just text. v0.4 wants structured outcomes for analytics on inter-analyst variance.
- **Cross-system cidadão mirror** — embedding the App do Cidadão view in the Auditoria UI requires a SSO bridge that doesn't yet exist.
- **Mobile / tablet for field auditors** — out of scope for v0.3; auditors work from the UGD HQ in Maputo.

This is the surface where stakeholder feedback at v0.3 review should land most heavily.

---

*This document is authoritative for the Auditoria surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins.*
