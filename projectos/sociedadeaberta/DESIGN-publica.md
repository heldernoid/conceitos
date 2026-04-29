# DESIGN-publica.md — Surface Pessoa pública · ficha agravada

**Status:** v0.3 · Abril 2026
**Surface:** 2 de 5
**Persona-alvo:** Eng. Augusto Nhantumbo (fictício) · DG empresa pública · NUIT 100 884 218

---

## 1. Propósito

Ficha "agravada" para pessoas com obrigação de declaração de bens (Lei 16/2012). Todos os elementos visíveis na ficha do cidadão comum, mais:

- Trajectória profissional pública completa
- Bens declarados Lei 16/2012 ano-a-ano
- Cálculo automático de discrepância patrimonial
- Empresas detidas com cadeia accionista visível
- Contratos públicos ganhos por entidades ligadas
- Timeline pública de processos CIP em curso

A persona Eng. Nhantumbo apresenta um caso paradigmático de discrepância (rácio 14,2×) com conflito de interesses estrutural (empresa detida ganha contratos da empresa pública dirigida pelo próprio).

---

## 2. Princípios

### 2.1 "Agravada" não significa punitiva
A ficha apresenta dados, não conclusões. Banners ink + amber explicitamente lembram que discrepância "não é prova de ilícito" — é sinal estatístico. O direito ao contraditório é absoluto e visível.

### 2.2 Coluna visual imediatamente diferenciada
Cabeçalho preto com bordadura vermelho-redaction sinaliza que se está numa ficha agravada. `.public-mark` aparece junto do nome em listas. Avatar com bolinha de "pessoa pública".

### 2.3 Cálculo automático de discrepância
A peça mais polémica do pacote. Sistema cruza rendimento declarado AT (5 anos) com bens declarados Lei 16/2012 e calcula rácio. Se &gt; 3× para pessoa pública, dispara processo CIP automático.

### 2.4 Conflito de interesses visível
Quando uma pessoa pública detém empresa que ganha contratos da entidade que dirige, isto é detectado e flag aparece automaticamente na cadeia accionista.

### 2.5 Timeline pública do processo CIP
Cidadão acompanha em tempo real cada decisão · transparência também sobre o processo de avaliação.

---

## 3. Cenas (7)

| # | Cena | Componente principal |
|---|---|---|
| 1 | Cabeçalho · ficha agravada | Hero preto+vermelho · 4 KPIs · banner red de discrepância |
| 2 | Trajectória profissional | Timeline vertical · 26 anos · 5 cargos |
| 3 | Bens declarados Lei 16/2012 | `.table` · 9 itens · cross-tags por categoria |
| 4 | Discrepância · cálculo | `.disc-card` grande · timeline CIP em coluna lateral |
| 5 | Empresas detidas · cadeia | `.net-card` SVG · 3 NUELs + 2 contratos |
| 6 | Contratos públicos | Tabela · 2 contratos · banner red de conflito · pull-quote do Savana |
| 7 | CIP timeline pública | Timeline vertical com 8 passos · 5 done + 1 active + 2 pending |

---

## 4. Componentes signature

- Hero header `var(--ink-noir)` + `var(--red-500)` border-bottom — distinção imediata
- `.disc-card` ampliado em Cena 4 (ratio 36px)
- `.net-card` em Cena 5 com 3 níveis de relacionamento
- `.public-mark` recorrente
- `.ficha public` com `ficha-tag` "Pessoa pública"
- Timeline com bullets coloridos (verde done, amber active pulsing, cinza pending)

---

## 5. Limiares de tolerância

| Pessoa | Rácio P/R aceitável | Limiar de flag automática | Limiar CIP automático |
|---|---|---|---|
| Cidadão comum | &lt; 5× | 5×-10× | &gt; 10× (raro, requer prova) |
| Pessoa pública | &lt; 3× | 3×-5× (alerta amarelo) | &gt; 5× (CIP abre processo) |

Nhantumbo: 14,2× → CIP automático, audição obrigatória.

---

## 6. Cross-system

`cross-CIP` `cross-PGR` `cross-CCEP` `cross-AT` `cross-NUEL` `cross-Terras` `cross-INC` (jornalismo) · `cross-Bo Moçambique` · `cross-Contratação Pública UFSA`

---

## 7. Personas mencionadas (todas fictícias)

| Persona | Papel |
|---|---|
| Eng. Augusto Nhantumbo | Alvo principal |
| Maria Sumane | Cônjuge · 10% Costa Norte |
| Pedro Sitole | Vogal CA · ex-CFM |
| Helena Cossa | Auditora ROC |
| Cristina Tembe Cossa | Vogal independente cooptada 2024 |
| Dr. Henriques Mucavele | Relator CIP |
| Costa Norte Logística SA | Empresa detida 84% |
| MTS Investments Lda | Holding intermediária |
| Mussassa Agro Lda | Empresa periférica |
| Portos & Caminhos de Ferro Norte SA | Empresa pública adjudicante (fictícia) |

---

## 8. Edge cases

- **Pessoa pública recém-nomeada** (&lt; 60 dias) → KPIs ainda em construção, ficha mostra "em processo de inventariação"
- **Pessoa pública não entregou Lei 16/2012** → flag amber permanente · CCEP notifica · impossibilidade de exercer cargo após 90 dias
- **Pessoa pública após cessação de funções** → ficha mantém-se 10 anos (limiar Lei 7/2014) · depois transita para "ex-pessoa pública"
- **Cônjuge / familiares ligados** → entram cross-eBI com tag "familiar de pessoa pública" · acesso diferenciado
- **Discrepância tem explicação documentada** → réplica anexa-se à ficha sem alterar números (Cena 6 do Titular)
