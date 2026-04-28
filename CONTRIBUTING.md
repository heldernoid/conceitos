# Contribuir para o Conceitos

Obrigado pelo interesse. Conceitos é um projecto aberto de imaginação cívica: qualquer pessoa pode criticar, melhorar ou propor.

## O que é este projecto

Cada entrada no Conceitos é um conjunto de **mocks HTML clicáveis** acompanhado de **documentação de desenho** (`DESIGN-*.md`). Não é software em produção — é uma proposta visual para conversa com cidadãos, técnicos e decisores.

A estrutura de cada projecto segue este padrão:

```
nome-do-projecto/
├── index.html          # Visão geral e navegação
├── superficie.html     # Uma superfície de produto por ficheiro
├── design-system.html  # Tokens, componentes, tipografia
├── shared/styles.css   # CSS partilhado do projecto
└── DESIGN-*.md         # Documento autoritativo por superfície
```

## Formas de contribuir

### Crítica de desenho

A forma mais valiosa de contribuição. Se algo não funciona, não reflecte a realidade moçambicana, ou podia ser mais simples: abre uma issue com o contexto. Não é preciso saber programar.

### Correcções e melhorias nos mocks

Para corrigir um fluxo, um texto, um estado de interface ou um problema de acessibilidade:

1. Faz fork do repositório
2. Edita o ficheiro HTML ou CSS relevante
3. Abre um pull request com uma descrição clara do que mudaste e porquê

Mantém o estilo existente: sem frameworks, sem bundlers, HTML e CSS directos. Os mocks usam IBM Plex Sans e IBM Plex Mono via Google Fonts.

### Actualizar documentação de desenho

Cada superfície tem um `DESIGN-*.md` que descreve princípios, fluxos, componentes, estados e questões em aberto. Se vires algo desactualizado ou incompleto, podes editar directamente e abrir um PR.

### Propor um conceito novo

Se há um serviço público que devia existir ou ser repensado, abre uma issue com:

- O serviço ou problema em concreto
- Quem usa (cidadão, funcionário, instituição)
- O que hoje não funciona bem
- Referências se tiveres (legislação, relatórios, exemplos de outros países)

Não é preciso ter o mock pronto. A ideia já é suficiente para começar.

## Princípios a seguir

Os projectos existentes seguem alguns princípios que vale a pena manter:

- **Contexto moçambicano em primeiro lugar.** Infraestrutura pública, não produto de consumo. Dispositivos de entrada no mercado, conectividade limitada, múltiplos idiomas.
- **Contenção visual.** Sem decoração desnecessária. Hierarquia clara, contraste suficiente, alvos de toque de 44 px mínimo.
- **Dados sempre fictícios.** Nomes, números, processos e conteúdos clínicos ou jurídicos são ilustrativos. Nunca usar dados reais.
- **Sem afiliação oficial.** Estes mocks não representam nenhuma entidade governamental. O aviso de independência deve manter-se em todos os projectos.

## O que não aceitamos

- Dados pessoais reais em qualquer ficheiro
- Referências a entidades reais de forma que possa ser confundida com posição oficial
- Dependências de runtime (frameworks JS, bibliotecas CSS externas)
- Alterações ao estilo visual sem discussão prévia em issue

## Dúvidas

Abre uma issue. É o melhor sítio para conversar antes de começar a trabalhar.
