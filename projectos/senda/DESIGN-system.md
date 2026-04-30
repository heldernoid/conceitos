# DESIGN-system.md — Sistema de design SENDA

**Status:** v0.5 · Abril 2026
**Domínio:** Sistema Electrónico Nacional de Dados Académicos
**Total:** 7 superfícies · 49 cenas · 14 cross-systems · 7 componentes signature

---

## 1. Princípio de design

SENDA é uma **infraestrutura nacional de dados académicos** · não uma app. É como uma rede eléctrica · invisível quando funciona · indispensável quando falha. O design reflecte esta natureza institucional: paleta sóbria · tipografia neutra · sem ornamento · com peso de Estado.

A linguagem visual deve dizer simultaneamente:
- **Confiança institucional** · cidadão acredita
- **Permanência** · 50+ anos · cradle-to-credential
- **Acessibilidade** · funciona em 4G · em smartphone barato · sem fricção
- **Auditabilidade** · cada decisão visível · cada cálculo exposto

---

## 2. Paleta · azul institucional académico

### Azul SENDA · primário
- `--blue-950 #0d2845` · headers escuros · noir de cerimónia
- `--blue-900 #123860` · deep · banner de hero · footer
- `--blue-800 #153f6e` · hover de botões primários
- `--blue-700 #1a4f8a` · **PRIMARY · marca SENDA**
- `--blue-500 #2d68a3` · variação · grupo B exames
- `--accent  #0ea5e9` · azul-céu · destaques pontuais · números grandes

### Hitos académicos · cores semânticas
- `--hito-primario   #16a34a` · verde · 1.ª-7.ª classe
- `--hito-secundario #1a4f8a` · azul · 8.ª-12.ª classe
- `--hito-superior   #b68813` · dourado · licenciatura+
- `--hito-continua   #6b7280` · cinza · pós-formação · pausas

### 4 grupos de exame
- `--grupo-a #dc2626` · vermelho · Letras / Humanidades
- `--grupo-b #2d68a3` · azul · Sociais / Económicas
- `--grupo-c #16a34a` · verde · Engenharias / Tecnologia
- `--grupo-d #b68813` · dourado · Saúde / Biológicas

A barra de 4px no topo (`.senda-stripe`) mostra os 4 grupos lado a lado · marca identitária do sistema.

---

## 3. Tipografia · 3 famílias

| Família | Uso |
|---|---|
| **Inter** | UI · botões · tabelas · formulários · 99% dos textos |
| **JetBrains Mono** | NUEL académico · DOC ID · hashes · números financeiros |
| **Lora** | Diploma fac-símile · pull-quotes solenes · serif cerimonial |

Inter para tudo o que é interface. Mono para o que precisa de precisão de identificador (NUEL, DOC ID). Serif só para o diploma e momentos de prosa solene.

---

## 4. Os 7 componentes signature

| # | Componente | Onde aparece principal |
|---|---|---|
| 1 | `.trajectoria-cradle` · linha do tempo escolar | Surface 2 (Pedro) · Surface 7 (Felisberto) · Sistema |
| 2 | `.programa-card` · cartão de curso | Surface 3 · Sistema |
| 3 | `.preferencias-stack` · 8 preferências ordenáveis | Surface 3 · Sistema |
| 4 | `.score-calculator` · cálculo transparente | Surface 4 · Sistema |
| 5 | `.ranking-public` · tabela ranking anonimizada | Surface 4 · Sistema |
| 6 | `.diploma-fac-simile` · réplica fiel do físico | Surface 5 · Sistema |
| 7 | `.verificacao-publica` · 3 estados | Surface 6 · Sistema |

Cada signature foi pensado para ser auto-explicativo · decompõe-se em outros componentes utilitários (badge, card, table) · funciona em isolamento mas ganha sentido no contexto narrativo.

---

## 5. Layout patterns

### Scenes · 7 cenas por superfície
Cada superfície tem 7 cenas. Cada cena tem:
- `<section class="scene">` · padding 36px
- `.scene-h` com número e label
- `.scene-c` com conteúdo · max-width 1280px

Variantes: `.alt` (fundo cinza-50) · `.dark` (fundo blue-950 · texto branco). Alternância entre elas dá ritmo de leitura.

### Phone / Tablet / Desktop frames
- `.phone` · 360px · simula smartphone (cidadão · enc. educação)
- `.desktop-frame` · simula browser (operador institucional · admin)
- Os 3 dots Mac (r/y/g) e URL bar dão contexto de onde a UI vive

### Grid · g-2, g-3, g-4
Sistema simples de grids para colunas. `.grid.g-2` é 2 colunas iguais. Para layouts assimétricos · usar `style="grid-template-columns:..."`.

---

## 6. Voz e tom

- **Português europeu de Moçambique** (cróspito, valido, registar não regista, candidatar não candidatar-se em primeira)
- **Sem jargão técnico desnecessário** · "diploma válido" não "credencial autenticada"
- **Sem entusiasmo gratuito** · não "Boa! Está dentro!" · sim "Está colocado em..."
- **Pull quotes longas e narrativas** · não one-liners · personas falam como pessoas reais
- **Stats sempre com contexto** · "184 K verificações" → "ou 19 dias úteis poupados"

---

## 7. Edge cases · sempre presentes

Cada superfície tem pelo menos 1 cena dedicada a edge cases:
- Trajectória · 6 cenários não-lineares (gravidez, doença, mudança área, interrupção, diáspora, refugiado)
- Candidatura · não-colocados (Cena 5 de Resultados)
- Equivalências · 3 casos paradigmáticos (diáspora · imigrante · refugiado)

Princípio: **se o caso normal é o protagonista · os casos limite são a prova de cobertura**.

---

## 8. O que NÃO usar

- **Não usar emojis decorativos no UI** · só ícones SVG simples ou sem ícone
- **Não usar gradientes coloridos** · gradientes apenas em variantes hero (blue-700 → blue-900)
- **Não usar serif fora do diploma e pull quotes** · Inter cobre 99%
- **Não usar referências numeradas a uma colecção externa** · SENDA é independente · personas e cross-systems referem-se por nome próprio
- **Não usar apelos comerciais** · "Cadastre-se já!" · "Não perca!" · zero · isto é serviço público

---

## 9. Continuidade narrativa

SENDA herda personas de outras superfícies da mesma autoria · sem nomeá-las como referências numeradas:

- **Felisberto Manjate** · pai · trajectória 1985-2035 cumulativa
- **Joana Sumane Manjate** · mãe · enfermeira · ESCMC
- **Pedro Manjate Sumane** · filho · 17 anos · 12.ª classe · 1.º voto cross-Eleições Digitais 2029
- **Joana Cossa Sumane** · diáspora portuguesa · regressa enfermeira (NÃO confundir com Joana Sumane Manjate · mãe)
- **Ana Cristina Tembe** · diplomada UEM 2025 · do design original SENDA
- **Maria Cumbe** · Registar UEM · do design original SENDA

Cross-systems explícitos:
`cross-Educação Digital` · `cross-Vida Civil` · `cross-eBI` · `cross-Migrações` · `cross-Justiça` · `cross-AT` · `cross-Sociedade Aberta` · `cross-Trabalho` · `cross-Eleições Digitais` · `cross-Saúde` · `cross-MECTS` · `cross-Resiliência Climática` · `cross-CFJP` · `cross-MNEC`.

---

## 10. Volume

Total · ~5 900 linhas · 9 HTML + 8 markdown.
- styles.css · 1 341
- index · 232
- design-system · 576
- 7 surfaces · 421-712 cada · médio ~530

A maior superfície é a Candidatura (712) · porque tem 4 passos do wizard + browser de cursos + paralelo nacional. A menor é a Painel (421) · porque é vista panorâmica · não fluxo.
