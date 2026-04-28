# DESIGN-portal-at.md — Surface 1 · Portal AT · Administração Tributária

**Status:** v0.3 · Abril 2026
**Form factor:** Web app on desktop (1280+ floor); secondary tablet support for inspectors em campo.
**Primary users:** Inspectores fiscais, chefes de DAF (Direcção de Área Fiscal), DPF (Direcção Provincial de Finanças), DFD (admin nacional). Read-only view for auditores externos do TA (Tribunal Administrativo).
**Setting:** DAFs em províncias, Sede da AT em Maputo. Working hours; some sessions are field visits to empresas em fiscalização.

---

## 1. Product purpose

A single national tax administration record. Every NUIT, every contribuinte, every empresa, every factura emitted, every declaração submitted, every cobrança coerciva — retrievable nationally with permissions tightly scoped (a fiscal sees their DAF; a DPF inspector sees their province; only DFD/Conselho Directivo sees nationally).

The Portal AT optimizes for three things, in order:

1. **Daily cobrança operations** — pendentes do dia, devedores, alertas de fraude.
2. **Auditable fiscalização** — open processo, gather evidence, issue notification, record decisions.
3. **Reporting upwards and outwards** — to DPF, to MEF, to TA, and to the public dashboards.

Deliberately *not*: not a tax filing tool for the fiscal themselves (they use Cidadão); not a CRM for taxpayer support (that's a separate AT support channel); not a banking system.

---

## 2. Information architecture

```
Sign in (functional email + password + 2FA SMS) → DAF bind → Painel
└─ Painel
   ├─ KPIs (NUITs activos, declarações pendentes, cobrança do dia, alertas fraude)
   ├─ Pendentes do dia (assigned to me)
   └─ Avisos da DPF
└─ Contribuintes
   ├─ Pesquisar (NUIT · BI · nome · empresa)
   ├─ Detalhe do contribuinte (5 abas: Visão geral · Declarações · Facturas · Cobranças · Histórico)
   └─ Suspender / reactivar NUIT
└─ Declarações
   ├─ Pendentes (atrasadas)
   ├─ Em revisão
   └─ Submetidas no mês
└─ Facturação electrónica
   ├─ Volume nacional em tempo real
   ├─ Anomalias detectadas (padrões suspeitos)
   └─ Validar facturas duvidosas
└─ Cobrança
   ├─ Em mora (notificações automáticas)
   ├─ Coerciva (processo aberto)
   └─ Liquidações do dia
└─ Fiscalização
   ├─ Processos em curso
   ├─ Abrir novo processo
   └─ Calendário de visitas
└─ Relatórios
   ├─ Para DPF (mensal)
   ├─ Para MEF (trimestral)
   └─ Para TA (anual)
```

Top bar: brand, primary nav, connectivity, identity badge with DAF + role.

---

## 3. Critical flows

### F1 — Sign in & DAF bind
Functional email + password + SMS OTP (mandatory; fiscals open processos). DAF bind for chefes de DAF; DPF inspectors switch between DAFs of their province.

### F2 — Painel
KPIs do dia: NUITs activos, declarações em atraso, cobrança do dia (MZN), alertas de fraude detectados pelo motor de regras. Pendentes assigned to me.

### F3 — Detalhe do contribuinte
Five tabs:
- **Visão geral** — NUIT, BI (lido do eBI), endereço, regime de tributação, situação fiscal
- **Declarações** — IRPS, IVA, IRPC, ISPC histórico
- **Facturas** — emitidas e recebidas (cross-system from e-Factura)
- **Cobranças** — em mora, liquidadas, coercivas
- **Histórico** — todas as interacções (visitas, notificações, recursos)

### F4 — Validar declaração
Submitted IRPS / IVA / IRPC declarations land in the fiscal's queue. Review checks: math consistency, comparison with prior year, cross-check with facturas. Two-step confirmation to validate; or open processo de fiscalização.

### F5 — Detectar fraude (motor de regras)
Auto-detected anomalies: factura emitida para NUIT inactivo, IVA declarado mas sem facturas correspondentes, padrão de subdeclaração face ao histórico, salto súbito de volume. Each alert links to a NUIT and suggests next step.

### F6 — Cobrança coerciva
Após mora (>60 dias), processo de cobrança coerciva pode ser aberto pelo chefe de DAF. Two-step: justificação + OTP. Notifica contribuinte por SMS + carta (impressa). Valor sobe com juros de mora. Em última instância, penhora bancária via SISTAFE.

### F7 — Fiscalização
Processo formal, com etapas: abertura → notificação → visita → recolha de provas → relatório → decisão. Registo cronológico imutável. Anexos: fotografias de facturas, cópias de extractos, relatos.

### F8 — Suspender NUIT
Casos: óbito (cross-system com Governo Digital eRegistos), fraude provada, dissolução de empresa. Two-step + OTP + justificação ≥80 chars.

### F9 — Relatório DPF
Auto-gerado mensal. KPIs da DAF, comparação com mês anterior, comparação com média provincial. Chefe revê, comenta, submete.

---

## 4. Components & patterns

| Component | Portal AT |
|---|---|
| Top bar | DAF badge "DAF Maputo · Sede" |
| Side rail | 220 px burgundy-900 fill |
| Contribuinte ficha | 5 tabs |
| NUIT card | Reused from system, mostra estado fiscal |
| Cobrança table | MZN amounts mono · juros visible |
| Fraude alert | Banner red with rule that triggered |
| Two-step modal | For all irreversible action |

---

## 5. Critical UI states

### 5.1 NUIT inactivo emitindo factura
Banner red: *"Anomalia · NUIT 100 281 749 está suspenso desde 12 Mar mas emitiu 14 facturas. Investigar."*

### 5.2 Subdeclaração suspeita
Banner amber: *"IVA declarado em Fev: 12 450 MZN. Volume de facturação: 880 000 MZN (16% = 140 800). Diferença de 128 350 MZN. Solicitar esclarecimento?"*

### 5.3 Visita programada
*"Visita à empresa Lojinha do João (NUIT 400 871 432) marcada para amanhã 10:00. Endereço: Av. 24 de Julho 167. Inspector: Carlos Bila."*

### 5.4 Sem rede
Mesmo padrão da família. Painel funciona, validação enfileirada.

### 5.5 Fim de exercício fiscal
60 dias antes do fecho: *"Exercício 2026 fecha a 31 Dez. Confirme declarações finais até 30 Nov."*

---

## 6. Estado fiscal · vocabulário

| State | Tone | Verb |
|---|---|---|
| Declaração · em rascunho (no Cidadão/Comercial) | grey | — |
| Declaração · submetida | burg | Validar / Devolver |
| Declaração · validada | green | — |
| Declaração · em fiscalização | amber | Continuar processo |
| Cobrança · em mora | amber | Notificar |
| Cobrança · coerciva | red | Penhorar / arquivar |
| Cobrança · liquidada | green | — |
| NUIT · activo | grey | — |
| NUIT · suspenso | red | Reactivar |
| NUIT · óbito | grey | (cross-system Governo Digital) |

---

## 7. Cross-system

Portal AT lê de:
- **eBI · Governo Digital** — identidade do contribuinte; cruza-se com declarações
- **eRegistos · Governo Digital** — óbito, dissolução de empresa
- **e-Factura · Cidadão · Comercial** — facturas emitidas e declarações
- **SISTAFE** — receitas liquidadas

Portal AT escreve a:
- **Registo nacional de contribuintes (DFD)** — NUIT lifecycle
- **SISTAFE** — cobrança coerciva, penhora
- **Cidadão / Comercial** — notificações, decisões de recurso

---

## 8. Open questions for v0.4

- Mobile app for inspectors em campo (tablet) — visita registo offline
- AI assistance for fraude detection — out of scope (legal review needed)
- Print stylesheet for notificação coerciva — needs MEF-prescribed format
- Multi-DAF inspector flow — not finalized

---

*Authoritative for Portal AT. DESIGN-system.md wins on conflict.*
