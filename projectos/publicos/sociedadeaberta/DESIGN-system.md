# DESIGN-system.md — Sociedade Aberta · Directório Público

**Status:** v0.3 · Abril 2026
**Pacote:** 9.º da família Conceitos
**Domínio:** transparência fiscal e patrimonial, ao estilo escandinavo

---

## 1. Premissa

Toda declaração fiscal é pública por defeito. Qualquer cidadão pode pesquisar qualquer outro pelo nome ou NUIT. Em troca, **o titular sempre vê quem o consultou** — auditoria recíproca, identidade do consultor sempre visível, anomalias sinalizadas.

A questão não é se isto é tecnicamente possível (é trivial). A questão é se Moçambique decide que o interesse público supera a privacidade fiscal individual quando se trata de:

- Pessoas que recebem do erário (políticos, magistrados, gestores públicos, pensionistas)
- Empresas que ganham contratos públicos
- DUATs concedidos pelo Estado
- Subsídios e isenções fiscais

A Suécia decidiu isto em 1766. A Noruega em 1814. A Finlândia tem o "Tax Day" no 1.º de Novembro — toda a imprensa publica os rendimentos das pessoas mais pagas. A Estónia digitalizou tudo isto com X-Road. **Não é experimento — é tradição liberal centenária.**

---

## 2. Lei moçambicana de inspiração

| Lei | Conteúdo | Como o pacote a estende |
| --- | --- | --- |
| Lei 16/2012 | Declaração de bens de funcionários públicos | Torna pública por defeito, não só consultável por petição |
| Lei 10/2017 | Direito à informação | Operacionaliza o direito · interface de pesquisa |
| Lei 7/2014 | Probidade pública | Mecanismo activo de detecção de discrepâncias |
| Lei 14/2018 | Combate ao branqueamento | Cadeia de propriedade pública · Cena Empresa |
| Lei 5/2002 | Tributário · IRPS | Reforma · publicação automática |
| Lei 22/2018 | Protecção de dados pessoais | Define os limites: menores, vítimas, testemunhas |
| Constituição art. 41 e 48 | Privacidade vs informação interesse público | Conflito que o pacote resolve por simetria |

---

## 3. Paleta · jornal-investigativo

A escolha visual sinaliza o género: isto não é UI corporativa cinzenta. É **jornal sério, com edge investigativo.**

### Núcleo
- **Ink-noir** `#0E0F11` — preto profundo · headlines, cabeçalhos, navegação activa
- **Papel envelhecido** `#FCFAF5` → `#E8E2D2` — fundo principal, simula papel-jornal
- **Redaction-red** `#C73E2E` → `#5C1B14` — destaque investigativo, sublinhado, alertas

### Suporte
- **Ledger-grey** — escala neutra para tabelas e dados
- **Good (verde escuro)** `#5A7C42` → confirmações, verificado
- **Cobalto** — referências cruzadas neutras (não-alarme)
- **Brass** `#8C6F32` — selos oficiais (CCEP, CIP)

### Tipografia
- **IBM Plex Serif** — headlines, fichas, citações (peso jornal)
- **IBM Plex Sans** — UI corpo
- **IBM Plex Mono** — dados, NUITs, timestamps, overlines

---

## 4. Componentes signature (6)

### 4.1 `.ficha` — cartão de pessoa ou entidade
Marca o registo. 3 variantes: cidadão (preto), pessoa pública (vermelho), empresa (cobalto). Sempre tem `ficha-tag` no topo identificando o tipo.

### 4.2 `.ledger-row` — linha de declaração fiscal
Estilo livro-razão. 4 colunas: ano, descrição, valor, percentagem. Variante `.flag` em vermelho para entradas anómalas.

### 4.3 `.consult-log` — auditoria recíproca
**O componente moralmente central do pacote.** Cabeçalho preto com "QUEM VIU ESTA FICHA". Cada linha mostra: timestamp, identidade do consultor, tipo (cidadão/jornalista/AT/banco/PGR/CIP), profundidade da consulta. Variante `.flag` para padrões anómalos (consultas repetidas pelo mesmo IP, p.ex.).

### 4.4 `.net-card` — grafo de propriedade
Cadeia accionista de uma empresa, mostra beneficiário efectivo. Nodos por tipo: pessoa (vermelho), empresa (cobalto), contrato (brass).

### 4.5 `.disc-card` — alerta de discrepância patrimonial
Compara duas figuras (ex: rendimento declarado vs património aparente) e calcula rácio. Vermelho-redaction.

### 4.6 `.pull-quote` — citação serif estilo jornal
Linha vertical vermelha à esquerda. Cita atribuída em mono-uppercase abaixo.

---

## 5. Categorias de consultor (6 tipos)

A peça-chave da auditoria recíproca: **cada consulta é classificada e visível ao titular.**

| Tipo | Cor visual | Identidade revelada? | Justificação obrigatória? |
| --- | --- | --- | --- |
| Cidadão particular | cinzento | sim, sempre | não |
| Jornalista credenciado | vermelho | sim, com credencial INC | breve, livre |
| Banco em due-diligence | cobalto | sim, NUEL banco | sim · contexto crédito |
| Autoridade Tributária | preto | sim, com mandato | sim · ID processo AT |
| Procuradoria-Geral / PRM | brass | sim, com despacho | sim · ID inquérito |
| CIP / CCEP | verde | sim | não · mandato legal |

Padrões anómalos disparam flag automática:
- Mesmo IP consulta &gt; 50 fichas em 1h → bloqueio
- Mesmo consultor visita ficha &gt; 14 vezes em 30 dias → flag
- Consulta seguida de actualização não-relacionada → registo

---

## 6. Limites legais que o pacote respeita

**Nunca aparecem no directório:**
- Menores de 18 (zero excepções)
- Vítimas de crime em programa de protecção (cross-PRM)
- Testemunhas em programa de protecção (cross-PGR)
- Saúde, religião, orientação sexual, filiação política
- Vítimas de violência doméstica (cross-GAVMV)

**Aparece com restrições:**
- Recém-falecidos &lt; 60 dias (proteger luto familiar)
- Pessoas com declaração de incapacidade (cross-Justiça)
- Estrangeiros sem residência permanente (só fração pública)

---

## 7. Personas convencionadas

Para evitar nomes reais de figuras políticas (instrução directa do briefing), todas as personas são fictícias e geograficamente coerentes:

| Pessoa | Papel | Detalhe |
| --- | --- | --- |
| **Felisberto Manjate** | Cidadão protagonista | Continuidade Terras Digitais · BI 110100442918 |
| **Joana Mahique Cossa** | Jornalista do Savana | Credenciada INC · investiga discrepâncias |
| **Eng. Augusto Nhantumbo** | Pessoa pública fictícia | Director-Geral de Empresa Pública (fictícia) "Portos & Caminhos de Ferro Norte SA" |
| **Dra. Cremilda Sitole** | Pessoa pública fictícia | Magistrada Tribunal Administrativo Provincial Sofala |
| **Manuel Tembe Sumane** | Pessoa pública fictícia | Antigo Governador Provincial (província não especificada) |
| **MTS Investments Lda** | Empresa-fachada fictícia | NUEL E-2019-MAP-014218 · cadeia de propriedade |
| **Costa Norte Logística SA** | Empresa fictícia | Contratos públicos · NUEL E-2017-NPL-008412 |

Nenhuma destas personas mapeia a figuras políticas reais. Os nomes são compostos genéricos consistentes com onomástica moçambicana.

---

## 8. Cross-system

Esta superfície depende de mais pacotes do que qualquer outra da família:

| Cross-tag | Pacote | O que provê |
| --- | --- | --- |
| `cross-AT` | Finanças Digitais | Declaração IRPS, IRPC |
| `cross-NUIT` | Finanças Digitais | Identidade fiscal |
| `cross-NUEL` | Finanças Digitais | Pessoas colectivas |
| `cross-eBI` | Governo Digital | Identidade civil |
| `cross-Terras` | Terras Digitais | DUATs detidos |
| `cross-NUSS` | Trabalho Digital | Salários declarados |
| `cross-CFJP` | Justiça Digital | Sentenças, condenações |
| `cross-PGR` | Justiça Digital | Inquéritos abertos |
| `cross-CIP` | Sociedade Aberta (este) | Centro de Integridade Pública |
| `cross-CCEP` | Sociedade Aberta (este) | Comissão Central de Ética |
| `cross-CNPDP` | Sociedade Aberta (este) | Protecção de dados |
| `cross-INSS` | Trabalho Digital | Pensões públicas |
| `cross-INC` | Imprensa (futuro) | Credencial jornalistas |
| `cross-Bo Moçambique` | Finanças Digitais | Transferências bancárias declaradas |

---

## 9. Open questions

- **Funcionários do Estado de baixo escalão** entram? O sistema sueco inclui todos. Sugestão: incluir, mas acima de salário-base do Estado (~ 12 k MT/mês), com flag "funcionário público".
- **Diáspora** com rendimentos no estrangeiro: declaração obrigatória, mas como verificar? Acordo bilateral SADC.
- **Isenção tributária por baixo rendimento** (&lt; 21 250 MT/mês IRPS isento) — entram com "isento" ou ficam fora? Argumento sueco: incluem-se, pelo princípio.
- **Pensão de reforma** dos magistrados — pública por serem cargos públicos transitados?
- **Redacção em casos sensíveis** — quando uma vítima de violência aparece no NUIT do agressor (declaração conjunta), como redactar sem trair o NUIT do agressor?
