# DESIGN-familia.md — Surface Família · árvore genealógica

**Status:** v0.3 · Abril 2026
**Surface:** 4 de 6
**Persona:** Felisberto Manjate (visualiza a sua família)

---

## 1. Propósito

Visualização do núcleo familiar do cidadão · 3 gerações documentadas (avós, pais, ego, descendentes), 11 pessoas no caso de Felisberto. Útil para:

- Compreender vínculos legais (filiação, casamento, sucessão)
- Investigação genealógica voluntária
- Sucessão de DUATs ancestrais (cross-Terras)
- Co-titularidade · regime de bens · partilha após divórcio ou óbito

---

## 2. Princípios

### 2.1 Construção automática
Árvore montada inteiramente cross-DNRN. Cada vínculo (filiação, casamento) tem assento legal subjacente. Nenhum dado manualmente inserido pelo cidadão.

### 2.2 Vivos vs falecidos diferenciados
Verde para vivos · cinza com ✝ para falecidos · brass para recém-nascidos. Visual respeitoso · sem ostentação fúnebre.

### 2.3 Filiação não-biológica · igual representação
Adoptados, reconhecidos tarde · todos representados como filhos sem distinção visual. Tag "(adoptado)" só se titular optar por declarar. Princípio · todos os filhos são filhos.

### 2.4 Privacidade granular
3 níveis de visibilidade · Nível 1 (só eu), Nível 2 (família próxima), Nível 3 (público em Sociedade Aberta). Composição familiar é facto público para fins legais (sucessão, alimentos).

### 2.5 Genealogia voluntária além de 3 gerações
Bisavós · pode ser carregado se assentos antigos foram digitalizados. 4.ª geração para trás muitas vezes não está digitalizada · cidadão pode pedir "registo tardio" voluntário.

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Árvore familiar · 3 gerações | `.arvore-fam` SVG completo · 11 pessoas |
| 2 | Carregar 4.ª geração · bisavós | Lista + estado dos assentos antigos |
| 3 | Cônjuges · regime de bens | Card cônjuge + `.regime-card` + efeitos |
| 4 | Co-titularidade DUATs e contas | Tabela de bens · individual vs comum |
| 5 | Lara · ramo descendente | Card detalhado + timeline marcos futuros |
| 6 | Privacidade · 3 níveis | Cards lado-a-lado por nível |
| 7 | Adopção e paternidade tardia | Cards explicativos + visual de filhos |

---

## 4. Componentes signature

- `.arvore-fam` (Cena 1) — peça maior do pacote · SVG 1100×480
- `.regime-card` (Cena 3)
- `.timeline-vida` (Cenas 3, 5)
- `.av.falec` com ✝ (Cena 1)
- `.av.bebe` (Cena 1, 5)

---

## 5. Cross-system

`cross-DNRN` (assentos), `cross-eBI` (cônjuges), `cross-Terras` (DUATs comuns/individuais), `cross-Bo Moçambique` (contas conjuntas), `cross-Saúde` (cartões dependentes), `cross-Sociedade Aberta` (regime de bens), `cross-Sucessão` (herdeiros legitimários).

---

## 6. Edge cases

- **Bisavós não encontrados** (sub-registo histórico 1900-1930) → "registo tardio" com testemunhos comunitários e régulo
- **Casamento poligâmico costumeiro** (cultural em MZ) → uniões separadas no DNRN, mas árvore reconhece todas
- **Famílias reconstituídas** (re-casamento com filhos de relações anteriores) → todos os filhos representados
- **Adopção plena** → vínculos com família biológica extintos · só família adoptiva visível (privacidade)
- **Adopção restrita** → vínculos preservados em parte · raro em MZ
- **Filiação contestada** (DNA, tribunal) → cross-Justiça · árvore actualizada após sentença
- **Nome alterado em qualquer geração** → árvore mostra apenas nome actual + tag opcional

---

## 7. Personas (11 no núcleo familiar)

**Avós paternos**: João Tembe Velho (1932-2008) + Florinda Mahique (1936-2014)
**Avós maternos**: Pedro Sumane (1948) + Cremilda Tembe (1952)
**Pais Felisberto**: João Mahique Tembe (1957-2026) + Filomena Cossa Tembe (1962)
**Sogros**: Cristina Sumane Tembe (1968)
**Felisberto + Júlia** (filhos de João + Filomena)
**Joana Sumane** (cônjuge de Felisberto)
**Lara Manjate Sumane** (filha · 04.05.2026)

Todas personas fictícias.
