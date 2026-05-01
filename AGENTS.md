# Conceitos · Agent Context

Conceitos é uma iniciativa cívica de design — uma biblioteca de protótipos HTML/CSS
interactivos que reimaginam serviços públicos digitais e produtos consumer para
Moçambique. São artefactos de design, não software em produção.

Site: https://conceitos.org · Autor: Hélder Monteiro · Licença: CC BY 4.0

## Dois casos de uso para agentes

1. **Explorar e compreender** — navegar o repositório, entender decisões de design,
   responder a perguntas sobre os projectos
2. **Construir produtos reais** — usar os protótipos como base para criar
   especificações técnicas e implementar MVPs

---

## Estrutura do repositório

```
conceitos/
├── index.html                      # Landing page com todos os projectos
├── projectos/
│   ├── publicos/                   # 13 serviços públicos reimaginados
│   │   ├── saudedigital/           # 01 · Saúde Digital
│   │   ├── governodigital/         # 02 · Governo Digital
│   │   ├── educacaodigital/        # 03 · Educação Digital
│   │   ├── financasdigitais/       # 04 · Finanças Digitais
│   │   ├── justicadigital/         # 05 · Justiça Digital
│   │   ├── trabalhodigital/        # 06 · Trabalho Digital
│   │   ├── transportesdigitais/    # 07 · Transportes Digitais
│   │   ├── terrasdigitais/         # 08 · Terras Digitais
│   │   ├── sociedadeaberta/        # 09 · Sociedade Aberta
│   │   ├── vidacivil/              # 10 · Vida Civil
│   │   ├── resilienciaclimatica/   # 11 · Resiliência Climática
│   │   ├── eleicoesdigitais/       # 12 · Eleições Digitais
│   │   └── senda/                  # 13 · Senda (equivalências académicas)
│   └── produtos/                   # 3 produtos consumer
│       ├── lavoura/                # P01 · assistente agrícola digital
│       ├── kuvona/                 # P02 · jornalismo e transparência cívica
│       └── comunidade/             # P03 · doações e transparência comunitária
```

## Estrutura de cada projecto

Cada projecto segue sempre este padrão de ficheiros:

| Ficheiro | Conteúdo |
|----------|----------|
| `index.html` | Landing com hero, 8 princípios fundadores, navegação para superfícies |
| `design-system.html` | Paleta, tipografia, componentes signature |
| `*.html` (5-9 ficheiros) | Superfícies: portais, fluxos, painéis, ferramentas |
| `PRINCIPIOS.md` | Documento fundador: 8 princípios + personas + operador fictício (presente nos Produtos) |
| `DESIGN-*.md` | Decisões de design por superfície + "o que deliberadamente NÃO está aqui" |
| `shared/styles.css` | ~1000 linhas · tokens CSS + componentes (único ficheiro em shared/) |

---

## Para construir produtos reais a partir destes protótipos

### 1. Ler antes de codificar

- `PRINCIPIOS.md` — princípios de design, personas, e restrições deliberadas (presente nos Produtos)
- `DESIGN-*.md` — cada decisão por superfície, incluindo o que foi conscientemente excluído
- `design-system.html` — tokens visuais, componentes, tipografia

### 2. Remover rastreamento

Remove o snippet do Google Analytics (`G-P01B93QSYD`) do `<head>` de cada ficheiro
HTML — serve apenas para medir visitas no conceitos.org, não tem utilidade noutro contexto.

### 3. Criar especificação técnica

Ao gerar specs ou arquitectura a partir destes protótipos:

- Nos produtos (Lavoura, KuVona, Comunidade), lê `PRINCIPIOS.md` para personas e restrições deliberadas
- Mantém os princípios fundadores — cada um existe por razão específica
- Respeita o que está deliberadamente ausente (ver secção abaixo)

---

## Princípios recorrentes de design

Estes princípios aparecem em todos os projectos com variações:

1. Dignidade do utilizador como primeira camada de design
2. Verificação séria com níveis adequados ao risco
3. Privacidade como restrição de sistema, não feature opcional
4. Sem competição entre actores no mesmo ecossistema
5. Transparência operacional pública por defeito
6. Estado e autoridades como parceiros — nunca substituídos
7. Auditoria por terceiros possível
8. Foco nacional — diáspora geralmente excluída do scope

**O que está deliberadamente ausente em todos os projectos:**
- Gamification — sem leaderboards, badges, rankings, pontos
- Anti-saviorism — os utilizadores são agentes, não beneficiários passivos
- Fotos de pessoas vulneráveis
- Acção política ou advocacy — informação e cooperação, não confronto

---

## Convenções de voz e linguagem

- **Língua**: Português europeu com marcadores moçambicanos: "óptimo", "facto", "actual", "sub-servido"
- **Tom**: Directo e sóbrio — sem "incrível", "transformador", "revolucionário"
- **Autoridades**: Tom institucional respeitoso — cooperação, não confronto
- **Separador `·`**: Usado entre elementos curtos em vez de vírgulas em listas de chips e tags

---

## Personas dos Produtos

- **Lavoura (P01)**: Sara Macuácua — agricultora
- **KuVona (P02)**: Cândida Sitoe + Beatriz Macuácua — jornalistas cidadãs
- **Comunidade (P03)**: Mãe Eulália Sitoe + Rui Manjate + Tia Ercília Bila

Nomes moçambicanos plausíveis, não clichê. "KuVona" = "ku vona" em changana
(língua do sul de Moçambique) = "ver" em português.

---

## Stack técnico

- HTML5 estático puro · CSS3 com variáveis de design · SVG inline · JS mínimo
- Sem frameworks · sem bundlers · sem dependências de runtime
- SVG sempre inline — ficheiros auto-contidos, funcionam offline
- `shared/` contém apenas `styles.css` — sem outros assets partilhados

---

## Atribuição

CC BY 4.0 — usar, adaptar e distribuir com atribuição:

> Baseado em Conceitos por Hélder Monteiro - https://conceitos.org (CC BY 4.0)
