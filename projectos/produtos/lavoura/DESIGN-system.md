# DESIGN-system.md — Sistema de design Lavoura

**Status:** v0.1 · Abril 2026
**Domínio:** Assistente Agrícola Digital · produto consumer · Moçambique
**Total:** 7 superfícies · 49 cenas · 6 componentes signature · 3 línguas (PT · Changana · Macua)

---

## 1. Princípio de design

Lavoura é um **produto consumer** · não infraestrutura. Não tem peso de Estado · tem calor de companheiro. A linguagem visual reflecte isso · paleta quente · tipografia mais humana · áudio omnipresente · botões grandes para dedo grosso.

A produtora-tipo é a Sara Mucavele · 34 anos · Boane · viúva · 6 ha · 3 filhos. Lê português hesitante · fala changana com a mãe · tem Android barato com 4G intermitente. **O design é para ela primeiro · todos os outros utilizadores são bónus.**

A linguagem deve dizer simultaneamente:
- **Companheirismo** · não comando institucional
- **Confiabilidade** · funciona offline · não falha quando precisa
- **Voz humana** · Mesu fala · não emite mensagens
- **Tecido social respeitado** · associação · liderança · troca de favores

---

## 2. Paleta · 4 famílias temáticas

### Terra · primary · castanho de barro
- `--terra-700 #6b4423` · **PRIMARY · marca Lavoura**
- `--terra-900 #3a2410` · headers escuros · footers
- `--terra-50 #faf6f1` · bg-page · papel quente

### Folha · sucesso/crescimento · verde lima
- `--folha-600 #4d7c0f` · sucesso · "está bom"
- `--folha-100 #e2f5cd` · backgrounds positivos

### Sol · atenção · amarelo âmbar
- `--sol-500 #f59e0b` · atenção · "olha bem"
- Usado em alertas amarelos · não emergências

### Céu · clima · azul
- `--ceu-600 #0284c7` · clima · chuva · vento
- Botões de áudio · informação atmosférica

### Perigo · vermelho
- `--perigo-600 #dc2626` · praga · seca · perda · só para emergências reais

A barra de 4px no topo (`.lavoura-stripe`) mostra as 4 cores em sequência · marca identitária do sistema.

**Decisão consciente:** paleta NÃO é a azul institucional do SENDA. Lavoura não é Estado. É terra · campo · sol. Cores quentes · não corporativas.

---

## 3. Tipografia · 3 famílias

| Família | Uso |
|---|---|
| **Inter** | UI · botões · tabelas · formulários · 99% dos textos |
| **Lora** | Headlines de campanha · pull quotes · vozes de Mesu (fala em serif) |
| **JetBrains Mono** | Números · IDs · GPS · medidas |

UI é maior do que SENDA · 15px base · botões 44-64px altura · ícones 32-48px. **Razão:** Sara lê ao sol · com olhos cansados após manhã na machamba. Botões pequenos não funcionam.

---

## 4. Os 6 componentes signature

| # | Componente | Onde aparece principal |
|---|---|---|
| 1 | `.machamba-card` · cartão de parcela com mini-mapa | Sistema · Agenda · Onboarding |
| 2 | `.tarefa-row` · tarefa do dia com check + áudio | Agenda · Plantio |
| 3 | `.calendar-strip` · 12 meses agrícolas em fita | Agenda · Plantio |
| 4 | `.diag-camera` · câmara + frame + resultado | Diagnóstico |
| 5 | `.preco-board` · 3 mercados com tendência | Mercado |
| 6 | `.caderno-entry` · diário de bordo · fotos · áudio | Caderno · Agenda |

Componentes auxiliares importantes:
- `.mesu` · avatar do conselheiro digital · pseudo-elementos para "olhos"
- `.btn-audio` · botão azul de áudio · presente em todo o lado
- `.btn-mic` · botão amarelo de microfone · entrada por voz
- `.lang-pill` · selector trilingue · acessível em 1 toque
- `.culture-tag` · tags coloridas por cultura (tomate · milho · feijão...)

---

## 5. Mesu · o conselheiro digital

**Mesu** = "olho" em Changana · vê a machamba contigo. Não é chatbot · é extensionista paciente.

### 5 regras da voz Mesu

1. **Sempre cumprimenta** · "Bom dia Sara" · "Boa tarde mamã"
2. **Nomeia coisas concretas** · "as tuas tomateiras" · não "as suas plantações"
3. **Dá razão antes de recomendação** · "choveu 4mm · então rega"
4. **Reconhece quando não sabe** · "esta praga não consigo identificar bem · vê com o extensionista"
5. **Não usa jargão** · "fungo" não "Phytophthora infestans" · só científico se Sara perguntar

### Mesu sugere · não impõe

Nunca diz "Tu deves". Diz "Sara · vê só · choveu pouco esta semana · talvez seja boa altura para regar". **Sara é a dona da machamba.** Mesu é apoio.

---

## 6. Layout patterns

### Phone frame · 380px
Interface principal é mobile. Phone frame com statusbar mostra contexto (hora · rede · bateria). Tab bar com 5 ícones grandes.

### Desktop frame · raro
Apenas usado em surface 0 (sistema) e quando comparações tabulares precisam de largura. **Lavoura é 95% mobile · 5% web.**

### Scenes · 7 cenas por superfície
Cada superfície tem 7 cenas. Cada cena tem `.scene-h` com número e label · `.scene-c` com conteúdo. Variantes `.alt` (fundo subtle), `.dark` (terra-900 fundo · texto branco), `.folha` (verde · usado em fechos positivos).

---

## 7. Voz e tom

- **Português europeu de Moçambique** · "machamba" não "horta" · "registar" não "regista"
- **Sem jargão técnico desnecessário** · "doença do tomate" não "fitopatologia"
- **Sem entusiasmo gratuito** · não "Boa! Está dentro!" · sim "Está bom · pode descansar"
- **Pull quotes longas e narrativas** · personas falam como pessoas reais · histórias completas
- **Stats sempre com contexto humano** · "+ 70% margem" → "1 944 MT extra · ou 5 horas mais com os filhos"

---

## 8. Princípios técnicos

### Offline-first · não offline-tolerant
Lavoura assume que **não há rede como default**. SQLite local · sincroniza quando há 4G. Modelo de classificação de imagens corre **no telemóvel** · não na nuvem · 8.4 MB · MobileNetV3-Small quantizado.

### 3 línguas · paralelas
PT (UI) · Changana · Macua. Cada utilizador escolhe língua escrita E língua falada (podem ser diferentes). Áudios pré-gravados em todas. Vídeos de extensionistas SDAE em Changana ou Macua com legendas PT.

### SMS gateway
Quando produtora está fora de cobertura 4G mas tem sinal de voz · alertas críticos vão por SMS via cross-INAM short code 1411.

---

## 9. O que NÃO usar

- **Não usar emojis decorativos no UI principal** · só em ícones de cultura (🍅 🌽) onde é deliberado
- **Não usar cores frias dominantes** · Lavoura é quente · terra-folha-sol
- **Não usar fontes com aspecto corporativo** · Inter é neutra · Lora é íntima
- **Não usar interjeições comerciais** · "Cadastre-se já!" · zero · isto é companheiro · não app
- **Não substituir liderança humana** · Carlota negocia · Lavoura suporta · nunca o inverso

---

## 10. Volume

Total · ~6 280 linhas de HTML/CSS · 9 ficheiros HTML + 8 markdown.
- styles.css · 1 121
- index · 250
- design-system · 488
- 7 surfaces · 527-714 cada · médio ~615

A maior superfície é Agenda (714) · porque tem 7 cenas com phone mockups · clima · timeline. A menor é Caderno (527) · porque é mais densa textualmente · menos elementos visuais novos.
