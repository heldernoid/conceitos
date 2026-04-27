# DESIGN-surveillance.md — Surface 5 · Vigilância e SIS-MA

**Status:** v0.5 · **esboço para validação** · Abril 2026
**Form factor:** Desktop browser, ≥ 1280 px. Information-dense; designed to live on a 24″ DPS / DPC monitor.
**Primary users:** Analistas de vigilância da DPS (Direcção Provincial de Saúde) e da DGS (Direcção Geral de Saúde Pública). Secondary: Direcção de Planificação Cooperativa (DPC), Inspectores de doenças notificáveis distritais.
**Setting:** Sala de situação provincial e nacional. Trabalho deliberado, não tempo-crítico — mas com janelas curtas (24–72 h) durante surtos declarados.

> ⚠ **Esta superfície é um esboço, não faz parte do v0.4.** É apresentada como **próxima iteração** à DPC e à DGS para validação antes de implementação. Não está construída na plataforma e nenhuma decisão clínica deve ser tomada com base nesta superfície enquanto não for ratificada. A implementação real ligará ao SIS-MA / DHIS2 do MISAU pelos canais oficiais.

---

## 1. Product purpose

Today, vigilância em Moçambique vive em três ferramentas separadas: BES-1 em papel preenchido pelo enfermeiro, transcrição manual para o SIS-MA pelo técnico distrital, e tabelas Excel partilhadas por email entre DPS e DGS. O sinal de surto chega à DGS com **5–14 dias de atraso médio**, o que é inaceitável para cólera, sarampo e dengue.

Esta superfície tem três promessas explícitas:

1. **Notificação electrónica directa do EMR para o SIS-MA.** O caso é declarado na consulta (CID-10 + sintomas + TDR), entra na fila do SIS-MA na mesma hora.
2. **Detecção precoce de cluster geográfico.** O sistema corre algoritmos baseline (C-Sum, EARS) sobre incidência distrital diária e levanta o sinal quando ≥ 3σ acima do esperado.
3. **Cadeia de custódia auditável até à DGS.** Cada notificação passa por 5 estados (EMR → DPS → DPC → SIS-MA → MISAU/DGS) e o auditor da DPI pode ver a viagem inteira.

A superfície deliberadamente **não é**: um sistema de modelação epidemiológica avançado (R₀, projecções, intervenções), um painel público para imprensa, ou um substituto para o SIS-MA — é o **front-end clínico** que o alimenta.

---

## 2. Information architecture

```
Sidebar (sticky)
├─ Visão geral             → KPIs nacionais, mapa de incidência, alertas activos, doenças notificáveis
├─ Casos notificáveis      → fila BES-1 electrónica, ficha individual, estados da cadeia
├─ Surtos declarados       → casos abertos com gestão (epidemiologista, distrito, intervenções)
├─ SIS-MA · DHIS2          → pipeline, log de envios, resolução de erros ETL
└─ Política & limiares     → limiares epidémicos por doença, regras C-Sum, contactos DGS/ANARME
```

Top bar: marca + "Saúde Moçambique · Vigilância · DPS", nav primária, conectividade ao SIS-MA (`SIS-MA · 43 em fila`), identidade do analista.

---

## 3. Screens

### S1 — Visão geral
Acima da dobra: 4 KPIs (casos notificáveis 7d, distritos acima do limiar, surtos activos, taxa de aceitação SIS-MA) com deltas semanais. Mapa de Moçambique com choropleth provincial por banda de incidência (≤ 50 / 50–150 / > 150 por 100 000) e pins de surto declarado. Mapa real cartográfico (geoBoundaries CC-BY 4.0) + Maputo Cidade (simplemaps).

Coluna direita: "sinais de surto · 7 dias" — máximo 3 cards de alerta (cólera Zambézia, sarampo Memba, dengue Beira), cada um com C-Sum, distritos afectados, e botão para abrir caso ou notificar DGS.

Abaixo do mapa: tabela de doenças de notificação obrigatória (cólera, sarampo, dengue, malária, peste, raiva, COVID-19, paludismo grave, doenças de origem alimentar, lesões por mordedura) com sparklines de 14 dias, contagem absoluta, taxa por 100 k, tempo desde o último caso, e meter de limiar epidémico.

### S2 — Casos notificáveis
Fila BES-1 electrónica. Filtros: província, distrito, doença, estado (rascunho / submetido / aceite SIS-MA / rejeitado / arquivado), data. Cada linha é um caso com: ID (mono `BES-2026-MZ-NNNNN`), CID-10, paciente (anonimizado a XX·123 quando o utilizador não tem clearance), unidade sanitária, profissional notificador, idade do caso, estado da cadeia.

Detalhe do caso: ficha BES-1 pré-preenchida (cabeçalho, dados demográficos, data de início de sintomas, sintomas marcados, TDR realizado, diagnóstico provisório, exposição/contactos, plano), com timeline de 5 estados em estepper horizontal, botões "Aceitar e enviar SIS-MA" / "Devolver ao notificador" / "Pedir confirmação laboratorial".

### S3 — Surtos declarados
Lista de surtos abertos por província com gestor epidemiológico, data de declaração, doenças, distritos, casos cumulativos, óbitos, duração estimada. Detalhe inclui: curva epidémica (data de início vs. casos novos), mapa do cluster com pontos georreferenciados (US, residência), lista de intervenções (água + saneamento, vacinação, busca activa, isolamento), recursos solicitados ao MISAU, e a folha de relatório semanal para a DGS.

### S4 — SIS-MA · DHIS2
Pipeline visual de 5 estados (EMR → DPS → DPC → SIS-MA → MISAU/DGS) com endpoint, autenticação mTLS, política de retry, e contagem em fila por estado. Tabela de envios recentes com status, payload size, latência, código de resposta. Painel de resolução de erros ETL (mapeamentos CID-10 → códigos DHIS2, falhas de validação, conflitos de identidade).

### S5 — Política & limiares
Tabela editável de limiares epidémicos por doença (cólera: 1 caso = limiar; sarampo: 5 casos / 100 k / semana; dengue: 50 casos / 100 k / 14 dias). Edição requer assinatura dupla DGS + ANARME. Histórico de alterações visível com versão, autor, justificação. Cards de configuração C-Sum (janela, σ, exclusão de fim-de-semana). Lista de contactos da DGS / ANARME / OMS-AFRO por especialidade.

---

## 4. Components & patterns

| Component | Surveillance-specific notes |
|---|---|
| **Mapa de incidência** | SVG com paths cartográficos reais (geoBoundaries). Coloração por banda; surtos declarados recebem hachura diagonal vermelha em vez de fill simples. Pins ancorados em coordenadas do viewBox (não absolute CSS) para escalarem com o mapa. |
| **Sparkline de doença** | 120 × 28 px, polyline 1.5 px, cor pelo critério: vermelho se acima do limiar, âmbar se em alerta, neutro caso contrário. Sem grid, sem eixos — leitura de tendência. |
| **Meter de limiar** | Barra horizontal compacta (60 × 6 px). Marca o ponto actual e a linha do limiar epidémico. Cor da preenchida segue a banda. |
| **Cadeia BES-1** | Estepper horizontal de 5 nós com etiquetas: EMR · DPS · DPC · SIS-MA · MISAU. Cada nó tem timestamp e profissional/sistema responsável. Estado completo a cheio, em curso a outline, futuro neutro. |
| **Pipeline SIS-MA** | Grid de 5 colunas + cabeça de seta. Cada estágio mostra endpoint, mecanismo de auth, política de retry, e contagem em fila. Erros surgem em row tinted vermelho. |
| **Card de alerta de surto** | Surface branca, indicador lateral colorido (4 px), título com doença + distritos, body com C-Sum + casos, footer com CID-10 + data + DPS responsável, actions: "Abrir caso" + "Notificar DGS". |
| **Pin de surto** | Círculo branco 11-px com borda colorida 3-px e ponto central 5-px da cor de severidade. Linha de chamada 2.5-px até cartão flutuante com eyebrow (CID-10 + nome da doença), título (província + distrito), valor (taxa + delta + casos). |
| **Privacy strip** | Como na auditoria: blue-100 fill, blue-700 border, 12-px ink. Texto: "Esta superfície apresenta apenas dados agregados ou casos notificáveis com base legal (DL 53/2014). Nunca exibe registos clínicos completos." |

---

## 5. Severidade e limiares epidémicos

| Doença | CID-10 | Limiar individual | Limiar epidémico (cluster) | SLA notificação DGS |
|---|---|---|---|---|
| Cólera | A00 | 1 caso confirmado | 2+ casos no mesmo distrito em 14d | **24 h** |
| Sarampo | B05 | 1 caso confirmado | 5 casos / 100 k / semana | **24 h** |
| Dengue | A90 | 1 caso confirmado | 50 casos / 100 k / 14d | 72 h |
| Peste | A20 | 1 caso suspeito | qualquer caso | **24 h, OMS imediato** |
| Raiva humana | A82 | 1 caso suspeito | qualquer caso | **24 h** |
| Paludismo grave | B50–B54 | — | desvio > 3σ acima da baseline sazonal | 7 d |
| COVID-19 / SARS-CoV-2 | U07.1 | — | sentinel agregado semanal | 7 d |
| Mordedura de cão | W54 | — | — | — (estatística) |
| Doenças de origem alimentar | A05 | — | 5+ casos com fonte comum em 72 h | 72 h |
| Lesões por arma de fogo | X95/Y22 | 1 caso (estatística) | — | — (mensal) |

Limiares editáveis em S5 com assinatura dupla DGS + ANARME e versão histórica.

---

## 6. Privacy & data flow

- A superfície apresenta predominantemente **dados agregados** (incidência por distrito, contagens por doença, séries temporais).
- **Casos individuais BES-1** mostram dados clínicos mínimos necessários à notificação obrigatória prevista em DL 53/2014: data de início, sintomas, TDR, diagnóstico, exposição. **Não** mostram a SOAP completa do encontro nem prescrições.
- Pacientes notificados em BES-1 são **anonimizados a `XX·NNN`** para analistas que não tenham clearance epidemiológica formal — apenas o epidemiologista distrital responsável e a DGS vêem identidade completa para busca activa de contactos.
- Toda a cadeia EMR → DGS é hash-encadeada como na auditoria: rotura de cadeia surge como alarme top-level.
- Cada execução de query agregada é registada no log auditor-do-auditor (visibilidade exclusiva à Inspectora-Geral).

---

## 7. Roles & permissions

| Role | Surface access |
|---|---|
| **Analista DPS** | Visão geral, casos da sua província, surtos da sua província, SIS-MA (read-only). |
| **Analista DGS** | Tudo. Pode aceitar/devolver casos, declarar surto, editar limiares (com co-assinatura ANARME). |
| **Epidemiologista distrital** | Casos do seu distrito com identidade completa para busca de contactos. |
| **Inspector ANARME** | Visão geral, política & limiares (co-assinatura). Read-only no resto. |
| **DPC (Planificação)** | Visão geral + dashboards trimestrais. Sem acesso a casos individuais. |
| **MISAU policy admin** | Política & limiares. Edits requerem dupla aprovação. |

---

## 8. Visual theme & posture (Surveillance)

A superfície vive entre **EMR (clínico, denso)** e **Auditoria (institucional, deliberado)**. Referências de desenho: dashboards do CDC FluView, semáforo da OMS-AFRO para emergências sanitárias, painéis epidemiológicos do ECDC. Anti-referências: dashboards de "executive overview" coloridos demais (Tableau / PowerBI templates), e ferramentas SOC tipo Splunk — vigilância **não é guerra**, é trabalho institucional metódico.

A cor dominante de chrome é a mesma da auditoria (`green-900` na sidebar) para reforçar o registo institucional e a co-residência com auditoria. O conteúdo usa `bg-2` (`#F2F1EB`) — meio passo mais quente que a página — para sinalizar "superfície de trabalho de dados".

Diferentemente da auditoria, a vigilância **tem direito a uso intencional de cor de severidade** porque a leitura de mapa exige distinguir bandas. A regra: o vermelho só aparece quando há sinal real (limiar excedido, surto declarado), nunca como elemento decorativo. Hachura diagonal sinaliza "surto declarado" em vez de "alerta", e é sempre acompanhada de borda da mesma cor para distinção do daltónico.

A tipografia é igual à do EMR: 14-px body em formulários BES-1, 13-px em tabelas de notificação (mais densas), mono em todos os identificadores de caso/CID-10/DHIS2-UID.

---

## 9. Component stylings (Surveillance)

### Mapa de incidência
- Container 680-px tall, `bg-2` background, 1-px `#E6E4DC` border, 4-px radius, posição relativa.
- SVG `viewBox="60 30 920 1480"` com `preserveAspectRatio="xMidYMid meet"`. Mapa real cartográfico (não esquemático).
- Province paths: `fill` por banda (`#E4EFE9` / `#F7ECCF` / `#F4D9D4`), `stroke="#FFFFFF"` 2-px (separação inter-provincial), 0-stroke nas fronteiras nacionais para o efeito choropleth limpo.
- Província com surto declarado: `fill="url(#hatch)"` (`<pattern>` de linhas vermelhas a 45° sobre fill rosa), `stroke="#C2392A"` 4-px.
- Província labels: `font-size: 24px` (no viewBox, ~9-10 px no ecrã), `font-weight: 600`, `fill: #1A1A1A`. Ancoragem `middle`.
- Capital dots: `r="6"`, `fill="#1A1A1A"`, `stroke="#fff"` 2-px. Apenas 5 capitais mostradas na vista nacional para reduzir ruído (Pemba, Lichinga, Tete, Beira, Maputo Cidade); outras em hover/zoom.
- Pin de surto: ver "Pin de surto" abaixo. Posicionamento em coordenadas do viewBox para escala correcta.
- Legenda: `position: absolute; right: 14px; bottom: 14px;` painel branco, 1-px `#D9D7CF`, 4-px radius, 240-px min-width, 4 linhas (≤ 50, 50–150, > 150, surto), `white-space: nowrap` por linha.
- Escala: `position: absolute; right: 14px; top: 14px;` painel branco, barra preta 80 × 3 px, label "0 — 200 km".
- Crédito: `position: absolute; left: 14px; bottom: 10px;` italic 10-px `var(--ink-3)` "Limites: geoBoundaries CC-BY 4.0 · Maputo Cidade: simplemaps.com".

### Sparkline de doença
- 120 × 28 px, sem viewBox padding.
- `<polyline>` 1.5-px stroke, sem fill.
- Cor pela banda: `#C2392A` se acima do limiar, `#C8911E` se em alerta, `#5E5E5E` se neutro, `#1B6B3A` se a melhorar.
- 13 pontos (1 por dia) — janela de 14 dias menos hoje.

### Meter de limiar
- 60 × 6 px container, fill `#F2F1EB`, 1-px `#D9D7CF`, 1-px radius.
- Barra preenchida da cor da banda actual.
- Linha vertical preta 1-px na posição do limiar.
- Tooltip on hover: "Actual: X / 100 k · Limiar: Y / 100 k".

### Cadeia BES-1 (estepper horizontal)
- Grid 5 colunas iguais + 24-px ponta de seta no fim.
- Cada nó: 28-px círculo + label 11-px / 600 / 0.06em UPPERCASE.
- Estado completo: círculo `#247A52` cheio + check branco. Em curso: outline 2-px `#C8911E` + ponto central. Futuro: outline 1-px `#A8A8A8`.
- Conexão: 2-px linha entre círculos, cor segue o estado (`#247A52` quando completo).
- Timestamp por baixo de cada nó: mono 11-px `#5E5E5E`.

### Pipeline SIS-MA
- Grid 5 colunas (`repeat(5, 1fr) 24px`), gap 0, alinhamento estendido.
- Cada estágio: padding 10 12, fundo branco, 1-px `#D9D7CF`, sem border-right (continuidade visual). Primeiro tem border-radius esquerdo, último direito.
- Header do estágio: 11-px / 600 / UPPERCASE 0.06em ink-3.
- Endpoint mono 11-px ink-2; auth+retry 11-px ink-3.
- Contagem em fila: chip mono 11-px com fundo `bg-2`.
- Erro: row tinted `#FCEFEC` + ícone vermelho à esquerda.

### Card de alerta de surto
- Layout `display: grid; grid-template-columns: 8px 1fr auto;` 12-px gap.
- Indicador lateral 8-px width altura total, cor por severidade (`var(--red-500)` para crítico, `var(--amber-500)` para alto).
- Body: H4 14-px / 600 ink, parágrafo 13-px ink-2, meta 12-px ink-3 (CID-10 + data + DPS responsável).
- Actions: 2 botões `sm` empilhados ou inline conforme largura — primário "Abrir caso", secondary "Notificar DGS".

### Pin de surto (dentro do mapa)
- Marca: `<circle r="11" fill="#fff" stroke-width="3">` + circle inner `r="5"` da cor de severidade.
- Linha de chamada: 2.5-px stroke da mesma cor.
- Cartão: rect 270–320 × 78 px, `rx="6"`, fill branco, 1.5-px `#1A1A1A` border, drop-shadow `dy=3 stdDeviation=3 opacity=.15`.
- Eyebrow: mono 14-px / 500 / 0.06em UPPERCASE ink-3 (ex: "CÓLERA · CID-10 A00").
- Título: 24-px / 700 ink (ex: "Zambézia").
- Valor: mono 18-px ink-2 (ex: "412 / 100k · ▲ 64% · 118 casos").

### Ficha BES-1 (formulário)
- Container: white, 1-px `#D9D7CF`, 4-px radius, 16-px padding.
- Grid 2 colunas (`1fr 1fr`) com 12-px gap por linha.
- Field: label 12-px / 500 ink-2, input/select 34-px alto / 13-px font.
- CID-10 picker: mono 13-px no input + sugestões abaixo (idênticas ao EMR).
- Sintomas: chips multi-selectivos 13-px com estado on/off, fundo `#E4EFE9` quando seleccionado.
- TDR / Resultado lab: rádio 3-estado (positivo / negativo / pendente).
- Botão submit: `lg` primary full-width, "Submeter para DPS" 14-px / 500.

---

## 10. Layout & spacing (Surveillance)

- Sidebar 240 px, sticky, `green-900`, items brancos 14-px / 500.
- Top bar 56 px, single row no-wrap (ver fix histórico para overflow).
- Conteúdo `bg-2`, padding 20 24, max-width 1500 px centrado.
- Grid de trabalho principal: `1.4fr 1fr` (mapa + alertas) com 16-px gap.
- KPIs: 4 colunas iguais, 12-px gap, 18-px margin-top.
- Tabela de notificáveis: full-bleed, 14-px header / 13-px body, 36-px row.
- Pipeline e xform-list: 2 colunas em viewport ≥ 1280, 1 coluna abaixo.

---

## 11. Do's and Don'ts (Surveillance)

### Do
- **Mostrar dados agregados por defeito.** Casos individuais só com clearance e justificação registada.
- **Verbalizar incerteza.** "Sinal de surto" ≠ "surto declarado". Use linguagem epidemiológica precisa.
- **Encadear cada notificação.** EMR → DPS → DPC → SIS-MA → MISAU; cada salto assinado e timestamped.
- **Cor de severidade só com sinal real.** Vermelho ≡ acima do limiar epidémico, nunca decorativo.
- **Mapa real cartográfico.** Limites geoBoundaries CC-BY 4.0; nunca esquemas geométricos para representar geografia.
- **Daltonismo:** banda + hachura, nunca apenas cor. Hachura para "surto declarado" complementa o vermelho.
- **Histórico de limiares editável e versionado.** Toda mudança de limiar requer assinatura dupla DGS + ANARME.
- **Logs auditor-do-auditor.** Cada query agregada é gravada no stream da Inspectora-Geral.

### Don't
- **Não mostrar SOAP completa.** Mesmo um excerpto da consulta do paciente notificado é violação. Mostre apenas os campos BES-1 obrigatórios.
- **Não declarar surto automaticamente.** O algoritmo levanta o sinal; a declaração formal é assinada pelo epidemiologista DGS.
- **Não usar mapas decorativos.** Choropleth apenas com fonte de dados explícita (CID-10 + período + numerador + denominador).
- **Não exibir alertas a piscar ou em movimento.** Vigilância é trabalho deliberado, não SOC. Sem ticker, sem countdown agressivo.
- **Não permitir edição directa do payload SIS-MA.** Erros de mapeamento ETL voltam ao EMR; a superfície de vigilância não tem privilégio de reescrever notificações.
- **Não publicar painéis em tempo real para imprensa.** A superfície é interna. Comunicação pública passa pela DGS / Gabinete de Imprensa, com agregação semanal e revisão.
- **Não substituir o SIS-MA.** Esta superfície ALIMENTA o SIS-MA via DHIS2; nunca compete com ele como sistema-de-registo.

---

## 12. Responsive behaviour (Surveillance)

| Width | Treatment |
|---|---|
| ≥ 1920 px | Sidebar 240 + content max 1500 + side gutters absorbem extra. Mapa expande até 720 px de altura. |
| 1440–1920 px | Default design target. Sidebar 240 + content. |
| 1280–1440 px | Mantém layout. Pipeline mantém-se em 5 colunas; tabela de notificáveis preserva colunas. |
| 1024–1280 px | Sidebar colapsa para rail de 60-px. Grid `.work` muda para 1 coluna (mapa em cima, alertas abaixo). Pipeline reduz para 3 colunas (EMR → SIS-MA → MISAU) com estados intermédios em tooltip. |
| 768–1024 px | Sidebar em drawer. Tabelas com scroll horizontal e primeira coluna sticky. Mapa simplifica para choropleth sem pins (pins viram lista abaixo). |
| < 768 px | Não suportado. Analistas DPS/DGS são utilizadores de gabinete. Login redireciona para "Use um desktop". |

---

## 13. Agent prompt guide (Surveillance)

### Component prompts
- **Mapa de incidência:** "SVG `viewBox=\"60 30 920 1480\"`, fundo `bg-2`, 680-px tall. Province paths from geoBoundaries CC-BY 4.0 dataset. Fill por banda: ≤ 50/100k = `#E4EFE9`, 50–150 = `#F7ECCF`, > 150 = `#F4D9D4`. Surto declarado: `fill=url(#hatch)` (45° red lines on rose) + `stroke=#C2392A` 4-px. Province labels 24-px / 600 fill-ink no viewBox. Capitais: dots 6-px ink + label 22-px ink-2."
- **Pin de surto:** "Marca circle r=11 white + 3-px stroke severidade + inner r=5 fill severidade. Leader line 2.5-px. Card 270×78 rx=6 white + 1.5-px ink border + dropshadow. Eyebrow mono 14-px UPPERCASE ink-3. Título 24-px / 700 ink. Valor mono 18-px ink-2."
- **Sparkline:** "120 × 28 polyline 1.5-px. Cor pela banda: red `#C2392A` se acima do limiar, amber `#C8911E` se em alerta, neutral `#5E5E5E` caso contrário, green `#1B6B3A` se a melhorar."
- **Meter de limiar:** "60 × 6 px barra horizontal, fill `bg-2`, 1-px ink-3 hairline. Preenchida pela cor da banda actual. Marker vertical 1-px black na posição do limiar epidémico."
- **Cadeia BES-1:** "Estepper horizontal 5 nós: EMR · DPS · DPC · SIS-MA · MISAU. Cada nó 28-px círculo + label 11-px UPPERCASE 0.06em. Completo: green-700 fill + check. Em curso: 2-px amber outline. Futuro: 1-px neutral. Connecting line 2-px segue estado."
- **Card de alerta de surto:** "Grid 8px 1fr auto. Indicador lateral 8-px altura total na cor de severidade. H4 14-px / 600 + body 13-px ink-2 + meta 12-px ink-3. Actions: btn `sm` primary 'Abrir caso' + btn `sm` secondary 'Notificar DGS'."
- **Pipeline SIS-MA:** "Grid `repeat(5,1fr) 24px` gap 0. Estágios border-collapse-style com border-radius apenas no primeiro/último. Header 11-px UPPERCASE 0.06em ink-3. Endpoint mono 11-px ink-2. Chip de fila mono 11-px com fundo bg-2."
- **Privacy strip:** "Full-width strip blue-100 fill, 1-px blue-700 border, 4-px radius, 12-px padding. 13-px ink. Texto: 'Esta superfície apresenta apenas dados agregados ou casos notificáveis com base legal (DL 53/2014).'"

### Iteration guide
1. **Cada cor é um sinal.** Vermelho = acima do limiar; âmbar = em alerta; verde = ok. Sem cor decorativa.
2. **Geografia é dado, não decoração.** Use sempre limites cartográficos reais. Cite a fonte (geoBoundaries CC-BY 4.0).
3. **Notificação tem cadeia.** EMR → DPS → DPC → SIS-MA → MISAU. Cada salto assinado.
4. **Sinal ≠ surto.** O algoritmo levanta sinal; o epidemiologista DGS declara o surto.
5. **Anonimização por defeito.** `XX·NNN` excepto para epidemiologista distrital com clearance e busca de contactos justificada.
6. **Alimenta SIS-MA, não o substitui.** O DHIS2 é o sistema-de-registo; esta superfície é o front-end clínico.
7. **Density on tables, prose on decisions.** Tabelas de notificação são 13-px; declaração de surto e relatório semanal são 14-px com prose cuidada.

---

## 14. Open questions

- **Definição operacional de "surto declarado".** O algoritmo levanta sinal a 3σ acima da baseline; a declaração formal é decisão humana. Quem assina (DPS provincial / DGS / ambos)? Co-assinatura dupla?
- **Janela de baseline.** Para cólera e dengue, baseline sazonal precisa de 5 anos de histórico; o SIS-MA tem 3. Como tratar o gap nos primeiros 2 anos da plataforma?
- **Busca activa de contactos.** Quem tem clearance para identidade completa? Apenas epidemiologista distrital, ou também enfermeiro chefe da US? Política precisa de redacção legal.
- **Integração ANARME e OMS-AFRO.** Notificações IHR-2005 (cólera, peste, raiva) requerem comunicação à OMS em 24 h. A superfície deve alertar automaticamente ou apenas a DGS aciona manualmente?
- **Modo offline para epidemiologista distrital.** O técnico distrital faz busca activa em terreno sem rede. Precisa de uma vista mobile com fila de actualizações para sync. Roadmap Q1 2027.
- **Interoperabilidade SADC.** Casos de cólera trans-fronteiriços (Tete-Malawi, Cabo Delgado-Tanzânia) requerem partilha. Protocolo SADC-EHR está em discussão; não decidido para v0.5.
- **Painel público.** A DGS quer publicar agregados semanais. A superfície suporta tecnicamente; é decisão política sobre granularidade (provincial? distrital? ponto-de-cuidado?) e periodicidade.
- **Falsos positivos do algoritmo.** Em distritos pequenos, 2 casos de cólera levantam sinal (denominador baixo). Como evitar fadiga de alarme sem perder sensibilidade real? Threshold dinâmico por população?

---

## 15. Roadmap

| Fase | Janela | Entregáveis |
|---|---|---|
| **Q3 2026** | 3 meses | BES-1 electrónico no EMR (formulário, submissão, queue local), pipeline mock SIS-MA com retry, dashboard DPS read-only com mapa choropleth e tabela de notificáveis. **Sem** declaração de surto, **sem** algoritmo C-Sum. |
| **Q1 2027** | 3 meses | Algoritmo C-Sum + EARS sobre baseline 12 meses. Declaração de surto manual com co-assinatura DGS+DPS. Vista do epidemiologista distrital com busca de contactos. Integração SIS-MA produção. |
| **Q3 2027** | 3 meses | Painel público trimestral com DGS. Notificação automática IHR-2005 à OMS-AFRO. Modo offline para distrital. Interoperabilidade SADC se acordo político fechar. |

---

## 16. Crédito de dados

- **Limites administrativos provinciais:** [geoBoundaries](https://www.geoboundaries.org/) CC-BY 4.0
- **Maputo Cidade enclave:** [simplemaps.com](https://simplemaps.com/) (uso permitido para projectos públicos)
- **Códigos CID-10:** OMS, edição PT 2023, formulário MISAU
- **Limiares epidémicos:** WHO-AFRO Integrated Disease Surveillance and Response (IDSR), 3rd edition (adaptação Moçambique)
- **Algoritmos de detecção:** EARS (CDC), C-Sum (Hutwagner et al.) — open algorithms

---
