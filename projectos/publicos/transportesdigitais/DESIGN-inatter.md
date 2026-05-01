# DESIGN-inatter.md — Surface 3 · INATTER · Gestão

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1440+ floor) para staff INATTER e MTC. Mobile responsive subset para directores em viagem.
**Primary users:** Director-Geral INATTER, directores provinciais, técnicos de cartas, técnicos de viaturas, examinadores, fiscais de escolas de condução. Read-only para MTC e parceiros sociais.

---

## 1. Product purpose

A espinha administrativa do trânsito moçambicano. Onde 1,2 M cartas activas, 482 k viaturas registadas, 218 k viaturas profissionais (chapas, machibombos, táxis, camiões), 184 escolas de condução licenciadas e 38 centros IPO são geridos.

Antes desta superfície, INATTER era papel e filas: livretes em pasta, IPO em selo de papel, cartas plastificadas com 3-5 dias de espera. Esta superfície centraliza:

- Mapa nacional · viaturas · cartas · IPO por província
- Renovações online (alvarás, cartas, IUC)
- Fiscalização de escolas de condução
- Cross-PRM para multas em mora
- Gestão de transporte público (chapas, machibombos)
- Audição pública (dados.transportes.gov.mz)

---

## 2. Information architecture

```
Sign in (functional email + 2FA) · RBAC
└─ Painel Nacional
   ├─ KPIs (cartas · viaturas · alvarás · IPO · multas)
   ├─ Mapa de Moçambique (densidade por província)
   ├─ Tendências
   └─ Alertas (mora · multas · alvarás a vencer)
└─ Cartas
   ├─ Vigentes (1,2 M)
   ├─ Em emissão
   ├─ Em renovação
   ├─ Suspensas (multas + tribunal)
   └─ Validar QR público
└─ Viaturas
   ├─ Registo nacional (482 k)
   ├─ Por modo (8 chips)
   ├─ Por província
   ├─ Importadas (cross-Aduanas)
   └─ Em mora IUC
└─ Transporte Público
   ├─ Operadores (1 482)
   ├─ Alvarás (28 412)
   ├─ Rotas
   └─ Tarifas
└─ IPO · centros
   ├─ 38 centros · 11 províncias
   ├─ Performance · taxa aprovação
   └─ Auditorias
└─ Escolas de Condução
   ├─ 184 escolas licenciadas
   ├─ Examinadores
   └─ Taxa aprovação por escola
└─ Multas · cross-PRM
   ├─ Lavradas (YTD)
   ├─ Pagas
   ├─ Em mora
   └─ Em execução fiscal
└─ Relatórios
   ├─ Mensal · ao MTC
   ├─ Trimestral
   └─ Anual · público
```

---

## 3. Critical flows

### F1 — Painel nacional
Mapa interactivo de MZ com densidade de viaturas por província. Cidade de Maputo tem 38% das viaturas. KPIs nacionais: 1,2 M cartas · 482 k viaturas · 28 412 alvarás TP.

### F2 — Aprovar emissão de carta
- Candidato passou no exame · escola submete
- Sistema cruza eBI · saúde (atestado médico) · sem multas em outra carta
- Director provincial aprova · two-step + OTP
- Carta digital emitida em 24h · cross-Condutor app

### F3 — Auditar escola de condução
- Escolha escola por taxa de aprovação suspeita (>95% ou <40%)
- Auditoria física · fiscal verifica instalações
- Submeter relatório · escola pode perder licenciamento

### F4 — Suspender carta por multas em mora
- Cross-PRM lista cartas com multas >90 dias em mora
- Cross-Justiça pede execução
- Sistema suspende carta · condutor não pode circular legalmente
- Notifica condutor · cross-Condutor app

### F5 — Aprovar importação de viatura
- Cross-Aduanas indica viatura desalfandegada
- INATTER atribui matrícula MZ (sequencial por província)
- Livrete digital criado · IUC programado · IPO programado
- Notifica proprietário · cross-Condutor app

### F6 — Reportar mensalmente ao MTC
- Sistema agrega tudo · KPIs · mapa · evolução
- Director-Geral assina e envia
- Versão pública vai para dados.transportes.gov.mz

---

## 4. Components

| Component | INATTER |
|---|---|
| Top bar | INATTER badge · função |
| Side rail | 220 px cobalt-900 fill |
| KPI cards | Painel · 4-up |
| MZ map | Densidade por província (cobalt intensity) |
| Vehicle list | Filtros modo/província/estado |
| Plate component | Inline em todas as listas |
| Two-step modal | Aprovar carta, suspender carta |

---

## 5. Critical UI states

### 5.1 Carta para aprovar
*"Aprovar emissão · CD-2026-MAP-018421 · João Mahique · cat. B · escola Carlos & Filhos · 1.ª tentativa."*

### 5.2 Escola com taxa anormal
*"Escola Cossa Lda · Maputo · 96% taxa aprovação (média nacional 64%). Auditar?"*

### 5.3 Cartas em mora >90 dias
*"82 cartas com multas em mora >90 dias. Cross-Justiça pode executar suspensão."*

### 5.4 Importação a aprovar
*"Cross-Aduanas · Toyota Hilux 2024 · valor 2 184 000 MZN · proprietário NUIT 400 218 421 · atribuir matrícula MP-918?"*

### 5.5 Centro IPO suspeito
*"CIPO Sommerschield · Q1 · 98% aprovação (média nacional 78%). Auditoria recomendada."*

---

## 6. Cross-system

INATTER lê de:
- **eBI · Governo** — identidades
- **Saúde** — atestado médico
- **PRM-Trânsito** — multas, autos
- **Aduanas** — viaturas importadas
- **Trabalho · NUSS** — motoristas profissionais

INATTER escreve a:
- **Condutor app** — confirmações, suspensões, lembretes
- **Operador** — alvarás emitidos
- **PRM-Trânsito** — cartas suspensas
- **Justiça · TJ Adm** — execuções fiscais
- **Finanças · SISTAFE** — taxas, IUC, IPO
- **dados.transportes.gov.mz** — agregados públicos

---

*Authoritative for INATTER. DESIGN-system.md wins on conflict.*
