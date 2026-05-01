# DESIGN-diagnostico.md — Surface 4 · Diagnóstico de pragas

**Persona:** Sara Mucavele · 5ª utilização · acabou de voltar do centro de saúde
**Forma:** Phone · viewfinder de câmara · resultado · biblioteca
**Foco temporal:** 04.11.2026 · 13h28-13h32 · 4 minutos
**Total cenas:** 7

---

## 1. Propósito

Mostrar **anti-fraude por desenho** mas em sentido agrícola · não há ID falsa · há diagnóstico errado. Sara não pode confiar só na memória · míldio · alternaria · oídio · podridão de raiz têm sintomas parecidos · pesticida errado = dinheiro perdido.

Lavoura corre modelo classificação local · 3 segundos · resultado com probabilidades honestas · 3 alternativas em vez de 1 só. **Honestidade epistémica.**

---

## 2. 7 cenas

| # | Título | Foco |
|---|---|---|
| 1 | Sara vê manchas | 13h28 · folhas baixas · contexto + histórico |
| 2 | Câmara · 4 fotos · 4 ângulos | Cima · baixo · lateral · planta inteira |
| 3 | Análise · 3 segundos visíveis | Cérebro a pensar · honestidade epistémica |
| 4 | Resultado · 82% · 3 alternativas | Míldio · alternaria · mancha bacteriana |
| 5 | Tratamento · calda bordalesa | Receita exacta · 4 colheres · 20 L · 4 passos |
| 6 | Caso ambíguo · 52% · agrónomo | Eng. Júlio Tembe IIAM · revisão humana 18h |
| 7 | Biblioteca · 28 pragas | Explorar antes de problema · prevenção informada |

---

## 3. Componente signature · Diag-camera

Viewfinder com viewfinder verde-folha · frame em sol-300 dashed · botão capture branco com border sol-500. Resultado em 3 estados (ok · warn · bad) · borda colorida · pull quote de Mesu em serif itálico.

---

## 4. Decisões críticas

### 4 fotos · 4 ângulos
Diagnosticar uma doença em folha precisa 4 informações · cima (cor · padrão) · baixo (pulgão · oídio) · lateral com luz (textura · pó branco) · planta inteira (contexto). **Modelo treinado IIAM com 28 mil imagens · cada uma 4 ângulos.**

### 3 segundos visíveis · não 0,2
Modelo realmente leva 0,8-1,2 segundos. Os outros 2 segundos são propositados. **Confiança &gt; velocidade.** Mostrar passos visíveis ("comparar com 28 pragas") constrói confiança.

### 3 alternativas · não 1 só
Mesu nunca diz só "míldio". Diz "82% míldio · 12% alternaria · 6% mancha bacteriana". **Sara decide quando confiar.** Se fosse 52% míldio · 38% alternaria · pediria 2.ª opinião.

### 4 níveis de confiança
- **≥ 90%** · "vou com isso" · age direto
- **70-89%** · "provavelmente · age" · vê tratamento
- **50-69%** · "talvez · vê 2 hipóteses" · pondera
- **&lt; 50%** · "não sei · pergunta a agrónomo"

### Receita concreta · não princípio abstracto
Mesu não diz "aplicar fungicida cúprico". Diz **"4 colheres de sulfato · 4 colheres de cal · 20 litros de água"**. Quantidades calculadas para a área de Sara (2,4 ha). **Sara não traduz nada.**

### Continuidade humana
Quando caso vai a agrónomo · Lavoura prefere encaminhar para o mesmo agrónomo (Eng. Júlio Tembe) que respondeu a Sara antes. **Continuidade humana · não cego cada vez.**

---

## 5. Modelo técnico

- **MobileNetV3-Small** · CPU mobile · quantizado 8 bit
- **28 classes** · pragas + doenças + "saudável" + "desconhecido"
- **28 412 imagens treino** · IIAM + parceiros · validadas
- **8.4 MB** · cabe em qualquer Android
- **Precisão 78-92%** · varia por classe · míldio é 89%
- **4 fotos · ensemble vote** · 4 inferências combinadas
- **Funciona offline 100%** · não precisa de nuvem

---

## 6. 4 padrões de fraude (não no Lavoura · mas no contexto)

Não há "fraude" agrícola digital · mas há **erro epistémico**. Lavoura combate:

1. **Confiar excessivamente em memória** · "já vi isto · é míldio" · pode estar errada
2. **Tratamento errado por diagnóstico errado** · sulfato no fungo errado · dinheiro perdido
3. **Negar problema** · "não é nada · vai passar" · míldio espalha em 48h
4. **Dependência de extensionista distante** · Sara está sozinha às 13h sábado · não há quem ligue

---

## 7. Personas

- **Sara Mucavele** · protagonista
- **Eng. Júlio Tembe** · 38 anos · IIAM Maputo · agrónomo · responde 4-6 casos/sem do sul MZ
- **14 agrónomos voluntários** · IIAM · 4 horas/semana cada
- **Verónica** · SDAE Boane · referenciada · pode ser consultada presencialmente

---

## 8. Cross-systems referenciados

- **IIAM · Instituto de Investigação Agrária** · validador modelo · agrónomos voluntários
- **SDAE Boane** · extensionistas presenciais · alternativa ao Lavoura quando necessário
- **TechnoServe · Helvetas · ADIPSA** · parceiros do treino do modelo

---

## 9. Pull quote final · Sara

> "No ciclo 1 perdi 800 kg para o míldio porque não vi a tempo. Este ciclo · 4 fotos · 3 segundos · 32 mil meticais salvos. Vale uma motoreta nova."

— Sara Mucavele · 04.11.2026 · 13h32
