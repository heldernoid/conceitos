# DESIGN-efactura.md — Surface 2 · e-Factura · Trabalhador Independente

**Status:** v0.3 · Abril 2026
**Form factor:** Mobile-first PWA (Android-first), 360×760 floor. Works on cheap phones, 2G, intermittent connectivity. USSD `*146#` fallback for no-smartphone universe.
**Primary users:** Trabalhadores independentes (consultores, electricistas, costureiras, mototáxis), pequenos comerciantes, vendedores de mercado, freelancers. The 600 000+ universe of ISPC contributors plus the long tail of regime normal individuals.
**Setting:** Mercados, kiosques, oficinas, casas particulares, viagens em chapa. Daily working life. Bateria fraca, rede instável, mãos ocupadas.

---

## 1. Product purpose

The Mozambican equivalent of Portugal's e-Fatura for self-employed workers — but designed for **the realities of the Mozambican economy**: cash dominance, intermittent 2G/3G, smartphones in the lower price range, and the legal reality of two regimes (ISPC simplified for <2,5M MZN/year, regime normal for above). The fastest path to **emit a valid factura is < 30 seconds** from app open. The most complex monthly task — paying ISPC trimestral — is **1 tap**.

Three things this surface optimizes for, in order:

1. **Emit factura in under 30 seconds** — even on a 2G connection, with a bateria at 12%, with one hand while a customer waits.
2. **IRPS retido na fonte calculated in real time** — the worker sees what they keep and what the State takes, every emission. No surprises in April.
3. **ISPC trimestral in 1 tap** — system aggregates all facturas in the trimester, calculates 3%, shows the amount, pays via M-Pesa/eMola/banco in one confirmation.

Deliberately *not*: not a CRM (no client database with notes); not an accounting tool (use Comercial for that); not a banking app (no balance, no investing); not an invoicing app for empresas (that's Comercial).

---

## 2. Information architecture

```
Onboarding (NUIT lookup via BI from eBI)
└─ Hoje (home)
   ├─ ISPC do trimestre · status
   ├─ Próxima emissão (atalho)
   └─ Receita do mês (resumo)
└─ Emitir factura (the hot path)
   ├─ Cliente (NUIT / SMS / "particular")
   ├─ Item · valor
   ├─ IVA opcional (regime normal só)
   ├─ IRPS retido auto-calculado
   ├─ Confirmar · QR + SMS ao cliente
└─ Facturas
   ├─ Este mês (lista)
   ├─ Pesquisar
   └─ Anular (two-step + justificação)
└─ Pagar imposto
   ├─ ISPC trimestral · 1-toque
   ├─ INSS (se aplicável)
   └─ Histórico de pagamentos
└─ Eu
   ├─ NUIT card
   ├─ Regime fiscal (ISPC ou normal)
   ├─ Mudar regime (1 vez por ano)
   └─ USSD ajuda
```

Bottom nav: 4 destinos — Hoje · Emitir · Pagar · Eu. The "Emitir" tab uses a primary burgundy fill (the action that matters most).

---

## 3. Critical flows

### F1 — Onboarding com BI/NUIT
Utilizador abre a app pela primeira vez. Insere número de BI. Se já tem NUIT, sistema lê do **eBI** (cross-system com Governo Digital) e mostra os dados. Se não tem, gera-se NUIT de pessoa singular automaticamente (começa com 1) após validação. SMS OTP. Tempo total alvo: **< 2 minutos**.

### F2 — Setup de regime
Default é **ISPC** (3% sobre vendas, sem IVA). Se utilizador esperar facturar > 2,5M MZN/ano, escolhe regime normal (IRPS profissional + IVA 16%). Mudança de regime só pode ser feita 1 vez por ano fiscal.

### F3 — Emitir factura · hot path
Tap em "Emitir" → wizard de 3 passos:
1. **Cliente** — NUIT (auto-completar do registo), SMS para cliente sem NUIT, ou "particular" para cash sem identificação.
2. **Item · valor** — descrição livre, valor em MZN.
3. **Confirmar** — preview da factura, IRPS retido visível, QR para o cliente, SMS automático.

Para regime normal, passo 2.5 inclui IVA (auto 16%). Para ISPC, sem IVA.

Tempo alvo: **< 30 segundos** end-to-end. App lembra cliente recente para um tap.

### F4 — Receptor sem NUIT (SMS / QR)
Se o cliente não tem NUIT, factura é emitida com NUIT do emissor + identificador "particular" e número de telefone do cliente. Cliente recebe SMS com link de validação. QR também impressível em recibo de papel.

### F5 — IRPS retido na hora
Em regime normal, sistema calcula automaticamente IRPS retido (20% padrão, ou taxa específica para a profissão). Mostra ao emissor: "Recebes 8 000 MZN. AT recebe 2 000 MZN. Cliente paga 10 000 MZN." Transparência radical.

### F6 — Receita dashboard
Tap em "Hoje" → painel mensal/trimestral. Receita bruta, ISPC estimado (3%), comparação com trimestre anterior. **Sem gamificação.** Sem confetti.

### F7 — ISPC trimestral · 1-toque
Final do trimestre, banner amber: "ISPC 1.º Tri 2026: 4 200 MZN. Vence 30 Abr." Tap → preview com cálculo (3% × volume), método de pagamento (M-Pesa / eMola / BCI / BIM / Standard Bank), confirmação. **Pagamento processado em < 4 segundos** via integração SISTAFE-bancos.

### F8 — USSD `*146#` fallback
Para sem-smartphone ou bateria descarregada. USSD permite: consultar NUIT, ver receita do mês, pagar ISPC vencido, consultar última factura emitida. Interface de texto ASCII, mostrada no protótipo como "demo screen".

### F9 — INSS pagamento alongside ISPC
Para quem queira contribuir voluntariamente para INSS (segurança social), opção surge no painel "Pagar imposto" com cálculo simplificado (mínimo, médio, alto). Pago no mesmo fluxo do ISPC.

### F10 — Offline com sync queue
App funciona offline. Facturas emitidas offline ficam em fila local com hash AT temporário. Sync automático quando rede volta. Cliente recebe SMS confirmação no momento da sincronização. Banner amber visível durante offline.

---

## 4. Components & patterns

| Component | Source · variation |
|---|---|
| Phone frame | 360×760 standard |
| Bottom nav | 4 destinos · "Emitir" em burgundy |
| Factura | `.factura` reused, mono, dashed dividers |
| NUIT card | Compacta; expansível em "Eu" |
| Emit wizard | 3 passos, stepper visível |
| Big amount | `.mzn xl` para receita do mês |
| Tax chip | `.tax.ispc` ou `.tax.iva` consoante regime |
| Banner | Sticky no top quando ISPC vence ou offline |

---

## 5. UI states críticos

### 5.1 Bateria <15%
Banner amber: *"Bateria baixa. Para emitir, prefere USSD `*146#` que poupa energia."*

### 5.2 Sem rede
Banner amber, persistent: *"Sem rede. Pode emitir facturas — serão sincronizadas mais tarde. Cliente recebe SMS quando a rede voltar."* Conta de items na fila visível.

### 5.3 ISPC vencido
Banner red, persistente até pagamento: *"ISPC 1.º Tri 2026: 4 200 MZN em mora desde 30 Abr. Juros + 21 MZN/dia. Pagar agora."*

### 5.4 NUIT cliente desconhecido
Pre-emit warning: *"NUIT não encontrado. Verifique. Pode emitir mesmo assim, mas cliente não verá no histórico."*

### 5.5 Volume aproxima 2,5M MZN/ano (ISPC limite)
*"Está a 92% do limite ISPC anual (2,3M / 2,5M MZN). Se ultrapassar, deve mudar para regime normal no próximo ano."*

### 5.6 Anular factura emitida
Two-step modal. Justificação ≥40 chars. OTP por SMS. Avisa que cliente é notificado.

---

## 6. Estado vocabulário

| State | Tone | Verb |
|---|---|---|
| Rascunho | grey | Continuar / descartar |
| Emitida | burg | Ver QR · enviar SMS |
| Emitida offline | amber | (em fila · sincroniza) |
| Liquidada (cliente pagou) | green | — |
| Anulada | red | (com justificação) |
| ISPC do trimestre · em prazo | grey | — |
| ISPC · vence em <7 dias | amber | Pagar 1-toque |
| ISPC · em mora | red | Pagar com juros |

---

## 7. Cross-system

e-Factura lê de:
- **eBI · Governo Digital** — para onboarding, validar BI/nome
- **Registo NUIT (DFD)** — auto-completar NUIT do cliente

e-Factura escreve a:
- **Portal AT** — facturas emitidas alimentam dashboards do fiscal
- **SISTAFE** — pagamentos ISPC liquidados em tempo real
- **Comercial** — se cliente é empresa, factura aparece no Portal Comercial dela

---

## 8. Open questions for v0.4

- Áudio para vendedores de baixa literacia (TTS em Macua, Changana, Sena)
- Plano de prestações para ISPC em mora (actualmente liquida ou em mora; sem meio-termo)
- Importação automática de despesas via SMS bancário
- Suporte multi-NUIT (caso raro: trabalhador com 2 actividades distintas)

---

*Authoritative for e-Factura. DESIGN-system.md wins on conflict.*
