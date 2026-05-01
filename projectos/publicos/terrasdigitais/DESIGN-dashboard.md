# DESIGN-dashboard.md — Dashboard nacional · DINAGECA

**Status:** v0.3 · Abril 2026
**Surface:** 5 de 5
**Persona principal:** Eng. P. Cossa · Director Geral DINAGECA

---

## 1. Propósito

Dashboard executivo nacional para a liderança da DINAGECA e briefings de Conselho de Ministros. Agrega dados dos 11 SPGC, indicadores ODS, receita, conflitos e cross-system com os 7 pacotes irmãos.

Cobre:

- KPIs nacionais consolidados
- Mapa MZ choropleth com SVG real (paths inline)
- Ranking dos 11 SPGC por eficiência cadastral
- ODS-1 · indicador de terra para todos
- Funil de resolução de conflitos cross-Justiça
- Receita taxa anual cross-Finanças
- Briefing para Conselho de Ministros

---

## 2. Princípios

### 2.1 Decisão sobre evidência
Dashboard não é decorativo. Cada cena leva a uma decisão concreta (intervenção, alocação, política). Cena 7 fecha o ciclo: 3 decisões pendem do CM, suportadas pelos dados das outras cenas.

### 2.2 Mapa MZ é central
Cena 2 usa o SVG geográfico real das 11 províncias (paths inline, ~95 KB). É a representação canónica de Moçambique no pacote — replicada em todas as cenas que beneficiam de visão nacional.

### 2.3 Comparação inter-provincial é honesta
Ranking SPGC mostra Manica em 1º e Cabo Delgado em 11º sem mascarar os números. Plano de intervenção é explícito.

### 2.4 ODS-1 é o âncora moral
Cobertura cadastral familiar é o KPI moral · 62% hoje, 85% meta 2030. Trajectória mostra gap de 7 pp · não há promessa fácil.

### 2.5 Cross-system visível em todo o lado
Esta superfície tem mais cross-tags do que qualquer outra. Reflecte que o cadastro nacional não vive isolado — depende de e alimenta os outros 7 pacotes.

---

## 3. Cenas (7)

| # | Cena                              | Componentes-chave                                    |
| - | --------------------------------- | ---------------------------------------------------- |
| 1 | Visão nacional                    | 4 KPIs · tabela 11 SPGC · alerta CD · stock uso      |
| 2 | Mapa MZ por uso                   | mapa SVG real inline · top províncias · top conservação |
| 3 | Ranking SPGC                      | tabela 11 linhas com score · plano intervenção 3 SPGC · boas práticas |
| 4 | ODS-1 terra para todos            | 4 KPIs ODS · barras por estrato · gráfico trajectória 2014-2030 |
| 5 | Conflitos · funil escalada        | 4 KPIs · funil 5-níveis · top 5 razões                |
| 6 | Receita taxa anual                | 4 KPIs · tabela receita por uso · método pagamento · destino |
| 7 | Briefing Conselho de Ministros    | 3 decisões · 4 indicadores mini · 4 riscos · cross-system 8 pacotes |

---

## 4. Componentes signature usados

- **Mapa MZ inline · 11 províncias** (Cena 2) — paths SVG reais geográficos, replicáveis em todas as superfícies que precisem
- **Tabela com score composto** (Cena 3) — 4 indicadores agregados, ranking 1-11
- **Trajectória ODS** (Cena 4) — gráfico de linha 2014-2030 com meta visualizada
- **Funil de resolução** (Cena 5) — 5 níveis · cores progressivas terra→red
- **Briefing CM** (Cena 7) — formato pronto-a-imprimir A4, 3 decisões + 4 riscos

---

## 5. Cross-system

| Cena | Cross                                           |
| ---- | ----------------------------------------------- |
| 1    | resumo · 11 SPGC                                |
| 2    | `cross-ANAC` · zonas conservação                |
| 3    | interno · benchmark                             |
| 4    | reporting ONU · ODS · Estatística (INE)         |
| 5    | `cross-CFJP` `cross-TJ` Justiça Digital         |
| 6    | `cross-AT` · Finanças Digitais                  |
| 7    | **TODOS** os 8 pacotes da família Conceitos     |

---

## 6. Personas

| Pessoa             | Papel                                       |
| ------------------ | ------------------------------------------- |
| Eng. P. Cossa      | DG DINAGECA · protagonista                  |
| Eng. F. Macuácua   | Chefe SPGC Manica · #1 ranking · referência |
| Ministra MTA       | Apresenta briefing CM (não-nomeada)         |
| Conselho Ministros | Audiência da Cena 7                         |

---

## 7. Edge cases

- **SPGC offline &gt; 24h** (Cabo Delgado actualmente) → flagged em vermelho, dados parciais com timestamp visível
- **Província sem polígono digitalizado** → mapa MZ mostra cinzento neutro, não verde (não confundir com "vazio = ok")
- **Receita anómala** (saltos &gt; 30%) → alerta automático ao DG · investigação cross-AT
- **Conflito mediático** (e.g., empresa estrangeira vs comunidade rural) → flag para comunicação social
- **Reporting ONU** → exporta automático em formato ODS-IAEG até 31.03 anual

---

## 8. Indicadores que vão ao Conselho de Ministros

Os 4 indicadores que o DG sempre apresenta:

1. **Cobertura ODS** (62% · meta 85%) — moral
2. **Receita 2026** (2,84 B MT · +14% YoY) — fiscal
3. **Conflitos resolvidos** (4 218 · 82% via cessão) — operacional
4. **Boa fé reconhecida** (218 k · +42 k YoY) — equidade rural

Estes 4 são os "vital signs" do sistema. Variações fortes em qualquer um disparam revisão de política.

---

## 9. Decisões pendentes Q2 2026

A Cena 7 mostra 3 decisões concretas que o CM tem que aprovar:

1. **Plano de emergência Cabo Delgado** · 42 M MT · 18 meses · cross-ANAC + CFJP
2. **Revisão tarifa industrial** +20% · receita +142 M MT/ano · aplicação Q3 2026
3. **Lei orgânica DTD** · oficialização da Direcção de Terras Digitais como camada permanente

A app gera os 3 documentos em PDF executivo formatado para A4, prontos para a sala do CM.
