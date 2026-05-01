# DESIGN-hospital.md — Surface Hospital · profissional registar

**Status:** v0.3 · Abril 2026
**Surface:** 2 de 6 · **inovação central do pacote**
**Personas:** Enf.ª Marta Macuácua + Dr. Pedro Cossa · Hospital Provincial Inhambane

---

## 1. Propósito · "Os actos vitais começam onde acontecem"

A surface materializa o princípio fundador do pacote: o registo civil do nascimento e do óbito **começa no hospital**, não no balcão da conservatória.

Esta inversão resolve dois problemas reais e específicos de Moçambique:

- **Sub-registo de nascimentos rurais** · 14% nacional, 28% em Cabo Delgado. Quando o registo depende dos pais comparecerem à conservatória, muitos não vão · transporte caro, distância, tempo. **Aqui · Enf.ª Marta regista no momento do parto.** Bebé sai do hospital legalmente existente.

- **Óbitos não comunicados** · reformados continuam a "receber" pensão por meses, eleitores continuam inscritos, contas bancárias congeladas, DUATs em limbo. **Aqui · Dr. Pedro comunica o óbito · em 0,8 segundos toda a malha cross-system actualiza.**

---

## 2. Princípios

### 2.1 Tablet rugged · não cadeira de balcão
Profissionais de saúde móveis · enfermeiras passam de sala em sala. Interface optimizada para tablet 12" IP67 (resistente a fluidos). Mesma metáfora visual da Surface "Fiscal" em Terras Digitais.

### 2.2 Identidade da mãe primeiro
Antes de registar bebé · confirmar mãe. Cross-eBI valida em 2 segundos. Se mãe não tem BI (refugiada, sem documentação) · fluxo alternativo (Cena 5).

### 2.3 Provisório imediato + completamento depois
Hospital regista sexo, hora, peso, APGAR · gera **número provisório**. Pais escolhem nome **mais tarde** na conservatória (Surface 3). Esta separação é a inovação central.

### 2.4 Parto domiciliar coberto
Parteira tradicional credenciada (cross-Saúde) usa app móvel simples. Régulo confirma identidade da mãe (cross-CFJP). Hospital de referência valida em 30 dias.

### 2.5 Óbito · tom respeitoso
Linguagem cuidadosa · "comunicar falecimento" não "submeter óbito". Causa de morte só visível a quem tem interesse legítimo (cônjuge, herdeiros, INSS).

### 2.6 Cross-system em 0,8 segundos
Cena 7 demonstra a cadeia completa de notificações que sai do hospital. Esta é a inovação prática que justifica o pacote inteiro.

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Painel maternidade · 4 nascimentos hoje | Tablet · cards de salas |
| 2 | Identificar mãe · Joana via eBI | Tablet · biometria + scan BI |
| 3 | Registar bebé · sexo, hora, peso, APGAR | Tablet · form passo 2 |
| 4 | Provisório PROV-2026-IH-04421 + SMS | `.assento-prov` + phone mockup SMS |
| 5 | Parto domiciliar · parteira tradicional | Phone + sidebar com regras |
| 6 | Médico regista óbito · Dr. Cossa | Tablet · modo sóbrio |
| 7 | Cross-system · 0,8s | 2 cards lado-a-lado · 8 entidades |

---

## 4. Componentes signature

- `.tablet` (Cenas 1, 2, 3, 4, 6) — diferencia visualmente esta surface
- `.phone` (Cena 5) — parteira no campo
- `.assento-prov` (Cena 4) — peça única do pacote
- `.av.bebe` e `.av.falec` — recém-nascido brass + falecido cinza ✝

---

## 5. Cross-system propagado

**Quando nasce a Lara** (8 segundos):
1. cross-DNRN (arquivo provisório)
2. cross-DIC (cédula 5y)
3. cross-Saúde (cartão SIS-MA + vacinas)
4. cross-INE (estatística vital)
5. cross-eBI (mãe + pai)
6. cross-Família (árvore actualizada)

**Quando falece João Mahique** (8 segundos):
1. cross-DNRN (óbito arquivado)
2. cross-AT (NUIT cessado)
3. cross-INSS (pensão sobrevivência abre)
4. cross-Terras (3 DUATs em sucessão)
5. cross-NUEL (participações)
6. cross-Eleições (eleitor riscado)
7. cross-Bo Moçambique (contas em sucessão)
8. cross-Sucessão (processo guiado abre · Surface 5)

---

## 6. Edge cases

- **Mãe sem BI** → fluxo registo tardio · refugiadas, jovens sem documentação
- **Pai contestado** (mãe afirma outro pai) → bebé fica como "filho de mãe solteira" · pai legal pode contestar
- **Natimorto** → assento de óbito sem assento de nascimento prévio
- **Bebé que morre durante parto** → assento de nascimento + assento de óbito imediato
- **Mãe falece no parto** → bebé fica vivo · pai (ou família) declarante imediato
- **Bebé abandonado** → autoridade hospitalar designada · cross-Tutela
- **Parto múltiplo** (gémeos, trigémeos) → registos separados, mesmos pais
- **Morte sem assistência médica** (em casa) → autoridade local declara · médico legista valida

---

## 7. Personas

| Persona | Papel |
|---|---|
| Enf.ª Marta Macuácua | Maternidade · supervisiona 4 nascimentos/dia · 142 este mês |
| Dr. Pedro Cossa | Médico · cardiologia · regista óbitos |
| Dra. Cristina Tembe | Médica obstetra · responsável pelo parto da Joana |
| Maria Macuácua | Parteira tradicional credenciada · Mussassa |
| Régulo Mahique de Cheringoma | Confirma identidade em parto domiciliar · cross-CFJP |
