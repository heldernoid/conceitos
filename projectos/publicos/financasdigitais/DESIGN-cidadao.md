# DESIGN-cidadao.md — Surface 3 · Cidadão Contribuinte

**Status:** v0.3 · Abril 2026
**Form factor:** Mobile PWA, 360×760 floor. Same constraints as e-Factura but for assalariados (the 4,8M+ NUIT universe of salaried workers).
**Primary users:** Trabalhadores assalariados (sector público e privado) — the universe that doesn't emit facturas, just receives a salary with IRPS retido on the source.
**Setting:** Casa, transporte, escritório. Mais previsível que e-Factura, mas com mesmas restrições de rede e bateria.

---

## 1. Product purpose

The personal tax companion for every salaried Mozambican. Three things:

1. **NUIT digital portátil** — substitui o cartão de papel. QR para o patrão registar. Abrir num clique.
2. **Transparência radical sobre IRPS retido** — vê em tempo real o que o patrão retém e entrega à AT. Se o patrão não entregar, alerta.
3. **"Onde vai o meu imposto"** — ligação directa entre os MZN que paga e o orçamento do Estado (cross-system com Governo Digital, Saúde Digital, Educação Digital).

Plus: declaração anual pré-preenchida, situação fiscal regular, reembolso pedido.

Deliberately *not*: not a place to emit facturas (use e-Factura); not personal banking; not a fiscal advisor.

---

## 2. Information architecture

```
Onboarding (BI lookup → NUIT existing or auto-generate)
└─ Hoje
   ├─ NUIT card (hero)
   ├─ IRPS retido este mês (em tempo real)
   ├─ Situação fiscal (regular / irregular)
   └─ Banner "Onde vai o meu imposto"
└─ Imposto
   ├─ IRPS retido · 12 meses
   ├─ Declaração anual 2025 (wizard)
   ├─ Reembolso pedido
   └─ Histórico
└─ Onde vai
   ├─ Resumo: dos meus 12 870 MZN deste mês...
   ├─ Educação · 23%
   ├─ Saúde · 18%
   ├─ Defesa · 12%
   ├─ Infra-estrutura · 14%
   └─ Outros (Segurança · Justiça · Admin · etc)
└─ Eu
   ├─ NUIT card · QR portátil
   ├─ Empregador actual
   ├─ Histórico de empregadores
   └─ Suporte AT
```

Bottom nav: Hoje · Imposto · Onde vai · Eu.

---

## 3. Critical flows

### F1 — Onboarding com BI
Mesmo padrão do e-Factura mas sem regime escolha — assalariados estão no regime IRPS por defeito. NUIT é gerado ou recuperado.

### F2 — NUIT digital QR
Hero card. Patrão scaneia para registar trabalhador automaticamente no sistema de retenções. Substitui cópia física do BI/NUIT.

### F3 — IRPS retido visível em tempo real
Sistema cruza com o sistema de retenções da empresa. Cada mês, mostra o salário declarado, a retenção feita, a entrega à AT. Se a empresa retém mas não entrega à AT em 30 dias, alerta vermelho.

### F4 — Alerta de patrão em incumprimento
Se o empregador retém mas não entrega à AT, banner red. Trabalhador pode reportar à AT directamente do app (sem retaliação possível — denúncia anónima).

### F5 — Declaração anual IRPS pré-preenchida
Em Março de cada ano, app abre wizard. Pré-preenchido com: salário declarado pela empresa, retenções, deduções (saúde, educação dos filhos cruzado com SIGE, INSS). Trabalhador acrescenta: rendas, outros rendimentos. Submete em 5 minutos.

### F6 — Situação fiscal regular
Badge verde: "Regular". Permite participar em concursos públicos, pedir empréstimos, etc. Se irregular, aparece a razão e o caminho para regularizar.

### F7 — "Onde vai o meu imposto" interactive
Para o IRPS retido este mês, o sistema decompõe segundo o Orçamento do Estado:
- Educação: 23% → 2 960 MZN
- Saúde: 18% → 2 317 MZN
- Defesa: 12% → 1 544 MZN
- Infra-estrutura: 14% → 1 802 MZN
- Pensões: 9% → 1 158 MZN
- Segurança: 7% → 901 MZN
- Justiça: 5% → 644 MZN
- Administração: 8% → 1 030 MZN
- Outros: 4% → 514 MZN

Cada categoria liga-se ao sistema relevante: Educação → SIGE/dashboard educação · Saúde → MISAU dashboard · Infraestrutura → projectos do govdigital · Pensões → INSS.

### F8 — Reembolso pedido
Se a declaração anual mostra retenções > IRPS devido, app sugere pedir reembolso. Wizard simples: confirma IBAN, submete, prazo legal de 60 dias.

---

## 4. Components & patterns

| Component | Cidadão |
|---|---|
| NUIT card | Hero, sempre visível na home |
| IRPS chart 12m | Bars com IRPS retido por mês |
| "Onde vai" donut | Decomposição visual do imposto |
| Cross-link card | Para Saúde · Educação · Governo |
| Banner red | Patrão não entrega à AT |

---

## 5. UI states críticos

### 5.1 Patrão não entregou retenção
Banner red persistent: *"A sua empresa reteve 8 200 MZN em IRPS este mês mas não entregou à AT (prazo: dia 20). Reportar à AT?"*

### 5.2 Mudou de empregador
*"Detectado novo empregador: Vodacom Mz · NUIT 400 102 880. Confirmar?"*

### 5.3 Declaração anual disponível
Banner amber em Mar: *"Declaração IRPS 2025 disponível. Pré-preenchida — confirme em 5 minutos."*

### 5.4 Reembolso devido
Banner green: *"As suas retenções somaram 780 000 MZN, mas o IRPS devido para 2025 é 696 692 MZN. Tem direito a reembolso de **83 308 MZN**."*

### 5.5 Sem rede
*"Sem rede. Última actualização: ontem 18:42."*

---

## 6. Cross-system

Cidadão lê de:
- **eBI · Governo Digital** — identidade
- **Sistema de retenções AT** — IRPS retido pela empresa
- **MISAU · SIGE** — para deduções automáticas (saúde, educação dos filhos)
- **OE · Governo Digital** — para "Onde vai o meu imposto"

Cidadão escreve a:
- **Portal AT** — declarações submetidas, denúncias de incumprimento
- **SISTAFE** — pagamentos (saldo a pagar) ou recebimentos (reembolso)

---

## 7. Open questions for v0.4

- "Onde vai" granularidade: por município? por projecto?
- Alertas push de marcos fiscais (declaração anual, reembolso recebido)
- Suporte a famílias (deduções por dependentes em conjunto)
- Integração com app do Governo Digital para pedido de Certidão Negativa de Dívidas

---

*Authoritative for Cidadão. DESIGN-system.md wins on conflict.*
