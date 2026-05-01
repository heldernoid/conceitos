# DESIGN-empresa.md — Empresa · Portal do Investidor

**Status:** v0.3 · Abril 2026
**Surface:** 2 de 5
**Persona principal:** Greenfield Forestry SA · NUEL E-2021-MAP-008214 · investidor agro-florestal

---

## 1. Propósito

Portal web desktop para empresas, cooperativas e investidores estrangeiros que precisam de pedir DUAT em Moçambique. Diferente do Cidadão: aqui é processo formal, com várias entidades em paralelo, prazos legais, e consulta comunitária obrigatória.

Cobre o ciclo completo:

1. Identificação e categoria de uso
2. Polígono GPS · detecção automática de sobreposição
3. Consulta comunitária com régulo (obrigatória)
4. Parecer CPI (se &gt; USD 500 k)
5. Acompanhamento de pareceres em paralelo
6. Recepção do DUAT serifado

---

## 2. Princípios

### 2.1 Consulta comunitária é obrigatória, não opcional
Sem acta autenticada por régulo + validação SMS, não há DUAT. A app força o upload e bloqueia avanço. Lei 19/97 art. 13 + 17.

### 2.2 Sobreposição = bloqueio total
Sistema impede emissão de DUAT sobre polígono já demarcado. Empresa tem 3 caminhos: renunciar à área conflitante, negociar com titular existente (com supervisão SPGC), ou esperar Tribunal Comunitário.

### 2.3 Investimento estrangeiro &gt; USD 500 k = CPI obrigatório
Acima deste limiar, parecer CPI é parte integrante do processo. Componente local mínimo 30% até ao ano 5 da operação.

### 2.4 Cross-system massivo
Esta superfície tem mais cross-tags do que qualquer outra do pacote: CPI, ANAC, CFJP, TJ, NUEL, NUIT, AT, NUSS. Reflecte que pedir um DUAT empresarial é uma operação inerentemente multi-stakeholder.

### 2.5 Pareceres em paralelo, não em série
SPGC, ANAC, CPI, CFJP, TJ correm em paralelo — não em sequência. Reduz prazo total de 36 meses para 18 meses (e em casos sem conflitos, &lt; 6 meses como o exemplo Greenfield).

---

## 3. Cenas (7)

| # | Cena                              | Componentes-chave                                          |
| - | --------------------------------- | ---------------------------------------------------------- |
| 1 | Login NUEL + eBI                  | hero split-pane · cross-NUEL + cross-eBI                   |
| 2 | Pedido novo · identificação       | sidebar com stepper · 8 chips uso · banner cross-CPI       |
| 3 | Polígono GPS + sobreposição       | poly-frame grande · 3 polígonos sobrepostos · KPI panel    |
| 4 | Consulta comunitária              | comm-card régulo + lista compromissos + tabela docs        |
| 5 | CPI · investimento estrangeiro    | KPI USD · breakdown investimento · timeline + critérios    |
| 6 | Acompanhamento · pareceres paralelos | tabela 5-row pareceres + timeline + banners por pendência |
| 7 | DUAT empresarial emitido          | duat-card + duat-doc lado-a-lado · KPIs · cross-tags total |

---

## 4. Componentes signature usados

- **Sidebar com stepper vertical** (Cena 2) — única deste pacote · 6 passos
- **Polígono GPS desktop grande** (Cena 3) — 600×420 viewBox · 3 polígonos com 3 hatch patterns distintos
- **Comm-card** (Cena 4) — régulo com blockquote serifado + cross-CFJP
- **Tabela de pareceres em paralelo** (Cena 6) — 5 entidades · estados visuais
- **DUAT card + DUAT doc lado-a-lado** (Cena 7) — síntese visual + texto legal

---

## 5. Personas convencionadas

| Pessoa / entidade            | Papel                              | Cross-pacote        |
| ---------------------------- | ---------------------------------- | ------------------- |
| Greenfield Forestry SA       | Empresa requerente                 | nova · só Terras    |
| Régulo Mahique de Cheringoma | Autoridade tradicional             | reaparece em SPGC e Fiscal |
| Reg. Manjate Cossa           | Titular DUAT-1992 · ocupação BF    | conflito 0,82 ha    |
| CPI · Centro Promoção Investimentos | Real (não fictício)         | parecer estrangeiro |
| ANAC · Áreas de Conservação  | Real                               | parecer ambiental   |

---

## 6. Cross-system (matriz desta surface)

| Cena | Cross                            | Razão                                       |
| ---- | -------------------------------- | ------------------------------------------- |
| 1    | `cross-NUEL` `cross-eBI`         | Empresa registada no BAU + representante legal |
| 2    | `cross-ANAC` `cross-CPI`         | Detectada mata + investimento &gt; 500 k    |
| 3    | `cross-cadastro` (interno)       | Sobreposição automática                     |
| 4    | `cross-CFJP` `cross-NUSS`        | Acta + postos comunitários                  |
| 5    | `cross-CPI` `cross-Bo Moçambique`| Investimento estrangeiro &gt; 50% capital   |
| 6    | `cross-SPGC` `cross-ANAC` `cross-CPI` `cross-CFJP` `cross-TJ` | Pareceres paralelos |
| 7    | `cross-AT` `cross-NUSS`          | Taxa anual + postos                         |

---

## 7. Edge cases tratados

- **Sobreposição com DUAT de boa fé histórica** → empresa não pode forçar; tribunal comunitário ou cessão negociada
- **Comunidade rejeita projecto** → pedido morre no passo 4, acta tem que reflectir consenso real
- **CPI rejeita** → empresa pode reapresentar com plano corrigido (pelo menos uma vez)
- **Investimento &lt; USD 500 k** → CPI dispensado, parecer simplificado SPGC
- **Cooperativa local** (não empresa) → fluxo idêntico mas sem CPI
- **Renovação de DUAT existente** → fluxo abreviado, só consulta comunitária se uso muda

---

## 8. Open questions

- Como deve a app gerir empresas em joint-venture (NUEL + NUEL + NUEL)?
- ANAC parecer é binário (favorável / não) ou tem condicionantes? Actualmente assume condicionado.
- Tribunal Comunitário pode ter sentença adversa à empresa — qual é o caminho? Recurso? Se sim, para onde?
