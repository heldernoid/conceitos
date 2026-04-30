# DESIGN-resultados.md — Surface 6 · Resultados públicos

**Status:** v0.4 · Surface 6 de 7
**Persona protagonista:** ninguém · esta surface é colectiva · qualquer cidadão acede
**Forma:** desktop · live updates · arquivo histórico · transmissão pública

---

## 1. Propósito

Transparência total · contagem por mesa em tempo real · histórico desde 1994 · auditoria cidadã com API pública · contestações geridas pelo TES · proclamação solene oficial · 35 anos de jurisprudência. Cada metical de informação eleitoral é auditável por qualquer cidadão · sem login · sem pagamento · sem identificação.

Esta surface valida que cross-Sociedade Aberta (Pacote 9) atinge o seu cumprimento mais alto · resultados eleitorais como bem público · não como propriedade de comissão.

---

## 2. Princípios

1. **Live + arquivo · ambos sempre acessíveis** · contagem 2029 + histórico 1994
2. **3 níveis de auditoria cidadã** · 30 segundos / 5 min / 1+ hora (pesquisador)
3. **API REST pública · open data** · sem chave · 1 000 req/h · cross-Sociedade Aberta
4. **Contestações lista pública · não escondidas** · 8 graves · todas em apuração
5. **Proclamação solene · serif gold** · variação tonal · momento cerimonial único
6. **Jurisprudência TES · 35 anos** · arquivo pesquisável · estudantes e jornalistas
7. **Resultado provisório vs final** · distinção clara visualmente

---

## 3. Cenas (7)

| # | Título | Cenário |
|---|---|---|
| 01 | Live nacional · 21:42 · 84% mesas | Noir · 4 partidos · MDP lidera 38,2% · live |
| 02 | Por mesa · Mesa 0142 destacada | Detalhe · 7 assinaturas · acta hash |
| 03 | Histórico · 1994-2029 · 7 eleições | Tabela · participação subindo · arquivo aberto |
| 04 | Auditoria cidadã · 3 níveis | API REST · cidadão atento · pesquisador |
| 05 | Contestações · 8 graves · TES decide | Lista pública · processo 14 dias |
| 06 | Proclamação solene · TES · 28.10 | Cerimonial · serif gold · Beatriz Cossa Tembe eleita |
| 07 | Jurisprudência TES · 35 anos | 8 marcos históricos · pull quote Dr. Salomão Bila |

---

## 4. Componentes signature usados

- `.contagem-publica` (Cenas 1, 2, 6) · 4 partidos com cor · live update
- `.gauge-participacao` (não usado aqui directamente · referenciado em Painel STED)

---

## 5. Cross-system

- `cross-TES` · contestações · proclamação · jurisprudência
- `cross-Sociedade Aberta` · API pública · arquivo permanente
- `cross-RM/TVM` · transmissão pública cerimónia
- `cross-OCI` · contagem cruzada validada
- `cross-Vida Civil` + `cross-eBI` + `cross-Terras` · auditoria cidadã transversal
- `cross-MININT` · ordem nas cerimónias

---

## 6. Edge cases

- **Resultado provisório vs final** · 84% mesas → 100% mesas · diferença 14 dias
- **Discrepância OCI ↔ STED** · 8 mesas · TES re-conta boletins físicos
- **Contestação grave · partido perdedor** · processo TES · 14 dias · recurso
- **Sondagens à boca da urna** · proibidas até 19:00 · cross-MININT fiscaliza
- **Servidor sob ataque DDoS** · backup 4G + offline · papel é decisivo
- **Resultado contestado · partido recusa** · TES decide · MININT garante segurança institucional
- **Pesquisador identifica anomalia** · API · publica paper · TES analisa

---

## 7. Personas referenciadas

- **Beatriz Cossa Tembe** · MDP · presidente eleita 2029 · 38,4%
- **Anastácio Mahique** · PVN · 31,9% · 2.º
- **Florêncio Sumane** · UC · 19,7% · 3.º
- **Esperança Macamo** · AT · 10,0% · 4.º
- **Dr. Salomão Bila** · presidente TES · proclamação solene
- **Aurélio Tembe** + Mesa 0142 · cross-Surface 4
- **Joana Mahique Cossa** · cross-Surface 5

---

## 8. Open questions

- **2.ª volta · se ninguém atinge 50%?** · MZ tem · processo idem
- **Eleições parlamentares e autárquicas** · simultâneas ou separadas? Boletins múltiplos?
- **Resultado por circuito (não só nacional)** · análise geográfica fina
- **Análise estatística automática** · Benford · clustering · alerta automático?
- **Imprensa · cobertura ao vivo** · regulação cross-RM/TVM · neutralidade
