# DESIGN-verificacao.md — Surface 6 · Verificação pública

**Personas:** Sandra Magaia (HR TechCorp) · Sarah van der Merwe (Goldfields SA) · Drª Helena Ferreira (Vice-Cônsul Portugal)
**Forma:** Phone (empregadora MZ) + desktop (embaixada / SA empresa)
**Foco temporal:** verificação · 3 segundos
**Total cenas:** 7

---

## 1. Propósito

Mostrar a **anti-fraude por desenho**. Um diploma SENDA é verificável em 3 segundos · sem login · sem custo · em qualquer país. Empregadores nacionais · diáspora · embaixadas · universidades estrangeiras — todos podem confiar.

Esta superfície existe para responder à pergunta · "ok · há um diploma digital · mas como é que eu sei que é verdadeiro?". A resposta é o componente signature 7 · `.verificacao-publica` · com 3 estados claros: válido · revogado · em equivalência.

---

## 2. 7 cenas

| # | Título | Cenário |
|---|---|---|
| 1 | Empregadora · Maputo · 14h22 | Sandra · TechCorp · escaneia QR de candidato · 3 seg |
| 2 | 3 estados · valid/revoked/pending | Componente signature 7 em 3 variantes |
| 3 | Diáspora · Joanesburgo SA | Sarah · Goldfields · valida diploma sem tradução |
| 4 | Embaixada Portugal · visto | Drª Helena · valida diploma para visto de mestrado |
| 5 | Detecção de fraude · 4 padrões | PDF adulterado · DOC ID inventado · QR substituído · diploma estrangeiro inventado |
| 6 | Privacidade · 4 níveis | O que é público · partilhável · privado · confidencial |
| 7 | 184 K verificações · 30 dias | Vista nacional · pull quote Sandra |

---

## 3. Componente signature 7 · `.verificacao-publica`

3 estados visuais:
- **Verde · DIPLOMA VÁLIDO** · success-bg · ✓ ícone · contratável
- **Vermelho · REVOGADO** · danger-bg · ✕ ícone · razão pública
- **Amarelo · EM EQUIVALÊNCIA** · warning-bg · ! ícone · processo aberto

Cada card mostra: titular · curso · ano · instituição · créditos + DOC ID em mono. Princípio · informação suficiente para decidir · não excessiva.

---

## 4. 4 padrões de fraude (Cena 5)

| Padrão | Tentativas 2025 | Como SENDA detecta |
|---|---|---|
| 1 · PDF adulterado | 1 218 | QR resolve para diploma original · discrepância visível |
| 2 · DOC ID inventado | 418 | senda.gov.mz responde "DOC ID inválido" |
| 3 · QR substituído | 218 | Nome do QR não bate com nome do PDF |
| 4 · Diploma estrangeiro inventado | 84 | Sem registo SENDA · sem processo de equivalência |

**1 938 tentativas · 0 sucessos · 100% taxa de detecção.** Antes de SENDA · taxa de fraude estimada 6-8% no mercado MZ (BM 2018).

---

## 5. 4 níveis de privacidade (Cena 6)

Decisão de design crítica · nem tudo é público · cidadão controla o que partilha:

| Nível | O quê | Quem vê | Cidadão controla |
|---|---|---|---|
| 1 · Público | Existência · curso · ano · instituição · estado · DOC ID | Qualquer um · sem login | Acordou na matrícula |
| 2 · Opcional partilha | Média · estágios · transcript completo | Empregador específico · URL com expiração | Sim · gera/revoga |
| 3 · Privado | Notas individuais · presenças · disputas | Só cidadão | N/A · não partilha |
| 4 · Confidencial | BI completo · biometria · saúde académica | Cross-Justiça com ordem judicial | Não · só por força legal |

**Sandra (empregadora) NÃO vê:** BI completo · morada · notas individuais · faltas · histórico de saúde · estado civil · disputas que cidadão abriu · outras candidaturas.

cross-CNPDP enforça · cidadão pode ver "quem verificou meu diploma · quando · que IP" · acesso anómalo gera alerta.

---

## 6. Cenários internacionais

**SA · Joanesburgo (Cena 3):** Sarah van der Merwe valida diploma de João Mucache em senda.gov.mz · Chrome · página em inglês (browser language) · 3 segundos · contrata em 14 dias. Poupa: 2 800 MT tradução juramentada · 1 200 MT apostilha Haia · 800 MT confirmação universidade · 60 dias.

**Embaixada Portugal · Maputo (Cena 4):** Drª Helena Ferreira · Vice-Cônsul · valida diploma de Ana para visto de mestrado UMinho · 3 segundos vs 30 dias do processo antigo. Visto emitido em 7 dias.

Acordos referenciados (fictícios):
- **CPLP** · 9 países · acordo 2025 · reconhecimento mútuo digital
- **SADC** · 6 países · acordo 2024 · validação cross-fronteira
- **218 universidades em 84 países** · acordos bilaterais

---

## 7. Cross-systems

cross-Vida Civil · cross-AT · cross-Justiça · cross-CNPDP · cross-MNEC · cross-Migrações.

---

## 8. Estatística (Cena 7)

184 124 verificações · 30 dias:
- 142 184 empregadores MZ (77%)
- 14 218 diáspora SA
- 8 412 diáspora Portugal
- 6 218 embaixadas
- 4 824 universidades estrangeiras (admissões)
- 3 218 diáspora Brasil
- 2 184 outros 14 países diáspora
- 2 866 cidadão verifica próprio

**3 segundos × 184 K = 552 K segundos poupados = 19 dias úteis poupados num mês = 11 funcionários públicos poupados anualmente.**

---

## 9. Pull quote · Sandra Magaia

> "Em 2018 contratei alguém com diploma falsificado. A empresa perdeu meio milhão. Eu quase perdi o emprego. Em 2026 · escaneio um QR · 3 segundos · sei a verdade. Não é só sobre dinheiro. É sobre poder dormir sossegada à noite · saber que contratei a pessoa certa · com a formação certa · sem ser enganada."

— Sandra Magaia · 38 anos · HR Director · TechCorp Mozambique · 30.04.2026

---

## 10. Personas

- **Sandra Magaia** · 38 anos · HR · TechCorp · pull quote final
- **Sarah van der Merwe** · HR Director · Goldfields Engineering · Joanesburgo
- **Drª Helena Ferreira** · Vice-Cônsul Portugal · Maputo
- **Ana Cristina Tembe** · diplomada · alvo de verificação 1
- **João Mucache** · diáspora SA · alvo de verificação 3
- **Joana Cossa Sumane** · pendente em equivalência · alvo de verificação 2 (estado pending)
