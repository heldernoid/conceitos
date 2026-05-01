# Conceitos · Codeium Context

Conceitos é uma biblioteca de protótipos HTML/CSS que reimagina serviços públicos
digitais e produtos consumer para Moçambique. São artefactos de design, não software
em produção. Site: https://conceitos.org · CC BY 4.0

Ver `AGENTS.md` na raiz para contexto completo.

## Estrutura rápida

- `projectos/publicos/` — 13 serviços públicos reimaginados
- `projectos/produtos/` — 3 produtos (Lavoura, KuVona, Comunidade)
- `PRINCIPIOS.md` em cada projecto — princípios fundadores e personas
- `DESIGN-*.md` em cada projecto — decisões de design por superfície

## Stack

HTML5 estático puro · CSS3 com variáveis · SVG inline · sem frameworks · sem runtime

## Regras

- SVG sempre inline, nunca em ficheiros separados
- `shared/` contém apenas `styles.css`
- Português europeu com marcadores moçambicanos
- Sem gamification — é deliberado, não omissão
- Remover GA tag (`G-P01B93QSYD`) ao reutilizar para produto próprio
