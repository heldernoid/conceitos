# DESIGN-system.md — Eleições Digitais · STED Digital

**Status:** v0.4 · Abril 2026
**Pacote:** 12.º · final da série Conceitos
**Domínio:** sistema eleitoral · auto-inscrição · cadernos vivos · voto físico · transparência digital

---

## 1. Premissa

O direito de votar não devia exigir uma fila para se inscrever. Em Moçambique, o recenseamento eleitoral é tradicionalmente feito por campanhas físicas periódicas que exigem deslocação · perda de dia de trabalho · falta de acesso em zonas rurais. Resultado · 30%+ de cidadãos elegíveis ficam fora dos cadernos.

Este pacote materializa um **STED Digital** (Secretariado Técnico das Eleições Digitais · entidade fictícia) onde quatro pilares operam em conjunto:

1. **Auto-inscrição automática aos 18** · cross-Vida Civil
2. **Vivacidade verificada continuamente** · cross-Vida Civil óbitos
3. **Mesa de voto atribuída por proximidade** · cross-Terras endereço
4. **Voto físico em papel · mas tudo o resto é digital e público**

---

## 2. Princípio fundamental

**Voto em papel · mas auditável digitalmente em cada momento.** Papel é inquebrável · funciona sem electricidade · qualquer cidadão consegue auditar uma urna física. Mas tudo o que rodeia o papel · cadernos eleitorais, atribuição de mesa, contagem, resultados · é digital e público em tempo real.

A confiança constrói-se com camadas: 1) papel auditável; 2) cross-Vida Civil verifica vivos; 3) cross-eBI valida identidade na mesa; 4) cross-Terras valida endereço; 5) hash imutável de cada acto registado; 6) observadores cidadãos cruzam contagens.

---

## 3. Cenário narrativo · Eleições Gerais 2029

Eleições gerais previstas Outubro 2029 · 3,5 anos no futuro a partir do "agora" do protótipo (Abril 2026). Permite mostrar:

- **Hoje (Abril 2026)** · sistema em modo "entre eleições" · purga, auto-inscrições, mesas atribuídas
- **Pré-eleitoral 2029** · cadernos consolidados · campanha em curso (não retratada · neutralidade)
- **Dia eleitoral** · mesa em funcionamento · contagem · resultados ao vivo
- **Pós-eleitoral** · auditoria cidadã · contestações · proclamação solene

Pedro Manjate Sumane · filho dos Manjate (introduzido em Vida Civil) · faz 18 anos em 2027 · 1.ª inscrição mostrada na Surface 3.

---

## 4. Entidades fictícias (não usar reais)

| Real (não usar) | Fictício (este pacote) |
|---|---|
| STAE | **STED** · Secretariado Técnico das Eleições Digitais |
| CNE | **CNED** · Comissão Nacional Eleitoral Digital |
| Conselho Constitucional | **TES** · Tribunal Eleitoral Superior |
| EISA / Observatório | **OCI** · Observatório Cívico Independente |
| Frelimo / Renamo / MDM | **MDP / PVN / UC / AT** (4 partidos fictícios) |

**Partidos fictícios · 4 forças**

| Sigla | Nome completo | Cor | Símbolo |
|---|---|---|---|
| **MDP** | Movimento Democrático Popular | Azul `#3A6788` | Livro aberto 📖 |
| **PVN** | Partido Verde Nacional | Verde `#5A8466` | Árvore 🌳 |
| **UC** | União Cívica | Laranja `#C46150` | Aperto de mão 🤝 |
| **AT** | Aliança da Terra | Castanho `#8B6F47` | Espiga 🌾 |

Designados deliberadamente sem semelhança caricatural com partidos reais. Cores e símbolos genéricos.

---

## 5. Paleta · "boletim-cívico"

### Núcleo institucional
- **Tinta-boletim** `#1A2238` → `#0E1525` · azul-escuro CNED
- **Carimbo-validação** `#9B2D20` → `#6B1E15` · vermelho-vinho do "VOTOU"
- **Papel-recenseado** `#F4ECDB` → `#FBF7EE` · ofício creme

### Estados eleitorais
- **Verde-confirmado** `#5A8466` → `#3F6B4C` · vivo no caderno
- **Cinza-purgado** `#7A7873` → `#4F4E4A` · saiu (óbito, mudança)
- **Dourado-discreto** `#B68813` → `#7E5C09` · só cerimónia (proclamação, certidão)

### Tipografia
- **IBM Plex Sans** · UI · rigor institucional
- **IBM Plex Mono** · NUEL eleitoral · números de mesa · hashes
- **IBM Plex Serif** · boletim físico · proclamação oficial · pull-quotes solenes

---

## 6. Componentes signature (7)

### 6.1 `.caderno-publico`
Entrada de cidadão no caderno eleitoral. 3 estados visuais: **verde** (activo), **cinza** (purgado · óbito ou mudança), **dourado** (novo · auto-inscrição). Hash de validação visível. Anonimização parcial (NUEL público, BI privado).

### 6.2 `.mesa-card`
Mesa de voto · número grande dourado sobre fundo tinta-900 · localização GPS · presidente, escrutinadores, fiscais, capacidade. 3 estados (normal/alta/cheia).

### 6.3 `.boletim-fac-simile`
Réplica fiel do boletim físico · serif · selo CNED · 4 partidos fictícios com símbolo · quadrado para X · variante "marcado" mostra X em carimbo-vermelho.

### 6.4 `.pulse-recenseamento`
Painel ao vivo · número grande dourado de eleitores activos · lista cronológica de eventos (inscrições + purgas) · animação de pulso no evento mais recente.

### 6.5 `.gauge-participacao`
Medidor circular · % de participação ao vivo durante dia eleitoral · 4 estados de cor (baixa/média/alta/saturada).

### 6.6 `.verificacao-cruzada`
Cidadão pode auditar próprio registo · 4 fontes verificadas (BI cross-eBI, endereço cross-Terras, idade cross-Vida Civil, vivacidade cross-Vida Civil). Cada item ✓ verde / ⚠ amarelo / ✕ vermelho.

### 6.7 `.contagem-publica`
Tabela horizontal · 4 partidos · barra preenchida com cor partidária · % e votos · live update durante contagem.

---

## 7. Personas

| Persona | Papel | Continuidade |
|---|---|---|
| **Dra. Adelina Cuamba** | Coordenadora STED provincial · Inhambane | Nova |
| **Felisberto Manjate** | Cidadão · vota desde 2014 · sempre na mesma mesa | 11 pacotes |
| **Joana Sumane Manjate** | Cidadã · votou 1.ª vez em 2019 | Vida Civil |
| **Pedro Manjate Sumane** | Filho · faz 18 anos 2027 · 1.ª inscrição · 1.º voto 2029 | **NOVA · introduzida em Vida Civil** |
| **Aurélio Tembe** | Presidente da mesa 0142 · Maxixe · professor reformado | Nova |
| **Joana Mahique Cossa** | Jornalista Savana + observadora OCI-credenciada | 3 pacotes (Sociedade Aberta + Resiliência + agora) |
| **Régulo Mahique de Cheringoma** | Mesa rural · cobertura sub-cobertura GSM · CFJP | 4 pacotes |
| **Sra. Cremilda Macuácua** | Viúva · marido faleceu 2024 · cadernos purgam dele em 24h | Nova (Surface 7) |
| **Dr. Salomão Bila** | Juiz do TES · valida resultados pós-eleitorais | Nova |

---

## 8. Cross-system · 12 entidades

| Cross-tag | Função |
|---|---|
| `cross-Vida Civil` | **Principal.** Auto-inscrição 18+ · purga óbitos · idade · estado civil |
| `cross-eBI` | Validação biométrica na mesa · digital + foto |
| `cross-Terras` | Endereço para atribuição de mesa próxima |
| `cross-CFJP` | Régulos validam zonas rurais sub-GSM |
| `cross-Migrações` | Diáspora · embaixadas · voto antecipado no estrangeiro |
| `cross-AT` | NUIT mantém · NUEL eleitoral é separado mas validado |
| `cross-Justiça · TES` | Contestações eleitorais · validação final de resultados |
| `cross-Sociedade Aberta` | Transparência amplificada · auditoria cidadã |
| `cross-Resiliência Climática` | Adiamento se ciclone na semana eleitoral · mesas em abrigos |
| `cross-MININT` | Polícia · Forças Armadas · neutralidade nas mesas |
| `cross-OCI` | Observadores cívicos credenciados |
| `cross-RM/TVM` | Transmissão pública · resultados em directo |

---

## 9. Edge cases

- **Dia da eleição com ciclone activo** · cross-Resiliência Climática · adiamento decretado · mesas em abrigos
- **Cidadão sem morada fixa** · sem-abrigo · pode votar na mesa mais próxima do último endereço · ou pedir transferência
- **Diáspora · 4,7 M moçambicanos no estrangeiro** · embaixadas como mesas · voto antecipado de 7 dias
- **Detidos preventivos** (não condenados) · direito ao voto preservado · mesa móvel
- **Pessoas com deficiência visual** · boletim em braille · acompanhante registado
- **Falsificação de identidade** · cross-eBI biométrico bloqueia em 2 segundos
- **Voto duplicado tentado** · sistema bloqueia em 2.ª mesa antes do boletim ser entregue
- **Mesa em zona de conflito armado** · cooperação MININT · mesas alternativas seguras
- **Cidadão mudou morada · não actualizou** · pode votar mesa antiga ou pedir transferência
- **Maputo vs rural** · UI degrada graciosamente · funciona em SMS-only
- **Resultados contestados** · TES decide · transparência preserva confiança
- **Cidadão que recusa estar no caderno** · direito de objecção de consciência · raro mas existe

---

## 10. Open questions

- **Voto electrónico real (urnas digitais)?** · NÃO · papel é o pilar de confiança · digital só rodeia
- **Idade mínima 16?** · debate aberto noutros países · MZ mantém 18 · pode ser revisto
- **Voto obrigatório?** · MZ é facultativo · sistema permite ambos sem alteração
- **Anonimato do boletim** · sempre · NUEL nunca liga a boletim físico específico
- **Auditoria forense pós-eleitoral** · TES + OCI · processo definido
- **Manipulação algorítmica** · todos os algoritmos publicados · open source · cross-Sociedade Aberta

---

## 11. Filosofia de fim de série

Este é o 12.º e último pacote. Foi escolhido para fechar porque:

1. **Toca todos os 11 anteriores** · Vida Civil (auto-inscrição), Terras (endereço), eBI (identidade), Sociedade Aberta (transparência), Resiliência (contingência), Justiça (TES), e todos os outros directa ou indirectamente
2. **Tem coerência cívica fundamental** · votar é o acto cidadão por excelência
3. **Permite mostrar processo completo** · entre eleições + dia eleitoral + pós-eleitoral
4. **Honra Pedro · primeira persona nova desde Vida Civil** · simboliza nova geração que herda o sistema

Se houver continuação, fica em aberto · mas Eleições Digitais era o lugar natural para parar.

---

## 12. Princípio final

> "Onze pacotes construíram o sistema. O 12.º entrega-o nas mãos do cidadão · que vota com ele."
