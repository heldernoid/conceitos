# DESIGN-inss.md — Surface 3 · INSS / Gestão (admin)

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1280+ floor) for INSS staff. Mobile responsive subset for managers.
**Primary users:** Funcionários da INSS (analistas de pensões, gestores de inscrições, fiscalizadores), administração central, delegações provinciais. Read-only views for OTM, parceiros sociais, MTSS.
**Setting:** Sede da INSS na Av. 24 de Julho, delegações provinciais. Daily flow of pensão claims, monthly flow of declarations, quarterly fiscalisation.

---

## 1. Product purpose

The administrative spine of segurança social moçambicana. Where 1.82 M inscritos, 184 k pensionistas, and 218 k empresas declarantes are managed. Before this surface, INSS operations were paper-heavy: declarações chegavam fisicamente, pensões eram concedidas com base em livros de ponto, and fiscalização cruzava INSS×folha manualmente. This surface integrates everything: declarações automáticas, pensões com cálculo automático, e cross-IGT para fiscalização dirigida.

Three priority use-cases:

1. **Gerir pensionistas e prestações.** Pensões de velhice, invalidez, sobrevivência. Subsídios de doença, maternidade, funeral. Aprovação, cálculo, pagamento mensal.
2. **Receber e validar declarações dos empregadores.** Cross-Empregador. Fila de declarações pendentes. Detectar discrepâncias.
3. **Fiscalização cruzada com IGT.** Identificar empresas com declarações inconsistentes (ex.: poucos trabalhadores declarados vs. dimensão da obra). Gerar lista de inspecção dirigida para a IGT.

Deliberately *not*: not a public-facing benefits explorer (that's the Trabalhador app), not a recruitment portal, not a finance management system (that's SISTAFE).

---

## 2. Information architecture

```
Sign in (functional email + 2FA)
└─ Painel Nacional
   ├─ KPIs (inscritos · pensionistas · contribuições mês · pendentes)
   ├─ Mapa de Moçambique (densidade de inscritos por província)
   ├─ Tendências
   └─ Alertas (mora · discrepâncias · pensões a vencer)
└─ Inscritos
   ├─ Lista (filtros: sector · província · estado)
   ├─ Detalhe (worker card · histórico contribuições · pensão estimada)
   ├─ Inscrever novo
   └─ Validar inscrições pendentes (24h)
└─ Empresas
   ├─ Declarantes (lista)
   ├─ Em mora (priorizada)
   ├─ Detalhe empresa (folha · contribuições · histórico)
   └─ Plano de regularização
└─ Pensões
   ├─ Velhice (pendentes · activas)
   ├─ Invalidez (com junta médica)
   ├─ Sobrevivência (com habilitação herdeiros)
   └─ Pagamento mensal massivo
└─ Subsídios
   ├─ Doença (em análise · aprovados · pagos)
   ├─ Maternidade
   ├─ Funeral
   └─ Auto-aprovação para casos simples
└─ Fiscalização
   ├─ Discrepâncias detectadas (auto)
   ├─ Lista para IGT (cross-system)
   └─ Histórico cruzamentos
└─ Relatórios
   ├─ Mensal · ao MTSS
   ├─ Trimestral · ao Conselho de Administração
   └─ Anual · público em dados.trabalho.gov.mz
```

---

## 3. Critical flows

### F1 — Painel Nacional
Mapa interactivo de Moçambique com densidade de inscritos por província. Cidade de Maputo lidera com ~28% dos inscritos. KPIs nacionais: 1,82 M inscritos · 184 k pensionistas · folha mês 2 184 M MZN.

### F2 — Aprovar pensão de velhice
- Pensionista candidato (ex.: Manuel Cossa, 60 anos, 32 anos de contribuições)
- Sistema calcula pensão estimada (base salarial × % por anos · Lei 4/2007)
- Histórico de contribuições visível (gaps a vermelho)
- Two-step + OTP do analista
- Aprovação → primeira pensão paga em ≤ 30 dias

### F3 — Detectar discrepância empresarial
- Sistema cruza folhas declaradas com presença em obras (cross-IGT geo-data)
- Empresa X declara 28 trabalhadores · IGT viu 42 em campo
- Auto-cria caso de inconsistência
- Atribui à fiscalização

### F4 — Cross-IGT · gerar lista dirigida
- Filtros: sector, província, magnitude da discrepância, histórico
- Sistema sugere top 20 empresas para inspecção este trimestre
- IGT recebe lista pré-ordenada com contexto

### F5 — Validar inscrição pendente (Empregador)
- Empresa onboarded um trabalhador novo · NUSS provisório
- Sistema cruza com eBI (cross-Governo Digital) e eventualmente NUS (cross-Saúde)
- Aprovado → NUSS oficial, comunicado ao empregador e ao trabalhador

### F6 — Regime simplificado para informais
- Trabalhador da economia informal pode auto-inscrever (cross-Trabalhador)
- Contribuição mínima: 10% sobre rendimento declarado (não < salário mínimo)
- INSS confere com cross-Finanças (NUIT) periodicamente

---

## 4. Components & patterns

| Component | INSS |
|---|---|
| Top bar | INSS badge · função |
| Side rail | 220 px orange-900 fill |
| KPI cards | Painel · 4-up |
| MZ map | Densidade de inscritos (cross-saudedigital pattern) |
| Worker list | Filtros sector / província / estado |
| Pension calculator | Cálculo automático com gaps visíveis |
| Two-step modal | Aprovar pensão, cancelar inscrição |

---

## 5. Critical UI states

### 5.1 Pensão a aprovar
*"Manuel Cossa atinge 60 anos em 18 dias. 32 anos de contribuições. Pensão estimada: 16 800 MZN/mês. Aprovar →"*

### 5.2 Empresa em mora 6+ meses
*"Construtora ALPHA Lda em mora há 8 meses. Total: 482 000 MZN. Cross-IGT recomenda inspecção urgente."*

### 5.3 Discrepância detectada
*"Empresa BETA declara 28 trabalhadores · IGT viu 42 em obra Tete (14 Abr). Diferença: 14 não declarados. Atribuir à fiscalização?"*

### 5.4 Pensionista falecido
*"Pensão #P-2018-MAP-04218 · titular faleceu 12 Abr. Suspender pagamento. Iniciar processo de sobrevivência (cônjuge)?"*

### 5.5 Subsídio funeral
*"Pedido SF-2026-04218. Familiar: Júlia Cossa (cônjuge). Documentos verificados. Pagamento 30 780 MZN aprovado · M-Pesa."*

---

## 6. Cross-system

INSS lê de:
- **eBI · Governo Digital** — identidades
- **NUS · Saúde Digital** — para subsídios doença/maternidade
- **NUIT · Finanças Digitais** — para empresas declarantes
- **Empregador app** — declarações mensais
- **IGT** — autos de notícia (sobre não-declarados)

INSS escreve a:
- **Trabalhador app** — confirmações, pensões, subsídios
- **Empregador app** — declarações validadas, alertas de mora
- **IGT** — listas de inspecção dirigida
- **Finanças Digitais** — pagamento via SISTAFE
- **dados.trabalho.gov.mz** — agregados públicos

---

## 7. Open questions for v0.4

- Pensões antigas dos mineiros AAEM (África do Sul) · reconciliação histórica
- Trabalhadores migrantes intra-SADC (acordo bilateral)
- Migração faseada de pensões em papel para digital
- Auditoria automática quarterly por amostragem

---

*Authoritative for INSS. DESIGN-system.md wins on conflict.*
