# Vona · princípios fundadores

**Vona** · do changana "vona" · ver. Aplicação de testemunho cidadão para Moçambique. Operada pelo **Centro de Jornalismo Cidadão · CJC-MZ** · consórcio independente fictício.

---

## Os 8 princípios

### 1 · Cidadão é fonte · não polícia

A polícia não tem acesso privilegiado a Vona. Não há API · não há push automático · não há canal traseiro. A polícia é leitora · igual a qualquer cidadã.

Material publicado é território público · qualquer um consulta livremente · incluindo a polícia. Material arquivado é território editorial protegido · só com pedido judicial específico · auditável publicamente.

### 2 · Editora decide · não algoritmo

Cada testemunho passa por revisão humana · nunca por publicação automática. Algoritmos servem para sugerir · nunca para decidir. **Decisão final é sempre de pessoa.**

### 3 · Publicação atrasada por design · 4-15 minutos

Não há feed em directo. Não há "trending now". Material entra em fila editorial · editora vê · valida · publica ou descarta. Atraso é a primeira protecção contra linchamento · contra propagação de erro · contra desinformação acelerada.

Mata o "wow factor" · salva vidas. **Velocidade é inimiga · não aliada.**

### 4 · Material arquivado é território editorial · não Estado

Testemunhos não publicados (descartados · em fila · arquivados por sensibilidade) ficam protegidos como qualquer fonte jornalística. Polícia precisa de pedido judicial específico · juíz autoriza · acesso registado e tornado público no relatório mensal de transparência.

**Sem back-channels · sem acordos institucionais privados · sem entregas voluntárias.**

### 5 · Anti-fake é primeira camada · não última

Cada testemunho passa por verificação automática antes de chegar à fila editorial:

- **EXIF intacto** · sem stripping · sem edição
- **GPS plausível** · não submetido de fora da zona
- **Timestamp recente** · janela curta após captura
- **Hash reverso** · não circulou antes na internet
- **Detecção de IA generativa** · modelos open-source
- **Watermark do device** se disponível (Apple/Samsung APIs)

Material que falha verificação não é descartado · é marcado **"verificação incompleta"** · editora decide. **Vona não confia · verifica.**

### 6 · Transparência operacional pública · mensal

Todo mês CJC-MZ publica relatório público com números crus:

- Testemunhos recebidos
- Testemunhos publicados
- Testemunhos descartados (e por que categoria)
- Testemunhos arquivados
- Pedidos judiciais recebidos
- Pedidos judiciais cumpridos
- Decisões editoriais contestadas pelo cidadão-fonte
- Erros publicados e corrigidos

**Não-transparência operacional (sigilo de fonte) compensada por transparência sistémica.**

### 7 · Linchamento não · suspeitas sem flagrante são descartadas

Vona aceita testemunho de:

- ✅ Acidente · em curso ou recente
- ✅ Evento público · manifestação · cerimónia
- ✅ Ambiente · poluição · destruição · desastre
- ✅ Acto criminoso em flagrante (rapto em curso · agressão visível)

Vona **não aceita** testemunho de:

- ❌ Suspeita sem flagrante ("este homem parece suspeito")
- ❌ Acusação a pessoa identificável sem prova
- ❌ Conteúdo que possa identificar vítima de violência (vítima de violação · criança em situação de abuso)
- ❌ Imagem de morte ou ferimento extremo (dignidade)

Editora descarta material destas categorias automaticamente · cidadão recebe aviso explicativo · não punição.

### 8 · IA tria · humano decide

A IA tem 6 funções claras dentro de Vona · todas sob supervisão humana:

| Função | O que faz | O que NÃO faz |
|---|---|---|
| **Triagem por urgência** | Sugere ordem da fila · vermelho/amarelo/cinza | Não publica · só sugere |
| **Verificação metadata** | EXIF · GPS · timestamp | Não descarta · só sinaliza |
| **Detecção de fakes** | IA generativa · adulteração | Não decide · alerta editora |
| **Reverse image search** | Imagem circulou antes? | Não bloqueia · informa |
| **Agrupar duplicados** | 14 pessoas reportam mesmo evento | Não unifica sozinha · sugere |
| **Detecção de violência gráfica** | Aviso antes de editora abrir | Não censura · protege |

A IA **não faz** nunca:

- Reconhecimento facial (face recognition)
- Identificação de pessoas em imagens
- Decisão final de publicação ou descarte
- Acesso a material arquivado para treino
- Avaliação de credibilidade da fonte

**A editora vê sempre o que a IA sugeriu e pode discordar com um toque.** Discordâncias são registadas · alimentam melhoria do modelo trimestralmente · processo é público.

---

## Decisões de design ancoradas

Cada uma das 7 superfícies do mock referencia explicitamente os princípios que serve:

| Surface | Princípios principais |
|---|---|
| 1 · Cidadão envia testemunho | 5 · 7 |
| 2 · Triagem · IA + verificação | 5 · 8 |
| 3 · Editora decide · fila | 1 · 2 · 3 · 8 |
| 4 · Publicação · cidadão lê | 1 · 6 |
| 5 · Arquivo · privacidade | 4 · 7 |
| 6 · Pedido judicial · workflow | 1 · 4 · 6 |
| 7 · Transparência · relatório mensal | 6 |

---

## Personas

**Cândida Sitoe** · 34 anos · vendedora ambulante · Av. 24 de Julho · Maputo. Smartphone Android barato. Testemunha o acidente que abre a narrativa · primeira protagonista.

**Beatriz Macuácua** · 38 anos · editora-chefe do CJC-MZ · 9 anos de experiência editorial · MA Comunicação. Decide se a foto da Cândida sai. Segunda protagonista.

**Manuel Tembe** · 52 anos · jornalista de investigação · trabalha com material arquivado em pesquisa de longa duração. Aparece nas surfaces de arquivo e pedido judicial.

**Juíz Daniel Cumbe** · 58 anos · Tribunal Judicial de Maputo. Aparece na surface 6 · workflow de pedido judicial.

---

## Operador · CJC-MZ (fictício)

**Centro de Jornalismo Cidadão · Moçambique.** Consórcio independente fundado em 2024 por:

- 3 redacções nacionais (fictícias · não nomes reais)
- 1 universidade nacional (faculdade de comunicação · fictícia)
- Orçamento de fundação fictícia + subscrições leitor
- Estatuto · associação sem fins lucrativos
- Sede · Maputo · com correspondentes em Beira · Nampula · Tete · Quelimane

**Não é entidade real · é construção narrativa do mock.** Decisão deliberada para não comprometer redacções existentes.
