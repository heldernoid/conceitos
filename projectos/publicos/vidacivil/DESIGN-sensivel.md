# DESIGN-sensivel.md — Surface Acto sensível · supervisão judicial

**Status:** v0.3 · Abril 2026
**Surface:** 6 de 6 · **a peça mais delicada do pacote**
**Persona:** Adelaide Cossa → Beatriz Cossa (mudança de nome)

---

## 1. Propósito

Algumas mudanças identitárias merecem cuidado especial. Esta surface é dedicada a esses momentos com:

- **Privacidade reforçada** · nome anterior redacted por defeito
- **Supervisão judicial obrigatória** · TJ Provincial avalia
- **Tom diferente** · sem KPIs, sem urgência, sem perguntas intrusivas
- **Sem julgamento moral** · app não pergunta "porquê"
- **Linguagem cuidadosa** · pessoa não é "processo"

Cobre: mudança de primeiro nome ou apelidos · mudança de marcador de género · recuperação de nome de origem · pessoas em programa de protecção.

---

## 2. Princípios

### 2.1 Tom respeitoso é arquitectura
Não é decoração. Cada decisão de design existe para acolher · headlines maiores, linguagem em primeira pessoa, ausência de barras de progresso, "tem o tempo que precisar". A surface inteira respira diferente.

### 2.2 Sem "porquê"
A app não pede justificação. O direito a alterar o nome é constitucional (Constituição art. 41 · "todo o cidadão tem direito ao bom nome e reputação"). Cabe ao Tribunal verificar livre vontade e ausência de fraude · não validar a "razão correcta".

### 2.3 Supervisão judicial · garantia, não obstáculo
TJ Provincial · 90 dias · advogado oficioso gratuito (cross-INADJ). Não é obstáculo · é garantia de que decisão é livre, esclarecida, e que terceiros (cônjuge, filhos) são protegidos.

### 2.4 Privacidade configurável em 5 níveis
Após sentença · pessoa decide quem sabe que mudou de nome. Do "Confidencial total" (nem família) até "Transparência total" (público em Sociedade Aberta). Pode mudar nível a qualquer altura.

### 2.5 Cross-system silencioso
Propaga sem broadcast a familiares ou empregadores · pessoa decide quando e como comunicar. Nome anterior redacted no arquivo público.

### 2.6 Sentença respeita
O `.assento.nome` mostra o nome anterior como `─ ─ ─ ─ ─ ─ ─ ─` (redacted bar visual). Linguagem · "a pessoa portadora do BI número X" não "Adelaide Cossa".

---

## 3. Cenas (7)

| # | Cena | Componente |
|---|---|---|
| 1 | Princípios · 4 cards explicativos | Cards numerados + sidebar com casos |
| 2 | Adelaide inicia pedido · interface serena | Form sem KPIs · serif dominante |
| 3 | Supervisão judicial · TJP · 90 dias | Timeline + magistrada + pareceres |
| 4 | Sentença + averbamento | `.assento.nome` com redacted bar |
| 5 | Privacidade · 5 níveis | Lista de níveis · escolha actual destacada |
| 6 | Edge cases · 6 cenários | Cards · género, proteção, recuperação |
| 7 | Direitos garantidos | 8 cards de direitos constitucionais + ensaio final |

---

## 4. Componentes signature

- `.assento.nome` (Cena 4) — única do pacote · com redacted bar visual
- Hero ink-marinho com headline em serif xl (Cena 1, 4)
- 5 níveis de privacidade lado-a-lado (Cena 5) — peça pedagógica única
- Cards com border-left brass/livro (Cena 7)

---

## 5. Mecanismo de redacted

Visual · `<span style="background:var(--ink-marinho);color:var(--ink-marinho);user-select:none">─ ─ ─ ─ ─ ─</span>`

Comportamento:
- Por defeito · nome anterior invisível mesmo a quem tem acesso ao arquivo
- Despacho judicial fundamentado · pode revelar em casos específicos (fraude, crime grave)
- Pessoa nunca pode reverter completamente o nome anterior · mas pode iniciar nova mudança

---

## 6. Cross-system

`cross-DNRN` (averbamento), `cross-DIC` (novo BI 5d), `cross-TJ Provincial`, `cross-PGR` (parecer), `cross-CNPDP` (privacidade), `cross-INADJ` (advogado oficioso), `cross-CFJP` (régulo em recuperação de nome de origem), `cross-AT`, `cross-Saúde`, `cross-Eleições`, `cross-Trabalho`, `cross-Sociedade Aberta` (configurável).

---

## 7. Edge cases (cenários cobertos · Cena 6)

- **Mudança de marcador de género** (F ↔ M ou X) · Lei moçambicana é silenciosa · processo por analogia · não exige cirurgia/hormonas/laudo
- **Pessoa em programa de protecção** (vítima violência doméstica, testemunha) · processo expedito 30 dias · cross-PGR + cross-MININT · agressor não notificado
- **Recuperação de nome de origem** (Macua, Changana, Sena vs nome português colonial) · antropólogo UEM acompanha · régulo confirma autenticidade
- **Correção de erro grafia** · processo administrativo simplificado · 30 dias · gratuito · sem TJ
- **Pós-divórcio · retorno ao nome de solteira** · processo administrativo · 14 dias · gratuito
- **Menores de idade** · pais conjuntamente · &gt;14a menor é ouvido · só por motivo grave · Tribunal de Família

---

## 8. Direitos garantidos (Cena 7)

- **Constituição art. 41** · direito ao bom nome
- **Constituição art. 35** · igualdade perante a lei
- **D.L. 60/2018** · processo gratuito
- **90 dias** · prazo legal · prorrogável uma vez 30d
- **Privacidade** · cross-CNPDP audita
- **Recurso** · TS, TC, CADHP
- **Sem julgamento moral** · só fraude/identidade alheia/evasão
- **Mudança contínua** · sem limite

---

## 9. Persona

**Adelaide Cossa → Beatriz Cossa** · 32 anos, professora em Inhambane.

Razão da mudança · não declarada (princípio 2.2). Persona deliberadamente ambígua — pode ser:
- Pessoa que quer simplesmente um nome diferente
- Pessoa que retoma nome de família tradicional
- Pessoa em transição de género que escolhe novo nome compatível
- Vítima que quer apagar associação ao agressor

A surface trata todas as razões com igual respeito · esse é o ponto.

---

## 10. Por que esta surface é a última do pacote

Cena 7 explicita: "Os actos vitais começam onde acontecem · mas alguns acontecem dentro da pessoa · e merecem o cuidado redobrado de uma surface inteira só para eles."

Esta surface é a peça do pacote onde mais se mostra a diferença entre **"o sistema permite"** e **"o sistema acolhe"**. Cada decisão de design — ausência de KPIs, recurso constante a Plex Serif, banner ink em vez de banner livro, supervisão judicial visível — existe para que pessoas como Beatriz encontrem aqui não obstáculo, mas instrumento.
