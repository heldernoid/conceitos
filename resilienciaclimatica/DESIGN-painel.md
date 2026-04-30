# DESIGN-painel.md — Surface 1 · Painel INGD

**Status:** v0.3 · Surface 1 de 7 · destacada
**Persona protagonista:** Eng.ª Esperança Macuácua · coordenadora INGD provincial Cabo Delgado
**Forma:** desktop frame · noir variant · painel de gestão

---

## 1. Propósito

Surface destacada do pacote. Visão de comando da coordenadora INGD provincial · pós-Chido · 184 dias após landfall. Combina: monitorização de eventos activos no Índico, mapa de risco nacional, tracker do Chido como referência histórica, recursos mobilizados, decisões pendentes diárias, cooperação SADC.

Esta superfície existe para mostrar **a quem comanda em crise** · uma única vista síntese.

---

## 2. Princípios

1. **Variant noir** · cabeçalho noir-1 + cards dark · contraste vivo do laranja-alerta
2. **KPI grid massivo** · 4 KPIs primeiros · 4 KPIs secundários · estado em segundos
3. **Pulsação onde é vivo** · `.alerta-pulsante` no topo · `.mapa-risco` com Cabo Delgado pulsa
4. **Decisões hoje à mão** · 4 acções urgentes sempre visíveis · não enterradas
5. **Histórico sempre acessível** · Idai, Kenneth, Freddy não são esquecidos · contextualizam o presente

---

## 3. Cenas (7)

| # | Título | Componente principal |
|---|---|---|
| 01 | Painel INGD nacional · Esperança | Cabeçalho noir + alerta-pulsante L2 + 4 KPIs + decisões pendentes |
| 02 | Mapa de risco nacional | `.mapa-risco` choropleth + 6 camadas + Cabo Delgado pulsa r4 |
| 03 | Tracker Chido · histórico | `.tracker-ciclone` 5 dias trajectória · cooperação Météo France |
| 04 | Histórico nacional · 6 eventos | Tabela 2019-2024 · Idai/Kenneth/Eloise/Gombe/Freddy/Chido |
| 05 | Recursos mobilizados | Abrigos abertos · bens distribuídos · voluntários · stocks |
| 06 | Decisões hoje · 4 itens urgentes | Realocação Quissanga · cólera Pemba · auditoria CIP · plano próxima época |
| 07 | Cooperação SADC | África do Sul · Madagáscar · Comores · La Réunion · Malawi |

---

## 4. Componentes signature usados

- `.alerta-pulsante` (Cena 1) · 4 níveis · vermelho/laranja pulsam
- `.mapa-risco` (Cena 2) · choropleth dinâmico
- `.tracker-ciclone` (Cena 3) · trajectória do Chido com cone de incerteza histórico
- `.abrigo-card` (Cena 5) · 3 estados (normal/cheio/lotado)

---

## 5. Cross-system

- `cross-INAM` · meteorologia parceira · partilha em tempo real
- `cross-Saúde` · surto cólera detectado · pedido reforço médico Pemba
- `cross-Terras` · realocação 218 famílias Quissanga · DUATs alternativos
- `cross-Vida Civil` · 218 famílias · óbitos Chido confirmados
- `cross-Sociedade Aberta` · auditoria CIP-2026-0142 em curso
- `cross-Cruz Vermelha · OMS · OMM` · cooperação técnica
- `cross-CIP` · processo de esclarecimento sobre fundos
- `cross-CFJP` · régulos como autoridade local

---

## 6. Edge cases

- Coordenadora vê painel · 5h da manhã · GSM intermitente · UI tem que carregar com 2G
- Decisão de realocação · 218 famílias · não pode ser tomada só pela Esperança · escala para INGD nacional + cross-Terras
- Auditoria CIP em paralelo · INGD não pode bloquear acesso · cross-Sociedade Aberta tudo público
- Surto de cólera · cross-Saúde tem prioridade absoluta · helicóptero pedido em horas

---

## 7. Personas referenciadas

- **Eng.ª Esperança Macuácua** · protagonista · coordenadora provincial Cabo Delgado
- **Aníbal Cossa** (Surface 3) · reporta diretamente
- **Maria Nhantumbo** (Surface 4) · alimenta painel via Cruz Vermelha
- **Joana Mahique Cossa** (Surface 5) · jornalista que audita

---

## 8. Open questions

- Painel para coordenadora **distrital** vs **provincial** · diferentes níveis de zoom?
- Versão simplificada para Maputo nacional · agregação de 11 províncias?
- Modo "evento agudo" · UI muda quando L3 activo · esconde estatísticas longas, mostra só accionável?
