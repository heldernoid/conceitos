# DESIGN-painel.md — Surface 1 · Painel STED

**Status:** v0.4 · Surface 1 de 7 · destacada
**Persona protagonista:** Dra. Adelina Cuamba · coordenadora STED provincial Inhambane
**Forma:** desktop frame · noir variant · painel de gestão eleitoral

---

## 1. Propósito

Surface destacada do pacote. Visão de comando da coordenadora STED provincial Inhambane · sistema "entre eleições" · 30 meses até Eleições Gerais 2029. Combina: pulse de inscrições/purgas em tempo real, cobertura nacional por província, mesas atribuídas por proximidade, observadores OCI credenciados, decisões pendentes diárias, auditoria pública aberta.

Esta superfície existe para mostrar **a quem coordena entre eleições** · um sistema vivo · não um arquivo morto.

---

## 2. Princípios

1. **Variant noir** · cabeçalho tinta-900 · destaca dourado e carimbo dos KPIs e decisões
2. **Sistema "entre eleições" é o estado normal** · contagem de eleições é a excepção · 30 meses de manutenção quotidiana
3. **Pulse-recenseamento como signature** · sistema vivo · 228 eleitores/dia
4. **Mapa de cobertura como narrativa** · 96,8% Inhambane vs 84,2% Cabo Delgado · contexto histórico
5. **4 decisões hoje · sempre visíveis** · não enterradas em sub-menus
6. **Auditoria como direito · não privilégio** · cidadão acede sem login

---

## 3. Cenas (7)

| # | Título | Componente principal |
|---|---|---|
| 01 | Painel STED nacional · Adelina | Cabeçalho noir + 4 KPIs + decisões pendentes |
| 02 | Cadernos vivos · pulse | `.pulse-recenseamento` + tabela variação 30 dias |
| 03 | Mapa nacional · cobertura | Mapa MZ choropleth + tabela 11 províncias |
| 04 | Mesas atribuídas · 2 184 | `.mesa-card` 3 estados + tabela 14 distritos |
| 05 | Observadores OCI · 2 184 | KPIs + tabela organizações + 14 países |
| 06 | Decisões hoje · 4 itens | 4 cards · 2 urgentes + 2 estratégicas |
| 07 | Auditoria pública · cross-Sociedade Aberta | Hash · API · open source |

---

## 4. Componentes signature usados

- `.pulse-recenseamento` (Cena 2) · número grande dourado · lista cronológica
- `.mesa-card` (Cena 4) · 3 estados normal/alta/cheia
- KPIs grandes em variantes dark e cores

---

## 5. Cross-system

- `cross-Vida Civil` · principal · auto-inscrição + purga
- `cross-eBI` · validação biométrica
- `cross-Terras` · endereço para mesa
- `cross-CFJP` · régulos confirmam zonas rurais
- `cross-Resiliência Climática` · plano contingência ciclones Out 2029
- `cross-OCI` · observadores credenciados
- `cross-TES` · contestações
- `cross-Sociedade Aberta` · transparência amplificada
- `cross-DNRN` · correcções de cédula

---

## 6. Edge cases

- Cobertura Cabo Delgado 84,2% · conflito armado + Chido · cross-Vida Civil reconstitui via régulos
- Mesa 0418 cheia (500/500) · novos eleitores vão para 0512 vizinha
- Sr. Domingos Cossa contesta purga incorrecta · cross-Vida Civil revisão urgente
- D. Hortência negada auto-inscrição · data nascimento errada · cross-Vida Civil + DNRN
- Plano contingência ciclones · TES tem que homologar adiamento se necessário

---

## 7. Personas referenciadas

- **Dra. Adelina Cuamba** · protagonista · coordenadora STED Inhambane
- **Sr. Domingos Cossa** · 71a · contestação purga · caso urgente
- **D. Hortência Macuácua** · 28a · auto-inscrição negada · caso urgente
- **Aurélio Tembe** (Surface 4) · presidente Mesa 0142
- **Joana Mahique Cossa** (Surface 5) · observadora OCI

---

## 8. Open questions

- Painel para coordenadora **distrital** vs **provincial** · diferentes níveis?
- Versão Maputo nacional · agregação 11 províncias?
- Modo "dia eleitoral" · UI muda · 18 422 mesas em paralelo · alta densidade?
