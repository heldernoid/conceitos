# DESIGN-operador.md — Surface 2 · Operador de Transporte

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1280+ floor)
**Primary users:** Operadores de chapas, machibombos, táxis, camiões. Gerentes de frota, RH, financeiro.

---

## 1. Product purpose

A interface do operador de transporte rodoviário. Antes desta superfície, gerir uma frota de 28 chapas era Excel + WhatsApp. Esta superfície substitui:

- Cadastros em papel das viaturas e motoristas
- Renovação manual de alvarás (3 dias de fila INATTER)
- IPO em papel · sem visibilidade até vencer
- Sinistros em participações fotocopiadas
- Salários/INSS dos motoristas em folhas separadas

E inaugura:
- Frota completa em painel · IPO/IUC/seguro a vencer destacados
- Alvarás de transporte público com renovação online
- Motoristas profissionais cross-NUSS · INSS · carta de condução
- Sinistros com cross-Saúde + cross-PRM + cross-seguradora
- Cross-Trabalho Digital para folha + INSS

---

## 2. Information architecture

```
Sign in (RH email + 2FA) · RBAC
└─ Painel
   ├─ KPIs (frota · motoristas · alvarás · sinistros · multas)
   ├─ Próximos prazos
   └─ Risk meter da empresa
└─ Frota
   ├─ Lista (chapas · machibombos · táxis · camiões)
   ├─ Detalhe (livrete · IPO · IUC · seguro · sinistros)
   ├─ Adicionar viatura
   ├─ Transferir / vender
   └─ Importar (cross-Aduanas)
└─ Motoristas
   ├─ Lista (cross-NUSS · cross-carta)
   ├─ Detalhe (carta · INSS · salário · histórico)
   ├─ Onboarding (cross-INATTER valida carta · cross-Trabalho cria contracto)
   └─ Rescisão · cross-Trabalho
└─ Alvarás
   ├─ Vigentes (lista por viatura/rota)
   ├─ A vencer (90 dias)
   ├─ Renovar (online · 24h)
   └─ Histórico
└─ Rotas
   ├─ Definidas
   ├─ Tarifas
   └─ Quilómetros mensais
└─ Manutenção
   ├─ Calendarizada
   ├─ Reparações
   └─ Custos por viatura
└─ Sinistros
   ├─ Em curso
   ├─ Encerrados
   └─ Histórico
└─ Multas
   ├─ Por motorista (responsável)
   ├─ Por viatura
   ├─ Pendentes vs pagas
   └─ Contestações
```

---

## 3. Critical flows

### F1 — Painel
Frota Sumbane Lda · 28 chapas · 8 motoristas · 1 alvará a vencer em 30 dias · 2 multas pendentes · sinistro de 14 Abr ainda em curso. Risco médio.

### F2 — Onboarding novo motorista
- Cross-eBI valida BI · cross-INATTER valida carta de condução
- Sistema verifica categoria (D1 mínimo para chapa)
- Cross-Trabalho lavra contracto profissional
- INSS atribuído automaticamente
- Bus da empresa atribuído

### F3 — Renovar alvará TP em 30 dias
- Alvará AT-2024-CHAPA-04218 termina em 30 dias
- Cross-INATTER valida: IPO em dia · IUC pago · seguro válido · sem multas em mora
- Renovação online se tudo OK · 24h
- Pagamento taxa 2 800 MZN via SISTAFE

### F4 — Sinistro com motorista da frota
- Motorista reporta via app · operador é notificado em tempo real
- Cross-PRM · cross-Saúde · cross-seguradora
- Operador acompanha cronologia
- Após auto PRM, decisão: viatura repara · motorista substituído · seguradora paga

### F5 — Multa associada a motorista
- Multa lavrada em viatura da frota
- Sistema cruza com escala do dia · identifica motorista responsável
- Pode ser paga pela empresa OU descontada ao motorista (se CT permite)

### F6 — Adicionar viatura · cross-Aduanas
- Nova viatura · ou importada via porto Maputo
- Cross-Aduanas valida desalfandegamento
- Cross-INATTER atribui matrícula MZ
- Livrete digital criado · IUC e IPO programados

---

## 4. Components

| Component | Operador |
|---|---|
| Top bar | Empresa badge + role |
| Side rail | 220 px cobalt-900 |
| KPI cards | Painel · 4-up |
| Fleet table | Filtros modo / província / estado |
| Plate component | Inline em todas as listas |
| Driver row | Foto + carta + estado |
| Risk meter | Painel principal |
| Auto serifado | Para sinistros |

---

## 5. Critical UI states

### 5.1 Alvará a vencer
*"Alvará AT-2024-CHAPA-04218 termina em 30 dias. Renovação online · 24h · 2 800 MZN. Renovar →"*

### 5.2 Motorista sem carta válida
*"Carlos Mahique · carta vence em 7 dias. Não pode conduzir após esse prazo. Notificar para renovar."*

### 5.3 Sinistro ainda em curso
*"Sinistro INC-2026-MAP-04218 · 14 Abr · responsabilidade outra viatura · seguradora processa · 8 dias."*

### 5.4 Multa ambígua
*"Multa AT-2026-MAP-08412 · viatura AAB 184 MP · escala não claramente atribuída · 2 motoristas no turno. Atribuir manualmente?"*

### 5.5 IPO de várias viaturas a vencer
*"4 viaturas com IPO a vencer nos próximos 30 dias. Marcar todas via INATTER?"*

---

## 6. Cross-system

Operador lê de:
- **eBI · Governo** — identidade dos motoristas
- **INATTER** — viaturas · alvarás · cartas dos motoristas
- **Trabalho · NUSS** — vínculos laborais
- **Saúde · NUS** — feridos em sinistro
- **Finanças** — IUC · multas via SISTAFE
- **Aduanas** — importação de viaturas

Operador escreve a:
- **Trabalho · INSS** — declarações · folhas · contractos
- **INATTER** — pedidos de alvará · renovações
- **Finanças · SISTAFE** — pagamentos
- **Justiça** — contestações de multas
- **Seguradora** — participações de sinistro

---

*Authoritative for Operador. DESIGN-system.md wins on conflict.*
