# DESIGN-prm.md — Surface 4 · PRM-Trânsito · Campo

**Status:** v0.3 · Abril 2026
**Form factor:** Tablet (10–11", 980×680) for road-side enforcement; Web admin for command.
**Primary users:** ~3 800 agentes da PRM-Trânsito (Polícia da República de Moçambique · ramo de trânsito) em 11 províncias. Comandos provinciais. Comando-Geral. Articulação com PGR (Procuradoria-Geral) para crimes graves.

---

## 1. Product purpose

A frente de fiscalização rodoviária. Antes desta superfície, fiscalização era papel (boletins de ocorrência), velocidade era radar com fotografia revelada em laboratório, e pagamento de multa era via banco com prazo de 5 dias úteis (frequentemente perdido). Esta superfície substitui:

- Boletins em livro carbonado · perdidos
- Radares isolados · sem cruzamento com base nacional
- Bafômetro com leitura sem registo
- Sem visibilidade de cartas suspensas em campo

E inaugura:
- Tablet PRM com auto digital geo-referenciado
- QR scanner para carta + matrícula em segundos
- Bafômetro Bluetooth · leitura automática no auto
- Cross-INATTER · cartas suspensas detectadas em fiscalização
- Cross-Justiça · escalada para Tribunal Administrativo

---

## 2. Information architecture

```
Sign in (cédula + senha + foto biométrica)
└─ Hoje (default)
   ├─ Operação programada (geo-localização)
   ├─ Em curso (fiscalização activa)
   └─ Atribuídas a mim
└─ Fiscalizar (em campo)
   ├─ Scanear carta + matrícula
   ├─ Verificar documentos
   ├─ Velocidade (radar)
   ├─ Álcool (bafômetro)
   ├─ EPI / sinalética da viatura
   ├─ Lavrar auto
   └─ Notificar condutor
└─ Sinistros
   ├─ Em curso (despachos cross-Saúde)
   ├─ Encerrados
   └─ Lavrar auto de sinistro
└─ Casos
   ├─ Em campo
   ├─ Resposta condutor pendente (30 dias)
   ├─ Multas pagas / pendentes
   ├─ Em recurso (cross-Justiça)
   └─ Suspensões cross-INATTER

Admin web
└─ Painel nacional
   ├─ Mapa de risco (sinistros · multas · álcool)
   ├─ KPIs (operações · autos · multas · acidentes)
   └─ Sectores de foco
└─ Planeamento
   ├─ Operações trimestrais
   ├─ Pontos negros (sinistralidade)
   └─ Atribuir agentes
└─ Relatórios
   ├─ Mensal · ao MTC
   └─ Public · dados.transportes.gov.mz
```

---

## 3. Critical flows

### F1 — Início de turno
- Agente entra · cédula + senha + foto biométrica
- Tablet mostra operações do dia · 3 fiscalizações geo-pinned
- Cada uma com contexto: porquê (rotina · ponto negro · denúncia)
- Carregamento offline antes de sair

### F2 — Mandar parar viatura
- Agente vê viatura em movimento
- Tablet pode scanear matrícula em movimento (câmara)
- Cross-INATTER · sistema mostra alertas (carta suspensa? IPO vencida?)
- Decide se manda parar

### F3 — Verificar documentos
- Condutor mostra QR da carta (Condutor app)
- Tablet scaneia · cross-INATTER valida em tempo real
- Mostra: cat. da carta · multas pendentes · estado
- Condutor sem app · agente digita BI · mesmo resultado

### F4 — Radar de velocidade
- Tablet conecta a radar (Bluetooth)
- Lê velocidade em tempo real
- Se >limite · agente lavra auto
- Foto da matrícula auto-anexada

### F5 — Bafômetro · álcool
- Tablet conecta a bafômetro (Bluetooth)
- Condutor sopra · leitura imediata
- ≤0,5 g/L OK · 0,5-1,2 g/L grave · >1,2 g/L muito grave (apreensão da carta)
- Agente lavra auto · cross-INATTER suspende imediatamente se grave

### F6 — Lavrar auto
- Sistema pré-preenche com base em discrepâncias
- Hi-vis stripe + selo PRM · serifado
- Condutor assina digitalmente (ou recusa · auto válido na mesma)
- Cross-Condutor app · multa imediata

### F7 — Atender sinistro
- Despacho da Central · GPS
- Agente chega · cross-Saúde já alertada (se feridos)
- Lavra auto de sinistro
- Cross-seguradoras · cross-Operador (se chapa)

### F8 — Escalar para Tribunal Administrativo
- Casos graves: condutor reincidente · álcool >1,2 · embate com fuga
- Cross-Justiça · cross-PGR (se crime)
- Cross-INATTER · suspensão imediata da carta

---

## 4. Components

| Component | PRM-Trânsito |
|---|---|
| Tablet frame | 980×680 |
| Touch targets | ≥48 px |
| Hi-vis stripe | Em autos · headers |
| Auto serifado | Plex Serif body · selo hi-vis |
| QR scanner | Para carta + matrícula |
| Speedometer | Velocidade em tempo real |
| Risk meter | Para condutor (histórico) |
| Map | mz-provinces.svg + density (admin) |
| Two-step modal | Apreensão de carta · escalada Tribunal |

---

## 5. Critical UI states

### 5.1 Carta suspensa detectada
*"Carta CD-2018-MAP-008412 SUSPENSA por mora · 184 dias. Condutor não pode circular. Apreender viatura."*

### 5.2 Álcool grave
*"1,42 g/L · muito grave (>1,2). Apreender carta · cross-INATTER suspende. Cross-Justiça · pode ser crime se reincidência."*

### 5.3 Recusa de assinatura
*"Condutor recusou contrassinar o auto. Auto válido na mesma · Lei 19/2007 art. 88. Foto da recusa anexada."*

### 5.4 Sinistro grave despachado
*"Sinistro INC-2026-MAP-04218 · 3 feridos · ETA 4 min. Cross-Saúde · ambulância já no local."*

### 5.5 Reincidente
*"Condutor reincidente · 4 multas em 12 meses. Recomendado · escalar para Tribunal Administrativo."*

---

## 6. Cross-system

PRM-Trânsito lê de:
- **eBI · Governo** — identidade
- **INATTER** — cartas · viaturas · multas em outras provinciais
- **Operador** — viaturas profissionais · alvarás
- **Saúde · NUS** — feridos em sinistros

PRM-Trânsito escreve a:
- **Condutor app** — autos lavrados · multas
- **INATTER** — autos · pedidos de suspensão
- **Saúde** — pedidos de ambulância
- **Justiça · TJ Adm** — escaladas
- **PGR** — crimes graves
- **Finanças · SISTAFE** — multas pagas
- **dados.transportes.gov.mz** — agregados anonimizados

---

*Authoritative for PRM-Trânsito. DESIGN-system.md wins on conflict.*
