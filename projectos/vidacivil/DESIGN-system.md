# DESIGN-system.md — Vida Civil · Conservatória Digital

**Status:** v0.3 · Abril 2026
**Pacote:** 10.º da família Conceitos
**Domínio:** registo civil completo · ciclo de vida do cidadão moçambicano

---

## 1. Premissa

Os actos vitais começam onde acontecem.

- **Nascimento** começa no hospital · enfermeira regista sexo, hora, peso, mãe (por eBI)
- **Óbito** começa no hospital · médico regista · todos os outros pacotes do ecossistema sabem em segundos
- **Casamento** começa onde for celebrado · oficiante credenciado regista
- **Divórcio consensual** na conservatória, litigioso no tribunal
- **Conservatória** deixa de ser ponto-de-partida · passa a ser **ponto-de-completamento**

Esta inversão resolve dois problemas reais e específicos de Moçambique:

1. **Sub-registo de nascimentos rurais.** Famílias sem meios ou cultura de deslocação à cidade para registar o bebé. Resultado: crianças sem assento, sem BI, sem direitos plenos. **Solução:** registar onde o bebé já é visto por profissional credenciado · maternidade.

2. **Óbitos não comunicados.** Reformados que continuam a "receber" pensão, eleitores que continuam inscritos, contas bancárias que continuam abertas, DUATs que não passam aos herdeiros. **Solução:** óbito hospitalar é automático cross-system · todos os pacotes irmãos sabem em segundos.

---

## 2. Lei moçambicana de inspiração

| Lei | Conteúdo |
|---|---|
| Lei 12/2004 | Registo Civil |
| Lei 10/2004 | Família · Casamento |
| Lei 22/2009 | Sucessões |
| Decreto-Lei 60/2018 | Mudança de nome em registo civil |
| Lei 23/2007 | Trabalho · pensão sobrevivência |
| Lei 19/97 | Terras · sucessão DUAT |
| Lei 14/2018 | Identidade civil eBI |
| Constituição art. 35-50 | Direitos da família |

---

## 3. Paleta · "papel cartório"

A escolha visual sinaliza dignidade institucional sem ser corporativa fria.

### Núcleo
- **Ink-marinho** `#1E3A5F` — cor de tinta de caneta cartorial · headlines, navegação activa
- **Papel cartolina** `#F4ECDA` → `#DBCDA6` — cream profundo, mais sólido que Sociedade Aberta
- **Brass** `#A87E3F` → `#7E5C2A` — selos oficiais, cunhos, validações brilhantes

### Suporte
- **Vermelho-livro-de-registo** `#7A2820` — linhas verticais nos formulários (livros de assento), divórcios, óbitos
- **Verde-cunho** `#5A7C42` → `#3F6B33` — confirmações, vivos, nascimentos
- **Amber** — pendências, processos em curso

### Tipografia
- **IBM Plex Serif dominante** — o pacote inteiro respira serif. Documentos legais. Headlines. Nomes próprios. Citações.
- **IBM Plex Sans** — UI corpo, formulários
- **IBM Plex Mono** — NUITs, datas, números, overlines

---

## 4. Componentes signature (6)

### 4.1 `.assento` — documento serifado
**O componente identitário do pacote.** Header com Plex Serif, papel cream, header-stripe brass+ink+livro, selo no rodapé, QR de validação. 6 variantes:
- `.nascimento` (border-top verde)
- `.casamento` (brass)
- `.obito` (cinza)
- `.divorcio` (vermelho-livro)
- `.nome` (ink-marinho)
- `.provisorio` (border tracejado brass)

### 4.2 `.cedula` — cartão de identificação infantil
Formato cartão real. Header ink-marinho com nome do documento. Foto + dados serifados + rodapé mono.

### 4.3 `.arvore-fam` — árvore genealógica SVG
Visualização hierárquica: ascendentes em cima, ego no centro, descendentes em baixo, cônjuges horizontais. Vivos (verde), falecidos (cinza com ✝), bebés (brass).

### 4.4 `.timeline-vida` — linha do tempo pessoal vertical
Da nascença ao presente. Eventos coloridos por tipo (nasc verde, casa brass, obit cinza, now livro com pulse). Útil em Cidadão e Sucessão.

### 4.5 `.regime-card` — visualização do regime patrimonial
3 variantes: separação total, comunhão de adquiridos, comunhão geral. Visual de barras mostra como bens se distribuem entre cônjuges.

### 4.6 `.assento-prov` — assento provisório do hospital
Border tracejado brass · "PROVISÓRIO" no canto · número grande mono. Componente único do pacote — tradução visual da inovação principal (registo no hospital).

---

## 5. Documentos · 6 amostras

Cada documento tem chancela legal e aparece como artefacto reutilizável:

| Documento | Onde aparece | Cores | Selo |
|---|---|---|---|
| Assento de nascimento de Lara | Cidadão Cena 2, Hospital Cena 4, Conservatória Cena 4 | verde + brass | DNRN |
| Cédula de identificação infantil | Conservatória Cena 4 | ink + brass | DIC |
| Certidão de casamento Felisberto+Joana | Cidadão Cena 4, Conservatória Cena 5 | brass | DNRN |
| Certidão de óbito de João Mahique | Cidadão Cena 6, Hospital Cena 7, Sucessão Cena 1 | cinza + ink | DNRN |
| Sentença de divórcio (caso fictício secundário) | Conservatória Cena 6 | livro | Tribunal de Família |
| Certidão de mudança de nome | Acto sensível Cena 4 | ink-marinho | DNRN + Tribunal Provincial |

Todos com QR validável e hash imutável.

---

## 6. Tom emocional

Diferente de tudo o que já fizemos no ecossistema. Aqui há:

- **Gentileza nos nascimentos** — "Bem-vinda, Lara" é mais apropriado que "Submeter requerimento"
- **Sobriedade nos óbitos** — sem exclamações, sem cores fortes. Espaço respiratório.
- **Solenidade nos casamentos** — Plex Serif majestoso. Os nomes em destaque grande.
- **Respeito na mudança de nome/género** — privacidade reforçada, vocabulário cuidadoso, supervisão judicial visível.

A linguagem da app evita burocratismo onde puder. "Comunicar nascimento de Lara" em vez de "Submeter requerimento de assento". "Comunicar falecimento" em vez de "Processar óbito".

---

## 7. Personas convencionadas

| Persona | Papel | Continuidade |
|---|---|---|
| **Felisberto Manjate** | Cidadão protagonista · 38 anos · Inhambane | Terras + Sociedade Aberta |
| **Joana Sumane** | Esposa · grávida → mãe de Lara | Nova |
| **Lara Manjate Sumane** | Bebé · nascida 4 Maio 2026 | Nova · personagem central da narrativa |
| **João Mahique Tembe** | Falecido 14.02.2026 · pai do Felisberto | Já existente em Terras |
| **Júlia Sumane Tembe** | Co-herdeira · fiscal Sofala | Terras + Fiscal |
| **Filomena Cossa Tembe** | Viúva de João · mãe de Felisberto e Júlia | Nova |
| **Enf.ª Marta Macuácua** | Enfermeira maternidade Maxixe | Nova |
| **Dr. Pedro Cossa** | Médico de família · regista óbitos | Nova |
| **Sr.ª Cremilda Tembe** | Conservadora Maxixe | Nova |
| **Padre António Sitole** | Oficiante casamento religioso · credenciado | Nova |
| **Régulo Mahique de Cheringoma** | Autoridade tradicional | Já existente em Terras |
| **Adelaide Cossa** | Persona de mudança de nome (Cena Acto sensível) | Nova · respeitosamente |

---

## 8. Cross-system (matriz)

Vida Civil é o pacote com mais cross-tags do ecossistema. Cada acto vital propaga-se:

| Cross-tag | O que provê / aciona |
|---|---|
| `cross-eBI` | Identidade civil de mãe/pai/cônjuge/falecido |
| `cross-Saúde` | Hospital regista nascimento e óbito |
| `cross-Terras` | DUAT herdado por sucessão |
| `cross-AT` | Cônjuge sobrevivo herda contas bancárias · cessação de NUIT por óbito |
| `cross-NUEL` | Cessação de pessoas colectivas em que falecido era único accionista |
| `cross-INSS` | Pensão de sobrevivência para viúva/o |
| `cross-NUSS` | Trabalho · contrato cessa por óbito |
| `cross-CFJP` | Régulo confirma óbito sem assistência médica |
| `cross-Justiça` | Divórcio litigioso · sucessão litigiosa |
| `cross-Eleições` (futuro) | Eleitor riscado por óbito |
| `cross-Bo Moçambique` | Contas bancárias do falecido |
| `cross-Migrações` | Adopção internacional · óbito de estrangeiro residente |
| `cross-Sociedade Aberta` | Casamento afecta património declarado · óbito risca pessoa pública |
| `cross-DIC` | Cédula de identificação infantil emitida pelo Direcção de Identificação Civil |

---

## 9. Edge cases (resumo)

- **Parto domiciliar com parteira tradicional** → app simples para parteira credenciada · cross-CFJP
- **Morte sem assistência médica** → autoridade local declara · médico legista valida posteriormente
- **Pais não comparecem para escolher nome** → bebé fica "Manjate Sumane" durante 12 meses · após esse prazo, conservadora atribui nome genérico
- **Casamento poligâmico costumeiro** (cultural em MZ) → reconhecido tradicionalmente, registado como uniões separadas
- **Mudança de género** → confidencial, supervisionado por TJ Provincial, privacidade configurável
- **Adopção internacional** → cross-Migrações
- **Pessoas sem assento (gerações mais velhas rurais)** → "registo tardio" com testemunhas comunitárias
- **Cidadão com Alzheimer/incapacidade** → representante legal designado pelo TJ
- **Bebé natimorto** → assento de óbito sem assento de nascimento
- **Bebé que morre durante parto** → assento de nascimento + assento de óbito imediato
- **Mãe falece no parto** → bebé fica vivo · pai (ou família) declarante imediato

---

## 10. Open questions

- Como gerir bebés abandonados em hospitais (lei MZ é silenciosa)?
- Casamento sem cônjuge presente (procuração) — admite a Lei 10/2004?
- Reconhecimento de paternidade post-mortem — DNA + tribunal — fluxo digital possível?
- Pessoas trans em Moçambique — Lei é progressiva no papel mas conservadora na implementação · tom da Surface 6 deve ser cuidadoso
- Casamento entre pessoas do mesmo sexo — não reconhecido por Lei 10/2004 · pacote não aborda
- Refugiados sem documentação de origem — fluxo cross-Migrações ou Vida Civil?
