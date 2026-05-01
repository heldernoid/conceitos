# Conceitos · Claude Code Context

Conceitos é uma iniciativa cívica de design — uma biblioteca de protótipos HTML/CSS
interactivos que reimaginam serviços públicos digitais e produtos consumer para
Moçambique. São artefactos de design, não software em produção.

Site: https://conceitos.org · Autor: Hélder Monteiro · Licença: CC BY 4.0

Ver `AGENTS.md` para contexto completo do repositório.

---

## Como trabalhar neste repositório

### Explorar um projecto

1. Lê o `PRINCIPIOS.md` do projecto — princípios fundadores, personas, operador fictício
2. Lê os `DESIGN-*.md` — decisões por superfície e o que foi deliberadamente excluído
3. Abre o `design-system.html` para entender tokens visuais e componentes
4. O `shared/styles.css` tem ~1000 linhas com todos os tokens CSS

### Construir produto real a partir de um protótipo

1. Remove o snippet GA (`G-P01B93QSYD`) do `<head>` de cada HTML
2. Usa `DESIGN-*.md` para cada superfície como PRD por ecrã
3. Nos produtos (Lavoura, KuVona, Comunidade), lê `PRINCIPIOS.md` para personas e restrições
4. Mantém as restrições deliberadas: sem gamification, privacidade como restrição de sistema

### Stack

HTML5 estático puro · CSS3 com variáveis · SVG inline · JS mínimo
Sem frameworks · sem bundlers · sem runtime

### Convenções

- Português europeu com marcadores moçambicanos
- SVG sempre inline — nunca em ficheiros separados em `shared/`
- `shared/` contém apenas `styles.css`
- Personas com nomes moçambicanos plausíveis

### O que não alterar sem contexto

- As restrições de design (sem gamification, sem badges, sem rankings)
- O tom institucional respeitoso em relação a autoridades moçambicanas
- Os operadores fictícios marcados explicitamente como tal nos rodapés
