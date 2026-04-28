# DESIGN-cadastro.md — Surface 4 · Cadastro Predial · DUATs

**Status:** v0.3 · Abril 2026
**Form factor:** Web desktop (1280+ floor) for DPCT staff and conservadores; mobile responsive subset for cidadão.
**Primary users:** DPCT (Direcção Provincial de Coordenação Territorial), conservadores do registo predial, técnicos cadastrais. Cidadãos consultam DUATs em seu nome ou disputam sobreposições.
**Setting:** DPCT provincial offices, urban registos prediais, occasionally field tablets. Land disputes drive 23% of cível volume in Maputo.

---

## 1. Product purpose

A terra é o conflito mais frequente em Moçambique. **Lei de Terras 19/97** estabelece que toda terra pertence ao Estado e que cidadãos e entidades obtêm DUATs (Direito de Uso e Aproveitamento da Terra) — não propriedade plena. Sobreposições, transmissões irregulares, e disputes de fronteira alimentam tribunais cíveis, comerciais e comunitários.

Esta superfície existe para:

1. **Mapa interactivo de DUATs** — visualizar parcelas, estado, processo aberto.
2. **Conflitos de sobreposição** — destacar onde dois DUATs se sobrepõem, tornar visível antes de agravar.
3. **Cross-link com tribunais** — ver acções judiciais sobre uma parcela, e referenciar parcelas em sentenças.
4. **Solicitar / transferir DUAT** — para cidadãos, com fluxo orientado.

Deliberadamente *não*: não é Google Maps, não é cadastro fiscal (isso é Finanças Digitais), não é mercado imobiliário.

---

## 2. Information architecture

```
Painel DPCT (interno)
├─ Mapa nacional (zoom em parcelas locais)
├─ Conflitos de sobreposição (lista priorizada)
├─ DUATs por estado (em registo, registado, em conflito, anulado)
├─ Pedidos pendentes (cidadão · empresa)
└─ Estatísticas (área registada, tempo médio de registo)

Detalhe do DUAT
├─ Parcela no mapa
├─ Titular (cidadão ou empresa)
├─ Histórico (transmissões, alterações, conflitos)
├─ Processos judiciais activos sobre a parcela
└─ Documentos (escritura, planta, parecer)

Cidadão (mobile · subset)
├─ Os meus DUATs
├─ Mapa local (zonas autorizadas vs proibidas)
├─ Solicitar DUAT novo
└─ Ver conflitos sobre o meu DUAT
```

---

## 3. Critical flows

### F1 — Mapa nacional · Maputo zoom
- Vista nacional (mz-provinces.svg) com 11 províncias coloridas por densidade de DUATs
- Click em província → zoom para mapa local (parcelas a brass, conflitos a vermelho)
- Filtros: tipo de uso (habitacional · comercial · industrial · agrícola · misto), estado, ano

### F2 — Detalhe do DUAT
- Header: número DUAT, área, titular, estado
- Mapa SVG da parcela
- Cronologia de transmissões
- Processos judiciais activos (cross-link Portal MJCR)
- Documentos (escritura, planta, parecer técnico)

### F3 — Conflito de sobreposição
- Mostrar visualmente os dois DUATs sobrepostos
- Histórico de cada DUAT (qual foi registado primeiro)
- Acções: abrir mediação · escalar para tribunal · pedir perícia · suspender ambos

### F4 — Transferir DUAT
- Two-step + OTP do conservador
- Verificar identidade do recebedor (eBI)
- Verificar pagamento de SISA (cross-Finanças)
- Gerar nova escritura · selo brass

### F5 — Solicitar DUAT novo (cidadão · mobile)
- Indicar zona desejada (no mapa)
- Sistema verifica se zona está disponível, em conflito, ou proibida
- Pré-pedido enviado a DPCT
- Acompanhamento na app Cidadão

### F6 — Cross-link com sentenças judiciais
- Sentença em P-2026-CIV-MAP-00481 → actualiza DUAT da fracção em causa
- Sentença em P-2025-CIV-MAP-04218 (Construtores União vs Município) → eventualmente reverte DUAT comercial

### F7 — Cancelar DUAT (DPCT · two-step)
- Quando há sentença transitada em julgado de anulação
- Two-step + OTP + justificação ≥ 100 chars com referência ao processo judicial

---

## 4. Components & patterns

| Component | Cadastro |
|---|---|
| Mapa nacional SVG | mz-provinces.svg, intensidade de cor = densidade de DUATs |
| Mapa de parcelas | SVG com `.parcela` (brass), `.parcela.dispute` (vermelho), `.parcela.cidadao` (verde) |
| DUAT card | Slate gradient, número DUAT, titular, área |
| Cronologia | Timeline de transmissões |
| Conflict diff | Side-by-side dos dois DUATs sobrepostos |
| Cross-link badges | "Processo aberto", "Sentença pendente", "Apelação" |

---

## 5. Critical UI states

### 5.1 Sobreposição detectada
*"Esta parcela sobrepõe-se 18% com DUAT-2025-MAP-000482 (titular: Construtora MZ Lda). Conflito não resolvido. Tribunal pendente: P-2026-COM-MAP-00128."*

### 5.2 DUAT em zona protegida
*"Zona não disponível para DUAT habitacional · reserva ecológica. Pode solicitar parecer ambiental."*

### 5.3 SISA por pagar
*"Transmissão suspensa: SISA de 248 000 MZN não paga. Pague via SISTAFE → para concluir."*

### 5.4 Sentença pendente
*"Esta parcela está sob acção judicial activa P-2026-CIV-MAP-00481. Transmissão bloqueada até trânsito em julgado."*

---

## 6. Cross-system

Cadastro lê de:
- **Portal MJCR** — sentenças sobre DUATs
- **Cidadão / Justiça** — pedidos de DUAT novo
- **Finanças Digitais** — pagamento de SISA
- **eBI · Governo Digital** — identidade do titular

Cadastro escreve a:
- **Registos Públicos** — escritura associada ao DUAT
- **Portal MJCR** — flagging de DUATs sob acção
- **Cidadão / Justiça** — actualizações sobre os meus DUATs
- **dados.justica.gov.mz** — agregado de conflitos por província

---

## 7. Open questions for v0.4

- Importação de cadastro tradicional/régulo
- DUATs comunitários (Lei de Terras prevê propriedade comunitária)
- Geo-fencing de zonas protegidas (parques, faixa litoral)
- Mobile field tablets para técnicos cadastrais

---

*Authoritative for Cadastro. DESIGN-system.md wins on conflict.*
