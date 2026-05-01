<div align="center">
  <img src="assets/mark-bg.svg" width="120" alt="Conceitos · sol nascente sobre horizonte">
  <h1>Conceitos</h1>
  <p>Imaginando um futuro digital para Moçambique.</p>
  <a href="https://conceitos.org">conceitos.org</a>
</div>

---

**Conceitos** é uma iniciativa cívica que reimagina serviços públicos digitais moçambicanos através de mocks e protótipos visuais. Cada projecto é um conjunto de interfaces clicáveis: ideias para conversar, criticar e melhorar, não software em produção.

Os projectos dividem-se em **Públicos** (serviços públicos reimaginados - saúde, educação, justiça, etc.) e **Produtos** (ferramentas independentes para o quotidiano de moçambicanos - agricultura, finanças pessoais, etc.). Os dois tipos partilham princípios de design e a mesma casa neste repositório, mas distinguem-se em propósito, vocabulário e leitor implícito.

Este repositório contém o código-fonte do site [conceitos.org](https://conceitos.org), servido via GitHub Pages.

## Projectos

### Públicos · serviços públicos reimaginados

| # | Projecto |
|---|----------|
| 01 | [Saúde Digital](projectos/publicos/saudedigital/) |
| 02 | [Governo Digital](projectos/publicos/governodigital/) |
| 03 | [Educação Digital](projectos/publicos/educacaodigital/) |
| 04 | [Finanças Digitais](projectos/publicos/financasdigitais/) |
| 05 | [Justiça Digital](projectos/publicos/justicadigital/) |
| 06 | [Trabalho Digital](projectos/publicos/trabalhodigital/) |
| 07 | [Transportes Digitais](projectos/publicos/transportesdigitais/) |
| 08 | [Terras Digitais](projectos/publicos/terrasdigitais/) |
| 09 | [Sociedade Aberta](projectos/publicos/sociedadeaberta/) |
| 10 | [Vida Civil](projectos/publicos/vidacivil/) |
| 11 | [Resiliência Climática](projectos/publicos/resilienciaclimatica/) |
| 12 | [Eleições Digitais](projectos/publicos/eleicoesdigitais/) |
| 13 | [Senda](projectos/publicos/senda/) |

### Produtos · ferramentas para o quotidiano

| # | Projecto |
|---|----------|
| P01 | [Lavoura](projectos/produtos/lavoura/) |
| P02 | [KuVona](projectos/produtos/kuvona/) |
| P03 | [Comunidade](projectos/produtos/comunidade/) |

## Estrutura

```
conceitos/
├── index.html
├── assets/
└── projectos/
    ├── index.html
    ├── publicos/
    │   ├── saudedigital/        # 01 · Saúde Digital
    │   ├── governodigital/      # 02 · Governo Digital
    │   ├── educacaodigital/     # 03 · Educação Digital
    │   ├── financasdigitais/    # 04 · Finanças Digitais
    │   ├── justicadigital/      # 05 · Justiça Digital
    │   ├── trabalhodigital/     # 06 · Trabalho Digital
    │   ├── transportesdigitais/ # 07 · Transportes Digitais
    │   ├── terrasdigitais/      # 08 · Terras Digitais
    │   ├── sociedadeaberta/     # 09 · Sociedade Aberta
    │   ├── vidacivil/           # 10 · Vida Civil
    │   ├── resilienciaclimatica/ # 11 · Resiliência Climática
    │   ├── eleicoesdigitais/    # 12 · Eleições Digitais
    │   └── senda/               # 13 · Senda
    └── produtos/
        ├── lavoura/             # P01 · Lavoura
        ├── kuvona/              # P02 · KuVona
        └── comunidade/          # P03 · Comunidade
```

Cada pasta de projecto contém: `index.html`, superfícies (`*.html`), `design-system.html`, `shared/styles.css` e ficheiros `DESIGN-*.md` com as decisões de design.

## Tecnologia

Site estático puro: HTML5, CSS3 com variáveis de design, SVG e JavaScript mínimo. Sem frameworks, sem bundlers, sem dependências de runtime.

## Aviso

Estes protótipos são conceitos visuais independentes, sem afiliação a qualquer entidade governamental, organização ou empresa. São exercícios de imaginação cívica partilhados em domínio público. Nenhum dado apresentado é real.

## Colaborar

Colaborações são bem-vindas: crítica de design, novas ideias de projectos, correcções ou melhorias de acessibilidade. Abre uma issue ou um pull request.

---

Publicado sob [CC BY 4.0](LICENSE) - podes usar, adaptar e distribuir com atribuição ao autor.
