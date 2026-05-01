# DESIGN-empregador.md — Surface 2 · Empregador / Portal

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1280+ floor); secondary tablet support for SMEs without dedicated workstation.
**Primary users:** RH (recursos humanos), técnicos de contabilidade, gerentes de pequena empresa, CEO/proprietários de PMEs. Different roles see different sections (RBAC).
**Setting:** Office floor, accountant's desk, small business owner's laptop. Monthly rhythm dictated by salary processing (every 25-30) and INSS declaration (until day 10 of next month).

---

## 1. Product purpose

The portal where employers register workers, process salaries, deduct INSS, retain IRPS, declare to the State, and respond to IGT inspections. Before this surface, payroll was Excel and paper, declarations were monthly visits to balcões INSS, and IGT inspections came as PDF forms in surprise visits. This surface integrates payroll → INSS declaration → IRPS retention → cross-Finanças in a single flow.

Three priority use-cases, in order:

1. **Processar salários do mês.** Folha de salários para todos os trabalhadores. Cada um com payslip auto-gerado. Horas extra, abonos, descontos.
2. **Declarar à INSS.** Pré-preenchida pela folha. Submeter em 1 clique. Pagar via SISTAFE.
3. **Onboarding de novo trabalhador.** Cross-eBI valida BI. Atribui NUSS se não tem. Lavra contracto digital. Notifica trabalhador.

Deliberately *not*: not a recruiting tool (use INEFP for vagas), not employee performance reviews, not internal chat, not time-tracking surveillance. Compliance and payroll. Nothing else.

---

## 2. Information architecture

```
Sign in (RH email + password + 2FA)
└─ Painel
   ├─ KPIs (trabalhadores activos · folha do mês · INSS prazo · alertas IGT)
   ├─ Próximos prazos (folha · INSS · IRPS · IGT)
   ├─ Risk meter da empresa (cross-IGT · histórico inspecções)
   └─ Cross-system alerts
└─ Trabalhadores
   ├─ Lista (filtro: sector · cargo · estado)
   ├─ Detalhe (ficha · contracto · histórico salarial · presença)
   ├─ Onboarding novo (cross-eBI · NUSS · contracto)
   ├─ Rescisão (two-step · justificação)
   └─ Aviso prévio
└─ Folha
   ├─ Processar mês actual (table · todos os trabalhadores)
   ├─ Recibos · enviar / re-enviar
   ├─ Histórico mensal
   └─ Calculadoras (bruto/líquido · IRPS · subsídios)
└─ INSS
   ├─ Declaração mensal (pré-preenchida)
   ├─ Pagamentos (cross-SISTAFE)
   ├─ Histórico
   └─ Em mora (alertas + plano de regularização)
└─ IRPS
   ├─ Retenção mensal automática
   ├─ Declaração anual (cross-Finanças)
   └─ Reconciliação
└─ Contractos
   ├─ Vigentes
   ├─ Em rescisão
   └─ Modelos (sem termo · termo certo · termo incerto · estágio)
└─ IGT
   ├─ Inspecções recebidas
   ├─ Autos de notícia (com prazos de resposta)
   ├─ Coimas pagas / pendentes
   └─ Recursos
└─ INEFP
   ├─ Trabalhadores em formação
   ├─ Subsídios solicitados
   └─ Programas (Jovem-Trabalhador · Estágio Profissional)
```

Top bar: brand, primary nav, connectivity, identity badge with empresa + role.

---

## 3. Critical flows

### F1 — Sign in & RBAC
Email + password + 2FA SMS. Roles: RH (full), Contabilista (folha + INSS + IRPS), Gerente (read + autorizar), Auditor (read-only).

### F2 — Painel
KPIs do mês corrente: 84 trabalhadores activos · folha de Abril 1 482 000 MZN · INSS termina em 8 dias · 1 inspecção IGT marcada para Maio. Ranking risco IGT (cross-Inspecção).

### F3 — Onboarding novo trabalhador
- BI → cross-eBI valida identidade
- Sistema verifica se tem NUSS → caso contrário, atribui via cross-INSS
- Cargo · sector · salário · horário
- Tipo de contracto · prazo
- Sistema lavra contracto serifado pré-preenchido
- Trabalhador assina (digital ou presencial)
- Notificação ao trabalhador (Cidadão app · cross-Trabalhador)
- Inscrição automática no INSS (se ainda não estava)

### F4 — Processar folha do mês
- Tabela com todos os trabalhadores
- Por trabalhador: salário base, dias trabalhados, horas extra, abonos, faltas
- Sistema calcula: bruto → INSS 3% → IRPS retido → líquido
- Validação cross-row (totais)
- Submeter → recibos enviados aos trabalhadores
- Pagamento M-Pesa em massa OU transferência bancária

### F5 — Declaração INSS
- Pré-preenchida pelo total da folha
- Trabalhador 3% + Empresa 4% = 7% do bruto
- Submeter à INSS · cross-system
- Gera guia de pagamento para SISTAFE (cross-Finanças)
- Pagar (M-Pesa institucional · transferência · cheque)
- Confirmação automática

### F6 — Inspecção IGT recebida
- IGT lavrou auto de notícia em campo
- Empresa recebe notificação
- 14 dias para responder
- Pode regularizar (ex.: pagar INSS em mora) → coima evitada
- Pode contestar (recurso administrativo)
- Pode aceitar coima → pagar via SISTAFE

### F7 — Rescisão de contracto · two-step
- Causa: caducidade / mútuo acordo / justa causa / despedimento sem justa causa / colectivo
- Cálculo automático: aviso prévio + indemnização (30 dias por ano) + férias + 13.º proporcional
- Two-step + OTP do gerente + justificação ≥ 100 chars
- Notificação trabalhador
- Cross-IGT (em despedimento sem justa causa, IGT é informada para validação)

### F8 — Risk meter
- Sistema calcula risco com base em: histórico de inspecções, sector, número de trabalhadores, mora INSS, queixas de trabalhadores
- Mostra na painel principal
- Sugere acções para reduzir risco

---

## 4. Components & patterns

| Component | Empregador |
|---|---|
| Top bar | Empresa badge + role |
| Side rail | 220 px orange-900 fill (admin) |
| KPI cards | Painel · 4-up |
| Worker list | Filtros sector / estado / cargo |
| Folha table | Editable cells, totalisers per row+column |
| Auto serifado | Para contractos lavrados |
| Risk meter | Painel principal |
| Two-step modal | Rescisão, despedimento, encerramento |
| Cross-system badges | "Cross-Finanças · IRPS retido", "Cross-INSS · declarado" |

---

## 5. Critical UI states

### 5.1 Folha pronta
*"Folha de Abril processada. 84 trabalhadores · 1 482 400 MZN bruto · 1 374 218 MZN líquido. Submeter para pagamento?"*

### 5.2 INSS prazo a expirar
*"Declaração INSS termina em 3 dias (10 Mai). Pré-preenchida com folha de Abril. Submeter →"*

### 5.3 IGT auto recebido
*"IGT lavrou auto de notícia em obra Polana · 8 trabalhadores sem EPI. Tens 14 dias para responder."*

### 5.4 Trabalhador sem contracto
*"Manuel Sitole iniciou trabalho há 16 dias sem contracto registado. Lei 23/2007 art. 41 obriga em 15 dias. Lavrar agora →"*

### 5.5 Risco alto
*"Risco IGT alto. 3 trabalhadores em mora INSS. 1 queixa anónima recebida. Recomendado regularizar antes de inspecção."*

---

## 6. Cross-system

Empregador lê de:
- **eBI · Governo Digital** — identidade dos trabalhadores
- **Trabalhador app** — confirmações de recibos
- **INSS** — declarações submetidas, em mora, pagamentos
- **IGT** — inspecções, autos, coimas
- **INEFP** — trabalhadores em formação
- **Finanças Digitais** — IRPS retido, NUIT da empresa

Empregador escreve a:
- **Trabalhador app** — recibos, contractos, notificações
- **INSS** — declarações mensais, pagamentos
- **Finanças Digitais** — IRPS retido (cross-SISTAFE)
- **IGT** — respostas a autos, planos de regularização
- **INEFP** — inscrições em programas

---

## 7. Open questions for v0.4

- Folha bulk para grandes empresas (1000+ trabalhadores · CSV import)
- Acordos colectivos sectoriais (cláusulas por sector)
- Declaração trimestral simplificada para PMEs (≤10 trabalhadores)
- Reconciliação anual automática IRPS
- API para integração com ERPs (SAP, Primavera)

---

*Authoritative for Empregador. DESIGN-system.md wins on conflict.*
