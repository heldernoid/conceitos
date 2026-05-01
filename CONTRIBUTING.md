# Colaborar no Conceitos

Obrigado pelo interesse. Conceitos é um projecto aberto de imaginação cívica: qualquer pessoa pode criticar, melhorar ou propor.

## O que é este projecto

Cada entrada no Conceitos é um conjunto de **mocks HTML clicáveis** acompanhado de **documentação de design** (`DESIGN-*.md`). Não é software em produção - é uma proposta visual para conversa com cidadãos, técnicos e decisores.

Os projectos dividem-se em duas famílias:

- **Públicos** - serviços públicos reimaginados (saúde, educação, justiça, identidade). Contexto institucional, vocabulário de Estado, cidadão em relação ao serviço público.
- **Produtos** - ferramentas independentes para o quotidiano de moçambicanos (agricultura, finanças pessoais, etc.). Contexto consumer, vocabulário do dia-a-dia, pessoa em relação à sua própria vida.

A estrutura de cada projecto segue este padrão:

```
nome-do-projecto/
├── index.html          # Visão geral e navegação
├── superficie.html     # Uma superfície de produto por ficheiro
├── design-system.html  # Tokens, componentes, tipografia
├── shared/styles.css   # CSS partilhado do projecto
└── DESIGN-*.md         # Documento autoritativo por superfície
```

## Formas de colaborar

### Crítica de design

A forma mais valiosa de colaboração. Se algo não funciona, não reflecte a realidade moçambicana, ou podia ser mais simples: abre uma issue com o contexto. Não é preciso saber programar.

### Correcções e melhorias nos mocks

Para corrigir um fluxo, um texto, um estado de interface ou um problema de acessibilidade:

1. Faz fork do repositório
2. Edita o ficheiro HTML ou CSS relevante
3. Abre um pull request com uma descrição clara do que mudaste e porquê

Mantém o estilo existente: sem frameworks, sem bundlers, HTML e CSS directos. Os mocks usam IBM Plex Sans e IBM Plex Mono via Google Fonts.

### Actualizar documentação de design

Cada superfície tem um `DESIGN-*.md` que descreve princípios, fluxos, componentes, estados e questões em aberto. Se vires algo desactualizado ou incompleto, podes editar directamente e abrir um PR.

### Propor um conceito novo

Podes propor tanto um serviço público como um produto consumer. Abre uma issue com:

- O serviço ou problema em concreto
- A família (Público ou Produto) e porquê
- Quem usa (cidadão, funcionário, agricultor, comerciante...)
- O que hoje não funciona bem
- Referências se tiveres (legislação, relatórios, exemplos de outros países)

Não é preciso ter o mock pronto. A ideia já é suficiente para começar.

## Princípios partilhados

Aplicam-se a Públicos e Produtos:

- **Contexto moçambicano em primeiro lugar.** Dispositivos de entrada no mercado, conectividade limitada, múltiplos idiomas, realidades rurais e urbanas.
- **Contenção visual.** Sem decoração desnecessária. Hierarquia clara, contraste suficiente, alvos de toque de 44 px mínimo.
- **Dados sempre fictícios.** Nomes, números, processos e conteúdos são ilustrativos. Nunca usar dados reais.
- **Sem afiliação oficial.** Estes mocks não representam nenhuma entidade governamental ou empresa. O aviso de independência deve manter-se em todos os projectos.
- **Sem dependências de runtime.** HTML e CSS directos. Sem frameworks JS, sem bibliotecas CSS externas.

## Princípios específicos de Produtos

- **Tom mais próximo.** Narrativa centrada em pessoa singular (ex: Sara, não "o cidadão"). Linguagem do quotidiano, não vocabulário institucional.
- **Paletas mais variadas.** Maior liberdade visual do que nos Públicos, mas sempre com contenção e propósito.
- **Voz e áudio como princípio.** Em produtos para contextos de baixa literacia ou uso em campo, pensar em voz não como feature mas como camada de design desde o início.
- **Mais ilustração, menos institucional.** Pode usar mais imagem e narrativa visual; menos tabelas e formulários densos.

## O que não aceitamos

- Dados pessoais reais em qualquer ficheiro
- Referências a entidades reais de forma que possa ser confundida com posição oficial
- Dependências de runtime (frameworks JS, bibliotecas CSS externas)
- Alterações ao estilo visual sem discussão prévia em issue

## Dúvidas

Abre uma issue. É o melhor sítio para conversar antes de começar a trabalhar.
