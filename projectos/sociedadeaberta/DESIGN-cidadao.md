# DESIGN-cidadao.md — Surface Cidadão · pesquisar

**Status:** v0.3 · Abril 2026
**Surface:** 1 de 5 · destacada
**Persona:** Felisberto Manjate · BI 110100442918 · cidadão comum (continuidade Terras Digitais)

---

## 1. Propósito

A interface principal do directório. Qualquer cidadão pode pesquisar qualquer outro pelo nome, NUIT, BI ou NUEL, e ver a sua ficha pública: rendimentos declarados, IRPS pago, DUATs detidos, NUELs ligados, evolução patrimonial 5 anos.

A Cena 7 (aviso ético antes de consultar pessoa pública) e o card escuro recorrente "Sempre lembra: a consulta é simétrica" sinalizam ao utilizador que ele está numa relação de transparência mútua, não de vigilância unilateral.

---

## 2. Princípios

### 2.1 Universalidade do acesso
Toda pesquisa é gratuita por direito constitucional. Não há "tier premium". Não há "verificação adicional". Todos os cidadãos com eBI têm acesso idêntico.

### 2.2 Identidade visível sempre
Não há pesquisa anónima. O sistema regista cada consulta com identidade civil completa do consultor — visível no Surface 5 do titular consultado.

### 2.3 Aviso ético antes de pessoa pública
Cena 7 confirma propósito antes da primeira consulta de pessoa pública por sessão. Não restringe — apenas explicita as consequências.

### 2.4 Tendências reveladoras
"Pessoas mais consultadas em 30 dias" é informação pública e sinaliza interesse colectivo. Útil para jornalismo, sociedade civil, e o próprio CIP.

---

## 3. Cenas (7)

| # | Cena | Componentes |
|---|---|---|
| 1 | Página inicial · pesquisar | Hero serif XL · campo de pesquisa proeminente · 3 cards orientadores |
| 2 | Resultados de pesquisa | Filtro-badges · cards com `.public-mark` em pessoas públicas |
| 3 | Ficha cidadão comum · Reginaldo | `.ficha` cidadão · KPIs simples · cross-tags ok |
| 4 | Histórico fiscal próprio | `.ledger-row` 5 anos · uma linha em flag · ferramentas de ficha própria |
| 5 | DUATs detidos · cross-Terras | 2 cards lado-a-lado · síntese patrimonial com rácio P/R |
| 6 | Quem me viu · auditoria recíproca | `.consult-log` · 14 entradas · 1 com flag · banner com tom escuro reforçando princípio |
| 7 | Aviso ético antes pessoa pública | Modal-style · 5 pontos · ficha visualizada · botão "Continuar" |

---

## 4. Componentes signature

- `.ficha` (cidadão preto) e `.ficha public` (vermelho) com `ficha-tag`
- `.ledger-row` com variante `.flag`
- `.consult-log` com `.clog-row` e `.consult-type` por categoria
- Cards escuros recorrentes (princípio ético) em `var(--ink-noir)` com texto em `var(--paper-3)`

---

## 5. Cross-system

| Cena | Cross | Razão |
|---|---|---|
| 1-2 | `cross-eBI` | Sessão de utilizador |
| 3-5 | `cross-AT` `cross-NUIT` `cross-NUEL` `cross-Terras` `cross-CFJP` `cross-NUSS` `cross-INSS` | Composição da ficha pública |
| 4 | `cross-AT` flag · revisão IRPS | Discrepâncias automáticas |
| 5 | `cross-Terras` | DUATs |
| 6 | `cross-CNPDP` | Auditoria de auditorias |
| 7 | — | Apenas confirmação local |

---

## 6. Edge cases

- **Cidadão pesquisa-se a si mesmo** → marca "(tu)" no resultado · ficha mostra ferramentas adicionais (exportar, reclamar)
- **Pesquisa devolve menor de idade** → não aparece, mensagem "esta pessoa não consta no directório" sem revelar idade
- **Pesquisa devolve vítima protegida** → idem, sem motivo revelado
- **Pesquisa sem resultados** → sugestões de grafia alternativa baseadas em onomástica MZ
- **Cidadão tenta pesquisar &gt; 50 fichas/h** → flag scraping · sessão suspensa, CNPDP investiga
- **Sessão eBI expira durante consulta** → consulta é interrompida, não registada parcialmente
