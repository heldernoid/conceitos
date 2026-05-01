# DESIGN-biblioteca.md — Surface 4 · Biblioteca Pública Nacional

**Status:** v0.3 · Abril 2026
**Form factor:** Public web. Desktop floor 1024 px; full responsive down to 360 px (read mode is critical on phone).
**Primary users:** Alunos, professores, cidadãos lusófonos. **Open** — no login required for reading. Login optional for marcadores e notas pessoais.
**Setting:** Sala de aula, casa, biblioteca municipal, rede 2G no Niassa. Often the user has 2 minutes and an idea of what they want to find.

---

## 1. Product purpose

The Biblioteca Pública Nacional is a **public knowledge surface**. Three things only:

1. **Manuais escolares INDE** — every official manual for every classe, in every disciplina, free, downloadable, offline-capable. The end of the era of "o manual não chegou à minha escola".
2. **Literatura moçambicana** — Mia Couto, Paulina Chiziane, José Craveirinha, Lília Momplé, Ungulani Ba Ka Khosa, Noémia de Sousa. With the cooperation of AEMO and editoras nacionais (Plural, Ndjira, Alcance), a permanent national reading shelf.
3. **Recursos pedagógicos** — INDE, IFP, professores que contribuem com fichas de exercício, planos de aula partilháveis.

What it deliberately is *not*:
- Not an e-commerce store. Tudo gratuito.
- Not a content moderation engine for user-generated reviews. There are no public reviews.
- Not a search engine for general literature. Catálogo curado por linha editorial pública.

---

## 2. Information architecture

```
Hero
├─ Pesquisar
└─ Colecções curadas (4–6 destacadas)

Catálogo
├─ Filtros (ciclo · disciplina · tipo · autor · ano)
├─ Resultados (grid de capas)
└─ Detalhe do livro
   ├─ Capa, autor, ano, descrição, citação
   ├─ Ler online (modo sepia)
   ├─ Descarregar (PDF, ePub)
   └─ Adicionar à biblioteca pessoal (login opcional)

Colecções curadas
├─ Literatura Moçambicana (~80 obras)
├─ Manuais INDE 2026 (~300 manuais)
├─ Recursos para Professores (~120 fichas)
├─ Para EP1 (1.ª–5.ª)
├─ Línguas Moçambicanas (Macua, Changana, Sena)
└─ Documentos cívicos (Constituição, Lei do SNE, etc.)

Sobre
├─ Linha editorial
├─ Instituições contribuintes (INDE, AEMO, Plural, Ndjira, Alcance)
└─ Como contribuir

Dados abertos
└─ Catálogo CSV · API JSON
```

---

## 3. Critical flows

### F1 — Catálogo
Vista grid de capas. Filtros à esquerda (sem dropdowns escondidos): ciclo · disciplina · tipo (manual · literatura · recurso · documento) · autor · ano · língua. Sort por relevância · ano · alfabético.

### F2 — Detalhe do livro
Capa (2:3, paleta de disciplina ou sépia para literatura), título em serif, autor + ano, sinopse curta, citação representativa (≤30 palavras). Botões: **Ler online**, **Descarregar PDF**, **Adicionar à minha biblioteca** (login opcional). Metadata: editora, ISBN, idioma, páginas, instituição contribuinte.

### F3 — Modo leitura
Fundo sépia (`--sepia-100`), texto Plex Serif 16/1.7 por defeito, ajustável (16/18/20/22, sépia/branco). Marcadores (login). Sem partilha social. **Sem rastreio de leitura para fora da App.**

### F4 — Colecções curadas
Páginas tipo "vitrina" — uma colecção é um conjunto curado por uma instituição (INDE para manuais, AEMO para literatura) ou por uma editor da DED. Linha editorial é pública.

### F5 — Pesquisa
Campo principal no hero. Resultados em < 200 ms (catálogo cached). Operadores simples: `autor:`, `disciplina:`, `ciclo:`, `ano:`. Sugestões enquanto se escreve.

### F6 — Contribuir
Para professores: submeter recurso pedagógico (ficha de exercícios, plano de aula). Revisão por DED + IFP antes de publicar. Para editoras: contactar a DED para inclusão.

### F7 — Dados abertos
CSV do catálogo completo, API JSON read-only, em `https://biblioteca.educacao.gov.mz/dados`. Para investigadores, jornalistas, e outros.

---

## 4. Components & patterns

| Component | Biblioteca |
|---|---|
| Hero | Indigo background, search box, 3 colecção tiles |
| Filter sidebar | 240 px desktop; sheet em mobile |
| Book card | 2:3 cover, subject palette gradient or sepia |
| Reader | Sepia background, Plex Serif body, typography toggle |
| Footer | Linha editorial, instituições, dados abertos |

---

## 5. Critical UI states

### 5.1 Sem rede
*"Modo offline · 8 livros descarregados disponíveis."* Tudo descarregado funciona; pesquisa cached para o que se viu antes.

### 5.2 Livro só online (com restrição editorial)
Banner sépia: *"Esta obra está disponível apenas para leitura online por acordo editorial."* (Caso de Niketche e algumas obras AEMO em que a editora pediu não-descarregamento).

### 5.3 Manual INDE em revisão
Banner âmbar: *"Versão 2026 deste manual está em revisão pelo INDE. Esta é a versão 2024."*

---

## 6. Voice & tone

- **Bibliotecário, não vendedor.** Sem "best-seller", sem "trending".
- **Curador, não algoritmo.** As colecções são assinadas: "Coleção curada por AEMO" / "Curada por INDE 2026" / "Curada pela DED".
- **Plural Português.** PT-MZ; em obras em línguas moçambicanas, o título e descrição na língua original com tradução PT.

---

## 7. Cross-system relationship

Biblioteca lê de:
- **INDE** — manuais oficiais
- **AEMO, Plural, Ndjira** — literatura
- **Caderno do Professor** — recursos partilhados (após revisão DED)

Biblioteca é lida por:
- **Caderno do Aluno** — descarrega manuais e literatura
- **Caderno do Professor** — anexa em planos de aula e TPC
- **SIGE** — link de manuais nas distribuições escolares

---

## 8. Open questions for v0.4

- Marcação de páginas em livros descarregados — sincronização entre dispositivos
- Versão impressão para distribuição em escolas sem rede
- Tradução automática para línguas moçambicanas (parceria com instituições linguísticas)
- Audio-livros (pessoas com baixa visão, baixa literacia parental)

---

*Authoritative for the Biblioteca Pública surface. DESIGN-system.md wins on conflict.*
