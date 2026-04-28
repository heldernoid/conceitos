# DESIGN-ebi.md — Surface 1 · eBI · Identidade Civil

**Status:** v0.3 · Abril 2026
**Form factor:** Web app on desktop browser (1280+ floor) and 10″ tablet at the conservatória counter (1024×768 floor).
**Primary users:** Conservadores e ajudantes de conservatória, operadores BAÚ. Secondary: directores provinciais de registo civil, UGD admins.
**Setting:** Conservatórias do registo civil, postos BAÚ, postos avançados em distritos remotos — variable connectivity.

---

## 1. Product purpose

A single national civil-identity record. Every birth, every BI emission, every renewal, every death attached to one civic identity, retrievable at any conservatória on the network. Offline-first because the network is not always there, but **emission of definitive BIs requires a sync** — provisional documents may be issued offline.

The eBI optimizes for three things, in this order:
1. **Identifying the right citizen quickly** — by BI, NUIT, name, parents, or biometric (where available).
2. **Producing a clean civil record** — birth → first BI → renewals → name changes → death, all in one ledger.
3. **Issuing a document that any institution will accept** — QR-coded, signed by the conservador, audited.

It deliberately does *not* try to be a passport system, an electoral register, or a NUIT registry — those consume the eBI as the source of truth for identity, not the other way round.

---

## 2. Information architecture

```
Sign in (operator email + password + 2FA SMS) → Posto selector → Dashboard
└─ Dashboard
   ├─ Atendimento de hoje (queue, ticket, type, status)
   ├─ Requerimentos online a aprovar (from App do Cidadão)
   └─ Alertas (suspeita de duplicado, óbito não registado, sync pendente)
└─ Cidadãos / Pesquisar
   ├─ Resultado · abrir Ficha do Cidadão
   ├─ Sem resultado → Criar novo registo (nascimento)
   └─ Aviso de duplicação → Fundir registos
└─ Ficha do Cidadão
   ├─ Visão geral · Histórico · Documentos · Família · Acessos
   ├─ Iniciar requerimento (Wizard)
   └─ Override de emergência (registo sem documentação parental)
└─ Wizard de requerimento (5 steps) → Assinar + emitir
└─ Estado offline (sync queue, available data, retry)
```

A persistent **top bar** carries: brand, primary nav, connectivity pill, identity badge with posto. Identity is always one click from sign-out and posto switch.

---

## 3. Critical flows

### F1 — Sign in & posto selection
Three-step. Step 1 authenticates the operator (email + password). Step 2 SMS OTP — required because operators handle civic identity. Step 3 binds the session to a posto. Posto selection persists for the shift; switching is one click and re-authenticates.

### F2 — Dashboard (today)
Above the fold: today's atendimento queue (default sort by ticket order), online requerimentos pending review, and civic alerts. Four KPI cards: tickets atendidos, requerimentos online a rever, suspeitas de duplicado, sync state. The sync KPI is *not* hidden in chrome.

### F3 — Identify citizen
Search supports four input types via segmented control: BI, NUIT, nome completo, processo. Camera-read of BI is a shortcut for tablets. **No-document path:** if the citizen has no BI (newborn, lost, never issued), the operator opens the *Novo registo* path from the empty state. The system never blocks service for lack of paperwork — it issues a `TMP-YYYY-NNNN-PPP` provisional record (PPP = posto code).

### F4 — Citizen profile
Five tabs (Visão geral, Histórico, Documentos, Família, Acessos). Visão geral is the daily working view: BI status (válido / a renovar / expirado / suspenso), NUIT, contacto, recent access trail (so the conservador sees what the citizen sees). The Acessos tab is the same data as in the App do Cidadão, surfaced here so operators remember they are visible.

### F5 — New civic event
A 5-step wizard: Tipo (nascimento / renovação / 2ª via / mudança de nome / óbito) → Identificação → Anexos → Pagamento → Assinar. Each step saves a draft locally. The wizard branches by type — nascimento has a parental section; óbito requires a death certificate from MISAU; mudança de nome requires a court order (anexo).

### F6 — Approve online requerimento
Requerimentos submitted via the App do Cidadão arrive in the dashboard's "online" pile. Two-step approval: review (validate anexos, cross-check identity, mark any concern) and assinar (signs digitally, emits the document, queues SMS to citizen). A reject path requires a reason from a controlled vocabulary plus optional free text.

### F7 — Merge duplicates
Side-by-side compare with the older record marked as the **winner** (or the one with more documentary evidence — operator override allowed with justification). A match score (telefone, DOB, distrito, apelido, sexo, parents). Mandatory operator confirmation that they verified identity in person *or* against a higher-trust source (e.g. existing passaporte). Action is irreversible from the UI; reversal requires UGD support and a court order.

### F8 — Register death
Two paths. **Path A (with MISAU certificate):** operator pulls the óbito record from Saúde Moçambique (cross-system call), confirms identity match, signs. **Path B (declared at counter):** family declares; operator records, marks as *aguarda certificação MISAU*, queues for follow-up. Either path triggers automatic NUIT and BI suspension and notifies the cidadão family contacts.

### F9 — Offline state
Dedicated screen, but offline state is also indicated in the top-bar pill at all times. Lists the pending sync queue (type, citizen, detail, time, status), what data is available offline (last 90 days of posto's citizens, full cidade catalogue of postos, CID-Civil event types, fee table), and what is not (national BI search, cross-posto verification, cross-system MISAU/SAGEDIS calls).

### F10 — Emergency civic override
Used when a child needs registration and parents lack BIs (rural, migrant, refugee). Two-step: justification (≥80 chars, witness selection — must be a leader comunitário or known operator, type of override, acknowledgement that record is provisional) and confirmation. Provisional record valid 90 days; flagged to UGD and to the provincial conservador for review.

---

## 4. Components & patterns

| Component | eBI-specific notes |
|---|---|
| Top bar | Carries posto badge ("BAÚ Inhambane Central"). Click → switch posto. |
| Connectivity pill | Three states. Sync queue count visible when amber. |
| Citizen search | Segmented BI / NUIT / Nome / Processo. Mono input for BI and NUIT. |
| Wizard | 5 steps; step labels reflect the chosen type (nascimento vs renovação). |
| Provenance footer | On every emitted document. Process number, conservador, posto, timestamp, QR. |
| Two-step modal | For emit, sign, merge, register death, void. Justification field for merge/void. |
| Side rail | Not used in eBI (top-bar nav is sufficient). |
| Phone frame | Not used. eBI is desktop/tablet only. |

---

## 5. Critical UI states

### 5.1 Citizen with conflicting records
The Ficha shows a red strip at the top: *Suspeita de duplicado · BI 110100099876 C também aparece como 110100099877 C em Beira (12 Mar 2024). Reveja antes de emitir.* Includes a *Comparar e fundir* CTA.

### 5.2 BI expirado
Header chip: red badge "BI expirado · 14 Fev 2026". The system still allows lookup but blocks emission of derivative documents (passaporte, antecedentes) until renewed.

### 5.3 Pendente de óbito
Yellow strip if the citizen has a death certificate pending from MISAU. Operators may not issue new documents but may print the histórico.

### 5.4 Emergency override active
Banner: *Este registo foi criado em modo de emergência por J. Massingue (04 Abr 2026). Provisional até 03 Jul 2026. Sujeito a revisão de UGD e Conservador Provincial.*

### 5.5 Citizen-facing access trail (mirror of App do Cidadão)
The Acessos tab shows: who (operator name + role), when, posto, action (consultou / emitiu / corrigiu), and reason where the operator entered one. Citizens see the same data in their app — operators are reminded by a footer note: *O cidadão vê esta lista no seu telemóvel.*

---

## 6. Civic-state vocabulary

The badges across the eBI surface map to a closed civic-state vocabulary:

| State | Tone | Verb available |
|---|---|---|
| Rascunho | grey | Continuar / Eliminar |
| Submetido | blue | Atribuir |
| Em análise | blue | Aprovar / Rejeitar |
| Aguarda pagamento | amber | Reenviar referência |
| Aguarda anexo | amber | Notificar cidadão |
| Assinado / Emitido | green | Imprimir / Enviar SMS |
| Rejeitado | red | Reabrir / Arquivar |
| Anulado | red | — |
| Suspenso | amber | Reactivar |
| Expirado | red | Renovar |
| Provisório | amber | Validar |

Operators learn the vocabulary; consistency across surfaces means a citizen's badge in the App do Cidadão means exactly the same thing as the conservador's badge here.

---

## 7. Two-step confirmations

These actions are gated by a justification modal:

- **Fundir registos** — minimum 80 chars + witness operator
- **Anular requerimento** — minimum 60 chars + select reason from controlled vocabulary
- **Emitir BI definitivo offline** — only allowed when the citizen has a verified Saúde Moçambique record we can cross-check; requires "Compreendo que este BI será revalidado quando o sistema sincronizar" check
- **Registar óbito sem certificado MISAU** — minimum 100 chars + two operator witnesses
- **Override de emergência** — minimum 80 chars + leader comunitário witness + type-of-override picker

---

## 8. Cross-system calls

eBI is consumed by:

- **App do Cidadão** — read identity, write requerimentos
- **Balcão** — read identity for queue ticket binding, write atendimento records
- **Saúde Moçambique** — read identity (BI lookup) when a citizen presents at a Centro de Saúde without their physical BI
- **NUIT registry (real, MEF)** — write the NUIT once a BI is emitted for the first time at age 18
- **Eleitoral registry (real, CNE)** — read at registration drives
- **Auditoria** — every read is logged; the citizen sees the read in their App

eBI calls *out* to:

- **Saúde Moçambique** for óbito certificates
- **Tribunal Judicial registry** for court-ordered name changes
- **MISAU vital records** for parental verification when a parent's BI is missing but we have a maternity record

These are conceptual integrations — not implemented in the protótipo.

---

## 9. Performance & offline

- First paint < 1.5 s on a 2018 desktop in Inhambane
- Search response < 800 ms p95 when online
- Last 90 days of posto citizens cached on the workstation
- Wizard drafts persist across sessions and across power cuts
- Sync queue retains up to 500 items; operators see counter; UGD alerted at 200

---

## 10. Open questions for v0.4

- Biometric capture (fingerprint at counter) — hardware not standardized; flow stubbed
- Integration with the foreign-residents registry (SADC card holders) — out of scope for v0.3
- "Mass campaign" mode for rural registration drives — needs a different UI density and a foreman role
- Print stylesheet for the BI itself — deferred until UGD prescribes the physical card spec
- Voice-driven entry for low-literacy operators — research not yet started

---

*This document is authoritative for the eBI surface. When this document contradicts DESIGN-system.md, DESIGN-system.md wins. This document may add specifics; it may not loosen the rules.*
