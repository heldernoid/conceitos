# DESIGN-titular.md — Surface Titular · auditoria recíproca

**Status:** v0.3 · Abril 2026
**Surface:** 5 de 5 · **coração ético do pacote**
**Persona:** Felisberto Manjate · qualquer cidadão na sua relação consigo próprio

---

## 1. Propósito

A surface que torna o sistema constitucionalmente defensável. Sem ela, este pacote seria vigilantismo unilateral. Com ela, é cidadania simétrica.

Cobre tudo o que o titular pode fazer com a sua própria ficha:

- Ver o que outros vêem dele (mesma view do Surface 1)
- Ver quem o consultou (auditoria recíproca completa)
- Ver detalhe técnico de cada consulta
- Pedir explicação a qualquer consultor
- Reclamar erros factuais à CNPDP
- Exercer direito a réplica (Lei 22/2018 art. 14)
- Configurar alertas e exportar dados
- Compreender o que pode e não pode controlar

---

## 2. Princípios

### 2.1 Simetria absoluta
Tudo o que outros vêem do titular, o titular vê de quem o consultou. Profundidade idêntica · 26 minutos de consulta da Joana correspondem a 26 minutos visíveis ao Felisberto. Identidade, IP, hash, exportações.

### 2.2 Direito sem custo
Reclamações, pedidos de explicação, exportações, exercício de réplica · todos gratuitos. CNPDP funciona como autoridade administrativa independente, financiada por orçamento de Estado.

### 2.3 Acção, não apenas observação
O titular não é espectador passivo da sua transparência. Tem ferramentas activas: pedir explicação, reclamar, replicar, exportar, reportar abuso. A surface é desenhada para encorajar uso destas ferramentas.

### 2.4 Limites claros · educativos
Cena 7 explicita o que o titular pode E não pode controlar. A não-controlabilidade da publicidade fiscal é o contrato social do sistema · explicar o limite é proteger o sistema da tentação de privilégio.

### 2.5 Réplica vs Reclamação
Distinção pedagógica importante. Reclamação corrige factos. Réplica adiciona contexto. Sistema apresenta a diferença visualmente em Cena 6 com cards lado-a-lado.

---

## 3. Cenas (7)

| # | Cena | Componente principal |
|---|---|---|
| 1 | Painel pessoal | Hero ink+red gradient · 4 KPIs · ficha + direitos lado-a-lado |
| 2 | Quem me viu · 30 dias | `.consult-log` extenso · 14 entradas · 1 com flag |
| 3 | Detalhe de consulta · Joana | Ficha do consultor + lista do que viu + sessão técnica · acções na coluna lateral |
| 4 | Pedir explicação | Form com mensagem pré-preenchida · banner ink explicando processo |
| 5 | Reclamar erro factual | Form com versão actual (vermelho) e versão proposta · 3 anexos PDF |
| 6 | Direito a réplica | Cards reclamação vs réplica · exemplo público da réplica do Eng. Nhantumbo |
| 7 | Configurações · controlo | 2 cards lado-a-lado: "posso configurar ✓" e "NÃO posso ✗" · 3 colunas direitos |

---

## 4. Componentes signature

- Hero gradient `var(--ink-noir)` → `var(--red-900)` em Cena 1 (único do pacote)
- `.consult-log` ampliado em Cena 2 com mais detalhe por linha
- Comparison cards (background tinted) em Cena 6 explicando reclamação/réplica
- Tabela de direitos vs limites em Cena 7 — pedagógica

---

## 5. Limites do sistema (Cena 7)

**O que o titular pode configurar ✓**
- Alertas SMS quando consultado
- Email semanal com resumo
- Exportar dados (qualquer altura, qualquer formato)
- Bloquear consultor específico (raro, com fundamentação CNPDP)
- Idioma e acessibilidade

**O que o titular NÃO pode controlar ✗**
- Tornar ficha privada (não há opt-out)
- Esconder rendimento de quem consulta
- Esconder DUATs detidos
- Apagar histórico de quem o viu
- Decidir quem pode consultar
- Limitar profundidade de consulta

A não-controlabilidade é o contrato social do sistema.

---

## 6. Cross-system

`cross-CNPDP` (autoridade reguladora central) · `cross-AT` (correcções IRPS) · `cross-eBI` (sessão segura) · `cross-Tribunal Administrativo` (recurso) · `cross-Tribunal Constitucional` (contra a Lei) · `cross-Comissão Africana de DH` (última instância)

---

## 7. Tipos de mensagens entre titular e consultor

| Mensagem | Iniciada por | Resposta obrigatória? | Visibilidade |
|---|---|---|---|
| Pedido de explicação | Titular | Não · ausência fica registada | Privada · 30 dias |
| Resposta à explicação | Consultor | — | Privada · entre os dois |
| Pedido de cessação | Titular | Sim · em 14 dias | Privada |
| Reclamação CNPDP | Titular | Sim · CNPDP responde | Pública (caso decidido) |
| Réplica formal | Titular | — (não exige resposta) | Pública · anexa à ficha |

---

## 8. Edge cases

- **Titular menor de idade** → não tem ficha (limites legais), portanto esta surface não se aplica
- **Titular falecido** → ficha mantém-se 60 dias (luto), depois transita para arquivo histórico, herdeiros podem aceder via representação
- **Titular em programa de protecção** → ficha invisível, esta surface mostra zero consultas (porque não há)
- **Titular contesta CNPDP** → recurso para Tribunal Administrativo · em 30 dias · sem custo
- **Titular contesta a própria Lei** → cidadão pode propor inconstitucionalidade ao TC (poucos legitimados, mas é direito)
- **Sessão eBI roubada** → todas as consultas suspeitas são reversíveis · CNPDP investiga em 7 dias

---

## 9. O contrato social explícito

A última banner da Cena 7 sintetiza o pacote inteiro:

> "Felisberto, este é o teu contrato social. Aceitas que outros saibam o teu rendimento e DUATs em troca de saberes o mesmo de outros — incluindo de quem decide e adjudica em teu nome. A simetria é o que torna isto justo. Este pacote inteiro é a tradução técnica desse contrato."

Esta frase é o "nascedouro" do pacote. Aparece também explicitamente noutras surfaces como reforço.

---

## 10. Persona

Felisberto Manjate · 38 anos · Inhambane · empregado sector privado · BI 110100442918 · NUIT 100 218 421 · 2 DUATs · sem antecedentes · cidadão modelo do sistema. Continuidade desde Terras Digitais (8.º pacote) e Cidadão (Surface 1).
