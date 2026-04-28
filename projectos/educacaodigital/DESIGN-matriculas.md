# DESIGN-matriculas.md — Surface 5 · Portal de Matrículas

**Status:** v0.3 · Abril 2026
**Form factor:** Public web. Desktop floor 1024 px; full responsive down to 360 px. Heavy mobile use expected — encarregados em telemóveis na rua.
**Primary users:** Encarregados de educação (parents/guardians) com filhos a entrar para a 1.ª classe ou a transitar entre ciclos. Secondary: directores escolares (recebem candidaturas), DPEDH (override em sobrelotação).
**Setting:** Campanha anual, geralmente Setembro–Outubro. Pico de tráfego concentrado em duas semanas.

---

## 1. Product purpose

The Portal de Matrículas substitutes the **fila à porta da escola** — the line at dawn that families have queued in for decades to register their children. Three priorities:

1. **Inscrição sem ir à escola.** O encarregado autentica-se com BI (eBI), preenche dados do aluno, escolhe até 3 escolas por preferência, submete.
2. **Atribuição transparente.** O algoritmo é público: ordem de preferência → irmão na escola → proximidade geográfica → ano de nascimento → ordem de submissão. Cada candidato vê *porque* foi colocado onde foi.
3. **Recurso real.** Se a atribuição é injusta, o recurso é submetido na App, decidido pela DPEDH, com prazo definido (10 dias úteis).

What it deliberately is *not*:
- Not a privatization vehicle. The portal trabalha com escolas oficiais e privadas registadas no SNE.
- Not a "school marketplace". As escolas não competem por candidatos — são distribuídas conforme o algoritmo.
- Not a chat com directores. Comunicação é mediada pela DPEDH.

---

## 2. Information architecture

```
Hero (estado da campanha)
├─ Procurar escola
└─ Iniciar candidatura

Procurar escola
├─ Mapa por distrito · classe · turno
├─ Lista por proximidade
└─ Detalhe da escola
   ├─ Vagas por classe
   ├─ Frequência média (do SIGE)
   ├─ Distância da residência
   └─ Adicionar à candidatura

Candidatura (wizard 5 passos)
├─ 1 · Encarregado (BI eBI · OTP)
├─ 2 · Aluno (BI/cédula · dados)
├─ 3 · Escolha de escolas (até 3 por preferência)
├─ 4 · Necessidades especiais (saúde, língua, irmãos)
└─ 5 · Confirmação (resumo + assinatura digital)

Minhas candidaturas
├─ Por aluno
├─ Estado (em análise · atribuída · lista de espera · recurso)
└─ Confirmação final / aceitação

Atribuição
├─ Vista do resultado
├─ Justificação algorítmica (por que esta escola)
└─ Recurso (se injusta)

Sobre
├─ Como funciona o algoritmo
├─ Calendário da campanha
└─ Contactos DPEDH
```

---

## 3. Critical flows

### F1 — Estado da campanha (hero)
Topo da página comunica: campanha aberta / fechada, dias restantes, total de vagas, total de candidaturas até agora. Cidadania transparente: o número não está escondido.

### F2 — Procurar escola
Filtros: distrito · classe · turno. Vista mapa (escolas próximas) + lista por proximidade. Cada escola mostra vagas disponíveis (lido do SIGE em tempo real).

### F3 — Detalhe da escola
Para cada escola: nome, distrito, vagas por classe (com gráfico de barras), frequência média (do SIGE), distância à residência (calculada se BI tem morada), classes disponíveis, turnos. Botão "Adicionar à candidatura".

### F4 — Candidatura (wizard 5 passos)
**Passo 1 — Encarregado.** BI lookup via eBI (Governo Digital). OTP. Confirmação dos dados.

**Passo 2 — Aluno.** Cédula ou BI do aluno. Dados pré-preenchidos do registo civil.

**Passo 3 — Escolha de escolas.** Até 3 escolas, ordenadas por preferência. Sistema mostra: vagas em cada, distância, frequência média.

**Passo 4 — Necessidades especiais.** Irmão na escola? (boost no algoritmo). Necessidades de saúde declaráveis (asma, diabetes, mobilidade reduzida). Língua materna não-portuguesa.

**Passo 5 — Confirmação.** Resumo. Assinatura digital (OTP do encarregado). Submissão.

### F5 — Atribuição transparente
Quando a atribuição é feita (data fixa: 25 Out), o encarregado vê:
- A escola atribuída
- O ranking onde ficou em cada escola candidatada
- A justificação ("foi colocado na 1.ª preferência porque havia vagas e tem irmão na escola")

Se ficou em lista de espera, vê a posição.

### F6 — Recurso
Se a atribuição é injusta (algoritmo aplicado mal, dados errados, etc.), submeter recurso. Vai à DPEDH provincial, decisão em 10 dias úteis.

### F7 — Confirmação final
Atribuída a escola, o encarregado tem 7 dias para **confirmar a aceitação**. Se não confirmar, a vaga liberta-se para a lista de espera. Confirmação requer OTP.

### F8 — Sobre o algoritmo
Página pública e simples explicando como o algoritmo funciona. Pseudo-código legível. Não-técnica em primeira leitura, técnica em segunda.

---

## 4. Components & patterns

| Component | Matrículas |
|---|---|
| Hero | Indigo, com counter de campanha |
| School card | Vagas (bar), distance, attendance |
| Wizard | 5-step stepper sticky |
| Algorithmic explainer | Stepper visual com cada critério |
| Confirmation modal | OTP + checkbox + botão consequência-nomeada |

---

## 5. Critical UI states

### 5.1 Campanha fechada
*"Campanha 2027 fecha a 18 de Outubro de 2026."* Após fecho, o portal mostra calendário do ciclo seguinte e abre canal "Casos especiais".

### 5.2 Sem vagas em todas as preferências
Banner âmbar: *"Nenhuma das 3 escolas escolhidas tem vagas. Será automaticamente colocado em lista de espera. Vamos sugerir 3 escolas com vagas próximas."*

### 5.3 Recurso pendente
Banner indigo: *"Recurso em análise pela DPEDH Cidade de Maputo. Resposta esperada até 5 Nov 2026."*

### 5.4 BI inválido / não encontrado
Erro claro: *"Não encontrámos este BI no eBI. Verifique o número ou registe o BI no balcão da Conservatória mais próxima."*

### 5.5 Aluno já matriculado
*"Este aluno já está matriculado na Esc. Sec. da Polana, 8.ª A. Para mudar de escola, use Transferência (não Matrícula)."*

---

## 6. Voice & tone

- **Cívico, não comercial.** Sem "Reserve já a sua vaga!", sem countdowns dramáticos.
- **Específico.** Sempre nomeia a campanha, a classe, a escola, o distrito.
- **Honesto sobre incerteza.** Se há sobrelotação numa zona, é dito; não se promete vagas que não existem.
- **PT-MZ.** "Matrícula" não "inscrição".

---

## 7. Algoritmo de atribuição (público)

```
para cada candidatura C:
  para cada escola E em preferências de C (até 3):
    se E tem vagas na classe pedida:
      pontuação = 0
      pontuação += 1000 × (4 − ordem_preferência)   # preferência 1 vale 3000
      pontuação +=  500 se C tem irmão matriculado em E
      pontuação +=  300 × (1 − distância_normalizada)
      pontuação +=  100 se C nasceu nesse distrito
      pontuação +=  ponto_aleatório [0..50]          # tie-breaker
      ordenar candidatos de E por pontuação descendente
      atribuir as primeiras N vagas
```

Resultado público anonimizado: distribuição final de pontuações por escola, número de candidatos por classe, taxa de atribuição em 1.ª preferência. Sem nomes de candidatos, sem BIs.

---

## 8. Cross-system relationship

Matrículas lê de:
- **eBI** — identidade do encarregado e do aluno
- **SIGE** — vagas, frequência, distância
- **Saúde Moçambique** — flags de necessidades especiais (com consentimento)

Matrículas escreve a:
- **SIGE** — após confirmação, cria registo de matrícula na escola atribuída
- **Caderno do Aluno** — onboarding pós-matrícula
- **DPEDH** — recursos pendentes

---

## 9. Open questions for v0.4

- Suporte a candidaturas em bloco (ex.: vários alunos transferidos colectivamente após calamidade)
- USSD para consulta de estado em zonas rurais sem internet
- Inscrição em escolas privadas (parceria de fluxo)
- Língua de portal — Bantu language toggle

---

*Authoritative for the Portal de Matrículas surface. DESIGN-system.md wins on conflict.*
