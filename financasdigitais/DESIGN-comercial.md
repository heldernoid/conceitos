# DESIGN-comercial.md — Surface 4 · Portal Comercial · Empresas e Contabilistas

**Status:** v0.3 · Abril 2026
**Form factor:** Web app desktop (1280+ floor). Used by sócios-gerentes em escritórios e por contabilistas que gerem múltiplas empresas em simultâneo.
**Primary users:** Sócios-gerentes de empresas (PME a grande dimensão), contabilistas (TOC) que gerem carteiras de empresas, técnicos de RH para folha de salários.
**Setting:** Escritórios em Maputo, Beira, Nampula. Conexão estável. Ecrã grande. Sessões longas (uma declaração de IVA mensal pode demorar 1h).

---

## 1. Product purpose

The web tool empresas use to comply with their fiscal obligations: IVA mensal, IRPC trimestral, folhas de salário com retenções, e a interface principal para o seu **contabilista**. Three things this surface optimizes for:

1. **Fluxos repetitivos eficientes** — IVA mensal, retenções salariais, devem ser feitos em minutos por contabilistas que fazem 14 empresas por mês.
2. **Multi-empresa para contabilistas** — switcher rápido. Mesmas operações em vários NUITs.
3. **Importação batch** — facturas vindas dos vendedores (CSV/XML), salários de RH (CSV), etc. Reduz transcrição manual.

Plus: certificado fiscal (regularizada), exportação para SISTAFE, gestão de procurações entre empresa e contabilista.

Deliberately *not*: not a full accounting suite (use software dedicado, integra via API); not banking; not an HR tool beyond folha de salário fiscal.

---

## 2. Information architecture

```
Login (multi-empresa switcher pós-OTP)
└─ Painel da empresa (Lojinha do João)
   ├─ Obrigações pendentes
   ├─ KPIs do mês
   └─ Avisos AT
└─ IVA
   ├─ Mensal · apuramento (IVA cobrado − IVA dedutível)
   ├─ Submeter declaração
   └─ Histórico
└─ IRPC
   ├─ Trimestral · pagamentos por conta
   ├─ Anual · declaração modelo 22 (equivalente)
   └─ Histórico
└─ Folha de Salários
   ├─ Mensal · 8 trabalhadores
   ├─ Retenção IRPS na fonte
   ├─ Mapa INSS (3% trabalhador + 4% empresa)
   └─ Mapa retenções AT
└─ Facturas
   ├─ Emitidas (cross-system com e-Factura ou Comercial)
   ├─ Recebidas (de outros NUITs)
   └─ Importar batch (CSV · XML)
└─ Contabilista
   ├─ Carteira (se sou contabilista)
   ├─ Procurações (que empresas me autorizam)
   └─ Auditoria de acessos
└─ Certificado fiscal
   └─ Pedir / renovar (Empresa Regularizada)
└─ SISTAFE
   └─ Exportar declarações para SISTAFE
```

Top bar: empresa actual com switcher; contabilista vê a carteira inteira.

---

## 3. Critical flows

### F1 — Login multi-empresa (contabilistas)
Eulália Macuácua é contabilista. Faz login. Após OTP, vê switcher com as **14 empresas** que gere. Selecciona Lojinha do João.

### F2 — Painel da empresa
KPIs do mês: IVA do mês, IRPC YTD, salários, facturas a receber, facturas pagas. Banner amber se há obrigações em prazo.

### F3 — IVA mensal
- IVA cobrado (das facturas emitidas via e-Factura ou Comercial)
- IVA dedutível (das facturas recebidas — fornecedores)
- Apuramento: IVA cobrado − IVA dedutível = a entregar (ou a recuperar)
- Submeter declaração (two-step + OTP)
- Pagar via M-Pesa Empresarial / banco / SISTAFE

### F4 — IRPC trimestral
Pagamento por conta (3 prestações no ano fiscal) baseado no IRPC do ano anterior. Sistema sugere o valor.

### F5 — Folha de Salários
8 trabalhadores. Sistema cruza com os NUITs registados como trabalhadores. Para cada um:
- Salário bruto
- INSS (3% trabalhador, 4% empresa)
- IRPS retido (escalões)
- Salário líquido
Submete mapa mensal à AT + mapa INSS ao INSS.

### F6 — Importar facturas batch
CSV ou XML padrão SAFT-MZ. Carrega 200 facturas Mar de fornecedores em segundos. Sistema valida NUITs. Marca as duvidosas.

### F7 — Procurações de contabilista
Empresa autoriza contabilista a operar em seu nome. Lista de empresas que me autorizam (vista do contabilista). Acessos auditáveis.

### F8 — Certificado fiscal · Empresa Regularizada
Documento oficial (ouro · Carimbada AT) que prova que a empresa está em dia. Necessário para concursos públicos. Pedido instantâneo se a empresa está regular; senão lista o que falta.

### F9 — Exportar para SISTAFE
Declarações IVA, IRPC, e folhas salariais exportáveis em formato SISTAFE (XML) para empresas que precisam de fluxo automatizado.

---

## 4. Components & patterns

| Component | Comercial |
|---|---|
| Top bar | Empresa actual + switcher · contabilista badge |
| Side rail | 220 px burgundy-900, secções operacionais |
| Apuramento IVA | Tabela com IVA cobrado vs dedutível |
| Salários | Tabela com 1 linha por trabalhador |
| Certificado fiscal | Selo dourado · serif preâmbulo |
| Procuração | Two-step + assinatura digital (signed token) |

---

## 5. UI states críticos

### 5.1 Atraso na declaração IVA
Banner red: *"IVA Fev 2026 venceu há 4 dias. Multa diária: 200 MZN. Submeta agora."*

### 5.2 Diferença significativa face ao mês anterior
*"IVA cobrado em Fev (12 450) é 91% inferior a Jan (140 800). Pode ser correcto, mas a AT pode questionar."*

### 5.3 Trabalhador sem NUIT
*"Trabalhador 'José Mucavel' não tem NUIT registado. Não pode ser declarado para retenção. Convide-o a registar via app Cidadão."*

### 5.4 Procuração revogada
Banner red para o contabilista: *"Lojinha do João revogou a sua procuração a 14 Abr 2026. Já não pode operar para esta empresa."*

---

## 6. Cross-system

Comercial lê de:
- **e-Factura · Comercial** — facturas emitidas pela empresa
- **e-Factura · Comercial** (de outros NUITs) — facturas recebidas
- **Cidadão Contribuinte** — para confirmar NUITs dos trabalhadores
- **Portal AT** — alertas e notificações

Comercial escreve a:
- **Portal AT** — declarações, salários, retenções
- **SISTAFE** — pagamentos, exportações XML
- **INSS** — mapa de contribuições

---

## 7. Open questions for v0.4

- Integração directa com software de contabilidade (Primavera, QuickBooks)
- Suporte para múltiplas filiais com NUITs distintos
- Aprovação multi-passo para empresas grandes (gestor → CFO → CEO)
- Bank reconciliation automática

---

*Authoritative for Comercial. DESIGN-system.md wins on conflict.*
