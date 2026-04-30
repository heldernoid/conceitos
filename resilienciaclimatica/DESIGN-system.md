# DESIGN-system.md — Resiliência Climática · INGD Digital

**Status:** v0.3 · Abril 2026
**Pacote:** 11.º · provavelmente último da família Conceitos
**Domínio:** gestão de risco climático · pré · durante · pós eventos extremos

---

## 1. Premissa

Moçambique é o 3.º país do mundo mais vulnerável a eventos climáticos extremos. Idai (2019, 1303 mortos, 1,85 mil milhões USD em prejuízos), Kenneth (2019), Eloise (2021), Gombe (2022), Freddy (2023, ciclone mais longo da história), Chido (2024). Não é "se" · é "quando".

Este pacote materializa o ecossistema digital que **existe antes** da catástrofe e está **pronto quando** acontece. Cobre os três tempos:

- **Antes** · vigilância calma · informativo · "preparem-se"
- **Durante** · urgência sem pânico · ordens claras · "vão para o abrigo X agora"
- **Depois** · luto público + esperança · "perdemos · vamos reconstruir"

---

## 2. Cenário narrativo · pós-Chido

Para coerência narrativa em todas as superfícies, o protótipo passa-se em **Abril 2026**, **184 dias após o Ciclone Chido** que atingiu Cabo Delgado em 14 de Dezembro de 2024 (categoria 4, 73 mortos, ainda em fase de reconstrução).

Esta escolha permite cobrir todos os três tempos:
- **Pós-Chido em Cabo Delgado** · reconstrução em curso (Surface 6, 7)
- **Histórico Idai · Sofala · 2019** · referência institucional (Surface 1)
- **Vigilância em curso · Janeiro–Março é época de ciclones** · cenário "próximo evento" (Surface 2, 3)

---

## 3. Lei moçambicana de inspiração

| Lei | Conteúdo |
|---|---|
| Lei 15/2014 | Gestão de Calamidades |
| Decreto 7/2020 | INGD · estatuto e funções |
| Resolução 32/2017 | Plano Director de Gestão de Risco |
| Decreto 64/2010 | Plano de Contingência Nacional |
| Lei 19/97 | Terras (relevante para DUATs destruídos) |
| Convenção SADC 2009 | Cooperação regional em catástrofes |

---

## 4. Paleta · "alerta-tempestade"

Distinta de tudo o que já fizemos:

### Núcleo
- **Tempestade-noir** `#0F1419` → fundo de alertas críticos, painel INGD, memorial
- **Areia-resiliência** `#F2EAD2` → fundo principal, comunidade
- **Céu-tempestade** `#3A6788` → `#1E3A5F` · institucional INGD, headers

### Alerta (4 níveis)
- **Verde-recuperação** `#5A7C42` → `#3F6B33` · monitorização normal
- **Alerta-amarelo** `#E8B33A` → `#B68813` · vigilância
- **Alerta-laranja** `#E8541F` → `#A53412` · evento iminente ou activo
- **Vermelho** `#A53412` → `#631D0A` · catástrofe em curso

### Suporte
- **Cinza-cinza** `#6E7077` → destruição, perdas
- **Verde-recuperação** · pós-evento, "tudo bem agora"

### Tipografia
- **IBM Plex Sans** dominante · urgência, leitura rápida
- **IBM Plex Mono** · coordenadas, alertas, números, NUITs
- **IBM Plex Serif** · só em momentos de luto e memória (Surface 7 Memorial · pull-quotes)

---

## 5. Componentes signature (7)

### 5.1 `.alerta-pulsante`
4 níveis (verde, amarelo, laranja, vermelho) com pulsação animada. Cabeçalho de cada estado de alerta · faixa lateral colorida + círculo grande com nível L0/L1/L2/L3 + título + descrição.

### 5.2 `.mapa-risco`
Mapa MZ com camadas de risco · choropleth dinâmico em 4 níveis (r1-r4). Pulsação automática quando província tem evento activo. Reaproveitamento dos paths SVG dos pacotes anteriores.

### 5.3 `.tracker-ciclone`
Trajectória prevista do ciclone no Índico · estilo NHC · cone de incerteza. Inspirado em meteorologistas profissionais. Visual nocturno (noir-1 com gradient radial).

### 5.4 `.abrigo-card`
Censo de abrigo · capacidade vs ocupação · barra de progresso. Variantes: normal · cheio · lotado. Mostra coordenadas, contacto, recursos disponíveis.

### 5.5 `.fluxo-ajuda`
Sankey simplificado · doador → INGD → província → comunidade → família afectada. Cada camada com valor numérico · transparência total · cross-Sociedade Aberta amplificado.

### 5.6 `.kit-emergencia`
Lista visual do que cada família deve ter em casa · 7 dias de água, comida, medicamentos, lanterna, rádio. Ícones grandes, descrição clara, quantidades por pessoa.

### 5.7 `.memorial`
Sóbrio · listagem de vítimas em duas colunas serif · só nome + idade + comunidade. Sem foto. Sem dramatização. Fundo noir. Footer com frase de luto colectivo.

---

## 6. Tom emocional

Diferente de tudo o que já fizemos · este é o pacote mais difícil tonalmente. Os três tempos exigem registos distintos:

### Antes (vigilância)
Calmo, informativo. "Preparem-se." Linguagem instrutiva. Plex Sans regular. Cores frias (céu).

### Durante (urgência)
Curto, claro, accionável. "Vai para o abrigo X agora." Frases imperativas mas não alarmistas. Tipografia maior. Cores quentes (laranja).

### Depois (luto + esperança)
Solene mas não fúnebre. Plex Serif aparece. Cores neutras + verde-recuperação. Memorial nunca explícito · sem fotos de vítimas · só nomes.

**Linguagem inclusiva:** Macua, Changana, Sena, Nyungwe disponíveis em alertas críticos. Nunca só português · zonas de maior risco têm menor alfabetização em português.

**Imagens não-explícitas:** destruição é representada por dados (% casas afectadas, hectares inundados), não por trauma visual. Vítimas com dignidade · só nome e idade.

---

## 7. Personas

| Persona | Papel | Continuidade |
|---|---|---|
| **Eng.ª Esperança Macuácua** | Coordenadora INGD provincial · Cabo Delgado | Nova |
| **Felisberto Manjate** | Cidadão em zona de risco · Maxixe (continuidade família) | 10 pacotes |
| **Joana Sumane** + **Lara Manjate Sumane** | Família a evacuar · cross-Vida Civil | Vida Civil |
| **Júlia Sumane Tembe** | Fiscal SPGC Sofala · agora também voluntária INGD | Terras + Vida Civil |
| **Padre Manuel Cossa** | Comunidade local · abrigo na igreja | Nova |
| **Joana Mahique Cossa** | Jornalista Savana · investiga gestão fundos pós-Chido | Sociedade Aberta |
| **Régulo Mahique de Cheringoma** | Censo comunitário · cross-CFJP | Terras + Vida Civil |
| **Maria Nhantumbo** | Voluntária Cruz Vermelha MZ · paramédica | Nova |
| **Dr. Pedro Cossa** | Médico de família · agora também médico de campanha | Vida Civil |
| **Dra. Cremilda Tembe** | Conservadora Maxixe · regista óbitos pós-evento | Vida Civil |
| **Banco Mundial / UN OCHA** | Doadores institucionais (transparência) | Novos |
| **Sr. José Sitole** | Família reconstruindo · cidadão idoso afectado | Nova |

---

## 8. Cross-system (matriz · este pacote toca todos)

Resiliência Climática é o pacote com maior fan-out cross-system de todos · porque uma catástrofe afecta literalmente tudo:

| Cross-tag | O que provê / aciona |
|---|---|
| `cross-INAM` | Meteorologia · parceiro técnico do INGD |
| `cross-Vida Civil` | Óbitos em massa · registo digno |
| `cross-Saúde` | Feridos · hospitais danificados · surtos pós-evento |
| `cross-Terras` | DUATs destruídos · regularização especial |
| `cross-Trabalho · INSS / NUSS` | Subsídio de emergência · contratos suspensos |
| `cross-Educação` | Escolas afectadas · plano de retoma |
| `cross-Justiça` | Disputas pós-evento · tutela de menores |
| `cross-Eleições` | Processo eleitoral em zonas afectadas |
| `cross-AT` | Suspensão de obrigações fiscais zonas declaradas |
| `cross-Sociedade Aberta` | Transparência da ajuda · doadores rastreáveis |
| `cross-Bo Moçambique` | Suspensão temporária obrigações bancárias |
| `cross-Migrações` | Deslocados internos · apoio consular se estrangeiros |
| `cross-Cruz Vermelha MZ` | Mobilização · rede de voluntários |
| `cross-CFJP` | Régulos como autoridade comunitária · censo |

---

## 9. Edge cases

- **Pessoas desaparecidas** (não confirmadas mortas) · 30 dias antes de presunção legal de óbito
- **Crianças órfãs** · cross-Tutela · recolocação familiar prioritária
- **Cidadãos estrangeiros afectados** · cooperação consular · cross-Migrações
- **Comunidades de difícil acesso** (ilhas Zambeze, montanha Manica) · plano específico
- **Idosos isolados** · prioridade de evacuação · vizinho-protector designado
- **Animais de criação** · subsistência rural · não esquecidos · abrigos com espaço
- **Património documental destruído** (assentos antigos em conservatórias inundadas) · processo de reconstituição via testemunhos
- **Fundos de doadores · suspeita de desvio** · cross-CIP investiga · cross-Sociedade Aberta amplifica
- **Refugiados pós-evento** (Cabo Delgado já tinha refugiados de conflito · agora soma deslocados de Chido) · plano duplo
- **Pessoas em programa de protecção** · evacuação não revela localização ao agressor
- **Ciclone em zona de conflito** · INGD coordena com Forças Armadas para acesso seguro

---

## 10. Open questions

- Como gerir alertas em zonas com sub-cobertura GSM? Rádio comunitário · sirenes físicas · plano híbrido
- Doação de criptomoedas internacional · como integrar com cross-Bo Moçambique?
- Animais de estimação em abrigos · regulamentar?
- Memorial nacional · centralizado em Maputo ou descentralizado por província afectada?
- Plataforma multilíngue · custos de tradução em tempo real durante evento?

---

## 11. Filosofia de fim de série

Este é provavelmente o último pacote da família Conceitos. Foi escolhido para ser o último porque:

1. **Toca todos os 10 anteriores** · validação cumulativa do ecossistema
2. **Tem urgência real e específica MZ** · não é exercício abstracto
3. **Tem três tempos narrativos** · permite mostrar maior amplitude tonal
4. **Honra os mortos** · o Memorial é o componente mais sóbrio que já desenhámos · sinal de respeito por um país que já viu demais

Se houver continuação, fica em aberto para sugestões da comunidade.
