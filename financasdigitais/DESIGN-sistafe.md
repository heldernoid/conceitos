# DESIGN-sistafe.md — Surface 5 · SISTAFE Interop & Transparência Pública

**Status:** v0.3 · Abril 2026
**Form factor:** Web · dual purpose. (a) Public dashboards open to citizens, journalists, researchers (`dados.financas.gov.mz`). (b) Technical admin sub-section for AT staff and SISTAFE engineers (`api.financas.gov.mz/admin`). (c) Public factura validator for QR scans (no login).
**Primary users:** Citizens (transparency dashboards), journalists, civil society (CIP, IESE), researchers, banks (validation API consumers), SISTAFE engineers.
**Setting:** News rooms, offices, civil society organizations, university research, banks. Some sessions are deep dives by analysts; others are 30-second factura QR scans by a customer.

---

## 1. Product purpose

Two distinct purposes share one surface because the underlying data is the same:

1. **Transparência pública radical.** Real-time receitas por imposto, distribuição geográfica, ligação directa ao OE (Orçamento do Estado), comparação com o previsto. The civic counterpart to the Cidadão "Onde vai o meu imposto" — but aggregate, public, downloadable.
2. **Validação técnica e dados abertos.** Validar uma factura pelo QR ou hash sem login. API documentada para integradores (bancos, software de contabilidade). Dados abertos CSV mensais. Painel técnico interno para SISTAFE-AT em tempo real.

Together they form Mozambique's fiscal transparency layer — the same data that drives the Portal AT's reports is published openly here, where any citizen, journalist, or auditor can examine it.

Reference points: Portal da Transparência (Brasil), e-Fatura Portugal validador, Iceland's national budget visualization, Open Spending UK.

Deliberately *not*: not a journalism CMS; not a personal-finance app; not an investment dashboard.

---

## 2. Information architecture

```
Landing público (dados.financas.gov.mz)
└─ Hero · receita ao vivo "Onde vai o meu imposto"
└─ Receitas por imposto · em tempo real
   ├─ IVA · IRPS · IRPC · ISPC · Aduaneiro · SISA
   └─ Comparação com previsto no OE
└─ Distribuição geográfica
   └─ Por província · DAF
└─ Ligação ao OE (Orçamento do Estado)
   └─ Cross-link para govdigital
└─ Validar factura
   └─ Input: QR · hash · número de factura
└─ API & integração
   └─ Documentação OpenAPI · sandbox
└─ Dados abertos
   └─ CSV mensal · histórico desde 2018

Painel técnico admin (autenticado)
└─ SISTAFE ↔ AT · monitorização tempo real
   ├─ Fluxos de dados
   ├─ Latência e erros
   └─ Reconciliação
└─ Integração bancos
   ├─ BCI · BIM · Standard Bank · Millennium BIM · Moza Banco
   └─ M-Pesa · eMola
```

Tabs/seções no landing: Receitas · Geografia · OE · Validar factura · API · Dados abertos.

---

## 3. Critical flows

### F1 — Hero "Onde vai o meu imposto" (público)
Receita acumulada do mês corrente, em tempo real. Decomposição donut por sector: Educação 23%, Saúde 18%, etc. Mesmo gráfico que aparece no Cidadão, mas agora com valores nacionais e cross-links a govdigital, saudedigital, educadigital.

### F2 — Receitas por imposto · tempo real
Para o mês corrente: totais por IVA, IRPS, IRPC, ISPC, Aduaneiro, SISA. Comparação com o previsto no OE 2026. Bar charts. Não é necessário login.

### F3 — Distribuição geográfica
Mapa de Moçambique. Receita por província (Cidade de Maputo, Maputo Província, Gaza, Inhambane, Sofala, Manica, Tete, Zambézia, Nampula, Cabo Delgado, Niassa). Drill-down por DAF. Comparação com população, PIB.

### F4 — Validar factura (público)
Hero: "Recebeu uma factura? Verifique se é real." Input campo único: hash, QR, ou número de factura. Resposta: válida (selo gold) ou inválida (red), com detalhes do emissor.

### F5 — API & sandbox
Documentação OpenAPI. Endpoints públicos: validar factura, consultar NUIT (existência apenas), receitas agregadas. Endpoints autenticados: integração bancária, exportação para SISTAFE. Sandbox interactivo.

### F6 — Dados abertos
CSV mensais por imposto, província, sector. Histórico desde 2018. Licença CC-BY 4.0. JSON API para investigadores.

### F7 — Painel SISTAFE ↔ AT (admin · interno)
Para SISTAFE engineers e DFD admin. Mostra fluxos em tempo real: facturas validadas/min, declarações entrando, pagamentos liquidados. Latência. Erros. Reconciliação diária.

### F8 — Integração bancos
Para banks integrating: documentação técnica + status do canal de cada banco. Disponibilidade, latência, volume.

---

## 4. Components & patterns

| Component | SISTAFE |
|---|---|
| Receita ao vivo (counter) | Mono, cresce em tempo real |
| Donut decomposição | Reuso do Cidadão, agora público |
| Mapa MZ | SVG simples · provinces clicáveis |
| OE comparison bars | Real vs previsto |
| API endpoint card | Method · path · params |
| CSV download card | Filename · size · last updated |
| Factura validator | Input + result card |

---

## 5. UI states

### 5.1 Receita actualizada agora
*"Última actualização: 28 Abr 2026 · 14:42:18 · próxima em 2 minutos."*

### 5.2 Discrepância OE vs real
Banner amber: *"IVA acumulado do trimestre está 8% acima do previsto no OE 2026. Reportar à AR."*

### 5.3 Factura inválida
Resposta vermelha: *"Esta factura não consta no registo da AT. Pode ser falsa. Reportar via *146*9#."*

### 5.4 API rate limit
Para integradores: *"100 chamadas/min sem chave. Pedir chave em api.financas.gov.mz/key."*

---

## 6. Cross-system

SISTAFE é o **eixo de leitura** do sistema:
- **Lê de**: e-Factura · Cidadão · Comercial · Portal AT (todas escrevem para o registo central)
- **Escreve a**: SISTAFE central (BdM, MEF), bancos (via API), painéis públicos
- **Cross-link de leitura** com: govdigital (OE detalhe), saudedigital (sector saúde), educadigital (sector educação)

---

## 7. Acessibilidade & princípio

- **Por defeito público.** Tudo o que não é PII fica em `dados.financas.gov.mz`. Pedido de informação não deve ser necessário para receitas agregadas.
- **CSV antes de PDF.** Formato máquina-legível primeiro. PDF é cortesia.
- **Histórico longo.** 2018 em diante.
- **Sem rastreio.** Sem analytics de terceiros. Logs anonimizados.
- **Sem login para ver.** Apenas para integrar.

---

## 8. Open questions for v0.4

- Granularidade municipal (autarquias)
- Acompanhamento de execução de projectos específicos (ex: Hospital Provincial X)
- Reconciliação automática com extractos bancários do Estado
- Auditoria pela TA (Tribunal Administrativo) embebida

---

*Authoritative for SISTAFE Interop. DESIGN-system.md wins on conflict.*
