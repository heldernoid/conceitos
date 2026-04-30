<div align="center">
  <img src="assets/mark-bg.svg" width="120" alt="Conceitos · sol nascente sobre horizonte">
  <h1>Conceitos</h1>
  <p>Imaginando um futuro digital para Moçambique.</p>
  <a href="https://conceitos.org">conceitos.org</a>
</div>

---

**Conceitos** é uma iniciativa cívica que reimagina serviços públicos digitais moçambicanos através de mocks e protótipos visuais. Cada projecto é um conjunto de interfaces clicáveis: ideias para conversar, criticar e melhorar, não software em produção.

Este repositório contém o código-fonte do site [conceitos.org](https://conceitos.org), servido via GitHub Pages.

## Projectos

| # | Projecto | Estado |
|---|----------|--------|
| 01 | [Saúde Digital](https://conceitos.org/projectos/saudedigital/) | Disponível |
| 02 | [Governo Digital](https://conceitos.org/projectos/governodigital/) | Disponível |
| 03 | [Educação Digital](https://conceitos.org/projectos/educacaodigital/) | Disponível |
| 04 | [Finanças Digitais](https://conceitos.org/projectos/financasdigitais/) | Disponível |
| 05 | [Justiça Digital](https://conceitos.org/projectos/justicadigital/) | Disponível |
| 06 | [Trabalho Digital](https://conceitos.org/projectos/trabalhodigital/) | Disponível |
| 07 | [Transportes Digitais](https://conceitos.org/projectos/transportesdigitais/) | Disponível |
| 08 | [Terras Digitais](https://conceitos.org/projectos/terrasdigitais/) | Disponível |
| 09 | [Sociedade Aberta](https://conceitos.org/projectos/sociedadeaberta/) | Disponível |
| 10 | [Vida Civil](https://conceitos.org/projectos/vidacivil/) | Disponível |
| 11 | [Resiliência Climática](https://conceitos.org/projectos/resilienciaclimatica/) | Disponível |

### Saúde Digital

Reimaginação da plataforma nacional de saúde com cinco superfícies interligadas: registo clínico electrónico (EMR), app do cidadão, farmácia comunitária, vigilância epidemiológica e auditoria clínica.

### Governo Digital

Reimaginação dos serviços de governação civil e transparência do Estado com cinco superfícies: bilhete de identidade electrónico (eBI), app do cidadão, balcão de atendimento digitalizado, orçamento aberto e auditoria pública.

### Educação Digital

Reimaginação da plataforma nacional de educação com cinco superfícies: gestão escolar integrada (SIGE), portal do professor, caderno electrónico do aluno, biblioteca pública nacional e portal de matrículas.

### Finanças Digitais

Reimaginação do sistema fiscal e orçamental com cinco superfícies: portal do cidadão (NUIT e IRS pessoal), declaração comercial (IRPC), eFactura para independentes e comerciantes, portal da Autoridade Tributária e interoperabilidade com a SISTAFE.

### Justiça Digital

Reimaginação do acesso à justiça com cinco superfícies: portal do cidadão (acompanhamento processual e certidões), tribunal comunitário digitalizado, cadastro predial, portal do MJCR e registos públicos (civil, comercial e predial).

### Trabalho Digital

Reimaginação do sistema de trabalho e protecção social com cinco superfícies: portal do trabalhador, portal do empregador, INSS (segurança social), IGT (inspecção do trabalho) e INEFP (formação profissional).

### Transportes Digitais

Reimaginação do sistema nacional de transportes com cinco superfícies: portal do condutor, portal do operador, INATTER (inspecção e licenciamento), transporte multimodal e PRM (passagem de fronteira).

### Terras Digitais

Reimaginação do sistema de gestão fundiária com cinco superfícies: portal do cidadão, portal da empresa, SPGC (cadastro e gestão), fiscalização e dashboard nacional.

### Sociedade Aberta

Reimaginação do acesso à informação pública com cinco superfícies: portal do cidadão, portal da empresa, ferramentas para jornalistas, plataforma pública de dados abertos e portal do titular de dados.

### Vida Civil

Reimaginação do registo civil com seis superfícies: portal do cidadão, conservatória, família, hospital, sucessão e gestão de dados sensíveis.

### Resiliência Climática

Reimaginação da resposta a desastres naturais com oito superfícies: portal do cidadão, painel de gestão, ajuda humanitária, reconstrução, voluntariado, terreno, memorial e coordenação de campo.

## Estrutura

```
conceitos/
├── index.html        # Página de entrada e directório de projectos
├── assets/           # Marca e SVGs partilhados
└── projectos/
    ├── saudedigital/        # 01 · Saúde Digital
    ├── governodigital/      # 02 · Governo Digital
    ├── educacaodigital/     # 03 · Educação Digital
    ├── financasdigitais/    # 04 · Finanças Digitais
    ├── justicadigital/      # 05 · Justiça Digital
    ├── trabalhodigital/     # 06 · Trabalho Digital
    ├── transportesdigitais/ # 07 · Transportes Digitais
    ├── terrasdigitais/      # 08 · Terras Digitais
    ├── sociedadeaberta/     # 09 · Sociedade Aberta
    ├── vidacivil/           # 10 · Vida Civil
    └── resilienciaclimatica/ # 11 · Resiliência Climática
```

Cada pasta de projecto contém: `index.html`, superfícies (`*.html`), `design-system.html`, `shared/styles.css` e ficheiros `DESIGN-*.md` com as decisões de design.

## Tecnologia

Site estático puro: HTML5, CSS3 com variáveis de design, SVG e JavaScript mínimo. Sem frameworks, sem bundlers, sem dependências de runtime.

## Aviso

Estes protótipos são conceitos visuais independentes, sem afiliação a qualquer entidade governamental, organização ou empresa. São exercícios de imaginação cívica partilhados em domínio público. Nenhum dado apresentado é real.

## Colaborar

Contribuições são bem-vindas: crítica de design, novas ideias de projectos, correcções ou melhorias de acessibilidade. Abre uma issue ou um pull request.

---

Publicado sob [CC BY 4.0](LICENSE) - podes usar, adaptar e distribuir com atribuição ao autor.
