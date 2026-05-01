# DESIGN-system.md — Terras Digitais

**Status:** v0.3 · Abril 2026
**Ownership:** DTD · Direcção de Terras Digitais (camada digital · sob MTA)
**Stakeholders:** MTA, DINAGECA, SPGC (10 províncias + Cidade de Maputo), CFJP/Tribunais Comunitários, ANAC, Autoridade Tributária (ATM), eBI, CPI

---

## 1. Sector & purpose

Terras Digitais cobre o ciclo completo do uso e aproveitamento da terra em Moçambique — uma matéria constitucional sensível, em que a terra pertence ao Estado mas é atribuída em **DUAT** (Direito de Uso e Aproveitamento da Terra) por 50 anos renováveis.

O sistema cobre quatro vias paralelas:

- **Via comum (cidadão / família)** — DUAT por ocupação de boa fé, ocupação por comunidade local, terra urbana de uso habitacional
- **Via empresarial (investidor)** — pedido novo de DUAT para fins agrícolas, industriais, turísticos · com consulta comunitária obrigatória
- **Via cadastral (SPGC)** — gestão provincial do registo, demarcação física, conflitos, sobreposições
- **Via fiscal (campo)** — verificação no terreno, GPS de demarcação, denúncia de ocupação ilegal

O sistema substitui:

- Cadastro fundiário em papel mantido nos SPGC provinciais
- Pedidos de DUAT que demoram **18-36 meses** entre aprovação provincial e título emitido
- Conflitos de terra que vão directos a Tribunal sem mediação prévia (>14 000 processos pendentes em 2024)
- Sobreposições não detectadas até o segundo titular tentar registar
- Falta de visibilidade entre SPGC, ATM (taxa anual DUAT) e Tribunais

E inaugura:

- DUAT digital com QR validável, ligado ao eBI do titular ou NUEL da empresa
- Polígono GPS demarcado por fiscal com tablet rugged · vértices georreferenciados
- Detecção automática de sobreposições no acto do pedido (cross-cadastro nacional)
- Mediação comunitária obrigatória **antes** de processo judicial (cross-Justiça)
- Pagamento de taxa anual DUAT cross-Finanças via M-Pesa
- Consulta comunitária formal para investidor, com acta digital assinada por régulo

---

## 2. Brand foundations

### 2.1 Terra ochre · primary

Cor de autoridade cadastral. Não é o castanho genérico de "terra" decorativa; é o ocre específico do solo ferroso de Moçambique central — o tom da terra batida, das estradas rurais, das paredes de adobe. Comunica enraizamento, registo, oficialidade rural.

```
--terra-900: #4A2E0E   (govstrip · DUAT-card hero)
--terra-800: #6B4416
--terra-700: #8C5A1F   (PRIMARY · botões · selos)
--terra-600: #A6691F   (anchor · ferro · paleta originária)
--terra-500: #BC7E2E
--terra-400: #CF9650
--terra-300: #DFB17C
--terra-200: #ECCBA4
--terra-100: #F5E0C5   (badges · backgrounds claros)
--terra-50:  #FBF0DD   (hover de botões secundários)
```

### 2.2 Savanna green · co-anchor

A vegetação dominante de Moçambique fora das cidades — savana arborizada de miombo. Acompanha estados de conservação, terra agrícola, comunitário. Não substitui o verde de Saúde ou Agricultura: este é mais frio, mais cinza-savana.

```
--savanna-900: #1F3A1A
--savanna-800: #2E5226
--savanna-700: #3F6B33
--savanna-600: #527F44   (uso agrícola · conservação)
--savanna-500: #6B9658
--savanna-300: #B4D0A4
--savanna-100: #DDEDD2
--savanna-50:  #EEF6E8
```

### 2.3 Paper cream · canvas

Não é branco. Não é off-white frio. É o creme de papel cadastral — quase como o livro de registos predial em couro com folhas amareladas. É o canvas de fundo (`--bg`).

```
--cream-paper: #FAF4E8   (canvas body)
--cream-2:     #F2EAD8   (bg-2 · elevações)
--cream-3:     #E9DEC3   (linha cadastral · seca)
--paper:       #FFFFFF   (apenas para mapas e documentos)
```

### 2.4 Cadastral stripe (8px)

Equivalente do `hivis` em Trabalho ou em Transportes — mas aqui é uma **stripe cadastral**: traços pretos longos com pontos ocres a marcar vértices de demarcação. Aparece apenas em autos de demarcação e selos de confirmação cadastral, **nunca decorativa**. Sugere a fita métrica do topógrafo.

```css
.cadastro-stripe {
  background: repeating-linear-gradient(
    90deg,
    var(--line-ink) 0 14px,
    var(--terra-600) 14px 18px,
    var(--line-ink) 18px 32px,
    var(--cream-paper) 32px 36px
  );
}
```

---

## 3. Type system

| Família       | Uso                                                    |
| ------------- | ------------------------------------------------------ |
| **Plex Sans** | UI, navegação, formulários, KPIs                       |
| **Plex Mono** | Números DUAT, BI, NUIT, hectares, coordenadas, tempos  |
| **Plex Serif**| Títulos do DUAT-doc, autos de demarcação, sentenças     |

Hierarquia: `t-h1` 28px · `t-h2` 22px · `t-h3` 18px · `t-h4` 15px · `t-body` 14px · `t-meta` 12px · `t-overline` 10px maiúsculas tracking 0.08em.

---

## 4. Signature components (únicos do pacote)

### 4.1 DUAT card (hero)
Cartão hero do titular: gradient ocre→savana, número DUAT mono em destaque, hectares com tipografia mono escala 26px, mini-mapa cadastral SVG no canto inferior direito (renderiza o polígono em pequena escala). Linhas cadastrais subtis no fundo (45° + -45° hatching a 3% de alpha). Selo brass rotacionado -3° no canto superior direito.

### 4.2 DUAT serifado (documento autoritativo)
Equivalente da carta serifada de Transportes ou da sentença de Justiça. Plex Serif 13px linha 1.75. Header com gradient terra-900→terra-700 com selo. Background do body com pauta horizontal a 26px (sugere papel pautado).

### 4.3 Polígono GPS (vertex frame) — **assinatura única**
Não existe em nenhum outro pacote. Renderiza um polígono cadastral em SVG dentro de um frame com:
- Background com grid cadastral (linhas a 24px)
- Vértices numerados (V1, V2, V3...)
- Tabela de coordenadas em mono abaixo do polígono
- Footer com área calculada e perímetro

Permite duas variantes:
- **demarcação simples** — polígono ocre
- **sobreposição/conflito** — dois polígonos sobrepostos com hatching vermelho na intersecção

### 4.4 Conflito card
Background `--red-50`, border-left 3px `--red-500`. Mostra dois titulares competidores, área em conflito (em hectares + percentagem), polígonos sobrepostos como mini-SVG.

### 4.5 Comunidade card (régulo · consulta)
Componente único: foto/inicial do régulo + acta da consulta comunitária. Inclui blockquote serifado com declaração da comunidade. Marcado com cross-Justiça quando dispara mediação.

### 4.6 Hectare meter
Visual de área: grelha 8×N de quadrados pequenos, cada quadrado = 1 hectare (até 64ha) ou 10ha (acima). Cor varia por uso (ocre = residencial, verde = agrícola).

### 4.7 Categoria de uso (8 chips)
8 modos de uso da terra — equivalente dos 8 chips de transporte de Transportes, mas para uso fundiário:

| Chip          | Cor     | Uso                                                  |
| ------------- | ------- | ---------------------------------------------------- |
| residencial   | ocre    | habitação familiar, urbana ou rural                  |
| agrícola      | verde   | machamba, exploração agrícola comercial              |
| industrial    | charcoal| fábrica, armazém, parque industrial                  |
| turismo       | azul    | resort, lodge, ecoturismo                            |
| conservação   | verde-+ | área protegida, ANAC, parque nacional                |
| comunitário   | warn    | terra de uso comum, pasto comunitário, mata sagrada  |
| infraestrutura| ink-3   | estrada, linha férrea, porto, aeroporto              |
| misto         | violeta | zoneamento misto urbano                              |

### 4.8 DUAT status (4 estados oficiais)
Pílulas com cores semânticas:
- `vigente` (verde) — DUAT em vigor
- `pedido` (warn) — pedido em análise
- `conflito` (vermelho) — conflito por sobreposição/disputa
- `caducado` (cinza) — não renovado, devolvido ao Estado

---

## 5. Layout primitives

- **Phone frame** 360×720 com bezel preto · usado em Cidadão e Empresa
- **Tablet frame** 980×680 standard · usado em SPGC e Dashboard
- **Tablet rugged** variant · bezel terra-900 mais grosso, ondulação lateral · usado em Fiscal Campo (sugere Panasonic Toughbook)
- **Phone rugged** ainda não definido · não usado neste pacote

---

## 6. Cross-system interop (tier B+C)

Marca `.cross` aparece sempre visível em qualquer interacção que envolva um pacote irmão. Nunca escondida. Quatro variantes: neutra, `ok` (verde), `warn` (amber), `savanna`.

| Interacção                                | Cross com…                          |
| ----------------------------------------- | ----------------------------------- |
| Validação de identidade do titular        | `cross-eBI`                         |
| Validação NUEL/NUIT da empresa            | `cross-NUEL` · `cross-NUIT`         |
| Pagamento de taxa anual DUAT              | `cross-AT` (Finanças)               |
| Conflito → mediação comunitária → tribunal| `cross-TJ` (Justiça)                |
| Trabalhadores em obra na exploração       | `cross-NUSS` (Trabalho · INSS)      |
| DUAT em zona protegida ANAC               | `cross-ANAC`                        |
| Investimento estrangeiro >USD 500k        | `cross-CPI` · `cross-IGEPE`         |

---

## 7. Personas convencionadas (para o pacote)

| Pessoa / entidade                         | Papel                              |
| ----------------------------------------- | ---------------------------------- |
| Felisberto Manjate                        | Cidadão titular DUAT residencial Inhambane |
| Eng. P. Cossa                             | Director Geral DINAGECA            |
| Eng. F. Macuácua                          | Chefe SPGC Manica                  |
| Júlia Sumane Tembe                        | Fiscal de campo Sofala (cédula 2418) |
| Régulo Mahique de Cheringoma              | Autoridade tradicional Sofala      |
| Frota Sumbane Lda                         | Empresa logística (já existe na família)|
| Vale Moçambique                           | Investidor mineiro real (Moatize)  |
| Greenfield Forestry SA (fictícia)         | Investidor florestal Manica        |

DUATs convencionados: formato `DUAT-YYYY-PROV-NNNNNN` (ex.: `DUAT-2018-MN-014218`).

---

## 8. Princípios não negociáveis

1. **Terra é do Estado.** Nenhum DUAT é "propriedade". A linguagem da app reflecte isto sempre: nunca "vender", sempre "transmitir DUAT" ou "ceder direitos de uso".
2. **Consulta comunitária é obrigatória** para empresa. Sem acta, sem DUAT. A app obriga ao upload da acta e à validação por régulo via SMS antes de finalizar.
3. **Sobreposição = conflito automático.** O sistema nunca emite DUAT sobre polígono já demarcado. Detecta no momento do pedido e dispara fluxo de conflito.
4. **Mediação antes de Tribunal.** Cross-Justiça abre Tribunal Comunitário primeiro; só escalar para Tribunal Administrativo se mediação falhar (90 dias).
5. **Boa fé histórica.** Ocupação de boa fé há mais de 10 anos por cidadão moçambicano gera direito de DUAT mesmo sem pedido formal — Lei 19/97 art. 12. A app reconhece e trata isto.

---

## 9. Linguagem & línguas

- PT-MZ é a língua institucional padrão.
- Citizen-facing: PT-MZ + **Macua** + **Changana** + **Sena** + **Nyungwe** (5 toggles).
- USSD `*146#` para fallback low-tech onde só há feature phones.
- Nunca usar termos legalistas em UI cidadã. "DUAT" é mantido (é constitucional), mas "alvará de demarcação" vira "demarcação aprovada".

---

## 10. Versão & changelog

- **v0.3 · Abril 2026** — Foundation publicada. Paleta ocre+savana confirmada. Polígono GPS como signature. Cross-Justiça via Tribunal Comunitário antes de TJ Adm.
