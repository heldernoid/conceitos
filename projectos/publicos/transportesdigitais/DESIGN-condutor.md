# DESIGN-condutor.md — Surface 1 · Condutor & Cidadão

**Status:** v0.3 · Abril 2026
**Form factor:** PWA mobile (360 × 720) · 5 línguas · USSD `*146#` fallback
**Primary user:** Cidadão moçambicano com BI · com ou sem carta · com ou sem viatura registada

---

## 1. Product purpose

A app que cabe no telemóvel de qualquer condutor moçambicano. Carta de condução digital validável por QR · viaturas com IUC e IPO no prazo · multas com pagamento M-Pesa em 30 dias · denúncia de chapa perigoso · sinistro com cross-Saúde para feridos.

Substitui:
- Carta plastificada perdida a cada 2-3 anos
- Idas ao INATTER para pagar IUC
- Multas em livro carbonado, frequentemente não recebidas
- Telefonemas a seguradoras após sinistro

Inaugura:
- Carta digital permanente · cross-eBI
- Lembretes 30 dias antes de IPO/IUC vencer
- Pagamento de multa em M-Pesa, com possibilidade de contestação em 60 dias
- Histórico completo de viaturas e infracções

---

## 2. Information architecture

```
Onboarding (sem login para pesquisar; login para acções)
└─ Hoje (default home)
   ├─ Carta digital · hero
   ├─ Próximos prazos (IPO · IUC · seguro · carta)
   ├─ Atalhos (multa · sinistro · denúncia · IPO)
   └─ Notificações
└─ Carta
   ├─ Vigente (categorias)
   ├─ Validar QR público
   ├─ Renovar (≤ 6 meses do vencimento)
   └─ Perdida / roubada
└─ Viaturas
   ├─ Lista (todas as registadas em meu nome)
   ├─ Detalhe (livrete · IPO · IUC · seguro · histórico)
   ├─ Transferir (cross-Finanças NUIT do comprador)
   └─ Importar (cross-Aduanas)
└─ Multas
   ├─ Pendentes (30 dias para pagar)
   ├─ Pagas
   ├─ Contestar (60 dias)
   └─ Histórico
└─ Sinistro
   ├─ Reportar agora (geo-localização)
   ├─ Em curso
   └─ Histórico
└─ Denúncia
   ├─ Chapa perigoso (anónima ou identificada)
   ├─ Estrada em mau estado (cross-ANE)
   └─ Histórico
```

---

## 3. Critical flows

### F1 — Onboarding · 1.ª vez
- BI digitado · cross-eBI valida
- Sistema verifica se tem carta · se sim, importa
- Sistema verifica viaturas em nome dele · cross-INATTER
- 5 línguas seleccionáveis no início

### F2 — Hoje · home view
Carta digital como hero. KPIs: 2 viaturas activas · IPO de uma viatura em 14 dias · 1 multa pendente (8 200 MZN). 4 atalhos rápidos.

### F3 — Pagar multa em 30 dias
- Multa AT-2026-MAP-04218 · 8 200 MZN · velocidade
- 3 opções: pagar agora (M-Pesa) · contestar (60 dias · Tribunal Administrativo) · pedir mais info
- Se paga em 14 dias = desconto 25% (6 150 MZN)
- Pagamento via cross-SISTAFE · M-Pesa · BCI

### F4 — IPO da viatura em 14 dias
- Lembrete a 30 e 14 dias
- Sistema mostra centros IPO próximos · cross-INATTER
- Marcar inspecção · disponibilidade em tempo real
- Após IPO aprovada · livrete actualizado automaticamente

### F5 — Reportar sinistro
- Botão SOS na home
- Captura GPS · foto da viatura · foto do local
- Cross-Saúde · se há feridos, ambulância via NUS
- Cross-PRM · auto policial obrigatório se há feridos
- Cross-seguradora · participação automática

### F6 — Denunciar chapa perigoso
- Anónima ou identificada
- Matrícula scaneada por câmara · ou digitada
- Tipo de infracção: excesso lotação, condutor embriagado, viatura em mau estado, pagamento abusivo
- Se anónima · IGT-equivalente envia ao INATTER · se identificada · há follow-up

### F7 — Renovar carta
- 6 meses antes do vencimento
- Se sem alterações de saúde/visão · renovação online (cross-Saúde valida atestado vigente)
- Se com alterações · agendamento de exame médico
- Pagamento taxa via M-Pesa · 1 850 MZN

---

## 4. Components & patterns

| Component | Condutor |
|---|---|
| Phone frame | 360 × 720 |
| Driver card | Hero da home |
| Plate (matrícula) | Em cards de viatura · scanner |
| Licence (serifada) | Expansão da carta |
| Banner | IPO/IUC a vencer · multa pendente |
| Toggle de língua | 5 langs no header |
| QR scanner | Para validar carta de outro condutor |
| Bottom nav | Hoje · Carta · Viaturas · Eu |

---

## 5. Critical UI states

### 5.1 IPO em 14 dias
*"A IPO da AAB 184 MP termina em 14 dias. 8 centros IPO próximos. Marcar →"*

### 5.2 Multa pendente
*"Multa AT-2026-MAP-04218 · 8 200 MZN · excesso velocidade. 14 dias para pagar com 25% desconto. Pagar 6 150 MZN agora →"*

### 5.3 Sinistro com feridos
*"3 feridos detectados na geo-localização. Ambulância chamada via Saúde Digital. PRM-Trânsito a caminho. Permanecer no local."*

### 5.4 Renovação simples
*"A tua carta vence em 5 meses. Sem alterações de saúde, podes renovar online · 1 850 MZN. Renovar →"*

### 5.5 Denúncia confirmada
*"Denúncia anónima de chapa MQR 482 MP submetida. INATTER vai investigar. Sem follow-up directo (anónima)."*

---

## 6. Cross-system

Condutor lê de:
- **eBI · Governo** — identidade
- **INATTER** — carta · viaturas · multas
- **Saúde Digital** — atestado médico (renovação)
- **Finanças** — saldo IUC · histórico pagamentos
- **PRM-Trânsito** — autos lavrados em meu nome

Condutor escreve para:
- **Finanças · SISTAFE** — pagamentos M-Pesa
- **Saúde Digital** — pedido ambulância (sinistro)
- **PRM-Trânsito** — denúncias e sinistros
- **INATTER** — denúncias de chapa · pedidos de renovação
- **Justiça · TJ Administrativo** — contestações

---

*Authoritative for Condutor surface. DESIGN-system.md wins on conflict.*
