# DESIGN-portal-mjcr.md — Surface 1 · Portal MJCR · Acompanhamento Processual

**Status:** v0.3 · Abril 2026
**Form factor:** Web app on desktop (1280+ floor); secondary tablet support for juízes em audiência.
**Primary users:** Juízes (de direito, de paz, de família), oficiais de justiça, escrivães, conservadores. Read-only views for OAM, PGR liaison, Tribunal Supremo, Tribunal Administrativo.
**Setting:** Câmaras dos juízes, secretarias dos tribunais judiciais nas 11 províncias. Working hours, deep concentration sessions, frequent court attendance switching.

---

## 1. Product purpose

A single national judicial workflow record. Every processo, every despacho, every audiência, every sentença — retrievable nationally with permissions tightly scoped (an oficial sees their tribunal; a juíz sees their secção; only DJD/Conselho Superior da Magistratura sees nationally).

The Portal MJCR optimizes for three things, in order:

1. **Daily work of judging** — pauta de hoje, despachos pendentes, prazos a expirar.
2. **Auditable, traceable processes** — every act with author + timestamp + legal basis.
3. **Reporting upwards** — to Tribunal Supremo (recursos), TA (auditoria), MJCR (estatísticas), and to public dashboards (`dados.justica.gov.mz`).

Deliberately *not*: not a CMS for legal opinions; not a CRM for litigants; not a billing system; not a forum for OAM.

---

## 2. Information architecture

```
Sign in (functional email + password + 2FA SMS) → Tribunal/Secção bind → Painel
└─ Painel
   ├─ Pauta de hoje (audiências marcadas)
   ├─ Despachos pendentes
   ├─ Prazos a expirar (≤7 dias)
   └─ Avisos do Conselho Superior da Magistratura
└─ Processos
   ├─ Pesquisar (n.º · partes · NUIT)
   ├─ Detalhe do processo (5 abas: Visão · Peças · Audiências · Despachos · Histórico)
   ├─ Distribuir (automática + manual)
   └─ Arquivar definitivamente
└─ Audiências
   ├─ Pauta semanal
   ├─ Convocações
   └─ Acta de audiência
└─ Despachos
   ├─ Modelos (despacho liminar · saneador · sentença)
   ├─ Em rascunho
   └─ Proferidos
└─ Recursos
   ├─ Para Tribunal Supremo (cível, criminal)
   ├─ Para TA (administrativo)
   └─ Em julgamento
└─ Cidadania
   ├─ Pedidos de certidão
   ├─ Queixas-crime entradas
   └─ Mediação solicitada (cross-link Comunitário)
└─ Relatórios
   ├─ Mensal · ao Tribunal Supremo
   ├─ Trimestral · ao MJCR
   └─ Estatísticas públicas (dados.justica.gov.mz)
```

Top bar: brand, primary nav, connectivity, identity badge with tribunal + secção + role.

---

## 3. Critical flows

### F1 — Sign in & Tribunal bind
Functional email + password + SMS OTP (mandatory). Tribunal/secção bind for each role. Magistrados itinerantes podem mudar de tribunal mediante autorização.

### F2 — Painel
Pauta de hoje, despachos pendentes, prazos a expirar, avisos do CSM. Para um juiz com sessão de manhã: o que decidir antes da audiência.

### F3 — Detalhe do processo
Five tabs:
- **Visão geral** — partes, espécie, valor da causa, estado actual, próxima diligência
- **Peças** — petição, contestação, anexos, todos os PDFs
- **Audiências** — actas, gravações de audio (se houver)
- **Despachos** — todos os actos do juiz, datados, com fundamentação
- **Histórico** — cronologia imutável de todo o processo

### F4 — Distribuir (manual)
Quando há suspeição, impedimento, ou redistribuição por motivo legal. Two-step + justificação.

### F5 — Proferir despacho
Editor com modelo. Fundamentação obrigatória ≥ 100 chars. Citação de artigos. Assinatura digital. Two-step para sentença.

### F6 — Sentenciar à revelia
Quando réu não comparece, devidamente citado. Two-step + OTP + justificação ≥ 80 chars. Acta automática. Notificação.

### F7 — Arquivar definitivamente
Após trânsito em julgado e cumprimento. Two-step + OTP. Sai da pauta activa, fica acessível por consulta.

### F8 — Recurso para Tribunal Supremo / TA
Marcação de recurso. Sistema prepara dossier electrónico. Cross-system para Supremo/TA.

### F9 — Pedido de certidão
Cidadão (via app) pede certidão de processo público. Conservador valida e emite com selo brass. Pago via SISTAFE (ligação a Finanças Digitais).

### F10 — Queixa-crime entrada
Cidadão apresenta queixa pelo Cidadão/Justiça app. Entra na fila do MP (Ministério Público) do tribunal. PGR vê aggregate.

---

## 4. Components & patterns

| Component | Portal MJCR |
|---|---|
| Top bar | Tribunal badge "TJ Maputo · 3.ª Sec. Cível" |
| Side rail | 220 px slate-900 fill |
| Process ficha | 5 tabs |
| Process card | Slate gradient hero |
| Pauta table | Hour-ordered, espécie chips |
| Despacho editor | Serif preview pane |
| Two-step modal | For sentenciar à revelia, arquivar, anular escritura |

---

## 5. Critical UI states

### 5.1 Réu não comparece à 3.ª chamada
*"Réu João Macia (NUIT 100 218 091) não compareceu nas 3 chamadas. Pode sentenciar à revelia (art. 484.º CPC) ou ordenar nova citação por edital."*

### 5.2 Prazo a expirar
*"3 prazos terminam amanhã. Despachar antes das 12:00."*

### 5.3 Suspeição declarada
*"Juíza M. Cuamba declarou suspeição em P-2026-CIV-MAP-00481. Distribuir a outro juiz da 3.ª Secção?"*

### 5.4 Audiência adiada por cidadão
*"Autora Maria Cuamba pediu adiamento (mediação suplementar). Aceitar? Próxima data 22 Mai."*

### 5.5 Recurso para Tribunal Supremo
*"Recurso interposto. Dossier de 14 peças (84 MB) preparado. Confirmar envio ao Supremo?"*

---

## 6. Estado processual · vocabulário

| State | Tone | Verb |
|---|---|---|
| Petição · em rascunho (pelo advogado, no Cidadão) | grey | — |
| Distribuído | slate | Despachar |
| Em instrução | slate | Diligenciar |
| Em audiência | amber | Convocar / decidir |
| Sentenciado | brass | (transitar) |
| Em recurso | amber | (aguardar Supremo / TA) |
| Transitado em julgado | green | — |
| Arquivado | grey | (consulta) |
| Suspenso | red | Reactivar |
| Revelia | red | Sentenciar à revelia |

---

## 7. Cross-system

Portal MJCR lê de:
- **eBI · Governo Digital** — identidade das partes
- **NUIT · Finanças Digitais** — identidade fiscal (para causas comerciais, SISA imobiliário)
- **Cidadão / Justiça** — peticões, queixas, pedidos de certidão
- **Tribunal Comunitário** — acordos homologados, mediações falhadas escaladas

Portal MJCR escreve a:
- **Cidadão / Justiça** — actualizações de processo (despachos, audiências, decisões)
- **Tribunal Supremo / TA** — recursos
- **Cadastro Predial** — sentenças sobre DUATs e propriedade
- **Registos Públicos** — escrituras anuladas, registos rectificados
- **dados.justica.gov.mz** — estatísticas agregadas

---

## 8. Open questions for v0.4

- Audio gravações de audiência — armazenamento, transcripção
- Print stylesheet para sentença e despacho — formato MJCR
- Multi-tribunal flow para juízes itinerantes
- Auditoria automática TA por amostragem

---

*Authoritative for Portal MJCR. DESIGN-system.md wins on conflict.*
