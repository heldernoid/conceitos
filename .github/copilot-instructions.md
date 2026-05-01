# Conceitos · GitHub Copilot Instructions

Conceitos é uma biblioteca de protótipos HTML/CSS que reimagina serviços públicos
digitais e produtos consumer para Moçambique. São artefactos de design, não software
em produção. Site: https://conceitos.org · CC BY 4.0

Ver `AGENTS.md` na raiz para contexto completo.

## Estrutura

- `projectos/publicos/` — 13 serviços públicos reimaginados (saúde, educação, etc.)
- `projectos/produtos/` — 3 produtos consumer (Lavoura, KuVona, Comunidade)
- Cada projecto tem: `DESIGN-*.md` (decisões por superfície), `design-system.html`, `shared/styles.css`
- Produtos (Lavoura, KuVona, Comunidade) também têm `PRINCIPIOS.md` (princípios + personas)

## Convenções a respeitar

- Stack: HTML5 estático puro · CSS3 · SVG inline · JS mínimo · sem frameworks
- SVG sempre inline — ficheiros auto-contidos
- `shared/` contém apenas `styles.css`
- Língua: Português europeu com marcadores moçambicanos
- Sem gamification por design — não sugerir leaderboards, badges ou rankings

## Para construir produto real

1. Remove o snippet Google Analytics (`G-P01B93QSYD`) de cada `<head>`
2. Nos produtos, lê `PRINCIPIOS.md` para personas e restrições deliberadas
3. Lê `DESIGN-*.md` para decisões de design por superfície
4. Atribuição: Baseado em Conceitos por Hélder Monteiro - https://conceitos.org (CC BY 4.0)
